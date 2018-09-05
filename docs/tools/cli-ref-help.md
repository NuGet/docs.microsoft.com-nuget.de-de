---
title: NuGet-CLI-Befehl "Hilfe"
description: Referenz für die nuget.exe-Help-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546562"
---
# <a name="help-or--command-nuget-cli"></a>help or ? Der Befehl (NuGet CLI)

**Gilt für:** alle &bullet; **unterstützten Versionen**: alle

Zeigt allgemeine Hilfeinformationen und Informationen zu bestimmten Befehlen helfen.

## <a name="usage"></a>Verwendung

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

[Befehl] identifiziert, in einem bestimmten Befehl für die zum Anzeigen der Hilfe.

> [!Warning]
> Einige Befehle, achten Sie an *Hilfe* zuerst mit `nuget help install`, da ein Paket mit dem Namen "help", auf nuget.org vorhanden ist. Wenn Sie den Befehl geben `nuget install help`, Sie erhalten Sie keine Hilfe zum Befehl "Install", jedoch wird stattdessen das Help-Paket installieren.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| Alle | Detaillierte Hilfe für alle verfügbaren Befehle gedruckt wird. ignoriert, wenn Sie ein bestimmten Befehl erhält. |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| ForceEnglishOutput | *(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden. |
| Hilfe | Zeigt die Hilfe zu den Hilfebefehl selbst. |
| Markdown | Drucken Sie detaillierte Hilfe im Markdown-Format bei Verwendung mit `-All`. Andernfalls ignoriert. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Ausführlichkeit | Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
