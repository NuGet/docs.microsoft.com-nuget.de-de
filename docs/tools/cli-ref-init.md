---
title: NuGet-CLI-Init-Befehl
description: Referenz für die nuget.exe-Init-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551409"
---
# <a name="init-command-nuget-cli"></a>Init-Befehl (NuGet-CLI)

**Gilt für:** paketerstellung &bullet; **unterstützte Versionen:** 3.3 und höher

Kopiert alle Pakete von einem Ordner in einen Zielordner mithilfe hierarchischen Anordnung, wie beschrieben für die [Befehl "hinzufügen"](cli-ref-add.md). D. h. `init` ist äquivalent zur Verwendung der `add` Befehl jedes Paket im Ordner "".

Wie bei `add`, das Ziel muss entweder einen lokalen Ordner oder einen UNC-Pfad sein. HTTP-Package-Repositorys wie nuget.org oder privater Server werden nicht unterstützt.

## <a name="usage"></a>Verwendung

```cli
nuget init <source> <destination> [options]
```

wo `<source>` ist der Paketordner und `<destination>` ist der lokale Ordner oder eine UNC-Pfadnamen, der die Pakete kopiert werden.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| ForceEnglishOutput | *(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden. |
| Expand | Fügt alle Dateien in jedem Paket, das die Paketquelle hinzugefügt wird; identisch mit `-Expand` mit der `add` Befehl. |
| Hilfe | Zeigt die Informationen für den Befehl Hilfe. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Ausführlichkeit | Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
