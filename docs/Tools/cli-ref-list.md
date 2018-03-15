---
title: NuGet CLI auflisten (Befehl) | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für den nuget.exe List-Befehl"
keywords: NuGet-Liste Verweis Pakete auflisten (Befehl)
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7e0945b9e64a15a839f62bde0a0ef8f3d83335d4
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
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
| PreRelease | Enthält Vorabversionen von Paketen in der Liste an. |
| Quelle | Gibt eine Liste der Pakete Quellen zu suchen. |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
