---
title: NuGet CLI delete-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenz für den Löschbefehl nuget.exe
keywords: NuGet Verweis löschen, löschen Sie die Paket-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9445042c46ef41721def1fbbb8dcebf4afc14d1b
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="delete-command-nuget-cli"></a>Delete-Befehl (NuGet CLI)

**Gilt für:** Verpacken Sie die Publishing &bullet; **unterstützte Versionen:** alle

Löscht oder unlists ein Pakets aus der Paketquelle. Für nuget.org, den Löschbefehl [unlists das Paket](../policies/deleting-packages.md).

## <a name="usage"></a>Verwendung

```cli
nuget delete <packageID> <packageVersion> [options]
```

wobei `<packageID>` und `<packageVersion>` das genaue Paket zu löschen oder die Benutzerauswahl zu identifizieren. Das genaue Verhalten hängt von der Quelle ab. Für lokale Ordner ist z. B. das Paket gelöscht. für nuget.org ist das Paket nicht aufgeführte.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ApiKey | Die API-Schlüssel für das Zielrepository. Wenn Sie nicht vorhanden ist, wird in der Datei "App.config" angegebenen verwendet. |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| ForceEnglishOutput | *(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Quelle | Gibt die Server-URL an. Die URL für nuget.org lautet `https://api.nuget.org/v3/index.json`. Private-Feeds als Ersatz für den Hostnamen, z. B. *%hostname%/api/v3*. |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
