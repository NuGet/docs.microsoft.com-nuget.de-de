---
title: 'Vorgehensweise: Verpacken von UWP-Steuerelementen mit NuGet | Microsoft-Dokumentation'
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 3/21/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 1f9de20a-f394-4cf2-8e40-ba0f4239cd5e
description: "Vorgehensweise beim Erstellen von NuGet-Paketen mit UWP-Steuerelementen einschließlich der erforderlichen Metadaten und der unterstützenden Dateien für die Visual Studio- und Blend-Designer."
keywords: UWP-Steuerelemente von NuGet, Visual Studio XAML-Designer, Blend-Designer, benutzerdefinierte Steuerelemente
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f51dbabd406199752e4f9d612b498f59ffb54021
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="creating-uwp-controls-as-nuget-packages"></a>Erstellen von UWP-Steuerelementen als NuGet-Pakete

Mit Visual Studio 2017 können Sie zusätzliche Funktionen für UWP-Steuerelemente nutzen, die Sie in NuGet-Pakete übermitteln. Dieser Leitfaden führt Sie anhand des [ExtensionSDKasNuGetPackage-Beispiels](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage) durch diese Funktionen. 

## <a name="pre-requisites"></a>Voraussetzungen:

1.  Visual Studio 2017
1.  Kenntnisse hinsichtlich der [Erstellung von UWP-Paketen](create-uwp-packages.md)

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Hinzufügen von Unterstützung für die Toolbox bzw. den Bereich „Objekte“ bei XAML-Steuerelementen

Damit ein XAML-Steuerelement in der Toolbox des XAML-Designers in Visual Studio und im Bereich „Objekte“ in Blend angezeigt wird, müssen Sie im Stammverzeichnis des Ordners `tools` Ihres Paketprojekts die Datei `VisualStudioToolsManifest.xml` erstellen. Diese Datei ist nicht erforderlich, wenn das Steuerelement in der Toolbox oder im Bereich „Objekte“ nicht angezeigt werden muss.

```
\build
\lib
\tools
    \VisualStudioToolsManifest.xml
```    

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

Angenommen beispielsweise, Sie haben die TPMinV für Ihr Steuerelementpaket auf Windows 10 Anniversary Edition (10.0; Build 14393) festgelegt und möchten sicherstellen, dass das Paket nur von UWP-Projekten genutzt wird, die dieser Untergrenze entsprechen. Damit Ihr Paket von UWP-Projekten genutzt werden kann, die auf `project.json` basieren, müssen Sie Ihre Steuerelemente mit den folgenden Ordnernamen packen:

```
\lib\uap10.0\*
\ref\uap10.0\*
```

Erstellen Sie zur Durchsetzung einer entsprechenden Überprüfung der TPMinV eine [MSBuild-Zieldatei](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets) und verpacken diese unter dem Buildordner (indem Sie „your_assembly_name“ durch den Namen Ihrer spezifischen Assembly ersetzen):

```
\build
    \uap10.0
        your_assembly_name.targets
\lib
\tools
```

Im Folgenden wird ein Beispiel dafür aufgeführt, wie die Zieldatei aussehen sollte:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="Build;ReBuild" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a>Hinzufügen von Entwurfszeitunterstützung

Wenn Sie konfigurieren möchten, wo die Steuerelementeigenschaften in der Eigenschaftenanalyse erscheinen sollen, wo benutzerdefinierte Adorner hinzugefügt werden können usw., müssen Sie Ihre Datei entsprechend der Zielplattform `design.dll` im Ordner `lib\<platform>\Design` anordnen. Zudem sollten Sie `Generic.xaml` und alle Ressourcenverzeichnisse einschließen, die im Ordner `<AssemblyName>\Themes` zusammengeführt werden, um sicherzustellen, dass das Feature **[Vorlage bearbeiten > Kopie bearbeiten](https://docs.microsoft.com/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funktioniert. (Diese Datei hat keine Auswirkungen auf das Laufzeitverhalten eines Steuerelements.)


```
\build
\lib
    \uap10.0.14393.0
        \Design
            \MyControl.design.dll
        \your_assembly_name
            \Themes     
                Generic.xaml
\tools
```

> [!Note]
> Steuerelementeigenschaften werden in der Eigenschaftenanalyse standardmäßig in der Kategorie „Sonstiges“ angezeigt.


## <a name="use-strings-and-resources"></a>Verwenden von Zeichenfolgen und Ressourcen

Sie können Zeichenfolgenressourcen (`.resw`) in Ihr Paket einbetten, das durch Ihr Steuerelement oder das verwendete UWP-Projekt verwendet werden kann, und die Eigenschaft **Buildvorgang** der `.resw`-Datei auf **PRIResource** festlegen.

Ein entsprechendes Beispiel finden Sie unter [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) im ExtensionSDKasNuGetPackage-Beispiel.

## <a name="package-content-such-as-images"></a>Paketinhalte wie Images

Zum Packen von Inhalten wie Images, die von Ihrem Steuerelement oder dem verwendeten UWP-Projekt verwendet werden können. Fügen Sie diese Dateien wie folgt zum Ordner `lib\uap10.0.14393.0` hinzu (dabei sollte „your_assembly_name“ wieder Ihrem spezifischen Steuerelement entsprechen):

```
\build
\lib
    \uap10.0.14393.0
        \Design
        \your_assembly_name
\contosoSampleImage.jpg
\tools
```

Sie können auch eine [MSBuild-Zieldatei](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets) erstellen, um sicherzustellen, dass das Objekt in den Ausgabeordner des verwendeten Projekts kopiert wird:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0.14393.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a>Siehe auch

- [Erstellen von UWP-Paketen](create-uwp-packages.md)
- [Beispiel „ExtensionSDKasNuGetPackage“](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
