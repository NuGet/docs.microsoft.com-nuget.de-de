---
title: Erstellen von NuGet-Paketen für die universelle Windows-Plattform | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/21/2017
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: Eine exemplarische End-to-End-Vorgehensweise für das Erstellen von NuGet-Paketen für die universelle Windows-Plattform mithilfe einer Komponente für Windows-Runtime.
keywords: Erstellen eines Pakets, Pakete für UWP, Komponenten für Windows-Runtime
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 6923cdc87b0a550abb51316e384c79137eeaf63a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="create-uwp-packages"></a><span data-ttu-id="06eae-104">Erstellen von UWP-Paketen</span><span class="sxs-lookup"><span data-stu-id="06eae-104">Create UWP packages</span></span>

<span data-ttu-id="06eae-105">Die [universelle Windows-Plattform (UWP)](https://developer.microsoft.com/windows) stellt eine allgemeine App-Plattform bereit für alle Windows 10-Geräte bereit.</span><span class="sxs-lookup"><span data-stu-id="06eae-105">The [Universal Windows Platform (UWP)](https://developer.microsoft.com/windows) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="06eae-106">Innerhalb dieses Modells können UWP-Apps sowohl die WinRT-APIs aufrufen, die für alle Geräte verwendet werden, als auch die APIs (einschließlich Win32 und .NET), die spezifisch für die Gerätefamilie sind, auf der die App ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="06eae-106">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="06eae-107">In dieser exemplarischen Vorgehensweise erstellen Sie ein NuGet-Paket mit einer nativen UWP-Komponente (einschließlich eines XAML-Steuerelements), das für verwaltete und native Projekte verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="06eae-107">In this walkthrough you create a NuGet package with a native UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06eae-108">Erforderliche Komponenten</span><span class="sxs-lookup"><span data-stu-id="06eae-108">Prerequisites</span></span>

1. <span data-ttu-id="06eae-109">Visual Studio 2017 oder Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="06eae-109">Visual Studio 2017 or Visual Studio 2015.</span></span> <span data-ttu-id="06eae-110">Sie können die 2017 Community Edition kostenlos über [visualstudio.com](https://www.visualstudio.com/) installieren oder die Professional bzw. Enterprise-Edition verwenden.</span><span class="sxs-lookup"><span data-stu-id="06eae-110">Install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="06eae-111">NuGet-CLI.</span><span class="sxs-lookup"><span data-stu-id="06eae-111">NuGet CLI.</span></span> <span data-ttu-id="06eae-112">Laden Sie die neuste Version von `nuget.exe` unter [nuget.org/downloads](https://nuget.org/downloads) herunter, und speichern Sie diese an einem beliebigen Ort (dies ist der direkte Download für die `.exe`).</span><span class="sxs-lookup"><span data-stu-id="06eae-112">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="06eae-113">Fügen Sie diesen Speicherort, falls erforderlich, anschließend der Umgebungsvariable „PATH“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="06eae-113">Then add that location to your PATH environment variable if it isn't already.</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="06eae-114">Erstellen einer UWP-Komponente für Windows-Runtime</span><span class="sxs-lookup"><span data-stu-id="06eae-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="06eae-115">Klicken Sie in Visual Studio auf **Datei > Neu > Projekt**, und erweitern Sie den Knoten **Visual C++ > Windows > Universell**. Wählen Sie die Vorlage **Komponente für Windows-Runtime (Universal Windows)** aus, ändern Sie den Namen in ImageEnhancer, und klicken Sie auf OK.</span><span class="sxs-lookup"><span data-stu-id="06eae-115">In Visual Studio, choose **File > New > Project**, expand the **Visual C++ > Windows > Universal** node, select the **Windows Runtime Component (Universal Windows)** template, change the name to ImageEnhancer, and click OK.</span></span> <span data-ttu-id="06eae-116">Übernehmen Sie die Standardwerte für „Zielversion“ und „Mindestens erforderliche Version“, wenn Sie dazu aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="06eae-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Erstellen eines neuen UWP-Projekts für eine Komponente für Windows-Runtime](media/UWP-NewProject.png)

1. <span data-ttu-id="06eae-118">Klicken Sie mit der rechten Maustaste auf das Projekt in Projektmappen-Explorer, klicken Sie auf **Hinzufügen > Neues Element** und dann auf den Knoten **Visual C++ > XAML**. Klicken Sie auf **Steuerelement mit Vorlagen**, ändern Sie den Namen in „AwesomeImageControl.cpp“, und klicken Sie auf **Hinzufügen**:</span><span class="sxs-lookup"><span data-stu-id="06eae-118">Right click the project in Solution Explorer, select **Add > New Item**, click the **Visual C++ > XAML** node, select **Templated Control**, change the name to AwesomeImageControl.cpp, and click **Add**:</span></span>

    ![Hinzufügen eines neuen XAML-Steuerelements mit Vorlagen zum Projekt](media/UWP-NewXAMLControl.png)

1. <span data-ttu-id="06eae-120">Klicken Sie in Projektmappen-Explorer mit der rechten Maustaste auf das Projekt, und wählen Sie **Eigenschaften** aus.</span><span class="sxs-lookup"><span data-stu-id="06eae-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="06eae-121">Erweitern Sie **Konfigurationseigenschaften > C/C++** auf der Seite „Eigenschaften“, und klicken Sie auf **Ausgabedateien**.</span><span class="sxs-lookup"><span data-stu-id="06eae-121">In the Properties page, expand **Configuration Properties > C/C++** and click **Output Files**.</span></span> <span data-ttu-id="06eae-122">Ändern Sie den Wert für **XML-Dokumentationsdateien generieren** im rechten Bereich in „Ja“.</span><span class="sxs-lookup"><span data-stu-id="06eae-122">In the pane on the right, change the value for **Generate XML Documentation Files** to Yes:</span></span>

    ![„XML-Dokumentationsdatei generieren“ auf „Ja“ einstellen](media/UWP-GenerateXMLDocFiles.png)

1. <span data-ttu-id="06eae-124">Klicken Sie nun mit der rechten Maustaste auf *Projektmappe* und dann auf **Batcherstellung**. Aktivieren Sie wie im Folgenden dargestellt die drei Kontrollkästchen für das Debuggen.</span><span class="sxs-lookup"><span data-stu-id="06eae-124">Right click the *solution* now, select **Batch Build**, check the three Debug boxes in the dialog as shown below.</span></span> <span data-ttu-id="06eae-125">Damit stellen Sie sicher, dass alle Artefakte für jedes der von Windows unterstützten Zielsysteme generiert wurde, wenn Sie einen Build erstellen.</span><span class="sxs-lookup"><span data-stu-id="06eae-125">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Batcherstellung](media/UWP-BatchBuild.png)

1. <span data-ttu-id="06eae-127">Klicken Sie im Dialogfeld „Batcherstellung“ auf **Erstellen**, um das Projekt zu überprüfen und die Ausgabedateien zu erstellen, die für das NuGet-Paket erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="06eae-127">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="06eae-128">In dieser exemplarischen Vorgehensweise werden die Debugartefakte für das Paket verwendet.</span><span class="sxs-lookup"><span data-stu-id="06eae-128">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="06eae-129">Überprüfen Sie für Nichtdebugpakete stattdessen die Releaseoptionen im Dialogfeld „Batcherstellung“, und verwenden Sie in den folgenden Schritten die als Ergebnis angezeigten Ordner für Releases.</span><span class="sxs-lookup"><span data-stu-id="06eae-129">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="06eae-130">Erstellen und Aktualisieren der NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="06eae-130">Create and update the .nuspec file</span></span>

<span data-ttu-id="06eae-131">Befolgen Sie folgende drei Schritte, um die erste `.nuspec`-Datei zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="06eae-131">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="06eae-132">In den folgenden Schritten werden weitere erforderliche Updates erläutert.</span><span class="sxs-lookup"><span data-stu-id="06eae-132">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="06eae-133">Öffnen Sie die Eingabeaufforderung, und navigieren Sie zu dem Ordner, der `ImageEnhancer.vcxproj` enthält. Dabei handelt es sich um einen Unterordner des Speicherorts der Projektmappendatei.</span><span class="sxs-lookup"><span data-stu-id="06eae-133">Open a command prompt and navigate to the folder containing `ImageEnhancer.vcxproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="06eae-134">Führen Sie den NuGet-Befehl `spec` aus, um `ImageEnhancer.nuspec` zu generieren. Der Name der Datei wird dem Namen der `.vcxproj`-Datei entnommen:</span><span class="sxs-lookup"><span data-stu-id="06eae-134">Run the NuGet `spec` command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.vcxproj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="06eae-135">Öffnen Sie `ImageEnhancer.nuspec` in einem Editor, und aktualisieren Sie die Datei, damit Sie dem Folgenden entspricht. Dabei wird YOUR_NAME durch einen passenden Wert ersetzt.</span><span class="sxs-lookup"><span data-stu-id="06eae-135">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="06eae-136">Insbesondere der `<id>`-Wert muss auf nuget.org eindeutig sein. Weitere Informationen zu den Namenskonventionen finden Sie unter [Creating a package (Erstellen eines Pakets)](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="06eae-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="06eae-137">Beachten Sie außerdem, dass Sie ebenfalls die Tags für den Autor und die Beschreibung ändern müssen, damit beim Packen kein Fehler ausgelöst wird.</span><span class="sxs-lookup"><span data-stu-id="06eae-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="06eae-138">Bei Paketen, die für die öffentliche Nutzung bereitgestellt werden, sollten Sie besonders auf das `<tags>`-Element achten, da diese Tags andere Personen dabei unterstützen, nach Ihrem Paket zu suchen und dessen Zweck nachzuvollziehen.</span><span class="sxs-lookup"><span data-stu-id="06eae-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="06eae-139">Hinzufügen von Windows-Metadaten zum Paket</span><span class="sxs-lookup"><span data-stu-id="06eae-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="06eae-140">Eine Komponente für Windows-Runtime erfordert Metadaten, die alle öffentlich verfügbaren Typen beschreibt. Dadurch wird es anderen Apps und Bibliotheken ermöglicht, die Komponente zu nutzen.</span><span class="sxs-lookup"><span data-stu-id="06eae-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="06eae-141">Die Metadaten sind in einer WINMD-Datei enthalten. Diese wird erstellt, wenn Sie das Projekt kompilieren und muss in Ihrem NuGet-Paket enthalten sein.</span><span class="sxs-lookup"><span data-stu-id="06eae-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="06eae-142">Gleichzeitig wird außerdem eine XML-Datei mit IntelliSense-Daten erstellt, die ebenfalls enthalten sein sollte.</span><span class="sxs-lookup"><span data-stu-id="06eae-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="06eae-143">Fügen Sie der `.nuspec`-Datei folgenden `<files>`-Knoten hinzu:</span><span class="sxs-lookup"><span data-stu-id="06eae-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="06eae-144">Hinzufügen von XAML-Inhalten</span><span class="sxs-lookup"><span data-stu-id="06eae-144">Adding XAML content</span></span>

<span data-ttu-id="06eae-145">Wenn Sie Ihrer Komponente ein XAML-Steuerelement hinzufügen möchten, müssen Sie die XAML-Datei hinzufügen, die die Standardvorlage für das Steuerelement enthält. Diese wurde von der Projektvorlage generiert.</span><span class="sxs-lookup"><span data-stu-id="06eae-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="06eae-146">Dies gilt ebenfalls für den Abschnitt `<files>`:</span><span class="sxs-lookup"><span data-stu-id="06eae-146">This also goes in the `<files>` section:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="06eae-147">Hinzufügen der nativen Bibliotheken für die Implementierung</span><span class="sxs-lookup"><span data-stu-id="06eae-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="06eae-148">Innerhalb Ihrer Komponente ist die Kernlogik des ImageEnhancer-Typs in nativem Code definiert. Dieser ist in den zahlreichen `ImageEnhancer.dll`-Assemblys enthalten, die für jede Zielruntime (ARM, x86, x64) generiert werden.</span><span class="sxs-lookup"><span data-stu-id="06eae-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.dll` assemblies that are generated for each target runtime (ARM, x86, and x64).</span></span> <span data-ttu-id="06eae-149">Verweisen Sie im Abschnitt `<files>` mithilfe der zugehörigen PRI-Ressourcendateien auf diese Assemblys, um diese in das Paket einzuschließen:</span><span class="sxs-lookup"><span data-stu-id="06eae-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a><span data-ttu-id="06eae-150">Hinzufügen von TARGETS-Dateien</span><span class="sxs-lookup"><span data-stu-id="06eae-150">Adding .targets</span></span>

<span data-ttu-id="06eae-151">Als nächstes benötigen die C++- und JavaScript-Projekte, die Ihr NuGet-Paket möglicherweise verwenden, eine TARGETS-Datei, um die notwendigen Assembly- und WINMD-Dateien zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="06eae-151">Next, C++ and JavaScript projects that might consume your NuGet package need a .targets file to identify the necessary assembly and winmd files.</span></span> <span data-ttu-id="06eae-152">(In C#- und Visual Basic-Projekten wird dies automatisch erledigt.) Erstellen Sie diese Datei, indem Sie den unten stehenden Text in `ImageEnhancer.targets` kopieren und diese im gleichen Ordner wie die `.nuspec`-Datei speichern.</span><span class="sxs-lookup"><span data-stu-id="06eae-152">(C# and Visual Basic projects do this automatically.) Create this file by copying the text below into `ImageEnhancer.targets` and save it in the same folder as the `.nuspec` file.</span></span> <span data-ttu-id="06eae-153">_Hinweis:_ Der Name der `.targets`-Datei muss die Paket-ID enthalten (also z.B. das `<Id>`-Element in der `.nupspec`-Datei):</span><span class="sxs-lookup"><span data-stu-id="06eae-153">_Note_: This `.targets` file needs to be the same name as the package ID (e.g. the `<Id>` element in the `.nupspec` file):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

<span data-ttu-id="06eae-154">Verweisen Sie dann in Ihrer `.nuspec`-Datei auf `ImageEnhancer.targets`:</span><span class="sxs-lookup"><span data-stu-id="06eae-154">Then refer to `ImageEnhancer.targets` in your `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="06eae-155">Endgültige NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="06eae-155">Final .nuspec</span></span>

<span data-ttu-id="06eae-156">Die endgültige `.nuspec`-Datei sollte nun folgendermaßen aussehen, wobei Sie erneut YOUR_NAME durch einen passenden Wert ersetzen sollten:</span><span class="sxs-lookup"><span data-stu-id="06eae-156">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="06eae-157">Packen der Komponente</span><span class="sxs-lookup"><span data-stu-id="06eae-157">Package the component</span></span>

<span data-ttu-id="06eae-158">Mithilfe der vollständigen `.nuspec`-Datei, die auf alle Dateien verweist, die Sie in das Paket einfügen müssen, können Sie jetzt den `pack`-Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="06eae-158">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="06eae-159">Dadurch wird die Datei `ImageEnhancer.YOUR_NAME.1.0.0.nupkg` generiert.</span><span class="sxs-lookup"><span data-stu-id="06eae-159">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="06eae-160">Wenn Sie diese Datei in einem Tool wie dem [NuGet-Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) öffnen und alle Knoten erweitern, werden Ihnen folgende Inhalte angezeigt:</span><span class="sxs-lookup"><span data-stu-id="06eae-160">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Der NuGet-Paket-Explorer, der das ImageEnhancer-Paket anzeigt](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="06eae-162">Bei einer `.nupkg`-Datei handelt es sich um eine ZIP-Datei mit einer anderen Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="06eae-162">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="06eae-163">Sie können auch die Paketinhalte untersuchen, indem Sie `.nupkg` in `.zip` ändern. Denken Sie jedoch daran, die Erweiterung wiederherzustellen, bevor Sie ein Paket auf nuget.org hochladen.</span><span class="sxs-lookup"><span data-stu-id="06eae-163">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="06eae-164">Befolgen Sie die Anweisungen unter [Veröffentlichen eines Pakets](../create-packages/publish-a-package.md), um Ihr Paket für andere Entwickler zur Verfügung zu stellen.</span><span class="sxs-lookup"><span data-stu-id="06eae-164">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="06eae-165">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="06eae-165">Related topics</span></span>

- [<span data-ttu-id="06eae-166">NUSPEC-Verweis</span><span class="sxs-lookup"><span data-stu-id="06eae-166">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="06eae-167">Symbolpakete</span><span class="sxs-lookup"><span data-stu-id="06eae-167">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="06eae-168">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="06eae-168">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="06eae-169">Unterstützung mehrerer .NET Framework-Versionen</span><span class="sxs-lookup"><span data-stu-id="06eae-169">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="06eae-170">Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket</span><span class="sxs-lookup"><span data-stu-id="06eae-170">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="06eae-171">Erstellen von lokalisierten Paketen</span><span class="sxs-lookup"><span data-stu-id="06eae-171">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
