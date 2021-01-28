---
title: Packen von UWP-Steuerelementen mit NuGet
description: Vorgehensweise beim Erstellen von NuGet-Paketen mit UWP- oder WPF-Steuerelementen einschließlich der erforderlichen Metadaten und der unterstützenden Dateien für die Visual Studio- und Blend-Designer.
author: JonDouglas
ms.author: jodou
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: 317937b4d9d773d74384b8ebfcd2146062236ac1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774331"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="e929e-103">Erstellen von Benutzeroberflächensteuerelementen als NuGet-Pakete</span><span class="sxs-lookup"><span data-stu-id="e929e-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="e929e-104">Ab Visual Studio 2017 können Sie zusätzliche Funktionen für UWP- und WPF-Steuerelemente nutzen, die Sie in NuGet-Pakete bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="e929e-104">Starting with Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="e929e-105">Dieser Leitfaden führt Sie anhand des [ExtensionSDKasNuGetPackage-Beispiels](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage) durch diese Funktionen bezüglich UWP-Steuerelementen.</span><span class="sxs-lookup"><span data-stu-id="e929e-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="e929e-106">Das gleiche gilt auch für WPF-Steuerelemente, wenn nicht anders angegeben.</span><span class="sxs-lookup"><span data-stu-id="e929e-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e929e-107">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="e929e-107">Prerequisites</span></span>

1. <span data-ttu-id="e929e-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="e929e-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="e929e-109">Kenntnisse hinsichtlich der [Erstellung von UWP-Paketen](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="e929e-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="e929e-110">Layout für Bibliothek generieren</span><span class="sxs-lookup"><span data-stu-id="e929e-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="e929e-111">Dies gilt nur für UWP-Steuerelemente.</span><span class="sxs-lookup"><span data-stu-id="e929e-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="e929e-112">Wenn Sie die `GenerateLibraryLayout`-Eigenschaft festlegen, stellt dies sicher, dass die Projekterstellungsausgabe in einem Layout erzeugt wird, das direkt gepackt werden kann, ohne dass einzelne Dateieinträge in der NUSPEC-Datei erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="e929e-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="e929e-113">Navigieren Sie über die Projekteigenschaften zur Registerkarte „Erstellen“, und aktivieren Sie das Kontrollkästchen „Layout für Bibliothek generieren“.</span><span class="sxs-lookup"><span data-stu-id="e929e-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="e929e-114">Dadurch wird die Projektdatei modifiziert, und das Flag `GenerateLibraryLayout` wird für die aktuell ausgewählte Buildkonfiguration und Plattform auf TRUE festgelegt.</span><span class="sxs-lookup"><span data-stu-id="e929e-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="e929e-115">Alternativ können Sie die Projektdatei bearbeiten, um `<GenerateLibraryLayout>true</GenerateLibraryLayout>` der ersten nicht bedingten Eigenschaftengruppe hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="e929e-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="e929e-116">Dadurch wird die Eigenschaft unabhängig von Buildkonfiguration und Plattform angewendet.</span><span class="sxs-lookup"><span data-stu-id="e929e-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="e929e-117">Hinzufügen von Unterstützung für die Toolbox bzw. den Bereich „Objekte“ bei XAML-Steuerelementen</span><span class="sxs-lookup"><span data-stu-id="e929e-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="e929e-118">Damit ein XAML-Steuerelement in der Toolbox des XAML-Designers in Visual Studio und im Bereich „Objekte“ in Blend angezeigt wird, müssen Sie im Stammverzeichnis des Ordners `tools` Ihres Paketprojekts die Datei `VisualStudioToolsManifest.xml` erstellen.</span><span class="sxs-lookup"><span data-stu-id="e929e-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="e929e-119">Diese Datei ist nicht erforderlich, wenn das Steuerelement in der Toolbox oder im Bereich „Objekte“ nicht angezeigt werden muss.</span><span class="sxs-lookup"><span data-stu-id="e929e-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

```
\build
\lib
\tools
    VisualStudioToolsManifest.xml
```

<span data-ttu-id="e929e-120">Die Struktur der Datei lautet wie folgt:</span><span class="sxs-lookup"><span data-stu-id="e929e-120">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems UIFramework="WPF" VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="e929e-121">Dabei gilt:</span><span class="sxs-lookup"><span data-stu-id="e929e-121">where:</span></span>

- <span data-ttu-id="e929e-122">*your_package_file*: Der Name Ihrer Steuerungsdatei, wie z.B. `ManagedPackage.winmd` („ManagedPackage“ ist ein beliebiger, in diesem Beispiel verwendeter Name und hat keine andere Bedeutung).</span><span class="sxs-lookup"><span data-stu-id="e929e-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="e929e-123">*vs_category*: Die Beschriftung der Gruppe, in der das Steuerelement in der Toolbox des Visual Studio-Designers angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="e929e-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="e929e-124">Damit das Steuerelement in der Toolbox angezeigt wird, ist ein `VSCategory` erforderlich.</span><span class="sxs-lookup"><span data-stu-id="e929e-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
<span data-ttu-id="e929e-125">*ui_framework*: Der Name des Frameworks, z. B. „WPF“'. Beachten Sie, dass das Attribut `UIFramework` für ToolboxItems-Knoten in Visual Studio 16.7 Vorschau 3 oder höher erforderlich ist, damit das Steuerelement in der Toolbox angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="e929e-125">*ui_framework*: The name of the Framework, such as 'WPF', note that `UIFramework` attribute is required on ToolboxItems nodes on Visual Studio 16.7 Preview 3 or above for the control to appear in toolbox.</span></span>
- <span data-ttu-id="e929e-126">*blend_category*: Die Bezeichnung der Gruppe, in der das Steuerelement im Bereich „Objekte“ des Blend-Designers angezeigt werden sollte.</span><span class="sxs-lookup"><span data-stu-id="e929e-126">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="e929e-127">Damit das Steuerelement unter „Objekte“ angezeigt wird, ist `BlendCategory` erforderlich.</span><span class="sxs-lookup"><span data-stu-id="e929e-127">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="e929e-128">*type_full_name_n*: Der vollständig qualifizierte Name der einzelnen Steuerelemente, einschließlich des Namespace, z.B. `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="e929e-128">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="e929e-129">Beachten Sie, dass das Format mit Punkt für verwaltete und native Typen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="e929e-129">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="e929e-130">In erweiterten Szenarios können Sie auch mehrere `<File>`-Elemente innerhalb von `<FileList>` einschließen, wenn ein einzelnes Paket mehrere Steuerelementassemblys enthält.</span><span class="sxs-lookup"><span data-stu-id="e929e-130">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="e929e-131">Es können auch mehrere `<ToolboxItems>`-Knoten in einem einzelnen `<File>`-Element enthalten sein, wenn Sie Ihre Steuerelemente in separaten Kategorien organisieren möchten.</span><span class="sxs-lookup"><span data-stu-id="e929e-131">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="e929e-132">Im folgenden Beispiel wird das in `ManagedPackage.winmd` angezeigte Steuerelement in Visual Studio und Blend in einer Gruppe mit dem Namen „Verwaltetes Paket“ angezeigt, und „MyCustomControl“ wird in dieser Gruppe angezeigt.</span><span class="sxs-lookup"><span data-stu-id="e929e-132">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="e929e-133">Alle diese Namen wurden willkürlich ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="e929e-133">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems UIFramework="WPF" VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Ein Beispielsteuerelement, wie es in Visual Studio angezeigt wird](media/UWP-control-vs-toolbox.png)

![Ein Beispielsteuerelement, wie es in Blend angezeigt wird](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="e929e-136">Sie müssen explizit jedes Steuerelement angeben, das in der Toolbox bzw. im Bereich „Objekte“ angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="e929e-136">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="e929e-137">Stellen Sie sicher, dass Sie die Steuerelemente im Format `Namespace.ControlName` angeben.</span><span class="sxs-lookup"><span data-stu-id="e929e-137">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="e929e-138">Hinzufügen benutzerdefinierter Symbole zu Ihren Steuerelementen</span><span class="sxs-lookup"><span data-stu-id="e929e-138">Add custom icons to your controls</span></span>

<span data-ttu-id="e929e-139">Damit Sie ein benutzerdefiniertes Symbol in der Toolbox bzw. im Bereich „Objekte“ anzeigen können, müssen Sie ein Image zu Ihrem Projekt oder dem entsprechenden `design.dll`-Projekt mit dem Namen „Namespace.ControlName.extension“ hinzufügen und den Buildvorgang auf „Eingebettete Ressource“ festlegen.</span><span class="sxs-lookup"><span data-stu-id="e929e-139">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="e929e-140">Sie müssen außerdem sicherstellen, dass die zugeordnete `AssemblyInfo.cs` das ProvideMetadata-Attribut angibt: `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span><span class="sxs-lookup"><span data-stu-id="e929e-140">You must also ensure that the associated `AssemblyInfo.cs` specifies the ProvideMetadata attribute - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span></span> <span data-ttu-id="e929e-141">Sehen Sie sich dazu dieses [Beispiel](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20) an.</span><span class="sxs-lookup"><span data-stu-id="e929e-141">See this [sample](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span></span>

<span data-ttu-id="e929e-142">Als Formate werden `.png`, `.jpg`, `.jpeg`, `.gif` und `.bmp` unterstützt.</span><span class="sxs-lookup"><span data-stu-id="e929e-142">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="e929e-143">Das empfohlene Format lautet BMP24 in 16×16 Pixeln.</span><span class="sxs-lookup"><span data-stu-id="e929e-143">The recommended format is BMP24 in 16 pixels by 16 pixels.</span></span>

![Beispiel für das Toolbbox-Symbol](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

<span data-ttu-id="e929e-145">Der rosa Hintergrund wird zur Laufzeit ersetzt.</span><span class="sxs-lookup"><span data-stu-id="e929e-145">The pink background is replaced at runtime.</span></span> <span data-ttu-id="e929e-146">Die Farbe der Symbole wird geändert, wenn das Visual Studio-Design geändert wird und diese Hintergrundfarbe erwartet wird.</span><span class="sxs-lookup"><span data-stu-id="e929e-146">The icons are recolored when the Visual Studio theme is changed and that background color is expected.</span></span> <span data-ttu-id="e929e-147">Weitere Informationen finden Sie unter [Bilder und Symbole für Visual Studio](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="e929e-147">For more information, please reference [Images and Icons for Visual Studio](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span></span>

<span data-ttu-id="e929e-148">Im nachfolgenden Beispiel enthält das Projekt eine Imagedatei mit dem Namen „ManagedPackage.MyCustomControl.png“.</span><span class="sxs-lookup"><span data-stu-id="e929e-148">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Festlegen eines benutzerdefinierten Symbols in einem Projekt](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="e929e-150">Bei nativen Steuerelementen müssen Sie das Symbol im Projekt `design.dll` als Ressource einfügen.</span><span class="sxs-lookup"><span data-stu-id="e929e-150">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="e929e-151">Unterstützung bestimmter Windows-Plattformversionen</span><span class="sxs-lookup"><span data-stu-id="e929e-151">Support specific Windows platform versions</span></span>

<span data-ttu-id="e929e-152">UWP-Pakete weisen eine TargetPlatformVersion (TPV) und eine TargetPlatformMinVersion (TPMinV) auf, die die oberen und unteren Grenzen der Betriebssystemversion definieren, unter der die App installiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="e929e-152">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="e929e-153">TPV gibt ferner die Version des SDK an, für das die App erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="e929e-153">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="e929e-154">Achten Sie bei der Erstellung eines UWP-Pakets auf diese Eigenschaften: Durch die Verwendung von APIs außerhalb der Grenzen der in der App definierten Plattformversionen schlägt entweder das Build oder die App zur Laufzeit fehl.</span><span class="sxs-lookup"><span data-stu-id="e929e-154">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="e929e-155">Gehen wir z.B. davon aus, dass Sie die TPMinV für Ihr Steuerelementpaket auf Windows 10 Anniversary Edition (10.0; Build 14393) festgelegt haben und sicherstellen möchten, dass das Paket nur von UWP-Projekten genutzt wird, die dieser Untergrenze entsprechen.</span><span class="sxs-lookup"><span data-stu-id="e929e-155">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="e929e-156">Damit Ihr Paket von UWP-Projekten genutzt werden kann, müssen Sie Ihre Steuerelemente mit den folgenden Ordnernamen packen:</span><span class="sxs-lookup"><span data-stu-id="e929e-156">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

```
\lib\uap10.0.14393\*
\ref\uap10.0.14393\*
```

<span data-ttu-id="e929e-157">NuGet überprüft automatisch TPMinV des nutzenden Projekts und lässt die Installation fehlschlagen, wenn die Version niedriger als Windows 10 Anniversary Edition (10.0, Build 14393) ist.</span><span class="sxs-lookup"><span data-stu-id="e929e-157">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="e929e-158">Gehen wir bei WPF davon aus, dass Sie möchten, dass Ihr WPF-Steuerelementpaket von Projekten mit .NET Framework 4.6.1 oder höher als Ziel verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="e929e-158">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="e929e-159">Sie müssen Ihre Steuerelemente mit den folgenden Ordnernamen packen, um dies zu erzwingen:</span><span class="sxs-lookup"><span data-stu-id="e929e-159">To enforce that, you must package your controls with the following folder names:</span></span>

```
\lib\net461\*
\ref\net461\*
```

## <a name="add-design-time-support"></a><span data-ttu-id="e929e-160">Hinzufügen von Entwurfszeitunterstützung</span><span class="sxs-lookup"><span data-stu-id="e929e-160">Add design-time support</span></span>

<span data-ttu-id="e929e-161">Wenn Sie konfigurieren möchten, wo die Steuerelementeigenschaften in der Eigenschaftenanalyse erscheinen sollen, wo benutzerdefinierte Adorner hinzugefügt werden können usw., müssen Sie Ihre Datei entsprechend der Zielplattform `design.dll` im Ordner `lib\uap10.0.14393\Design` anordnen.</span><span class="sxs-lookup"><span data-stu-id="e929e-161">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="e929e-162">Zudem sollten Sie `Generic.xaml` und alle Ressourcenwörterbücher einschließen, die im Ordner `<your_assembly_name>\Themes` zusammengeführt werden, um sicherzustellen, dass das Feature **[Vorlage bearbeiten > Kopie bearbeiten](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funktioniert. (Verwenden Sie dafür erneut Ihren Assemblynamen).</span><span class="sxs-lookup"><span data-stu-id="e929e-162">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="e929e-163">(Diese Datei hat keine Auswirkungen auf das Laufzeitverhalten eines Steuerelements.) Die Ordnerstruktur sollte dann wie folgt angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="e929e-163">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

```
\lib
  \uap10.0.14393
    \Design
      \MyControl.design.dll
    \your_assembly_name
      \Themes
        Generic.xaml
```

<span data-ttu-id="e929e-164">Gehen wir für WPF weiterhin davon aus, dass Sie möchten, dass Ihr WPF-Steuerelementpaket von Projekten mit .NET Framework 4.6.1 oder höher als Ziel verwendet wird:</span><span class="sxs-lookup"><span data-stu-id="e929e-164">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

```
\lib
  \net461
    \Design
      \MyControl.design.dll
    \your_assembly_name
      \Themes
        Generic.xaml
```

> [!Note]
> <span data-ttu-id="e929e-165">Steuerelementeigenschaften werden in der Eigenschaftenanalyse standardmäßig in der Kategorie „Sonstiges“ angezeigt.</span><span class="sxs-lookup"><span data-stu-id="e929e-165">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="e929e-166">Verwenden von Zeichenfolgen und Ressourcen</span><span class="sxs-lookup"><span data-stu-id="e929e-166">Use strings and resources</span></span>

<span data-ttu-id="e929e-167">Sie können Zeichenfolgenressourcen (`.resw`) in Ihr Paket einbetten, das durch Ihr Steuerelement oder das verwendete UWP-Projekt verwendet werden kann, und die Eigenschaft **Buildvorgang** der `.resw`-Datei auf **PRIResource** festlegen.</span><span class="sxs-lookup"><span data-stu-id="e929e-167">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="e929e-168">Ein entsprechendes Beispiel finden Sie unter [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) im ExtensionSDKasNuGetPackage-Beispiel.</span><span class="sxs-lookup"><span data-stu-id="e929e-168">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="e929e-169">Dies gilt nur für UWP-Steuerelemente.</span><span class="sxs-lookup"><span data-stu-id="e929e-169">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="e929e-170">Weitere Informationen</span><span class="sxs-lookup"><span data-stu-id="e929e-170">See also</span></span>

- [<span data-ttu-id="e929e-171">Erstellen von UWP-Paketen</span><span class="sxs-lookup"><span data-stu-id="e929e-171">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="e929e-172">Beispiel „ExtensionSDKasNuGetPackage“</span><span class="sxs-lookup"><span data-stu-id="e929e-172">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)