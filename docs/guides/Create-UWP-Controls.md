---
title: 'Vorgehensweise: Verpacken von UWP-Steuerelementen mit NuGet | Microsoft-Dokumentation'
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/14/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Vorgehensweise beim Erstellen von NuGet-Paketen mit UWP-Steuerelementen einschließlich der erforderlichen Metadaten und der unterstützenden Dateien für die Visual Studio- und Blend-Designer."
keywords: UWP-Steuerelemente von NuGet, Visual Studio XAML-Designer, Blend-Designer, benutzerdefinierte Steuerelemente
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1af5118eb71836d8b8bcfa8ff713d9fef3c86374
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a>Erstellen von UWP-Steuerelementen als NuGet-Pakete

Mit Visual Studio 2017 können Sie zusätzliche Funktionen für UWP-Steuerelemente nutzen, die Sie in NuGet-Pakete übermitteln. Dieser Leitfaden führt Sie anhand des [ExtensionSDKasNuGetPackage-Beispiels](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage) durch diese Funktionen. 

## <a name="prerequisites"></a>Erforderliche Komponenten

1. Visual Studio 2017
1. Kenntnisse hinsichtlich der [Erstellung von UWP-Paketen](create-uwp-packages.md)

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Hinzufügen von Unterstützung für die Toolbox bzw. den Bereich „Objekte“ bei XAML-Steuerelementen

Damit ein XAML-Steuerelement in der Toolbox des XAML-Designers in Visual Studio und im Bereich „Objekte“ in Blend angezeigt wird, müssen Sie im Stammverzeichnis des Ordners `tools` Ihres Paketprojekts die Datei `VisualStudioToolsManifest.xml` erstellen. Diese Datei ist nicht erforderlich, wenn das Steuerelement in der Toolbox oder im Bereich „Objekte“ nicht angezeigt werden muss.

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

Die Struktur der Datei lautet wie folgt:

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

Dabei gilt:

- *your_package_file*: Der Name Ihrer Steuerungsdatei, wie z.B. `ManagedPackage.winmd` („ManagedPackage“ ist ein beliebiger, in diesem Beispiel verwendeter Name und hat keine andere Bedeutung).
- *vs_category*: Die Bezeichnung der Gruppe, in der das Steuerelement in der Toolbox des Visual Studio-Designers angezeigt werden sollte. Damit das Steuerelement in der Toolbox angezeigt wird, ist ein `VSCategory` erforderlich.
- *blend_category*: Die Bezeichnung der Gruppe, in der das Steuerelement im Bereich „Objekte“ des Blend-Designers angezeigt werden sollte. Damit das Steuerelement unter „Objekte“ angezeigt wird, ist `BlendCategory` erforderlich.
- *type_full_name_n*: Der vollständig qualifizierte Name der einzelnen Steuerelemente, einschließlich des Namespace, z.B. `ManagedPackage.MyCustomControl`. Beachten Sie, dass das Format mit Punkt für verwaltete und native Typen verwendet wird.

In erweiterten Szenarios können Sie auch mehrere `<File>`-Elemente innerhalb von `<FileList>` einschließen, wenn ein einzelnes Paket mehrere Steuerelementassemblys enthält. Es können auch mehrere `<ToolboxItems>`-Knoten in einem einzelnen `<File>`-Element enthalten sein, wenn Sie Ihre Steuerelemente in separaten Kategorien organisieren möchten.

Im folgenden Beispiel wird das in `ManagedPackage.winmd` angezeigte Steuerelement in Visual Studio und Blend in einer Gruppe mit dem Namen „Verwaltetes Paket“ angezeigt, und „MyCustomControl“ wird in dieser Gruppe angezeigt. Alle diese Namen wurden willkürlich ausgewählt.

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Ein Beispielsteuerelement, wie es in Visual Studio angezeigt wird](media/UWP-control-vs-toolbox.png)

![Ein Beispielsteuerelement, wie es in Blend angezeigt wird](media/UWP-control-blend-assets.png)

> [!Note]
> Sie müssen explizit jedes Steuerelement angeben, das in der Toolbox bzw. im Bereich „Objekte“ angezeigt werden soll. Stellen Sie sicher, dass Sie die Steuerelemente im Format `Namespace.ControlName` angeben.

## <a name="add-custom-icons-to-your-controls"></a>Hinzufügen benutzerdefinierter Symbole zu Ihren Steuerelementen

Damit Sie ein benutzerdefiniertes Symbol in der Toolbox bzw. im Bereich „Objekte“ anzeigen können, müssen Sie ein Image zu Ihrem Projekt oder dem entsprechenden `design.dll`-Projekt mit dem Namen „Namespace.ControlName.extension“ hinzufügen und den Buildvorgang auf „Eingebettete Ressource“ festlegen. Als Formate werden `.png`, `.jpg`, `.jpeg`, `.gif` und `.bmp` unterstützt. Die empfohlene Bildgröße ist 64 x 64 Pixel.

Im nachfolgenden Beispiel enthält das Projekt eine Imagedatei mit dem Namen „ManagedPackage.MyCustomControl.png“.

![Festlegen eines benutzerdefinierten Symbols in einem Projekt](media/UWP-control-custom-icon.png)

> [!Note]
> Bei nativen Steuerelementen müssen Sie das Symbol im Projekt `design.dll` als Ressource einfügen.

## <a name="support-specific-windows-platform-versions"></a>Unterstützung bestimmter Windows-Plattformversionen

UWP-Pakete weisen eine TargetPlatformVersion (TPV) und eine TargetPlatformMinVersion (TPMinV) auf, die die oberen und unteren Grenzen der Betriebssystemversion definieren, unter der die App installiert werden kann. TPV gibt ferner die Version des SDK an, für das die App erstellt wird. Achten Sie bei der Erstellung eines UWP-Pakets auf diese Eigenschaften: Durch die Verwendung von APIs außerhalb der Grenzen der in der App definierten Plattformversionen schlägt entweder das Build oder die App zur Laufzeit fehl.

Angenommen beispielsweise, Sie haben die TPMinV für Ihr Steuerelementpaket auf Windows 10 Anniversary Edition (10.0; Build 14393) festgelegt und möchten sicherstellen, dass das Paket nur von UWP-Projekten genutzt wird, die dieser Untergrenze entsprechen. Damit Ihr Paket von UWP-Projekten genutzt werden kann, müssen Sie Ihre Steuerelemente mit den folgenden Ordnernamen packen:

    \lib\uap10.0\*
    \ref\uap10.0\*

Erstellen Sie zur Durchsetzung einer entsprechenden Überprüfung von TPMinV eine [MSBuild-Zieldatei](/visualstudio/msbuild/msbuild-targets), und packen Sie diese unter `build\uap10.0" folder as `<your_assembly_name>.targets`, replacing `<your_assembly_name> mit dem Namen Ihrer spezifischen Assembly.

Im Folgenden wird ein Beispiel dafür aufgeführt, wie die Zieldatei aussehen sollte:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="ResolveAssemblyReferences" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a>Hinzufügen von Entwurfszeitunterstützung

Wenn Sie konfigurieren möchten, wo die Steuerelementeigenschaften in der Eigenschaftenanalyse erscheinen sollen, wo benutzerdefinierte Adorner hinzugefügt werden können usw., müssen Sie Ihre Datei entsprechend der Zielplattform `design.dll` im Ordner `lib\uap10.0\Design` anordnen. Zudem sollten Sie `Generic.xaml` und alle Ressourcenwörterbücher einschließen, die im Ordner `<your_assembly_name>\Themes` zusammengeführt werden, um sicherzustellen, dass das Feature **[Vorlage bearbeiten > Kopie bearbeiten](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funktioniert. (Verwenden Sie dafür erneut Ihren Assemblynamen). (Diese Datei hat keine Auswirkungen auf das Laufzeitverhalten eines Steuerelements.) Die Ordnerstruktur sollte dann wie folgt angezeigt werden:

    \lib
      \uap10.0
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> Steuerelementeigenschaften werden in der Eigenschaftenanalyse standardmäßig in der Kategorie „Sonstiges“ angezeigt.

## <a name="use-strings-and-resources"></a>Verwenden von Zeichenfolgen und Ressourcen

Sie können Zeichenfolgenressourcen (`.resw`) in Ihr Paket einbetten, das durch Ihr Steuerelement oder das verwendete UWP-Projekt verwendet werden kann, und die Eigenschaft **Buildvorgang** der `.resw`-Datei auf **PRIResource** festlegen.

Ein entsprechendes Beispiel finden Sie unter [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) im ExtensionSDKasNuGetPackage-Beispiel.

## <a name="package-content-such-as-images"></a>Paketinhalte wie Images

Platzieren Sie zum Packen von Inhalten wie Images, die von Ihrem Steuerelement oder dem verwendeten UWP-Projekt verwendet werden können, diese Dateien in dem `lib\uap10.0`-Ordner.

Sie können auch eine [MSBuild-Zieldatei](/visualstudio/msbuild/msbuild-targets) erstellen, um sicherzustellen, dass das Objekt in den Ausgabeordner des verwendeten Projekts kopiert wird:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a>Siehe auch

- [Erstellen von UWP-Paketen](create-uwp-packages.md)
- [Beispiel „ExtensionSDKasNuGetPackage“](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
