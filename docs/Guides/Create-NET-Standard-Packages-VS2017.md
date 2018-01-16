---
title: Erstellen von .NET Standard 2.0-NuGet-Paketen mit Visual Studio 2017 | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: Eine exemplarische End-to-End-Vorgehensweise zum Erstellen von .NET Standard 2.0-NuGet-Paketen mithilfe von NuGet 4.x und Visual Studio 2017.
keywords: Erstellen eines Pakets, .NET Standard-Pakete, .NET Core
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5b48ad2f062fd3a9b99985dbda6f89e6039dac4d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/05/2018
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a><span data-ttu-id="6ee2f-104">Erstellen von .NET Standard 2.0-Paketen mit Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="6ee2f-104">Create .NET Standard 2.0 packages with Visual Studio 2017</span></span>

<span data-ttu-id="6ee2f-105">*Gilt für NuGet 4.x und höher sowie MSBuild 15.3 und höher mit Visual Studio 2017 Update 3. Für frühere Versionen von Visual Studio 2017 gelten dieses Anweisungen für .NET Standard 1.4 bis 1.6 durch Ändern der Eigenschaft \<TargetFramework\>. Unter [Create .NET Standard Packages with Visual Studio 2015 (Erstellen von .NET Standard-Paketen mit Visual Studio 2015)](../guides/create-net-standard-packages-vs2015.md) erhalten Sie weitere Informationen zur Arbeit mit NuGet 3.x und höher.*</span><span class="sxs-lookup"><span data-stu-id="6ee2f-105">*Applies to NuGet 4.x+ and MSBuild 15.3+ as provided with Visual Studio 2017 Update 3. For earlier versions of Visual Studio 2017, these instructions apply to .NET Standard 1.4 to 1.6 by changing the \<TargetFramework\> property. Also see [Create .NET Standard Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) for working with NuGet 3.x+.*</span></span>

<span data-ttu-id="6ee2f-106">Die [.NET-Standardbibliothek](/dotnet/articles/standard/library) ist eine formale Spezifikation von .NET-APIs, die in allen .NET-Runtimes verfügbar sein soll, um so eine umfassendere Einheitlichkeit im .NET-Ökosystem herzustellen.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="6ee2f-107">Die .NET-Standardbibliothek definiert einen einheitlichen Satz von BCL-APIs (Base Class Library), die unabhängig von der Workload für alle .NET-Plattformen implementiert werden.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="6ee2f-108">Sie ermöglicht Entwicklern, portable Klassenbibliotheken (PCLs) zu erzeugen, die für alle .NET-Runtimes verwendet werden können, und reduziert plattformspezifische Anweisungen für die bedingte Kompilierung in freigegebenem Code, wenn diese nicht sogar ausgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="6ee2f-109">Diese Anleitung begleitet Sie durch das Erstellen eines NuGet-Pakets für die .NET-Standardbibliothek 2.0 mit Visual Studio 2017 Update 3 und NuGet 4.0.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 2.0 with Visual Studio 2017 Update 3 and NuGet 4.0.</span></span>

1. [<span data-ttu-id="6ee2f-110">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="6ee2f-110">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="6ee2f-111">Erstellen des Klassenbibliotheksprojekts</span><span class="sxs-lookup"><span data-stu-id="6ee2f-111">Create the class library project</span></span>](#create-the-netstandard-class-library-project)
1. [<span data-ttu-id="6ee2f-112">Bearbeiten von Metadaten in der CSPROJ-Datei</span><span class="sxs-lookup"><span data-stu-id="6ee2f-112">Edit metadata in the .csproj file</span></span>](#edit-metadata-in-the-csproj-file)
1. [<span data-ttu-id="6ee2f-113">Packen der Komponente</span><span class="sxs-lookup"><span data-stu-id="6ee2f-113">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="6ee2f-114">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="6ee2f-114">Related topics</span></span>](#related-topics)

## <a name="pre-requisites"></a><span data-ttu-id="6ee2f-115">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="6ee2f-115">Pre-requisites</span></span>

<span data-ttu-id="6ee2f-116">Für diese exemplarische Vorgehensweise ist Visual Studio 2017 Update 3 mit der Workload für die **plattformübergreifende .NET Core-Entwicklung** erforderlich.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-116">This walkthrough requires Visual Studio 2017 Update 3 with the **.NET Core cross-platform development** workload.</span></span> <span data-ttu-id="6ee2f-117">Sie können die Community Edition kostenlos über [visualstudio.com](https://www.visualstudio.com/) installieren oder die Professional bzw. Enterprise Edition verwenden.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-117">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/), or use the Professional and Enterprise editions.</span></span>

<span data-ttu-id="6ee2f-118">Die erforderliche Workload erscheint wie im Folgenden dargestellt im Visual Studio-Installer:</span><span class="sxs-lookup"><span data-stu-id="6ee2f-118">The require workload appears as follows in the Visual Studio installer:</span></span>

![Workload für die plattformübergreifende .NET Core-Entwicklung im Visual Studio-Installer](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a><span data-ttu-id="6ee2f-120">Erstellen des .NET Standard-Klassenbibliotheksprojekts</span><span class="sxs-lookup"><span data-stu-id="6ee2f-120">Create the .NET Standard class library project</span></span>

1. <span data-ttu-id="6ee2f-121">Klicken Sie in Visual Studio auf **Datei > Neu > Projekt**, erweitern Sie den Knoten **Visual C# > .NET Standard**, wählen Sie **Klassenbibliothek (.NET Standard)** aus, ändern Sie den Namen in „AppLogger“, und klicken Sie anschließend auf „OK“.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-121">In Visual Studio, **File > New > Project**, expand the **Visual C# > .NET Standard** node, select **Class Library (Net Standard)**, change the name to AppLogger, and click OK.</span></span>

    ![Erstellen eines neuen Klassenbibliotheksprojekts](media/NuGet4-02-NewProject.png)

1. <span data-ttu-id="6ee2f-123">Ändern Sie die Buildkonfiguration in **Release**.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-123">Change the build configuration to **Release**.</span></span>
1. <span data-ttu-id="6ee2f-124">Klicken Sie mit der rechten Maustaste auf das `AppLogger`-Projekt im Projektmappen-Explorer, wählen Sie **Eigenschaften** aus, und klicken Sie auf die Registerkarte **Build**. Anschließend aktivieren Sie das Feld für die **XML-Dokumentationsdatei** und legen den Dateinamen auf `AppLogger.xml` fest.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-124">Right-click the `AppLogger` project in Solution Explorer, select **Properties**, select the **Build** tab, check the box for **XML documentation file**, and set the filename to just `AppLogger.xml`.</span></span> <span data-ttu-id="6ee2f-125">Speichern Sie das Projekt.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-125">Then save the project.</span></span>

1. <span data-ttu-id="6ee2f-126">Fügen Sie Ihrer Komponente den Code hinzu, wie unten dargestellt (dadurch werden nur Meldungen an die Konsole ausgegeben):</span><span class="sxs-lookup"><span data-stu-id="6ee2f-126">Add your code to the component, such as the following (which clearly just outputs messages to the console):</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. <span data-ttu-id="6ee2f-127">Erstellen Sie das Projekt (mit der Releasekonfiguration), und überprüfen Sie, ob die DLL und die XML-Dateien innerhalb des `bin\Release\netstandard2.0`-Ordners erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-127">Build the project (with the Release configuration) and check that DLL and XML files are produced within the `bin\Release\netstandard2.0` folder.</span></span>

## <a name="edit-metadata-in-the-csproj-file"></a><span data-ttu-id="6ee2f-128">Bearbeiten von Metadaten in der CSPROJ-Datei</span><span class="sxs-lookup"><span data-stu-id="6ee2f-128">Edit metadata in the .csproj file</span></span>

<span data-ttu-id="6ee2f-129">Mit NuGet 4.0- und .NET Core-Projekten sind die Paketmetadaten direkt in der `.csproj`-Datei enthalten und nicht in externen Dateien wie `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-129">With NuGet 4.0 and .NET Core projects, package metadata is contained directly in the `.csproj` file instead of external files such as a `.nuspec`.</span></span> <span data-ttu-id="6ee2f-130">Sie finden eine vollständige Beschreibung dieser Metadaten unter [NuGet pack and restore as MSBuild targets (Packen und Wiederherstellen von NuGet als MSBuild-Ziele)](../schema/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="6ee2f-130">A full description of that metadata is found in [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

1. <span data-ttu-id="6ee2f-131">Klicken Sie mit der rechten Maustaste in das Projekt im Projektmappen-Explorer, wählen Sie **Edit AppLogger.csproj** aus, und bearbeiten Sie anschließend die erste Eigenschaftengruppe, sodass diese Paketinformationen wie die Folgenden enthalten soll:</span><span class="sxs-lookup"><span data-stu-id="6ee2f-131">Right-click the project in Solution Explorer, select **Edit AppLogger.csproj**, and then edit the first property group to include package information such as the following:</span></span>

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. <span data-ttu-id="6ee2f-132">Speichern Sie das Projekt, klicken Sie dann mit der rechten Maustaste auf die Projektmappe, und wählen Sie **Projektmappe erstellen** aus, um erneut alle Dateien für das Paket zu generieren – dieses Mal mit den richtigen Metadaten.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-132">Save the project, then right-click the solution and select **Build Solution** to again generate all the files for the package, this time with the correct metadata.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="6ee2f-133">Packen der Komponente</span><span class="sxs-lookup"><span data-stu-id="6ee2f-133">Package the component</span></span>

<span data-ttu-id="6ee2f-134">NuGet 4.0 unterstützt ein Packziel mit MSBuild-Version 15.1 und höher (einschließlich MSBuild 15.3 als Teil von Visual Studio 2017 Update 3), wenn das Projekt die erforderlichen Paketmetadaten enthält, die im vorherigen Abschnitt hinzugefügt worden sind.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-134">NuGet 4.0 supports a pack target using MSBuild version 15.1+ (including MSBuild 15.3 as part of Visual Studio 2017 Update 3) when the project contains the necessary package metadata, as was added in the previous section.</span></span> <span data-ttu-id="6ee2f-135">Geben Sie einfach das Packziel auf der Befehlszeile im selben Ordner wie die `.csproj`-Datei an, um MSBuild auf diese Weise aufzurufen:</span><span class="sxs-lookup"><span data-stu-id="6ee2f-135">To invoke MSBuild in this way, simply specify the pack target on the command line in the same folder as the `.csproj` file:</span></span>

    msbuild /t:pack /p:Configuration=Release

<span data-ttu-id="6ee2f-136">Zusätzliche Informationen zu `msbuild /t:pack`, z.B. das Einschließen von Inhaltsdateien, Symbolen und Quellcode, finden Sie auf der Seite [NuGet pack and restore as MSBuild targets (Packen und Wiederherstellen von NuGet als MSBuild-Ziele)](../schema/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="6ee2f-136">For additional options with `msbuild /t:pack`, such as including content files, symbols, and source code, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

<span data-ttu-id="6ee2f-137">Auf jeden Fall generiert der obenstehende Code standardmäßig `AppLogger.YOUR_NAME.1.0.0.nupkg` im Ordner `bin\Release` beim Erstellen dieser Konfiguration.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-137">In any case, the command above generates `AppLogger.YOUR_NAME.1.0.0.nupkg` in the `bin\Release` folder by default, as it builds that configuration.</span></span> <span data-ttu-id="6ee2f-138">Wenn Sie den `/p`-Schalter nicht verwenden, lautet die Standardkonfiguration `Debug`.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-138">If you omit the `/p` switch, the default configuration will be `Debug`.</span></span> 

<span data-ttu-id="6ee2f-139">Wenn Sie diese Datei in einem Tool wie dem [NuGet-Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) öffnen und alle Knoten erweitern, wird Ihnen folgender Inhalt angezeigt:</span><span class="sxs-lookup"><span data-stu-id="6ee2f-139">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![Der NuGet-Paket-Explorer zeigt das AppLogger-Paket an](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="6ee2f-141">Bei einer `.nupkg`-Datei handelt es sich um eine ZIP-Datei mit einer anderen Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-141">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="6ee2f-142">Sie können auch die Paketinhalte untersuchen, indem Sie `.nupkg` in `.zip` ändern. Denken Sie jedoch daran, die Erweiterung wiederherzustellen, bevor Sie ein Paket auf nuget.org hochladen.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-142">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="6ee2f-143">Befolgen Sie die Anweisungen unter [Veröffentlichen eines Pakets](../create-packages/publish-a-package.md), um Ihr Paket für andere Entwickler zur Verfügung zu stellen.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-143">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="6ee2f-144">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="6ee2f-144">Related topics</span></span>

- <span data-ttu-id="6ee2f-145">Unter [Packen von Verweisen in Projektdateien](../consume-packages/package-references-in-project-files.md) werden alle Details zum Beschreiben Ihres Pakets direkt in der Projektdatei beschrieben.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-145">[Package References in Project Files](../consume-packages/package-references-in-project-files.md) describes all the details of describing your package directly in the project file.</span></span>
- <span data-ttu-id="6ee2f-146">Unter [NuGet pack and restore as MSBuild targets (Packen und Wiederherstellen von NuGet als MSBuild-Ziele)](../schema/msbuild-targets.md) werden alle Optionen zur Verwendung von `msbuild /t:pack` zum Erstellen des Pakets beschrieben.</span><span class="sxs-lookup"><span data-stu-id="6ee2f-146">[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md) describes all the options for using `msbuild /t:pack` to create the package.</span></span>
- [<span data-ttu-id="6ee2f-147">Dokumentation zur .NET Standard-Bibliothek</span><span class="sxs-lookup"><span data-stu-id="6ee2f-147">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="6ee2f-148">Portieren von .NET Framework auf .NET Core</span><span class="sxs-lookup"><span data-stu-id="6ee2f-148">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
