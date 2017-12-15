---
title: NuGet CLI delete-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: c213a07a-711d-47e0-9ee6-1d582e6cdb69
description: "Referenz für den Löschbefehl nuget.exe"
keywords: "NuGet Verweis löschen, löschen Sie die Paket-Befehl"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 92af9dc356f3932347864976496e0ba1216496c9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="delete-command-nuget-cli"></a>Delete-Befehl (NuGet CLI)

**Gilt für:** Verpacken Sie die Publishing &bullet; **unterstützte Versionen:** alle

Löscht oder unlists ein Pakets aus der Paketquelle. Für nuget.org, den Löschbefehl [unlists das Paket](../policies/Deleting-Packages.md).

## <a name="usage"></a>Verwendung

```
nuget delete <packageID> <packageVersion> [options]
```

wobei `<packageID>` und `<packageVersion>` das genaue Paket zu löschen oder die Benutzerauswahl zu identifizieren. Das genaue Verhalten hängt von der Quelle ab. Für lokale Ordner ist z. B. das Paket gelöscht. für nuget.org ist das Paket nicht aufgeführte.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| "apikey" | Die API-Schlüssel für das Zielrepository. Wenn Sie nicht vorhanden ist, der im angegebenen *%AppData%\NuGet\NuGet.Config* verwendet wird. |
| "ConfigFile" hinzu | *(2,5 +)*  Das NuGet-Konfigurationsdatei angewendet. Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird. |
| ForceEnglishOutput | *(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| Nicht interaktive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Quelle | Gibt die Server-URL an. Die URL für nuget.org lautet `https://api.nuget.org/v3/index.json`. Private-Feeds als Ersatz für den Hostnamen, z. B. *%hostname%/api/v3*. |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *detaillierte (2.5 und höher)*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
