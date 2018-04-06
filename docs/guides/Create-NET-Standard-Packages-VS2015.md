---
title: Erstellen von .NET Standard- und .NET Framework-NuGet-Paketen mit Visual Studio 2015 | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: Eine exemplarische End-to-End-Vorgehensweise zum Erstellen von .NET Standard- und .NET Framework-NuGet-Paketen mithilfe von NuGet 3.x und Visual Studio 2015.
keywords: Erstellen eines Pakets, .NET Standard-Pakete, .NET Framework-Pakete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: dbe0a0788b5fc9ba37f7db601bd51c3e4f78f5b8
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a>Erstellen von .NET Standard- und .NET Framework-Paketen mit Visual Studio 2015

**Hinweis**: Visual Studio 2017 wird für die Entwicklung von .NET Standard-Bibliotheken empfohlen. Visual Studio 2015 kann auch funktionieren, aber die .NET Core-Tools befinden sich darin noch im Vorschaustadium. Unter [Erstellen und Veröffentlichen eines Pakets mithilfe von Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) finden Sie weitere Informationen zum Arbeiten mit NuGet 4.x und höher sowie mit Visual Studio 2017.

Die [.NET-Standardbibliothek](/dotnet/articles/standard/library) ist eine formale Spezifikation von .NET-APIs, die in allen .NET-Runtimes verfügbar sein soll, um so eine umfassendere Einheitlichkeit im .NET-Ökosystem herzustellen. Die .NET-Standardbibliothek definiert einen einheitlichen Satz von BCL-APIs (Base Class Library), die unabhängig von der Workload für alle .NET-Plattformen implementiert werden. Sie ermöglicht Entwicklern, Code zu erzeugen, der für alle .NET-Runtimes verwendet werden kann, und reduziert plattformspezifische Anweisungen für die bedingte Kompilierung in freigegebenem Code, wenn diese nicht sogar ausgeschlossen werden.

Dieser Leitfaden begleitet Sie durch das Erstellen eines NuGet-Pakets für die .NET Standard 1.4-Bibliothek oder für .NET Framework 4.6. Eine .NET Standard 1.4-Bibliothek gilt für .NET Framework 4.6.1, Universelle Windows-Plattform 10, .NET Core und Mono/Xamarin. Weitere Informationen finden Sie unter [.NET Standard mapping table (.NET Standard-Zuordnungstabelle)](/dotnet/standard/net-standard#net-implementation-support) (.NET-Dokumentation). Wenn Sie möchten, können Sie auch eine andere Version der .NET Standard-Bibliothek wählen.

## <a name="prerequisites"></a>Erforderliche Komponenten

1. Visual Studio 2015 Update 3
1. (nur .NET Standard) [.NET Core SDK](https://www.microsoft.com/net/download/)
1. NuGet-CLI. Laden Sie die neuste Version von „nuget.exe“ unter [nuget.org/downloads](https://nuget.org/downloads) herunter, und speichern Sie diese an einem beliebigen Ort. Fügen Sie diesen Speicherort, falls erforderlich, anschließend der Umgebungsvariable „PATH“ hinzu.

    > [!Note]
    > „Nuget.exe“ ist kein Installer, sondern ein CLI-Tool. Vergewissern Sie sich daher, dass Sie die im Browser heruntergeladene Datei speichern, anstatt sie auszuführen.

## <a name="create-the-class-library-project"></a>Erstellen des Klassenbibliotheksprojekts

1. Klicken Sie in Visual Studio auf **Datei > Neu > Projekt**, erweitern Sie den Knoten **Visual C# > Windows**, wählen Sie **Klassenbibliothek (portabel)** aus, ändern Sie den Namen in „AppLogger“, und wählen Sie anschließend **OK**.

    ![Erstellen eines neuen Klassenbibliotheksprojekts](media/NetStandard-NewProject.png)

1. Wählen Sie im angezeigten Dialogfeld **Portable Klassenbibliothek hinzufügen** die Optionen für `.NET Framework 4.6` und `ASP.NET Core 1.0` aus. (Für .NET Framework können Sie die entsprechenden Optionen auswählen.)

1. Für .NET Standard klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf `AppLogger (Portable)`, und wählen Sie dann unter **Eigenschaften** die Registerkarte **Bibliothek**. Wählen Sie dort im Abschnitt **Ziel** die Option **Ziel: .NET-Plattform (Standard)**. Sie werden aufgefordert, diese Aktion zu bestätigen. Anschließend können Sie `.NET Standard 1.4` (oder eine andere verfügbare Version) aus der Dropdownliste auswählen:

    ![Festlegen des Ziels auf .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. Klicken Sie auf die Registerkarte **Erstellen**, ändern Sie die **Konfiguration** in `Release`, und aktivieren Sie das Kontrollkästchen **XML-Dokumentationsdatei**.

1. Fügen Sie der Komponente wie im folgenden Beispiel dargestellt Ihren Code hinzu:

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. Legen Sie die Konfiguration auf „Release“ fest, erstellen Sie das Projekt, und überprüfen Sie, ob die DLL und die XML-Dateien innerhalb des `bin\Release`-Ordners erstellt werden.

## <a name="create-and-update-the-nuspec-file"></a>Erstellen und Aktualisieren der NUSPEC-Datei

1. Öffnen Sie eine Eingabeaufforderung, navigieren Sie zum Ordner, der den `AppLogger.csproj`-Ordner enthält (dieser befindet sich eine Ebene unter der `.sln`-Datei), und führen Sie den `spec`-Befehl für NuGet aus, um eine erste Version der `AppLogger.nuspec`-Datei zu erstellen:

    ```cli
    nuget spec
    ```

1. Öffnen Sie `AppLogger.nuspec` in einem Editor, aktualisieren Sie die Datei gemäß den folgenden Angaben, und ersetzen Sie YOUR_NAME dabei durch einen entsprechenden Wert. Insbesondere der `<id>`-Wert muss auf nuget.org eindeutig sein. Weitere Informationen zu den Namenskonventionen finden Sie unter [Creating a package (Erstellen eines Pakets)](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). Beachten Sie außerdem, dass Sie ebenfalls die Tags für den Autor und die Beschreibung ändern müssen, damit beim Packen kein Fehler ausgelöst wird.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. Fügen Sie Verweisassemblys (die DLL-Datei der Bibliothek und die XML-Datei von IntelliSense) zur `.nuspec`-Datei hinzu:

    Wenn das Ziel .NET Standard ist, ähneln die Einträge den folgenden:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    Wenn das Ziel .NET Framework ist, ähneln die Einträge den folgenden:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. Klicken Sie mit der rechten Maustaste auf die Projektmappe, und klicken Sie dann auf **Projektmappe erstellen**, um sämtliche Dateien für das Paket zu generieren.

### <a name="declaring-dependencies"></a>Deklarieren von Abhängigkeiten

Wenn Abhängigkeiten von anderen NuGet-Paketen bestehen, listen Sie diese im `<dependencies>`-Element des Manifests mit den `<group>`-Elementen auf. Fügen Sie beispielsweise Folgendes hinzu, um eine Abhängigkeit von NewtonSoft.Json 8.0.3 oder höher zu deklarieren:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

Die Syntax des *version*-Attributs gibt an, dass Version 8.0.3 oder höher akzeptiert wird. Weitere Informationen zum Angeben von anderen Versionsbereichen finden Sie unter [Package versioning (Paketversionsverwaltung)](../reference/package-versioning.md).

### <a name="adding-a-readme"></a>Hinzufügen einer Infodatei

Erstellen Sie Ihre `readme.txt`-Datei, platzieren Sie diese im Stammordner des Projekts, und verweisen Sie in der `.nuspec`-Datei auf diese:

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```

Visual Studio zeigt `readme.txt` an, wenn das Paket in dem Projekt installiert wird. Wenn die Datei in .NET Core-Projekten installiert wurde, wird diese nicht angezeigt. Außerdem wird sie nicht für Pakete angezeigt, die als Abhängigkeiten installiert wurden.

## <a name="package-the-component"></a>Packen der Komponente

Mithilfe der vollständigen `.nuspec`-Datei, die auf alle Dateien verweist, die Sie in das Paket einfügen müssen, können Sie jetzt den `pack`-Befehl ausführen:

```cli
nuget pack AppLogger.nuspec
```

Dadurch wird die Datei `AppLogger.YOUR_NAME.1.0.0.nupkg` generiert. Wenn Sie diese Datei in einem Tool wie dem [NuGet-Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) öffnen und alle Knoten erweitern, werden Ihnen (für .NET Standard) folgende Inhalte angezeigt:

![Der NuGet-Paket-Explorer zeigt das AppLogger-Paket an](media/NetStandard-PackageExplorer.png)

> [!Tip]
> Bei einer `.nupkg`-Datei handelt es sich um eine ZIP-Datei mit einer anderen Erweiterung. Sie können auch die Paketinhalte untersuchen, indem Sie `.nupkg` in `.zip` ändern. Denken Sie jedoch daran, die Erweiterung wiederherzustellen, bevor Sie ein Paket auf nuget.org hochladen.

Befolgen Sie die Anweisungen unter [Veröffentlichen eines Pakets](../create-packages/publish-a-package.md), um Ihr Paket für andere Entwickler zur Verfügung zu stellen.

Beachten Sie, dass für `pack` Mono 4.4.2 unter Mac OS X erforderlich ist und dass dieser Befehl auf Linux-Systemen nicht funktioniert. Auf einem Mac müssen Sie ebenfalls Windows-Pfadnamen in der `.nuspec`-Datei in Pfade im Unix-Format konvertieren.

## <a name="related-topics"></a>Verwandte Themen

- [NUSPEC-Referenz](../reference/nuspec.md)
- [Unterstützen mehrerer .NET Framework-Versionen](../create-packages/supporting-multiple-target-frameworks.md)
- [Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Erstellen von lokalisierten Paketen](../create-packages/creating-localized-packages.md)
- [Symbolpakete](../create-packages/symbol-packages.md)
- [Paketversionsverwaltung](../reference/package-versioning.md)
- [Dokumentation zur .NET Standard-Bibliothek](/dotnet/articles/standard/library)
- [Portieren von .NET Framework auf .NET Core](/dotnet/articles/core/porting/index)
