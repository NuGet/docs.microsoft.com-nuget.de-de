---
title: Befehl "nuget CLI-init"
description: Referenz für den Befehl "nuget. exe init"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327777"
---
# <a name="init-command-nuget-cli"></a>init-Befehl (nuget-CLI)

**Gilt für: von** der &bullet; Paket Erstellung **unterstützte Versionen:** 3.3+

Kopiert alle Pakete aus einem flatfolder in einen Zielordner mit einem hierarchischen Layout, wie für den [Befehl hinzufügen](cli-ref-add.md)beschrieben. Das heißt, die `init` Verwendung von entspricht der Verwendung `add` des-Befehls für jedes Paket im Ordner.

Wie bei `add`muss das Ziel entweder ein lokaler Ordner oder ein UNC-Pfad sein. HTTP-paketrepositorys wie nuget.org oder Private Server werden nicht unterstützt.

## <a name="usage"></a>Verwendung

```cli
nuget init <source> <destination> [options]
```

Dabei ist der Ordner, der die `<destination>` Pakete enthält, und ist der lokale Ordner oder UNC-Pfadname, in den die Pakete kopiert werden. `<source>`

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.|
| ForceEnglishOutput | *(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird. |
| Expand | Fügt alle Dateien in jedem Paket hinzu, das der Paketquelle hinzugefügt wird. identisch mit dem `add`Befehl. `-Expand` |
| Help | Zeigt Hilfe Informationen für den Befehl an. |
| NonInteractive | Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen. |
| Verbosity | Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
