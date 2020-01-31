---
title: Befehl "nuget CLI List"
description: Referenz für den Befehl "nuget. exe list"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813337"
---
# <a name="list-command-nuget-cli"></a>List-Befehl (nuget-CLI)

**Gilt für:** Paket Verbrauch, Veröffentlichung &bullet; **unterstützten Versionen:** alle

Zeigt eine Liste von Paketen aus einer angegebenen Quelle an. Wenn keine Quellen angegeben werden, werden alle Quellen verwendet, die in der globalen Konfigurationsdatei (`%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config`definiert sind. Wenn `NuGet.Config` keine Quellen angibt, verwendet `list` den Standard Feed (nuget.org).

## <a name="usage"></a>Verwendungs-

```cli
nuget list [search terms] [options]
```

Gibt an, wo die optionalen Suchbegriffe die angezeigte Liste filtern. Suchbegriffe werden auf die Namen von Paketen, Tags und Paketbeschreibungen angewendet, genauso wie Sie Sie auf nuget.org verwenden.

## <a name="options"></a>Options

| -Option | Beschreibung |
| --- | --- |
| AllVersions | Listet alle Versionen eines Pakets auf. Standardmäßig wird nur die neueste Paketversion angezeigt. |
| ConfigFile | Die anzuwendende nuget-Konfigurationsdatei. Wenn nicht angegeben, wird `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet.|
| ForceEnglishOutput | *(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird. |
| Hilfe | Zeigt Hilfe Informationen für den Befehl an. |
| IncludeDelisted | *(3.2 +)* Nicht aufgelistete Pakete anzeigen. |
| NonInteractive | Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen. |
| PreRelease | Schließt vorab Pakete in die Liste ein. |
| Quelle | Gibt eine Liste der zu durchsuchenden Paketquellen an. |
| Ausführlichkeit | Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

Auflisten aller Pakete aus konfigurierten Feeds:
```
nuget list
```
Auflisten von Azure-bezogenen Paketen mit detaillierter Ausführlichkeit:
```
nuget list Azure -Verbosity detailed
```
Auflisten aller Versionen von Azure-bezogenen Paketen aus konfigurierten Feeds:
```
nuget list Azure -AllVersions
```
Listet alle Versionen von JSON-bezogenen Paketen aus der angegebenen Quelle bzw. dem Feed auf:
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
Auflisten von JSON-bezogenen Paketen aus mehreren Quellen/Feeds:
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

