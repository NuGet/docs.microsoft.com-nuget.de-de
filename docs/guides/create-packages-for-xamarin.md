---
title: Erstellen von NuGet-Paketen für Xamarin (für iOS, Android und Windows) mit Visual Studio 2015
description: Eine exemplarische Vorgehensweise zum Erstellen von NuGet-Paketen für Xamarin, die native APIs unter iOS, Android und Windows verwenden.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: tutorial
ms.openlocfilehash: 927991429d8d4ce54aa35be3e450475a38141b11
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488910"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2015"></a>Erstellen von Paketen für Xamarin mit Visual Studio 2015

Ein Paket für Xamarin enthält Code, der native APIs unter iOS, Android und Windows verwendet und von dem Betriebssystem zur Laufzeit abhängig ist. Obwohl dies ein einfacher Vorgang ist, ist es besser, wenn Entwickler das Paket aus einer PCL- oder .NET Standard-Bibliothek über eine allgemeine API-Oberfläche verarbeiten.

In dieser exemplarischen Vorgehensweise erstellen Sie mit Visual Studio 2015 ein plattformübergreifendes NuGet-Paket, das in mobilen Projekten unter iOS, Android und Windows verwendet werden kann.

1. [Erforderliche Komponenten](#prerequisites)
1. [Erstellen der Projektstruktur und abstrakten Codes](#create-the-project-structure-and-abstraction-code)
1. [Schreiben von plattformspezifischem Code](#write-your-platform-specific-code)
1. [Erstellen und Aktualisieren der NUSPEC-Datei](#create-and-update-the-nuspec-file)
1. [Packen der Komponente](#package-the-component)
1. [Verwandte Themen](#related-topics)

## <a name="prerequisites"></a>Erforderliche Komponenten

1. Visual Studio 2015 mit Universelle Windows-Plattform (UWP) und Xamarin. Installieren Sie die Community Edition kostenlos über [visualstudio.com](https://www.visualstudio.com/), oder verwenden Sie die Professional bzw. Enterprise Edition. Wählen Sie eine benutzerdefinierte Installation aus, und überprüfen Sie die passenden Optionen, um UWP- und Xamarin-Tools hinzuzufügen.
1. NuGet-CLI. Laden Sie die neuste Version von „nuget.exe“ unter [nuget.org/downloads](https://nuget.org/downloads) herunter, und speichern Sie diese an einem beliebigen Ort. Fügen Sie diesen Speicherort, falls erforderlich, anschließend der Umgebungsvariable „PATH“ hinzu.

> [!Note]
> „Nuget.exe“ ist kein Installer, sondern ein CLI-Tool. Vergewissern Sie sich daher, dass Sie die im Browser heruntergeladene Datei speichern, anstatt sie auszuführen.

## <a name="create-the-project-structure-and-abstraction-code"></a>Erstellen der Projektstruktur und abstrakten Codes

1. Laden Sie das [Plug-In für Erweiterungen von Xamarin-Vorlagen](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) für Visual Studio herunter, und führen Sie es aus. Diese Vorlagen vereinfachen das Erstellen der für diese exemplarische Vorgehensweise notwendigen Projektstruktur.
1. Suchen Sie in Visual Studio über **Datei > Neu > Projekt** nach `Plugin`, wählen Sie die Vorlage **Plug-In für Xamarin** aus, ändern Sie den Namen in „LoggingLibrary“, und klicken Sie auf „OK“.

    ![Neues, leeres App-Projekt (Xamarin.Forms Portable) in Visual Studio](media/CrossPlatform-NewProject.png)

Die resultierende Projektmappe enthält neben verschiedenen plattformspezifischen Projekten auch zwei PCL-Projekte:

- Der PCL mit dem Namen `Plugin.LoggingLibrary.Abstractions (Portable)` definiert die öffentliche Schnittstelle (API-Oberfläche) der Komponente. In diesem Fall handelt es sich dabei um die `ILoggingLibrary`-Schnittstelle in der Datei „ILoggingLibrary.cs“. Hier definieren Sie die Schnittstelle zu Ihrer Bibliothek.
- `Plugin.LoggingLibrary (Portable)`, der andere PCL, enthält Code in der Datei „CrossLoggingLibrary.cs“, der eine plattformspezifische Implementierung der abstrakten Schnittstelle zur Laufzeit findet. In der Regel müssen an dieser Datei keine Änderungen vorgenommen werden.
- Die plattformspezifischen Projekte, z.B. `Plugin.LoggingLibrary.Android`, enthalten alle in den jeweiligen „LoggingLibraryImplementation.cs“-Dateien eine native Implementierung ihrer Schnittstelle. Hier erstellen Sie den Code Ihrer Bibliothek.

Standardmäßig enthält die Datei „ILoggingLibrary.cs“ des Abstraktionsprojekts zwar eine Schnittstellendefinition, aber keine Methoden. Fügen Sie für diese exemplarische Vorgehensweise wie folgt eine `Log`-Methode hinzu:

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

## <a name="write-your-platform-specific-code"></a>Schreiben von plattformspezifischem Code

Führen Sie die folgenden Schritte aus, um eine plattformspezifische Implementierung der `ILoggingLibrary`-Schnittstelle und deren Methoden zu implementieren:

1. Öffnen Sie die `LoggingLibraryImplementation.cs`-Dateien der Plattformprojekte, und fügen Sie den benötigten Code hinzu. Verwenden Sie z.B. das `Plugin.LoggingLibrary.Android`-Projekt:

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

1. Wiederholen Sie diese Implementierung in den Projekten für jede Plattform, die Sie unterstützen möchten.
1. Klicken Sie mit der rechten Maustaste auf das iOS-Projekt, klicken Sie erst auf **Eigenschaften** und dann auf die Registerkarte **Build**, und entfernen Sie „\iPhone“ aus dem **Ausgabepfad** und den **XML-Dokumentationsdatei**-Einstellungen. Dieser Schritt dient zur Vereinfachung späterer Schritte in dieser exemplarischen Vorgehensweise. Speichern Sie die Datei anschließend.
1. Klicken Sie mit der rechten Maustaste auf die Projektmappe, wählen Sie **Konfigurations-Manager...** aus, und überprüfen Sie die **Build**-Felder für die PCLs und alle von Ihnen unterstützen Plattformen.
1. Klicken Sie mit der rechten Maustaste auf die Projektmappe, und wählen Sie **Projektmappe erstellen** aus, um Ihre Arbeit zu überprüfen und die Elemente zu erstellen, die Sie als Nächstes packen möchten. Wenn Ihnen Fehler aufgrund von fehlenden Verweisen angezeigt werden, klicken Sie mit der rechten Maustaste auf die Projektmappe, wählen Sie **NuGet-Pakete wiederherstellen** aus, um die Abhängigkeiten zu installieren, und erstellen Sie die Projektmappe erneut.

> [!Note]
> Sie benötigen für die Erstellung für iOS einen Mac im Netzwerk, für den eine Verbindung mit Visual Studio besteht. Dies wird unter [Introduction to Xamarin.iOS for Visual Studio (Einführung in Xamarin.iOS für Visual Studio)](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/) beschrieben. Wenn Sie keinen Mac zur Hand haben, entfernen Sie das iOS-Projekt aus dem Konfigurations-Manager (s. Schritt 3).

## <a name="create-and-update-the-nuspec-file"></a>Erstellen und Aktualisieren der NUSPEC-Datei

1. Öffnen Sie eine Eingabeaufforderung, navigieren Sie zum `LoggingLibrary`-Ordner, der sich eine Ebene unter der `.sln`-Datei befindet, und führen Sie den `spec`-Befehl für NuGet aus, um eine erste Version der `Package.nuspec`-Datei zu erstellen:

    ```cli
    nuget spec
    ```

1. Benennen Sie diese Datei in `LoggingLibrary.nuspec` um, und öffnen Sie sie im Editor.
1. Aktualisieren Sie die Datei, damit sie wie folgt aussieht, indem Sie „IHREN_NAMEN“ durch einen passenden Wert ersetzen. Insbesondere der `<id>`-Wert muss auf nuget.org eindeutig sein. Weitere Informationen zu den Namenskonventionen finden Sie unter [Creating a package (Erstellen eines Pakets)](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number). Beachten Sie außerdem, dass Sie ebenfalls die Tags für den Autor und die Beschreibung ändern müssen, damit beim Packen kein Fehler ausgelöst wird.

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
> Sie können an Ihre Paketversion `-alpha`, `-beta` oder `-rc` anhängen, um die Pakete als Vorabversionen zu markieren. Weitere Informationen zu Vorabversionen finden Sie unter [Vorabversionen](../create-packages/prerelease-packages.md).

### <a name="add-reference-assemblies"></a>Hinzufügen von Verweisassemblys

Fügen Sie, abhängig davon, welche Plattformen Sie unterstützen, dem `<files>`-Element von `LoggingLibrary.nuspec` Folgendes hinzu, um plattformspezifische Verweisassemblys hinzuzufügen:

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
> Klicken Sie mit der rechten Maustaste auf ein beliebiges Projekt, wählen Sie die Registerkarte **Bibliothek** aus, und ändern Sie die Assemblynamen, um die Namen der DLL- und XML-Dateien zu ändern.

### <a name="add-dependencies"></a>Hinzufügen von Abhängigkeiten

Wenn Sie über bestimmte Abhängigkeiten für native Implementierungen verfügen, verwenden Sie das `<dependencies>`-Element zusammen mit `<group>`-Elementen, um diese anzugeben. Z.B.:

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

Im folgenden Beispiel wird „iTextSharp“ als Abhängigkeit für ein UAP-Ziel festgelegt:

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>Endgültige NUSPEC-Datei

Die endgültige `.nuspec`-Datei sollte nun folgendermaßen aussehen, wobei Sie erneut YOUR_NAME durch einen passenden Wert ersetzen sollten:

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

## <a name="package-the-component"></a>Packen der Komponente

Mithilfe der vollständigen `.nuspec`-Datei, die auf alle Dateien verweist, die Sie in das Paket einfügen müssen, können Sie jetzt den `pack`-Befehl ausführen:

```cli
nuget pack LoggingLibrary.nuspec
```

Dadurch wird `LoggingLibrary.YOUR_NAME.1.0.0.nupkg` generiert. Wenn Sie diese Datei in einem Tool wie dem [NuGet-Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) öffnen und alle Knoten erweitern, werden Ihnen folgende Inhalte angezeigt:

![NuGet-Paket-Explorer zeigt das LoggingLibrary-Paket an](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> Bei einer `.nupkg`-Datei handelt es sich um eine ZIP-Datei mit einer anderen Erweiterung. Sie können auch die Paketinhalte untersuchen, indem Sie `.nupkg` in `.zip` ändern. Denken Sie jedoch daran, die Erweiterung wiederherzustellen, bevor Sie ein Paket auf nuget.org hochladen.

Befolgen Sie die Anweisungen unter [Veröffentlichen eines Pakets](../nuget-org/publish-a-package.md), um Ihr Paket für andere Entwickler zur Verfügung zu stellen.

## <a name="related-topics"></a>Verwandte Themen

- [NUSPEC-Referenz](../reference/nuspec.md)
- [Symbolpakete](../create-packages/symbol-packages.md)
- [Paketversionsverwaltung](../concepts/package-versioning.md)
- [Unterstützung mehrerer .NET Framework-Versionen](../create-packages/supporting-multiple-target-frameworks.md)
- [Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Erstellen von lokalisierten Paketen](../create-packages/creating-localized-packages.md)