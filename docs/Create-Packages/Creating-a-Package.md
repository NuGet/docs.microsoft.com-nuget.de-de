---
title: Erstellen eines NuGet-Pakets | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 456797cb-e3e4-4b88-9b01-8b5153cee802
description: "Eine ausführliche Anleitung zum Entwerfen und Erstellen eines NuGet-Pakets, einschließlich der wichtigsten Entscheidungspunkte wie Dateien und Versionsverwaltung"
keywords: Erstellen von NuGet-Paketen, Erstellen eines Pakets, NUSPEC-Manifest, NuGet-Paketkonventionen, Version des NuGet-Pakets
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6675d21a2900a1b61e17c08518b328732f4472c5
ms.sourcegitcommit: 1cb047b24b3b69d80e808c23b2ace0d98d2dfdcc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="29436-104">Erstellen von NuGet-Paketen</span><span class="sxs-lookup"><span data-stu-id="29436-104">Creating NuGet packages</span></span>

<span data-ttu-id="29436-105">Unabhängig davon, was Ihr Paket macht oder welchen Code es enthält, können Sie die Funktionalität mit `nuget.exe` in eine Komponente packen, die für andere Entwickler freigegeben und von ihnen verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="29436-105">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="29436-106">Weitere Informationen zum Installieren von `nuget.exe` finden Sie unter [Install NuGet CLI (Installieren der NuGet-CLI)](../guides/Install-NuGet.md#nuget-cli).</span><span class="sxs-lookup"><span data-stu-id="29436-106">To install `nuget.exe`, see [Install NuGet CLI](../guides/Install-NuGet.md#nuget-cli).</span></span> <span data-ttu-id="29436-107">Beachten Sie, dass `nuget.exe` nicht automatisch in Visual Studio enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="29436-107">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="29436-108">Technisch gesehen ist ein NuGet-Paket eine ZIP-Datei, die mit der `.nupkg`-Erweiterung umbenannt wurde und deren Inhalt bestimmten Konventionen entspricht.</span><span class="sxs-lookup"><span data-stu-id="29436-108">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="29436-109">In diesem Thema werden die Schritte zum Erstellen eines Pakets, das diesen Konventionen entspricht, ausführlich beschrieben.</span><span class="sxs-lookup"><span data-stu-id="29436-109">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="29436-110">Eine fokussierte exemplarische Vorgehensweise finden Sie unter [Create and Publish a Package Quickstart (Schnellstart zum Erstellen und Veröffentlichen eines Pakets)](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="29436-110">For a focused walkthrough, refer to [Create and Publish a Package Quickstart](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="29436-111">Das Packen beginnt mit dem kompilierten Code (Assemblys), Symbolen und/oder anderen Dateien, die Sie als Paket übermitteln möchten. Weitere Informationen finden Sie unter [Overview and workflow (Übersicht und Workflow)](Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="29436-111">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](Overview-and-Workflow.md)).</span></span> <span data-ttu-id="29436-112">Dieser Vorgang wird unabhängig vom Kompilieren oder jeder anderen Methode zum Generieren der Dateien ausgeführt, die in das Paket gepackt werden. Sie können die kompilierten Assemblys und Pakete jedoch mithilfe der Informationen in einer Projektdatei kontinuierlich synchronisieren.</span><span class="sxs-lookup"><span data-stu-id="29436-112">This process is independent from compiling or otherwise generating the files that go into the package, although you can use draw from information in a project file to keep the compiled assemblines and packages in sync.</span></span>

<span data-ttu-id="29436-113">In diesem Thema:</span><span class="sxs-lookup"><span data-stu-id="29436-113">In this topic:</span></span>

- [<span data-ttu-id="29436-114">Welche Assemblys sollen gepackt werden?</span><span class="sxs-lookup"><span data-stu-id="29436-114">Deciding which assemblies to package</span></span>](#deciding-which-assemblies-to-package)
- [<span data-ttu-id="29436-115">Rolle und Struktur der Datei `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="29436-115">The role and structure of the `.nuspec` file</span></span>](#the-role-and-structure-of-the-nuspec-file)
- <span data-ttu-id="29436-116">[Erstellen der `.nuspec`-Datei ](#creating-the-nuspec-file) aus:</span><span class="sxs-lookup"><span data-stu-id="29436-116">[Creating the `.nuspec` file](#creating-the-nuspec-file) from:</span></span>
    - [<span data-ttu-id="29436-117">einem konventionsbasierten Arbeitsverzeichnis</span><span class="sxs-lookup"><span data-stu-id="29436-117">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
    - [<span data-ttu-id="29436-118">einer Assembly-DLL</span><span class="sxs-lookup"><span data-stu-id="29436-118">An assembly DLL</span></span>](#from-an-assembly-dll)
    - [<span data-ttu-id="29436-119">einem Visual Studio-Projekt</span><span class="sxs-lookup"><span data-stu-id="29436-119">A Visual Studio project</span></span>](#from-a-visual-studio-project)
    - [<span data-ttu-id="29436-120">einer neuen Datei mit Standardwerten</span><span class="sxs-lookup"><span data-stu-id="29436-120">New file with default values</span></span>](#new-file-with-default-values)    
- [<span data-ttu-id="29436-121">Auswählen eines eindeutigen Paketbezeichners und Festlegen der Versionsnummer</span><span class="sxs-lookup"><span data-stu-id="29436-121">Choosing a unique package identifier and setting the version number</span></span>](#choosing-a-unique-package-identifier-and-setting-the-version-number)
- <span data-ttu-id="29436-122">[Festlegen eines Pakettyps](#setting-a-package-type) (NuGet 3.5 und höher)</span><span class="sxs-lookup"><span data-stu-id="29436-122">[Setting a package type](#setting-a-package-type) (NuGet 3.5 and later)</span></span>
- [<span data-ttu-id="29436-123">Hinzufügen einer Infodatei und anderer Dateien</span><span class="sxs-lookup"><span data-stu-id="29436-123">Adding a readme and other files</span></span>](#adding-a-readme-and-other-files)
- [<span data-ttu-id="29436-124">Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket</span><span class="sxs-lookup"><span data-stu-id="29436-124">Including MSBuild props and targets in a package</span></span>](#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="29436-125">Erstellen von Paketen, die COM-Interop-Assemblys enthalten</span><span class="sxs-lookup"><span data-stu-id="29436-125">Authoring packages that contain COM interop assemblies</span></span>](#authoring-packages-with-com-interop-assemblies)
- [<span data-ttu-id="29436-126">Ausführen von „nuget pack“ zum Generieren der NUPKG-Datei</span><span class="sxs-lookup"><span data-stu-id="29436-126">Running nuget pack to generate the .nupkg file</span></span>](#running-nuget-pack-to-generate-the-nupkg-file)

<span data-ttu-id="29436-127">Im Anschluss an diese Anleitung können Sie, wie an anderer Stelle in dieser Dokumentation beschrieben, weitere Funktionen integrieren.</span><span class="sxs-lookup"><span data-stu-id="29436-127">After these core steps, you can incorporate a variety of other features as described elsewhere in this documentation.</span></span> <span data-ttu-id="29436-128">Weitere Informationen finden Sie unten im Abschnitt [Nächste Schritte](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="29436-128">See [Next steps](#next-steps) below.</span></span>

> [!Note]
> <span data-ttu-id="29436-129">Dieses Thema gilt nicht für .NET Core-Projekte, in denen Visual Studio 2017 und NuGet 4.0 und höher verwendet wurde.</span><span class="sxs-lookup"><span data-stu-id="29436-129">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="29436-130">In diesen Projekten verwendet NuGet die Informationen direkt in der `.csproj`-Datei.</span><span class="sxs-lookup"><span data-stu-id="29436-130">In those .NET Core projects, NuGet uses information in the `.csproj` file directly.</span></span> <span data-ttu-id="29436-131">Weitere Informationen finden Sie unter [Create .NET Standard Packages with Visual Studio 2017 (Erstellen von .NET Standard-Paketen mit Visual Studio 2017)](../guides/create-net-standard-packages-vs2017.md) und [NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ als MSBuild-Ziele)](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="29436-131">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="29436-132">Welche Assemblys sollen gepackt werden?</span><span class="sxs-lookup"><span data-stu-id="29436-132">Deciding which assemblies to package</span></span>

<span data-ttu-id="29436-133">Die meisten allgemeinen Pakete enthalten mindestens eine Assembly, die andere Entwickler in ihren eigenen Projekten verwenden können.</span><span class="sxs-lookup"><span data-stu-id="29436-133">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="29436-134">Es ist empfehlenswert, in jedem NuGet-Paket eine Assembly zu haben, vorausgesetzt, dass jede Assembly für sich nützlich ist.</span><span class="sxs-lookup"><span data-stu-id="29436-134">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="29436-135">Beispiel: Wenn `Utilities.dll` von `Parser.dll` abhängt und `Parser.dll` für sich allein bereits nützlich ist, dann müssen Sie für jede Datei ein eigenes Paket erstellen.</span><span class="sxs-lookup"><span data-stu-id="29436-135">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="29436-136">So können Entwickler `Parser.dll` unabhängig von `Utilities.dll` verwenden.</span><span class="sxs-lookup"><span data-stu-id="29436-136">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="29436-137">Wenn Ihre Bibliothek aus mehreren Assemblys besteht, die für sich allein nicht nützlich sind, können diese in einem Paket zusammengefasst werden.</span><span class="sxs-lookup"><span data-stu-id="29436-137">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="29436-138">Bleiben wir beim vorherigen Beispiel: Wenn `Parser.dll` Code enthält, der nur von `Utilities.dll` verwendet wird, kann `Parser.dll` in dasselbe Paket eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="29436-138">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>
    - <span data-ttu-id="29436-139">Auch `Utilities.dll` und `Utilities.resources.dll` können im selben Paket zusammengefasst werden, wenn erstere DLL von der letzteren abhängt und die letztere nicht für sich allein nützlich ist.</span><span class="sxs-lookup"><span data-stu-id="29436-139">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="29436-140">Ressourcen hingegen sind ein besonderer Fall.</span><span class="sxs-lookup"><span data-stu-id="29436-140">Resources are, in fact, a special case.</span></span> <span data-ttu-id="29436-141">Wenn ein Paket in einem Projekt installiert wird, fügt NuGet automatisch den DLLs des Pakets Assemblyverweise hinzu. Die Verweise, die mit `.resources.dll` benannt sind, werden dabei allerdings *nicht* hinzugefügt, da angenommen wird, dass es sich dabei um lokalisierte Satellitenassemblys handelt. Weitere Informationen finden Sie unter [Creating localized NuGet packages (Erstellen lokalisierter NuGet-Pakete)](creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="29436-141">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="29436-142">Vermeiden Sie aus diesem Grund die Verwendung von `.resources.dll` für Dateien, die darüber hinaus wichtigen Paketcode enthalten.</span><span class="sxs-lookup"><span data-stu-id="29436-142">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="29436-143">Wenn Ihre Bibliothek COM-Interop-Assemblys enthält, führen Sie die zusätzlichen Schritte unter [Erstellen von Paketen, die COM-Interop-Assemblys enthalten](#authoring-packages-with-com-interop-assemblies) aus.</span><span class="sxs-lookup"><span data-stu-id="29436-143">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="29436-144">Rolle und Struktur der NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="29436-144">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="29436-145">Nachdem Sie entschieden haben, welche Dateien gepackt werden sollen, erstellen Sie ein Paketmanifest in einer `.nuspec`-XML-Datei.</span><span class="sxs-lookup"><span data-stu-id="29436-145">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="29436-146">Das Manifest:</span><span class="sxs-lookup"><span data-stu-id="29436-146">The manifest:</span></span>

1. <span data-ttu-id="29436-147">Beschreibt den Inhalt des Pakets und ist im Paket enthalten.</span><span class="sxs-lookup"><span data-stu-id="29436-147">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="29436-148">Ist unerlässlich für die Erstellung des Pakets und weist NuGet an, wie das Paket in ein Projekt installiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="29436-148">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="29436-149">Das Manifest erkennt z.B. andere Paketabhängigkeiten, sodass NuGet bei der Installation des Hauptpakets auch diese installieren kann.</span><span class="sxs-lookup"><span data-stu-id="29436-149">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="29436-150">Enthält wie unten beschrieben erforderliche und optionale Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="29436-150">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="29436-151">Weitere Informationen, einschließlich anderer Eigenschaften, die hier nicht erwähnt werden, finden Sie unter [.nuspec reference (NUSPEC-Referenz)](../schema/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="29436-151">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../schema/nuspec.md).</span></span>

<span data-ttu-id="29436-152">Erforderliche Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="29436-152">Required properties:</span></span>

- <span data-ttu-id="29436-153">Der Paketbezeichner. Dieser muss im Katalog, der das Paket hostet, eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="29436-153">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="29436-154">Eine bestimmte Versionsnummer in der Schreibweise *Hauptversion.Nebenversion.Patch[-Suffix]*, wobei im *-Suffix* die [Vorabversionen](Prerelease-Packages.md) angegeben werden</span><span class="sxs-lookup"><span data-stu-id="29436-154">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](Prerelease-Packages.md)</span></span>
- <span data-ttu-id="29436-155">Der Titel des Pakets, so wie er auf dem Host (z.B. „nuget.org“) angezeigt werden sollte</span><span class="sxs-lookup"><span data-stu-id="29436-155">The package title as it should appears on the host (like nuget.org)</span></span>
- <span data-ttu-id="29436-156">Informationen zum Autor und zum Besitzer</span><span class="sxs-lookup"><span data-stu-id="29436-156">Author and owner information.</span></span>
- <span data-ttu-id="29436-157">Eine ausführliche Beschreibung des Pakets</span><span class="sxs-lookup"><span data-stu-id="29436-157">A long description of the package.</span></span>

<span data-ttu-id="29436-158">Allgemeine optionale Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="29436-158">Common optional properties:</span></span>

- <span data-ttu-id="29436-159">Anmerkungen zu diesem Release</span><span class="sxs-lookup"><span data-stu-id="29436-159">Release notes</span></span>
- <span data-ttu-id="29436-160">Copyrightinformationen</span><span class="sxs-lookup"><span data-stu-id="29436-160">Copyright information</span></span>
- <span data-ttu-id="29436-161">Eine kurze Beschreibung der [Paket-Manager-UI in Visual Studio](../Tools/Package-Manager-UI.md)</span><span class="sxs-lookup"><span data-stu-id="29436-161">A short description for the [Package Manager UI in Visual Studio](../Tools/Package-Manager-UI.md)</span></span>
- <span data-ttu-id="29436-162">Eine Gebietsschema-ID</span><span class="sxs-lookup"><span data-stu-id="29436-162">A locale ID</span></span>
- <span data-ttu-id="29436-163">URL der Startseite und der Lizenz</span><span class="sxs-lookup"><span data-stu-id="29436-163">Home page and license URLs</span></span>
- <span data-ttu-id="29436-164">Eine URL für das Symbol</span><span class="sxs-lookup"><span data-stu-id="29436-164">An icon URL</span></span>
- <span data-ttu-id="29436-165">Listen der Abhängigkeiten und Verweise</span><span class="sxs-lookup"><span data-stu-id="29436-165">Lists of dependencies and references</span></span>
- <span data-ttu-id="29436-166">Tags für die Katalogsuche</span><span class="sxs-lookup"><span data-stu-id="29436-166">Tags that assist in gallery searches</span></span>

<span data-ttu-id="29436-167">Im folgenden Beispiel sehen Sie eine typische, aber fiktive `.nuspec`-Datei mit Kommentaren, die die Eigenschaften beschreiben:</span><span class="sxs-lookup"><span data-stu-id="29436-167">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- The identifier that must be unique within the hosting gallery -->
    <id>Contoso.Utility.UsefulStuff</id>

    <!-- The package version number that is used when resolving dependencies -->
    <version>1.8.3-beta</version>

    <!-- Authors contain text that appears directly on the gallery -->
    <authors>Dejana Tesic, Rajeev Dey</authors>

    <!-- Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  -->
    <owners>dejanatc, rjdey</owners>

    <!-- License and project URLs provide links for the gallery -->
    <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
    <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

    <!-- The icon is used in Visual Studio's package manager UI -->
    <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

    <!-- If true, this value prompts the user to accept the license when
            installing the package. -->
    <requireLicenseAcceptance>false</requireLicenseAcceptance>

    <!-- Any details about this particular release -->
    <releaseNotes>Bug fixes and performance improvements</releaseNotes>

    <!-- The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. -->
    <description>Core utility functions for web applications</description>

    <!-- Copyright information -->
    <copyright>Copyright ©2016 Contoso Corporation</copyright>

    <!-- Tags appear in the gallery and can be used for tag searches -->
    <tags>web utility http json url parsing</tags>

    <!-- Dependencies are automatically installed when the package is installed -->
    <dependencies>
        <dependency id="Newtonsoft.Json" version="9.0" />
    </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

<span data-ttu-id="29436-168">Weitere Informationen zum Deklarieren von Abhängigkeiten und zum Angeben von Versionsnummern finden Sie unter [Package versioning (Paketversionsverwaltung)](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="29436-168">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="29436-169">Es ist auch möglich, Ressourcen aus Abhängigkeiten mithilfe der Attribute `include` und `exclude` des Elements `dependency` direkt im Paket verfügbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="29436-169">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="29436-170">Informationen dazu finden Sie unter [.nuspec Reference – Dependencies (NUSPEC-Referenz: Abhängigkeiten)](../Schema/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="29436-170">See [.nuspec Reference - Dependencies](../Schema/nuspec.md#dependencies).</span></span>

<span data-ttu-id="29436-171">Da das Manifest im Paket enthalten ist, aus dem es erstellt wurde, finden Sie viele weitere Beispiele in den vorhandenen Paketen.</span><span class="sxs-lookup"><span data-stu-id="29436-171">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="29436-172">Eine gute Quelle ist z.B. der globale Paketcache auf Ihrem Computer, der sich mithilfe des folgenden Befehls öffnen lässt:</span><span class="sxs-lookup"><span data-stu-id="29436-172">A good source is the global package cache on your machine, the location of which is returned by the following command:</span></span>

```
nuget locals -list global-packages
```

<span data-ttu-id="29436-173">Wechseln Sie in einen Ordner unter *package\version*, kopieren die `.nupkg`- in eine `.zip`-Datei, öffnen Sie dann die `.zip`-Datei, und sehen Sie sich die `.nuspec`-Datei darin an.</span><span class="sxs-lookup"><span data-stu-id="29436-173">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="29436-174">Wenn Sie eine `.nuspec`-Datei aus einem Visual Studio-Projekt erstellen, enthält das Manifest Tokens, die bei der Paketerstellung durch Informationen aus dem Projekt ersetzt werden.</span><span class="sxs-lookup"><span data-stu-id="29436-174">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="29436-175">Weitere Informationen finden Sie im Abschnitt [Aus einem Visual Studio-Projekt](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="29436-175">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="29436-176">Erstellen der NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="29436-176">Creating the .nuspec file</span></span>

<span data-ttu-id="29436-177">Das Erstellen eines vollständigen Manifests beginnt in der Regel mit einer einfachen `.nuspec`-Datei, die mithilfe einer der folgenden Methoden generiert wird:</span><span class="sxs-lookup"><span data-stu-id="29436-177">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="29436-178">einem konventionsbasierten Arbeitsverzeichnis</span><span class="sxs-lookup"><span data-stu-id="29436-178">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="29436-179">einer Assembly-DLL</span><span class="sxs-lookup"><span data-stu-id="29436-179">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="29436-180">einem Visual Studio-Projekt</span><span class="sxs-lookup"><span data-stu-id="29436-180">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="29436-181">einer neuen Datei mit Standardwerten</span><span class="sxs-lookup"><span data-stu-id="29436-181">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="29436-182">Anschließend bearbeiten Sie die Datei manuell, sodass sie den genauen Inhalt beschreibt, den das letzte Paket enthalten soll.</span><span class="sxs-lookup"><span data-stu-id="29436-182">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="29436-183">Generierte `.nuspec`-Dateien enthalten Platzhalter. Diese müssen geändert werden, bevor das Paket mit dem Befehl `nuget pack` erstellt wird,</span><span class="sxs-lookup"><span data-stu-id="29436-183">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="29436-184">da dieser fehlschlägt, wenn die `.nuspec`-Datei Platzhalter enthält.</span><span class="sxs-lookup"><span data-stu-id="29436-184">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="29436-185">Aus einem konventionsbasierten Arbeitsverzeichnis</span><span class="sxs-lookup"><span data-stu-id="29436-185">From a convention-based working directory</span></span>

<span data-ttu-id="29436-186">Da ein NuGet-Paket nur eine mit der `.nupkg`-Erweiterung umbenannte ZIP-Datei ist, ist es oftmals am einfachsten, die gewünschte Ordnerstruktur im Dateisystem und die `.nuspec`-Datei anschließend direkt aus dieser Struktur zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="29436-186">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, its often easiest to create the folder structure you want on the file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="29436-187">Der Befehl `nuget pack` fügt dann automatisch alle Dateien in dieser Ordnerstruktur ein (außer den Ordnern, die mit einem `.` beginnen, sodass private Dateien in der gleichen Struktur bleiben können).</span><span class="sxs-lookup"><span data-stu-id="29436-187">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you keep private files in the same structure).</span></span>

<span data-ttu-id="29436-188">Der Vorteil dieses Ansatzes ist, dass Sie nicht wie weiter unten in diesem Thema erläutert im Manifest angeben müssen, welche Dateien im Paket enthalten sein sollen.</span><span class="sxs-lookup"><span data-stu-id="29436-188">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="29436-189">Sie können einfach beim Buildprozess die genaue Ordnerstruktur für das Paket erstellen lassen und problemlos weitere Dateien aufnehmen, die andernfalls zu keinem Projekt gehören würden:</span><span class="sxs-lookup"><span data-stu-id="29436-189">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="29436-190">Inhalt und Quellcode, der in das Zielprojekt eingefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="29436-190">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="29436-191">PowerShell-Skripts (in NuGet 2.x verwendete Pakete können auch Installationsskripts enthalten, die in NuGet 3.x und höher nicht unterstützt werden).</span><span class="sxs-lookup"><span data-stu-id="29436-191">PowerShell scripts (packages used in NuGet 2.x can include installation scripts as well, which is not supported in NuGet 3.x and later).</span></span>
- <span data-ttu-id="29436-192">Transformationen in vorhandene Konfigurations- und Quellcodedateien in einem Projekt.</span><span class="sxs-lookup"><span data-stu-id="29436-192">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="29436-193">Die Ordnerkonventionen lauten folgendermaßen:</span><span class="sxs-lookup"><span data-stu-id="29436-193">The folder conventions are as follows:</span></span>

| <span data-ttu-id="29436-194">Ordner</span><span class="sxs-lookup"><span data-stu-id="29436-194">Folder</span></span> | <span data-ttu-id="29436-195">description</span><span class="sxs-lookup"><span data-stu-id="29436-195">Description</span></span> | <span data-ttu-id="29436-196">Aktion bei der Paketinstallation</span><span class="sxs-lookup"><span data-stu-id="29436-196">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="29436-197">(Stammverzeichnis)</span><span class="sxs-lookup"><span data-stu-id="29436-197">(root)</span></span> | <span data-ttu-id="29436-198">Speicherort für „readme.txt“</span><span class="sxs-lookup"><span data-stu-id="29436-198">Location for readme.txt</span></span> | <span data-ttu-id="29436-199">In Visual Studio wird die Datei „readme.txt“ im Stammverzeichnis des Pakets angezeigt, wenn das Paket installiert wird.</span><span class="sxs-lookup"><span data-stu-id="29436-199">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="29436-200">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="29436-200">lib/{tfm}</span></span> | <span data-ttu-id="29436-201">Assembly- (`.dll`), Dokumentations- (`.xml`) und Symboldateien (`.pdb`) für den angegebenen Zielframeworkmoniker (Target Framework Moniker, TFM)</span><span class="sxs-lookup"><span data-stu-id="29436-201">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="29436-202">Assemblys werden als Verweise hinzugefügt, und `.xml` sowie `.pdb` werden in Projektordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="29436-202">Assemblies are added as references; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="29436-203">Informationen zum Erstellen von für das Zielframework spezifischen Unterordnern finden Sie unter [Supporting multiple .NET framework versions (Unterstützen mehrerer .NET Framework-Versionen)](Supporting-Multiple-Target-Frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="29436-203">See [Supporting multiple target frameworks](Supporting-Multiple-Target-Frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="29436-204">Laufzeiten</span><span class="sxs-lookup"><span data-stu-id="29436-204">runtimes</span></span> | <span data-ttu-id="29436-205">Architekturspezifische Assembly- (`.dll`), Symbol- (`.pdb`) und native Ressourcendateien (`.pri`)</span><span class="sxs-lookup"><span data-stu-id="29436-205">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="29436-206">Assemblys werden als Verweise hinzugefügt. Andere Dateien werden in Projektordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="29436-206">Assemblies are added as references; other files are copied into project folders.</span></span> <span data-ttu-id="29436-207">Weitere Informationen finden Sie unter [Supporting multiple .NET framework versions (Unterstützen mehrerer .NET Framework-Versionen)](Supporting-Multiple-Target-Frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="29436-207">See [Supporting multiple target frameworks](Supporting-Multiple-Target-Frameworks.md).</span></span> |
| <span data-ttu-id="29436-208">Inhalt</span><span class="sxs-lookup"><span data-stu-id="29436-208">content</span></span> | <span data-ttu-id="29436-209">Beliebige Dateien</span><span class="sxs-lookup"><span data-stu-id="29436-209">Arbitrary files</span></span> | <span data-ttu-id="29436-210">Inhalte werden in das Projektstammverzeichnis kopiert.</span><span class="sxs-lookup"><span data-stu-id="29436-210">Contents are copied to the project root.</span></span> <span data-ttu-id="29436-211">Der Ordner **content** (Inhalt) entspricht in etwa dem Stammverzeichnis der Zielanwendung, die das Paket letztendlich nutzt.</span><span class="sxs-lookup"><span data-stu-id="29436-211">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="29436-212">Damit das Paket dem Ordner */images* der Anwendung ein Image hinzufügt, müssen Sie es im Ordner *content/images* ablegen.</span><span class="sxs-lookup"><span data-stu-id="29436-212">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="29436-213">Build</span><span class="sxs-lookup"><span data-stu-id="29436-213">build</span></span> | <span data-ttu-id="29436-214">MSBuild-Dateien `.targets` und `.props`</span><span class="sxs-lookup"><span data-stu-id="29436-214">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="29436-215">Sie werden automatisch in die Projektdatei (NuGet 2.x) oder in `project.lock.json` (NuGet 3.x+) eingefügt.</span><span class="sxs-lookup"><span data-stu-id="29436-215">Automatically inserted into the project file (NuGet 2.x) or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="29436-216">Tools</span><span class="sxs-lookup"><span data-stu-id="29436-216">tools</span></span> | <span data-ttu-id="29436-217">PowerShell-Skripts und -Programme, auf die über die Paket-Manager-Konsole zugegriffen werden kann</span><span class="sxs-lookup"><span data-stu-id="29436-217">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="29436-218">Der Ordner `tools` wird nur zur Umgebungsvariable `PATH` der Paket-Manager-Konsole hinzugefügt, *niemals* jedoch zu `PATH`, so wie es für MSBuild beim Erstellen des Projekts festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="29436-218">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="29436-219">Da die Ordnerstruktur beliebig viele Assemblys für beliebig viele Zielframeworks enthalten kann, ist diese Methode für das Erstellen von Paketen erforderlich, die mehrere Frameworks unterstützen.</span><span class="sxs-lookup"><span data-stu-id="29436-219">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks</span></span> 

<span data-ttu-id="29436-220">Sobald Sie die gewünschte Ordnerstruktur eingerichtet haben, führen Sie den folgenden Befehl in diesem Ordner aus, um die `.nuspec`-Datei zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="29436-220">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```
nuget spec
```

<span data-ttu-id="29436-221">Die generierte `.nuspec`-Datei enthält wie bereits erwähnt keine expliziten Verweise auf Dateien in der Ordnerstruktur.</span><span class="sxs-lookup"><span data-stu-id="29436-221">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="29436-222">NuGet schließt bei der Paketerstellung automatisch alle Dateien ein.</span><span class="sxs-lookup"><span data-stu-id="29436-222">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="29436-223">Die Platzhalterwerte müssen jedoch trotzdem noch in anderen Teilen des Manifests bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="29436-223">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="29436-224">Aus einer Assembly-DLL</span><span class="sxs-lookup"><span data-stu-id="29436-224">From an assembly DLL</span></span>

<span data-ttu-id="29436-225">Das Erstellen eines Pakets aus einer Assembly ist ein einfacher Vorgang. Dabei können Sie eine `.nuspec`-Datei aus den Metadaten in der Assembly mithilfe des folgenden Befehls generieren:</span><span class="sxs-lookup"><span data-stu-id="29436-225">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```
nuget spec <assembly-name>.dll
```

<span data-ttu-id="29436-226">Bei dieser Schreibweise werden einige Platzhalter im Manifest durch bestimmte Werte aus der Assembly ersetzt.</span><span class="sxs-lookup"><span data-stu-id="29436-226">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="29436-227">Die Eigenschaft `<id>` wird beispielsweise auf den Assemblynamen festgelegt und `<version>` auf die Version.</span><span class="sxs-lookup"><span data-stu-id="29436-227">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="29436-228">Andere Manifesteigenschaften haben jedoch keine übereinstimmenden Werte in der Assembly und enthalten somit weiterhin Platzhalter.</span><span class="sxs-lookup"><span data-stu-id="29436-228">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="29436-229">Aus einem Visual Studio-Projekt</span><span class="sxs-lookup"><span data-stu-id="29436-229">From a Visual Studio project</span></span>

<span data-ttu-id="29436-230">Es empfiehlt sich, eine `.nuspec`-Datei aus einer `.csproj`- oder `.vbproj`-Datei zu erstellen, da auf andere Pakete, die in dieses Projekt installiert wurden, automatisch als Abhängigkeiten verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="29436-230">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="29436-231">Verwenden Sie einfach den folgenden Befehl im Ordner der Projektdatei:</span><span class="sxs-lookup"><span data-stu-id="29436-231">Simply use the following command in the same folder as the project file:</span></span>

```
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="29436-232">Die anschließend erstellte `<project-name>.nuspec`-Datei enthält *Tokens*, die zur Packzeit durch Werte aus dem Projekt ersetzt werden, einschließlich der Verweise auf alle anderen Pakete, die bereits installiert wurden.</span><span class="sxs-lookup"><span data-stu-id="29436-232">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="29436-233">Ein Token wird auf beiden Seiten der Projekteigenschaft durch das Symbol `$` begrenzt.</span><span class="sxs-lookup"><span data-stu-id="29436-233">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="29436-234">Wird der Wert `<id>` auf diese Weise in einem Manifest generiert, wird er in der Regel folgendermaßen angezeigt:</span><span class="sxs-lookup"><span data-stu-id="29436-234">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="29436-235">Dieses Token wird zur Packzeit durch den Wert `AssemblyName` aus der Projektdatei ersetzt.</span><span class="sxs-lookup"><span data-stu-id="29436-235">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="29436-236">Weitere Informationen zur genauen Zuordnung von Projektwerten und `.nuspec`-Tokens finden Sie im Abschnitt [Replacement tokens (Ersetzungstokens)](../schema/nuspec.md#replacement-tokens) im Artikel „.nuspec reference“ (NUSPEC-Referenz).</span><span class="sxs-lookup"><span data-stu-id="29436-236">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../schema/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="29436-237">Durch Tokens müssen Sie wichtige Werte wie die Versionsnummer in der `.nuspec`-Datei nicht mit dem Projekt zusammen aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="29436-237">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="29436-238">Sie können die Tokens bei Bedarf jederzeit durch Literalwerte ersetzen.</span><span class="sxs-lookup"><span data-stu-id="29436-238">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="29436-239">Wenn Sie in einem Visual Studio-Projekt arbeiten, haben weitere Packoptionen zur Auswahl. Dies wird weiter unten im Abschnitt [Ausführen von „nuget pack“ zum Generieren der NUPKG-Datei](#running-nuget-pack-to-generate-the-nupkg-file) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="29436-239">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="29436-240">Pakete auf Projektmappenebene</span><span class="sxs-lookup"><span data-stu-id="29436-240">Solution-level packages</span></span>

<span data-ttu-id="29436-241">*Nur NuGet 2.x. Nicht verfügbar in NuGet 3.0 und höher.*</span><span class="sxs-lookup"><span data-stu-id="29436-241">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="29436-242">In NuGet 2.x werden Pakete auf Projektmappenebene unterstützt, über die Tools oder zusätzliche Befehle für die Paket-Manager-Konsole installiert werden (der Inhalt des Ordners `tools`), die jedoch weder Verweise noch Inhalt hinzufügen oder Anpassungen für Projekte in der Projektmappe erstellen.</span><span class="sxs-lookup"><span data-stu-id="29436-242">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="29436-243">Solche Pakete enthalten keine Dateien in den direkten Ordnern `lib`, `content` oder `build`, und keine der dazugehörigen Abhängigkeiten besitzt Dateien in den jeweiligen `lib`-, `content`- oder `build`-Ordnern.</span><span class="sxs-lookup"><span data-stu-id="29436-243">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span> 

<span data-ttu-id="29436-244">NuGet verfolgt installierte Pakete auf Projektmappenebene in einer `packages.config`-Datei im Ordner `.nuget` nach, statt in der `packages.config`-Datei des Projekts.</span><span class="sxs-lookup"><span data-stu-id="29436-244">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="29436-245">Neue Datei mit Standardwerten</span><span class="sxs-lookup"><span data-stu-id="29436-245">New file with default values</span></span>

<span data-ttu-id="29436-246">Mit dem folgenden Befehl wird ein Standardmanifest mit Platzhaltern erstellt, das gewährleistet, dass Sie mit der richtigen Dateistruktur beginnen:</span><span class="sxs-lookup"><span data-stu-id="29436-246">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```
nuget spec [<package-name>]
```

<span data-ttu-id="29436-247">Wenn Sie \<package-name\> weglassen, lautet die Ergebnisdatei `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="29436-247">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="29436-248">Wenn Sie einen Namen wie `Contoso.Utility.UsefulStuff` angeben, lautet die Datei `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="29436-248">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="29436-249">Die resultierende `.nuspec`-Datei enthält Platzhalter für Werte wie `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="29436-249">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="29436-250">Denken Sie daran, die Datei zu bearbeiten, bevor Sie mit ihr die endgültige `.nupkg`-Datei erstellen.</span><span class="sxs-lookup"><span data-stu-id="29436-250">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="29436-251">Auswählen eines eindeutigen Paketbezeichners und Festlegen der Versionsnummer</span><span class="sxs-lookup"><span data-stu-id="29436-251">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="29436-252">Der Paketbezeichner (`<id>`-Element) und die Versionsnummer (`<version>`-Element) sind die beiden wichtigsten Werte im Manifest, da sie eindeutig den exakten Code bezeichnen, der im Paket enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="29436-252">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="29436-253">**Bewährte Methoden für den Paketbezeichner:**</span><span class="sxs-lookup"><span data-stu-id="29436-253">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="29436-254">**Eindeutigkeit:** Der Bezeichner muss auf „nuget.org“ bzw. in dem Katalog, in dem das Paket gehostet wird, eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="29436-254">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="29436-255">Bevor Sie sich für einen Bezeichner entscheiden, vergewissern Sie sich, dass dieser im entsprechenden Katalog nicht bereits verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="29436-255">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="29436-256">Zur Vermeidung von Konflikten empfiehlt es sich, den Namen Ihres Unternehmens im ersten Teil des Bezeichners zu nutzen, z.B. `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="29436-256">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="29436-257">**Namespace-ähnliche Namen:** Verwenden Sie Punkte statt Bindestrichen, wie bei der Notation von Namespaces in .NET.</span><span class="sxs-lookup"><span data-stu-id="29436-257">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="29436-258">Schreiben Sie z.B. `Contoso.Utility.UsefulStuff` statt `Contoso-Utility-UsefulStuff` oder `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="29436-258">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="29436-259">Benutzer finden es auch hilfreich, wenn der Paketbezeichner den im Code verwendeten Namespaces entspricht.</span><span class="sxs-lookup"><span data-stu-id="29436-259">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="29436-260">**Beispielpakete:** Wenn Sie ein Paket mit Beispielcode erstellen, das veranschaulicht, wie ein anderes Paket verwenden, fügen Sie `.Sample` als Suffix an den Bezeichner an, z.B. `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="29436-260">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="29436-261">Das Beispielpaket würde natürlich vom anderen Paket abhängen. Verwenden Sie beim Erstellen eines Beispielpakets wie weiter oben beschrieben das konventionsbasierte Arbeitsverzeichnis.</span><span class="sxs-lookup"><span data-stu-id="29436-261">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="29436-262">Arrangieren Sie den Beispielcode im Ordner `content` in einem Ordner namens `\Samples\<identifier>`, z.B. `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="29436-262">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="29436-263">**Bewährte Methoden für die Paketversion:**</span><span class="sxs-lookup"><span data-stu-id="29436-263">**Best practices for the package version:**</span></span>

- <span data-ttu-id="29436-264">Legen Sie die Version des Pakets auf die der Bibliothek fest, obwohl dies nicht zwingend erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="29436-264">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="29436-265">Dies ist sehr einfach, wenn Sie ein Paket, wie zuvor im Abschnitt [Welche Assemblys sollen gepackt werden?](#deciding-which-assemblies-to-package) beschrieben, auf eine einzelne Assembly beschränken.</span><span class="sxs-lookup"><span data-stu-id="29436-265">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="29436-266">Bedenken Sie, dass NuGet sich beim Auflösen der Abhängigkeiten nach den Paketversionen richtet, nicht nach den Assemblyversionen.</span><span class="sxs-lookup"><span data-stu-id="29436-266">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="29436-267">Wenn Sie ein nicht standardmäßiges Versionsschema verwenden, müssen Sie die NuGet-Versionsregeln wie unter [Package versioning (Paketversionsverwaltung](../reference/package-versioning.md) beschrieben anwenden.</span><span class="sxs-lookup"><span data-stu-id="29436-267">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="29436-268">Die folgenden kurzen Blogbeiträge enthalten weitere Informationen zur Versionsverwaltung:</span><span class="sxs-lookup"><span data-stu-id="29436-268">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="29436-269">Part 1: Taking on DLL Hell (Teil 1: DLLs)</span><span class="sxs-lookup"><span data-stu-id="29436-269">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="29436-270">Part 2: The core algorithm (Teil 2: Der Kernalgorithmus)</span><span class="sxs-lookup"><span data-stu-id="29436-270">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="29436-271">Part 3: Unification via Binding Redirects (Teil 3: Vereinheitlichung über Bindungsumleitungen)</span><span class="sxs-lookup"><span data-stu-id="29436-271">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a><span data-ttu-id="29436-272">Festlegen eines Pakettyps</span><span class="sxs-lookup"><span data-stu-id="29436-272">Setting a package type</span></span>

<span data-ttu-id="29436-273">In NuGet 3.5 und höher können Pakete mit einem bestimmten *Pakettyp* gekennzeichnet werden, um den vorgesehenen Zweck anzugeben.</span><span class="sxs-lookup"><span data-stu-id="29436-273">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="29436-274">Pakete ohne Typ, einschließlich aller mit früheren Versionen von NuGet erstellten Pakete, haben standardmäßig den Typ `Dependency`.</span><span class="sxs-lookup"><span data-stu-id="29436-274">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="29436-275">Pakete mit Typ `Dependency` fügen Bibliotheken und Anwendungen Build- oder Laufzeitressourcen hinzu und können in jedem Projekttyp installiert werden, wenn sie kompatibel sind.</span><span class="sxs-lookup"><span data-stu-id="29436-275">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="29436-276">Pakete mit Typ `DotnetCliTool` sind Erweiterungen der [.NET-CLI](/dotnet/articles/core/tools/index) und werden über die Befehlszeile aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="29436-276">`DotnetCliTool` type packages are extensions to the [.NET CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="29436-277">Solche Pakete können nur in .NET Core-Projekten installiert werden und haben keine Auswirkungen auf Wiederherstellungsvorgänge.</span><span class="sxs-lookup"><span data-stu-id="29436-277">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="29436-278">Weitere Informationen zu diesen projektspezifischen Erweiterungen finden Sie in der Dokumentation zur [.NET Core-Erweiterbarkeit](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).</span><span class="sxs-lookup"><span data-stu-id="29436-278">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

    <span data-ttu-id="29436-279">Wenn ein DotnetCliTool-Paket installiert wurde, fügt Visual Studio das Paket in den Knoten `project.json` `tools` ein, nicht in den Knoten `dependencies`.</span><span class="sxs-lookup"><span data-stu-id="29436-279">When a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

- <span data-ttu-id="29436-280">Pakete des benutzerdefinierten Typs verwenden einen willkürlichen Typbezeichner, der den gleichen Formatierungsregeln wie Paketbezeichner unterliegt.</span><span class="sxs-lookup"><span data-stu-id="29436-280">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="29436-281">Der NuGet-Paket-Manager in Visual Studio erkennt jedoch nur die Typen `Dependency` und `DotnetCliTool`.</span><span class="sxs-lookup"><span data-stu-id="29436-281">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="29436-282">Pakettypen werden entweder in der `.nuspec`-Datei oder in `project.json` festgelegt.</span><span class="sxs-lookup"><span data-stu-id="29436-282">Package types are set either in the `.nuspec` file or in `project.json`.</span></span> <span data-ttu-id="29436-283">In beiden Fällen empfiehlt es sich für die Abwärtskompatibilität, den `Dependency`-Typ *nicht* explizit festzulegen und stattdessen NuGet entscheiden zu lassen, wenn kein Typ angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="29436-283">In both cases, it's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="29436-284">`.nuspec`: Geben Sie den Pakettyp innerhalb eines `packageTypes\packageType`-Knotens unter dem `<metadata>`-Element an:</span><span class="sxs-lookup"><span data-stu-id="29436-284">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

- <span data-ttu-id="29436-285">`project.json`: Geben Sie den Pakettyp innerhalb einer JSON-formatierten `packOptions.packageType`-Eigenschaft an:</span><span class="sxs-lookup"><span data-stu-id="29436-285">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="29436-286">Hinzufügen einer Infodatei und anderer Dateien</span><span class="sxs-lookup"><span data-stu-id="29436-286">Adding a readme and other files</span></span>

<span data-ttu-id="29436-287">Verwenden Sie den `<files>`-Knoten in der `.nuspec`-Datei, die dem `<metadata>`-Tag *folgt*, um Dateien, die in das Paket aufgenommen werden sollen, direkt anzugeben:</span><span class="sxs-lookup"><span data-stu-id="29436-287">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
    <!-- Add a readme -->
    <file src="readme.txt" target="" />

    <!-- Add files from an arbitrary folder that's not necessarily in the project -->
    <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> <span data-ttu-id="29436-288">Bei einem konventionsbasierten Arbeitsverzeichnis können Sie die Datei „readme.txt“ im Stammverzeichnis des Pakets und andere Inhalte im Ordner `content` platzieren.</span><span class="sxs-lookup"><span data-stu-id="29436-288">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="29436-289">Dazu sind keine `<file>`-Elemente im Manifest erforderlich.</span><span class="sxs-lookup"><span data-stu-id="29436-289">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="29436-290">Wenn Sie eine Datei namens `readme.txt` im Stammverzeichnis des Pakets einschließen, zeigt Visual Studio unmittelbar nach der direkten Installation des Pakets den Inhalt der Datei als Nur-Text an.</span><span class="sxs-lookup"><span data-stu-id="29436-290">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="29436-291">Für Pakete, die als Abhängigkeiten installiert wurden, werden keine Infodateien angezeigt.</span><span class="sxs-lookup"><span data-stu-id="29436-291">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="29436-292">Die Infodatei für das Paket „HtmlAgilityPack“ wird z.B. folgendermaßen angezeigt:</span><span class="sxs-lookup"><span data-stu-id="29436-292">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Anzeige einer Infodatei für ein NuGet-Paket nach der Installation](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="29436-294">Wenn Sie einen leeren `<files>`-Knoten in die `.nuspec`-Datei einschließen, fügt NuGet dem Paket keine weiteren Inhalte außer denen im Ordner `lib` hinzu.</span><span class="sxs-lookup"><span data-stu-id="29436-294">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="29436-295">Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket</span><span class="sxs-lookup"><span data-stu-id="29436-295">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="29436-296">In einigen Fällen (z.B. beim Ausführen eines benutzerdefinierten Tools oder Prozesses während des Buildvorgangs) sollten Sie benutzerdefinierte Buildziele oder -eigenschaften zu Projekten hinzufügen, die Ihr Paket nutzen.</span><span class="sxs-lookup"><span data-stu-id="29436-296">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="29436-297">Platzieren Sie dazu Dateien mit der Schreibweise `<package_id>.targets` oder `<package_id>.props` (z.B. `Contoso.Utility.UsefulStuff.targets`) im `\build`-Ordner des Projekts.</span><span class="sxs-lookup"><span data-stu-id="29436-297">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="29436-298">Dateien im `\build`-Stammverzeichnis gelten als für alle Zielframeworks geeignet.</span><span class="sxs-lookup"><span data-stu-id="29436-298">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="29436-299">Um frameworkspezifische Dateien bereitzustellen, platzieren Sie zuerst Dateien wie die folgenden in den entsprechenden Unterordnern:</span><span class="sxs-lookup"><span data-stu-id="29436-299">To provide framework-specific files, first place those within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="29436-300">Verweisen Sie dann in der `.nuspec`-Datei im `<files>`-Knoten auf diese Dateien:</span><span class="sxs-lookup"><span data-stu-id="29436-300">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
    <!-- Include everything in \build -->
    <file src="build\**" target="build" />

    <!-- Other files -->
    <!-- ... -->
    </files>
</package>
```

<span data-ttu-id="29436-301">Wenn NuGet 2.x ein Paket mit `\build`-Dateien erstellt, wird der Projektdatei ein MSBuild-`<Import>`-Element hinzufügt, das auf die `.targets`- und `.props`-Dateien zeigt.</span><span class="sxs-lookup"><span data-stu-id="29436-301">When NuGet 2.x installs a package with `\build` files, it adds an MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="29436-302">`.props` wird oben in der Projektdatei hinzugefügt und `.targets` ganz unten.</span><span class="sxs-lookup"><span data-stu-id="29436-302">(`.props` is added at the top of the project file; `.targets` is added at the bottom.)</span></span>

<span data-ttu-id="29436-303">In NuGet 3.x werden Ziele nicht zum Projekt hinzugefügt, sondern über `project.lock.json` zur Verfügung gestellt.</span><span class="sxs-lookup"><span data-stu-id="29436-303">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="29436-304">Erstellen von Paketen, die COM-Interop-Assemblys enthalten</span><span class="sxs-lookup"><span data-stu-id="29436-304">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="29436-305">Pakete, die COM-Interop-Assemblys enthalten, müssen eine entsprechende [Zieledatei](#including-msbuild-props-and-targets-in-a-package) enthalten, damit die richtigen `EmbedInteropTypes`-Metadaten zu Projekten hinzugefügt werden, die das Format „PackageReference“ verwenden.</span><span class="sxs-lookup"><span data-stu-id="29436-305">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="29436-306">Die `EmbedInteropTypes`-Metadaten sind für alle Assemblys immer FALSE, wenn „PackageReference“ verwendet wird, damit die Zieledatei diese Metadaten explizit hinzufügt.</span><span class="sxs-lookup"><span data-stu-id="29436-306">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="29436-307">Um Konflikte zu vermeiden, sollte der Name des Ziels eindeutig sein. Verwenden Sie am besten eine Kombination aus dem Paketnamen und der Assembly, die eingebettet wird, und ersetzen Sie `{InteropAssemblyName}` im folgenden Beispiel durch diesen Wert.</span><span class="sxs-lookup"><span data-stu-id="29436-307">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="29436-308">Ein weiteres Beispiel finden Sie unter [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop).</span><span class="sxs-lookup"><span data-stu-id="29436-308">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml      
<Target Name="EmbeddingAssemblyNameFromPackageId" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <PropertyGroup>
    <_InteropAssemblyFileName>{InteropAssemblyName}</_InteropAssemblyFileName>
  </PropertyGroup>
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '$(_InteropAssemblyFileName)' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="29436-309">Hinweis: Wenn Sie das `packages.config`-Verweisformat verwenden, prüfen NuGet und Visual Studio beim Hinzufügen von Verweisen zu den Assemblys aus Paketen auf COM-Interop-Assemblys und legen `EmbedInteropTypes` in der Projektdatei auf TRUE fest.</span><span class="sxs-lookup"><span data-stu-id="29436-309">Note that when using the `packages.config` reference format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="29436-310">In diesem Fall werden die Ziele überschrieben.</span><span class="sxs-lookup"><span data-stu-id="29436-310">In this case the targets are overriden.</span></span>

<span data-ttu-id="29436-311">Darüber hinaus werden die [Buildressourcen standardmäßig nicht transitiv weitergeben](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="29436-311">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="29436-312">Pakete, die dieser Beschreibung nach erstellt werden, funktionieren anders, wenn sie als transitive Abhängigkeit aus einem Projekt in einen Projektverweis gezogen werden.</span><span class="sxs-lookup"><span data-stu-id="29436-312">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="29436-313">Der Paketbenutzer kann die Weiterleitung zulassen, indem er den Standardwert „PrivateAssets“ so ändert, dass „build“ nicht enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="29436-313">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>  

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="29436-314">Ausführen von „nuget pack“ zum Generieren der NUPKG-Datei</span><span class="sxs-lookup"><span data-stu-id="29436-314">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="29436-315">Wenn Sie eine Assembly oder das konventionsbasierte Arbeitsverzeichnis verwenden, erstellen Sie ein Paket, indem Sie den Befehl `nuget pack` mit der `.nuspec`-Datei ausführen und dabei `<manifest-name>` durch den bestimmten Dateinamen ersetzen:</span><span class="sxs-lookup"><span data-stu-id="29436-315">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<manifest-name>` with your specific filename:</span></span>

```
nuget pack <project-name>.nuspec
```

<span data-ttu-id="29436-316">Wenn Sie ein Visual Studio-Projekt verwenden, führen Sie `nuget pack` mit der Projektdatei aus, die automatisch die `.nuspec`-Datei des Projekts lädt und alle Tokens darin durch die Werte in der Projektdatei ersetzt:</span><span class="sxs-lookup"><span data-stu-id="29436-316">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="29436-317">Die direkte Verwendung der Projektdatei ist für die Tokenersetzung erforderlich, da das Projekt die Quelle der Tokenwerte ist.</span><span class="sxs-lookup"><span data-stu-id="29436-317">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="29436-318">Die Tokenersetzung wird nicht ausgeführt, wenn Sie `nuget pack` mit einer `.nuspec`-Datei verwenden.</span><span class="sxs-lookup"><span data-stu-id="29436-318">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="29436-319">`nuget pack` schließt auf jeden Fall Ordner aus, die mit einem Punkt beginnen, z.B. `.git` oder `.hg`.</span><span class="sxs-lookup"><span data-stu-id="29436-319">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="29436-320">NuGet gibt an, ob die `.nuspec`-Datei Fehler enthält, die korrigiert werden müssen, z.B. nicht geänderte Platzhalterwerte im Manifest.</span><span class="sxs-lookup"><span data-stu-id="29436-320">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="29436-321">Wenn `nuget pack` erfolgreich ausgeführt wurde, können Sie die erstellte `.nupkg`-Datei wie in [Publishing packages (Veröffentlichen von Paketen)](../create-packages/publish-a-package.md) beschrieben in einem geeigneten Katalog veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="29436-321">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="29436-322">Wenn Sie sich das erstellte Paket genauer ansehen möchten, öffnen Sie es einfach im [Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer).</span><span class="sxs-lookup"><span data-stu-id="29436-322">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="29436-323">Dieser stellt den Inhalt des Pakets und das Manifest grafisch dar.</span><span class="sxs-lookup"><span data-stu-id="29436-323">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="29436-324">Sie können die resultierende `.nupkg`-Datei auch in eine `.zip`-Datei umbenennen und deren Inhalt direkt prüfen.</span><span class="sxs-lookup"><span data-stu-id="29436-324">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="29436-325">Zusätzliche Optionen</span><span class="sxs-lookup"><span data-stu-id="29436-325">Additional options</span></span>

<span data-ttu-id="29436-326">Sie können `nuget pack` mit verschiedenen Befehlszeilenparameter verwenden, um z.B. Dateien auszuschließen, die Versionsnummer im Manifest zu überschreiben und den Ausgabeordner zu ändern.</span><span class="sxs-lookup"><span data-stu-id="29436-326">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="29436-327">Eine vollständige Liste finden Sie in der [Referenz zum Packbefehl](../tools/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="29436-327">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="29436-328">Folgende Optionen werden beispielsweise häufig in Visual Studio-Projekten verwendet:</span><span class="sxs-lookup"><span data-stu-id="29436-328">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="29436-329">**Referenzierte Projekte:** Wenn das Projekt auf andere verweist, können Sie die referenzierten Projekte mithilfe der Option `-IncludeReferencedProjects` als Teil des Pakets oder als Abhängigkeiten hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="29436-329">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="29436-330">Diese Einschließung ist rekursiv. Wenn also `MyProject.csproj` auf die Projekte B und C verweist und diese Projekte ihrerseits auf die Projekte D, E und F, dann werden Dateien aus B, C, D, E und F in das Paket aufgenommen.</span><span class="sxs-lookup"><span data-stu-id="29436-330">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="29436-331">Wenn ein referenziertes Projekt selbst eine `.nuspec`-Datei enthält, fügt NuGet dieses Projekt stattdessen als Abhängigkeit hinzu.</span><span class="sxs-lookup"><span data-stu-id="29436-331">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="29436-332">Dieses Projekt muss separat gepackt und veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="29436-332">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="29436-333">**Buildkonfiguration:** NuGet verwendet die in der Projektdatei festgelegte Standardbuildkonfiguration, üblicherweise *Debuggen*.</span><span class="sxs-lookup"><span data-stu-id="29436-333">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="29436-334">Um Dateien aus einer anderen Buildkonfiguration zu packen, z.B. *Release*, verwenden Sie die Option `-properties` mit folgender Konfiguration:</span><span class="sxs-lookup"><span data-stu-id="29436-334">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="29436-335">**Symbole:** Um Symbole einzuschließen, mit denen Benutzer den Paketcode im Debugger schrittweise ausführen können, verwenden Sie die Option `-Symbols`:</span><span class="sxs-lookup"><span data-stu-id="29436-335">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="29436-336">Testen der Paketinstallation</span><span class="sxs-lookup"><span data-stu-id="29436-336">Testing package installation</span></span>

<span data-ttu-id="29436-337">Vor dem Veröffentlichen eines Pakets testen Sie in der Regel die Installation eines Pakets in einem Projekt.</span><span class="sxs-lookup"><span data-stu-id="29436-337">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="29436-338">Diese Tests stellen sicher, dass die erforderlichen Dateien an den richtigen Orten im Projekt installiert werden.</span><span class="sxs-lookup"><span data-stu-id="29436-338">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="29436-339">Installationen lassen sich manuell in Visual Studio oder mithilfe der normalen [Paketinstallationsschritte](../Quickstart/Use-a-Package.md) über die Befehlszeile testen.</span><span class="sxs-lookup"><span data-stu-id="29436-339">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../Quickstart/Use-a-Package.md).</span></span>

<span data-ttu-id="29436-340">Für automatisierte Tests gehen Sie folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="29436-340">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="29436-341">Kopieren Sie die `.nupkg`-Datei in einen lokalen Ordner.</span><span class="sxs-lookup"><span data-stu-id="29436-341">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="29436-342">Fügen Sie den Ordner mithilfe des `nuget sources -name <name> -source <path>`-Befehls den Paketquellen hinzu. Weitere Informationen finden Sie unter [sources command (NuGet CLI) (sources-Befehl (NuGet-CLI))](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="29436-342">Add the folder to your package sources using the `nuget sources -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="29436-343">Diese lokale Quelle muss auf einem Computer nur einmal festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="29436-343">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="29436-344">Installieren Sie das Paket aus dieser Quelle mithilfe von `nuget install <packageID> -source <name>`, wobei `<name>` dem Namen der Quelle entspricht, so wie er an `nuget sources` übergeben wurde.</span><span class="sxs-lookup"><span data-stu-id="29436-344">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="29436-345">Durch das Angeben der Quelle wird sichergestellt, dass das Paket nur aus dieser Quelle installiert wird.</span><span class="sxs-lookup"><span data-stu-id="29436-345">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="29436-346">Überprüfen Sie das Dateisystem, um sicherzustellen, dass Dateien richtig installiert wurden.</span><span class="sxs-lookup"><span data-stu-id="29436-346">Examine the file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29436-347">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="29436-347">Next Steps</span></span>

<span data-ttu-id="29436-348">Nachdem Sie ein Paket erstellt haben, das eine `.nupkg`-Datei ist, können Sie sie wie unter [Publishing packages (Veröffentlichen von Paketen)](../create-packages/publish-a-package.md) beschrieben im Katalog Ihrer Wahl veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="29436-348">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="29436-349">Sie können auch die Funktionen des Pakets erweitern oder wie in den folgenden Themen beschrieben andere Szenarios unterstützen:</span><span class="sxs-lookup"><span data-stu-id="29436-349">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="29436-350">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="29436-350">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="29436-351">Unterstützen mehrerer Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="29436-351">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="29436-352">Transformationen von Quell- und Konfigurationsdateien</span><span class="sxs-lookup"><span data-stu-id="29436-352">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="29436-353">Lokalisierung</span><span class="sxs-lookup"><span data-stu-id="29436-353">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="29436-354">Vorabversionen</span><span class="sxs-lookup"><span data-stu-id="29436-354">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="29436-355">Außerdem sollten Sie die folgenden zusätzlichen Pakettypen berücksichtigen:</span><span class="sxs-lookup"><span data-stu-id="29436-355">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="29436-356">Native Pakete</span><span class="sxs-lookup"><span data-stu-id="29436-356">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="29436-357">Symbolpakete</span><span class="sxs-lookup"><span data-stu-id="29436-357">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
