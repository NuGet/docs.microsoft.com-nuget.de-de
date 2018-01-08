---
title: Erstellen von .NET Standard 2.0-NuGet-Paketen mit Visual Studio 2017 | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: Eine exemplarische End-to-End-Vorgehensweise zum Erstellen von .NET Standard 2.0-NuGet-Paketen mithilfe von NuGet 4.x und Visual Studio 2017.
keywords: Erstellen eines Pakets, .NET Standard-Pakete, .NET Core
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82e413119b12503336becd6019e4fa3e4ac0b1f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a>Erstellen von .NET Standard 2.0-Paketen mit Visual Studio 2017

*Gilt für NuGet 4.x und höher sowie MSBuild 15.3 und höher mit Visual Studio 2017 Update 3. Für frühere Versionen von Visual Studio 2017 gelten dieses Anweisungen für .NET Standard 1.4 bis 1.6 durch Ändern der Eigenschaft \<TargetFramework\>. Unter [Create .NET Standard Packages with Visual Studio 2015 (Erstellen von .NET Standard-Paketen mit Visual Studio 2015)](../guides/create-net-standard-packages-vs2015.md) erhalten Sie weitere Informationen zur Arbeit mit NuGet 3.x und höher.*

Die [.NET-Standardbibliothek](https://docs.microsoft.com/dotnet/articles/standard/library) ist eine formale Spezifikation von .NET-APIs, die in allen .NET-Runtimes verfügbar sein soll, um so eine umfassendere Einheitlichkeit im .NET-Ökosystem herzustellen. Die .NET-Standardbibliothek definiert einen einheitlichen Satz von BCL-APIs (Base Class Library), die unabhängig von der Workload für alle .NET-Plattformen implementiert werden. Sie ermöglicht Entwicklern, portable Klassenbibliotheken (PCLs) zu erzeugen, die für alle .NET-Runtimes verwendet werden können, und reduziert plattformspezifische Anweisungen für die bedingte Kompilierung in freigegebenem Code, wenn diese nicht sogar ausgeschlossen werden.

Diese Anleitung begleitet Sie durch das Erstellen eines NuGet-Pakets für die .NET-Standardbibliothek 2.0 mit Visual Studio 2017 Update 3 und NuGet 4.0.

1. [Voraussetzungen](#pre-requisites)
1. [Erstellen des Klassenbibliotheksprojekts](#create-the-netstandard-class-library-project)
1. [Bearbeiten von Metadaten in der CSPROJ-Datei](#edit-metadata-in-the-csproj-file)
1. [Packen der Komponente](#package-the-component)
1. [Verwandte Themen](#related-topics)

## <a name="pre-requisites"></a>Voraussetzungen

Für diese exemplarische Vorgehensweise ist Visual Studio 2017 Update 3 mit der Workload für die **plattformübergreifende .NET Core-Entwicklung** erforderlich. Sie können die Community Edition kostenlos über [visualstudio.com](https://www.visualstudio.com/) installieren oder die Professional bzw. Enterprise Edition verwenden.

Die erforderliche Workload erscheint wie im Folgenden dargestellt im Visual Studio-Installer:

![Workload für die plattformübergreifende .NET Core-Entwicklung im Visual Studio-Installer](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a>Erstellen des .NET Standard-Klassenbibliotheksprojekts

1. Klicken Sie in Visual Studio auf **Datei > Neu > Projekt**, erweitern Sie den Knoten **Visual C# > .NET Standard**, wählen Sie **Klassenbibliothek (.NET Standard)** aus, ändern Sie den Namen in „AppLogger“, und klicken Sie anschließend auf „OK“.

    ![Erstellen eines neuen Klassenbibliotheksprojekts](media/NuGet4-02-NewProject.png)

1. Ändern Sie die Buildkonfiguration in **Release**.
1. Klicken Sie mit der rechten Maustaste auf das `AppLogger`-Projekt im Projektmappen-Explorer, wählen Sie **Eigenschaften** aus, und klicken Sie auf die Registerkarte **Build**. Anschließend aktivieren Sie das Feld für die **XML-Dokumentationsdatei** und legen den Dateinamen auf `AppLogger.xml` fest. Speichern Sie das Projekt.

1. Fügen Sie Ihrer Komponente den Code hinzu, wie unten dargestellt (dadurch werden nur Meldungen an die Konsole ausgegeben):

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

1. Erstellen Sie das Projekt (mit der Releasekonfiguration), und überprüfen Sie, ob die DLL und die XML-Dateien innerhalb des `bin\Release\netstandard2.0`-Ordners erstellt werden.

## <a name="edit-metadata-in-the-csproj-file"></a>Bearbeiten von Metadaten in der CSPROJ-Datei

Mit NuGet 4.0- und .NET Core-Projekten sind die Paketmetadaten direkt in der `.csproj`-Datei enthalten und nicht in externen Dateien wie `.nuspec`. Sie finden eine vollständige Beschreibung dieser Metadaten unter [NuGet pack and restore as MSBuild targets (Packen und Wiederherstellen von NuGet als MSBuild-Ziele)](../schema/msbuild-targets.md#pack-target).

1. Klicken Sie mit der rechten Maustaste in das Projekt im Projektmappen-Explorer, wählen Sie **Edit AppLogger.csproj** aus, und bearbeiten Sie anschließend die erste Eigenschaftengruppe, sodass diese Paketinformationen wie die Folgenden enthalten soll:

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. Speichern Sie das Projekt, klicken Sie dann mit der rechten Maustaste auf die Projektmappe, und wählen Sie **Projektmappe erstellen** aus, um erneut alle Dateien für das Paket zu generieren – dieses Mal mit den richtigen Metadaten.


## <a name="package-the-component"></a>Packen der Komponente

NuGet 4.0 unterstützt ein Packziel mit MSBuild-Version 15.1 und höher (einschließlich MSBuild 15.3 als Teil von Visual Studio 2017 Update 3), wenn das Projekt die erforderlichen Paketmetadaten enthält, die im vorherigen Abschnitt hinzugefügt worden sind. Geben Sie einfach das Packziel auf der Befehlszeile im selben Ordner wie die `.csproj`-Datei an, um MSBuild auf diese Weise aufzurufen:

    msbuild /t:pack /p:Configuration=Release

Zusätzliche Informationen zu `msbuild /t:pack`, z.B. das Einschließen von Inhaltsdateien, Symbolen und Quellcode, finden Sie auf der Seite [NuGet pack and restore as MSBuild targets (Packen und Wiederherstellen von NuGet als MSBuild-Ziele)](../schema/msbuild-targets.md#pack-target).

Auf jeden Fall generiert der obenstehende Code standardmäßig `AppLogger.YOUR_NAME.1.0.0.nupkg` im Ordner `bin\Release` beim Erstellen dieser Konfiguration. Wenn Sie den `/p`-Schalter nicht verwenden, lautet die Standardkonfiguration `Debug`. 

Wenn Sie diese Datei in einem Tool wie dem [NuGet-Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) öffnen und alle Knoten erweitern, wird Ihnen folgender Inhalt angezeigt:

![Der NuGet-Paket-Explorer zeigt das AppLogger-Paket an](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> Bei einer `.nupkg`-Datei handelt es sich um eine ZIP-Datei mit einer anderen Erweiterung. Sie können auch die Paketinhalte untersuchen, indem Sie `.nupkg` in `.zip` ändern. Denken Sie jedoch daran, die Erweiterung wiederherzustellen, bevor Sie ein Paket auf nuget.org hochladen.

Befolgen Sie die Anweisungen unter [Veröffentlichen eines Pakets](../create-packages/publish-a-package.md), um Ihr Paket für andere Entwickler zur Verfügung zu stellen.

## <a name="related-topics"></a>Verwandte Themen

- Unter [Packen von Verweisen in Projektdateien](../consume-packages/package-references-in-project-files.md) werden alle Details zum Beschreiben Ihres Pakets direkt in der Projektdatei beschrieben.
- Unter [NuGet pack and restore as MSBuild targets (Packen und Wiederherstellen von NuGet als MSBuild-Ziele)](../schema/msbuild-targets.md) werden alle Optionen zur Verwendung von `msbuild /t:pack` zum Erstellen des Pakets beschrieben.
- [Dokumentation zur .NET Standard-Bibliothek](https://docs.microsoft.com/dotnet/articles/standard/library)
- [Portieren von .NET Framework auf .NET Core](https://docs.microsoft.com/dotnet/articles/core/porting/index)
