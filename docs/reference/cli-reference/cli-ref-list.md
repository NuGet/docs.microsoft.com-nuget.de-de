---
title: Befehl "nuget CLI List"
description: Referenz für den Befehl "nuget. exe list"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327737"
---
# <a name="list-command-nuget-cli"></a>List-Befehl (nuget-CLI)

**Gilt für:** Paket Verbrauch, &bullet; **unterstützte Versionen** werden veröffentlicht: alle

Zeigt eine Liste von Paketen aus einer angegebenen Quelle an. Wenn keine Quellen angegeben werden, werden alle Quellen verwendet, die in der globalen `%AppData%\NuGet\NuGet.Config` Konfigurationsdatei (Windows `~/.nuget/NuGet/NuGet.Config`) oder definiert sind. Wenn `NuGet.Config` keine Quellen angibt `list` , verwendet den Standard-Feed (nuget.org).

## <a name="usage"></a>Verwendung

```cli
nuget list [search terms] [options]
```

Gibt an, wo die optionalen Suchbegriffe die angezeigte Liste filtern. Suchbegriffe werden auf die Namen von Paketen, Tags und Paketbeschreibungen angewendet, genauso wie Sie Sie auf nuget.org verwenden.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| AllVersions | Listet alle Versionen eines Pakets auf. Standardmäßig wird nur die neueste Paketversion angezeigt. |
| ConfigFile | Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.|
| ForceEnglishOutput | *(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird. |
| Help | Zeigt Hilfe Informationen für den Befehl an. |
| IncludeDelisted | *(3.2 +)* Nicht aufgelistete Pakete anzeigen. |
| NonInteractive | Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen. |
| PreRelease | Schließt vorab Pakete in die Liste ein. |
| Source | Gibt eine Liste der zu durchsuchenden Paketquellen an. |
| Verbosity | Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
