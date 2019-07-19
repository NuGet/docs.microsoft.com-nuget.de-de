---
title: Befehl "nuget-CLI"
description: Verweis auf den Hilfe Befehl "nuget. exe"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327797"
---
# <a name="help-or--command-nuget-cli"></a>help or ? Der Befehl (NuGet CLI)

**Gilt für:** alle &bullet; **unterstützten Versionen**: alle

Zeigt allgemeine Hilfe Informationen und Hilfe Informationen zu bestimmten Befehlen an.

## <a name="usage"></a>Verwendung

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

WHERE [Command] identifiziert einen bestimmten Befehl, für den Hilfe angezeigt werden soll.

> [!Warning]
> Beachten Sie bei einigen Befehlen, dass Sie zuerst die *Hilfe* angeben, `nuget help install`wie bei, da ein Paket mit dem Namen "Help" auf nuget.org vorhanden ist. Wenn Sie den Befehl `nuget install help`verwenden, erhalten Sie keine Hilfe zum Installations Befehl, sondern installieren das Paket mit dem Namen "Help".

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| All | Ausführliche Hilfe für alle verfügbaren Befehle drucken wird ignoriert, wenn ein bestimmter Befehl angegeben wird. |
| ConfigFile | Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.|
| ForceEnglishOutput | *(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird. |
| Help | Zeigt Hilfe Informationen für den Befehl "Hilfe" an. |
| Markdown | Drucken Sie ausführliche Hilfe im Markdown-Format, `-All`Wenn Sie mit verwendet werden. Andernfalls ignoriert. |
| NonInteractive | Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen. |
| Verbosity | Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
