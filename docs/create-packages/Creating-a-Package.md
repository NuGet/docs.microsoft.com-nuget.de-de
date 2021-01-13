---
title: Erstellen eines NuGet-Pakets mithilfe der „nuget.exe“-CLI
description: Bei diesem Artikel handelt es sich um eine ausführliche Anleitung für das Entwerfen und Erstellen eines NuGet-Pakets. Außerdem finden Sie Informationen zu Dateien und zur Versionsverwaltung.
author: karann-msft
ms.author: feaguila
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: ec06a8f721b7b67ddc5d72323305b9b22f292de6
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699791"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a><span data-ttu-id="56f31-103">Erstellen eines Pakets mithilfe der „nuget.exe“-CLI</span><span class="sxs-lookup"><span data-stu-id="56f31-103">Create a package using the nuget.exe CLI</span></span>

<span data-ttu-id="56f31-104">Unabhängig davon, welchen Zweck Ihr Paket erfüllt oder welchen Code es enthält, verwenden Sie eines der CLI-Tools (entweder `nuget.exe` oder `dotnet.exe`), um diese Funktionalität in einer Komponente zu verpacken, die für andere Entwickler freigegeben und von ihnen verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="56f31-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="56f31-105">Informationen zur Installation von NuGet-CLI-Tools finden Sie unter [Installieren von NuGet-Clienttools](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="56f31-105">To install NuGet CLI tools, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="56f31-106">Beachten Sie, dass Visual Studio nicht automatisch ein CLI-Tool enthält.</span><span class="sxs-lookup"><span data-stu-id="56f31-106">Note that Visual Studio does not automatically include a CLI tool.</span></span>

- <span data-ttu-id="56f31-107">Für Projekte im Nicht-SDK-Format, in der Regel .NET Framework-Projekte, befolgen Sie die in diesem Artikel beschriebenen Schritte zum Erstellen eines Pakets.</span><span class="sxs-lookup"><span data-stu-id="56f31-107">For non-SDK-style projects, typically .NET Framework projects, follow the steps described in this article to create a package.</span></span> <span data-ttu-id="56f31-108">Eine Schritt-für-Schritt-Anleitung für die Verwendung von Visual Studio und der `nuget.exe`-CLI finden Sie unter[ Erstellen und Veröffentlichen eines .NET Framework-Pakets](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="56f31-108">For step-by-step instructions using Visual Studio and the `nuget.exe` CLI, see [Create and publish a .NET Framework package](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span></span>

- <span data-ttu-id="56f31-109">Für .NET Core- und .NET Standard-Projekte, die das [SDK-Format](../resources/check-project-format.md) verwenden, und für alle anderen Projekte im SDK-Format finden Sie weitere Informationen unter [Erstellen eines NuGet-Pakets mit der dotnet-CLI](creating-a-package-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="56f31-109">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, see [Create a NuGet package using the dotnet CLI](creating-a-package-dotnet-cli.md).</span></span>

- <span data-ttu-id="56f31-110">Für Projekte, die von `packages.config` zu [PackageReference](../consume-packages/package-references-in-project-files.md) migriert wurden, verwenden Sie [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="56f31-110">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

<span data-ttu-id="56f31-111">Technisch gesehen ist ein NuGet-Paket eine ZIP-Datei, die mit der `.nupkg`-Erweiterung umbenannt wurde und deren Inhalt bestimmten Konventionen entspricht.</span><span class="sxs-lookup"><span data-stu-id="56f31-111">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="56f31-112">In diesem Thema werden die Schritte zum Erstellen eines Pakets, das diesen Konventionen entspricht, ausführlich beschrieben.</span><span class="sxs-lookup"><span data-stu-id="56f31-112">This topic describes the detailed process of creating a package that meets those conventions.</span></span>

<span data-ttu-id="56f31-113">Das Packen beginnt mit dem kompilierten Code (Assemblys), Symbolen und/oder anderen Dateien, die Sie als Paket übermitteln möchten. Weitere Informationen finden Sie unter [Overview and workflow (Übersicht und Workflow)](overview-and-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="56f31-113">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="56f31-114">Dieser Vorgang wird unabhängig vom Kompilieren oder jeder anderen Methode zum Erstellen der Dateien ausgeführt, die in das Paket einfließen. Sie können die kompilierten Assemblys und Pakete jedoch mithilfe der Informationen in einer Projektdatei kontinuierlich synchronisieren.</span><span class="sxs-lookup"><span data-stu-id="56f31-114">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Important]
> <span data-ttu-id="56f31-115">Dieses Thema gilt für Nicht-SDK-Projekte, in der Regel andere als .NET Core- und .NET Standard-Projekte mit Visual Studio 2017 und höheren Versionen und NuGet 4.0 und höher.</span><span class="sxs-lookup"><span data-stu-id="56f31-115">This topic applies to non-SDK-style projects, typically projects other than .NET Core and .NET Standard projects using Visual Studio 2017 and higher versions and NuGet 4.0+.</span></span>

## <a name="decide-which-assemblies-to-package"></a><span data-ttu-id="56f31-116">Welche Assemblys sollten gepackt werden?</span><span class="sxs-lookup"><span data-stu-id="56f31-116">Decide which assemblies to package</span></span>

<span data-ttu-id="56f31-117">Die meisten allgemeinen Pakete enthalten mindestens eine Assembly, die andere Entwickler in ihren eigenen Projekten verwenden können.</span><span class="sxs-lookup"><span data-stu-id="56f31-117">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="56f31-118">Es ist empfehlenswert, in jedem NuGet-Paket eine Assembly zu haben, vorausgesetzt, dass jede Assembly für sich nützlich ist.</span><span class="sxs-lookup"><span data-stu-id="56f31-118">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="56f31-119">Beispiel: Wenn `Utilities.dll` von `Parser.dll` abhängt und `Parser.dll` für sich allein bereits nützlich ist, dann müssen Sie für jede Datei ein eigenes Paket erstellen.</span><span class="sxs-lookup"><span data-stu-id="56f31-119">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="56f31-120">So können Entwickler `Parser.dll` unabhängig von `Utilities.dll` verwenden.</span><span class="sxs-lookup"><span data-stu-id="56f31-120">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="56f31-121">Wenn Ihre Bibliothek aus mehreren Assemblys besteht, die für sich allein nicht nützlich sind, können diese in einem Paket zusammengefasst werden.</span><span class="sxs-lookup"><span data-stu-id="56f31-121">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="56f31-122">Bleiben wir beim vorherigen Beispiel: Wenn `Parser.dll` Code enthält, der nur von `Utilities.dll` verwendet wird, kann `Parser.dll` in dasselbe Paket eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="56f31-122">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="56f31-123">Auch `Utilities.dll` und `Utilities.resources.dll` können im selben Paket zusammengefasst werden, wenn erstere DLL von der letzteren abhängt und die letztere nicht für sich allein nützlich ist.</span><span class="sxs-lookup"><span data-stu-id="56f31-123">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="56f31-124">Ressourcen hingegen sind ein besonderer Fall.</span><span class="sxs-lookup"><span data-stu-id="56f31-124">Resources are, in fact, a special case.</span></span> <span data-ttu-id="56f31-125">Wenn ein Paket in einem Projekt installiert wird, fügt NuGet automatisch den DLLs des Pakets Assemblyverweise hinzu. Die Verweise, die mit `.resources.dll` benannt sind, werden dabei allerdings *nicht* hinzugefügt, da angenommen wird, dass es sich dabei um lokalisierte Satellitenassemblys handelt. Weitere Informationen finden Sie unter [Creating localized NuGet packages (Erstellen lokalisierter NuGet-Pakete)](creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="56f31-125">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="56f31-126">Vermeiden Sie aus diesem Grund die Verwendung von `.resources.dll` für Dateien, die darüber hinaus wichtigen Paketcode enthalten.</span><span class="sxs-lookup"><span data-stu-id="56f31-126">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="56f31-127">Wenn Ihre Bibliothek COM-Interop-Assemblys enthält, führen Sie die zusätzlichen Schritte unter [Erstellen von Paketen mit COM-Interop-Assemblys](author-packages-with-com-interop-assemblies.md) aus.</span><span class="sxs-lookup"><span data-stu-id="56f31-127">If your library contains COM interop assemblies, follow additional the guidelines in [Create packages with COM interop assemblies](author-packages-with-com-interop-assemblies.md).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="56f31-128">Rolle und Struktur der NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="56f31-128">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="56f31-129">Nachdem Sie entschieden haben, welche Dateien gepackt werden sollen, erstellen Sie ein Paketmanifest in einer `.nuspec`-XML-Datei.</span><span class="sxs-lookup"><span data-stu-id="56f31-129">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="56f31-130">Das Manifest:</span><span class="sxs-lookup"><span data-stu-id="56f31-130">The manifest:</span></span>

1. <span data-ttu-id="56f31-131">Beschreibt den Inhalt des Pakets und ist im Paket enthalten.</span><span class="sxs-lookup"><span data-stu-id="56f31-131">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="56f31-132">Ist unerlässlich für die Erstellung des Pakets und weist NuGet an, wie das Paket in ein Projekt installiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="56f31-132">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="56f31-133">Das Manifest erkennt z.B. andere Paketabhängigkeiten, sodass NuGet bei der Installation des Hauptpakets auch diese installieren kann.</span><span class="sxs-lookup"><span data-stu-id="56f31-133">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="56f31-134">Enthält wie unten beschrieben erforderliche und optionale Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="56f31-134">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="56f31-135">Weitere Informationen, einschließlich anderer Eigenschaften, die hier nicht erwähnt werden, finden Sie unter [.nuspec reference (NUSPEC-Referenz)](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="56f31-135">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="56f31-136">Erforderliche Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="56f31-136">Required properties:</span></span>

- <span data-ttu-id="56f31-137">Der Paketbezeichner. Dieser muss im Katalog, der das Paket hostet, eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="56f31-137">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="56f31-138">Eine bestimmte Versionsnummer in der Schreibweise *Hauptversion.Nebenversion.Patch[-Suffix]* , wobei im *-Suffix* die [Vorabversionen](prerelease-packages.md) angegeben werden</span><span class="sxs-lookup"><span data-stu-id="56f31-138">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="56f31-139">Der Titel des Pakets, so wie er auf dem Host (z.B. „nuget.org“) angezeigt werden sollte</span><span class="sxs-lookup"><span data-stu-id="56f31-139">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="56f31-140">Informationen zum Autor und zum Besitzer</span><span class="sxs-lookup"><span data-stu-id="56f31-140">Author and owner information.</span></span>
- <span data-ttu-id="56f31-141">Eine ausführliche Beschreibung des Pakets</span><span class="sxs-lookup"><span data-stu-id="56f31-141">A long description of the package.</span></span>

<span data-ttu-id="56f31-142">Allgemeine optionale Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="56f31-142">Common optional properties:</span></span>

- <span data-ttu-id="56f31-143">Anmerkungen zu diesem Release</span><span class="sxs-lookup"><span data-stu-id="56f31-143">Release notes</span></span>
- <span data-ttu-id="56f31-144">Copyrightinformationen</span><span class="sxs-lookup"><span data-stu-id="56f31-144">Copyright information</span></span>
- <span data-ttu-id="56f31-145">Eine kurze Beschreibung der [Paket-Manager-UI in Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="56f31-145">A short description for the [Package Manager UI in Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span></span>
- <span data-ttu-id="56f31-146">Eine Gebietsschema-ID</span><span class="sxs-lookup"><span data-stu-id="56f31-146">A locale ID</span></span>
- <span data-ttu-id="56f31-147">Projekt-URL</span><span class="sxs-lookup"><span data-stu-id="56f31-147">Project URL</span></span>
- <span data-ttu-id="56f31-148">Eine Lizenz als Ausdruck oder Datei (`licenseUrl` wird als veraltet markiert. Nutzen Sie stattdessen das [Nuspec-Metadatenelement `license`](../reference/nuspec.md#license).)</span><span class="sxs-lookup"><span data-stu-id="56f31-148">License as an expression or file (`licenseUrl` is deprecated, use [`license` nuspec metadata element](../reference/nuspec.md#license) instead)</span></span>
- <span data-ttu-id="56f31-149">Eine Symboldatei (`iconUrl` wird als veraltet markiert. Nutzen Sie stattdessen das [Nuspec-Metadatenelement `icon`](../reference/nuspec.md#icon).)</span><span class="sxs-lookup"><span data-stu-id="56f31-149">An icon file (`iconUrl` is deprecated use [`icon` nuspec metadata element](../reference/nuspec.md#icon) instead)</span></span>
- <span data-ttu-id="56f31-150">Listen der Abhängigkeiten und Verweise</span><span class="sxs-lookup"><span data-stu-id="56f31-150">Lists of dependencies and references</span></span>
- <span data-ttu-id="56f31-151">Tags für die Katalogsuche</span><span class="sxs-lookup"><span data-stu-id="56f31-151">Tags that assist in gallery searches</span></span>

<span data-ttu-id="56f31-152">Im folgenden Beispiel sehen Sie eine typische, aber fiktive `.nuspec`-Datei mit Kommentaren, die die Eigenschaften beschreiben:</span><span class="sxs-lookup"><span data-stu-id="56f31-152">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- Package version number that is used when resolving dependencies -->
        <version>1.8.3</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>
        
         <!-- Project URL provides a link for the gallery -->
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

         <!-- License information is displayed on the gallery -->
        <license type="expression">Apache-2.0</license>
        

        <!-- Icon is used in Visual Studio's package manager UI -->
        <icon>icon.png</icon>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
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
        <file src="icon.png" target="" />
    </files>
</package>
```

<span data-ttu-id="56f31-153">Weitere Informationen zum Deklarieren von Abhängigkeiten und zum Angeben von Versionsnummern finden Sie unter [packages.config](../reference/packages-config.md) und [Package versioning](../concepts/package-versioning.md) (Paketversionsverwaltung).</span><span class="sxs-lookup"><span data-stu-id="56f31-153">For details on declaring dependencies and specifying version numbers, see [packages.config](../reference/packages-config.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="56f31-154">Es ist auch möglich, Ressourcen aus Abhängigkeiten mithilfe der Attribute `include` und `exclude` des Elements `dependency` direkt im Paket verfügbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="56f31-154">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="56f31-155">Informationen dazu finden Sie unter [.nuspec Reference – Dependencies (NUSPEC-Referenz: Abhängigkeiten)](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="56f31-155">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="56f31-156">Da das Manifest im Paket enthalten ist, aus dem es erstellt wurde, finden Sie viele weitere Beispiele in den vorhandenen Paketen.</span><span class="sxs-lookup"><span data-stu-id="56f31-156">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="56f31-157">Eine gute Quelle ist z.B. der Ordner *global-packages* auf Ihrem Computer, der sich mithilfe des folgenden Befehls öffnen lässt:</span><span class="sxs-lookup"><span data-stu-id="56f31-157">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="56f31-158">Wechseln Sie in einen Ordner unter *package\version*, kopieren die `.nupkg`- in eine `.zip`-Datei, öffnen Sie dann die `.zip`-Datei, und sehen Sie sich die `.nuspec`-Datei darin an.</span><span class="sxs-lookup"><span data-stu-id="56f31-158">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="56f31-159">Wenn Sie eine `.nuspec`-Datei aus einem Visual Studio-Projekt erstellen, enthält das Manifest Tokens, die bei der Paketerstellung durch Informationen aus dem Projekt ersetzt werden.</span><span class="sxs-lookup"><span data-stu-id="56f31-159">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="56f31-160">Weitere Informationen finden Sie im Abschnitt [Aus einem Visual Studio-Projekt](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="56f31-160">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="create-the-nuspec-file"></a><span data-ttu-id="56f31-161">Erstellen der NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="56f31-161">Create the .nuspec file</span></span>

<span data-ttu-id="56f31-162">Das Erstellen eines vollständigen Manifests beginnt in der Regel mit einer einfachen `.nuspec`-Datei, die mithilfe einer der folgenden Methoden generiert wird:</span><span class="sxs-lookup"><span data-stu-id="56f31-162">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="56f31-163">einem konventionsbasierten Arbeitsverzeichnis</span><span class="sxs-lookup"><span data-stu-id="56f31-163">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="56f31-164">einer Assembly-DLL</span><span class="sxs-lookup"><span data-stu-id="56f31-164">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="56f31-165">einem Visual Studio-Projekt</span><span class="sxs-lookup"><span data-stu-id="56f31-165">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="56f31-166">einer neuen Datei mit Standardwerten</span><span class="sxs-lookup"><span data-stu-id="56f31-166">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="56f31-167">Anschließend bearbeiten Sie die Datei manuell, sodass sie den genauen Inhalt beschreibt, den das letzte Paket enthalten soll.</span><span class="sxs-lookup"><span data-stu-id="56f31-167">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="56f31-168">Generierte `.nuspec`-Dateien enthalten Platzhalter. Diese müssen geändert werden, bevor das Paket mit dem Befehl `nuget pack` erstellt wird,</span><span class="sxs-lookup"><span data-stu-id="56f31-168">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="56f31-169">da dieser fehlschlägt, wenn die `.nuspec`-Datei Platzhalter enthält.</span><span class="sxs-lookup"><span data-stu-id="56f31-169">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="56f31-170">Aus einem konventionsbasierten Arbeitsverzeichnis</span><span class="sxs-lookup"><span data-stu-id="56f31-170">From a convention-based working directory</span></span>

<span data-ttu-id="56f31-171">Da ein NuGet-Paket nur eine mit der `.nupkg`-Erweiterung umbenannte ZIP-Datei ist, ist es oftmals am einfachsten, die gewünschte Ordnerstruktur in Ihrem lokalen Dateisystem und die `.nuspec`-Datei anschließend direkt aus dieser Struktur zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="56f31-171">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="56f31-172">Der Befehl `nuget pack` fügt dann automatisch alle Dateien in dieser Ordnerstruktur ein (außer den Ordnern, die mit einem `.` beginnen, sodass private Dateien in der gleichen Struktur bleiben können).</span><span class="sxs-lookup"><span data-stu-id="56f31-172">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="56f31-173">Der Vorteil dieses Ansatzes ist, dass Sie nicht wie weiter unten in diesem Thema erläutert im Manifest angeben müssen, welche Dateien im Paket enthalten sein sollen.</span><span class="sxs-lookup"><span data-stu-id="56f31-173">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="56f31-174">Sie können einfach beim Buildprozess die genaue Ordnerstruktur für das Paket erstellen lassen und problemlos weitere Dateien aufnehmen, die andernfalls zu keinem Projekt gehören würden:</span><span class="sxs-lookup"><span data-stu-id="56f31-174">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="56f31-175">Inhalt und Quellcode, der in das Zielprojekt eingefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="56f31-175">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="56f31-176">PowerShell-Skripts</span><span class="sxs-lookup"><span data-stu-id="56f31-176">PowerShell scripts</span></span>
- <span data-ttu-id="56f31-177">Transformationen in vorhandene Konfigurations- und Quellcodedateien in einem Projekt.</span><span class="sxs-lookup"><span data-stu-id="56f31-177">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="56f31-178">Die Ordnerkonventionen lauten folgendermaßen:</span><span class="sxs-lookup"><span data-stu-id="56f31-178">The folder conventions are as follows:</span></span>

| <span data-ttu-id="56f31-179">Ordner</span><span class="sxs-lookup"><span data-stu-id="56f31-179">Folder</span></span> | <span data-ttu-id="56f31-180">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="56f31-180">Description</span></span> | <span data-ttu-id="56f31-181">Aktion bei der Paketinstallation</span><span class="sxs-lookup"><span data-stu-id="56f31-181">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="56f31-182">(Stammverzeichnis)</span><span class="sxs-lookup"><span data-stu-id="56f31-182">(root)</span></span> | <span data-ttu-id="56f31-183">Speicherort für „readme.txt“</span><span class="sxs-lookup"><span data-stu-id="56f31-183">Location for readme.txt</span></span> | <span data-ttu-id="56f31-184">In Visual Studio wird die Datei „readme.txt“ im Stammverzeichnis des Pakets angezeigt, wenn das Paket installiert wird.</span><span class="sxs-lookup"><span data-stu-id="56f31-184">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="56f31-185">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="56f31-185">lib/{tfm}</span></span> | <span data-ttu-id="56f31-186">Assembly- (`.dll`), Dokumentations- (`.xml`) und Symboldateien (`.pdb`) für den angegebenen Zielframeworkmoniker (Target Framework Moniker, TFM)</span><span class="sxs-lookup"><span data-stu-id="56f31-186">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="56f31-187">Assemblys werden als Verweise für die Kompilierzeit ebenso wie für die Laufzeit hinzugefügt, und `.xml` sowie `.pdb` werden in Projektordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="56f31-187">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="56f31-188">Informationen zum Erstellen von für das Zielframework spezifischen Unterordnern finden Sie unter [Supporting multiple .NET framework versions (Unterstützen mehrerer .NET Framework-Versionen)](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="56f31-188">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="56f31-189">ref/{tfm}</span><span class="sxs-lookup"><span data-stu-id="56f31-189">ref/{tfm}</span></span> | <span data-ttu-id="56f31-190">Dateien für Assembly (`.dll`) und Symbole (`.pdb`) für den angegebenen Zielframeworkmoniker (Target Framework Moniker, TFM)</span><span class="sxs-lookup"><span data-stu-id="56f31-190">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="56f31-191">Assemblys werden nur als Verweise für die Kompilierzeit hinzugefügt, daher werden keine Daten in den bin-Ordner des Projekts kopiert.</span><span class="sxs-lookup"><span data-stu-id="56f31-191">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="56f31-192">runtimes</span><span class="sxs-lookup"><span data-stu-id="56f31-192">runtimes</span></span> | <span data-ttu-id="56f31-193">Architekturspezifische Assembly- (`.dll`), Symbol- (`.pdb`) und native Ressourcendateien (`.pri`)</span><span class="sxs-lookup"><span data-stu-id="56f31-193">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="56f31-194">Assemblys werden nur als Verweise für die Laufzeit hinzugefügt. Andere Dateien werden in Projektordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="56f31-194">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="56f31-195">Es sollte immer eine entsprechende für `AnyCPU` spezifische TFM-Assembly im Ordner `/ref/{tfm}` vorhanden sein, um eine entsprechende Assembly für die Kompilierzeit bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="56f31-195">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="56f31-196">Weitere Informationen finden Sie unter [Supporting multiple .NET framework versions (Unterstützen mehrerer .NET Framework-Versionen)](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="56f31-196">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="56f31-197">content</span><span class="sxs-lookup"><span data-stu-id="56f31-197">content</span></span> | <span data-ttu-id="56f31-198">Beliebige Dateien</span><span class="sxs-lookup"><span data-stu-id="56f31-198">Arbitrary files</span></span> | <span data-ttu-id="56f31-199">Inhalte werden in das Projektstammverzeichnis kopiert.</span><span class="sxs-lookup"><span data-stu-id="56f31-199">Contents are copied to the project root.</span></span> <span data-ttu-id="56f31-200">Der Ordner **content** (Inhalt) entspricht in etwa dem Stammverzeichnis der Zielanwendung, die das Paket letztendlich nutzt.</span><span class="sxs-lookup"><span data-stu-id="56f31-200">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="56f31-201">Damit das Paket dem Ordner */images* der Anwendung ein Image hinzufügt, müssen Sie es im Ordner *content/images* ablegen.</span><span class="sxs-lookup"><span data-stu-id="56f31-201">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="56f31-202">build</span><span class="sxs-lookup"><span data-stu-id="56f31-202">build</span></span> | <span data-ttu-id="56f31-203">*(3.x+)* MSBuild-Dateien `.targets` und `.props`</span><span class="sxs-lookup"><span data-stu-id="56f31-203">*(3.x+)* MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="56f31-204">Wird automatisch in das Projekt eingefügt.</span><span class="sxs-lookup"><span data-stu-id="56f31-204">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="56f31-205">buildMultiTargeting</span><span class="sxs-lookup"><span data-stu-id="56f31-205">buildMultiTargeting</span></span> | <span data-ttu-id="56f31-206">*(4.0+)* MSBuild-Dateien `.targets` und `.props` für frameworkübergreifende Ziele</span><span class="sxs-lookup"><span data-stu-id="56f31-206">*(4.0+)* MSBuild `.targets` and `.props` files for cross-framework targeting</span></span> | <span data-ttu-id="56f31-207">Wird automatisch in das Projekt eingefügt.</span><span class="sxs-lookup"><span data-stu-id="56f31-207">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="56f31-208">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="56f31-208">buildTransitive</span></span> | <span data-ttu-id="56f31-209">*(5.0 und höher)* : MSBuild-Dateien `.targets` und `.props`, die transitiv in beliebige verarbeitende Projekte eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="56f31-209">*(5.0+)* MSBuild `.targets` and `.props` files that flow transitively to any consuming project.</span></span> <span data-ttu-id="56f31-210">Weitere Informationen finden Sie auf der Seite [Feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior).</span><span class="sxs-lookup"><span data-stu-id="56f31-210">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> | <span data-ttu-id="56f31-211">Wird automatisch in das Projekt eingefügt.</span><span class="sxs-lookup"><span data-stu-id="56f31-211">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="56f31-212">Tools</span><span class="sxs-lookup"><span data-stu-id="56f31-212">tools</span></span> | <span data-ttu-id="56f31-213">PowerShell-Skripts und -Programme, auf die über die Paket-Manager-Konsole zugegriffen werden kann</span><span class="sxs-lookup"><span data-stu-id="56f31-213">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="56f31-214">Der Ordner `tools` wird nur zur Umgebungsvariable `PATH` der Paket-Manager-Konsole hinzugefügt, *niemals* jedoch zu `PATH`, so wie es für MSBuild beim Erstellen des Projekts festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="56f31-214">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="56f31-215">Da die Ordnerstruktur beliebig viele Assemblys für beliebig viele Zielframeworks enthalten kann, ist diese Methode für das Erstellen von Paketen erforderlich, die mehrere Frameworks unterstützen.</span><span class="sxs-lookup"><span data-stu-id="56f31-215">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="56f31-216">Sobald Sie die gewünschte Ordnerstruktur eingerichtet haben, führen Sie den folgenden Befehl in diesem Ordner aus, um die `.nuspec`-Datei zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="56f31-216">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="56f31-217">Die generierte `.nuspec`-Datei enthält wie bereits erwähnt keine expliziten Verweise auf Dateien in der Ordnerstruktur.</span><span class="sxs-lookup"><span data-stu-id="56f31-217">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="56f31-218">NuGet schließt bei der Paketerstellung automatisch alle Dateien ein.</span><span class="sxs-lookup"><span data-stu-id="56f31-218">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="56f31-219">Die Platzhalterwerte müssen jedoch trotzdem noch in anderen Teilen des Manifests bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="56f31-219">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="56f31-220">Aus einer Assembly-DLL</span><span class="sxs-lookup"><span data-stu-id="56f31-220">From an assembly DLL</span></span>

<span data-ttu-id="56f31-221">Das Erstellen eines Pakets aus einer Assembly ist ein einfacher Vorgang. Dabei können Sie eine `.nuspec`-Datei aus den Metadaten in der Assembly mithilfe des folgenden Befehls generieren:</span><span class="sxs-lookup"><span data-stu-id="56f31-221">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="56f31-222">Bei dieser Schreibweise werden einige Platzhalter im Manifest durch bestimmte Werte aus der Assembly ersetzt.</span><span class="sxs-lookup"><span data-stu-id="56f31-222">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="56f31-223">Die Eigenschaft `<id>` wird beispielsweise auf den Assemblynamen festgelegt und `<version>` auf die Version.</span><span class="sxs-lookup"><span data-stu-id="56f31-223">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="56f31-224">Andere Manifesteigenschaften haben jedoch keine übereinstimmenden Werte in der Assembly und enthalten somit weiterhin Platzhalter.</span><span class="sxs-lookup"><span data-stu-id="56f31-224">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="56f31-225">Aus einem Visual Studio-Projekt</span><span class="sxs-lookup"><span data-stu-id="56f31-225">From a Visual Studio project</span></span>

<span data-ttu-id="56f31-226">Es empfiehlt sich, eine `.nuspec`-Datei aus einer `.csproj`- oder `.vbproj`-Datei zu erstellen, da auf andere Pakete, die in dieses Projekt installiert wurden, automatisch als Abhängigkeiten verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="56f31-226">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="56f31-227">Verwenden Sie einfach den folgenden Befehl im Ordner der Projektdatei:</span><span class="sxs-lookup"><span data-stu-id="56f31-227">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="56f31-228">Die anschließend erstellte `<project-name>.nuspec`-Datei enthält *Tokens*, die zur Packzeit durch Werte aus dem Projekt ersetzt werden, einschließlich der Verweise auf alle anderen Pakete, die bereits installiert wurden.</span><span class="sxs-lookup"><span data-stu-id="56f31-228">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="56f31-229">Wenn Sie Paketabhängigkeiten in die *NUSPEC*-Datei einbinden müssen, verwenden Sie stattdessen `nuget pack`, und rufen Sie die *NUSPEC*-Datei aus der generierten *NUPKG*-Datei ab.</span><span class="sxs-lookup"><span data-stu-id="56f31-229">If you have package dependencies to include in the *.nuspec*, instead use `nuget pack`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="56f31-230">Verwenden Sie z.B. den folgenden Befehl.</span><span class="sxs-lookup"><span data-stu-id="56f31-230">For example, use the following command.</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

<span data-ttu-id="56f31-231">Ein Token wird auf beiden Seiten der Projekteigenschaft durch das Symbol `$` begrenzt.</span><span class="sxs-lookup"><span data-stu-id="56f31-231">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="56f31-232">Wird der Wert `<id>` auf diese Weise in einem Manifest generiert, wird er in der Regel folgendermaßen angezeigt:</span><span class="sxs-lookup"><span data-stu-id="56f31-232">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="56f31-233">Dieses Token wird zur Packzeit durch den Wert `AssemblyName` aus der Projektdatei ersetzt.</span><span class="sxs-lookup"><span data-stu-id="56f31-233">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="56f31-234">Weitere Informationen zur genauen Zuordnung von Projektwerten und `.nuspec`-Tokens finden Sie im Abschnitt [Replacement tokens (Ersetzungstokens)](../reference/nuspec.md#replacement-tokens) im Artikel „.nuspec reference“ (NUSPEC-Referenz).</span><span class="sxs-lookup"><span data-stu-id="56f31-234">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="56f31-235">Durch Tokens müssen Sie wichtige Werte wie die Versionsnummer in der `.nuspec`-Datei nicht mit dem Projekt zusammen aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="56f31-235">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="56f31-236">Sie können die Tokens bei Bedarf jederzeit durch Literalwerte ersetzen.</span><span class="sxs-lookup"><span data-stu-id="56f31-236">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="56f31-237">Wenn Sie in einem Visual Studio-Projekt arbeiten, haben weitere Packoptionen zur Auswahl. Dies wird weiter unten im Abschnitt [Ausführen von „nuget pack“ zum Generieren der NUPKG-Datei](#run-nuget-pack-to-generate-the-nupkg-file) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="56f31-237">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#run-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="56f31-238">Pakete auf Projektmappenebene</span><span class="sxs-lookup"><span data-stu-id="56f31-238">Solution-level packages</span></span>

<span data-ttu-id="56f31-239">*Nur NuGet 2.x. Nicht verfügbar in NuGet 3.0 und höher.*</span><span class="sxs-lookup"><span data-stu-id="56f31-239">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="56f31-240">In NuGet 2.x werden Pakete auf Projektmappenebene unterstützt, über die Tools oder zusätzliche Befehle für die Paket-Manager-Konsole installiert werden (der Inhalt des Ordners `tools`), die jedoch weder Verweise noch Inhalt hinzufügen oder Anpassungen für Projekte in der Projektmappe erstellen.</span><span class="sxs-lookup"><span data-stu-id="56f31-240">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="56f31-241">Solche Pakete enthalten keine Dateien in den direkten Ordnern `lib`, `content` oder `build`, und keine der dazugehörigen Abhängigkeiten besitzt Dateien in den jeweiligen `lib`-, `content`- oder `build`-Ordnern.</span><span class="sxs-lookup"><span data-stu-id="56f31-241">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="56f31-242">NuGet verfolgt installierte Pakete auf Projektmappenebene in einer `packages.config`-Datei im Ordner `.nuget` nach, statt in der `packages.config`-Datei des Projekts.</span><span class="sxs-lookup"><span data-stu-id="56f31-242">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="56f31-243">Neue Datei mit Standardwerten</span><span class="sxs-lookup"><span data-stu-id="56f31-243">New file with default values</span></span>

<span data-ttu-id="56f31-244">Mit dem folgenden Befehl wird ein Standardmanifest mit Platzhaltern erstellt, das gewährleistet, dass Sie mit der richtigen Dateistruktur beginnen:</span><span class="sxs-lookup"><span data-stu-id="56f31-244">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="56f31-245">Wenn Sie \<package-name\> auslassen, ergibt sich daraus die Datei `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="56f31-245">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="56f31-246">Wenn Sie einen Namen wie `Contoso.Utility.UsefulStuff` angeben, lautet die Datei `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="56f31-246">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="56f31-247">Die resultierende `.nuspec`-Datei enthält Platzhalter für Werte wie `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="56f31-247">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="56f31-248">Denken Sie daran, die Datei zu bearbeiten, bevor Sie mit ihr die endgültige `.nupkg`-Datei erstellen.</span><span class="sxs-lookup"><span data-stu-id="56f31-248">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="56f31-249">Auswählen eines eindeutigen Paketbezeichners und Festlegen der Versionsnummer</span><span class="sxs-lookup"><span data-stu-id="56f31-249">Choose a unique package identifier and setting the version number</span></span>

<span data-ttu-id="56f31-250">Der Paketbezeichner (`<id>`-Element) und die Versionsnummer (`<version>`-Element) sind die beiden wichtigsten Werte im Manifest, da sie eindeutig den exakten Code bezeichnen, der im Paket enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="56f31-250">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="56f31-251">**Bewährte Methoden für den Paketbezeichner:**</span><span class="sxs-lookup"><span data-stu-id="56f31-251">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="56f31-252">**Eindeutigkeit**: Der Bezeichner muss auf „nuget.org“ bzw. in dem Katalog, in dem das Paket gehostet wird, eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="56f31-252">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="56f31-253">Bevor Sie sich für einen Bezeichner entscheiden, vergewissern Sie sich, dass dieser im entsprechenden Katalog nicht bereits verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="56f31-253">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="56f31-254">Zur Vermeidung von Konflikten empfiehlt es sich, den Namen Ihres Unternehmens im ersten Teil des Bezeichners zu nutzen, z.B. `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="56f31-254">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="56f31-255">**Namespace-ähnliche Namen**: Verwenden Sie Punkte statt Bindestrichen, wie bei der Notation von Namespaces in .NET.</span><span class="sxs-lookup"><span data-stu-id="56f31-255">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="56f31-256">Schreiben Sie z.B. `Contoso.Utility.UsefulStuff` statt `Contoso-Utility-UsefulStuff` oder `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="56f31-256">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="56f31-257">Benutzer finden es auch hilfreich, wenn der Paketbezeichner den im Code verwendeten Namespaces entspricht.</span><span class="sxs-lookup"><span data-stu-id="56f31-257">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="56f31-258">**Beispielpakete**: Wenn Sie ein Paket mit Beispielcode erstellen, das veranschaulicht, wie ein anderes Paket verwendet wird, fügen Sie `.Sample` als Suffix an den Bezeichner an, z. B. `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="56f31-258">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="56f31-259">Das Beispielpaket würde natürlich vom anderen Paket abhängen. Verwenden Sie beim Erstellen eines Beispielpakets wie weiter oben beschrieben das konventionsbasierte Arbeitsverzeichnis.</span><span class="sxs-lookup"><span data-stu-id="56f31-259">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="56f31-260">Arrangieren Sie den Beispielcode im Ordner `content` in einem Ordner namens `\Samples\<identifier>`, z.B. `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="56f31-260">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="56f31-261">**Bewährte Methoden für die Paketversion:**</span><span class="sxs-lookup"><span data-stu-id="56f31-261">**Best practices for the package version:**</span></span>

- <span data-ttu-id="56f31-262">Legen Sie die Version des Pakets auf die der Bibliothek fest, obwohl dies nicht zwingend erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="56f31-262">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="56f31-263">Dies ist sehr einfach, wenn Sie ein Paket, wie zuvor im Abschnitt [Welche Assemblys sollen gepackt werden?](#decide-which-assemblies-to-package) beschrieben, auf eine einzelne Assembly beschränken.</span><span class="sxs-lookup"><span data-stu-id="56f31-263">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#decide-which-assemblies-to-package).</span></span> <span data-ttu-id="56f31-264">Bedenken Sie, dass NuGet sich beim Auflösen der Abhängigkeiten nach den Paketversionen richtet, nicht nach den Assemblyversionen.</span><span class="sxs-lookup"><span data-stu-id="56f31-264">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="56f31-265">Wenn Sie ein nicht standardmäßiges Versionsschema verwenden, müssen Sie die NuGet-Versionsregeln wie unter [Package versioning (Paketversionsverwaltung](../concepts/package-versioning.md) beschrieben anwenden.</span><span class="sxs-lookup"><span data-stu-id="56f31-265">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../concepts/package-versioning.md).</span></span>

> <span data-ttu-id="56f31-266">Die folgenden kurzen Blogbeiträge enthalten weitere Informationen zur Versionsverwaltung:</span><span class="sxs-lookup"><span data-stu-id="56f31-266">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="56f31-267">Teil 1: Taking on DLL Hell (Teil 1: DLLs)</span><span class="sxs-lookup"><span data-stu-id="56f31-267">Part 1: Taking on DLL Hell</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="56f31-268">Teil 2: The core algorithm (Teil 2: Der Kernalgorithmus)</span><span class="sxs-lookup"><span data-stu-id="56f31-268">Part 2: The core algorithm</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="56f31-269">Part 3: Unification via Binding Redirects (Teil 3: Vereinheitlichung über Bindungsumleitungen)</span><span class="sxs-lookup"><span data-stu-id="56f31-269">Part 3: Unification via Binding Redirects</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a><span data-ttu-id="56f31-270">Hinzufügen einer Infodatei und anderer Dateien</span><span class="sxs-lookup"><span data-stu-id="56f31-270">Add a readme and other files</span></span>

<span data-ttu-id="56f31-271">Verwenden Sie den `<files>`-Knoten in der `.nuspec`-Datei, die dem `<metadata>`-Tag *folgt*, um Dateien, die in das Paket aufgenommen werden sollen, direkt anzugeben:</span><span class="sxs-lookup"><span data-stu-id="56f31-271">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
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
> <span data-ttu-id="56f31-272">Bei einem konventionsbasierten Arbeitsverzeichnis können Sie die Datei „readme.txt“ im Stammverzeichnis des Pakets und andere Inhalte im Ordner `content` platzieren.</span><span class="sxs-lookup"><span data-stu-id="56f31-272">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="56f31-273">Dazu sind keine `<file>`-Elemente im Manifest erforderlich.</span><span class="sxs-lookup"><span data-stu-id="56f31-273">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="56f31-274">Wenn Sie eine Datei namens `readme.txt` im Stammverzeichnis des Pakets einschließen, zeigt Visual Studio unmittelbar nach der direkten Installation des Pakets den Inhalt der Datei als Nur-Text an.</span><span class="sxs-lookup"><span data-stu-id="56f31-274">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="56f31-275">Für Pakete, die als Abhängigkeiten installiert wurden, werden keine Infodateien angezeigt.</span><span class="sxs-lookup"><span data-stu-id="56f31-275">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="56f31-276">Die Infodatei für das Paket „HtmlAgilityPack“ wird z.B. folgendermaßen angezeigt:</span><span class="sxs-lookup"><span data-stu-id="56f31-276">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Anzeige einer Infodatei für ein NuGet-Paket nach der Installation](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="56f31-278">Wenn Sie einen leeren `<files>`-Knoten in die `.nuspec`-Datei einschließen, fügt NuGet dem Paket keine weiteren Inhalte außer denen im Ordner `lib` hinzu.</span><span class="sxs-lookup"><span data-stu-id="56f31-278">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="include-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="56f31-279">Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket</span><span class="sxs-lookup"><span data-stu-id="56f31-279">Include MSBuild props and targets in a package</span></span>

<span data-ttu-id="56f31-280">In einigen Fällen (z.B. beim Ausführen eines benutzerdefinierten Tools oder Prozesses während des Buildvorgangs) sollten Sie benutzerdefinierte Buildziele oder -eigenschaften zu Projekten hinzufügen, die Ihr Paket nutzen.</span><span class="sxs-lookup"><span data-stu-id="56f31-280">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="56f31-281">Platzieren Sie dazu Dateien mit der Schreibweise `<package_id>.targets` oder `<package_id>.props` (z.B. `Contoso.Utility.UsefulStuff.targets`) im `\build`-Ordner des Projekts.</span><span class="sxs-lookup"><span data-stu-id="56f31-281">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="56f31-282">Dateien im `\build`-Stammverzeichnis gelten als für alle Zielframeworks geeignet.</span><span class="sxs-lookup"><span data-stu-id="56f31-282">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="56f31-283">Um frameworkspezifische Dateien bereitzustellen, platzieren Sie zuerst Dateien wie die folgenden in den entsprechenden Unterordnern:</span><span class="sxs-lookup"><span data-stu-id="56f31-283">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

```
    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
```

<span data-ttu-id="56f31-284">Verweisen Sie dann in der `.nuspec`-Datei im `<files>`-Knoten auf diese Dateien:</span><span class="sxs-lookup"><span data-stu-id="56f31-284">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
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

<span data-ttu-id="56f31-285">Das Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket wurde [mit NuGet 2.5 eingeführt](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files). Daher wird empfohlen, dem Element `metadata` das `minClientVersion="2.5"`-Attribut hinzuzufügen, damit die für das Paket erforderliche Mindestversion des NuGet-Clients angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="56f31-285">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="56f31-286">Wenn NuGet ein Paket mit `\build`-Dateien erstellt, werden der Projektdatei MSBuild-`<Import>`-Elemente hinzufügt, die auf die `.targets`- und `.props`-Dateien zeigen.</span><span class="sxs-lookup"><span data-stu-id="56f31-286">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="56f31-287">`.props` wird oben in der Projektdatei hinzugefügt und `.targets` ganz unten. Für jedes Zielframework wird ein eigenes bedingtes MSBuild-`<Import>`-Element hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="56f31-287">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="56f31-288">MSBuild-`.props`- und -`.targets`-Dateien für frameworkübergreifende Ziele können im Ordner `\buildMultiTargeting` abgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="56f31-288">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildMultiTargeting` folder.</span></span> <span data-ttu-id="56f31-289">Bei der Paketinstallation fügt NuGet die entsprechenden `<Import>`-Elemente in die Projektdatei mit der Bedingung ein, dass das Zielframework nicht festgelegt ist (die MSBuild-Eigenschaft `$(TargetFramework)` muss leer sein).</span><span class="sxs-lookup"><span data-stu-id="56f31-289">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="56f31-290">In NuGet 3.x werden Ziele nicht zum Projekt hinzugefügt, sondern über `{projectName}.nuget.g.targets` und `{projectName}.nuget.g.props` zur Verfügung gestellt.</span><span class="sxs-lookup"><span data-stu-id="56f31-290">With NuGet 3.x, targets are not added to the project but are instead made available through `{projectName}.nuget.g.targets` and `{projectName}.nuget.g.props`.</span></span>

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="56f31-291">Ausführen von „nuget pack“ zum Generieren der NUPKG-Datei</span><span class="sxs-lookup"><span data-stu-id="56f31-291">Run nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="56f31-292">Wenn Sie eine Assembly oder das konventionsbasierte Arbeitsverzeichnis verwenden, erstellen Sie ein Paket, indem Sie den Befehl `nuget pack` mit der `.nuspec`-Datei ausführen und dabei `<project-name>` durch den bestimmten Dateinamen ersetzen:</span><span class="sxs-lookup"><span data-stu-id="56f31-292">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="56f31-293">Wenn Sie ein Visual Studio-Projekt verwenden, führen Sie `nuget pack` mit der Projektdatei aus, die automatisch die `.nuspec`-Datei des Projekts lädt und alle Tokens darin durch die Werte in der Projektdatei ersetzt:</span><span class="sxs-lookup"><span data-stu-id="56f31-293">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="56f31-294">Die direkte Verwendung der Projektdatei ist für die Tokenersetzung erforderlich, da das Projekt die Quelle der Tokenwerte ist.</span><span class="sxs-lookup"><span data-stu-id="56f31-294">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="56f31-295">Die Tokenersetzung wird nicht ausgeführt, wenn Sie `nuget pack` mit einer `.nuspec`-Datei verwenden.</span><span class="sxs-lookup"><span data-stu-id="56f31-295">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="56f31-296">`nuget pack` schließt auf jeden Fall Ordner aus, die mit einem Punkt beginnen, z.B. `.git` oder `.hg`.</span><span class="sxs-lookup"><span data-stu-id="56f31-296">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="56f31-297">NuGet gibt an, ob die `.nuspec`-Datei Fehler enthält, die korrigiert werden müssen, z.B. nicht geänderte Platzhalterwerte im Manifest.</span><span class="sxs-lookup"><span data-stu-id="56f31-297">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="56f31-298">Wenn `nuget pack` erfolgreich ausgeführt wurde, können Sie die erstellte `.nupkg`-Datei wie in [Publishing packages (Veröffentlichen von Paketen)](../nuget-org/publish-a-package.md) beschrieben in einem geeigneten Katalog veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="56f31-298">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="56f31-299">Wenn Sie sich das erstellte Paket genauer ansehen möchten, öffnen Sie es einfach im [Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer).</span><span class="sxs-lookup"><span data-stu-id="56f31-299">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="56f31-300">Dieser stellt den Inhalt des Pakets und das Manifest grafisch dar.</span><span class="sxs-lookup"><span data-stu-id="56f31-300">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="56f31-301">Sie können die resultierende `.nupkg`-Datei auch in eine `.zip`-Datei umbenennen und deren Inhalt direkt prüfen.</span><span class="sxs-lookup"><span data-stu-id="56f31-301">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="56f31-302">Zusätzliche Optionen</span><span class="sxs-lookup"><span data-stu-id="56f31-302">Additional options</span></span>

<span data-ttu-id="56f31-303">Sie können `nuget pack` mit verschiedenen Befehlszeilenparameter verwenden, um z.B. Dateien auszuschließen, die Versionsnummer im Manifest zu überschreiben und den Ausgabeordner zu ändern.</span><span class="sxs-lookup"><span data-stu-id="56f31-303">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="56f31-304">Eine vollständige Liste finden Sie in der [Referenz zum Packbefehl](../reference/cli-reference/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="56f31-304">For a complete list, refer to the [pack command reference](../reference/cli-reference/cli-ref-pack.md).</span></span>

<span data-ttu-id="56f31-305">Folgende Optionen werden beispielsweise häufig in Visual Studio-Projekten verwendet:</span><span class="sxs-lookup"><span data-stu-id="56f31-305">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="56f31-306">**Referenzierte Projekte**: Wenn das Projekt auf andere verweist, können Sie die referenzierten Projekte mithilfe der Option `-IncludeReferencedProjects` als Teil des Pakets oder als Abhängigkeiten hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="56f31-306">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="56f31-307">Diese Einschließung ist rekursiv. Wenn also `MyProject.csproj` auf die Projekte B und C verweist und diese Projekte ihrerseits auf die Projekte D, E und F, dann werden Dateien aus B, C, D, E und F in das Paket aufgenommen.</span><span class="sxs-lookup"><span data-stu-id="56f31-307">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="56f31-308">Wenn ein referenziertes Projekt selbst eine `.nuspec`-Datei enthält, fügt NuGet dieses Projekt stattdessen als Abhängigkeit hinzu.</span><span class="sxs-lookup"><span data-stu-id="56f31-308">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="56f31-309">Dieses Projekt muss separat gepackt und veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="56f31-309">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="56f31-310">**Buildkonfiguration**: NuGet verwendet die in der Projektdatei festgelegte Standardbuildkonfiguration, üblicherweise *Debuggen*.</span><span class="sxs-lookup"><span data-stu-id="56f31-310">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="56f31-311">Um Dateien aus einer anderen Buildkonfiguration zu packen, z.B. *Release*, verwenden Sie die Option `-properties` mit folgender Konfiguration:</span><span class="sxs-lookup"><span data-stu-id="56f31-311">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="56f31-312">**Symbole:** Um Symbole einzuschließen, mit denen Benutzer den Paketcode im Debugger schrittweise ausführen können, verwenden Sie die Option `-Symbols`:</span><span class="sxs-lookup"><span data-stu-id="56f31-312">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a><span data-ttu-id="56f31-313">Testen der Paketinstallation</span><span class="sxs-lookup"><span data-stu-id="56f31-313">Test package installation</span></span>

<span data-ttu-id="56f31-314">Vor dem Veröffentlichen eines Pakets testen Sie in der Regel die Installation eines Pakets in einem Projekt.</span><span class="sxs-lookup"><span data-stu-id="56f31-314">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="56f31-315">Diese Tests stellen sicher, dass die erforderlichen Dateien an den richtigen Orten im Projekt installiert werden.</span><span class="sxs-lookup"><span data-stu-id="56f31-315">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="56f31-316">Installationen lassen sich manuell in Visual Studio oder mithilfe der normalen [Paketinstallationsschritte](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package) über die Befehlszeile testen.</span><span class="sxs-lookup"><span data-stu-id="56f31-316">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

<span data-ttu-id="56f31-317">Für automatisierte Tests gehen Sie folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="56f31-317">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="56f31-318">Kopieren Sie die `.nupkg`-Datei in einen lokalen Ordner.</span><span class="sxs-lookup"><span data-stu-id="56f31-318">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="56f31-319">Fügen Sie den Ordner mithilfe des `nuget sources add -name <name> -source <path>`-Befehls den Paketquellen hinzu. Weitere Informationen finden Sie unter [sources command (NuGet CLI) (sources-Befehl (NuGet-CLI))](../reference/cli-reference/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="56f31-319">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../reference/cli-reference/cli-ref-sources.md)).</span></span> <span data-ttu-id="56f31-320">Diese lokale Quelle muss auf einem Computer nur einmal festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="56f31-320">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="56f31-321">Installieren Sie das Paket aus dieser Quelle mithilfe von `nuget install <packageID> -source <name>`, wobei `<name>` dem Namen der Quelle entspricht, so wie er an `nuget sources` übergeben wurde.</span><span class="sxs-lookup"><span data-stu-id="56f31-321">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="56f31-322">Durch das Angeben der Quelle wird sichergestellt, dass das Paket nur aus dieser Quelle installiert wird.</span><span class="sxs-lookup"><span data-stu-id="56f31-322">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="56f31-323">Überprüfen Sie Ihr Dateisystem, um sicherzustellen, dass Dateien richtig installiert wurden.</span><span class="sxs-lookup"><span data-stu-id="56f31-323">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56f31-324">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="56f31-324">Next Steps</span></span>

<span data-ttu-id="56f31-325">Nachdem Sie ein Paket erstellt haben, das eine `.nupkg`-Datei ist, können Sie sie wie unter [Publishing packages (Veröffentlichen von Paketen)](../nuget-org/publish-a-package.md) beschrieben im Katalog Ihrer Wahl veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="56f31-325">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="56f31-326">Sie können auch die Funktionen des Pakets erweitern oder wie in den folgenden Themen beschrieben andere Szenarios unterstützen:</span><span class="sxs-lookup"><span data-stu-id="56f31-326">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="56f31-327">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="56f31-327">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="56f31-328">Unterstützen mehrerer Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="56f31-328">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="56f31-329">Transformationen von Quell- und Konfigurationsdateien</span><span class="sxs-lookup"><span data-stu-id="56f31-329">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="56f31-330">Lokalisierung</span><span class="sxs-lookup"><span data-stu-id="56f31-330">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="56f31-331">Vorabversionen</span><span class="sxs-lookup"><span data-stu-id="56f31-331">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="56f31-332">Festlegen des Pakettyps</span><span class="sxs-lookup"><span data-stu-id="56f31-332">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="56f31-333">Erstellen von Paketen mit COM-Interop-Assemblys</span><span class="sxs-lookup"><span data-stu-id="56f31-333">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="56f31-334">Außerdem sollten Sie die folgenden zusätzlichen Pakettypen berücksichtigen:</span><span class="sxs-lookup"><span data-stu-id="56f31-334">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="56f31-335">Native Pakete</span><span class="sxs-lookup"><span data-stu-id="56f31-335">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="56f31-336">Symbolpakete</span><span class="sxs-lookup"><span data-stu-id="56f31-336">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
