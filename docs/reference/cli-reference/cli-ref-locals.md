---
title: Befehl "nuget CLI Locals"
description: Referenz für den Befehl "nuget.exe Locals"
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: cdc2b760021ffc4a9e02edacb45beac01cc99bf1
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623057"
---
# <a name="locals-command-nuget-cli"></a>Befehl "Locals" (nuget-CLI)

**Gilt für:** &bullet; **unterstützte Versionen** von Paket Verbrauch: 3.3 und höher

Löscht lokale nuget-Ressourcen wie den Ordner " *http-Cache*", " *Global-Packages* " und den Ordner "Temp" oder listet diese auf. Der `locals` Befehl kann auch verwendet werden, um eine Liste dieser Speicherorte anzuzeigen. Weitere Informationen finden Sie unter [Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Verwendung

```cli
nuget locals <folder> [options]
```

dabei `<folder>` ist eine von `all` , `http-cache` , `packages-cache` *(3,5 und früher)*, `global-packages` , `temp` *(3.4 +)* und `plugins-cache` *(4.8 +)*.

## <a name="options"></a>Optionen

- **`-Clear`**

  Löscht den angegebenen Ordner.

- **`-ConfigFile`**

  Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.

- **`-ForceEnglishOutput`**

  *(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.

- **`-?|-help`**

  Zeigt Hilfe Informationen für den Befehl an.

- **`-List`**

  Listet den Speicherort des angegebenen Ordners oder die Speicherorte aller Ordner bei Verwendung mit *allen*auf.

- **`-NonInteractive`**

  Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Weitere Beispiele finden Sie unter [Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md).
