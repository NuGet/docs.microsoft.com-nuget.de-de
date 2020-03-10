---
title: Erstellen eines NuGet-Pakets mit MSBuild
description: Eine ausführliche Anleitung zum Entwerfen und Erstellen eines NuGet-Pakets, einschließlich der wichtigsten Entscheidungspunkte wie Dateien und Versionsverwaltung
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 7166d622ef9d3975fc1c931d30caf570a765a6da
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231317"
---
# <a name="create-a-nuget-package-using-msbuild"></a><span data-ttu-id="b5286-103">Erstellen eines NuGet-Pakets mit MSBuild</span><span class="sxs-lookup"><span data-stu-id="b5286-103">Create a NuGet package using MSBuild</span></span>

<span data-ttu-id="b5286-104">Wenn Sie ein NuGet-Paket aus Ihrem Code erstellen, verpacken Sie diese Funktionalität in eine Komponente, die mit einer beliebigen Anzahl anderer Entwickler geteilt und von diesen verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="b5286-104">When you create a NuGet package from your code, you package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="b5286-105">In diesem Artikel wird das Erstellen eines Pakets mithilfe von MSBuild beschrieben.</span><span class="sxs-lookup"><span data-stu-id="b5286-105">This article describes how to create a package using MSBuild.</span></span> <span data-ttu-id="b5286-106">MSBuild wird mit allen Visual Studio-Workloads vorinstalliert, die NuGet enthalten.</span><span class="sxs-lookup"><span data-stu-id="b5286-106">MSBuild comes preinstalled with every Visual Studio workload that contains NuGet.</span></span> <span data-ttu-id="b5286-107">Zusätzlich können Sie MSBuild auch über die dotnet-CLI mit [dotnet msbuild](https://docs.microsoft.com/dotnet/core/tools/dotnet-msbuild) verwenden.</span><span class="sxs-lookup"><span data-stu-id="b5286-107">Additionally you can also use MSBuild through the dotnet CLI with [dotnet msbuild](https://docs.microsoft.com/dotnet/core/tools/dotnet-msbuild).</span></span>

<span data-ttu-id="b5286-108">Für .NET Core- und .NET Standard-Projekte, die das [SDK-Format](../resources/check-project-format.md) verwenden, und für alle anderen Projekte im SDK-Format verwendet NuGet Informationen in der Projektdatei direkt zum Erstellen eines Pakets.</span><span class="sxs-lookup"><span data-stu-id="b5286-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span>  <span data-ttu-id="b5286-109">Für ein Projekt im Nicht-SDK-Stil, das `<PackageReference>` verwendet, verwendet NuGet auch die Projektdatei, um ein Paket zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="b5286-109">For a non-SDK-style project that uses `<PackageReference>`, NuGet also uses the project file to create a package.</span></span>

<span data-ttu-id="b5286-110">Für Projekte im SDK-Stil ist die Packfunktionalität standardmäßig verfügbar.</span><span class="sxs-lookup"><span data-stu-id="b5286-110">SDK-style projects have the pack functionality available by default.</span></span> <span data-ttu-id="b5286-111">Für PackageReference-Projekte, die nicht im SDK-Stil erstellt werden, müssen Sie den Projektabhängigkeiten das Paket NuGet.Build.Tasks.Pack hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="b5286-111">For non SDK-style PackageReference projects, you need to add the NuGet.Build.Tasks.Pack package to the project dependencies.</span></span> <span data-ttu-id="b5286-112">Ausführliche Informationen zu MSBuild-Packzielen finden Sie unter [NuGet-Befehle „pack“ und „restore“ als MSBuild-Ziele](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="b5286-112">For detailed information about MSBuild pack targets, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

<span data-ttu-id="b5286-113">Der Befehl, mit dem ein Paket erstellt wird (`msbuild -t:pack`), ist funktional äquivalent mit `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="b5286-113">The command that creates a package, `msbuild -t:pack`, is functionality equivalent to `dotnet pack`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b5286-114">Dieses Thema gilt für Projekte im [SDK-Stil](../resources/check-project-format.md), in der Regel .NET Core- und .NET Standard-Projekte, und für Projekte im Nicht-SDK-Stil, die PackageReference verwenden.</span><span class="sxs-lookup"><span data-stu-id="b5286-114">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects, and to non-SDK-style projects that use PackageReference.</span></span>

## <a name="set-properties"></a><span data-ttu-id="b5286-115">Eigenschaften festlegen</span><span class="sxs-lookup"><span data-stu-id="b5286-115">Set properties</span></span>

<span data-ttu-id="b5286-116">Die folgenden Eigenschaften sind für die Erstellung eines Pakets erforderlich.</span><span class="sxs-lookup"><span data-stu-id="b5286-116">The following properties are required to create a package.</span></span>

- <span data-ttu-id="b5286-117">`PackageId`, der Paketbezeichner. Dieser muss im Katalog, der das Paket hostet, eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="b5286-117">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="b5286-118">Wenn Sie hier nichts angeben, lautet der Standardwert `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="b5286-118">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="b5286-119">`Version`, eine bestimmte Versionsnummer in der Schreibweise *Hauptversion.Nebenversion.Patch[-Suffix]* , wobei im *-Suffix* die [Vorabversionen](prerelease-packages.md) angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="b5286-119">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="b5286-120">Wenn Sie hier nichts angeben, lautet der Standardwert 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="b5286-120">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="b5286-121">Der Titel des Pakets, so wie er auf dem Host (z.B. „nuget.org“) angezeigt werden sollte</span><span class="sxs-lookup"><span data-stu-id="b5286-121">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="b5286-122">`Authors`, Informationen zum Autor und Besitzer.</span><span class="sxs-lookup"><span data-stu-id="b5286-122">`Authors`, author and owner information.</span></span> <span data-ttu-id="b5286-123">Wenn Sie hier nichts angeben, lautet der Standardwert `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="b5286-123">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="b5286-124">`Company`, der Firmenname.</span><span class="sxs-lookup"><span data-stu-id="b5286-124">`Company`, your company name.</span></span> <span data-ttu-id="b5286-125">Wenn Sie hier nichts angeben, lautet der Standardwert `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="b5286-125">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="b5286-126">Wenn Sie Nicht-SDK-Projekte packen, die PackageReference verwenden, ist außerdem Folgendes erforderlich:</span><span class="sxs-lookup"><span data-stu-id="b5286-126">Additionally if you are packing non-SDK-style projects that use PackageReference, the following is required:</span></span>

- <span data-ttu-id="b5286-127">`PackageOutputPath`, der Ausgabeordner für das Paket, das beim Paketaufruf generiert wird.</span><span class="sxs-lookup"><span data-stu-id="b5286-127">`PackageOutputPath`, the output folder for the package generated when calling pack.</span></span>

<span data-ttu-id="b5286-128">In Visual Studio können Sie diese Werte in den Projekteigenschaften festlegen (Rechtsklick auf das Projekt im Projektmappen-Explorer, wählen Sie **Eigenschaften** und dann die Registerkarte **Paket** aus).</span><span class="sxs-lookup"><span data-stu-id="b5286-128">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="b5286-129">Sie können diese Eigenschaften auch direkt in den Projektdateien festlegen ( *.csproj*).</span><span class="sxs-lookup"><span data-stu-id="b5286-129">You can also set these properties directly in the project files (*.csproj*).</span></span>

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="b5286-130">Weisen Sie dem Paket einen Bezeichner zu, der auf nuget.org bzw. in der Paketquelle, den Sie verwenden, einzigartig ist.</span><span class="sxs-lookup"><span data-stu-id="b5286-130">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="b5286-131">Das folgende Beispiel zeigt eine einfache, vollständige Projektdatei, in der diese Eigenschaften enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="b5286-131">The following example shows a simple, complete project file with these properties included.</span></span>

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

<span data-ttu-id="b5286-132">Sie können auch die optionalen Eigenschaften wie `Title`, `PackageDescription` und `PackageTags` festlegen, wie in [MSBuild-Paketziele](../reference/msbuild-targets.md#pack-target), [Steuern von Abhängigkeitsobjekten](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) und [NuGet-Metadateneigenschaften](/dotnet/core/tools/csproj#nuget-metadata-properties) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="b5286-132">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="b5286-133">Bei Paketen für die öffentliche Nutzung sollten Sie besonders auf die **PackageTags**-Eigenschaft achten, da Tags anderen dabei helfen, Ihr Paket zu finden und dessen Funktion zu verstehen.</span><span class="sxs-lookup"><span data-stu-id="b5286-133">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="b5286-134">Weitere Informationen zum Deklarieren von Abhängigkeiten und zum Angeben von Versionsnummern finden Sie unter [Paketverweise in Projektdateien](../consume-packages/package-references-in-project-files.md) und [Paketversionsverwaltung](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b5286-134">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="b5286-135">Es ist auch möglich, Ressourcen aus Abhängigkeiten mithilfe der Attribute `<IncludeAssets>` und `<ExcludeAssets>` direkt im Paket verfügbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="b5286-135">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="b5286-136">Weitere Informationen finden Sie unter [Steuern von Abhängigkeitsobjekten](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="b5286-136">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="b5286-137">Hinzufügen eines optionalen Beschreibungsfelds</span><span class="sxs-lookup"><span data-stu-id="b5286-137">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="b5286-138">Auswählen eines eindeutigen Paketbezeichners und Festlegen der Versionsnummer</span><span class="sxs-lookup"><span data-stu-id="b5286-138">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a><span data-ttu-id="b5286-139">Hinzufügen des Pakets NuGet.Build.Tasks.Pack</span><span class="sxs-lookup"><span data-stu-id="b5286-139">Add the NuGet.Build.Tasks.Pack package</span></span>

<span data-ttu-id="b5286-140">Wenn Sie MSBuild mit einem Projekt im Nicht-SDK-Stil und PackageReference verwenden, fügen Sie Ihrem Projekt das Paket NuGet.Build.Tasks.Pack hinzu.</span><span class="sxs-lookup"><span data-stu-id="b5286-140">If you are using MSBuild with a non-SDK-style project and PackageReference, add the NuGet.Build.Tasks.Pack package to your project.</span></span>

1. <span data-ttu-id="b5286-141">Öffnen Sie die Projektdatei, und fügen Sie Folgendes hinter dem `<PropertyGroup>`-Element hinzu:</span><span class="sxs-lookup"><span data-stu-id="b5286-141">Open the project file and add the following after the `<PropertyGroup>` element:</span></span>

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. <span data-ttu-id="b5286-142">Öffnen Sie eine Developer-Eingabeaufforderung (geben Sie **Developer-Eingabeaufforderung** im **Suchfeld** ein).</span><span class="sxs-lookup"><span data-stu-id="b5286-142">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="b5286-143">In der Regel sollten Sie die „Developer-Eingabeaufforderung für Visual Studio“ über das **Startmenü** starten, da dieses mit allen nötigen Pfaden für MSBuild konfiguriert ist.</span><span class="sxs-lookup"><span data-stu-id="b5286-143">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

3. <span data-ttu-id="b5286-144">Wechseln Sie zu dem Ordner, der die Projektdatei enthält, und geben Sie den folgenden Befehl ein, um das Paket NuGet.Build.Tasks.Pack zu installieren.</span><span class="sxs-lookup"><span data-stu-id="b5286-144">Switch to the folder containing the project file and type the following command to install the NuGet.Build.Tasks.Pack package.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   <span data-ttu-id="b5286-145">Stellen Sie sicher, dass die MSBuild-Ausgabe angibt, dass der Build erfolgreich abgeschlossen wurde.</span><span class="sxs-lookup"><span data-stu-id="b5286-145">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="run-the-msbuild--tpack-command"></a><span data-ttu-id="b5286-146">Ausführen des Befehls msbuild -t:pack</span><span class="sxs-lookup"><span data-stu-id="b5286-146">Run the msbuild -t:pack command</span></span>

<span data-ttu-id="b5286-147">Um ein NuGet-Paket (eine `.nupkg`-Datei) aus dem Projekt zu erstellen, führen Sie den `msbuild -t:pack`-Befehl aus, der auch das Projekt automatisch erstellt:</span><span class="sxs-lookup"><span data-stu-id="b5286-147">To build a NuGet package (a `.nupkg` file) from the project, run the `msbuild -t:pack` command, which also builds the project automatically:</span></span>

<span data-ttu-id="b5286-148">Geben Sie an der Developer-Eingabeaufforderung für Visual Studio den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="b5286-148">In the Developer command prompt for Visual Studio, type the following command:</span></span>

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

<span data-ttu-id="b5286-149">Die Ausgabe zeigt den Pfad zur `.nupkg`-Datei.</span><span class="sxs-lookup"><span data-stu-id="b5286-149">The output shows the path to the `.nupkg` file.</span></span>

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

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="b5286-150">Automatisches Generieren des Pakets bei der Erstellung</span><span class="sxs-lookup"><span data-stu-id="b5286-150">Automatically generate package on build</span></span>

<span data-ttu-id="b5286-151">Um `msbuild -t:pack` automatisch auszuführen, wenn Sie das Projekt erstellen oder wiederherstellen, fügen Sie Ihrer Projektdatei in `<PropertyGroup>` die folgende Zeile hinzu:</span><span class="sxs-lookup"><span data-stu-id="b5286-151">To automatically run `msbuild -t:pack` when you build or restore the project, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="b5286-152">Wenn Sie `msbuild -t:pack` für eine Lösung ausführen, werden alle Projekte in der Lösung verpackt, die verpackt werden können (die Eigenschaft [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) wird auf `true` festgelegt).</span><span class="sxs-lookup"><span data-stu-id="b5286-152">When you run `msbuild -t:pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="b5286-153">Wenn Sie das Paket automatisch generieren, erhöht die Zeit zum Verpacken die Erstellungszeit für Ihr Projekt.</span><span class="sxs-lookup"><span data-stu-id="b5286-153">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="b5286-154">Testen der Paketinstallation</span><span class="sxs-lookup"><span data-stu-id="b5286-154">Test package installation</span></span>

<span data-ttu-id="b5286-155">Vor dem Veröffentlichen eines Pakets testen Sie in der Regel die Installation eines Pakets in einem Projekt.</span><span class="sxs-lookup"><span data-stu-id="b5286-155">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="b5286-156">Diese Tests stellen sicher, dass die erforderlichen Dateien an den richtigen Orten im Projekt installiert werden.</span><span class="sxs-lookup"><span data-stu-id="b5286-156">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="b5286-157">Installationen lassen sich manuell in Visual Studio oder mithilfe der normalen [Paketinstallationsschritte](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package) über die Befehlszeile testen.</span><span class="sxs-lookup"><span data-stu-id="b5286-157">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b5286-158">Pakete sind unveränderlich.</span><span class="sxs-lookup"><span data-stu-id="b5286-158">Packages are immutable.</span></span> <span data-ttu-id="b5286-159">Wenn Sie ein Problem beheben, ändern Sie den Inhalt des Pakets und verpacken Sie es erneut. Wenn Sie es erneut testen, verwenden Sie weiterhin die alte Version des Pakets, bis Sie Ihren Ordner [für globale Pakete](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) löschen.</span><span class="sxs-lookup"><span data-stu-id="b5286-159">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="b5286-160">Dies ist besonders relevant, wenn Sie Pakete testen, die nicht bei jedem Build eine eindeutige Vorabversionsbezeichnung verwenden.</span><span class="sxs-lookup"><span data-stu-id="b5286-160">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5286-161">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="b5286-161">Next Steps</span></span>

<span data-ttu-id="b5286-162">Nachdem Sie ein Paket erstellt haben, das eine `.nupkg`-Datei ist, können Sie sie wie unter [Publishing packages (Veröffentlichen von Paketen)](../nuget-org/publish-a-package.md) beschrieben im Katalog Ihrer Wahl veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="b5286-162">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="b5286-163">Sie können auch die Funktionen des Pakets erweitern oder wie in den folgenden Themen beschrieben andere Szenarios unterstützen:</span><span class="sxs-lookup"><span data-stu-id="b5286-163">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="b5286-164">NuGet-Befehle „pack“ und „restore“ als MSBuild-Ziele</span><span class="sxs-lookup"><span data-stu-id="b5286-164">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
- [<span data-ttu-id="b5286-165">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="b5286-165">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="b5286-166">Unterstützung mehrerer Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="b5286-166">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="b5286-167">Transformationen von Quell- und Konfigurationsdateien</span><span class="sxs-lookup"><span data-stu-id="b5286-167">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="b5286-168">Lokalisierung</span><span class="sxs-lookup"><span data-stu-id="b5286-168">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="b5286-169">Vorabversionen</span><span class="sxs-lookup"><span data-stu-id="b5286-169">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="b5286-170">Festlegen des Pakettyps</span><span class="sxs-lookup"><span data-stu-id="b5286-170">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="b5286-171">Erstellen von Paketen mit COM-Interop-Assemblys</span><span class="sxs-lookup"><span data-stu-id="b5286-171">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="b5286-172">Außerdem sollten Sie die folgenden zusätzlichen Pakettypen berücksichtigen:</span><span class="sxs-lookup"><span data-stu-id="b5286-172">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="b5286-173">Native Pakete</span><span class="sxs-lookup"><span data-stu-id="b5286-173">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="b5286-174">Symbolpakete</span><span class="sxs-lookup"><span data-stu-id="b5286-174">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
