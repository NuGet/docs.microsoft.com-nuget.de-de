---
title: Erstellen von .NET Standard-NuGet-Paketen mit Visual Studio 2015 | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: Eine exemplarische End-to-End-Vorgehensweise zum Erstellen von .NET Standard-NuGet-Paketen mithilfe von NuGet 3.x und Visual Studio 2015.
keywords: Erstellen eines Pakets, .NET Standard-Pakete, .NET Standard-Zuordnungstabelle
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: abf6a56cbc84bdd066e31e77c7883825a8456144
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="ef9c6-104">Erstellen von .NET Standard-Paketen mit Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="ef9c6-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="ef9c6-105">*Gilt für NuGet 3.x. Unter [Create and publish a package with Visual Studio 2017 (Erstellen und Veröffentlichen eines Pakets mit Visual Studio 2017)](../quickstart/create-and-publish-a-package-using-visual-studio.md) finden Sie weitere Informationen zum Arbeiten mit NuGet 4.x und höher.*</span><span class="sxs-lookup"><span data-stu-id="ef9c6-105">*Applies to NuGet 3.x. See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="ef9c6-106">Die [.NET-Standardbibliothek](/dotnet/articles/standard/library) ist eine formale Spezifikation von .NET-APIs, die in allen .NET-Runtimes verfügbar sein soll, um so eine umfassendere Einheitlichkeit im .NET-Ökosystem herzustellen.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="ef9c6-107">Die .NET-Standardbibliothek definiert einen einheitlichen Satz von BCL-APIs (Base Class Library), die unabhängig von der Workload für alle .NET-Plattformen implementiert werden.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="ef9c6-108">Sie ermöglicht Entwicklern, Code zu erzeugen, der für alle .NET-Runtimes verwendet werden kann, und reduziert plattformspezifische Anweisungen für die bedingte Kompilierung in freigegebenem Code, wenn diese nicht sogar ausgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-108">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="ef9c6-109">Diese Anleitung erläutert das Erstellen eines NuGet-Pakets für die .NET-Standard-Bibliothek 1.4.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-109">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="ef9c6-110">Sie gilt für .NET Framework 4.6.1,Universelle Windows-Plattform 10, .NET Core und Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-110">Such a library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="ef9c6-111">Weitere Informationen finden Sie in diesem Artikel unter [.NET Standard mapping table (.NET Standard-Zuordnungstabelle)](#net-standard-mapping-table).</span><span class="sxs-lookup"><span data-stu-id="ef9c6-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef9c6-112">Erforderliche Komponenten</span><span class="sxs-lookup"><span data-stu-id="ef9c6-112">Prerequisites</span></span>

1. <span data-ttu-id="ef9c6-113">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="ef9c6-113">Visual Studio 2015 Update 3</span></span>
1. [<span data-ttu-id="ef9c6-114">.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="ef9c6-114">.NET Core SDK</span></span>](https://www.microsoft.com/net/download/)
1. <span data-ttu-id="ef9c6-115">NuGet-CLI.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-115">NuGet CLI.</span></span> <span data-ttu-id="ef9c6-116">Laden Sie die neuste Version von „nuget.exe“ unter [nuget.org/downloads](https://nuget.org/downloads) herunter, und speichern Sie diese an einem beliebigen Ort.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-116">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="ef9c6-117">Fügen Sie diesen Speicherort, falls erforderlich, anschließend der Umgebungsvariable „PATH“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-117">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="ef9c6-118">„Nuget.exe“ ist kein Installer, sondern ein CLI-Tool. Vergewissern Sie sich daher, dass Sie die im Browser heruntergeladene Datei speichern, anstatt sie auszuführen.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-118">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="ef9c6-119">Erstellen des Klassenbibliotheksprojekts</span><span class="sxs-lookup"><span data-stu-id="ef9c6-119">Create the class library project</span></span>

1. <span data-ttu-id="ef9c6-120">Klicken Sie in Visual Studio auf **Datei > Neu > Projekt**, erweitern Sie den Knoten **Visual C# > Windows**, wählen Sie **Klassenbibliothek (portabel)** aus, ändern Sie den Namen in „AppLogger“, und klicken Sie anschließend auf OK.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-120">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![Erstellen eines neuen Klassenbibliotheksprojekts](media/NetStandard-NewProject.png)

1. <span data-ttu-id="ef9c6-122">Wählen Sie im angezeigten Dialogfeld **Portable Klassenbibliothek hinzufügen** die Optionen `.NET Framework 4.6` und `ASP.NET Core 1.0` aus.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-122">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>

1. <span data-ttu-id="ef9c6-123">Klicken Sie in Projektmappen-Explorer mit der rechten Maustaste auf `AppLogger (Portable)`, und klicken Sie dann unter **Eigenschaften** auf die Registerkarte **Bibliothek**. Klicken Sie dort im Abschnitt **Ziel** auf **Ziel: .NET-Plattform (Standard)**.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-123">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="ef9c6-124">Dadurch werden Sie zu einer Bestätigung aufgefordert. Anschließend können Sie `.NET Standard 1.4` aus der Dropdownliste auswählen:</span><span class="sxs-lookup"><span data-stu-id="ef9c6-124">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![Festlegen des Ziels auf .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="ef9c6-126">Klicken Sie auf die Registerkarte **Erstellen**, ändern Sie die **Konfiguration** in `Release`, und aktivieren Sie das Kontrollkästchen **XML-Dokumentationsdatei**.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-126">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="ef9c6-127">Fügen Sie der Komponente wie im folgenden Beispiel dargestellt Ihren Code hinzu:</span><span class="sxs-lookup"><span data-stu-id="ef9c6-127">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="ef9c6-128">Legen Sie die Konfiguration auf „Release“ fest, erstellen Sie das Projekt, und überprüfen Sie, ob die DLL und die XML-Dateien innerhalb des `bin\Release`-Ordners erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-128">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="ef9c6-129">Erstellen und Aktualisieren der NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="ef9c6-129">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="ef9c6-130">Öffnen Sie eine Eingabeaufforderung, navigieren Sie zum Ordner, der den `AppLogger.csproj`-Ordner enthält (dieser befindet sich eine Ebene unter der `.sln`-Datei), und führen Sie den `spec`-Befehl für NuGet aus, um eine erste Version der `AppLogger.nuspec`-Datei zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="ef9c6-130">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="ef9c6-131">Öffnen Sie `AppLogger.nuspec` in einem Editor, aktualisieren Sie die Datei gemäß den folgenden Angaben, und ersetzen Sie YOUR_NAME dabei durch einen entsprechenden Wert.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-131">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="ef9c6-132">Insbesondere der `<id>`-Wert muss auf nuget.org eindeutig sein. Weitere Informationen zu den Namenskonventionen finden Sie unter [Creating a package (Erstellen eines Pakets)](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="ef9c6-132">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="ef9c6-133">Beachten Sie außerdem, dass Sie ebenfalls die Tags für den Autor und die Beschreibung ändern müssen, damit beim Packen kein Fehler ausgelöst wird.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-133">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="ef9c6-134">Fügen Sie Verweisassemblys (die DLL-Datei der Bibliothek und die XML-Datei von IntelliSense) zur `.nuspec`-Datei hinzu:</span><span class="sxs-lookup"><span data-stu-id="ef9c6-134">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="ef9c6-135">Klicken Sie mit der rechten Maustaste auf die Projektmappe, und klicken Sie dann auf **Projektmappe erstellen**, um sämtliche Dateien für das Paket zu generieren.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-135">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="ef9c6-136">Deklarieren von Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="ef9c6-136">Declaring dependencies</span></span>

<span data-ttu-id="ef9c6-137">Wenn Abhängigkeiten von anderen NuGet-Paketen bestehen, listen Sie diese im `<dependencies>`-Element des Manifests mit den `<group>`-Elementen auf.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-137">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="ef9c6-138">Fügen Sie beispielsweise Folgendes hinzu, um eine Abhängigkeit von NewtonSoft.Json 8.0.3 oder höher zu deklarieren:</span><span class="sxs-lookup"><span data-stu-id="ef9c6-138">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="ef9c6-139">Die Syntax des *version*-Attributs gibt an, dass Version 8.0.3 oder höher akzeptiert wird.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-139">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="ef9c6-140">Weitere Informationen zum Angeben von anderen Versionsbereichen finden Sie unter [Package versioning (Paketversionsverwaltung)](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="ef9c6-140">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="ef9c6-141">Hinzufügen einer Infodatei</span><span class="sxs-lookup"><span data-stu-id="ef9c6-141">Adding a readme</span></span>

<span data-ttu-id="ef9c6-142">Erstellen Sie Ihre `readme.txt`-Datei, platzieren Sie diese im Stammordner des Projekts, und verweisen Sie in der `.nuspec`-Datei auf diese:</span><span class="sxs-lookup"><span data-stu-id="ef9c6-142">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="ef9c6-143">Visual Studio zeigt `readme.txt` an, wenn das Paket in dem Projekt installiert wird.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-143">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="ef9c6-144">Wenn die Datei in .NET Core-Projekten installiert wurde, wird diese nicht angezeigt. Außerdem wird sie nicht für Pakete angezeigt, die als Abhängigkeiten installiert wurden.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-144">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="ef9c6-145">Packen der Komponente</span><span class="sxs-lookup"><span data-stu-id="ef9c6-145">Package the component</span></span>

<span data-ttu-id="ef9c6-146">Mithilfe der vollständigen `.nuspec`-Datei, die auf alle Dateien verweist, die Sie in das Paket einfügen müssen, können Sie jetzt den `pack`-Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="ef9c6-146">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="ef9c6-147">Dadurch wird `AppLogger.YOUR_NAME.1.0.0.nupkg` generiert.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-147">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="ef9c6-148">Wenn Sie diese Datei in einem Tool wie dem [NuGet-Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) öffnen und alle Knoten erweitern, werden Ihnen folgende Inhalte angezeigt:</span><span class="sxs-lookup"><span data-stu-id="ef9c6-148">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Der NuGet-Paket-Explorer zeigt das AppLogger-Paket an](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="ef9c6-150">Bei einer `.nupkg`-Datei handelt es sich um eine ZIP-Datei mit einer anderen Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-150">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="ef9c6-151">Sie können auch die Paketinhalte untersuchen, indem Sie `.nupkg` in `.zip` ändern. Denken Sie jedoch daran, die Erweiterung wiederherzustellen, bevor Sie ein Paket auf nuget.org hochladen.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-151">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="ef9c6-152">Befolgen Sie die Anweisungen unter [Veröffentlichen eines Pakets](../create-packages/publish-a-package.md), um Ihr Paket für andere Entwickler zur Verfügung zu stellen.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-152">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="ef9c6-153">Beachten Sie, dass für `pack` Mono 4.4.2 unter Mac OS X erforderlich ist und dass dieser Befehl auf Linux-Systemen nicht funktioniert.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-153">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="ef9c6-154">Auf einem Mac müssen Sie ebenfalls Windows-Pfadnamen in der `.nuspec`-Datei in Pfade im Unix-Format konvertieren.</span><span class="sxs-lookup"><span data-stu-id="ef9c6-154">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="net-standard-mapping-table"></a><span data-ttu-id="ef9c6-155">.NET Standard-Zuordnungstabelle</span><span class="sxs-lookup"><span data-stu-id="ef9c6-155">.NET Standard mapping table</span></span>

| <span data-ttu-id="ef9c6-156">Plattformname</span><span class="sxs-lookup"><span data-stu-id="ef9c6-156">Platform Name</span></span> | <span data-ttu-id="ef9c6-157">Alias</span><span class="sxs-lookup"><span data-stu-id="ef9c6-157">Alias</span></span> |
| --- | --- |
| <span data-ttu-id="ef9c6-158">.NET-Standard</span><span class="sxs-lookup"><span data-stu-id="ef9c6-158">.NET Standard</span></span> | <span data-ttu-id="ef9c6-159">netstandard</span><span class="sxs-lookup"><span data-stu-id="ef9c6-159">netstandard</span></span> | <span data-ttu-id="ef9c6-160">1,0</span><span class="sxs-lookup"><span data-stu-id="ef9c6-160">1.0</span></span> | <span data-ttu-id="ef9c6-161">1,1</span><span class="sxs-lookup"><span data-stu-id="ef9c6-161">1.1</span></span> | <span data-ttu-id="ef9c6-162">1.2</span><span class="sxs-lookup"><span data-stu-id="ef9c6-162">1.2</span></span> | <span data-ttu-id="ef9c6-163">1.3</span><span class="sxs-lookup"><span data-stu-id="ef9c6-163">1.3</span></span> | <span data-ttu-id="ef9c6-164">1.4</span><span class="sxs-lookup"><span data-stu-id="ef9c6-164">1.4</span></span> | <span data-ttu-id="ef9c6-165">1.5</span><span class="sxs-lookup"><span data-stu-id="ef9c6-165">1.5</span></span> | <span data-ttu-id="ef9c6-166">1.6</span><span class="sxs-lookup"><span data-stu-id="ef9c6-166">1.6</span></span> |
| <span data-ttu-id="ef9c6-167">.NET Core</span><span class="sxs-lookup"><span data-stu-id="ef9c6-167">.NET Core</span></span> | <span data-ttu-id="ef9c6-168">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="ef9c6-168">netcoreapp</span></span> | <span data-ttu-id="ef9c6-169">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ef9c6-169">&#x2192;</span></span> | <span data-ttu-id="ef9c6-170">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ef9c6-170">&#x2192;</span></span> | <span data-ttu-id="ef9c6-171">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ef9c6-171">&#x2192;</span></span> | <span data-ttu-id="ef9c6-172">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ef9c6-172">&#x2192;</span></span> | <span data-ttu-id="ef9c6-173">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ef9c6-173">&#x2192;</span></span> | <span data-ttu-id="ef9c6-174">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ef9c6-174">&#x2192;</span></span> | <span data-ttu-id="ef9c6-175">1,0</span><span class="sxs-lookup"><span data-stu-id="ef9c6-175">1.0</span></span> |
| <span data-ttu-id="ef9c6-176">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="ef9c6-176">.NET Framework</span></span> | <span data-ttu-id="ef9c6-177">net</span><span class="sxs-lookup"><span data-stu-id="ef9c6-177">net</span></span> | <span data-ttu-id="ef9c6-178">4.5</span><span class="sxs-lookup"><span data-stu-id="ef9c6-178">4.5</span></span> | <span data-ttu-id="ef9c6-179">4.5.1</span><span class="sxs-lookup"><span data-stu-id="ef9c6-179">4.5.1</span></span> | <span data-ttu-id="ef9c6-180">4.6</span><span class="sxs-lookup"><span data-stu-id="ef9c6-180">4.6</span></span> | <span data-ttu-id="ef9c6-181">4.6.1</span><span class="sxs-lookup"><span data-stu-id="ef9c6-181">4.6.1</span></span> | <span data-ttu-id="ef9c6-182">4.6.2</span><span class="sxs-lookup"><span data-stu-id="ef9c6-182">4.6.2</span></span> | <span data-ttu-id="ef9c6-183">4.6.3</span><span class="sxs-lookup"><span data-stu-id="ef9c6-183">4.6.3</span></span> |
| <span data-ttu-id="ef9c6-184">Mono-/Xamarin-Plattformen</span><span class="sxs-lookup"><span data-stu-id="ef9c6-184">Mono/Xamarin Platforms</span></span> | <span data-ttu-id="ef9c6-185">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ef9c6-185">&#x2192;</span></span> | <span data-ttu-id="ef9c6-186">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ef9c6-186">&#x2192;</span></span> | <span data-ttu-id="ef9c6-187">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ef9c6-187">&#x2192;</span></span> | <span data-ttu-id="ef9c6-188">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ef9c6-188">&#x2192;</span></span> | <span data-ttu-id="ef9c6-189">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ef9c6-189">&#x2192;</span></span> | <span data-ttu-id="ef9c6-190">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ef9c6-190">&#x2192;</span></span> |
| <span data-ttu-id="ef9c6-191">Universelle Windows-Plattform</span><span class="sxs-lookup"><span data-stu-id="ef9c6-191">Universal Windows Platform</span></span> | <span data-ttu-id="ef9c6-192">uap</span><span class="sxs-lookup"><span data-stu-id="ef9c6-192">uap</span></span> | <span data-ttu-id="ef9c6-193">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ef9c6-193">&#x2192;</span></span> | <span data-ttu-id="ef9c6-194">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ef9c6-194">&#x2192;</span></span> | <span data-ttu-id="ef9c6-195">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ef9c6-195">&#x2192;</span></span> | <span data-ttu-id="ef9c6-196">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ef9c6-196">&#x2192;</span></span> |<span data-ttu-id="ef9c6-197">10.0</span><span class="sxs-lookup"><span data-stu-id="ef9c6-197">10.0</span></span> |
| <span data-ttu-id="ef9c6-198">Windows</span><span class="sxs-lookup"><span data-stu-id="ef9c6-198">Windows</span></span> | <span data-ttu-id="ef9c6-199">win</span><span class="sxs-lookup"><span data-stu-id="ef9c6-199">win</span></span>| <span data-ttu-id="ef9c6-200">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ef9c6-200">&#x2192;</span></span> | <span data-ttu-id="ef9c6-201">8.0</span><span class="sxs-lookup"><span data-stu-id="ef9c6-201">8.0</span></span> | <span data-ttu-id="ef9c6-202">8.1</span><span class="sxs-lookup"><span data-stu-id="ef9c6-202">8.1</span></span> |
| <span data-ttu-id="ef9c6-203">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="ef9c6-203">Windows Phone</span></span> | <span data-ttu-id="ef9c6-204">wpa</span><span class="sxs-lookup"><span data-stu-id="ef9c6-204">wpa</span></span>| <span data-ttu-id="ef9c6-205">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ef9c6-205">&#x2192;</span></span>| <span data-ttu-id="ef9c6-206">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ef9c6-206">&#x2192;</span></span> | <span data-ttu-id="ef9c6-207">8.1</span><span class="sxs-lookup"><span data-stu-id="ef9c6-207">8.1</span></span> |
| <span data-ttu-id="ef9c6-208">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="ef9c6-208">Windows Phone Silverlight</span></span> | <span data-ttu-id="ef9c6-209">wp</span><span class="sxs-lookup"><span data-stu-id="ef9c6-209">wp</span></span> | <span data-ttu-id="ef9c6-210">8.0</span><span class="sxs-lookup"><span data-stu-id="ef9c6-210">8.0</span></span> |

## <a name="related-topics"></a><span data-ttu-id="ef9c6-211">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="ef9c6-211">Related topics</span></span>

- [<span data-ttu-id="ef9c6-212">NUSPEC-Referenz</span><span class="sxs-lookup"><span data-stu-id="ef9c6-212">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="ef9c6-213">Unterstützen mehrerer .NET Framework-Versionen</span><span class="sxs-lookup"><span data-stu-id="ef9c6-213">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="ef9c6-214">Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket</span><span class="sxs-lookup"><span data-stu-id="ef9c6-214">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="ef9c6-215">Erstellen von lokalisierten Paketen</span><span class="sxs-lookup"><span data-stu-id="ef9c6-215">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="ef9c6-216">Symbolpakete</span><span class="sxs-lookup"><span data-stu-id="ef9c6-216">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="ef9c6-217">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="ef9c6-217">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="ef9c6-218">Dokumentation zur .NET Standard-Bibliothek</span><span class="sxs-lookup"><span data-stu-id="ef9c6-218">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="ef9c6-219">Portieren von .NET Framework auf .NET Core</span><span class="sxs-lookup"><span data-stu-id="ef9c6-219">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
