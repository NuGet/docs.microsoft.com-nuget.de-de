---
title: NuGet CLI auflisten (Befehl)
description: Referenz für den nuget.exe List-Befehl
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4a44c70937e7cb49e472c53e9857e9f44d269f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="list-command-nuget-cli"></a>Auflisten (Befehl) (NuGet CLI)

**Gilt für:** Paket Verbrauchs, Veröffentlichung &bullet; **unterstützte Versionen:** alle

Zeigt eine Liste der Pakete aus einer bestimmten Quelle an. Wenn keine Datenquellen angegeben sind, alle Datenquellen definiert, in der Konfigurationsdatei des globalen `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config`, verwendet werden. Wenn `NuGet.Config` gibt keine Quellen `list` den Standard-Feed (nuget.org) verwendet.

## <a name="usage"></a>Verwendung

```cli
nuget list [search terms] [options]
```

die optionale Suchbegriffe werden, in dem die angezeigte Liste herausgefiltert. Suchbegriffe werden auf die Namen der Pakete, Tags und Beschreibungen Paket angewendet werden, wie bei ihrer auf nuget.org Verwendung.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| AllVersions | Listen Sie aller Versionen eines Pakets an auf. Standardmäßig wird nur die neueste Paketversion angezeigt. |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| ForceEnglishOutput | *(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| IncludeDelisted | *(3.2 +)*  Nicht aufgelistete Pakete angezeigt. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Vorabversion | Enthält Vorabversionen von Paketen in der Liste an. |
| Quelle | Gibt eine Liste der Pakete Quellen zu suchen. |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
