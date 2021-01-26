---
title: Befehl "nuget-CLI"
description: Verweis auf den nuget.exe Help-Befehl
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5d91638c4a6f167ea8a04e5dfa2905cb55084ddd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779354"
---
# <a name="help-or--command-nuget-cli"></a>help or ? Befehl (nuget-CLI)

**Gilt für:** alle &bullet; **unterstützten Versionen**: alle

Zeigt allgemeine Hilfe Informationen und Hilfe Informationen zu bestimmten Befehlen an.

## <a name="usage"></a>Verwendung

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

WHERE [Command] identifiziert einen bestimmten Befehl, für den Hilfe angezeigt werden soll.

> [!Warning]
> Beachten Sie bei einigen Befehlen, dass Sie zuerst die *Hilfe* angeben, wie bei `nuget help install` , da ein Paket mit dem Namen "Help" auf nuget.org vorhanden ist. Wenn Sie den Befehl verwenden `nuget install help` , erhalten Sie keine Hilfe zum Installations Befehl, sondern installieren das Paket mit dem Namen "Help".

## <a name="options"></a>Optionen

- **`-All`**

  Ausführliche Hilfe für alle verfügbaren Befehle drucken wird ignoriert, wenn ein bestimmter Befehl angegeben wird.

- **`-ConfigFile`**

  Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.

- **`-ForceEnglishOutput`**

  *(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.

- **`-?|-help`**

  Zeigt Hilfe Informationen für den Befehl an.

- **`-Markdown`**

  Drucken Sie ausführliche Hilfe im Markdown-Format, wenn Sie mit verwendet werden `-All` . Andernfalls ignoriert.

- **`-NonInteractive`**

  Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
