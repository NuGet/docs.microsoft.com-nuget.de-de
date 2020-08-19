---
title: Befehl "nuget CLI Restore"
description: Referenz für den nuget.exe Restore-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 108317aba2107948180ab0149c0c5ba5150cf9b8
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622829"
---
# <a name="restore-command-nuget-cli"></a>Restore-Befehl (nuget-CLI)

**Gilt für:** &bullet; **unterstützte Versionen** von Paketen: 2.7 und höher

Alle Pakete, die im Ordner fehlen, werden heruntergeladen und installiert `packages` . Bei der Verwendung mit nuget 4.0 und höher und dem packagereferenzierungsformat wird `<project>.nuget.props` bei Bedarf im Ordner eine Datei generiert `obj` . (Die Datei kann in der Quell Code Verwaltung ausgelassen werden.)

Unter Mac OSX und Linux mit der CLI in Mono wird das Wiederherstellen von Paketen mit packagereferenzierung nicht unterstützt.

## <a name="usage"></a>Verwendung

```cli
nuget restore <projectPath> [options]
```

dabei `<projectPath>` gibt den Speicherort einer Projekt Mappe oder einer `packages.config` Datei an. Informationen zu den Verhaltens [Details finden Sie unten in](#remarks) den hinweisen.

## <a name="options"></a>Optionen

- **`-ConfigFile`**

  Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.

- **`-DirectDownload`**

  *(4.0* und höher) Pakete werden direkt heruntergeladen, ohne dass Caches mit Binärdateien oder Metadaten aufgefüllt werden.

- **`-DisableParallelProcessing`**

   Deaktiviert die parallele Wiederherstellung mehrerer Pakete.

- **`-FallbackSource`**

  *(3.2 +)* Eine Liste von Paketquellen, die als Fallbacks verwendet werden sollen, falls das Paket nicht in der primären oder der Standard Quelle gefunden wurde. Verwenden Sie zum Trennen von Listeneinträgen ein Semikolon.

- **`-Force`**

  In packagereferenzierungsbasierten Projekten erzwingt, dass alle Abhängigkeiten gelöst werden, auch wenn die letzte Wiederherstellung erfolgreich war. Die Angabe dieses Flags ähnelt dem Löschen der `project.assets.json` Datei. Dadurch wird der HTTP-Cache nicht umgangen.

- **`-ForceEnglishOutput`**

  *(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.

- **`-ForceEvaluate`**

  Erzwingt die Neubewertung aller Abhängigkeiten bei der Wiederherstellung, selbst wenn bereits eine Sperrdatei vorhanden ist.

- **`-?|-help`**

  Zeigt Hilfe Informationen für den Befehl an.

- **`-LockFilePath`**

  Ausgabespeicherort, in den die Projektsperrdatei geschrieben wird. Die Standardeinstellung ist `PROJECT_ROOT\packages.lock.json`.

- **`-LockedMode`**

  Lassen Sie keine Aktualisierung der Projektsperrdatei zu.

- **`-MSBuildPath`**

   *(4.0* und höher) Gibt den Pfad von MSBuild an, der mit dem Befehl verwendet werden soll, und hat Vorrang vor `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2 +)* Gibt die Version von MSBuild an, die mit diesem Befehl verwendet werden soll. Unterstützte Werte sind 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Standardmäßig wird der MSBuild in Ihrem Pfad ausgewählt; andernfalls wird standardmäßig die höchste installierte Version von MSBuild verwendet.

- **`-NoCache`**

  Verhindert, dass nuget zwischengespeicherte Pakete verwendet. Weitere Informationen finden Sie [unter Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-NonInteractive`**

  Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.

- **`-OutputDirectory`**

  Gibt den Ordner an, in dem Pakete installiert werden. Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet. Erforderlich, wenn mit einer `packages.config` Datei wieder hergestellt wird, sofern nicht `PackagesDirectory` oder `SolutionDirectory` verwendet wird.

- **`-PackageSaveMode`**

  Gibt die Dateitypen an, die nach der Paketinstallation gespeichert werden sollen: einer von `nuspec` , `nupkg` oder `nuspec;nupkg` .

- **`-PackagesDirectory`**

  Wie in `OutputDirectory`. Erforderlich, wenn mit einer `packages.config` Datei wieder hergestellt wird, sofern nicht `OutputDirectory` oder `SolutionDirectory` verwendet wird.

- **`-Project2ProjectTimeOut`**

  Timeout in Sekunden für das Auflösen von Projekt-zu-Projekt-verweisen.

- **`-Recursive`**

  *(4.0* und höher) Stellt alle Referenzprojekte für UWP-und .net Core-Projekte wieder her. Gilt nicht für Projekte, die verwenden `packages.config` .

- **`-RequireConsent`**

  Überprüft, ob das Wiederherstellen von Paketen aktiviert ist, bevor die Pakete heruntergeladen und installiert werden. Weitere Informationen finden Sie unter [Paket Wiederherstellung](../../consume-packages/package-restore.md).

- **`-SolutionDirectory`**

  Gibt den Projektmappenordner an. Ungültig beim Wiederherstellen von Paketen für eine Projekt Mappe. Erforderlich, wenn mit einer `packages.config` Datei wieder hergestellt wird, sofern nicht `PackagesDirectory` oder `OutputDirectory` verwendet wird.

- **`-Source`**

  Gibt die Liste der Paketquellen (als URLs) an, die für die Wiederherstellung verwendet werden sollen. Wenn der Befehl weggelassen wird, verwendet der Befehl die in den Konfigurationsdateien bereitgestellten Quellen, siehe [Konfigurieren des nuget-Verhaltens](../../consume-packages/configuring-nuget-behavior.md). Verwenden Sie zum Trennen von Listeneinträgen ein Semikolon.

- **`-UseLockFile`**

  Ermöglicht das Generieren und Verwenden einer Projektsperrdatei bei der Wiederherstellung.

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="remarks"></a>Hinweise

Der Restore-Befehl führt die folgenden Schritte aus:

1. Bestimmen Sie den Betriebsmodus des Restore-Befehls.

   | ProjectPath-Dateityp | Verhalten |
   | --- | --- |
   | Lösung (Ordner) | Nuget sucht nach einer `.sln` Datei und verwendet diese, wenn Sie gefunden wird, andernfalls wird ein Fehler ausgegeben. `(SolutionDir)\.nuget` wird als Startordner verwendet. |
   | `.sln`-Datei | Von der Lösung identifizierte Pakete wiederherstellen; Gibt einen Fehler aus, wenn `-SolutionDirectory` verwendet wird. `$(SolutionDir)\.nuget` wird als Startordner verwendet. |
   | `packages.config` -oder-Projektdatei | Wiederherstellen der in der Datei aufgeführten Pakete, auflösen und Installieren von Abhängigkeiten. |
   | Anderer Dateityp | Es wird davon ausgegangen, dass eine Datei `.sln` wie oben angegeben wird. wenn es sich nicht um eine Lösung handelt, gibt nuget einen Fehler aus. |
   | (ProjectPath nicht angegeben) | <ul><li>Nuget sucht im aktuellen Ordner nach Projektmappendateien. Wenn eine einzelne Datei gefunden wird, wird diese zum Wiederherstellen von Paketen verwendet. Wenn mehrere Lösungen gefunden werden, gibt nuget einen Fehler aus.</li><li>Wenn keine Projektmappendateien vorhanden sind, sucht nuget nach einem `packages.config` und verwendet dieses zum Wiederherstellen von Paketen.</li><li>Wenn keine Projekt `packages.config` Mappe oder Datei gefunden wird, gibt nuget einen Fehler aus.</ul> |

2. Bestimmen Sie den Ordner "Pakete" mit der folgenden Prioritäts Reihenfolge (nuget gibt einen Fehler aus, wenn keiner dieser Ordner gefunden wird):

    - Der mit angegebene Ordner `-PackagesDirectory` .
    - Der `repositoryPath` Wert in `Nuget.Config`
    - Der mit angegebene Ordner `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Beim Wiederherstellen von Paketen für eine Lösung führt nuget Folgendes aus:
    - Lädt die Projektmappendatei.
    - Stellt Pakete auf `$(SolutionDir)\.nuget\packages.config` Projektmappenebene wieder her, die in aufgelistet sind `packages` .
    - Wiederherstellen der in aufgelisteten Pakete in `$(ProjectDir)\packages.config` den `packages` Ordner. Stellen Sie das Paket für jedes angegebene Paket parallel wieder her, es sei denn, `-DisableParallelProcessing` wird angegeben.

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
