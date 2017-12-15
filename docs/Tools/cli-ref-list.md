---
title: NuGet CLI auflisten (Befehl) | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: "Referenz für den nuget.exe List-Befehl"
keywords: NuGet-Liste Verweis Pakete auflisten (Befehl)
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a>Auflisten (Befehl) (NuGet CLI)

**Gilt für:** Paket Verbrauchs, Veröffentlichung &bullet; **unterstützte Versionen:** alle

Zeigt eine Liste der Pakete aus einer bestimmten Quelle an. Wenn keine Datenquellen angegeben sind, alle Datenquellen definiert, in der Konfigurationsdatei des globalen `%AppData%\NuGet\NuGet.Config`, verwendet werden. Wenn `NuGet.Config` gibt keine Quellen `list` den Standard-Feed (nuget.org) verwendet.

## <a name="usage"></a>Verwendung

```
nuget list [search terms] [options]
```

die optionale Suchbegriffe werden, in dem die angezeigte Liste herausgefiltert. Suchbegriffe werden auf die Namen der Pakete, Tags und Beschreibungen des Pakets angewendet.

## <a name="options"></a>Optionen
| Option | Beschreibung |
| --- | --- |
| AllVersions | Listen Sie aller Versionen eines Pakets an auf. Standardmäßig wird nur die neueste Paketversion angezeigt. |
| "ConfigFile" hinzu | *(2,5 +)*  Das NuGet-Konfigurationsdatei angewendet. Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird. |
| ForceEnglishOutput | *(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| IncludeDelisted | *(3.2 +)*  Nicht aufgelistete Pakete angezeigt. |
| Nicht interaktive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Vorabversion | Enthält Vorabversionen von Paketen in der Liste an. |
| Quelle | Gibt eine Liste der Pakete Quellen zu suchen. |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *detaillierte (2.5 und höher)*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
