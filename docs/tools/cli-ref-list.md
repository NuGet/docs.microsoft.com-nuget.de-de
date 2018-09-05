---
title: NuGet-CLI-Befehl "auflisten"
description: Referenz für die nuget.exe-List-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549800"
---
# <a name="list-command-nuget-cli"></a>List-Befehl (NuGet-CLI)

**Gilt für:** -paketverbrauch, Veröffentlichung &bullet; **unterstützte Versionen:** alle

Zeigt eine Liste der Pakete aus einer vorgegebenen Quelle an. Wenn keine Quellen angegeben werden, werden alle Quellen in die globale XML-Konfigurationsdatei definiert `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config`, verwendet werden. Wenn `NuGet.Config` keine Quellen, dann gibt `list` der standardfeed (nuget.org) verwendet.

## <a name="usage"></a>Verwendung

```cli
nuget list [search terms] [options]
```

die optionale Suchbegriffe werden, in der angezeigten Liste gefiltert. Suchbegriffe werden auf die Namen der Pakete, Tags und Beschreibungen von Paket angewendet, wie sie sind, wenn sie auf "NuGet.org" zu verwenden.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| AllVersions | Listen Sie aller Versionen eines Pakets an auf. Standardmäßig wird nur die aktuelle Paketversion angezeigt. |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| ForceEnglishOutput | *(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden. |
| Hilfe | Zeigt die Informationen für den Befehl Hilfe. |
| IncludeDelisted | *(3.2 und höher)*  Nicht aufgelistete Pakete anzuzeigen. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Vorabversion | Schließt Vorabversionen von Paketen in der Liste aus. |
| Quelle | Gibt eine Liste der Paketquellen zu suchen. |
| Ausführlichkeit | Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
