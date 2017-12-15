---
title: NuGet-CLI "lokal"-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 7f672c7c-74c9-4296-bc27-4d47882b541c
description: "Referenz für den nuget.exe \"lokal\"-Befehl"
keywords: NuGet "lokal" Verweis "lokal"-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8cc06eedc20507e2bdd210e40c471ff551b89563
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
## <a name="locals-command-nuget-cli"></a>"lokal"-Befehl (NuGet CLI)

**Gilt für:** Verpacken Sie Verbrauch &bullet; **unterstützte Versionen:** 3.3 +

Löscht oder lokale NuGet-Ressourcen wie z. B. http-Anforderung Cache Pakete Cache und den Ordner computerweite globalen Pakete aufgelistet. Die `locals` -Befehl kann außerdem verwendet werden, um eine Liste der beiden Speicherorte anzuzeigen. Weitere Informationen finden Sie unter [Verwalten von NuGet-Cache](../consume-packages/managing-the-nuget-cache.md).

## <a name="usage"></a>Verwendung

```
nuget locals <cache> [options]
```

wobei `<cache>` ist einer der `all`, `http-cache`, `packages-cache`, `global-packages`, und `temp` *(3.4 +)*.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| Clear | Löscht den angegebenen Cache. |
| "ConfigFile" hinzu | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird. |
| ForceEnglishOutput | *(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| Liste | Listet den Speicherort des angegebenen Cache oder die Speicherorte der alle Caches, die bei Verwendung mit *alle*. |
| Nicht interaktive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```
nuget locals all -list
nuget locals http-cache -clear
```
