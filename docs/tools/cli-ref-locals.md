---
title: NuGet-CLI-Locals-Befehl
description: Referenz für den Befehl "nuget.exe" Locals "
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 38d8b9366fb2749b77c987c950da3aa9e7f029fc
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794134"
---
# <a name="locals-command-nuget-cli"></a>Der Befehl „locals“ (NuGet-CLI)

**Gilt für:** Paket Verbrauch &bullet; **unterstützte Versionen:** 3.3 und höher

Löscht bzw. listet diese lokale NuGet-Ressourcen wie z. B. die *http-Cache*, *global-Packages* Ordner und den temporären Ordner. Die `locals` Befehl kann auch verwendet werden, um eine Liste dieser Orte anzuzeigen. Weitere Informationen finden Sie unter [Verwalten der globalen Paketordner und Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Verwendung

```cli
nuget locals <folder> [options]
```

wo `<folder>` ist einer der `all`, `http-cache`, `packages-cache` *(3.5 und früher)*, `global-packages`, `temp` *(3.4 und höher)*, und `plugins-cache` *(4.8 und höher)*.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| Clear | Löscht den angegebenen Ordner. |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| ForceEnglishOutput | *(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden. |
| Hilfe | Zeigt die Informationen für den Befehl Hilfe. |
| Liste | Listet den Speicherort des angegebenen Ordners oder auf die Speicherorte aller Ordner bei der Verwendung mit *alle*. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Ausführlichkeit | Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Weitere Beispiele finden Sie unter [Verwalten der globalen Paketordner und Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md).
