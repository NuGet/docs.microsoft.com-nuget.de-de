---
title: NuGet-CLI "lokal"-Befehl
description: Referenz für den nuget.exe "lokal"-Befehl
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ac07dc306bc23c2fedd33c5627e8d34a6098387c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="locals-command-nuget-cli"></a>Der Befehl „locals“ (NuGet-CLI)

**Gilt für:** Verpacken Sie Verbrauch &bullet; **unterstützte Versionen:** 3.3 +

Löscht oder lokale NuGet-Ressourcen wie z. B. Listet die *http-Cache*, *globalen Pakete* Ordner und den temporären Ordner. Die `locals` -Befehl kann außerdem verwendet werden, um eine Liste der beiden Speicherorte anzuzeigen. Weitere Informationen finden Sie unter [Verwaltung der globalen Pakete und der Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Verwendung

```cli
nuget locals <folder> [options]
```

wobei `<folder>` ist einer der `all`, `http-cache`, `packages-cache` *(3.5 und früher)*, `global-packages`, und `temp` *(3.4 +)*.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| Clear | Löscht den angegebenen Ordner. |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| ForceEnglishOutput | *(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| Liste | Listet den Speicherort des angegebenen Ordners oder der Speicherorte von allen Ordnern bei Verwendung mit *alle*. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Weitere Beispiele finden Sie unter [Verwaltung der globalen Pakete und der Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md).
