---
title: "Erstellen von plattformübergreifenden NuGet-Paketen (für iOS, Android und Windows) | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: ae24824b-a138-4d12-a810-1f653ddffd32
description: "Eine exemplarische Vorgehensweise zum Erstellen von NuGet-Paketen für Xamarin, die native APIs unter iOS, Android und Windows verwenden."
keywords: "Erstellen eines Pakets, Pakete für Xamarin, plattformübergreifende Pakete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f372856232f151efcf972881cffbe7d4bb7ed6ee
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/05/2018
---
# <a name="create-cross-platform-packages"></a><span data-ttu-id="fb414-104">Erstellen von plattformübergreifenden Paketen</span><span class="sxs-lookup"><span data-stu-id="fb414-104">Create cross-platform packages</span></span>

<span data-ttu-id="fb414-105">Ein plattformübergreifendes Paket enthält Code, der native APIs unter iOS, Android und Windows verwendet und von dem Betriebssystem zur Laufzeit abhängig ist.</span><span class="sxs-lookup"><span data-stu-id="fb414-105">A cross-platform package contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="fb414-106">Obwohl dies ein einfacher Vorgang ist, ist es besser, wenn Entwickler das Paket aus einer PCL- oder .NET Standard-Bibliothek über eine allgemeine API-Oberfläche verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="fb414-106">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="fb414-107">Mithilfe dieser exemplarischen Vorgehensweise können Sie ein plattformübergreifendes NuGet-Paket erstellen, das in mobilen Projekten unter iOS, Android und Windows verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="fb414-107">In this walkthrough you'll create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="fb414-108">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="fb414-108">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="fb414-109">Erstellen der Projektstruktur und abstrakten Codes</span><span class="sxs-lookup"><span data-stu-id="fb414-109">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="fb414-110">Schreiben von plattformspezifischem Code</span><span class="sxs-lookup"><span data-stu-id="fb414-110">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="fb414-111">Erstellen und Aktualisieren der NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="fb414-111">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="fb414-112">Packen der Komponente</span><span class="sxs-lookup"><span data-stu-id="fb414-112">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="fb414-113">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="fb414-113">Related topics</span></span>](#related-topics)

## <a name="pre-requisites"></a><span data-ttu-id="fb414-114">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="fb414-114">Pre-requisites</span></span>

1. <span data-ttu-id="fb414-115">Visual Studio 2015 mit Universelle Windows-Plattform (UWP) und Xamarin.</span><span class="sxs-lookup"><span data-stu-id="fb414-115">Visual Studio 2015 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="fb414-116">Installieren Sie die Community Edition kostenlos über [visualstudio.com](https://www.visualstudio.com/), oder verwenden Sie die Professional bzw. Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="fb414-116">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="fb414-117">Wählen Sie eine benutzerdefinierte Installation aus, und überprüfen Sie die passenden Optionen, um UWP- und Xamarin-Tools hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="fb414-117">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="fb414-118">NuGet-CLI.</span><span class="sxs-lookup"><span data-stu-id="fb414-118">NuGet CLI.</span></span> <span data-ttu-id="fb414-119">Laden Sie die neuste Version von „nuget.exe“ unter [nuget.org/downloads](https://nuget.org/downloads) herunter, und speichern Sie diese an einem beliebigen Ort.</span><span class="sxs-lookup"><span data-stu-id="fb414-119">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="fb414-120">Fügen Sie diesen Speicherort, falls erforderlich, anschließend der Umgebungsvariable „PATH“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="fb414-120">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="fb414-121">„Nuget.exe“ ist kein Installer, sondern ein CLI-Tool. Vergewissern Sie sich daher, dass Sie die im Browser heruntergeladene Datei speichern, anstatt sie auszuführen.</span><span class="sxs-lookup"><span data-stu-id="fb414-121">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>


## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="fb414-122">Erstellen der Projektstruktur und abstrakten Codes</span><span class="sxs-lookup"><span data-stu-id="fb414-122">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="fb414-123">Laden Sie das [Plug-In für Erweiterungen von Xamarin-Vorlagen](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) für Visual Studio herunter, und führen Sie es aus.</span><span class="sxs-lookup"><span data-stu-id="fb414-123">Download and run the [Plugin for Xamarin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="fb414-124">Diese Vorlagen vereinfachen das Erstellen der für diese exemplarische Vorgehensweise notwendigen Projektstruktur.</span><span class="sxs-lookup"><span data-stu-id="fb414-124">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="fb414-125">Suchen Sie in Visual Studio über **Datei > Neu > Projekt** nach `Plugin`, wählen Sie die Vorlage **Plug-In für Xamarin** aus, ändern Sie den Namen in „LoggingLibrary“, und klicken Sie auf „OK“.</span><span class="sxs-lookup"><span data-stu-id="fb414-125">In Visual Studio, **File > New > Project**, search for `Plugin`, select the **Plugin for Xamarin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Neues, leeres App-Projekt (Xamarin.Forms Portable) in Visual Studio](media/CrossPlatform-NewProject.png)

<span data-ttu-id="fb414-127">Die resultierende Projektmappe enthält neben verschiedenen plattformspezifischen Projekten auch zwei PCL-Projekte:</span><span class="sxs-lookup"><span data-stu-id="fb414-127">The resulting solution contains two PCL projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="fb414-128">Der PCL mit dem Namen `Plugin.LoggingLibrary.Abstractions (Portable)` definiert die öffentliche Schnittstelle (API-Oberfläche) der Komponente. In diesem Fall handelt es sich dabei um die `ILoggingLibrary`-Schnittstelle in der Datei „ILoggingLibrary.cs“.</span><span class="sxs-lookup"><span data-stu-id="fb414-128">The PCL named `Plugin.LoggingLibrary.Abstractions (Portable)`, defines the public interface (the API surface area) of the component, in this case the `ILoggingLibrary` interface contained in the ILoggingLibrary.cs file.</span></span> <span data-ttu-id="fb414-129">An dieser Stelle definieren Sie die Schnittstelle zu Ihrer Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="fb414-129">This is where you'll define the interface to your library.</span></span>
- <span data-ttu-id="fb414-130">`Plugin.LoggingLibrary (Portable)`, der andere PCL, enthält Code in der Datei „CrossLoggingLibrary.cs“, der eine plattformspezifische Implementierung der abstrakten Schnittstelle zur Laufzeit findet.</span><span class="sxs-lookup"><span data-stu-id="fb414-130">The other PCL, `Plugin.LoggingLibrary (Portable)`, contains code in CrossLoggingLibrary.cs that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="fb414-131">In der Regel müssen an dieser Datei keine Änderungen vorgenommen werden.</span><span class="sxs-lookup"><span data-stu-id="fb414-131">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="fb414-132">Die plattformspezifischen Projekte, z.B. `Plugin.LoggingLibrary.Android`, enthalten alle in den jeweiligen „LoggingLibraryImplementation.cs“-Dateien eine native Implementierung ihrer Schnittstelle.</span><span class="sxs-lookup"><span data-stu-id="fb414-132">The platform-specific projects, such as `Plugin.LoggingLibrary.Android`, each contain contain a native implementation of the interface in their respective LoggingLibraryImplementation.cs files.</span></span> <span data-ttu-id="fb414-133">An dieser Stelle erstellen Sie den Code Ihrer Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="fb414-133">This is where you'll build out your library's code.</span></span>

<span data-ttu-id="fb414-134">Standardmäßig enthält die Datei „ILoggingLibrary.cs“ des Abstraktionsprojekts zwar eine Schnittstellendefinition, aber keine Methoden.</span><span class="sxs-lookup"><span data-stu-id="fb414-134">By default, the ILoggingLibrary.cs file of the Abstractions project contains an interface definition, but no methods.</span></span> <span data-ttu-id="fb414-135">Fügen Sie für diese exemplarische Vorgehensweise wie folgt eine `Log`-Methode hinzu:</span><span class="sxs-lookup"><span data-stu-id="fb414-135">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;

namespace Plugin.LoggingLibrary.Abstractions
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="fb414-136">Schreiben von plattformspezifischem Code</span><span class="sxs-lookup"><span data-stu-id="fb414-136">Write your platform-specific code</span></span>

<span data-ttu-id="fb414-137">Führen Sie die folgenden Schritte aus, um eine plattformspezifische Implementierung der `ILoggingLibrary`-Schnittstelle und deren Methoden zu implementieren:</span><span class="sxs-lookup"><span data-stu-id="fb414-137">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="fb414-138">Öffnen Sie die `LoggingLibraryImplementation.cs`-Dateien der Plattformprojekte, und fügen Sie den benötigten Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="fb414-138">Open the `LoggingLibraryImplementation.cs` file of each platform project and add the necessary code.</span></span> <span data-ttu-id="fb414-139">Verwenden Sie z.B. das `Plugin.LoggingLibrary.Android`-Projekt:</span><span class="sxs-lookup"><span data-stu-id="fb414-139">For example (using the `Plugin.LoggingLibrary.Android` project):</span></span>

    ```cs
    using Plugin.LoggingLibrary.Abstractions;
    using System;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. <span data-ttu-id="fb414-140">Wiederholen Sie diese Implementierung in den Projekten für jede Plattform, die Sie unterstützen möchten.</span><span class="sxs-lookup"><span data-stu-id="fb414-140">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="fb414-141">Klicken Sie mit der rechten Maustaste auf das iOS-Projekt, klicken Sie erst auf **Eigenschaften** und dann auf die Registerkarte **Build**, und entfernen Sie „\iPhone“ aus dem **Ausgabepfad** und den **XML-Dokumentationsdatei**-Einstellungen.</span><span class="sxs-lookup"><span data-stu-id="fb414-141">Right-click the iOS project, select **Properties**, click the **Build** tab, and remove "\iPhone" from the **Output path** and **XML documentation file** settings.</span></span> <span data-ttu-id="fb414-142">Dieser Schritt dient zur Vereinfachung späterer Schritte in dieser exemplarischen Vorgehensweise.</span><span class="sxs-lookup"><span data-stu-id="fb414-142">This is just for later convenience in this walkthrough.</span></span> <span data-ttu-id="fb414-143">Speichern Sie die Datei anschließend.</span><span class="sxs-lookup"><span data-stu-id="fb414-143">Save the file when done.</span></span>
1. <span data-ttu-id="fb414-144">Klicken Sie mit der rechten Maustaste auf die Projektmappe, wählen Sie **Konfigurations-Manager...** aus, und überprüfen Sie die **Build**-Felder für die PCLs und alle von Ihnen unterstützen Plattformen.</span><span class="sxs-lookup"><span data-stu-id="fb414-144">Right-click the solution, select **Configuration Manager...**, and check the **Build** boxes for the PCLs and each platform you're supporting.</span></span>
1. <span data-ttu-id="fb414-145">Klicken Sie mit der rechten Maustaste auf die Projektmappe, und wählen Sie **Projektmappe erstellen** aus, um Ihre Arbeit zu überprüfen und die Elemente zu erstellen, die Sie als Nächstes packen möchten.</span><span class="sxs-lookup"><span data-stu-id="fb414-145">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you'll package next.</span></span> <span data-ttu-id="fb414-146">Wenn Ihnen Fehler aufgrund von fehlenden Verweisen angezeigt werden, klicken Sie mit der rechten Maustaste auf die Projektmappe, wählen Sie **NuGet-Pakete wiederherstellen** aus, um die Abhängigkeiten zu installieren, und erstellen Sie die Projektmappe erneut.</span><span class="sxs-lookup"><span data-stu-id="fb414-146">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="fb414-147">Sie benötigen für die Erstellung für iOS einen Mac im Netzwerk, für den eine Verbindung mit Visual Studio besteht. Dies wird unter [Introduction to Xamarin.iOS for Visual Studio (Einführung in Xamarin.iOS für Visual Studio)](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="fb414-147">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="fb414-148">Wenn Sie keinen Mac zur Hand haben, entfernen Sie das iOS-Projekt aus dem Konfigurations-Manager (s. Schritt 3).</span><span class="sxs-lookup"><span data-stu-id="fb414-148">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>


## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="fb414-149">Erstellen und Aktualisieren der NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="fb414-149">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="fb414-150">Öffnen Sie eine Eingabeaufforderung, navigieren Sie zum `LoggingLibrary`-Ordner, der sich eine Ebene unter der `.sln`-Datei befindet, und führen Sie den `spec`-Befehl für NuGet aus, um eine erste Version der `Package.nuspec`-Datei zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="fb414-150">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

```
nuget spec
```

1. <span data-ttu-id="fb414-151">Benennen Sie diese Datei in `LoggingLibrary.nuspec` um, und öffnen Sie sie im Editor.</span><span class="sxs-lookup"><span data-stu-id="fb414-151">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="fb414-152">Aktualisieren Sie die Datei, damit sie wie folgt aussieht, indem Sie „IHREN_NAMEN“ durch einen passenden Wert ersetzen.</span><span class="sxs-lookup"><span data-stu-id="fb414-152">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="fb414-153">Insbesondere der `<id>`-Wert muss auf nuget.org eindeutig sein. Informationen zu den Namenskonventionen finden Sie unter [Creating a package (Erstellen eines Pakets)](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="fb414-153">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="fb414-154">Beachten Sie außerdem, dass Sie ebenfalls die Tags für den Autor und die Beschreibung ändern müssen, damit beim Packen kein Fehler ausgelöst wird.</span><span class="sxs-lookup"><span data-stu-id="fb414-154">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```
    
> [!Tip]
> <span data-ttu-id="fb414-155">Sie können an Ihre Paketversion `-alpha`, `-beta` oder `-rc` anhängen, um die Pakete als Vorabversionen zu markieren. Weitere Informationen zu Vorabversionen finden Sie unter [Vorabversionen](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="fb414-155">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="fb414-156">Hinzufügen von Verweisassemblys</span><span class="sxs-lookup"><span data-stu-id="fb414-156">Add reference assemblies</span></span>

<span data-ttu-id="fb414-157">Fügen Sie, abhängig davon, welche Plattformen Sie unterstützen, dem `<files>`-Element von `LoggingLibrary.nuspec` Folgendes hinzu, um plattformspezifische Verweisassemblys hinzuzufügen:</span><span class="sxs-lookup"><span data-stu-id="fb414-157">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> <span data-ttu-id="fb414-158">Klicken Sie mit der rechten Maustaste auf ein beliebiges Projekt, wählen Sie die Registerkarte **Bibliothek** aus, und ändern Sie die Assemblynamen, um die Namen der DLL- und XML-Dateien zu ändern.</span><span class="sxs-lookup"><span data-stu-id="fb414-158">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>


### <a name="add-dependencies"></a><span data-ttu-id="fb414-159">Hinzufügen von Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="fb414-159">Add dependencies</span></span>

<span data-ttu-id="fb414-160">Wenn Sie über bestimmte Abhängigkeiten für native Implementierungen verfügen, verwenden Sie das `<dependencies>`-Element zusammen mit `<group>`-Elementen, um diese anzugeben. Z.B.:</span><span class="sxs-lookup"><span data-stu-id="fb414-160">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

<span data-ttu-id="fb414-161">Im folgenden Beispiel wird „iTextSharp“ als Abhängigkeit für ein UAP-Ziel festgelegt:</span><span class="sxs-lookup"><span data-stu-id="fb414-161">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="fb414-162">Endgültige NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="fb414-162">Final .nuspec</span></span>

<span data-ttu-id="fb414-163">Die endgültige `.nuspec`-Datei sollte nun folgendermaßen aussehen, wobei Sie erneut YOUR_NAME durch einen passenden Wert ersetzen sollten:</span><span class="sxs-lookup"><span data-stu-id="fb414-163">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="fb414-164">Packen der Komponente</span><span class="sxs-lookup"><span data-stu-id="fb414-164">Package the component</span></span>

<span data-ttu-id="fb414-165">Mithilfe der vollständigen `.nuspec`-Datei, die auf alle Dateien verweist, die Sie in das Paket einfügen müssen, können Sie jetzt den `pack`-Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="fb414-165">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="fb414-166">Dadurch wird `LoggingLibrary.YOUR_NAME.1.0.0.nupkg` generiert.</span><span class="sxs-lookup"><span data-stu-id="fb414-166">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="fb414-167">Wenn Sie diese Datei in einem Tool wie dem [NuGet-Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) öffnen und alle Knoten erweitern, werden Ihnen folgende Inhalte angezeigt:</span><span class="sxs-lookup"><span data-stu-id="fb414-167">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![NuGet-Paket-Explorer zeigt das LoggingLibrary-Paket an](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="fb414-169">Bei einer `.nupkg`-Datei handelt es sich um eine ZIP-Datei mit einer anderen Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="fb414-169">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="fb414-170">Sie können auch die Paketinhalte untersuchen, indem Sie `.nupkg` in `.zip` ändern. Denken Sie jedoch daran, die Erweiterung wiederherzustellen, bevor Sie ein Paket auf nuget.org hochladen.</span><span class="sxs-lookup"><span data-stu-id="fb414-170">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>


<span data-ttu-id="fb414-171">Befolgen Sie die Anweisungen unter [Veröffentlichen eines Pakets](../create-packages/publish-a-package.md), um Ihr Paket für andere Entwickler zur Verfügung zu stellen.</span><span class="sxs-lookup"><span data-stu-id="fb414-171">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="fb414-172">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="fb414-172">Related topics</span></span>

- [<span data-ttu-id="fb414-173">NUSPEC-Referenz</span><span class="sxs-lookup"><span data-stu-id="fb414-173">Nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="fb414-174">Symbolpakete</span><span class="sxs-lookup"><span data-stu-id="fb414-174">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="fb414-175">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="fb414-175">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="fb414-176">Unterstützung mehrerer .NET Framework-Versionen</span><span class="sxs-lookup"><span data-stu-id="fb414-176">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="fb414-177">Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket</span><span class="sxs-lookup"><span data-stu-id="fb414-177">Including MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="fb414-178">Erstellen von lokalisierten Paketen</span><span class="sxs-lookup"><span data-stu-id="fb414-178">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)