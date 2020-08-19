---
title: Befehl "nuget CLI-init"
description: Referenz für den nuget.exe init-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3b830d678a473c917b70bd46900bdb0206d3652e
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623083"
---
# <a name="init-command-nuget-cli"></a>init-Befehl (nuget-CLI)

**Gilt für: von** der Paket Erstellung &bullet; **unterstützte Versionen:** 3.3 und höher

Kopiert alle Pakete aus einem flatfolder in einen Zielordner mit einem hierarchischen Layout, wie für den [Befehl hinzufügen](cli-ref-add.md)beschrieben. Das heißt, `init` die Verwendung von entspricht der Verwendung des- `add` Befehls für jedes Paket im Ordner.

Wie bei `add` muss das Ziel entweder ein lokaler Ordner oder ein UNC-Pfad sein. HTTP-paketrepositorys wie nuget.org oder Private Server werden nicht unterstützt.

## <a name="usage"></a>Verwendung

```cli
nuget init <source> <destination> [options]
```

dabei `<source>` ist der Ordner, der die Pakete enthält `<destination>` , und ist der lokale Ordner oder UNC-Pfadname, in den die Pakete kopiert werden.

## <a name="options"></a>Optionen

- **`-ConfigFile`**

  Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.

- **`-Expand`**

  Fügt alle Dateien in jedem Paket hinzu, das der Paketquelle hinzugefügt wird. identisch `-Expand` mit dem `add` Befehl.

- **`-ForceEnglishOutput`**

  *(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.

- **`-?|-help`**

  Zeigt Hilfe Informationen für den Befehl an.

- **`-NonInteractive`**

  Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
