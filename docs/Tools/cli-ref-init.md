---
title: NuGet-CLI-Init-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d413e4f3-1b41-4a92-8df8-87d21b542bd3
description: "Referenz für den nuget.exe Init-Befehl"
keywords: NuGet-Init-Verweis, Init-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f63a3cbcca1aeff02995f23afd217c76e534b3be
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="init-command-nuget-cli"></a>Init-Befehl (NuGet CLI)

**Gilt für:** Erstellen von Paketen &bullet; **unterstützte Versionen:** 3.3 +

Kopiert alle Pakete aus einem Ordner in einen Zielordner mithilfe hierarchischen Anordnung dargestellt, wie beschrieben für die [hinzufügen (Befehl)](#add) oben. D. h. `init` entspricht der `add` Befehl jedes Paket im Ordner "".

Wie bei `add`, das Ziel muss entweder einen lokalen Ordner oder eine UNC-Pfad sein. HTTP-Paket-Repositorys, z. B. nuget.org oder privaten Servern werden nicht unterstützt.

## <a name="usage"></a>Verwendung

```
nuget init <source> <destination> [options]
```

auf dem `<source>` ist der Ordner mit Paketen und `<destination>` ist der lokale Ordner oder ein UNC-Pfadnamen, der die Pakete werden kopiert.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| "ConfigFile" hinzu | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird. |
| ForceEnglishOutput | *(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Expand | Fügt alle Dateien in den einzelnen Paketen, die für die Paketquelle hinzugefügt wird; identisch mit `-Expand` mit der `add` Befehl. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| Nicht interaktive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *detaillierte (2.5 und höher)*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
