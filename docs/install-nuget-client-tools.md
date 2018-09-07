---
title: Installieren von NuGet-Clienttools
description: Anleitung zum Installieren von Clienttools, der dotnet- und nuget-Befehlszeilenschnittstellen (Command-Line Interface, CLI) und des Paket-Managers für Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 04/09/2018
ms.topic: quickstart
ms.openlocfilehash: b3be75a5af85bd3048c8b0eb71d90238b9349e09
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549721"
---
# <a name="installing-nuget-client-tools"></a>Installieren von NuGet-Clienttools

> **Sie möchten ein Paket installieren? Weitere Informationen unter [Möglichkeiten zum Installieren von NuGet-Paketen](consume-packages/ways-to-install-a-package.md).**

Damit Sie als Paketverbraucher oder -ersteller mit NuGet arbeiten können, können Sie [Befehlszeilenschnittstellentools (CLI)](#cli-tools) und [NuGet-Features in Visual Studio](#visual-studio) verwenden. Dieser Artikel beschreibt kurz die Funktionen der verschiedenen Tools, wie sie installiert werden und ihre [Verfügbarkeit von Features](#feature-availability) im Vergleich. Informationen zum Einstieg in das Nutzen von Paketen mithilfe von NuGet finden Sie unter [Install and use a package (.NET CLI) [Installieren und Verwenden eines Pakets (.NET CLI)]](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) und [Install and use a package (Visual Studio) [Installieren und Verwenden eines Pakets (Visual Studio)]](quickstart/install-and-use-a-package-in-visual-studio.md). Informationen zum Einstieg in das Erstellen von NuGet-Paketen finden Sie unter [Create and publish a NET Standard package (dotnet CLI) [Erstellen und Veröffentlichen eines NET Standard-Pakets (.NET CLI)]](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) und [Create and publish a NET Standard package (Visual Studio) [Erstellen und Veröffentlichen eines NET Standard-Pakets (Visual Studio)]](quickstart/create-and-publish-a-package-using-visual-studio.md).

| Tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Beschreibung  | Herunterladen&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | Im .NET Core SDK enthalten und stellt NuGet-Kernfeatures auf allen Plattformen bereit. | [.NET Core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Stellt alle Funktionen von NuGet unter Windows und die meisten Features für Mac und Linux unter Mono bereit. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | Stellt unter Windows Funktionen von NuGet über die Benutzeroberfläche und die Konsole des Paket-Managers bereit, einschließlich .NET-bezogener Workloads. Stellt unter Mac bestimmte Features über die Benutzeroberfläche bereit. In Visual Studio werden NuGet-Features über Erweiterungen bereitgestellt. | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

Die [MSBuild-CLI](reference/msbuild-targets.md) bietet auch die Möglichkeit, Pakete wiederherzustellen und zu erstellen, was vor allem auf Buildservern nützlich ist. MSBuild ist kein Allzwecktool für die Arbeit mit NuGet.

## <a name="cli-tools"></a>CLI-Tools

`dotnet.exe` und `nuget.exe` sind die zwei NuGet-CLI-Tools. Einen Vergleich finden Sie unter [Verfügbarkeit von Features](#feature-availability).

### <a name="dotnetexe-cli"></a>dotnet.exe-CLI

Die .NET Core 2.0-CLI `dotnet.exe` funktioniert auf allen Plattformen (Windows, Mac und Linux) und stellt NuGet-Kernfeatures bereit, wie z.B. das Installieren, Wiederherstellen und Veröffentlichen von Paketen. Durch `dotnet` wird die direkte Integration von .NET Core-Projektdateien (z.B. `.csproj`) ermöglicht, was in den meisten Szenarios hilfreich ist. `dotnet` wird auch für jede Plattform direkt erstellt und erfordert keine Installation von Mono.

Installation:

- Installieren Sie auf Entwicklercomputern das [.NET Core SDK](https://aka.ms/dotnetcoregs).
- Befolgen Sie für Buildserver die Anweisungen unter [Verwenden der .NET Core SDK und Tools in Continuous Integration](/dotnet/core/tools/using-ci-with-cli).

Weitere Informationen finden Sie unter [Tools für die .NET Core-Befehlszeilenschnittstelle](/dotnet/core/tools/index?tabs=netcore2x#tabpanel_fXL5YCOYDa_netcore2x).

### <a name="nugetexe-cli"></a>nuget.exe-CLI

Die NuGet-CLI `nuget.exe` ist das Befehlszeilenprogramm für Windows, über das alle Funktionen von NuGet bereitgestellt werden. Mit [Mono](http://www.mono-project.com/docs/getting-started/install/) kann es auch unter Mac OSX und Linux ausgeführt werden (mit Einschränkungen). Im Gegensatz zu `dotnet`, wirkt sich die `nuget.exe`-CLI nicht auf die Projektdateien aus, und beim Installieren von Paketen wird `packages.config` nicht aktualisiert.

Installation:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Verwenden Sie unter Windows `nuget update -self`, um eine vorhandene „nuget.exe“-Datei auf die neueste Version zu aktualisieren.

> [!Note]
> Die neueste empfohlene NuGet-CLI ist immer unter `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe` verfügbar. Für die Kompatibilität mit älteren Continuous Integration-Systemen wird aktuell über die vorherige URL, `https://nuget.org/nuget.exe`, das [veraltete 2.8.6 CLI-Tool](https://github.com/NuGet/NuGetGallery/issues/5381) zur Verfügung gestellt.

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code: Funktionen von NuGet sind über Marketplace-Erweiterungen oder die Verwendung der CLI-Tools `dotnet.exe` oder `nuget.exe` verfügbar.

- Visual Studio für Mac: Bestimmte Funktionen von NuGet sind direkt integriert. Eine exemplarische Vorgehensweise finde Sie unter [Einschließen eines NuGet-Pakets in Ihr Projekt](/visualstudio/mac/nuget-walkthrough). Verwenden Sie die CLI-Tools `dotnet.exe` oder `nuget.exe` für weitere Funktionen.

- Visual Studio unter Windows: Der **NuGet-Paket-Manager** ist in Visual Studio 2012 und höher enthalten. Der Paket-Manager stellt die [Paket-Manager-Benutzeroberfläche](tools/package-manager-ui.md) und die [Paket-Manager-Konsole](tools/package-manager-console.md) bereit, durch die Sie die meisten NuGet-Vorgänge ausführen können.
  - Der Installer von Visual Studio 2017 umfasst den NuGet-Paket-Manager mit allen Workloads, die .NET verwenden. Führen Sie den Installer von Visual Studio 2017 aus, und überprüfen Sie die Option unter **Einzelne Komponenten > Codetools > NuGet-Paket-Manager**, um eine separate Installation auszuführen oder um zu überprüfen, ob der Paket-Manager installiert wurde.
  - Die Benutzeroberfläche und die Konsole des Paket-Managers sind nur für Visual Studio unter Windows verfügbar. Sie sind aktuell nicht in Visual Studio für Mac verfügbar.
  - Visual Studio enthält die `nuget.exe`-CLI nicht automatisch, sie muss, wie oben beschrieben, separat installiert werden.
  - Die Konsolenbefehle des Paket-Managers funktionieren nur in Visual Studio unter Windows und nicht in anderen PowerShell-Umgebungen.
  - Installieren Sie die Erweiterung „NuGet-Paket-Manager in Visual Studio“, wenn Sie Visual Studio 2010 oder früher verwenden.
  - NuGet-Erweiterungen für Visual Studio 2013 und 2015 können auch über [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) heruntergeladen werden.
  - Wenn Sie eine Vorschau der geplanten NuGet-Funktionen sehen möchten, installieren Sie die [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), die parallel mit stabilen Releases von Visual Studio arbeitet. Wenn Sie Probleme melden oder Ideen für Vorschauversionen teilen möchten, können Sie sich am [GitHub-Repository von NuGet](https://github.com/Nuget/Home/issues) beteiligen.

## <a name="feature-availability"></a>Verfügbarkeit von Features

| Feature | dotnet-CLI | NuGet-CLI (Windows) | NuGet-CLI (Mono) | Visual Studio (Windows) | Visual Studio für Mac |
| --- | --- | --- | --- | --- | --- |
| Suchen von Paketen |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Pakete installieren oder deinstallieren | &#10004;(1) | &#10004;(2) | &#10004; | &#10004; | &#10004; |
| Aktualisieren von Paketen | &#10004; | &#10004; | | &#10004; | &#10004; |
| Pakete wiederherstellen | &#10004; | &#10004; | &#10004;(3) | &#10004; | &#10004; |
| Paketfeeds verwalten (Quellen) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Pakete auf einem Feed verwalten | &#10004;(1) | &#10004; | &#10004; | | |
| API-Schlüsseln für Feeds festlegen | | &#10004; | &#10004; | | |
| Paket erstellen(4) | &#10004; | &#10004; | &#10004;(5) | &#10004; | |
| Veröffentlichen von Paketen | &#10004;(1) | &#10004; | &#10004; | &#10004; |  |
| Pakete replizieren |  | &#10004; | &#10004; | | |
| Verwalten des Ordners *global-packages* und des Cacheordners | &#10004; | &#10004; | &#10004; | | |
| NuGet-Konfiguration verwalten | | &#10004; | &#10004; | | |

(1) Pakete nur auf nuget.org

(2) Hat keinen Einfluss auf Projektdateien; verwenden Sie stattdessen `dotnet.exe`.

(3) Funktioniert nur mit der `packages.config`-Datei und nicht mit Projektmappendateien (`.sln`).

(4) Verschiedene fortgeschrittene Paketfeatures sind nur über die CLI verfügbar, sie werden nicht in den Tools der Visual Studio-Benutzeroberfläche dargestellt.

(5) Funktioniert bei `.nuspec`-Dateien, jedoch nicht bei Projektdateien.

### <a name="related-topics"></a>Verwandte Themen

- [dotnet-Befehle](tools/dotnet-commands.md)
- [Verweis auf NuGet-CLI](tools/nuget-exe-cli-reference.md)
- [Benutzeroberflächenverweis des Paket-Managers](tools/package-manager-ui.md)
- [Verweis der Paket-Manager-Konsole](tools/package-manager-console.md)
- [PowerShell-Verweis des Paket-Managers](tools/powershell-reference.md)
- [Erstellen eines Pakets](create-packages/creating-a-package.md)
- [Veröffentlichen eines Pakets](create-packages/publish-a-package.md)

Entwickler, die unter Windows arbeiten, können auch den [NuGet-Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) durchsuchen, ein eigenständiges Open-Source-Tool, mit dem NuGet-Pakete visuell angezeigt, erstellt und bearbeitet werden können. Dieses Tool ist beispielsweise sehr hilfreich, wenn experimentelle Änderungen an einer Paketstruktur vorgenommen werden, ohne das Paket jedes Mal neu erstellen zu müssen.
