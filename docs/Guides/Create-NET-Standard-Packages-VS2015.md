---
title: Erstellen von .NET Standard-NuGet-Paketen mit Visual Studio 2015 | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: Eine exemplarische End-to-End-Vorgehensweise zum Erstellen von .NET Standard-NuGet-Paketen mithilfe von NuGet 3.x und Visual Studio 2015.
keywords: Erstellen eines Pakets, .NET Standard-Pakete, .NET Standard-Zuordnungstabelle
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a912c27e1873d60426f2147995f69e2dcc433ca9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="a3dbe-104">Erstellen von .NET Standard-Paketen mit Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="a3dbe-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="a3dbe-105">*Gilt für NuGet 3.x. Unter [Create .NET Standard Packages with Visual Studio 2017 (Erstellen von .NET Standard-Paketen mit Visual Studio 2017)](../guides/create-net-standard-packages-vs2017.md) finden Sie weitere Informationen zum Arbeiten mit NuGet 4.x und höher.*</span><span class="sxs-lookup"><span data-stu-id="a3dbe-105">*Applies to NuGet 3.x. See [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="a3dbe-106">Die [.NET-Standardbibliothek](https://docs.microsoft.com/dotnet/articles/standard/library) ist eine formale Spezifikation von .NET-APIs, die in allen .NET-Runtimes verfügbar sein soll, um so eine umfassendere Einheitlichkeit im .NET-Ökosystem herzustellen.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-106">The [.NET Standard Library](https://docs.microsoft.com/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="a3dbe-107">Die .NET-Standardbibliothek definiert einen einheitlichen Satz von BCL-APIs (Base Class Library), die unabhängig von der Workload für alle .NET-Plattformen implementiert werden.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="a3dbe-108">Sie ermöglicht Entwicklern, portable Klassenbibliotheken (PCLs) zu erzeugen, die für alle .NET-Runtimes verwendet werden können, und reduziert plattformspezifische Anweisungen für die bedingte Kompilierung in freigegebenem Code, wenn diese nicht sogar ausgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="a3dbe-109">Diese Anleitung erläutert das Erstellen eines NuGet-Pakets für die .NET-Standardbibliothek 1.4.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="a3dbe-110">Sie gilt für .NET Framework 4.6.1, universelle Windows-Plattform 10, .NET Core, Mono und Xamarin.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-110">This will work across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="a3dbe-111">Weitere Informationen finden Sie in diesem Artikel unter [.NET Standard mapping table (.NET Standard-Zuordnungstabelle)](#net-standard-mapping-table).</span><span class="sxs-lookup"><span data-stu-id="a3dbe-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

1. [<span data-ttu-id="a3dbe-112">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="a3dbe-112">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="a3dbe-113">Erstellen des Klassenbibliotheksprojekts</span><span class="sxs-lookup"><span data-stu-id="a3dbe-113">Create the class library project</span></span>](#create-the-class-library-project)
1. [<span data-ttu-id="a3dbe-114">Erstellen und Aktualisieren der NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="a3dbe-114">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="a3dbe-115">Packen der Komponente</span><span class="sxs-lookup"><span data-stu-id="a3dbe-115">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="a3dbe-116">Zusätzliche Optionen</span><span class="sxs-lookup"><span data-stu-id="a3dbe-116">Additional options</span></span>](#additional-options)
1. [<span data-ttu-id="a3dbe-117">.NET Standard-Zuordnungstabelle</span><span class="sxs-lookup"><span data-stu-id="a3dbe-117">.NET Standard mapping table</span></span>](#net-standard-mapping-table)
1. [<span data-ttu-id="a3dbe-118">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="a3dbe-118">Related topics</span></span>](#related-topics)


## <a name="pre-requisites"></a><span data-ttu-id="a3dbe-119">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="a3dbe-119">Pre-requisites</span></span>

1. <span data-ttu-id="a3dbe-120">Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-120">Visual Studio 2015.</span></span> <span data-ttu-id="a3dbe-121">Installieren Sie die Community Edition kostenlos über [visualstudio.com](https://www.visualstudio.com/), oder verwenden Sie die Professional bzw. Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-121">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span>
1. <span data-ttu-id="a3dbe-122">.NET Core: Installieren Sie .NET Core zusammen mit den Vorlagen und anderen Tools für Visual Studio 2015 über [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span><span class="sxs-lookup"><span data-stu-id="a3dbe-122">.NET Core: Install .NET Core along with templates and other tools for Visual Studio 2015 from [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span></span>
1. <span data-ttu-id="a3dbe-123">NuGet-CLI.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-123">NuGet CLI.</span></span> <span data-ttu-id="a3dbe-124">Laden Sie die neuste Version von „nuget.exe“ unter [nuget.org/downloads](https://nuget.org/downloads) herunter, und speichern Sie diese an einem beliebigen Ort.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-124">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="a3dbe-125">Fügen Sie diesen Speicherort, falls erforderlich, anschließend der Umgebungsvariable „PATH“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-125">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="a3dbe-126">„Nuget.exe“ ist kein Installer, sondern ein CLI-Tool. Vergewissern Sie sich daher, dass Sie die im Browser heruntergeladene Datei speichern, anstatt sie auszuführen.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-126">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>



## <a name="create-the-class-library-project"></a><span data-ttu-id="a3dbe-127">Erstellen des Klassenbibliotheksprojekts</span><span class="sxs-lookup"><span data-stu-id="a3dbe-127">Create the class library project</span></span>

1. <span data-ttu-id="a3dbe-128">Klicken Sie in Visual Studio auf **Datei > Neu > Projekt**, erweitern Sie den Knoten **Visual C# > Windows**, wählen Sie **Klassenbibliothek (portabel)** aus, ändern Sie den Namen in „AppLogger“, und klicken Sie anschließend auf OK.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-128">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![Erstellen eines neuen Klassenbibliotheksprojekts](media/NetStandard-NewProject.png)

1. <span data-ttu-id="a3dbe-130">Wählen Sie im angezeigten Dialogfeld **Portable Klassenbibliothek hinzufügen** die Optionen `.NET Framework 4.6` und `ASP.NET Core 1.0` aus.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-130">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>
1. <span data-ttu-id="a3dbe-131">Klicken Sie in Projektmappen-Explorer mit der rechten Maustaste auf `AppLogger (Portable)`, und klicken Sie dann unter **Eigenschaften** auf die Registerkarte **Bibliothek**. Klicken Sie dort im Abschnitt **Ziel** auf **Ziel: .NET-Plattform (Standard)**.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-131">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="a3dbe-132">Dadurch werden Sie zu einer Bestätigung aufgefordert. Anschließend können Sie `.NET Standard 1.4` aus der Dropdownliste auswählen:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-132">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![Festlegen des Ziels auf .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="a3dbe-134">Klicken Sie auf die Registerkarte **Erstellen**, ändern Sie die **Konfiguration** in `Release`, und aktivieren Sie das Kontrollkästchen **XML-Dokumentationsdatei**.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-134">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>
1. <span data-ttu-id="a3dbe-135">Fügen Sie der Komponente wie im folgenden Beispiel dargestellt Ihren Code hinzu:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-135">Add your code to the component, for example:</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. <span data-ttu-id="a3dbe-136">Erstellen Sie das Projekt (mit der Releasekonfiguration), und überprüfen Sie, ob die DLL und die XML-Dateien innerhalb des bin\Release-Ordners erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-136">Build the project (with the Release configuration) and check that DLL and XML files are produced within the bin\Release folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="a3dbe-137">Erstellen und Aktualisieren der NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="a3dbe-137">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="a3dbe-138">Öffnen Sie eine Eingabeaufforderung, navigieren Sie zum Ordner, der den `AppLogg.csproj`-Ordner enthält (dieser befindet sich eine Ebene unter der `.sln`-Datei), und führen Sie den `spec`-Befehl für NuGet aus, um eine erste Version der `AppLogger.nuspec`-Datei zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-138">Open a command prompt, navigate to the folder containing `AppLogg.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

```
nuget spec
```

1. <span data-ttu-id="a3dbe-139">Öffnen Sie `AppLogger.nuspec` in einem Editor, aktualisieren Sie die Datei gemäß den folgenden Angaben, und ersetzen Sie YOUR_NAME dabei durch einen entsprechenden Wert.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-139">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="a3dbe-140">Insbesondere der `<id>`-Wert muss auf nuget.org eindeutig sein. Weitere Informationen zu den Namenskonventionen finden Sie unter [Creating a package (Erstellen eines Pakets)](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="a3dbe-140">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="a3dbe-141">Beachten Sie außerdem, dass Sie ebenfalls die Tags für den Autor und die Beschreibung ändern müssen, damit beim Packen kein Fehler ausgelöst wird.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-141">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>AppLogger.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>AppLogger</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. <span data-ttu-id="a3dbe-142">Fügen Sie Verweisassemblys (die DLL-Datei der Bibliothek und die XML-Datei von IntelliSense) zur `.nuspec`-Datei hinzu:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-142">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="a3dbe-143">Klicken Sie mit der rechten Maustaste auf die Projektmappe, und klicken Sie dann auf **Projektmappe erstellen**, um sämtliche Dateien für das Paket zu generieren.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-143">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="a3dbe-144">Packen der Komponente</span><span class="sxs-lookup"><span data-stu-id="a3dbe-144">Package the component</span></span>

<span data-ttu-id="a3dbe-145">Mithilfe der vollständigen `.nuspec`-Datei, die auf alle Dateien verweist, die Sie in das Paket einfügen müssen, können Sie jetzt den `pack`-Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-145">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```
nuget pack AppLogger.nuspec
```

<span data-ttu-id="a3dbe-146">Dadurch wird `AppLogger.YOUR_NAME.1.0.0.nupkg` generiert.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-146">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="a3dbe-147">Wenn Sie diese Datei in einem Tool wie dem [NuGet-Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) öffnen und alle Knoten erweitern, werden Ihnen folgende Inhalte angezeigt:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-147">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![Der NuGet-Paket-Explorer zeigt das AppLogger-Paket an](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="a3dbe-149">Bei einer `.nupkg`-Datei handelt es sich um eine ZIP-Datei mit einer anderen Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-149">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="a3dbe-150">Sie können auch die Paketinhalte untersuchen, indem Sie `.nupkg` in `.zip` ändern. Denken Sie jedoch daran, die Erweiterung wiederherzustellen, bevor Sie ein Paket auf nuget.org hochladen.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-150">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="a3dbe-151">Befolgen Sie die Anweisungen unter [Veröffentlichen eines Pakets](../create-packages/publish-a-package.md), um Ihr Paket für andere Entwickler zur Verfügung zu stellen.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-151">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="a3dbe-152">Beachten Sie, dass für `pack` Mono 4.4.2 unter Mac OS X erforderlich ist und dass dieser Befehl auf Linux-Systemen nicht funktioniert.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-152">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="a3dbe-153">Auf einem Mac müssen Sie ebenfalls Windows-Pfadnamen in der `.nuspec`-Datei in Pfade im Unix-Format konvertieren.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-153">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="additional-options"></a><span data-ttu-id="a3dbe-154">Zusätzliche Optionen</span><span class="sxs-lookup"><span data-stu-id="a3dbe-154">Additional options</span></span>

<span data-ttu-id="a3dbe-155">In den folgenden Abschnitten werden zusätzliche Optionen zum Erstellen von NuGet-Paketen erläutert:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-155">The following sections go into additional options for NuGet package creation:</span></span>

- [<span data-ttu-id="a3dbe-156">Deklarieren von Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="a3dbe-156">Declaring dependencies</span></span>](#declaring-dependencies)
- [<span data-ttu-id="a3dbe-157">Unterstützen mehrerer Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="a3dbe-157">Supporting multiple target frameworks</span></span>](#supporting-multiple-target-frameworks)
- [<span data-ttu-id="a3dbe-158">Hinzufügen von Zielen und Eigenschaften für MSBuild</span><span class="sxs-lookup"><span data-stu-id="a3dbe-158">Adding targets and props for MSBuild</span></span>](#adding-targets-and-props-for-msbuild)
- [<span data-ttu-id="a3dbe-159">Erstellen von lokalisierten Paketen</span><span class="sxs-lookup"><span data-stu-id="a3dbe-159">Creating localized packages</span></span>](#creating-localized-packages)
- [<span data-ttu-id="a3dbe-160">Hinzufügen einer Infodatei</span><span class="sxs-lookup"><span data-stu-id="a3dbe-160">Adding a readme</span></span>](#adding-a-readme)

### <a name="declaring-dependencies"></a><span data-ttu-id="a3dbe-161">Deklarieren von Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="a3dbe-161">Declaring dependencies</span></span>

<span data-ttu-id="a3dbe-162">Wenn Abhängigkeiten von anderen NuGet-Paketen bestehen, listen Sie diese im `<dependencies>`-Element mit den `<group>`-Elementen auf.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-162">If you have any dependencies on other NuGet packages, list those in the `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="a3dbe-163">Fügen Sie beispielsweise Folgendes hinzu, um eine Abhängigkeit von NewtonSoft.Json 8.0.3 oder höher zu deklarieren:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-163">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="a3dbe-164">Die Syntax des *version*-Attributs gibt an, dass Version 8.0.3 oder höher akzeptiert wird.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-164">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="a3dbe-165">Weitere Informationen zum Angeben von anderen Versionsbereichen finden Sie unter [Package versioning (Paketversionsverwaltung)](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="a3dbe-165">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="supporting-multiple-target-frameworks"></a><span data-ttu-id="a3dbe-166">Unterstützen mehrerer Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="a3dbe-166">Supporting multiple target frameworks</span></span>

<span data-ttu-id="a3dbe-167">Angenommen, Sie möchten eine API in .NET Framework 4.6.2 nutzen, die nicht in .NET Standard 1.4 verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-167">Suppose you'd like to take advantage of an API in .NET Framework 4.6.2 that is not available in .NET Standard 1.4.</span></span> <span data-ttu-id="a3dbe-168">Dazu müssen Sie zunächst sicherstellen, dass die Bibliothek für .NET 4.6.2 kompiliert, indem Sie die bedingte Kompilierung oder freigegebene Projekte verwenden.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-168">To do this, you'll first need to make sure the library compiles for .NET 4.6.2 by using conditional compilation or shared projects.</span></span> <span data-ttu-id="a3dbe-169">(In Visual Studio können Sie ein .NET Core-Projekt erstellen, das gewünschte Framework zum Abschnitt für mehrere Frameworks hinzufügen und anschließend einen Build durchführen.) Sie können das Paket dann wie im Folgenden dargestellt mithilfe einer einfachen, konventionsbasierten Technik für Arbeitsverzeichnisse erstellen:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-169">(In Visual Studio, you can create a NetCore project, add the framework of choice to the multiple framework section, and then build.) Then you create the package using the simple convention-based working directory technique as follows:</span></span>

1. <span data-ttu-id="a3dbe-170">Erstellen Sie im Stammordner des Projekts, der die `.nuspec`-Datei enthält, einen Ordner namens `lib`.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-170">In the project's root folder containing your `.nuspec` file, create a folder named `lib`.</span></span>
1. <span data-ttu-id="a3dbe-171">Erstellen Sie innerhalb von `lib` Ordner für jede Plattform, die Sie unterstützen möchten:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-171">Inside `lib`, create folders for each platform you want to support:</span></span>

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. <span data-ttu-id="a3dbe-172">Fügen Sie in der `.nuspec`-Datei einen `files`-Knoten unter dem `package`-Knoten hinzu, und verweisen Sie mithilfe von Platzhaltern auf die Dateien in `lib`.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-172">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `lib` using wildcards.</span></span> <span data-ttu-id="a3dbe-173">**Hinweis:** Ersetzungen von Tokens werden im konventionsbasierten Ansatz für Arbeitsverzeichnisse nicht unterstützt, sodass Sie diese durch Literalwerte ersetzen sollten:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-173">**Note:** Token replacements are not supported with the convention-based working directory approach, so replace them with literal values:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="a3dbe-174">Erstellen Sie das Paket mithilfe von `nuget pack AppLogger.spec` erneut.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-174">Create the package again using `nuget pack AppLogger.spec`.</span></span>

<span data-ttu-id="a3dbe-175">Weitere Informationen zum Verwenden dieser Technik finden Sie unter [Supporting Multiple .NET Framework Versions (Unterstützen mehrerer Versionen von .NET Framework)](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="a3dbe-175">For more details on using this technique, see [Supporting Multiple .NET Framework Versions](../create-packages/supporting-multiple-target-frameworks.md)</span></span>

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="a3dbe-176">Hinzufügen von Zielen und Eigenschaften für MSBuild</span><span class="sxs-lookup"><span data-stu-id="a3dbe-176">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="a3dbe-177">In einigen Fällen (z.B. beim Ausführen eines benutzerdefinierten Tools oder Prozesses während des Buildvorgangs) sollten Sie benutzerdefinierte Buildziele oder Eigenschaften zu Projekten hinzufügen, die Ihr Paket nutzen.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-177">In some cases you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="a3dbe-178">Fügen Sie hierzu wie in den folgenden Schritten beschrieben Dateien zu einem `\build`-Ordner hinzu.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-178">You do this by adding files in a `\build` folder as described in the steps below.</span></span> <span data-ttu-id="a3dbe-179">Wenn NuGet ein Paket mit \build-Dateien erstellt, wird der Projektdatei ein MSBuild-Element hinzufügt, das auf die TARGETS- und PROPS-Dateien zeigt.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-179">When NuGet installs a package with \build files, it adds an MSBuild element in the project file pointing to the .targets and .props files.</span></span>

> [!Note]
> <span data-ttu-id="a3dbe-180">Wenn Sie `project.json` verwenden, werden Ziele nicht zum Projekt hinzugefügt, sondern über `project.lock.json` zur Verfügung gestellt.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-180">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>


1. <span data-ttu-id="a3dbe-181">Erstellen Sie im Ordner des Projekts, der die `.nuspec`-Datei enthält, einen Ordner namens `build`.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-181">In the project folder containing the your `.nuspec` file, create a folder named `build`.</span></span>
1. <span data-ttu-id="a3dbe-182">Erstellen Sie innerhalb von `build` Ordner für jede unterstützte Plattform, und platzieren Sie dort jeweils Ihre `.targets`- und `.props`-Dateien:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-182">Inside `build`, create folders for each supported, and within those place your `.targets` and `.props` files:</span></span>

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. <span data-ttu-id="a3dbe-183">Fügen Sie in der `.nuspec`-Datei einen `files`-Knoten unter dem `package`-Knoten hinzu, und verweisen Sie mithilfe von Platzhaltern auf die Dateien in `build`.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-183">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `build` using wildcards.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. <span data-ttu-id="a3dbe-184">Erstellen Sie das Paket mithilfe von `nuget pack AppLogger.nuspec` erneut.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-184">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>

<span data-ttu-id="a3dbe-185">Weitere Informationen finden Sie unter [Include MSBuild props and targets in a package (Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket)](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="a3dbe-185">For additional details, refer to [Include MSBuild props and targets in a package](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span></span>


### <a name="creating-localized-packages"></a><span data-ttu-id="a3dbe-186">Erstellen von lokalisierten Paketen</span><span class="sxs-lookup"><span data-stu-id="a3dbe-186">Creating localized packages</span></span>

<span data-ttu-id="a3dbe-187">Zum Erstellen von lokalisierten Versionen Ihrer Bibliothek können Sie entweder separate Pakete für unterschiedliche Gebietsschemas erstellen oder lokalisierte Ressourcenassemblys in ein einzelnes Paket einschließen.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-187">To create localized versions of your library, you can either create separate packages for different locales, or include localized resource assemblies within a single package.</span></span> <span data-ttu-id="a3dbe-188">Im Folgenden wird der zweite Ansatz für Deutsch und Italienisch durchgeführt:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-188">Here's how to do the latter approach for German and Italian:</span></span>

1. <span data-ttu-id="a3dbe-189">Erstellen Sie innerhalb jedes Ordners für Zielframeworks unter `lib` einen Ordner für jede andere unterstützte Sprache als Englisch (Standard).</span><span class="sxs-lookup"><span data-stu-id="a3dbe-189">Within each target framework folder under `lib`, create folders for each supported language other than the English default.</span></span> <span data-ttu-id="a3dbe-190">In diesen Ordnern können Sie die Ressourcenassemblys und die lokalisierten XML-Dateien von IntelliSense platzieren.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-190">In these folders you can place resource assemblies  and localized IntelliSense XML files.</span></span> <span data-ttu-id="a3dbe-191">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-191">For example:</span></span>

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. <span data-ttu-id="a3dbe-192">Verweisen Sie auf diese Dateien im `<files>`-Knoten der `.nuspec`-Datei:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-192">In the `.nuspec` file, reference these files in the `<files>` node:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="a3dbe-193">Erstellen Sie das Paket mithilfe von `nuget pack AppLogger.nuspec` erneut.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-193">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>


### <a name="adding-a-readme"></a><span data-ttu-id="a3dbe-194">Hinzufügen einer Infodatei</span><span class="sxs-lookup"><span data-stu-id="a3dbe-194">Adding a readme</span></span>

<span data-ttu-id="a3dbe-195">Wenn Sie eine `readme.txt`-Datei zum Stamm des Pakets hinzufügen, zeigt Visual Studio diese direkt an, wenn das Paket installiert wird.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-195">When you include a `readme.txt` file in the root of the package, Visual Studio will display it when the package is installed directly.</span></span>

> [!Note]
> <span data-ttu-id="a3dbe-196">Infodateien werden nicht für .NET Core-Projekte und für Pakete angezeigt, die als Abhängigkeiten installiert werden.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-196">Readme files are not shown for packages that are installed as a dependency, or for .NET Core projects.</span></span>


<span data-ttu-id="a3dbe-197">Erstellen Sie hierfür Ihre `readme.txt`-Datei, platzieren Sie diese im Stammordner des Projekts, und verweisen Sie in der `.nuspec`-Datei auf diese:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-197">To do this, create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```


## <a name="net-standard-mapping-table"></a><span data-ttu-id="a3dbe-198">.NET Standard-Zuordnungstabelle</span><span class="sxs-lookup"><span data-stu-id="a3dbe-198">.NET Standard mapping table</span></span>

|<span data-ttu-id="a3dbe-199">Plattformname</span><span class="sxs-lookup"><span data-stu-id="a3dbe-199">Platform Name</span></span> |<span data-ttu-id="a3dbe-200">Alias</span><span class="sxs-lookup"><span data-stu-id="a3dbe-200">Alias</span></span>|
|--------------|-----|
|<span data-ttu-id="a3dbe-201">.NET-Standard</span><span class="sxs-lookup"><span data-stu-id="a3dbe-201">.NET Standard</span></span> | <span data-ttu-id="a3dbe-202">netstandard</span><span class="sxs-lookup"><span data-stu-id="a3dbe-202">netstandard</span></span>| <span data-ttu-id="a3dbe-203">1,0</span><span class="sxs-lookup"><span data-stu-id="a3dbe-203">1.0</span></span>| <span data-ttu-id="a3dbe-204">1,1</span><span class="sxs-lookup"><span data-stu-id="a3dbe-204">1.1</span></span>| <span data-ttu-id="a3dbe-205">1.2</span><span class="sxs-lookup"><span data-stu-id="a3dbe-205">1.2</span></span>| <span data-ttu-id="a3dbe-206">1.3</span><span class="sxs-lookup"><span data-stu-id="a3dbe-206">1.3</span></span>| <span data-ttu-id="a3dbe-207">1.4</span><span class="sxs-lookup"><span data-stu-id="a3dbe-207">1.4</span></span>| <span data-ttu-id="a3dbe-208">1.5</span><span class="sxs-lookup"><span data-stu-id="a3dbe-208">1.5</span></span>| <span data-ttu-id="a3dbe-209">1.6</span><span class="sxs-lookup"><span data-stu-id="a3dbe-209">1.6</span></span>|
|<span data-ttu-id="a3dbe-210">.NET Core</span><span class="sxs-lookup"><span data-stu-id="a3dbe-210">.NET Core</span></span> | <span data-ttu-id="a3dbe-211">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="a3dbe-211">netcoreapp</span></span>| <span data-ttu-id="a3dbe-212">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="a3dbe-212">&#x2192;</span></span>| <span data-ttu-id="a3dbe-213">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="a3dbe-213">&#x2192;</span></span>| <span data-ttu-id="a3dbe-214">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="a3dbe-214">&#x2192;</span></span>| <span data-ttu-id="a3dbe-215">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="a3dbe-215">&#x2192;</span></span>| <span data-ttu-id="a3dbe-216">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="a3dbe-216">&#x2192;</span></span>| <span data-ttu-id="a3dbe-217">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="a3dbe-217">&#x2192;</span></span>| <span data-ttu-id="a3dbe-218">1.0</span><span class="sxs-lookup"><span data-stu-id="a3dbe-218">1.0</span></span>|
|<span data-ttu-id="a3dbe-219">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="a3dbe-219">.NET Framework</span></span>| <span data-ttu-id="a3dbe-220">net</span><span class="sxs-lookup"><span data-stu-id="a3dbe-220">net</span></span>| <span data-ttu-id="a3dbe-221">4.5</span><span class="sxs-lookup"><span data-stu-id="a3dbe-221">4.5</span></span>| <span data-ttu-id="a3dbe-222">4.5.1</span><span class="sxs-lookup"><span data-stu-id="a3dbe-222">4.5.1</span></span>| <span data-ttu-id="a3dbe-223">4.6</span><span class="sxs-lookup"><span data-stu-id="a3dbe-223">4.6</span></span>| <span data-ttu-id="a3dbe-224">4.6.1</span><span class="sxs-lookup"><span data-stu-id="a3dbe-224">4.6.1</span></span>| <span data-ttu-id="a3dbe-225">4.6.2</span><span class="sxs-lookup"><span data-stu-id="a3dbe-225">4.6.2</span></span>| <span data-ttu-id="a3dbe-226">4.6.3</span><span class="sxs-lookup"><span data-stu-id="a3dbe-226">4.6.3</span></span>|
|<span data-ttu-id="a3dbe-227">Mono-/Xamarin-Plattformen</span><span class="sxs-lookup"><span data-stu-id="a3dbe-227">Mono/Xamarin Platforms</span></span>| <span data-ttu-id="a3dbe-228">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="a3dbe-228">&#x2192;</span></span>| <span data-ttu-id="a3dbe-229">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="a3dbe-229">&#x2192;</span></span>| <span data-ttu-id="a3dbe-230">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="a3dbe-230">&#x2192;</span></span>| <span data-ttu-id="a3dbe-231">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="a3dbe-231">&#x2192;</span></span>| <span data-ttu-id="a3dbe-232">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="a3dbe-232">&#x2192;</span></span>| <span data-ttu-id="a3dbe-233">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="a3dbe-233">&#x2192;</span></span>|
|<span data-ttu-id="a3dbe-234">Universelle Windows-Plattform</span><span class="sxs-lookup"><span data-stu-id="a3dbe-234">Universal Windows Platform</span></span>| <span data-ttu-id="a3dbe-235">uap</span><span class="sxs-lookup"><span data-stu-id="a3dbe-235">uap</span></span>| <span data-ttu-id="a3dbe-236">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="a3dbe-236">&#x2192;</span></span>| <span data-ttu-id="a3dbe-237">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="a3dbe-237">&#x2192;</span></span>| <span data-ttu-id="a3dbe-238">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="a3dbe-238">&#x2192;</span></span>| <span data-ttu-id="a3dbe-239">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="a3dbe-239">&#x2192;</span></span>|<span data-ttu-id="a3dbe-240">10.0</span><span class="sxs-lookup"><span data-stu-id="a3dbe-240">10.0</span></span>|
|<span data-ttu-id="a3dbe-241">Windows</span><span class="sxs-lookup"><span data-stu-id="a3dbe-241">Windows</span></span>| <span data-ttu-id="a3dbe-242">win</span><span class="sxs-lookup"><span data-stu-id="a3dbe-242">win</span></span>| <span data-ttu-id="a3dbe-243">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="a3dbe-243">&#x2192;</span></span>| <span data-ttu-id="a3dbe-244">8.0</span><span class="sxs-lookup"><span data-stu-id="a3dbe-244">8.0</span></span>| <span data-ttu-id="a3dbe-245">8.1</span><span class="sxs-lookup"><span data-stu-id="a3dbe-245">8.1</span></span>|
|<span data-ttu-id="a3dbe-246">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="a3dbe-246">Windows Phone</span></span>| <span data-ttu-id="a3dbe-247">wpa</span><span class="sxs-lookup"><span data-stu-id="a3dbe-247">wpa</span></span>| <span data-ttu-id="a3dbe-248">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="a3dbe-248">&#x2192;</span></span>| <span data-ttu-id="a3dbe-249">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="a3dbe-249">&#x2192;</span></span>|<span data-ttu-id="a3dbe-250">8.1</span><span class="sxs-lookup"><span data-stu-id="a3dbe-250">8.1</span></span>|
|<span data-ttu-id="a3dbe-251">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="a3dbe-251">Windows Phone Silverlight</span></span>| <span data-ttu-id="a3dbe-252">wp</span><span class="sxs-lookup"><span data-stu-id="a3dbe-252">wp</span></span>| <span data-ttu-id="a3dbe-253">8.0</span><span class="sxs-lookup"><span data-stu-id="a3dbe-253">8.0</span></span>|



## <a name="related-topics"></a><span data-ttu-id="a3dbe-254">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="a3dbe-254">Related topics</span></span>

- [<span data-ttu-id="a3dbe-255">NUSPEC-Referenz</span><span class="sxs-lookup"><span data-stu-id="a3dbe-255">Nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="a3dbe-256">Symbolpakete</span><span class="sxs-lookup"><span data-stu-id="a3dbe-256">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="a3dbe-257">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="a3dbe-257">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="a3dbe-258">Unterstützung mehrerer .NET Framework-Versionen</span><span class="sxs-lookup"><span data-stu-id="a3dbe-258">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="a3dbe-259">Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket</span><span class="sxs-lookup"><span data-stu-id="a3dbe-259">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="a3dbe-260">Erstellen von lokalisierten Paketen</span><span class="sxs-lookup"><span data-stu-id="a3dbe-260">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="a3dbe-261">Dokumentation zur .NET Standard-Bibliothek</span><span class="sxs-lookup"><span data-stu-id="a3dbe-261">.NET Standard Library documentation</span></span>](https://docs.microsoft.com/dotnet/articles/standard/library)
- [<span data-ttu-id="a3dbe-262">Portieren von .NET Framework auf .NET Core</span><span class="sxs-lookup"><span data-stu-id="a3dbe-262">Porting to .NET Core from .NET Framework</span></span>](https://docs.microsoft.com/dotnet/articles/core/porting/index)
