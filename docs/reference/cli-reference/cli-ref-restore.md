---
title: Befehl "nuget CLI Restore"
description: Referenz für den Befehl "nuget. exe Restore"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 211f24ff67c06da00d6a014e679cc422d493d6d5
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959740"
---
# <a name="restore-command-nuget-cli"></a>Restore-Befehl (nuget-CLI)

**Gilt für:** &bullet; **unterstützte Versionen** : 2.7+

Alle Pakete, die im `packages` Ordner fehlen, werden heruntergeladen und installiert. Bei der Verwendung mit nuget 4.0 und höher und dem packagereferenzierungsformat wird `<project>.nuget.props` `obj` bei Bedarf im Ordner eine Datei generiert. (Die Datei kann in der Quell Code Verwaltung ausgelassen werden.)

Unter Mac OSX und Linux mit der CLI in Mono wird das Wiederherstellen von Paketen mit packagereferenzierung nicht unterstützt.

## <a name="usage"></a>Verwendung

```cli
nuget restore <projectPath> [options]
```

Dabei gibt den Speicherort einer Projekt Mappe oder `packages.config` einer Datei an. `<projectPath>` Weitere Informationen zum Verhalten finden Sie in den [Hinweisen](#remarks).

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.|
| DirectDownload | *(4.0* und höher) Pakete werden direkt heruntergeladen, ohne dass Caches mit Binärdateien oder Metadaten aufgefüllt werden. |
| DisableParallelProcessing | Deaktiviert die parallele Wiederherstellung mehrerer Pakete. |
| FallbackSource | *(3.2 +)* Eine Liste von Paketquellen, die als Fallbacks verwendet werden sollen, falls das Paket nicht in der primären oder der Standard Quelle gefunden wurde. Verwenden Sie zum Trennen von Listeneinträgen ein Semikolon. |
| ForceEnglishOutput | *(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird. |
| Help | Zeigt Hilfe Informationen für den Befehl an. |
| MSBuildPath | *(4.0* und höher) Gibt den Pfad von MSBuild an, der mit dem Befehl verwendet werden soll `-MSBuildVersion`, und hat Vorrang vor. |
| MSBuildVersion | *(3.2 +)* Gibt die Version von MSBuild an, die mit diesem Befehl verwendet werden soll. Unterstützte Werte sind 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Standardmäßig wird der MSBuild in Ihrem Pfad ausgewählt; andernfalls wird standardmäßig die höchste installierte Version von MSBuild verwendet. |
| NoCache | Verhindert, dass nuget zwischengespeicherte Pakete verwendet. Weitere Informationen finden Sie [unter Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen. |
| OutputDirectory | Gibt den Ordner an, in dem Pakete installiert werden. Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet. Erforderlich, wenn mit einer `packages.config` Datei wieder `PackagesDirectory` hergestellt `SolutionDirectory` wird, sofern nicht oder verwendet wird.|
| PackageSaveMode | Gibt die Dateitypen an, die nach der Paketinstallation gespeichert werden `nuspec`sollen `nupkg`: einer `nuspec;nupkg`von, oder. |
| PackagesDirectory | Wie in `OutputDirectory`. Erforderlich, wenn mit einer `packages.config` Datei wieder `OutputDirectory` hergestellt `SolutionDirectory` wird, sofern nicht oder verwendet wird. |
| Project2ProjectTimeOut | Timeout in Sekunden für das Auflösen von Projekt-zu-Projekt-verweisen. |
| Rekursive | *(4.0* und höher) Stellt alle Referenzprojekte für UWP-und .net Core-Projekte wieder her. Gilt nicht für Projekte, die `packages.config`verwenden. |
| RequireConsent | Überprüft, ob das Wiederherstellen von Paketen aktiviert ist, bevor die Pakete heruntergeladen und installiert werden. Weitere Informationen finden Sie unter [Paket Wiederherstellung](../../consume-packages/package-restore.md). |
| Projektmappenverzeichnis | Gibt den Projektmappenordner an. Ungültig beim Wiederherstellen von Paketen für eine Projekt Mappe. Erforderlich, wenn mit einer `packages.config` Datei wieder `PackagesDirectory` hergestellt `OutputDirectory` wird, sofern nicht oder verwendet wird. |
| Source | Gibt die Liste der Paketquellen (als URLs) an, die für die Wiederherstellung verwendet werden sollen. Wenn der Befehl weggelassen wird, verwendet der Befehl die in den Konfigurationsdateien bereitgestellten Quellen, siehe [Konfigurieren des nuget-Verhaltens](../../consume-packages/configuring-nuget-behavior.md). Verwenden Sie zum Trennen von Listeneinträgen ein Semikolon. |
| Verbosity | Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="remarks"></a>Hinweise

Der Restore-Befehl führt die folgenden Schritte aus:

1. Bestimmen Sie den Betriebsmodus des Restore-Befehls.

   | ProjectPath-Dateityp | Verhalten |
   | --- | --- |
   | Lösung (Ordner) | Nuget sucht nach einer `.sln` Datei und verwendet diese, wenn Sie gefunden wird, andernfalls wird ein Fehler ausgegeben. `(SolutionDir)\.nuget`wird als Startordner verwendet. |
   | `.sln`Datei | Von der Lösung identifizierte Pakete wiederherstellen; Gibt einen Fehler aus `-SolutionDirectory` , wenn verwendet wird. `$(SolutionDir)\.nuget`wird als Startordner verwendet. |
   | `packages.config`-oder-Projektdatei | Wiederherstellen der in der Datei aufgeführten Pakete, auflösen und Installieren von Abhängigkeiten. |
   | Anderer Dateityp | Es wird davon ausgegangen, dass `.sln` eine Datei wie oben angegeben wird. wenn es sich nicht um eine Lösung handelt, gibt nuget einen Fehler aus. |
   | (ProjectPath nicht angegeben) | <ul><li>Nuget sucht im aktuellen Ordner nach Projektmappendateien. Wenn eine einzelne Datei gefunden wird, wird diese zum Wiederherstellen von Paketen verwendet. Wenn mehrere Lösungen gefunden werden, gibt nuget einen Fehler aus.</li><li>Wenn keine Projektmappendateien vorhanden sind, sucht nuget `packages.config` nach einem und verwendet dieses zum Wiederherstellen von Paketen.</li><li>Wenn keine Projekt Mappe `packages.config` oder Datei gefunden wird, gibt nuget einen Fehler aus.</ul> |

2. Bestimmen Sie den Ordner "Pakete" mit der folgenden Prioritäts Reihenfolge (nuget gibt einen Fehler aus, wenn keiner dieser Ordner gefunden wird):

    - Der mit `-PackagesDirectory`angegebene Ordner.
    - Der `repositoryPath` Wert in`Nuget.Config`
    - Der mit angegebene Ordner`-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Beim Wiederherstellen von Paketen für eine Lösung führt nuget Folgendes aus:
    - Lädt die Projektmappendatei.
    - Stellt Pakete auf Projektmappenebene wieder `packages` her, die in `$(SolutionDir)\.nuget\packages.config` aufgelistet sind.
    - Wiederherstellen der in `$(ProjectDir)\packages.config` aufgelisteten Pakete `packages` in den Ordner. Stellen Sie das Paket für jedes angegebene Paket parallel wieder her `-DisableParallelProcessing` , es sei denn, wird angegeben.

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
