---
title: Befehl "nuget CLI-Update"
description: Referenz für den nuget.exe Update-Befehl
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 84f939188ac190f6d539f8ee2b422049a274f178
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622576"
---
# <a name="update-command-nuget-cli"></a>Befehl Aktualisieren (nuget-CLI)

**Gilt für:** &bullet; **unterstützte Versionen** von Paket Verbrauch: alle

Alle Pakete in einem Projekt werden (unter Verwendung von `packages.config`) auf die neuesten verfügbaren Versionen aktualisiert. Es wird empfohlen, ["Restore"](cli-ref-restore.md) auszuführen, bevor Sie Ausführen `update` . (Um ein einzelnes Paket zu aktualisieren, verwenden Sie, [`nuget install`](cli-ref-install.md) ohne eine Versionsnummer anzugeben. in diesem Fall installiert nuget die neueste Version.)

Hinweis: `update` funktioniert nicht mit der CLI, die unter Mono (Mac OSX oder Linux) ausgeführt wird, oder wenn das packagereferenzierungsformat verwendet wird.

Der `update` Befehl aktualisiert außerdem Assemblyverweise in der Projektdatei, sofern diese Verweise bereits vorhanden sind. Wenn ein aktualisiertes Paket über eine hinzugefügte Assembly verfügt, wird *kein* neuer Verweis hinzugefügt. Neuen Paketabhängigkeiten werden auch keine Assemblyverweise hinzugefügt. Aktualisieren Sie das Paket in Visual Studio mithilfe der Benutzeroberfläche des Paket-Managers oder der Paket-Manager-Konsole, um diese Vorgänge als Teil eines Updates einzuschließen.

Dieser Befehl kann auch verwendet werden, um nuget.exe mit dem *-Self-* Flag zu aktualisieren.

## <a name="usage"></a>Verwendung

```cli
nuget update <configPath> [options]
```

dabei `<configPath>` identifiziert entweder eine `packages.config` oder eine Projektmappendatei, die die Abhängigkeiten des Projekts auflistet.

## <a name="options"></a>Optionen

- **`-ConfigFile`**

  Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  Gibt die Standardaktion an, wenn eine Datei aus einem Paket im Ziel Projekt bereits vorhanden ist. Legen Sie auf fest, `Overwrite` um Dateien immer zu überschreiben. Auf festlegen, `Ignore` um Dateien zu überspringen.

  Durch die `PromptUser` Aktion (Standardeinstellung) wird eine Eingabeaufforderung für jede in Konflikt stehende Datei angezeigt, sofern nicht `OverwriteAll` oder angegeben wird `IgnoreAll` , was für alle verbleibenden Dateien gilt.

- **`-ForceEnglishOutput`**

  *(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.

- **`-?|-help`**

  Zeigt Hilfe Informationen für den Befehl an.

- **`-Id`**

  Gibt eine Liste der zu aktualisierenden Paket-IDs an.

- **`-MSBuildPath`**

  *(4.0* und höher) Gibt den Pfad von MSBuild an, der mit dem Befehl verwendet werden soll, und hat Vorrang vor `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2 +)* Gibt die Version von MSBuild an, die mit diesem Befehl verwendet werden soll. Unterstützte Werte sind 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Standardmäßig wird der MSBuild in Ihrem Pfad ausgewählt; andernfalls wird standardmäßig die höchste installierte Version von MSBuild verwendet.

- **`-NonInteractive`**

  Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.

- **`-PreRelease`**

  Ermöglicht das Aktualisieren von vorab Versionen. Dieses Flag ist beim Aktualisieren bereits installierter vorab Pakete nicht erforderlich.

- **`-RepositoryPath`**

  Gibt den lokalen Ordner an, in dem Pakete installiert werden.

- **`-Safe`**

  Gibt an, dass nur Updates mit der höchsten Version, die innerhalb derselben Haupt-und neben Version wie das installierte Paket verfügbar ist, installiert werden.

- **`-Self`**

  Aktualisiert nuget.exe auf die neueste Version. alle anderen Argumente werden ignoriert.

- **`-Source`**

  Gibt die Liste der Paketquellen (als URLs) an, die für die Updates verwendet werden sollen. Wenn der Befehl nicht angegeben wird, verwendet der Befehl die in den Konfigurationsdateien bereitgestellten Quellen, siehe [Allgemeine nuget-Konfigurationen](../../consume-packages/configuring-nuget-behavior.md).

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .

- **`-Version`**

  Gibt bei Verwendung mit einer Paket-ID die Version des zu aktualisierenden Pakets an.

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
