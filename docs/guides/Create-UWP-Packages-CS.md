---
title: Erstellen von NuGet-Paketen für die universelle Windows-Plattform
description: Eine exemplarische End-to-End-Vorgehensweise für das Erstellen von NuGet-Paketen für die universelle Windows-Plattform in C# mithilfe einer Komponente für Windows-Runtime.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231752"
---
# <a name="create-uwp-packages-c"></a><span data-ttu-id="cd4f3-103">Erstellen von UWP-Paketen (C#)</span><span class="sxs-lookup"><span data-stu-id="cd4f3-103">Create UWP packages (C#)</span></span>

<span data-ttu-id="cd4f3-104">Die [universelle Windows-Plattform (UWP)](/windows/uwp) stellt eine allgemeine App-Plattform bereit für alle Windows 10-Geräte bereit.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-104">The [Universal Windows Platform (UWP)](/windows/uwp) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="cd4f3-105">Innerhalb dieses Modells können UWP-Apps sowohl die WinRT-APIs aufrufen, die für alle Geräte verwendet werden, als auch die APIs (einschließlich Win32 und .NET), die spezifisch für die Gerätefamilie sind, auf der die App ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="cd4f3-106">In dieser exemplarischen Vorgehensweise erstellen Sie ein NuGet-Paket mit einer C#-UWP-Komponente (einschließlich eines XAML-Steuerelements), das für verwaltete und native Projekte verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-106">In this walkthrough you create a NuGet package with a C# UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd4f3-107">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="cd4f3-107">Prerequisites</span></span>

1. <span data-ttu-id="cd4f3-108">Visual Studio 2019:</span><span class="sxs-lookup"><span data-stu-id="cd4f3-108">Visual Studio 2019.</span></span> <span data-ttu-id="cd4f3-109">Sie können die 2019 Community Edition kostenlos über [visualstudio.com](https://www.visualstudio.com/) installieren oder die Professional bzw. Enterprise-Edition verwenden.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-109">Install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="cd4f3-110">NuGet-CLI.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-110">NuGet CLI.</span></span> <span data-ttu-id="cd4f3-111">Laden Sie die neuste Version von `nuget.exe` unter [nuget.org/downloads](https://nuget.org/downloads) herunter, und speichern Sie diese an einem beliebigen Ort (dies ist der direkte Download für die `.exe`).</span><span class="sxs-lookup"><span data-stu-id="cd4f3-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="cd4f3-112">Fügen Sie diesen Speicherort, falls erforderlich, anschließend der Umgebungsvariable „PATH“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-112">Then add that location to your PATH environment variable if it isn't already.</span></span> <span data-ttu-id="cd4f3-113">[Weitere Informationen](/nuget/reference/nuget-exe-cli-reference#windows)</span><span class="sxs-lookup"><span data-stu-id="cd4f3-113">[More details](/nuget/reference/nuget-exe-cli-reference#windows).</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="cd4f3-114">Erstellen einer UWP-Komponente für Windows-Runtime</span><span class="sxs-lookup"><span data-stu-id="cd4f3-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="cd4f3-115">Klicken Sie in Visual Studio auf **Datei > Neu > Projekt**, und suchen Sie nach „uwp c#“. Wählen Sie die Vorlage **Komponente für Windows-Runtime (Universal Windows)** aus, klicken Sie auf „Weiter“, ändern Sie den Namen in ImageEnhancer, und klicken Sie auf „Erstellen“.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-115">In Visual Studio, choose **File > New > Project**, search for "uwp c#", select the **Windows Runtime Component (Universal Windows)** template, click next, change the name to ImageEnhancer, and click Create.</span></span> <span data-ttu-id="cd4f3-116">Übernehmen Sie die Standardwerte für „Zielversion“ und „Mindestens erforderliche Version“, wenn Sie dazu aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Erstellen eines neuen UWP-Projekts für eine Komponente für Windows-Runtime](media/UWP-NewProject-CS.png)

1. <span data-ttu-id="cd4f3-118">Klicken Sie mit der rechten Maustaste auf das Projekt in Projektmappen-Explorer, und klicken Sie auf **Hinzufügen > Neues Element**. Klicken Sie auf **Steuerelement mit Vorlagen**, ändern Sie den Namen in „AwesomeImageControl.cs“, und klicken Sie auf **Hinzufügen**:</span><span class="sxs-lookup"><span data-stu-id="cd4f3-118">Right click the project in Solution Explorer, select **Add > New Item**, select **Templated Control**, change the name to AwesomeImageControl.cs, and click **Add**:</span></span>

    ![Hinzufügen eines neuen XAML-Steuerelements mit Vorlagen zum Projekt](media/UWP-NewXAMLControl-CS.png)

1. <span data-ttu-id="cd4f3-120">Klicken Sie in Projektmappen-Explorer mit der rechten Maustaste auf das Projekt, und wählen Sie **Eigenschaften** aus.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="cd4f3-121">Wählen Sie auf der Seite „Eigenschaften“ die Registerkarte **Erstellen** aus, und aktivieren Sie **XML-Dokumentationsdatei**:</span><span class="sxs-lookup"><span data-stu-id="cd4f3-121">In the Properties page, choose **Build** tab and enable **XML Documentation File**:</span></span>

    ![„XML-Dokumentationsdatei generieren“ auf „Ja“ einstellen](media/UWP-GenerateXMLDocFiles-CS.png)

1. <span data-ttu-id="cd4f3-123">Klicken Sie nun mit der rechten Maustaste auf *Projektmappe* und dann auf **Batcherstellung**. Aktivieren Sie wie im Folgenden gezeigt die fünf Kontrollkästchen im Dialogfeld.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-123">Right click the *solution* now, select **Batch Build**, check the five build boxes in the dialog as shown below.</span></span> <span data-ttu-id="cd4f3-124">Damit stellen Sie sicher, dass alle Artefakte für jedes der von Windows unterstützten Zielsysteme generiert wurde, wenn Sie einen Build erstellen.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Batcherstellung](media/UWP-BatchBuild-CS.png)

1. <span data-ttu-id="cd4f3-126">Klicken Sie im Dialogfeld „Batcherstellung“ auf **Erstellen**, um das Projekt zu überprüfen und die Ausgabedateien zu erstellen, die für das NuGet-Paket erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="cd4f3-127">In dieser exemplarischen Vorgehensweise werden die Debugartefakte für das Paket verwendet.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="cd4f3-128">Überprüfen Sie für Nichtdebugpakete stattdessen die Releaseoptionen im Dialogfeld „Batcherstellung“, und verwenden Sie in den folgenden Schritten die als Ergebnis angezeigten Ordner für Releases.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="cd4f3-129">Erstellen und Aktualisieren der NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="cd4f3-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="cd4f3-130">Befolgen Sie folgende drei Schritte, um die erste `.nuspec`-Datei zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="cd4f3-131">In den folgenden Schritten werden weitere erforderliche Updates erläutert.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="cd4f3-132">Öffnen Sie die Eingabeaufforderung, und navigieren Sie zu dem Ordner, der `ImageEnhancer.csproj` enthält. Dabei handelt es sich um einen Unterordner des Speicherorts der Projektmappendatei.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.csproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="cd4f3-133">Führen Sie den [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec)-Befehl aus, um `ImageEnhancer.nuspec` zu generieren (der Name der Datei wird dem Namen der `.csroj`-Datei entnommen):</span><span class="sxs-lookup"><span data-stu-id="cd4f3-133">Run the [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.csroj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="cd4f3-134">Öffnen Sie `ImageEnhancer.nuspec` in einem Editor, aktualisieren Sie die Datei gemäß den folgenden Angaben, und ersetzen Sie YOUR_NAME dabei durch einen entsprechenden Wert.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="cd4f3-135">Belassen Sie keinen der $propertyName$-Werte.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-135">Do not leave any of the $propertyName$ values.</span></span> <span data-ttu-id="cd4f3-136">Insbesondere der `<id>`-Wert muss auf nuget.org eindeutig sein. Weitere Informationen zu den Namenskonventionen finden Sie unter [Creating a package (Erstellen eines Pakets)](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="cd4f3-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="cd4f3-137">Beachten Sie außerdem, dass Sie ebenfalls die Tags für den Autor und die Beschreibung ändern müssen, damit beim Packen kein Fehler ausgelöst wird.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2020</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="cd4f3-138">Bei Paketen, die für die öffentliche Nutzung bereitgestellt werden, sollten Sie besonders auf das `<tags>`-Element achten, da diese Tags andere Personen dabei unterstützen, nach Ihrem Paket zu suchen und dessen Zweck nachzuvollziehen.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="cd4f3-139">Hinzufügen von Windows-Metadaten zum Paket</span><span class="sxs-lookup"><span data-stu-id="cd4f3-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="cd4f3-140">Eine Komponente für Windows-Runtime erfordert Metadaten, die alle öffentlich verfügbaren Typen beschreibt. Dadurch wird es anderen Apps und Bibliotheken ermöglicht, die Komponente zu nutzen.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="cd4f3-141">Die Metadaten sind in einer WINMD-Datei enthalten. Diese wird erstellt, wenn Sie das Projekt kompilieren und muss in Ihrem NuGet-Paket enthalten sein.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="cd4f3-142">Gleichzeitig wird außerdem eine XML-Datei mit IntelliSense-Daten erstellt, die ebenfalls enthalten sein sollte.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="cd4f3-143">Fügen Sie der `.nuspec`-Datei folgenden `<files>`-Knoten hinzu:</span><span class="sxs-lookup"><span data-stu-id="cd4f3-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="cd4f3-144">Hinzufügen von XAML-Inhalten</span><span class="sxs-lookup"><span data-stu-id="cd4f3-144">Adding XAML content</span></span>

<span data-ttu-id="cd4f3-145">Wenn Sie Ihrer Komponente ein XAML-Steuerelement hinzufügen möchten, müssen Sie die XAML-Datei hinzufügen, die die Standardvorlage für das Steuerelement enthält. Diese wurde von der Projektvorlage generiert.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="cd4f3-146">Dies gilt ebenfalls für den Abschnitt `<files>`:</span><span class="sxs-lookup"><span data-stu-id="cd4f3-146">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="cd4f3-147">Hinzufügen der nativen Bibliotheken für die Implementierung</span><span class="sxs-lookup"><span data-stu-id="cd4f3-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="cd4f3-148">Innerhalb Ihrer Komponente ist die Kernlogik des ImageEnhancer-Typs in nativem Code definiert. Dieser ist in den zahlreichen `ImageEnhancer.winmd`-Assemblys enthalten, die für jede Zielruntime (ARM, ARM64, x86 und x64) generiert werden.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.winmd` assemblies that are generated for each target runtime (ARM, ARM64, x86, and x64).</span></span> <span data-ttu-id="cd4f3-149">Verweisen Sie im Abschnitt `<files>` mithilfe der zugehörigen PRI-Ressourcendateien auf diese Assemblys, um diese in das Paket einzuschließen:</span><span class="sxs-lookup"><span data-stu-id="cd4f3-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="cd4f3-150">Endgültige NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="cd4f3-150">Final .nuspec</span></span>

<span data-ttu-id="cd4f3-151">Die endgültige `.nuspec`-Datei sollte nun folgendermaßen aussehen, wobei Sie erneut YOUR_NAME durch einen passenden Wert ersetzen sollten:</span><span class="sxs-lookup"><span data-stu-id="cd4f3-151">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2020</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="cd4f3-152">Packen der Komponente</span><span class="sxs-lookup"><span data-stu-id="cd4f3-152">Package the component</span></span>

<span data-ttu-id="cd4f3-153">Mithilfe der vollständigen `.nuspec`-Datei, die auf alle Dateien verweist, die Sie in das Paket einfügen müssen, können Sie jetzt den Befehl [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) ausführen:</span><span class="sxs-lookup"><span data-stu-id="cd4f3-153">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="cd4f3-154">Dadurch wird die Datei `ImageEnhancer.YOUR_NAME.1.0.0.nupkg` generiert.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-154">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="cd4f3-155">Wenn Sie diese Datei in einem Tool wie dem [NuGet-Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) öffnen und alle Knoten erweitern, werden Ihnen folgende Inhalte angezeigt:</span><span class="sxs-lookup"><span data-stu-id="cd4f3-155">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Der NuGet-Paket-Explorer, der das ImageEnhancer-Paket anzeigt](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="cd4f3-157">Bei einer `.nupkg`-Datei handelt es sich um eine ZIP-Datei mit einer anderen Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-157">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="cd4f3-158">Sie können auch die Paketinhalte untersuchen, indem Sie `.nupkg` in `.zip` ändern. Denken Sie jedoch daran, die Erweiterung wiederherzustellen, bevor Sie ein Paket auf nuget.org hochladen.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-158">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="cd4f3-159">Befolgen Sie die Anweisungen unter [Veröffentlichen eines Pakets](../nuget-org/publish-a-package.md), um Ihr Paket für andere Entwickler zur Verfügung zu stellen.</span><span class="sxs-lookup"><span data-stu-id="cd4f3-159">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="cd4f3-160">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="cd4f3-160">Related topics</span></span>

- [<span data-ttu-id="cd4f3-161">NUSPEC-Verweis</span><span class="sxs-lookup"><span data-stu-id="cd4f3-161">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="cd4f3-162">Symbolpakete</span><span class="sxs-lookup"><span data-stu-id="cd4f3-162">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="cd4f3-163">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="cd4f3-163">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="cd4f3-164">Unterstützung mehrerer .NET Framework-Versionen</span><span class="sxs-lookup"><span data-stu-id="cd4f3-164">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="cd4f3-165">Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket</span><span class="sxs-lookup"><span data-stu-id="cd4f3-165">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="cd4f3-166">Erstellen von lokalisierten Paketen</span><span class="sxs-lookup"><span data-stu-id="cd4f3-166">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
