---
title: Befehl "nuget CLI-Update"
description: Referenz für den Befehl "nuget. exe Update"
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327507"
---
# <a name="update-command-nuget-cli"></a>Der Befehl „commnad“ (NuGet CLI)

**Gilt für:** &bullet; **unterstützte Versionen** von Paket Verbrauch: alle

Alle Pakete in einem Projekt werden (unter Verwendung von `packages.config`) auf die neuesten verfügbaren Versionen aktualisiert. Es wird empfohlen, ["Restore"](cli-ref-restore.md) auszuführen, bevor Sie `update`ausführen. (Um ein einzelnes Paket zu aktualisieren, [`nuget install`](cli-ref-install.md) verwenden Sie, ohne eine Versionsnummer anzugeben. in diesem Fall installiert nuget die neueste Version.)

Hinweis: `update` funktioniert nicht mit der CLI, die unter Mono (Mac OSX oder Linux) ausgeführt wird, oder wenn das packagereferenzierungsformat verwendet wird.

Der `update` Befehl aktualisiert außerdem Assemblyverweise in der Projektdatei, sofern diese Verweise bereits vorhanden sind. Wenn ein aktualisiertes Paket über eine hinzugefügte Assembly verfügt, wird *kein* neuer Verweis hinzugefügt. Neuen Paketabhängigkeiten werden auch keine Assemblyverweise hinzugefügt. Aktualisieren Sie das Paket in Visual Studio mithilfe der Benutzeroberfläche des Paket-Managers oder der Paket-Manager-Konsole, um diese Vorgänge als Teil eines Updates einzuschließen.

Dieser Befehl kann auch verwendet werden, um nuget. exe selbst mit dem *-Self-* Flag zu aktualisieren.

## <a name="usage"></a>Verwendung

```cli
nuget update <configPath> [options]
```

Dabei identifiziert entweder eine `packages.config` oder eine Projektmappendatei, die die Abhängigkeiten des Projekts auflistet. `<configPath>`

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.|
| FileConflictAction | Gibt die Aktion an, die ausgeführt werden soll, wenn die vom Projekt referenzierten Dateien überschrieben oder ignoriert werden sollen. Werte sind über *schreiben, ignorieren, keine*. |
| ForceEnglishOutput | *(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird. |
| Help | Zeigt Hilfe Informationen für den Befehl an. |
| Id | Gibt eine Liste der zu aktualisierenden Paket-IDs an. |
| MSBuildPath | *(4.0* und höher) Gibt den Pfad von MSBuild an, der mit dem Befehl verwendet werden soll `-MSBuildVersion`, und hat Vorrang vor. |
| MSBuildVersion | *(3.2 +)* Gibt die Version von MSBuild an, die mit diesem Befehl verwendet werden soll. Unterstützte Werte sind 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Standardmäßig wird der MSBuild in Ihrem Pfad ausgewählt; andernfalls wird standardmäßig die höchste installierte Version von MSBuild verwendet. |
| NonInteractive | Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen. |
| Vorab | Ermöglicht das Aktualisieren von vorab Versionen. Dieses Flag ist beim Aktualisieren bereits installierter vorab Pakete nicht erforderlich. |
| RepositoryPath | Gibt den lokalen Ordner an, in dem Pakete installiert werden. |
| Sauberem | Gibt an, dass nur Updates mit der höchsten Version, die innerhalb derselben Haupt-und neben Version wie das installierte Paket verfügbar ist, installiert werden. |
| Selbstbedienungs | Aktualisiert "nuget. exe" auf die neueste Version. alle anderen Argumente werden ignoriert. |
| Source | Gibt die Liste der Paketquellen (als URLs) an, die für die Updates verwendet werden sollen. Wenn der Befehl nicht angegeben wird, verwendet der Befehl die in den Konfigurationsdateien bereitgestellten Quellen, siehe [Allgemeine nuget-Konfigurationen](../../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*. |
| Version | Gibt bei Verwendung mit einer Paket-ID die Version des zu aktualisierenden Pakets an. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
