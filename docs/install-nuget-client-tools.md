---
title: Installieren von NuGet-Clienttools
description: Anleitung zum Installieren von Clienttools, der dotnet- und nuget-Befehlszeilenschnittstellen (Command-Line Interface, CLI) und des Paket-Managers für Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: 0e3938fc1ac748285ba26541a7d4e907c9a64156
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775902"
---
# <a name="install-nuget-client-tools"></a>Installieren von NuGet-Clienttools

> **Sie möchten ein Paket installieren? Weitere Informationen unter [Möglichkeiten zum Installieren von NuGet-Paketen](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).**

Damit Sie als Paketverbraucher oder -ersteller mit NuGet arbeiten können, können Sie Befehlszeilenschnittstellentools (CLI) und NuGet-Features in Visual Studio verwenden. Dieser Artikel beschreibt kurz die Funktionen der verschiedenen Tools, wie sie installiert werden und ihre [Verfügbarkeit von Features](#feature-availability) im Vergleich. Informationen zum Einstieg in das Nutzen von Paketen mithilfe von NuGet finden Sie unter [Installieren und Verwenden eines Pakets (dotnet-CLI)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) und [Installieren und Verwenden eines Pakets (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md). Informationen zum Einstieg in das Erstellen von NuGet-Paketen finden Sie unter [Create and publish a NET Standard package (dotnet CLI) [Erstellen und Veröffentlichen eines NET Standard-Pakets (.NET CLI)]](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) und [Create and publish a NET Standard package (Visual Studio) [Erstellen und Veröffentlichen eines NET Standard-Pakets (Visual Studio)]](quickstart/create-and-publish-a-package-using-visual-studio.md).

| Tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Beschreibung | Herunterladen&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | CLI-Tool für .NET Core- und .NET Standard-Bibliotheken und für beliebige [Projekte im SDK-Format](resources/check-project-format.md), z. B. ein Projekt für .NET Framework. Im .NET Core SDK enthalten und stellt NuGet-Kernfeatures auf allen Plattformen bereit. (Ab Visual Studio 2017 wird die dotnet-CLI automatisch mit jeder .NET Core-bezogenen Workload installiert.)| [.NET Core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | CLI-Tool für .NET Framework-Bibliotheken und für beliebige [Projekte, im Nicht-SDK-Format](resources/check-project-format.md), z.B. ein Projekt für .NET-Standard-Bibliotheken. Stellt alle Funktionen von NuGet unter Windows und die meisten Features für Mac und Linux unter Mono bereit. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | Unter Windows ist der **NuGet-Paket-Manager** in Visual Studio 2012 und höher enthalten. Visual Studio stellt die [Paket-Manager-Benutzeroberfläche](consume-packages/install-use-packages-visual-studio.md) und die [Paket-Manager-Konsole](consume-packages/install-use-packages-powershell.md) bereit, über die Sie die meisten NuGet-Vorgänge ausführen können. | [Visual Studio](https://www.visualstudio.com/downloads/) |
| [Visual Studio für Mac](/visualstudio/mac/nuget-walkthrough) | Unter Mac sind bestimmte Funktionen von NuGet direkt integriert. Die Paket-Manager-Konsole ist derzeit nicht verfügbar. Verwenden Sie die CLI-Tools `dotnet.exe` oder `nuget.exe` für weitere Funktionen.  | [Visual Studio für Mac](https://visualstudio.microsoft.com/vs/mac/) |
| [Visual Studio Code](https://code.visualstudio.com/docs) | Unter Windows, Mac oder Linux sind Funktionen von NuGet über Marketplace-Erweiterungen oder durch die Verwendung der CLI-Tools `dotnet.exe` oder `nuget.exe` verfügbar. | [Visual Studio Code](https://code.visualstudio.com/Download/)|

Die [MSBuild-CLI](reference/msbuild-targets.md) bietet auch die Möglichkeit, Pakete wiederherzustellen und zu erstellen, was vor allem auf Buildservern nützlich ist. MSBuild ist kein Allzwecktool für die Arbeit mit NuGet.

Die Konsolenbefehle des Paket-Managers funktionieren nur in Visual Studio unter Windows und nicht in anderen PowerShell-Umgebungen.

## <a name="visual-studio"></a>Visual Studio
### <a name="install-on-visual-studio-2017-and-newer"></a>Installieren in Visual Studio 2017 und höher
Ab Visual Studio 2017 schließt der Installer den NuGet-Paket-Manager für alle Workloads ein, die .NET verwenden. Um eine separate Installation durchzuführen oder um zu überprüfen, ob der Paket-Manager installiert wurde, führen Sie den Visual Studio-Installer aus, und überprüfen Sie die Option unter **Einzelne Komponenten > Codetools > NuGet-Paket-Manager**.

### <a name="install-on-visual-studio-2015-and-older"></a>Installieren in Visual Studio 2015 und früheren Versionen
NuGet-Erweiterungen für Visual Studio 2013 und 2015 können über [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) heruntergeladen werden.

Installieren Sie die Erweiterung „NuGet-Paket-Manager in Visual Studio“, wenn Sie Visual Studio 2010 oder früher verwenden. Hinweis: Wenn die Erweiterung nicht auf der ersten Seite der Suchergebnisse angezeigt wird, versuchen Sie, die Dropdownliste „Sortieren nach“ in „Am häufigsten heruntergeladen“ oder in eine alphabetische Sortierung zu ändern.

## <a name="cli-tools"></a>CLI-Tools
Sie können entweder die `dotnet`-CLI oder die `nuget.exe`-CLI verwenden, um NuGet-Features in der IDE zu unterstützen. Die `dotnet`-CLI wird mit einigen Visual Studio-Workloads installiert, z.B. .NET Core. Die `nuget.exe`-CLI muss wie oben beschrieben separat installiert werden.

`dotnet.exe` und `nuget.exe` sind die zwei NuGet-CLI-Tools. Einen Vergleich finden Sie unter [Verfügbarkeit von Features](#feature-availability).

* Für .NET Core oder .NET Standard verwenden Sie die dotnet-CLI. Die `dotnet`-CLI ist für das Projektformat im SDK-Stil erforderlich, welches das [SDK-Attribut](/dotnet/core/tools/csproj#additions) verwendet.
* Verwenden Sie für eine Ausrichtung auf .NET Framework (nur Nicht-SDK-Projekte) die `nuget.exe`-CLI. Wenn das Projekt von `packages.config` zu PackageReference migriert wird, verwenden Sie die dotnet-CLI.

### <a name="dotnetexe-cli"></a>dotnet.exe-CLI

Die .NET Core 2.0-CLI `dotnet.exe` funktioniert auf allen Plattformen (Windows, Mac und Linux) und stellt NuGet-Kernfeatures bereit, wie z.B. das Installieren, Wiederherstellen und Veröffentlichen von Paketen. Durch `dotnet` wird die direkte Integration von .NET Core-Projektdateien (z.B. `.csproj`) ermöglicht, was in den meisten Szenarios hilfreich ist. `dotnet` wird auch für jede Plattform direkt erstellt und erfordert keine Installation von Mono.

Installation:

- Installieren Sie auf Entwicklercomputern das [.NET Core SDK](https://aka.ms/dotnetcoregs). Ab Visual Studio 2017 wird die dotnet-CLI automatisch mit jeder .NET Core-bezogenen Workload installiert.
- Befolgen Sie für Buildserver die Anweisungen unter [Verwenden der .NET Core SDK und Tools in Continuous Integration](/dotnet/core/tools/using-ci-with-cli).

Informationen zur Verwendung grundlegender Befehle der dotnet-CLI finden Sie unter [Installieren und Verwenden von Paketen mit der dotnet-CLI](consume-packages/install-use-packages-dotnet-cli.md).

### <a name="nugetexe-cli"></a>nuget.exe-CLI

Die `nuget.exe`-CLI `nuget.exe` ist das Befehlszeilenprogramm für Windows, über das alle Funktionen von NuGet bereitgestellt werden. Mit [Mono](https://www.mono-project.com/docs/getting-started/install/) kann es (mit Einschränkungen) auch unter Mac OSX und Linux ausgeführt werden.

Informationen zur Verwendung grundlegender Befehle der `nuget.exe`-CLI finden Sie unter [Installieren und Verwenden von Paketen mit der nuget.exe-CLI](consume-packages/install-use-packages-nuget-cli.md).

Installation:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Verwenden Sie unter Windows `nuget update -self`, um eine vorhandene „nuget.exe“-Datei auf die neueste Version zu aktualisieren.

> [!Note]
> Die neueste empfohlene NuGet-CLI ist immer unter `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe` verfügbar. Für die Kompatibilität mit älteren Continuous Integration-Systemen wird aktuell über die vorherige URL, `https://nuget.org/nuget.exe`, das [veraltete 2.8.6 CLI-Tool](https://github.com/NuGet/NuGetGallery/issues/5381) zur Verfügung gestellt.

## <a name="feature-availability"></a>Verfügbarkeit von Features

| Feature | dotnet-CLI | NuGet-CLI (Windows) | NuGet-CLI (Mono) | Visual Studio (Windows) | Visual Studio für Mac |
| --- | --- | --- | --- | --- | --- |
| Suchen von Paketen |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Pakete installieren oder deinstallieren | &#10004; | &#10004;(1) | &#10004; | &#10004; | &#10004; |
| Aktualisieren von Paketen | &#10004; | &#10004; | | &#10004; | &#10004; |
| Pakete wiederherstellen | &#10004; | &#10004; | &#10004;(2) | &#10004; | &#10004; |
| Paketfeeds verwalten (Quellen) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Pakete auf einem Feed verwalten | &#10004; | &#10004; | &#10004; | | |
| API-Schlüsseln für Feeds festlegen | | &#10004; | &#10004; | | |
| Pakete erstellen(3) | &#10004; | &#10004; | &#10004;(4) | &#10004; | |
| Veröffentlichen von Paketen | &#10004; | &#10004; | &#10004; | &#10004; |  |
| Pakete replizieren |  | &#10004; | &#10004; | | |
| Verwalten des Ordners *global-packages* und des Cacheordners | &#10004; | &#10004; | &#10004; | | |
| NuGet-Konfiguration verwalten | | &#10004; | &#10004; | | |

(1) Hat keinen Einfluss auf Projektdateien; verwenden Sie stattdessen `dotnet.exe`.

(2) Funktioniert nur mit der `packages.config`-Datei und nicht mit Projektmappendateien (`.sln`).

(3) Verschiedene fortgeschrittene Paketfeatures sind nur über die CLI verfügbar, sie werden nicht in den Tools der Visual Studio-Benutzeroberfläche dargestellt.

(4) Funktioniert bei `.nuspec`-Dateien, jedoch nicht bei Projektdateien.

## <a name="upcoming-features"></a>Demnächst verfügbare Features
Wenn Sie eine Vorschau der geplanten NuGet-Features sehen möchten, installieren Sie eine [Vorschauversion von Visual Studio](https://www.visualstudio.com/vs/preview/), die mit stabilen Releases von Visual Studio zusammenarbeitet. Wenn Sie Probleme melden oder Ideen für Vorschauversionen teilen möchten, können Sie sich am [GitHub-Repository von NuGet](https://github.com/Nuget/Home/issues) beteiligen.

### <a name="related-topics"></a>Verwandte Themen

- [Installieren und Verwalten von Paketen mit Visual Studio](consume-packages/install-use-packages-visual-studio.md)
- [Installieren und Verwalten von Paketen mit PowerShell](consume-packages/install-use-packages-powershell.md)
- [Installieren und Verwalten von Paketen mit der dotnet-CLI](consume-packages/install-use-packages-dotnet-cli.md)
- [Installieren und Verwalten von Paketen mit der nuget.exe-CLI](consume-packages/install-use-packages-nuget-cli.md)
- [PowerShell-Verweis des Paket-Managers](reference/powershell-reference.md)
- [Erstellen eines Pakets](create-packages/creating-a-package.md)
- [Veröffentlichen eines Pakets](nuget-org/publish-a-package.md)

Entwickler, die unter Windows arbeiten, können auch den [NuGet-Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) durchsuchen, ein eigenständiges Open-Source-Tool, mit dem NuGet-Pakete visuell angezeigt, erstellt und bearbeitet werden können. Dieses Tool ist beispielsweise sehr hilfreich, wenn experimentelle Änderungen an einer Paketstruktur vorgenommen werden, ohne das Paket jedes Mal neu erstellen zu müssen.
