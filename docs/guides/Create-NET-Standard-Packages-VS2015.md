---
title: Erstellen von .NET Standard- und .NET Framework-NuGet-Paketen mit Visual Studio 2015
description: Eine exemplarische End-to-End-Vorgehensweise zum Erstellen von .NET Standard- und .NET Framework-NuGet-Paketen mithilfe von NuGet 3.x und Visual Studio 2015.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: b16bf422e2627be3b8516a875d749639734064a9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380723"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="bb4ed-103">Erstellen von .NET Standard- und .NET Framework-Paketen mit Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="bb4ed-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="bb4ed-104">**Hinweis**: Visual Studio 2017 wird für die Entwicklung von .NET Standard-Bibliotheken empfohlen.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="bb4ed-105">Visual Studio 2015 kann auch funktionieren, aber die .NET Core-Tools befinden sich darin noch im Vorschaustadium.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="bb4ed-106">Unter [Erstellen und Veröffentlichen eines Pakets mithilfe von Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) finden Sie weitere Informationen zum Arbeiten mit NuGet 4.x und höher sowie mit Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="bb4ed-107">Die [.NET-Standardbibliothek](/dotnet/articles/standard/library) ist eine formale Spezifikation von .NET-APIs, die in allen .NET-Runtimes verfügbar sein soll, um so eine umfassendere Einheitlichkeit im .NET-Ökosystem herzustellen.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="bb4ed-108">Die .NET-Standardbibliothek definiert einen einheitlichen Satz von BCL-APIs (Base Class Library), die unabhängig von der Workload für alle .NET-Plattformen implementiert werden.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="bb4ed-109">Sie ermöglicht Entwicklern, Code zu erzeugen, der für alle .NET-Runtimes verwendet werden kann, und reduziert plattformspezifische Anweisungen für die bedingte Kompilierung in freigegebenem Code, wenn diese nicht sogar ausgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="bb4ed-110">Dieser Leitfaden begleitet Sie durch das Erstellen eines NuGet-Pakets für die .NET Standard 1.4-Bibliothek oder für .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="bb4ed-111">Eine .NET Standard 1.4-Bibliothek gilt für .NET Framework 4.6.1, Universelle Windows-Plattform 10, .NET Core und Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="bb4ed-112">Weitere Informationen finden Sie unter [.NET Standard mapping table (.NET Standard-Zuordnungstabelle)](/dotnet/standard/net-standard#net-implementation-support) (.NET-Dokumentation).</span><span class="sxs-lookup"><span data-stu-id="bb4ed-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="bb4ed-113">Wenn Sie möchten, können Sie auch eine andere Version der .NET Standard-Bibliothek wählen.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb4ed-114">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="bb4ed-114">Prerequisites</span></span>

1. <span data-ttu-id="bb4ed-115">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="bb4ed-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="bb4ed-116">(nur .NET Standard) [.NET Core SDK](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="bb4ed-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="bb4ed-117">NuGet-CLI.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-117">NuGet CLI.</span></span> <span data-ttu-id="bb4ed-118">Laden Sie die neuste Version von „nuget.exe“ unter [nuget.org/downloads](https://nuget.org/downloads) herunter, und speichern Sie diese an einem beliebigen Ort.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="bb4ed-119">Fügen Sie diesen Speicherort, falls erforderlich, anschließend der Umgebungsvariable „PATH“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="bb4ed-120">„Nuget.exe“ ist kein Installer, sondern ein CLI-Tool. Vergewissern Sie sich daher, dass Sie die im Browser heruntergeladene Datei speichern, anstatt sie auszuführen.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="bb4ed-121">Erstellen des Klassenbibliotheksprojekts</span><span class="sxs-lookup"><span data-stu-id="bb4ed-121">Create the class library project</span></span>

1. <span data-ttu-id="bb4ed-122">Klicken Sie in Visual Studio auf **Datei > Neu > Projekt**, erweitern Sie den Knoten **Visual C# > Windows**, wählen Sie **Klassenbibliothek (portabel)** aus, ändern Sie den Namen in „AppLogger“, und wählen Sie anschließend **OK**.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![Erstellen eines neuen Klassenbibliotheksprojekts](media/NetStandard-NewProject.png)

1. <span data-ttu-id="bb4ed-124">Wählen Sie im angezeigten Dialogfeld **Portable Klassenbibliothek hinzufügen** die Optionen für `.NET Framework 4.6` und `ASP.NET Core 1.0` aus.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="bb4ed-125">(Für .NET Framework können Sie die entsprechenden Optionen auswählen.)</span><span class="sxs-lookup"><span data-stu-id="bb4ed-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="bb4ed-126">Für .NET Standard klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf `AppLogger (Portable)`, und wählen Sie dann unter **Eigenschaften** die Registerkarte **Bibliothek**. Wählen Sie dort im Abschnitt **Ziel** die Option **Ziel: .NET-Plattform (Standard)**.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="bb4ed-127">Sie werden aufgefordert, diese Aktion zu bestätigen. Anschließend können Sie `.NET Standard 1.4` (oder eine andere verfügbare Version) aus der Dropdownliste auswählen:</span><span class="sxs-lookup"><span data-stu-id="bb4ed-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![Festlegen des Ziels auf .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="bb4ed-129">Klicken Sie auf die Registerkarte **Erstellen**, ändern Sie die **Konfiguration** in `Release`, und aktivieren Sie das Kontrollkästchen **XML-Dokumentationsdatei**.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="bb4ed-130">Fügen Sie der Komponente wie im folgenden Beispiel dargestellt Ihren Code hinzu:</span><span class="sxs-lookup"><span data-stu-id="bb4ed-130">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="bb4ed-131">Legen Sie die Konfiguration auf „Release“ fest, erstellen Sie das Projekt, und überprüfen Sie, ob die DLL und die XML-Dateien innerhalb des `bin\Release`-Ordners erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="bb4ed-132">Erstellen und Aktualisieren der NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="bb4ed-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="bb4ed-133">Öffnen Sie eine Eingabeaufforderung, navigieren Sie zum Ordner, der den `AppLogger.csproj`-Ordner enthält (dieser befindet sich eine Ebene unter der `.sln`-Datei), und führen Sie den `spec`-Befehl für NuGet aus, um eine erste Version der `AppLogger.nuspec`-Datei zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="bb4ed-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="bb4ed-134">Öffnen Sie `AppLogger.nuspec` in einem Editor, aktualisieren Sie die Datei gemäß den folgenden Angaben, und ersetzen Sie YOUR_NAME dabei durch einen entsprechenden Wert.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="bb4ed-135">Insbesondere der `<id>`-Wert muss auf nuget.org eindeutig sein. Weitere Informationen zu den Namenskonventionen finden Sie unter [Creating a package (Erstellen eines Pakets)](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="bb4ed-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="bb4ed-136">Beachten Sie außerdem, dass Sie ebenfalls die Tags für den Autor und die Beschreibung ändern müssen, damit beim Packen kein Fehler ausgelöst wird.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="bb4ed-137">Fügen Sie Verweisassemblys (die DLL-Datei der Bibliothek und die XML-Datei von IntelliSense) zur `.nuspec`-Datei hinzu:</span><span class="sxs-lookup"><span data-stu-id="bb4ed-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="bb4ed-138">Wenn das Ziel .NET Standard ist, ähneln die Einträge den folgenden:</span><span class="sxs-lookup"><span data-stu-id="bb4ed-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="bb4ed-139">Wenn das Ziel .NET Framework ist, ähneln die Einträge den folgenden:</span><span class="sxs-lookup"><span data-stu-id="bb4ed-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="bb4ed-140">Klicken Sie mit der rechten Maustaste auf die Projektmappe, und klicken Sie dann auf **Projektmappe erstellen**, um sämtliche Dateien für das Paket zu generieren.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="bb4ed-141">Deklarieren von Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="bb4ed-141">Declaring dependencies</span></span>

<span data-ttu-id="bb4ed-142">Wenn Abhängigkeiten von anderen NuGet-Paketen bestehen, listen Sie diese im `<dependencies>`-Element des Manifests mit den `<group>`-Elementen auf.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="bb4ed-143">Fügen Sie beispielsweise Folgendes hinzu, um eine Abhängigkeit von NewtonSoft.Json 8.0.3 oder höher zu deklarieren:</span><span class="sxs-lookup"><span data-stu-id="bb4ed-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="bb4ed-144">Die Syntax des *version*-Attributs gibt an, dass Version 8.0.3 oder höher akzeptiert wird.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="bb4ed-145">Weitere Informationen zum Angeben von anderen Versionsbereichen finden Sie unter [Package versioning (Paketversionsverwaltung)](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="bb4ed-145">To specify different version ranges, refer to [Package versioning](../concepts/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="bb4ed-146">Hinzufügen einer Infodatei</span><span class="sxs-lookup"><span data-stu-id="bb4ed-146">Adding a readme</span></span>

<span data-ttu-id="bb4ed-147">Erstellen Sie Ihre `readme.txt`-Datei, platzieren Sie diese im Stammordner des Projekts, und verweisen Sie in der `.nuspec`-Datei auf diese:</span><span class="sxs-lookup"><span data-stu-id="bb4ed-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="bb4ed-148">Visual Studio zeigt `readme.txt` an, wenn das Paket in dem Projekt installiert wird.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="bb4ed-149">Wenn die Datei in .NET Core-Projekten installiert wurde, wird diese nicht angezeigt. Außerdem wird sie nicht für Pakete angezeigt, die als Abhängigkeiten installiert wurden.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="bb4ed-150">Packen der Komponente</span><span class="sxs-lookup"><span data-stu-id="bb4ed-150">Package the component</span></span>

<span data-ttu-id="bb4ed-151">Mithilfe der vollständigen `.nuspec`-Datei, die auf alle Dateien verweist, die Sie in das Paket einfügen müssen, können Sie jetzt den `pack`-Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="bb4ed-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="bb4ed-152">Dadurch wird die Datei `AppLogger.YOUR_NAME.1.0.0.nupkg` generiert.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="bb4ed-153">Wenn Sie diese Datei in einem Tool wie dem [NuGet-Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) öffnen und alle Knoten erweitern, werden Ihnen (für .NET Standard) folgende Inhalte angezeigt:</span><span class="sxs-lookup"><span data-stu-id="bb4ed-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![Der NuGet-Paket-Explorer zeigt das AppLogger-Paket an](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="bb4ed-155">Bei einer `.nupkg`-Datei handelt es sich um eine ZIP-Datei mit einer anderen Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="bb4ed-156">Sie können auch die Paketinhalte untersuchen, indem Sie `.nupkg` in `.zip` ändern. Denken Sie jedoch daran, die Erweiterung wiederherzustellen, bevor Sie ein Paket auf nuget.org hochladen.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="bb4ed-157">Befolgen Sie die Anweisungen unter [Veröffentlichen eines Pakets](../nuget-org/publish-a-package.md), um Ihr Paket für andere Entwickler zur Verfügung zu stellen.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-157">To make your package available to other developers, follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="bb4ed-158">Beachten Sie, dass für `pack` Mono 4.4.2 unter Mac OS X erforderlich ist und dass dieser Befehl auf Linux-Systemen nicht funktioniert.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="bb4ed-159">Auf einem Mac müssen Sie ebenfalls Windows-Pfadnamen in der `.nuspec`-Datei in Pfade im Unix-Format konvertieren.</span><span class="sxs-lookup"><span data-stu-id="bb4ed-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="bb4ed-160">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="bb4ed-160">Related topics</span></span>

- [<span data-ttu-id="bb4ed-161">NUSPEC-Referenz</span><span class="sxs-lookup"><span data-stu-id="bb4ed-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="bb4ed-162">Unterstützen mehrerer .NET Framework-Versionen</span><span class="sxs-lookup"><span data-stu-id="bb4ed-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="bb4ed-163">Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket</span><span class="sxs-lookup"><span data-stu-id="bb4ed-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="bb4ed-164">Erstellen von lokalisierten Paketen</span><span class="sxs-lookup"><span data-stu-id="bb4ed-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="bb4ed-165">Symbolpakete</span><span class="sxs-lookup"><span data-stu-id="bb4ed-165">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="bb4ed-166">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="bb4ed-166">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="bb4ed-167">Dokumentation zur .NET Standard-Bibliothek</span><span class="sxs-lookup"><span data-stu-id="bb4ed-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="bb4ed-168">Portieren von .NET Framework auf .NET Core</span><span class="sxs-lookup"><span data-stu-id="bb4ed-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
