---
title: Installieren von NuGet-Clienttools | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "Anleitung zum Installieren von Clienttools, der Befehlszeilenschnittstelle (Command-Line Interface, CLI) und des Paket-Managers für Visual Studio."
keywords: "CLI von nuget.exe, NuGet-Clienttools, NuGet-Paket-Manager, NuGet-Paket-Manager-Konsole, NuGet für Visual Studio, NuGet-Beta-Kanal"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1abb30458c9ebfb0ffb28be254efd9709a9627f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="installing-nuget-client-tools"></a>Installieren von NuGet-Clienttools

> [!Tip]
> **Sie möchten ein Paket installieren? Unter [Schnellstart - Verwenden eines Pakets](../Quickstart/Use-a-Package.md) finden Sie weitere Informationen.**

Es gibt zwei primäre Tools, die Sie beim Erstellen, Veröffentlichen und Verwenden von NuGet-Paketen unterstützen:

1. Die [**NuGet-CLI**](#nuget-cli) ist das Befehlszeilenprogramm für Windows, über die alle Funktionen von NuGet bereitgestellt werden; sie kann auch unter Mac OSX und Linux mit Mono oder über die .NET Core-CLI (`dotnet`) ausgeführt werden.
1. Bei dem [**NuGet-Paket-Manager in Visual Studio**](#nuget-package-manager-in-visual-studio) (nur Windows) handelt es sich um ein GUI-Tool für die Verwaltung von Paketen. Es enthält eine PowerShell-Konsole, über die Sie bestimmte NuGet-Befehle direkt in Visual Studio verwenden können. Die Benutzeroberfläche des Paket-Managers und die Paket-Manager-Konsole sind beide in Visual Studio 2012 und höher (unter Windows) enthalten und können manuell für frühere Versionen installiert werden.

    Bei Visual Studio für Mac sind NuGet-Funktionen direkt integriert. Eine exemplarische Vorgehensweise finde Sie unter [Einschließen eines NuGet-Pakets in Ihr Projekt](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).

    Visual Studio Code verfügt derzeit über keine integrierte NuGet-Unterstützung. Verwenden Sie die NuGet-CLI oder die [Dotnet-CLI](../Tools/dotnet-Commands.md).

Die NuGet-CLI und der Paket-Manager unterstützen folgende Vorgänge:

- Suchen von Paketen
- Installieren von Paketen
- Aktualisieren von Paketen
- Deinstallieren von Paketen
- Wiederherstellen von Paketen (UI nur im Paket-Manager)
- Verwalten von NuGet-Quellen

Die folgenden Funktionen werden nur in der NuGet-CLI unterstützt:

- Verwalten von Paketen (nuget.org oder privater Feed)
- Erstellen von Paketen 
- Veröffentlichen von Paketen
- Verwalten von „Nuget.Config“
- Verwalten des NuGet-Cache
- Replizieren eines Pakets

> [!Note]
> Ein weiteres gutes Tool ist der [NuGet-Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), ein eigenständiges Open Source-Tool, mit dem NuGet-Pakete visuell angezeigt, erstellt und bearbeitet werden können. Dieses Tool ist beispielsweise sehr hilfreich, wenn experimentelle Änderungen an einer Paketstruktur vorgenommen werden, ohne das Paket jedes Mal neu erstellen zu müssen.
> Die für die Entwicklung von .NET Core-Apps verwendete plattformübergreifende Toolkette der [.NET Core-CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) unterstützt mehrere NuGet-Befehle, wie z.B. „delete“, „locals“, „push“, „pack“ und „restore“. 

## <a name="nuget-cli"></a>NuGet-CLI

Die NuGet-Befehlszeilenschnittstelle ermöglicht den Zugriff auf alle NuGet-Funktionen und kann unter Windows, Mac OSX und Linux ausgeführt werden, wie in den folgenden Abschnitten beschrieben.

### <a name="windows"></a>Windows

**Direkter Download:**

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> In NuGet 1.4 oder höher können Sie `nuget update -self` für das Update Ihrer vorhandenen nuget.exe auf die neueste Version verwenden.

**Weitere Methoden:**

- **Chocolatey**: Installieren Sie das Chocolatey-Paket [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) mithilfe des [Chocolatey](http://chocolatey.org)-Clients. 

    ```ps
    choco install nuget.commandline
    ```

- **Visual Studio**: Installieren Sie das Paket [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) über die Paket-Manager-Konsole in Visual Studio.

    > [!Note]
    > **Für Benutzer von NuGet 2.x**: Aufgrund von wichtigen Änderungen in NuGet 3.2 wird auf [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) auf das neueste stabile Release von NuGet-2.x verwiesen, damit eine potenzielle Unterbrechung von Continuous Integration-Systemen verhindert werden kann.

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a>Mac OSX und Linux

Unter Mac OSX und Linux gibt es zwei Möglichkeiten für die Ausführung der NuGet-CLI:

- Installieren Sie das [.NET Core SDK](https://www.microsoft.com/net/download/core), darunter die NuGet-Hauptfunktionen. Downloads werden auch unter [github.com/dotnet/cli](https://github.com/dotnet/cli) aufgeführt. Wenn Sie umfassendere Funktionen benötigen, verwenden Sie die zweite, nachfolgende Option für die Verwendung von `nuget.exe` mit Mono.

- Installieren Sie [Mono](http://www.mono-project.com/docs/getting-started/install/), und verwenden Sie anschließend die ausführbare Befehlszeilendatei von `nuget.exe` für Windows (Version 3.2 und höher) von [nuget.org/downloads](https://nuget.org/downloads). Die Ausführung von NuGet in Mono unterliegt folgenden Einschränkungen:

    - Auf ihre Funktionsfähigkeit getestete Befehle:
        - config
        - Löschen
        - help
        - install
        - Liste
        - push
        - setApiKey
        - sources
        - spec

    - Teilweise funktionierende Befehle:
        - pack: Funktioniert bei `.nuspec`-Dateien, jedoch nicht bei Projektdateien.
        - restore: Funktioniert bei `packages.config`- und `project.json`-Dateien, jedoch nicht bei Projektmappendateien (`.sln`).

    - Nicht funktionierende Befehle:
        - aktualisieren

### <a name="related-topics"></a>Verwandte Themen

- [Verweis auf NuGet-CLI](../tools/nuget-exe-cli-reference.md)
- [Erstellen eines Pakets](../create-packages/creating-a-package.md)
- [Veröffentlichen eines Pakets](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a>NuGet-Paket-Manager in Visual Studio

Der NuGet-Paket-Manager ist in jeder Edition von Visual Studio unter Windows ab Version 2012 enthalten. Er umfasst die Benutzeroberfläche des Paket-Managers ([Referenz](../tools/package-manager-ui.md)) sowie die Paket-Manager-Konsole, über die Sie auf Tools zugreifen können, die im Lieferumfang bestimmter Pakete enthalten sind ([Referenz](../tools/package-manager-console.md)).

Der Installer von Visual Studio 2017 umfasst den NuGet-Paket-Manager mit allen Workloads, die .NET verwenden. Führen Sie den Installer von Visual Studio 2017 aus, und überprüfen Sie die Option unter **Einzelne Komponenten > Codetools > NuGet-Paket-Manager**, um eine separate Installation auszuführen oder um zu überprüfen, ob der Paket-Manager installiert wurde.

> [!Note]
> Für die Konsole ist [PowerShell 2.0](http://support.microsoft.com/kb/968929) erforderlich, das unter Windows 7 oder höher und Windows Server 2008 R2 oder höher bereits installiert ist.
>
> Befehle der Paket-Manager-Konsole funktionieren auch nur in Visual Studio unter Windows. Verwenden Sie die NuGet-CLI außerhalb dieser Umgebung, einschließlich mit Visual Studio für Mac und Visual Studio Code.

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a>Installation des Paket-Managers für Visual Studio 2010 oder ältere Versionen

*Diese Schritte sind für Visual Studio 2012 und höher nicht erforderlich, da der Paket-Manager dort bereits enthalten ist.*

1. Klicken Sie in Visual Studio 2010 und älteren Versionen auf **Tools > Erweiterungen und Updates**.
1. Navigieren Sie zu **Online**, suchen Sie nach „NuGet-Paket-Manager für Visual Studio“, und klicken Sie auf **Herunterladen**.
1. Klicken Sie im Dialogfeld „Installer“ auf **Installieren**.
1. Starten Sie Visual Studio nach Abschluss der Installation erneut.

> [!Tip]
> Wenn Sie das Dialogfeld **Erweiterungen und Updates** in Visual Studio nicht verwenden können (da es z.B. von einem Proxy blockiert wird), können Sie Erweiterungen für Visual Studio 2013 und 2015 direkt unter [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) herunterladen.

### <a name="updating-the-package-manager"></a>Aktualisieren des Paket-Managers

In Visual Studio 2015 Update 2 und höher wird der Paket-Manager automatisch auf das neueste stabile Release aktualisiert.

Wählen Sie bei Visual Studio 2015 Update 1 und früher den Befehl **Tools > Erweiterungen und Updates** aus, und klicken Sie auf die Registerkarte **Updates**, um zu überprüfen, ob eine neue Version des Paket-Managers verfügbar ist.  

### <a name="nuget-previews"></a>NuGet-Vorschauen

Wenn Sie eine Vorschau der geplanten NuGet-Funktionen sehen möchten, installieren Sie die [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), die parallel mit stabilen Releases von Visual Studio arbeitet.

Beachten Sie, dass der vorherige NuGet-Beta-Kanal (`https://dotnet.myget.org/F/nuget-beta/vsix/`) für Visual Studio 2015 nicht mehr verwendet wird.

Wenn Sie Probleme mit einem Release von NuGet melden oder Ideen teilen möchten, können Sie sich im [GitHub-Repository von NuGet](https://github.com/Nuget/Home) beteiligen.

### <a name="related-topics"></a>Verwandte Themen

- [Benutzeroberflächenverweis des Paket-Managers](../tools/package-manager-ui.md)
- [Verweis der Paket-Manager-Konsole](../tools/package-manager-console.md)
- [PowerShell-Verweis des Paket-Managers](../tools/powershell-reference.md)