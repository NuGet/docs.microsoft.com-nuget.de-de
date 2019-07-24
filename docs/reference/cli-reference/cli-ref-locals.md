---
title: Befehl "nuget CLI Locals"
description: Referenz für den lokalen Befehl "nuget. exe"
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327807"
---
# <a name="locals-command-nuget-cli"></a>Der Befehl „locals“ (NuGet-CLI)

**Gilt für:** &bullet; **unterstützte Versionen** : 3.3+

Löscht lokale nuget-Ressourcen wie den Ordner " *http-Cache*", " *Global-Packages* " und den Ordner "Temp" oder listet diese auf. Der `locals` Befehl kann auch verwendet werden, um eine Liste dieser Speicherorte anzuzeigen. Weitere Informationen finden Sie unter [Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Verwendung

```cli
nuget locals <folder> [options]
```

`all` `http-cache` `global-packages` `temp` `plugins-cache`   dabei ist eine von,, `packages-cache` (3,5 und früher),, (3.4 +) und (4.8 +). `<folder>`

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| Clear | Löscht den angegebenen Ordner. |
| ConfigFile | Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.|
| ForceEnglishOutput | *(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird. |
| Help | Zeigt Hilfe Informationen für den Befehl an. |
| Liste | Listet den Speicherort des angegebenen Ordners oder die Speicherorte aller Ordner bei Verwendung mit *allen*auf. |
| NonInteractive | Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen. |
| Verbosity | Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Weitere Beispiele finden Sie unter [Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md).
