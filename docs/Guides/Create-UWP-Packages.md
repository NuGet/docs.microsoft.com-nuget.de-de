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
# <a name="create-uwp-packages"></a>Erstellen von UWP-Paketen

Die [universelle Windows-Plattform (UWP)](https://developer.microsoft.com/windows) stellt eine allgemeine App-Plattform bereit für alle Windows 10-Geräte bereit. Innerhalb dieses Modells können UWP-Apps sowohl die WinRT-APIs aufrufen, die für alle Geräte verwendet werden, als auch die APIs (einschließlich Win32 und .NET), die spezifisch für die Gerätefamilie sind, auf der die App ausgeführt wird.

In dieser exemplarischen Vorgehensweise erstellen Sie ein NuGet-Paket mit einer nativen UWP-Komponente (einschließlich eines XAML-Steuerelements), das für verwaltete und native Projekte verwendet werden kann.

## <a name="prerequisites"></a>Erforderliche Komponenten

1. Visual Studio 2017 oder Visual Studio 2015. Sie können die 2017 Community Edition kostenlos über [visualstudio.com](https://www.visualstudio.com/) installieren oder die Professional bzw. Enterprise-Edition verwenden.

1. NuGet-CLI. Laden Sie die neuste Version von `nuget.exe` unter [nuget.org/downloads](https://nuget.org/downloads) herunter, und speichern Sie diese an einem beliebigen Ort (dies ist der direkte Download für die `.exe`). Fügen Sie diesen Speicherort, falls erforderlich, anschließend der Umgebungsvariable „PATH“ hinzu.

## <a name="create-a-uwp-windows-runtime-component"></a>Erstellen einer UWP-Komponente für Windows-Runtime

1. Klicken Sie in Visual Studio auf **Datei > Neu > Projekt**, und erweitern Sie den Knoten **Visual C++ > Windows > Universell**. Wählen Sie die Vorlage **Komponente für Windows-Runtime (Universal Windows)** aus, ändern Sie den Namen in ImageEnhancer, und klicken Sie auf OK. Übernehmen Sie die Standardwerte für „Zielversion“ und „Mindestens erforderliche Version“, wenn Sie dazu aufgefordert werden.

    ![Erstellen eines neuen UWP-Projekts für eine Komponente für Windows-Runtime](media/UWP-NewProject.png)

1. Klicken Sie mit der rechten Maustaste auf das Projekt in Projektmappen-Explorer, klicken Sie auf **Hinzufügen > Neues Element** und dann auf den Knoten **Visual C++ > XAML**. Klicken Sie auf **Steuerelement mit Vorlagen**, ändern Sie den Namen in „AwesomeImageControl.cpp“, und klicken Sie auf **Hinzufügen**:

    ![Hinzufügen eines neuen XAML-Steuerelements mit Vorlagen zum Projekt](media/UWP-NewXAMLControl.png)

1. Klicken Sie in Projektmappen-Explorer mit der rechten Maustaste auf das Projekt, und wählen Sie **Eigenschaften** aus. Erweitern Sie **Konfigurationseigenschaften > C/C++** auf der Seite „Eigenschaften“, und klicken Sie auf **Ausgabedateien**. Ändern Sie den Wert für **XML-Dokumentationsdateien generieren** im rechten Bereich in „Ja“.

    ![„XML-Dokumentationsdatei generieren“ auf „Ja“ einstellen](media/UWP-GenerateXMLDocFiles.png)

1. Klicken Sie nun mit der rechten Maustaste auf *Projektmappe* und dann auf **Batcherstellung**. Aktivieren Sie wie im Folgenden dargestellt die drei Kontrollkästchen für das Debuggen. Damit stellen Sie sicher, dass alle Artefakte für jedes der von Windows unterstützten Zielsysteme generiert wurde, wenn Sie einen Build erstellen.

    ![Batcherstellung](media/UWP-BatchBuild.png)

1. Klicken Sie im Dialogfeld „Batcherstellung“ auf **Erstellen**, um das Projekt zu überprüfen und die Ausgabedateien zu erstellen, die für das NuGet-Paket erforderlich sind.

> [!Note]
> In dieser exemplarischen Vorgehensweise werden die Debugartefakte für das Paket verwendet. Überprüfen Sie für Nichtdebugpakete stattdessen die Releaseoptionen im Dialogfeld „Batcherstellung“, und verwenden Sie in den folgenden Schritten die als Ergebnis angezeigten Ordner für Releases.

## <a name="create-and-update-the-nuspec-file"></a>Erstellen und Aktualisieren der NUSPEC-Datei

Befolgen Sie folgende drei Schritte, um die erste `.nuspec`-Datei zu erstellen. In den folgenden Schritten werden weitere erforderliche Updates erläutert.

1. Öffnen Sie die Eingabeaufforderung, und navigieren Sie zu dem Ordner, der `ImageEnhancer.vcxproj` enthält. Dabei handelt es sich um einen Unterordner des Speicherorts der Projektmappendatei.
1. Führen Sie den NuGet-Befehl `spec` aus, um `ImageEnhancer.nuspec` zu generieren. Der Name der Datei wird dem Namen der `.vcxproj`-Datei entnommen:

    ```cli
    nuget spec
    ```

1. Öffnen Sie `ImageEnhancer.nuspec` in einem Editor, und aktualisieren Sie die Datei, damit Sie dem Folgenden entspricht. Dabei wird YOUR_NAME durch einen passenden Wert ersetzt. Insbesondere der `<id>`-Wert muss auf nuget.org eindeutig sein. Weitere Informationen zu den Namenskonventionen finden Sie unter [Creating a package (Erstellen eines Pakets)](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). Beachten Sie außerdem, dass Sie ebenfalls die Tags für den Autor und die Beschreibung ändern müssen, damit beim Packen kein Fehler ausgelöst wird.

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
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
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

Innerhalb Ihrer Komponente ist die Kernlogik des ImageEnhancer-Typs in nativem Code definiert. Dieser ist in den zahlreichen `ImageEnhancer.dll`-Assemblys enthalten, die für jede Zielruntime (ARM, x86, x64) generiert werden. Verweisen Sie im Abschnitt `<files>` mithilfe der zugehörigen PRI-Ressourcendateien auf diese Assemblys, um diese in das Paket einzuschließen:

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

### <a name="adding-targets"></a>Hinzufügen von TARGETS-Dateien

Als nächstes benötigen die C++- und JavaScript-Projekte, die Ihr NuGet-Paket möglicherweise verwenden, eine TARGETS-Datei, um die notwendigen Assembly- und WINMD-Dateien zu identifizieren. (In C#- und Visual Basic-Projekten wird dies automatisch erledigt.) Erstellen Sie diese Datei, indem Sie den unten stehenden Text in `ImageEnhancer.targets` kopieren und diese im gleichen Ordner wie die `.nuspec`-Datei speichern. _Hinweis:_ Der Name der `.targets`-Datei muss die Paket-ID enthalten (also z.B. das `<Id>`-Element in der `.nupspec`-Datei):

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

Verweisen Sie dann in Ihrer `.nuspec`-Datei auf `ImageEnhancer.targets`:

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

## <a name="package-the-component"></a>Packen der Komponente

Mithilfe der vollständigen `.nuspec`-Datei, die auf alle Dateien verweist, die Sie in das Paket einfügen müssen, können Sie jetzt den `pack`-Befehl ausführen:

```cli
nuget pack ImageEnhancer.nuspec
```

Dadurch wird die Datei `ImageEnhancer.YOUR_NAME.1.0.0.nupkg` generiert. Wenn Sie diese Datei in einem Tool wie dem [NuGet-Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) öffnen und alle Knoten erweitern, werden Ihnen folgende Inhalte angezeigt:

![Der NuGet-Paket-Explorer, der das ImageEnhancer-Paket anzeigt](media/UWP-PackageExplorer.png)

> [!Tip]
> Bei einer `.nupkg`-Datei handelt es sich um eine ZIP-Datei mit einer anderen Erweiterung. Sie können auch die Paketinhalte untersuchen, indem Sie `.nupkg` in `.zip` ändern. Denken Sie jedoch daran, die Erweiterung wiederherzustellen, bevor Sie ein Paket auf nuget.org hochladen.

Befolgen Sie die Anweisungen unter [Veröffentlichen eines Pakets](../create-packages/publish-a-package.md), um Ihr Paket für andere Entwickler zur Verfügung zu stellen.

## <a name="related-topics"></a>Verwandte Themen

- [NUSPEC-Verweis](../reference/nuspec.md)
- [Symbolpakete](../create-packages/symbol-packages.md)
- [Paketversionsverwaltung](../reference/package-versioning.md)
- [Unterstützung mehrerer .NET Framework-Versionen](../create-packages/supporting-multiple-target-frameworks.md)
- [Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Erstellen von lokalisierten Paketen](../create-packages/creating-localized-packages.md)
