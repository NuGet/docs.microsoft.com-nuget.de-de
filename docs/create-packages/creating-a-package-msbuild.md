---
title: Erstellen eines NuGet-Pakets mit MSBuild
description: Eine ausführliche Anleitung zum Entwerfen und Erstellen eines NuGet-Pakets mittels MSBuild, einschließlich der wichtigsten Entscheidungspunkte wie Dateien und Versionsverwaltung.
author: JonDouglas
ms.author: jodou
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 18e0da335f65fde99d035388b95f35160757ee84
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901459"
---
# <a name="create-a-nuget-package-using-msbuild"></a>Erstellen eines NuGet-Pakets mit MSBuild

Wenn Sie ein NuGet-Paket aus Ihrem Code erstellen, verpacken Sie diese Funktionalität in eine Komponente, die mit einer beliebigen Anzahl anderer Entwickler geteilt und von diesen verwendet werden kann. In diesem Artikel wird das Erstellen eines Pakets mithilfe von MSBuild beschrieben. MSBuild wird mit allen Visual Studio-Workloads vorinstalliert, die NuGet enthalten. Zusätzlich können Sie MSBuild auch über die dotnet-CLI mit [dotnet msbuild](/dotnet/core/tools/dotnet-msbuild) verwenden.

Für .NET Core- und .NET Standard-Projekte, die das [SDK-Format](../resources/check-project-format.md) verwenden, und für alle anderen Projekte im SDK-Format verwendet NuGet Informationen in der Projektdatei direkt zum Erstellen eines Pakets.  Für ein Projekt im Nicht-SDK-Stil, das `<PackageReference>` verwendet, verwendet NuGet auch die Projektdatei, um ein Paket zu erstellen.

Für Projekte im SDK-Stil ist die Packfunktionalität standardmäßig verfügbar. Für PackageReference-Projekte, die nicht im SDK-Stil erstellt werden, müssen Sie den Projektabhängigkeiten das Paket NuGet.Build.Tasks.Pack hinzufügen. Ausführliche Informationen zu MSBuild-Packzielen finden Sie unter [NuGet-Befehle „pack“ und „restore“ als MSBuild-Ziele](../reference/msbuild-targets.md).

Der Befehl, mit dem ein Paket erstellt wird (`msbuild -t:pack`), ist funktional äquivalent mit `dotnet pack`.

> [!IMPORTANT]
> Dieses Thema gilt für Projekte im [SDK-Stil](../resources/check-project-format.md), in der Regel .NET Core- und .NET Standard-Projekte, und für Projekte im Nicht-SDK-Stil, die PackageReference verwenden.

## <a name="set-properties"></a>Eigenschaften festlegen

Die folgenden Eigenschaften sind für die Erstellung eines Pakets erforderlich.

- `PackageId`, der Paketbezeichner. Dieser muss im Katalog, der das Paket hostet, eindeutig sein. Wenn Sie hier nichts angeben, lautet der Standardwert `AssemblyName`.
- `Version`, eine bestimmte Versionsnummer in der Schreibweise *Hauptversion.Nebenversion.Patch[-Suffix]* , wobei im *-Suffix* die [Vorabversionen](prerelease-packages.md) angegeben werden. Wenn Sie hier nichts angeben, lautet der Standardwert 1.0.0.
- Der Titel des Pakets, so wie er auf dem Host (z.B. „nuget.org“) angezeigt werden sollte
- `Authors`, Informationen zum Autor und Besitzer. Wenn Sie hier nichts angeben, lautet der Standardwert `AssemblyName`.
- `Company`, der Firmenname. Wenn Sie hier nichts angeben, lautet der Standardwert `AssemblyName`.

Wenn Sie Nicht-SDK-Projekte packen, die PackageReference verwenden, ist außerdem Folgendes erforderlich:

- `PackageOutputPath`, der Ausgabeordner für das Paket, das beim Paketaufruf generiert wird.

In Visual Studio können Sie diese Werte in den Projekteigenschaften festlegen (Rechtsklick auf das Projekt im Projektmappen-Explorer, wählen Sie **Eigenschaften** und dann die Registerkarte **Paket** aus). Sie können diese Eigenschaften auch direkt in den Projektdateien festlegen (*.csproj*).

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Weisen Sie dem Paket einen Bezeichner zu, der auf nuget.org bzw. in der Paketquelle, den Sie verwenden, einzigartig ist.

Das folgende Beispiel zeigt eine einfache, vollständige Projektdatei, in der diese Eigenschaften enthalten sind.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

Sie können auch die optionalen Eigenschaften wie `Title`, `PackageDescription` und `PackageTags` festlegen, wie in [MSBuild-Paketziele](../reference/msbuild-targets.md#pack-target), [Steuern von Abhängigkeitsobjekten](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) und [NuGet-Metadateneigenschaften](/dotnet/core/tools/csproj#nuget-metadata-properties) beschrieben.

> [!NOTE]
> Bei Paketen für die öffentliche Nutzung sollten Sie besonders auf die **PackageTags**-Eigenschaft achten, da Tags anderen dabei helfen, Ihr Paket zu finden und dessen Funktion zu verstehen.

Weitere Informationen zum Deklarieren von Abhängigkeiten und zum Angeben von Versionsnummern finden Sie unter [Paketverweise in Projektdateien](../consume-packages/package-references-in-project-files.md) und [Paketversionsverwaltung](../concepts/package-versioning.md). Es ist auch möglich, Ressourcen aus Abhängigkeiten mithilfe der Attribute `<IncludeAssets>` und `<ExcludeAssets>` direkt im Paket verfügbar zu machen. Weitere Informationen finden Sie unter [Steuern von Abhängigkeitsobjekten](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="add-an-optional-description-field"></a>Hinzufügen eines optionalen Beschreibungsfelds

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Auswählen eines eindeutigen Paketbezeichners und Festlegen der Versionsnummer

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a>Hinzufügen des Pakets NuGet.Build.Tasks.Pack

Wenn Sie MSBuild mit einem Projekt im Nicht-SDK-Stil und PackageReference verwenden, fügen Sie Ihrem Projekt das Paket NuGet.Build.Tasks.Pack hinzu.

1. Öffnen Sie die Projektdatei, und fügen Sie Folgendes hinter dem `<PropertyGroup>`-Element hinzu:

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. Öffnen Sie eine Developer-Eingabeaufforderung (geben Sie **Developer-Eingabeaufforderung** im **Suchfeld** ein).

   In der Regel sollten Sie die „Developer-Eingabeaufforderung für Visual Studio“ über das **Startmenü** starten, da dieses mit allen nötigen Pfaden für MSBuild konfiguriert ist.

3. Wechseln Sie zu dem Ordner, der die Projektdatei enthält, und geben Sie den folgenden Befehl ein, um das Paket NuGet.Build.Tasks.Pack zu installieren.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   Stellen Sie sicher, dass die MSBuild-Ausgabe angibt, dass der Build erfolgreich abgeschlossen wurde.

## <a name="run-the-msbuild--tpack-command"></a>Ausführen des Befehls msbuild -t:pack

Um ein NuGet-Paket (eine `.nupkg`-Datei) aus dem Projekt zu erstellen, führen Sie den `msbuild -t:pack`-Befehl aus, der auch das Projekt automatisch erstellt:

Geben Sie an der Developer-Eingabeaufforderung für Visual Studio den folgenden Befehl ein:

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

Die Ausgabe zeigt den Pfad zur `.nupkg`-Datei.

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a>Automatisches Generieren des Pakets bei der Erstellung

Um `msbuild -t:pack` automatisch auszuführen, wenn Sie das Projekt erstellen oder wiederherstellen, fügen Sie Ihrer Projektdatei in `<PropertyGroup>` die folgende Zeile hinzu:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Wenn Sie `msbuild -t:pack` für eine Lösung ausführen, werden alle Projekte in der Lösung verpackt, die verpackt werden können (die Eigenschaft [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) wird auf `true` festgelegt).

> [!NOTE]
> Wenn Sie das Paket automatisch generieren, erhöht die Zeit zum Verpacken die Erstellungszeit für Ihr Projekt.

### <a name="test-package-installation"></a>Testen der Paketinstallation

Vor dem Veröffentlichen eines Pakets testen Sie in der Regel die Installation eines Pakets in einem Projekt. Diese Tests stellen sicher, dass die erforderlichen Dateien an den richtigen Orten im Projekt installiert werden.

Installationen lassen sich manuell in Visual Studio oder mithilfe der normalen [Paketinstallationsschritte](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package) über die Befehlszeile testen.

> [!IMPORTANT]
> Pakete sind unveränderlich. Wenn Sie ein Problem beheben, ändern Sie den Inhalt des Pakets und verpacken Sie es erneut. Wenn Sie es erneut testen, verwenden Sie weiterhin die alte Version des Pakets, bis Sie Ihren Ordner [für globale Pakete](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) löschen. Dies ist besonders relevant, wenn Sie Pakete testen, die nicht bei jedem Build eine eindeutige Vorabversionsbezeichnung verwenden.

## <a name="next-steps"></a>Nächste Schritte

Nachdem Sie ein Paket erstellt haben, das eine `.nupkg`-Datei ist, können Sie sie wie unter [Publishing packages (Veröffentlichen von Paketen)](../nuget-org/publish-a-package.md) beschrieben im Katalog Ihrer Wahl veröffentlichen.

Sie können auch die Funktionen des Pakets erweitern oder wie in den folgenden Themen beschrieben andere Szenarios unterstützen:

- [NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ MSBuild-Ziele)](../reference/msbuild-targets.md)
- [Paketversionsverwaltung](../concepts/package-versioning.md)
- [Unterstützung mehrerer Zielframeworks](../create-packages/multiple-target-frameworks-project-file.md)
- [Transformationen von Quell- und Konfigurationsdateien](../create-packages/source-and-config-file-transformations.md)
- [Lokalisierung](../create-packages/creating-localized-packages.md)
- [Vorabversionen](../create-packages/prerelease-packages.md)
- [Festlegen des Pakettyps](../create-packages/set-package-type.md)
- [Erstellen von Paketen mit COM-Interop-Assemblys](../create-packages/author-packages-with-COM-interop-assemblies.md)

Außerdem sollten Sie die folgenden zusätzlichen Pakettypen berücksichtigen:

- [Native Pakete](../guides/native-packages.md)
- [Symbolpakete](../create-packages/symbol-packages-snupkg.md)