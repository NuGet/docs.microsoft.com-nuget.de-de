---
title: Packen von UWP-Steuerelementen mit NuGet
description: Vorgehensweise beim Erstellen von NuGet-Paketen mit UWP- oder WPF-Steuerelementen einschließlich der erforderlichen Metadaten und der unterstützenden Dateien für die Visual Studio- und Blend-Designer.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: e1ebf5042597693ee55d986a4f93e797c27ad30a
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622706"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>Erstellen von Benutzeroberflächensteuerelementen als NuGet-Pakete

Ab Visual Studio 2017 können Sie zusätzliche Funktionen für UWP- und WPF-Steuerelemente nutzen, die Sie in NuGet-Pakete bereitstellen. Dieser Leitfaden führt Sie anhand des [ExtensionSDKasNuGetPackage-Beispiels](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage) durch diese Funktionen bezüglich UWP-Steuerelementen. Das gleiche gilt auch für WPF-Steuerelemente, wenn nicht anders angegeben.

## <a name="prerequisites"></a>Voraussetzungen

1. Visual Studio 2017
1. Kenntnisse hinsichtlich der [Erstellung von UWP-Paketen](create-uwp-packages.md)

## <a name="generate-library-layout"></a>Layout für Bibliothek generieren

> [!Note]
> Dies gilt nur für UWP-Steuerelemente.

Wenn Sie die `GenerateLibraryLayout`-Eigenschaft festlegen, stellt dies sicher, dass die Projekterstellungsausgabe in einem Layout erzeugt wird, das direkt gepackt werden kann, ohne dass einzelne Dateieinträge in der NUSPEC-Datei erforderlich sind.

Navigieren Sie über die Projekteigenschaften zur Registerkarte „Erstellen“, und aktivieren Sie das Kontrollkästchen „Layout für Bibliothek generieren“. Dadurch wird die Projektdatei modifiziert, und das Flag `GenerateLibraryLayout` wird für die aktuell ausgewählte Buildkonfiguration und Plattform auf TRUE festgelegt.

Alternativ können Sie die Projektdatei bearbeiten, um `<GenerateLibraryLayout>true</GenerateLibraryLayout>` der ersten nicht bedingten Eigenschaftengruppe hinzuzufügen. Dadurch wird die Eigenschaft unabhängig von Buildkonfiguration und Plattform angewendet.

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
    <ToolboxItems UIFramework="WPF" VSCategory="vs_category" BlendCategory="blend_category">
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
- *vs_category*: Die Beschriftung der Gruppe, in der das Steuerelement in der Toolbox des Visual Studio-Designers angezeigt werden soll. Damit das Steuerelement in der Toolbox angezeigt wird, ist ein `VSCategory` erforderlich.
*ui_framework*: Der Name des Frameworks, z. B. „WPF“'. Beachten Sie, dass das Attribut `UIFramework` für ToolboxItems-Knoten in Visual Studio 16.7 Vorschau 3 oder höher erforderlich ist, damit das Steuerelement in der Toolbox angezeigt wird.
- *blend_category*: Die Bezeichnung der Gruppe, in der das Steuerelement im Bereich „Objekte“ des Blend-Designers angezeigt werden sollte. Damit das Steuerelement unter „Objekte“ angezeigt wird, ist `BlendCategory` erforderlich.
- *type_full_name_n*: Der vollständig qualifizierte Name der einzelnen Steuerelemente, einschließlich des Namespace, z.B. `ManagedPackage.MyCustomControl`. Beachten Sie, dass das Format mit Punkt für verwaltete und native Typen verwendet wird.

In erweiterten Szenarios können Sie auch mehrere `<File>`-Elemente innerhalb von `<FileList>` einschließen, wenn ein einzelnes Paket mehrere Steuerelementassemblys enthält. Es können auch mehrere `<ToolboxItems>`-Knoten in einem einzelnen `<File>`-Element enthalten sein, wenn Sie Ihre Steuerelemente in separaten Kategorien organisieren möchten.

Im folgenden Beispiel wird das in `ManagedPackage.winmd` angezeigte Steuerelement in Visual Studio und Blend in einer Gruppe mit dem Namen „Verwaltetes Paket“ angezeigt, und „MyCustomControl“ wird in dieser Gruppe angezeigt. Alle diese Namen wurden willkürlich ausgewählt.

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
> Sie müssen explizit jedes Steuerelement angeben, das in der Toolbox bzw. im Bereich „Objekte“ angezeigt werden soll. Stellen Sie sicher, dass Sie die Steuerelemente im Format `Namespace.ControlName` angeben.

## <a name="add-custom-icons-to-your-controls"></a>Hinzufügen benutzerdefinierter Symbole zu Ihren Steuerelementen

Damit Sie ein benutzerdefiniertes Symbol in der Toolbox bzw. im Bereich „Objekte“ anzeigen können, müssen Sie ein Image zu Ihrem Projekt oder dem entsprechenden `design.dll`-Projekt mit dem Namen „Namespace.ControlName.extension“ hinzufügen und den Buildvorgang auf „Eingebettete Ressource“ festlegen. Sie müssen außerdem sicherstellen, dass die zugeordnete `AssemblyInfo.cs` das ProvideMetadata-Attribut angibt: `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`. Sehen Sie sich dazu dieses [Beispiel](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20) an.

Als Formate werden `.png`, `.jpg`, `.jpeg`, `.gif` und `.bmp` unterstützt. Das empfohlene Format lautet BMP24 in 16×16 Pixeln.

![Beispiel für das Toolbbox-Symbol](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

Der rosa Hintergrund wird zur Laufzeit ersetzt. Die Farbe der Symbole wird geändert, wenn das Visual Studio-Design geändert wird und diese Hintergrundfarbe erwartet wird. Weitere Informationen finden Sie unter [Bilder und Symbole für Visual Studio](https://docs.microsoft.com/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).

Im nachfolgenden Beispiel enthält das Projekt eine Imagedatei mit dem Namen „ManagedPackage.MyCustomControl.png“.

![Festlegen eines benutzerdefinierten Symbols in einem Projekt](media/UWP-control-custom-icon.png)

> [!Note]
> Bei nativen Steuerelementen müssen Sie das Symbol im Projekt `design.dll` als Ressource einfügen.

## <a name="support-specific-windows-platform-versions"></a>Unterstützung bestimmter Windows-Plattformversionen

UWP-Pakete weisen eine TargetPlatformVersion (TPV) und eine TargetPlatformMinVersion (TPMinV) auf, die die oberen und unteren Grenzen der Betriebssystemversion definieren, unter der die App installiert werden kann. TPV gibt ferner die Version des SDK an, für das die App erstellt wird. Achten Sie bei der Erstellung eines UWP-Pakets auf diese Eigenschaften: Durch die Verwendung von APIs außerhalb der Grenzen der in der App definierten Plattformversionen schlägt entweder das Build oder die App zur Laufzeit fehl.

Gehen wir z.B. davon aus, dass Sie die TPMinV für Ihr Steuerelementpaket auf Windows 10 Anniversary Edition (10.0; Build 14393) festgelegt haben und sicherstellen möchten, dass das Paket nur von UWP-Projekten genutzt wird, die dieser Untergrenze entsprechen. Damit Ihr Paket von UWP-Projekten genutzt werden kann, müssen Sie Ihre Steuerelemente mit den folgenden Ordnernamen packen:

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

NuGet überprüft automatisch TPMinV des nutzenden Projekts und lässt die Installation fehlschlagen, wenn die Version niedriger als Windows 10 Anniversary Edition (10.0, Build 14393) ist.

Gehen wir bei WPF davon aus, dass Sie möchten, dass Ihr WPF-Steuerelementpaket von Projekten mit .NET Framework 4.6.1 oder höher als Ziel verwendet wird. Sie müssen Ihre Steuerelemente mit den folgenden Ordnernamen packen, um dies zu erzwingen:

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a>Hinzufügen von Entwurfszeitunterstützung

Wenn Sie konfigurieren möchten, wo die Steuerelementeigenschaften in der Eigenschaftenanalyse erscheinen sollen, wo benutzerdefinierte Adorner hinzugefügt werden können usw., müssen Sie Ihre Datei entsprechend der Zielplattform `design.dll` im Ordner `lib\uap10.0.14393\Design` anordnen. Zudem sollten Sie `Generic.xaml` und alle Ressourcenwörterbücher einschließen, die im Ordner `<your_assembly_name>\Themes` zusammengeführt werden, um sicherzustellen, dass das Feature **[Vorlage bearbeiten > Kopie bearbeiten](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funktioniert. (Verwenden Sie dafür erneut Ihren Assemblynamen). (Diese Datei hat keine Auswirkungen auf das Laufzeitverhalten eines Steuerelements.) Die Ordnerstruktur sollte dann wie folgt angezeigt werden:

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


Gehen wir für WPF weiterhin davon aus, dass Sie möchten, dass Ihr WPF-Steuerelementpaket von Projekten mit .NET Framework 4.6.1 oder höher als Ziel verwendet wird:

    \lib
      \net461
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

> [!Note]
> Dies gilt nur für UWP-Steuerelemente.

## <a name="see-also"></a>Weitere Informationen

- [Erstellen von UWP-Paketen](create-uwp-packages.md)
- [Beispiel „ExtensionSDKasNuGetPackage“](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
