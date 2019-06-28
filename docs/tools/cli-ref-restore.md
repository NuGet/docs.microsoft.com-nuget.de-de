---
title: NuGet-CLI-Befehl "Restore"
description: Referenz für die nuget.exe-Restore-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3d7a4188de4fb6f812ca19e7f9e302a5a133c58b
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425969"
---
# <a name="restore-command-nuget-cli"></a>RESTORE-Befehl (NuGet-CLI)

**Gilt für:** Paket Verbrauch &bullet; **unterstützte Versionen:** 2.7+

Heruntergeladen und installiert alle Pakete fehlen die `packages` Ordner. Mit NuGet 4.0 und höher und das PackageReference-Format verwendet, generiert eine `<project>.nuget.props` Datei bei Bedarf, in der `obj` Ordner. (Die Datei kann aus der quellcodeverwaltung ausgelassen werden.)

Unter Mac OSX und Linux über die Befehlszeilenschnittstelle in Mono wird das Wiederherstellen von Paketen nicht mit "packagereference" unterstützt.

## <a name="usage"></a>Verwendung

```cli
nuget restore <projectPath> [options]
```

wo `<projectPath>` gibt den Speicherort einer Projektmappe oder ein `packages.config` Datei. Finden Sie unter ["Hinweise"](#remarks) unten Verhalten Details.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| DirectDownload | *(4.0 und höher)*  Werden Pakete direkt, ohne Auffüllen des Caches mit Binärdateien oder Metadaten heruntergeladen. |
| DisableParallelProcessing | Deaktiviert, die mehrere Pakete gleichzeitig wiederhergestellt werden. |
| FallbackSource | *(3.2 und höher)*  Eine Liste der Paketquellen, die als Fallbacks verwendet werden soll, für den Fall, dass das Paket nicht, auf dem primären gefunden wird oder Standardquelle. |
| ForceEnglishOutput | *(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden. |
| Help | Zeigt die Informationen für den Befehl Hilfe. |
| MSBuildPath | *(4.0 und höher)*  Gibt den Pfad des MSBuild für die Verwendung mit dem Befehl vor `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 und höher)*  Gibt die Version von MSBuild mit dem folgenden Befehl verwendet werden. Unterstützte Werte sind 4, 12, 14, 15.1, 15.3, Version 15.4, Version 15.5, 15.6, 15.7, 15.8, 15.9. Standardmäßig die MSBuild in Ihrem Pfad ausgewählt wird, wird standardmäßig andernfalls die neueste installierte Version von MSBuild. |
| NoCache | Verhindert, dass NuGet zwischengespeicherte Pakete verwenden. Finden Sie unter [Verwalten der globalen Paketordner und Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| OutputDirectory | Gibt den Ordner, in dem Pakete installiert sind. Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet. Erforderlich, wenn die Wiederherstellung mit einem `packages.config` Datei, wenn `PackagesDirectory` oder `SolutionDirectory` verwendet wird.|
| PackageSaveMode | Gibt die Typen von Dateien, die nach der Paketinstallation speichern: einer der `nuspec`, `nupkg`, oder `nuspec;nupkg`. |
| PackagesDirectory | Wie in `OutputDirectory`. Erforderlich, wenn die Wiederherstellung mit einem `packages.config` Datei, wenn `OutputDirectory` oder `SolutionDirectory` verwendet wird. |
| Project2ProjectTimeOut | Timeout in Sekunden zum Auflösen von Projekt-zu-Projekt-verweisen. |
| Rekursive | *(4.0 und höher)*  Stellt alle Verweise-Projekte für UWP und .NET Core-Projekte wieder her. Gilt nicht für Projekte mit `packages.config`. |
| RequireConsent | Stellt sicher, dass die Wiederherstellung von Paketen aktiviert ist, vor dem Herunterladen und Installieren der Pakete. Weitere Informationen finden Sie unter [Paketwiederherstellung](../consume-packages/package-restore.md). |
| SolutionDirectory | Gibt den Projektmappenordner. Gilt nicht beim Wiederherstellen von Paketen für eine Lösung. Erforderlich, wenn die Wiederherstellung mit einem `packages.config` Datei, wenn `PackagesDirectory` oder `OutputDirectory` verwendet wird. |
| Source | Gibt die Liste der Paketquellen (wie URLs) für die Verwendung für die Wiederherstellung an. Wenn nicht angegeben, wird der Befehl verwendet die Quellen in Konfigurationsdateien, finden Sie unter [Konfigurieren des NuGet-Verhaltens](../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="remarks"></a>Hinweise

Der Restore-Befehl führt die folgenden Schritte aus:

1. Bestimmen Sie den Betriebsmodus des Restore-Befehl.

   | ProjectPath-Dateityp | Verhalten |
   | --- | --- |
   | Projektmappen (Ordner) | NuGet sucht nach einer `.sln` -Datei und verwendet, die andernfalls ein Fehler angezeigt wird. `(SolutionDir)\.nuget` Dient als Ordner ab. |
   | `.sln` Datei | Wiederherstellen von Paketen, die von der Lösung identifiziert; Gibt einen Fehler aus, wenn `-SolutionDirectory` verwendet wird. `$(SolutionDir)\.nuget` Dient als Ordner ab. |
   | `packages.config` oder einer Projektdatei | Wiederherstellen von Paketen, die in der Datei, beheben und Installieren von Abhängigkeiten aufgeführt. |
   | Andere Dateityp | Datei wird als eine `.sln` wie oben beschrieben; Datei, wenn es sich nicht um eine Lösung, NuGet bietet ein Fehler ist. |
   | (ProjectPath nicht angegeben) | <ul><li>NuGet sucht nach Projektmappendateien im aktuellen Ordner. Wenn eine einzelne Datei gefunden wird, ist, dass eine zum Wiederherstellen von Paketen verwendet. Wenn mehrere Lösungen gefunden werden, gibt NuGet einen Fehler aus.</li><li>Wenn keine Projektmappendateien vorhanden sind, sucht NuGet nach einem `packages.config` verwendet, um die Pakete wiederherzustellen.</li><li>Wenn keine Projektmappe oder `packages.config` Datei gefunden wird, gibt NuGet einen Fehler aus.</ul> |

2. Bestimmen Sie den Ordner "Pakete" mithilfe der folgenden Prioritätsreihenfolge (NuGet gibt einen Fehler, wenn keiner dieser Ordner gefunden werden):

    - Der Ordner, der mit angegebenen `-PackagesDirectory`.
    - Die `repositoryPath` Wert `Nuget.Config`
    - Der Ordner, der mit angegebenen `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Beim Wiederherstellen von Paketen für eine Projektmappe, führt NuGet Folgendes aus:
    - Lädt die Projektmappendatei.
    - Ebene aufgeführt, die Projektmappen-Pakete wiederhergestellt `$(SolutionDir)\.nuget\packages.config` in die `packages` Ordner.
    - Wiederherstellen von Paketen in aufgeführten `$(ProjectDir)\packages.config` in die `packages` Ordner. Das Paket parallel wiederherstellen für jedes Paket angegeben, es sei denn, `-DisableParallelProcessing` angegeben ist.

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
