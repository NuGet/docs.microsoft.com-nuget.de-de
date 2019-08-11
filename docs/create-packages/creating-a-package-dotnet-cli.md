---
title: Erstellen eines NuGet-Pakets mithilfe der dotnet-CLI
description: Eine ausführliche Anleitung zum Entwerfen und Erstellen eines NuGet-Pakets, einschließlich der wichtigsten Entscheidungspunkte wie Dateien und Versionsverwaltung
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 8222e1edfa13951d2fda9a2384d93bba38ef4979
ms.sourcegitcommit: ba8ad1bd13a4bba3df94374e34e20c425a05af2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2019
ms.locfileid: "68833290"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="60a28-103">Erstellen eines NuGet-Pakets mithilfe der dotnet-CLI</span><span class="sxs-lookup"><span data-stu-id="60a28-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="60a28-104">Unabhängig davon, welchen Zweck Ihr Paket erfüllt oder welchen Code es enthält, verwenden Sie eines der CLI-Tools (entweder `nuget.exe` oder `dotnet.exe`), um diese Funktionalität in einer Komponente zu verpacken, die für andere Entwickler freigegeben und von ihnen verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="60a28-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="60a28-105">In diesem Artikel wird das Erstellen eines Pakets mithilfe der dotnet-CLI beschrieben.</span><span class="sxs-lookup"><span data-stu-id="60a28-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="60a28-106">Informationen zur Installation der `dotnet`-CLI finden Sie unter [Installieren von NuGet-Clienttools](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="60a28-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="60a28-107">Ab Visual Studio 2017 ist die dotnet-CLI in .NET Core-Workloads enthalten.</span><span class="sxs-lookup"><span data-stu-id="60a28-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="60a28-108">Für .NET Core- und .NET Standard-Projekte, die das [SDK-Format](../resources/check-project-format.md) verwenden, und für alle anderen Projekte im SDK-Format verwendet NuGet Informationen in der Projektdatei direkt zum Erstellen eines Pakets.</span><span class="sxs-lookup"><span data-stu-id="60a28-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="60a28-109">Schritt-für-Schritt-Tutorials finden Sie unter [Erstellen von .NET Standard-Paketen mit der dotnet-CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) und [Erstellen von .NET Standard-Paketen mit Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="60a28-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) or [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="60a28-110">`msbuild -t:pack` ist funktionell gleichwertig mit `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="60a28-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="60a28-111">Informationen zum Erstellen mit MSBuild finden Sie unter [Erstellen eines NuGet-Pakets mit MSBuild](creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="60a28-111">To build with MSBuild, see [Create a NuGet package using MSBuild](creating-a-package-msbuild.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60a28-112">Dieses Thema bezieht sich auf Projekte im [SDK-Stil](../resources/check-project-format.md), in der Regel .NET Core- und .NET Standard-Projekte.</span><span class="sxs-lookup"><span data-stu-id="60a28-112">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="60a28-113">Eigenschaften festlegen</span><span class="sxs-lookup"><span data-stu-id="60a28-113">Set properties</span></span>

<span data-ttu-id="60a28-114">Die folgenden Eigenschaften sind für die Erstellung eines Pakets erforderlich.</span><span class="sxs-lookup"><span data-stu-id="60a28-114">The following properties are required to create a package.</span></span>

- <span data-ttu-id="60a28-115">`PackageId`, der Paketbezeichner. Dieser muss im Katalog, der das Paket hostet, eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="60a28-115">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="60a28-116">Wenn Sie hier nichts angeben, lautet der Standardwert `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="60a28-116">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="60a28-117">`Version`, eine bestimmte Versionsnummer in der Schreibweise *Hauptversion.Nebenversion.Patch[-Suffix]* , wobei im *-Suffix* die [Vorabversionen](prerelease-packages.md) angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="60a28-117">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="60a28-118">Wenn Sie hier nichts angeben, lautet der Standardwert 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="60a28-118">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="60a28-119">Der Titel des Pakets, so wie er auf dem Host (z.B. „nuget.org“) angezeigt werden sollte</span><span class="sxs-lookup"><span data-stu-id="60a28-119">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="60a28-120">`Authors`, Informationen zum Autor und Besitzer.</span><span class="sxs-lookup"><span data-stu-id="60a28-120">`Authors`, author and owner information.</span></span> <span data-ttu-id="60a28-121">Wenn Sie hier nichts angeben, lautet der Standardwert `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="60a28-121">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="60a28-122">`Company`, der Firmenname.</span><span class="sxs-lookup"><span data-stu-id="60a28-122">`Company`, your company name.</span></span> <span data-ttu-id="60a28-123">Wenn Sie hier nichts angeben, lautet der Standardwert `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="60a28-123">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="60a28-124">In Visual Studio können Sie diese Werte in den Projekteigenschaften festlegen (Rechtsklick auf das Projekt im Projektmappen-Explorer, wählen Sie **Eigenschaften** und dann die Registerkarte **Paket** aus).</span><span class="sxs-lookup"><span data-stu-id="60a28-124">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="60a28-125">Sie können diese Eigenschaften auch direkt in den Projektdateien festlegen (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="60a28-125">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="60a28-126">Weisen Sie dem Paket einen Bezeichner zu, der auf nuget.org bzw. in der Paketquelle, den Sie verwenden, einzigartig ist.</span><span class="sxs-lookup"><span data-stu-id="60a28-126">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="60a28-127">Das folgende Beispiel zeigt eine einfache, vollständige Projektdatei, in der diese Eigenschaften enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="60a28-127">The following example shows a simple, complete project file with these properties included.</span></span> <span data-ttu-id="60a28-128">(Sie können ein neues Standardprojekt mit dem Befehl `dotnet new classlib` erstellen.)</span><span class="sxs-lookup"><span data-stu-id="60a28-128">(You can create a new default project using the `dotnet new classlib` command.)</span></span>

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

<span data-ttu-id="60a28-129">Sie können auch die optionalen Eigenschaften wie `Title`, `PackageDescription` und `PackageTags` festlegen, wie in [MSBuild-Paketziele](../reference/msbuild-targets.md#pack-target), [Steuern von Abhängigkeitsobjekten](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) und [NuGet-Metadateneigenschaften](/dotnet/core/tools/csproj#nuget-metadata-properties) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="60a28-129">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="60a28-130">Bei Paketen für die öffentliche Nutzung sollten Sie besonders auf die **PackageTags**-Eigenschaft achten, da Tags anderen dabei helfen, Ihr Paket zu finden und dessen Funktion zu verstehen.</span><span class="sxs-lookup"><span data-stu-id="60a28-130">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="60a28-131">Weitere Informationen zum Deklarieren von Abhängigkeiten und zum Angeben von Versionsnummern finden Sie unter [Paketverweise in Projektdateien](../consume-packages/package-references-in-project-files.md) und [Paketversionsverwaltung](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="60a28-131">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="60a28-132">Es ist auch möglich, Ressourcen aus Abhängigkeiten mithilfe der Attribute `<IncludeAssets>` und `<ExcludeAssets>` direkt im Paket verfügbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="60a28-132">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="60a28-133">Weitere Informationen finden Sie unter [Steuern von Abhängigkeitsobjekten](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="60a28-133">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="60a28-134">Auswählen eines eindeutigen Paketbezeichners und Festlegen der Versionsnummer</span><span class="sxs-lookup"><span data-stu-id="60a28-134">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a><span data-ttu-id="60a28-135">Ausführen des Befehls pack</span><span class="sxs-lookup"><span data-stu-id="60a28-135">Run the pack command</span></span>

<span data-ttu-id="60a28-136">Um ein NuGet-Paket (eine `.nupkg`-Datei) aus dem Projekt zu erstellen, führen Sie den `dotnet pack`-Befehl aus, der auch das Projekt automatisch erstellt:</span><span class="sxs-lookup"><span data-stu-id="60a28-136">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="60a28-137">Die Ausgabe zeigt den Pfad zur `.nupkg`-Datei.</span><span class="sxs-lookup"><span data-stu-id="60a28-137">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="60a28-138">Automatisches Generieren des Pakets bei der Erstellung</span><span class="sxs-lookup"><span data-stu-id="60a28-138">Automatically generate package on build</span></span>

<span data-ttu-id="60a28-139">Um automatisch `dotnet pack` auszuführen, wenn Sie `dotnet build` ausführen, fügen Sie folgende Zeile zu Ihrer Projektdatei in `<PropertyGroup>` hinzu:</span><span class="sxs-lookup"><span data-stu-id="60a28-139">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="60a28-140">Wenn Sie `dotnet pack` für eine Projektmappe ausführen, werden alle Projekte in der Projektmappe verpackt, die verpackt werden können (die Eigenschaft [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) wird auf `true` festgelegt).</span><span class="sxs-lookup"><span data-stu-id="60a28-140">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="60a28-141">Wenn Sie das Paket automatisch generieren, erhöht die Zeit zum Verpacken die Erstellungszeit für Ihr Projekt.</span><span class="sxs-lookup"><span data-stu-id="60a28-141">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="60a28-142">Testen der Paketinstallation</span><span class="sxs-lookup"><span data-stu-id="60a28-142">Test package installation</span></span>

<span data-ttu-id="60a28-143">Vor dem Veröffentlichen eines Pakets testen Sie in der Regel die Installation eines Pakets in einem Projekt.</span><span class="sxs-lookup"><span data-stu-id="60a28-143">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="60a28-144">Diese Tests stellen sicher, dass die erforderlichen Dateien an den richtigen Orten im Projekt installiert werden.</span><span class="sxs-lookup"><span data-stu-id="60a28-144">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="60a28-145">Installationen lassen sich manuell in Visual Studio oder mithilfe der normalen [Paketinstallationsschritte](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package) über die Befehlszeile testen.</span><span class="sxs-lookup"><span data-stu-id="60a28-145">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60a28-146">Pakete sind unveränderlich.</span><span class="sxs-lookup"><span data-stu-id="60a28-146">Packages are immutable.</span></span> <span data-ttu-id="60a28-147">Wenn Sie ein Problem beheben, ändern Sie den Inhalt des Pakets und verpacken Sie es erneut. Wenn Sie es erneut testen, verwenden Sie weiterhin die alte Version des Pakets, bis Sie Ihren Ordner [für globale Pakete](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) löschen.</span><span class="sxs-lookup"><span data-stu-id="60a28-147">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="60a28-148">Dies ist besonders relevant, wenn Sie Pakete testen, die nicht bei jedem Build eine eindeutige Vorabversionsbezeichnung verwenden.</span><span class="sxs-lookup"><span data-stu-id="60a28-148">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60a28-149">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="60a28-149">Next Steps</span></span>

<span data-ttu-id="60a28-150">Nachdem Sie ein Paket erstellt haben, das eine `.nupkg`-Datei ist, können Sie sie wie unter [Publishing packages (Veröffentlichen von Paketen)](../nuget-org/publish-a-package.md) beschrieben im Katalog Ihrer Wahl veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="60a28-150">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="60a28-151">Sie können auch die Funktionen des Pakets erweitern oder wie in den folgenden Themen beschrieben andere Szenarios unterstützen:</span><span class="sxs-lookup"><span data-stu-id="60a28-151">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="60a28-152">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="60a28-152">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="60a28-153">Unterstützung mehrerer Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="60a28-153">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="60a28-154">Transformationen von Quell- und Konfigurationsdateien</span><span class="sxs-lookup"><span data-stu-id="60a28-154">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="60a28-155">Lokalisierung</span><span class="sxs-lookup"><span data-stu-id="60a28-155">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="60a28-156">Vorabversionen</span><span class="sxs-lookup"><span data-stu-id="60a28-156">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="60a28-157">Festlegen des Pakettyps</span><span class="sxs-lookup"><span data-stu-id="60a28-157">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="60a28-158">Erstellen von Paketen mit COM-Interop-Assemblys</span><span class="sxs-lookup"><span data-stu-id="60a28-158">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="60a28-159">Außerdem sollten Sie die folgenden zusätzlichen Pakettypen berücksichtigen:</span><span class="sxs-lookup"><span data-stu-id="60a28-159">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="60a28-160">Native Pakete</span><span class="sxs-lookup"><span data-stu-id="60a28-160">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="60a28-161">Symbolpakete</span><span class="sxs-lookup"><span data-stu-id="60a28-161">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
