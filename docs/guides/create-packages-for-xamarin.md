---
title: Erstellen von NuGet-Paketen für Xamarin (für iOS, Android und Windows) mit Visual Studio 2017 oder 2019
description: Eine exemplarische Vorgehensweise zum Erstellen von NuGet-Paketen für Xamarin, die native APIs unter iOS, Android und Windows verwenden.
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: 0cb653bad9e853d908039b3f7a94e1dd7eefdde5
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230901"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a><span data-ttu-id="1f2f4-103">Erstellen von Paketen für Xamarin mit Visual Studio 2017 oder 2019</span><span class="sxs-lookup"><span data-stu-id="1f2f4-103">Create packages for Xamarin with Visual Studio 2017 or 2019</span></span>

<span data-ttu-id="1f2f4-104">Ein Paket für Xamarin enthält Code, der native APIs unter iOS, Android und Windows verwendet und von dem Betriebssystem zur Laufzeit abhängig ist.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="1f2f4-105">Obwohl dies ein einfacher Vorgang ist, ist es besser, wenn Entwickler das Paket aus einer PCL- oder .NET Standard-Bibliothek über eine allgemeine API-Oberfläche verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="1f2f4-106">In dieser exemplarischen Vorgehensweise erstellen Sie mit Visual Studio 2017 oder 2019 ein plattformübergreifendes NuGet-Paket, das in mobilen Projekten unter iOS, Android und Windows verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-106">In this walkthrough you use Visual Studio 2017 or 2019 to create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="1f2f4-107">Erforderliche Komponenten</span><span class="sxs-lookup"><span data-stu-id="1f2f4-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="1f2f4-108">Erstellen der Projektstruktur und abstrakten Codes</span><span class="sxs-lookup"><span data-stu-id="1f2f4-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="1f2f4-109">Schreiben von plattformspezifischem Code</span><span class="sxs-lookup"><span data-stu-id="1f2f4-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="1f2f4-110">Erstellen und Aktualisieren der NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="1f2f4-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="1f2f4-111">Packen der Komponente</span><span class="sxs-lookup"><span data-stu-id="1f2f4-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="1f2f4-112">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="1f2f4-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="1f2f4-113">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="1f2f4-113">Prerequisites</span></span>

1. <span data-ttu-id="1f2f4-114">Visual Studio 2017 oder 2019 mit Universelle Windows-Plattform (UWP) und Xamarin.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-114">Visual Studio 2017 or 2019 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="1f2f4-115">Installieren Sie die Community Edition kostenlos über [visualstudio.com](https://www.visualstudio.com/), oder verwenden Sie die Professional bzw. Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="1f2f4-116">Wählen Sie eine benutzerdefinierte Installation aus, und überprüfen Sie die passenden Optionen, um UWP- und Xamarin-Tools hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="1f2f4-117">NuGet-CLI.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-117">NuGet CLI.</span></span> <span data-ttu-id="1f2f4-118">Laden Sie die neuste Version von „nuget.exe“ unter [nuget.org/downloads](https://nuget.org/downloads) herunter, und speichern Sie diese an einem beliebigen Ort.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="1f2f4-119">Fügen Sie diesen Speicherort, falls erforderlich, anschließend der Umgebungsvariable „PATH“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="1f2f4-120">„Nuget.exe“ ist kein Installer, sondern ein CLI-Tool. Vergewissern Sie sich daher, dass Sie die im Browser heruntergeladene Datei speichern, anstatt sie auszuführen.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="1f2f4-121">Erstellen der Projektstruktur und abstrakten Codes</span><span class="sxs-lookup"><span data-stu-id="1f2f4-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="1f2f4-122">Laden Sie das [plattformübergreifende .NET Standard-Plug-In für Erweiterungen von Vorlagen](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) für Visual Studio herunter, und führen Sie es aus.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-122">Download and run the [Cross-Platform .NET Standard Plugin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="1f2f4-123">Diese Vorlagen vereinfachen das Erstellen der für diese exemplarische Vorgehensweise notwendigen Projektstruktur.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="1f2f4-124">Suchen Sie in Visual Studio 2017 über **Datei > Neu > Projekt** nach `Plugin`, wählen Sie die Vorlage für das **plattformübergreifende .NET Standardbibliothek-Plug-In** aus, ändern Sie den Namen in „LoggingLibrary“, und klicken Sie auf „OK“.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-124">In Visual Studio 2017, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Neues, leeres App-Projekt (Xamarin.Forms Portable) in Visual Studio 2017](media/CrossPlatform-NewProject.png)

    <span data-ttu-id="1f2f4-126">Suchen Sie in Visual Studio 2019 über **Datei > Neu > Projekt** nach `Plugin`, wählen Sie die Vorlage für das **plattformübergreifende .NET Standardbibliothek-Plug-In** aus, und klicken Sie auf „Weiter“.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-126">In Visual Studio 2019, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, and click Next.</span></span>

    ![Neues, leeres App-Projekt (Xamarin.Forms Portable) in Visual Studio 2019](media/CrossPlatform-NewProject19-Part1.png)

    <span data-ttu-id="1f2f4-128">Ändern Sie den Namen in „LoggingLibrary“, und klicken Sie auf „Erstellen“.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-128">Change the name to LoggingLibrary, and click Create.</span></span>

    ![Neue, leere App-Konfiguration (Xamarin.Forms Portable) in Visual Studio 2019](media/CrossPlatform-NewProject19-Part2.png)

<span data-ttu-id="1f2f4-130">Die resultierende Projektmappe enthält neben verschiedenen plattformspezifischen Projekten auch zwei gemeinsam genutzte Projekte:</span><span class="sxs-lookup"><span data-stu-id="1f2f4-130">The resulting solution contains two Shared projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="1f2f4-131">Das Projekt `ILoggingLibrary`, das in der Datei `ILoggingLibrary.shared.cs` enthalten ist, definiert die öffentliche Schnittstelle (die API-Oberfläche) der Komponente.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-131">The `ILoggingLibrary` project, which is contained in the `ILoggingLibrary.shared.cs` file, defines the public interface (the API surface area) of the component.</span></span> <span data-ttu-id="1f2f4-132">Hier definieren Sie die Schnittstelle zu Ihrer Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-132">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="1f2f4-133">Das andere gemeinsam genutzte Projekt, enthält Code in `CrossLoggingLibrary.shared.cs`, die eine plattformspezifische Implementierung der abstrakten Schnittstelle zur Laufzeit findet.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-133">The other Shared project contains code in `CrossLoggingLibrary.shared.cs` that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="1f2f4-134">In der Regel müssen an dieser Datei keine Änderungen vorgenommen werden.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-134">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="1f2f4-135">Die plattformspezifischen Projekte, z. B. `LoggingLibrary.android.cs`, enthalten alle in den jeweiligen `LoggingLibraryImplementation.cs`- (VS 2017) oder `LoggingLibrary.<PLATFORM>.cs`-Dateien (VS 2019) eine native Implementierung ihrer Schnittstelle.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-135">The platform-specific projects, such as `LoggingLibrary.android.cs`, each contain a native implementation of the interface in their respective `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) files.</span></span> <span data-ttu-id="1f2f4-136">Hier erstellen Sie den Code Ihrer Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-136">This is where you build out your library's code.</span></span>

<span data-ttu-id="1f2f4-137">Standardmäßig enthält die Datei „ILoggingLibrary.shared.cs“ des `ILoggingLibrary`-Projekts zwar eine Schnittstellendefinition, aber keine Methoden.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-137">By default, the ILoggingLibrary.shared.cs file of the `ILoggingLibrary` project contains an interface definition, but no methods.</span></span> <span data-ttu-id="1f2f4-138">Fügen Sie für diese exemplarische Vorgehensweise wie folgt eine `Log`-Methode hinzu:</span><span class="sxs-lookup"><span data-stu-id="1f2f4-138">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace Plugin.LoggingLibrary
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

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="1f2f4-139">Schreiben von plattformspezifischem Code</span><span class="sxs-lookup"><span data-stu-id="1f2f4-139">Write your platform-specific code</span></span>

<span data-ttu-id="1f2f4-140">Führen Sie die folgenden Schritte aus, um eine plattformspezifische Implementierung der `ILoggingLibrary`-Schnittstelle und deren Methoden zu implementieren:</span><span class="sxs-lookup"><span data-stu-id="1f2f4-140">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="1f2f4-141">Öffnen Sie die `LoggingLibraryImplementation.cs`- (VS 2017) oder `LoggingLibrary.<PLATFORM>.cs`-Datei (VS 2019) der Plattformprojekte, und fügen Sie den benötigten Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-141">Open the `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) file of each platform project and add the necessary code.</span></span> <span data-ttu-id="1f2f4-142">Beispiel (mithilfe des `Android`-Plattformprojekts):</span><span class="sxs-lookup"><span data-stu-id="1f2f4-142">For example (using the `Android` platform project):</span></span>

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Text;

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

1. <span data-ttu-id="1f2f4-143">Wiederholen Sie diese Implementierung in den Projekten für jede Plattform, die Sie unterstützen möchten.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-143">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="1f2f4-144">Klicken Sie mit der rechten Maustaste auf die Projektmappe, und wählen Sie **Projektmappe erstellen** aus, um Ihre Arbeit zu überprüfen und die Elemente zu erstellen, die Sie als Nächstes packen möchten.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="1f2f4-145">Wenn Ihnen Fehler aufgrund von fehlenden Verweisen angezeigt werden, klicken Sie mit der rechten Maustaste auf die Projektmappe, wählen Sie **NuGet-Pakete wiederherstellen** aus, um die Abhängigkeiten zu installieren, und erstellen Sie die Projektmappe erneut.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="1f2f4-146">Wenn Sie Visual Studio 2019 verwenden, müssen Sie vor der Auswahl von **NuGet-Pakete wiederherstellen** und dem Versuch einer Neuerstellung die Version von `MSBuild.Sdk.Extras` von `2.0.54` in `LoggingLibrary.csproj` ändern.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-146">If you are using Visual Studio 2019, before selecting **Restore NuGet Packages** and trying to rebuild, you need to change the version of `MSBuild.Sdk.Extras` to `2.0.54` in `LoggingLibrary.csproj`.</span></span> <span data-ttu-id="1f2f4-147">Auf diese Datei kann nur zugegriffen werden, indem Sie zuerst mit der rechten Maustaste auf das Projekt (unter der Projektmappe) klicken und `Unload Project` auswählen. Dann klicken Sie mit der rechten Maustaste auf das entladene Projekt und wählen `Edit LoggingLibrary.csproj` aus.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-147">This file can only be accessed by first right-clicking the project (below the solution) and selecting `Unload Project`, after which you right-click on the unloaded project and select `Edit LoggingLibrary.csproj`.</span></span>

> [!Note]
> <span data-ttu-id="1f2f4-148">Sie benötigen für die Erstellung für iOS einen Mac im Netzwerk, für den eine Verbindung mit Visual Studio besteht. Dies wird unter [Introduction to Xamarin.iOS for Visual Studio (Einführung in Xamarin.iOS für Visual Studio)](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-148">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="1f2f4-149">Wenn Sie keinen Mac zur Hand haben, entfernen Sie das iOS-Projekt aus dem Konfigurations-Manager (s. Schritt 3).</span><span class="sxs-lookup"><span data-stu-id="1f2f4-149">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="1f2f4-150">Erstellen und Aktualisieren der NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="1f2f4-150">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="1f2f4-151">Öffnen Sie eine Eingabeaufforderung, navigieren Sie zum `LoggingLibrary`-Ordner, der sich eine Ebene unter der `.sln`-Datei befindet, und führen Sie den `spec`-Befehl für NuGet aus, um eine erste Version der `Package.nuspec`-Datei zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="1f2f4-151">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="1f2f4-152">Benennen Sie diese Datei in `LoggingLibrary.nuspec` um, und öffnen Sie sie im Editor.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-152">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="1f2f4-153">Aktualisieren Sie die Datei, damit sie wie folgt aussieht, indem Sie „IHREN_NAMEN“ durch einen passenden Wert ersetzen.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-153">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="1f2f4-154">Insbesondere der `<id>`-Wert muss auf nuget.org eindeutig sein. Weitere Informationen zu den Namenskonventionen finden Sie unter [Creating a package (Erstellen eines Pakets)](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="1f2f4-154">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="1f2f4-155">Beachten Sie außerdem, dass Sie ebenfalls die Tags für den Autor und die Beschreibung ändern müssen, damit beim Packen kein Fehler ausgelöst wird.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-155">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2018</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="1f2f4-156">Sie können an Ihre Paketversion `-alpha`, `-beta` oder `-rc` anhängen, um die Pakete als Vorabversionen zu markieren. Weitere Informationen zu Vorabversionen finden Sie unter [Vorabversionen](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="1f2f4-156">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="1f2f4-157">Hinzufügen von Verweisassemblys</span><span class="sxs-lookup"><span data-stu-id="1f2f4-157">Add reference assemblies</span></span>

<span data-ttu-id="1f2f4-158">Fügen Sie, abhängig davon, welche Plattformen Sie unterstützen, dem `<files>`-Element von `LoggingLibrary.nuspec` Folgendes hinzu, um plattformspezifische Verweisassemblys hinzuzufügen:</span><span class="sxs-lookup"><span data-stu-id="1f2f4-158">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

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
> <span data-ttu-id="1f2f4-159">Klicken Sie mit der rechten Maustaste auf ein beliebiges Projekt, wählen Sie die Registerkarte **Bibliothek** aus, und ändern Sie die Assemblynamen, um die Namen der DLL- und XML-Dateien zu ändern.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-159">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="1f2f4-160">Hinzufügen von Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="1f2f4-160">Add dependencies</span></span>

<span data-ttu-id="1f2f4-161">Wenn Sie über bestimmte Abhängigkeiten für native Implementierungen verfügen, verwenden Sie das `<dependencies>`-Element zusammen mit `<group>`-Elementen, um diese anzugeben. Z.B.:</span><span class="sxs-lookup"><span data-stu-id="1f2f4-161">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

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

<span data-ttu-id="1f2f4-162">Im folgenden Beispiel wird „iTextSharp“ als Abhängigkeit für ein UAP-Ziel festgelegt:</span><span class="sxs-lookup"><span data-stu-id="1f2f4-162">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="1f2f4-163">Endgültige NUSPEC-Datei</span><span class="sxs-lookup"><span data-stu-id="1f2f4-163">Final .nuspec</span></span>

<span data-ttu-id="1f2f4-164">Die endgültige `.nuspec`-Datei sollte nun folgendermaßen aussehen, wobei Sie erneut YOUR_NAME durch einen passenden Wert ersetzen sollten:</span><span class="sxs-lookup"><span data-stu-id="1f2f4-164">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2018</copyright>
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

## <a name="package-the-component"></a><span data-ttu-id="1f2f4-165">Packen der Komponente</span><span class="sxs-lookup"><span data-stu-id="1f2f4-165">Package the component</span></span>

<span data-ttu-id="1f2f4-166">Mithilfe der vollständigen `.nuspec`-Datei, die auf alle Dateien verweist, die Sie in das Paket einfügen müssen, können Sie jetzt den `pack`-Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="1f2f4-166">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="1f2f4-167">Dadurch wird `LoggingLibrary.YOUR_NAME.1.0.0.nupkg` generiert.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-167">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="1f2f4-168">Wenn Sie diese Datei in einem Tool wie dem [NuGet-Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) öffnen und alle Knoten erweitern, werden Ihnen folgende Inhalte angezeigt:</span><span class="sxs-lookup"><span data-stu-id="1f2f4-168">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet-Paket-Explorer zeigt das LoggingLibrary-Paket an](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="1f2f4-170">Bei einer `.nupkg`-Datei handelt es sich um eine ZIP-Datei mit einer anderen Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-170">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="1f2f4-171">Sie können auch die Paketinhalte untersuchen, indem Sie `.nupkg` in `.zip` ändern. Denken Sie jedoch daran, die Erweiterung wiederherzustellen, bevor Sie ein Paket auf nuget.org hochladen.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-171">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="1f2f4-172">Befolgen Sie die Anweisungen unter [Veröffentlichen eines Pakets](../nuget-org/publish-a-package.md), um Ihr Paket für andere Entwickler zur Verfügung zu stellen.</span><span class="sxs-lookup"><span data-stu-id="1f2f4-172">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="1f2f4-173">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="1f2f4-173">Related topics</span></span>

- [<span data-ttu-id="1f2f4-174">NUSPEC-Referenz</span><span class="sxs-lookup"><span data-stu-id="1f2f4-174">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="1f2f4-175">Symbolpakete</span><span class="sxs-lookup"><span data-stu-id="1f2f4-175">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="1f2f4-176">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="1f2f4-176">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="1f2f4-177">Unterstützung mehrerer .NET Framework-Versionen</span><span class="sxs-lookup"><span data-stu-id="1f2f4-177">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="1f2f4-178">Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket</span><span class="sxs-lookup"><span data-stu-id="1f2f4-178">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="1f2f4-179">Erstellen von lokalisierten Paketen</span><span class="sxs-lookup"><span data-stu-id="1f2f4-179">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
