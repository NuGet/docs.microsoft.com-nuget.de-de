---
title: NuGet CLI Wiederherstellungsbefehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenz für die nuget.exe Restore-Befehl
keywords: NuGet restore Verweis, der Synchronisierungsbefehl der Pakete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 64f12fdedc8fbfcee15c1dcddc445148f458c030
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="restore-command-nuget-cli"></a>RESTORE-Befehl (NuGet CLI)

**Gilt für:** Verpacken Sie Verbrauch &bullet; **unterstützte Versionen:** 2.7 +

Herunterlädt und installiert alle Pakete fehlen in der `packages` Ordner. Bei Verwendung mit NuGet 4.0 und höher und das Format PackageReference generiert eine `<project>.nuget.props` -Datei bei Bedarf in den `obj` Ordner. (Die Datei kann aus der quellcodeverwaltung ausgelassen werden.)

Unter Mac OS x und Linux mit der CLI auf Mono wird Wiederherstellen von Paketen mit PackageReference nicht unterstützt.

## <a name="usage"></a>Verwendung

```cli
nuget restore <projectPath> [options]
```

wobei `<projectPath>` gibt den Speicherort einer Projektmappe oder ein `packages.config` Datei. Finden Sie unter ["Hinweise"](#remarks) unten überwachungshilfsprogrammen Informationen.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| DirectDownload | *(4.0 und höher)*  Werden Pakete direkt ohne das Auffüllen des Caches mit Binärdateien oder Metadaten heruntergeladen. |
| DisableParallelProcessing | Deaktiviert, die mehrere Pakete gleichzeitig wiederhergestellt werden. |
| FallbackSource | *(3.2 +)*  Eine Liste der Paketquellen überein, die als Zugriffe verwendet werden soll, für den Fall, dass das Paket nicht, in der primären gefunden wird oder Standardquelle. |
| ForceEnglishOutput | *(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| MSBuildPath | *(4.0 und höher)*  Gibt den Pfad des MSBuild für die Verwendung mit dem Befehl, Vorrang vor `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Gibt die Version von MSBuild mit diesem Befehl verwendet werden soll. Unterstützte Werte sind 4, 12, 14, 15. Standardmäßig werden die MSBuild-Datei in Ihrem Pfad abgerufen wird, wird standardmäßig andernfalls die neueste installierte Version von MSBuild. |
| NoCache | Verhindert, dass NuGet zwischengespeicherten Pakete verwenden. Finden Sie unter [Verwaltung der globalen Pakete und der Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| OutputDirectory | Gibt den Ordner, in dem Pakete installiert sind. Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet. Erforderlich, wenn die Wiederherstellung mit einem `packages.config` Datei, es sei denn, `PackagesDirectory` oder `SolutionDirectory` verwendet wird.|
| PackageSaveMode | Gibt die Typen von Dateien nach der Paketinstallation speichern: einer der `nuspec`, `nupkg`, oder `nuspec;nupkg`. |
| PackagesDirectory | Wie in `OutputDirectory`. Erforderlich, wenn die Wiederherstellung mit einem `packages.config` Datei, es sei denn, `OutputDirectory` oder `SolutionDirectory` verwendet wird. |
| Project2ProjectTimeOut | Timeout in Sekunden für das Auflösen von Verweisen zwischen Projekten. |
| Rekursive | *(4.0 und höher)*  Stellt alle Verweise-Projekte für universelle Windows-Plattform und .NET Core-Projekte wieder her. Gilt nicht für Projekte mit `packages.config`. |
| RequireConsent | Überprüft, ob Pakete werden wiederhergestellt aktiviert wird vor dem Herunterladen und Installieren der Pakete. Weitere Informationen finden Sie unter [Paketwiederherstellung](../consume-packages/package-restore.md). |
| SolutionDirectory | Gibt den Projektmappenordner. Gilt nicht beim Wiederherstellen von Paketen für eine Projektmappe. Erforderlich, wenn die Wiederherstellung mit einem `packages.config` Datei, es sei denn, `PackagesDirectory` oder `OutputDirectory` verwendet wird. |
| Quelle | Gibt die Liste der Paketquellen (wie URLs) für die Verwendung für die Wiederherstellung an. Wenn nicht angegeben, wird der Befehl verwendet die Quellen in Konfigurationsdateien bereitgestellt, finden Sie unter [NuGet Konfigurieren von Verhalten](../consume-packages/configuring-nuget-behavior.md). |
| Ausführlichkeit |> Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="remarks"></a>Hinweise

Der Restore-Befehl führt die folgenden Schritte aus:

1. Bestimmen Sie den Betriebsmodus des Restore-Befehl.
    ProjectPath-Dateityp | Verhalten
    | --- | --- |
    Lösung (Ordner) | NuGet sucht nach einem `.sln` Datei und verwendet, die andernfalls einen Fehler enthält. `(SolutionDir)\.nuget` Dient als Ordner ab.
    `.sln` Datei | Wiederherstellen von Paketen, die von der Lösung identifiziert; generiert einen Fehler, wenn `-SolutionDirectory` verwendet wird. `$(SolutionDir)\.nuget` Dient als Ordner ab.
    `packages.config` oder der Projektdatei | Stellen Sie Pakete, die in der Datei, die zu beheben, und Installieren von Abhängigkeiten aufgelisteten wieder her.
    Andere Dateityp | Datei wird angenommen, ein `.sln` Datei wie oben beschrieben; Wenn es sich nicht um eine Lösung, die NuGet-gibt einen Fehler handelt.
    (ProjectPath nicht angegeben) | -NuGet sucht nach berichtsprojektmappen-Dateien im aktuellen Ordner. Wenn eine einzelne Datei gefunden wird, verwendet wird, dass eine, Pakete wiederherzustellen. Wenn mehrere Lösungen gefunden werden, wird von NuGet ein Fehler generiert.
    |– Wenn keine Lösungsdateien vorhanden sind, sucht NuGet nach einem `packages.config` dann verwendet, um das Wiederherstellen von Paketen.
    |– Wenn keine Lösung oder `packages.config` Datei gefunden wird, NuGet generiert einen Fehler.

1. Bestimmen Sie den Ordner "Pakete" mithilfe der folgenden Prioritätsreihenfolge (NuGet generiert einen Fehler, wenn keiner dieser Ordner gefunden werden):

    - Mit angegebenen Ordner `-PackagesDirectory`.
    - Die `repositoryPath` Wert in `Nuget.Config`
    - Den Ordner mit angegeben wird. `-SolutionDirectory`
    - `$(SolutionDir)\packages`

1. Beim Wiederherstellen von Paketen für eine Projektmappe führt NuGet Folgendes aus:
    - Lädt die Projektmappendatei.
    - Level-Lösungspakete abgelesen wiederhergestellt `$(SolutionDir)\.nuget\packages.config` in den `packages` Ordner.
    - Wiederherstellen aufgelisteten Pakete `$(ProjectDir)\packages.config` in den `packages` Ordner. Für jedes Paket angegeben wird, Wiederherstellen das Paket gleichzeitig, es sei denn, `-DisableParallelProcessing` angegeben ist.

## <a name="examples"></a>Beispiele

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
