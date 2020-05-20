---
title: Erstellen von NuGet-Paketen für die universelle Windows-Plattform
description: Eine exemplarische End-to-End-Vorgehensweise für das Erstellen von NuGet-Paketen für die universelle Windows-Plattform in C# mithilfe einer Komponente für Windows-Runtime.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231752"
---
# <a name="create-uwp-packages-c"></a>Erstellen von UWP-Paketen (C#)

Die [universelle Windows-Plattform (UWP)](/windows/uwp) stellt eine allgemeine App-Plattform bereit für alle Windows 10-Geräte bereit. Innerhalb dieses Modells können UWP-Apps sowohl die WinRT-APIs aufrufen, die für alle Geräte verwendet werden, als auch die APIs (einschließlich Win32 und .NET), die spezifisch für die Gerätefamilie sind, auf der die App ausgeführt wird.

In dieser exemplarischen Vorgehensweise erstellen Sie ein NuGet-Paket mit einer C#-UWP-Komponente (einschließlich eines XAML-Steuerelements), das für verwaltete und native Projekte verwendet werden kann.

## <a name="prerequisites"></a>Voraussetzungen

1. Visual Studio 2019: Sie können die 2019 Community Edition kostenlos über [visualstudio.com](https://www.visualstudio.com/) installieren oder die Professional bzw. Enterprise-Edition verwenden.

1. NuGet-CLI. Laden Sie die neuste Version von `nuget.exe` unter [nuget.org/downloads](https://nuget.org/downloads) herunter, und speichern Sie diese an einem beliebigen Ort (dies ist der direkte Download für die `.exe`). Fügen Sie diesen Speicherort, falls erforderlich, anschließend der Umgebungsvariable „PATH“ hinzu. [Weitere Informationen](/nuget/reference/nuget-exe-cli-reference#windows)

## <a name="create-a-uwp-windows-runtime-component"></a>Erstellen einer UWP-Komponente für Windows-Runtime

1. Klicken Sie in Visual Studio auf **Datei > Neu > Projekt**, und suchen Sie nach „uwp c#“. Wählen Sie die Vorlage **Komponente für Windows-Runtime (Universal Windows)** aus, klicken Sie auf „Weiter“, ändern Sie den Namen in ImageEnhancer, und klicken Sie auf „Erstellen“. Übernehmen Sie die Standardwerte für „Zielversion“ und „Mindestens erforderliche Version“, wenn Sie dazu aufgefordert werden.

    ![Erstellen eines neuen UWP-Projekts für eine Komponente für Windows-Runtime](media/UWP-NewProject-CS.png)

1. Klicken Sie mit der rechten Maustaste auf das Projekt in Projektmappen-Explorer, und klicken Sie auf **Hinzufügen > Neues Element**. Klicken Sie auf **Steuerelement mit Vorlagen**, ändern Sie den Namen in „AwesomeImageControl.cs“, und klicken Sie auf **Hinzufügen**:

    ![Hinzufügen eines neuen XAML-Steuerelements mit Vorlagen zum Projekt](media/UWP-NewXAMLControl-CS.png)

1. Klicken Sie in Projektmappen-Explorer mit der rechten Maustaste auf das Projekt, und wählen Sie **Eigenschaften** aus. Wählen Sie auf der Seite „Eigenschaften“ die Registerkarte **Erstellen** aus, und aktivieren Sie **XML-Dokumentationsdatei**:

    ![„XML-Dokumentationsdatei generieren“ auf „Ja“ einstellen](media/UWP-GenerateXMLDocFiles-CS.png)

1. Klicken Sie nun mit der rechten Maustaste auf *Projektmappe* und dann auf **Batcherstellung**. Aktivieren Sie wie im Folgenden gezeigt die fünf Kontrollkästchen im Dialogfeld. Damit stellen Sie sicher, dass alle Artefakte für jedes der von Windows unterstützten Zielsysteme generiert wurde, wenn Sie einen Build erstellen.

    ![Batcherstellung](media/UWP-BatchBuild-CS.png)

1. Klicken Sie im Dialogfeld „Batcherstellung“ auf **Erstellen**, um das Projekt zu überprüfen und die Ausgabedateien zu erstellen, die für das NuGet-Paket erforderlich sind.

> [!Note]
> In dieser exemplarischen Vorgehensweise werden die Debugartefakte für das Paket verwendet. Überprüfen Sie für Nichtdebugpakete stattdessen die Releaseoptionen im Dialogfeld „Batcherstellung“, und verwenden Sie in den folgenden Schritten die als Ergebnis angezeigten Ordner für Releases.

## <a name="create-and-update-the-nuspec-file"></a>Erstellen und Aktualisieren der NUSPEC-Datei

Befolgen Sie folgende drei Schritte, um die erste `.nuspec`-Datei zu erstellen. In den folgenden Schritten werden weitere erforderliche Updates erläutert.

1. Öffnen Sie die Eingabeaufforderung, und navigieren Sie zu dem Ordner, der `ImageEnhancer.csproj` enthält. Dabei handelt es sich um einen Unterordner des Speicherorts der Projektmappendatei.
1. Führen Sie den [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec)-Befehl aus, um `ImageEnhancer.nuspec` zu generieren (der Name der Datei wird dem Namen der `.csroj`-Datei entnommen):

    ```cli
    nuget spec
    ```

1. Öffnen Sie `ImageEnhancer.nuspec` in einem Editor, aktualisieren Sie die Datei gemäß den folgenden Angaben, und ersetzen Sie YOUR_NAME dabei durch einen entsprechenden Wert. Belassen Sie keinen der $propertyName$-Werte. Insbesondere der `<id>`-Wert muss auf nuget.org eindeutig sein. Weitere Informationen zu den Namenskonventionen finden Sie unter [Creating a package (Erstellen eines Pakets)](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number). Beachten Sie außerdem, dass Sie ebenfalls die Tags für den Autor und die Beschreibung ändern müssen, damit beim Packen kein Fehler ausgelöst wird.

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
> Bei Paketen, die für die öffentliche Nutzung bereitgestellt werden, sollten Sie besonders auf das `<tags>`-Element achten, da diese Tags andere Personen dabei unterstützen, nach Ihrem Paket zu suchen und dessen Zweck nachzuvollziehen.

### <a name="adding-windows-metadata-to-the-package"></a>Hinzufügen von Windows-Metadaten zum Paket

Eine Komponente für Windows-Runtime erfordert Metadaten, die alle öffentlich verfügbaren Typen beschreibt. Dadurch wird es anderen Apps und Bibliotheken ermöglicht, die Komponente zu nutzen. Die Metadaten sind in einer WINMD-Datei enthalten. Diese wird erstellt, wenn Sie das Projekt kompilieren und muss in Ihrem NuGet-Paket enthalten sein. Gleichzeitig wird außerdem eine XML-Datei mit IntelliSense-Daten erstellt, die ebenfalls enthalten sein sollte.

Fügen Sie der `.nuspec`-Datei folgenden `<files>`-Knoten hinzu:

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

### <a name="adding-xaml-content"></a>Hinzufügen von XAML-Inhalten

Wenn Sie Ihrer Komponente ein XAML-Steuerelement hinzufügen möchten, müssen Sie die XAML-Datei hinzufügen, die die Standardvorlage für das Steuerelement enthält. Diese wurde von der Projektvorlage generiert. Dies gilt ebenfalls für den Abschnitt `<files>`:

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

### <a name="adding-the-native-implementation-libraries"></a>Hinzufügen der nativen Bibliotheken für die Implementierung

Innerhalb Ihrer Komponente ist die Kernlogik des ImageEnhancer-Typs in nativem Code definiert. Dieser ist in den zahlreichen `ImageEnhancer.winmd`-Assemblys enthalten, die für jede Zielruntime (ARM, ARM64, x86 und x64) generiert werden. Verweisen Sie im Abschnitt `<files>` mithilfe der zugehörigen PRI-Ressourcendateien auf diese Assemblys, um diese in das Paket einzuschließen:

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

### <a name="final-nuspec"></a>Endgültige NUSPEC-Datei

Die endgültige `.nuspec`-Datei sollte nun folgendermaßen aussehen, wobei Sie erneut YOUR_NAME durch einen passenden Wert ersetzen sollten:

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

## <a name="package-the-component"></a>Packen der Komponente

Mithilfe der vollständigen `.nuspec`-Datei, die auf alle Dateien verweist, die Sie in das Paket einfügen müssen, können Sie jetzt den Befehl [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) ausführen:

```cli
nuget pack ImageEnhancer.nuspec
```

Dadurch wird die Datei `ImageEnhancer.YOUR_NAME.1.0.0.nupkg` generiert. Wenn Sie diese Datei in einem Tool wie dem [NuGet-Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) öffnen und alle Knoten erweitern, werden Ihnen folgende Inhalte angezeigt:

![Der NuGet-Paket-Explorer, der das ImageEnhancer-Paket anzeigt](media/UWP-PackageExplorer.png)

> [!Tip]
> Bei einer `.nupkg`-Datei handelt es sich um eine ZIP-Datei mit einer anderen Erweiterung. Sie können auch die Paketinhalte untersuchen, indem Sie `.nupkg` in `.zip` ändern. Denken Sie jedoch daran, die Erweiterung wiederherzustellen, bevor Sie ein Paket auf nuget.org hochladen.

Befolgen Sie die Anweisungen unter [Veröffentlichen eines Pakets](../nuget-org/publish-a-package.md), um Ihr Paket für andere Entwickler zur Verfügung zu stellen.

## <a name="related-topics"></a>Verwandte Themen

- [NUSPEC-Verweis](../reference/nuspec.md)
- [Symbolpakete](../create-packages/symbol-packages-snupkg.md)
- [Paketversionsverwaltung](../concepts/package-versioning.md)
- [Unterstützung mehrerer .NET Framework-Versionen](../create-packages/supporting-multiple-target-frameworks.md)
- [Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Erstellen von lokalisierten Paketen](../create-packages/creating-localized-packages.md)
