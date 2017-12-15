---
title: NuGet CLI Wiederherstellungsbefehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee41020-e548-4e61-b8cd-c82b77ac6af7
description: "Referenz für die nuget.exe Restore-Befehl"
keywords: NuGet restore Verweis, der Synchronisierungsbefehl der Pakete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b435a3c2ffe08e3c2f8fc6a4dacb06cf674e4fb9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="restore-command-nuget-cli"></a>RESTORE-Befehl (NuGet CLI)

**Gilt für:** Verpacken Sie Verbrauch &bullet; **unterstützte Versionen:** 2.7 +

NuGet 2.7 +: Heruntergeladen und installiert alle Pakete fehlen in der `packages` Ordner.

NuGet 3.3 + mit Projekten, die mit `project.json`: generiert eine `project.lock.json` Datei und ein `<project>.nuget.props` -Datei bei Bedarf. (Beide Dateien können aus der quellcodeverwaltung weggelassen.)

NuGet 4.0 und höher mit Projekt, in welches Paket Verweise in der Projektdatei direkt enthalten sind: generiert eine `<project>.nuget.props` -Datei bei Bedarf in den `obj` Ordner. (Die Datei kann aus der quellcodeverwaltung ausgelassen werden.)

Unter Mac OS x und Linux mit der CLI auf Mono wird Wiederherstellen von Paketen mit dem PackageReference-Format nicht unterstützt.

## <a name="usage"></a>Verwendung

```
nuget restore <projectPath> [options]
```

auf dem `<projectPath>` gibt den Speicherort einer Projektmappe ein `packages.config` -Datei oder eine `project.json` Datei. Finden Sie unter ["Hinweise"](#remarks) unten überwachungshilfsprogrammen Informationen.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| "ConfigFile" hinzu | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird. |
| DirectDownload | *(4.0 und höher)*  Werden Pakete direkt ohne das Auffüllen des Caches mit Binärdateien oder Metadaten heruntergeladen. |
| DisableParallelProcessing | Deaktiviert, die mehrere Pakete gleichzeitig wiederhergestellt werden. |
| Alternativer | *(3.2 +)*  Eine Liste der Paketquellen überein, die als Zugriffe verwendet werden soll, für den Fall, dass das Paket nicht, in der primären gefunden wird oder Standardquelle. |
| ForceEnglishOutput | *(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| MSBuildPath | *(4.0 und höher)*  Gibt den Pfad des MSBuild für die Verwendung mit dem Befehl, Vorrang vor `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Gibt die Version von MSBuild mit diesem Befehl verwendet werden soll. Unterstützte Werte sind 4, 12, 14, 15. Standardmäßig werden die MSBuild-Datei in Ihrem Pfad abgerufen wird, wird standardmäßig andernfalls die neueste installierte Version von MSBuild. |
| NoCache | Verhindert, dass NuGet Pakete aus lokalen Caches. |
| Nicht interaktive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| OutputDirectory | Gibt den Ordner, in dem Pakete installiert sind. Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet. |
| PackageSaveMode | Gibt die Typen von Dateien nach der Paketinstallation speichern: einer der `nuspec`, `nupkg`, oder `nuspec;nupkg`. |
| PackagesDirectory | Wie in `OutputDirectory`. |
| Project2ProjectTimeOut | Timeout in Sekunden für das Auflösen von Verweisen zwischen Projekten. |
| Rekursive | *(4.0 und höher)*  Stellt alle Verweise-Projekte für universelle Windows-Plattform und .NET Core-Projekte wieder her. Gilt nicht für Projekte mit `packages.config`. |
| RequireConsent | Überprüft, ob Pakete werden wiederhergestellt aktiviert wird vor dem Herunterladen und Installieren der Pakete. Weitere Informationen finden Sie unter [Paketwiederherstellung](../consume-packages/package-restore.md). |
| SolutionDirectory | Gibt den Projektmappenordner. Gilt nicht beim Wiederherstellen von Paketen für eine Projektmappe. |
| Quelle | Gibt die Liste der Paketquellen (wie URLs) für die Verwendung für die Wiederherstellung an. Wenn nicht angegeben, wird der Befehl verwendet die Quellen in Konfigurationsdateien bereitgestellt, finden Sie unter [NuGet Konfigurieren von Verhalten](../Consume-Packages/Configuring-NuGet-Behavior.md). |
| Ausführlichkeit |> Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *detaillierte (2.5 und höher)*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="remarks"></a>Hinweise

Der Restore-Befehl führt die folgenden Schritte aus:

1. Bestimmen Sie den Betriebsmodus des Restore-Befehl.
    ProjectPath-Dateityp | Verhalten
    | --- | --- |
    Lösung (Ordner) | NuGet sucht nach einem `.sln` Datei und verwendet, die andernfalls einen Fehler enthält. `(SolutionDir)\.nuget`Dient als Ordner ab.
    `.sln`Datei | Wiederherstellen von Paketen, die von der Lösung identifiziert; generiert einen Fehler, wenn `-SolutionDirectory` verwendet wird. `$(SolutionDir)\.nuget`Dient als Ordner ab.
    `packages.config`, `project.json`, oder der Projektdatei | Stellen Sie Pakete, die in der Datei, die zu beheben, und Installieren von Abhängigkeiten aufgelisteten wieder her.
    Andere Dateityp | Datei wird angenommen, ein `.sln` Datei wie oben beschrieben; Wenn es sich nicht um eine Lösung, die NuGet-gibt einen Fehler handelt.
    (ProjectPath nicht angegeben) | -NuGet sucht nach berichtsprojektmappen-Dateien im aktuellen Ordner. Wenn eine einzelne Datei gefunden wird, verwendet wird, dass eine, Pakete wiederherzustellen. Wenn mehrere Lösungen gefunden werden, wird von NuGet ein Fehler generiert.
    |– Wenn keine Lösungsdateien vorhanden sind, sucht NuGet nach einem `packages.config` oder `project.json` dann verwendet, um das Wiederherstellen von Paketen.
    |– Wenn keine Projektmappendatei `packages.config`, oder `project.json` gefunden wird, ist NuGet generiert einen Fehler.

1. Bestimmen Sie den Ordner "Pakete" mithilfe der folgenden Prioritätsreihenfolge (NuGet generiert einen Fehler, wenn keiner dieser Ordner gefunden werden):

    - Die `%userprofile%\.nuget\packages` Wert in `project.json`.
    - Mit angegebenen Ordner `-PackagesDirectory`.
    - Die `repositoryPath` Wert in`Nuget.Config`
    - Den Ordner mit angegeben wird.`-SolutionDirectory`
    - `$(SolutionDir)\packages`

1. Beim Wiederherstellen von Paketen für eine Projektmappe führt NuGet Folgendes aus:
    - Lädt die Projektmappendatei.
    - Level-Lösungspakete abgelesen wiederhergestellt `$(SolutionDir)\.nuget\packages.config` in den `packages` Ordner.
    - Wiederherstellen aufgelisteten Pakete `$(ProjectDir)\packages.config` in den `packages` Ordner. Für jedes Paket angegeben wird, Wiederherstellen das Paket gleichzeitig, es sei denn, `-DisableParallelProcessing` angegeben ist.

## <a name="examples"></a>Beispiele

```
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
