---
title: NuGet-CLI-Befehl "Hilfe" | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für den Befehl \"nuget.exe Help\""
keywords: Referenz zur Hilfe von NuGet, Befehl "Hilfe"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 97f72e1be0df6e97f8b06696b2b3861800e4ea08
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="help-or--command-nuget-cli"></a>Hilfe oder? Befehl (NuGet CLI)

**Gilt für:** alle &bullet; **unterstützten Versionen**: alle

Zeigt allgemeine Hilfe-Informationen und Hilfe-Informationen zu bestimmten Befehlen.

## <a name="usage"></a>Verwendung

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

[Befehl] identifiziert, in einen bestimmten Befehl für die Hilfe angezeigt werden sollen.

> [!Warning]
> Einige Befehle werden an laufen *Hilfe* ersten, als mit `nuget help install`, da ein Paket mit dem Namen "help" auf nuget.org vorhanden ist. Wenn Sie den Befehl geben `nuget install help`, erhalten Sie keine Hilfe zum Befehl "Install", aber das Paket mit dem Namen Hilfe wird stattdessen installieren.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| Alle | Drucken von ausführlichen Hilfeinformationen für alle verfügbaren Befehle; ignoriert, wenn Sie ein bestimmten Befehl angegeben wird. |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird. |
| ForceEnglishOutput | *(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl "Help" selbst. |
| Markdown | Drucken von ausführlichen Hilfeinformationen in Markdown-Format bei Verwendung mit `-All`. Andernfalls ignoriert. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
