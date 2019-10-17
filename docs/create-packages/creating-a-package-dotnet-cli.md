---
title: Erstellen eines NuGet-Pakets mithilfe der dotnet-CLI
description: Eine ausführliche Anleitung zum Entwerfen und Erstellen eines NuGet-Pakets, einschließlich der wichtigsten Entscheidungspunkte wie Dateien und Versionsverwaltung
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: ec37057d40ddc9ed1826b0628aaa573c342b92b6
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380744"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>Erstellen eines NuGet-Pakets mithilfe der dotnet-CLI

Unabhängig davon, welchen Zweck Ihr Paket erfüllt oder welchen Code es enthält, verwenden Sie eines der CLI-Tools (entweder `nuget.exe` oder `dotnet.exe`), um diese Funktionalität in einer Komponente zu verpacken, die für andere Entwickler freigegeben und von ihnen verwendet werden kann. In diesem Artikel wird das Erstellen eines Pakets mithilfe der dotnet-CLI beschrieben. Informationen zur Installation der `dotnet`-CLI finden Sie unter [Installieren von NuGet-Clienttools](../install-nuget-client-tools.md). Ab Visual Studio 2017 ist die dotnet-CLI in .NET Core-Workloads enthalten.

Für .NET Core- und .NET Standard-Projekte, die das [SDK-Format](../resources/check-project-format.md) verwenden, und für alle anderen Projekte im SDK-Format verwendet NuGet Informationen in der Projektdatei direkt zum Erstellen eines Pakets. Schritt-für-Schritt-Tutorials finden Sie unter [Erstellen von .NET Standard-Paketen mit der dotnet-CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) und [Erstellen von .NET Standard-Paketen mit Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).

`msbuild -t:pack` ist funktionell gleichwertig mit `dotnet pack`. Informationen zum Erstellen mit MSBuild finden Sie unter [Erstellen eines NuGet-Pakets mit MSBuild](creating-a-package-msbuild.md).

> [!IMPORTANT]
> Dieses Thema bezieht sich auf Projekte im [SDK-Stil](../resources/check-project-format.md), in der Regel .NET Core- und .NET Standard-Projekte.

## <a name="set-properties"></a>Eigenschaften festlegen

Die folgenden Eigenschaften sind für die Erstellung eines Pakets erforderlich.

- `PackageId`, der Paketbezeichner. Dieser muss im Katalog, der das Paket hostet, eindeutig sein. Wenn Sie hier nichts angeben, lautet der Standardwert `AssemblyName`.
- `Version`, eine bestimmte Versionsnummer in der Schreibweise *Hauptversion.Nebenversion.Patch[-Suffix]* , wobei im *-Suffix* die [Vorabversionen](prerelease-packages.md) angegeben werden. Wenn Sie hier nichts angeben, lautet der Standardwert 1.0.0.
- Der Titel des Pakets, so wie er auf dem Host (z.B. „nuget.org“) angezeigt werden sollte
- `Authors`, Informationen zum Autor und Besitzer. Wenn Sie hier nichts angeben, lautet der Standardwert `AssemblyName`.
- `Company`, der Firmenname. Wenn Sie hier nichts angeben, lautet der Standardwert `AssemblyName`.

In Visual Studio können Sie diese Werte in den Projekteigenschaften festlegen (Rechtsklick auf das Projekt im Projektmappen-Explorer, wählen Sie **Eigenschaften** und dann die Registerkarte **Paket** aus). Sie können diese Eigenschaften auch direkt in den Projektdateien festlegen (`.csproj`).

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Weisen Sie dem Paket einen Bezeichner zu, der auf nuget.org bzw. in der Paketquelle, den Sie verwenden, einzigartig ist.

Das folgende Beispiel zeigt eine einfache, vollständige Projektdatei, in der diese Eigenschaften enthalten sind. (Sie können ein neues Standardprojekt mit dem Befehl `dotnet new classlib` erstellen.)

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
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

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Auswählen eines eindeutigen Paketbezeichners und Festlegen der Versionsnummer

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a>Ausführen des Befehls pack

Um ein NuGet-Paket (eine `.nupkg`-Datei) aus dem Projekt zu erstellen, führen Sie den `dotnet pack`-Befehl aus, der auch das Projekt automatisch erstellt:

```cli
# Uses the project file in the current folder by default
dotnet pack
```

Die Ausgabe zeigt den Pfad zur `.nupkg`-Datei.

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Automatisches Generieren des Pakets bei der Erstellung

Um automatisch `dotnet pack` auszuführen, wenn Sie `dotnet build` ausführen, fügen Sie folgende Zeile zu Ihrer Projektdatei in `<PropertyGroup>` hinzu:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Wenn Sie `dotnet pack` für eine Projektmappe ausführen, werden alle Projekte in der Projektmappe verpackt, die verpackt werden können (die Eigenschaft [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) wird auf `true` festgelegt).

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
