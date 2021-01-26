---
title: Befehl "nuget CLI Locals"
description: Referenz für den Befehl "nuget.exe Locals"
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 25feb29c7b96c47681cedd8208b8595952d3ca49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779193"
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

  Listet den Speicherort des angegebenen Ordners oder die Speicherorte aller Ordner bei Verwendung mit *allen* auf.

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
