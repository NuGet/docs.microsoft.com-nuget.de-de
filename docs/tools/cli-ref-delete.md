---
title: NuGet-CLI-Befehl "löschen"
description: Referenz für die nuget.exe-Delete-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 11eea6e806d7bfe364587db9c7ef8374da1819f9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548509"
---
# <a name="delete-command-nuget-cli"></a>Delete-Befehl (NuGet-CLI)

**Gilt für:** Paket veröffentlichen &bullet; **unterstützte Versionen:** alle

Löscht oder hebt dessen Auflistung auf ein Paket aus der Paketquelle. Für "nuget.org" der Delete-Befehl [hebt dessen Auflistung auf das Paket](../policies/deleting-packages.md).

## <a name="usage"></a>Verwendung

```cli
nuget delete <packageID> <packageVersion> [options]
```

wo `<packageID>` und `<packageVersion>` identifizieren Sie das genaue Paket löschen oder aus der Liste entfernen. Das genaue Verhalten hängt von der Quelle ab. Für lokale Ordner ist wird z. B. das Paket gelöscht. für "NuGet.org" für das Paket nicht aufgelistet ist.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| "Apikey" | Die API-Schlüssel für die Ziel-Repository. Wenn nicht vorhanden ist, wird angegeben, in der Konfigurationsdatei verwendet. |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| ForceEnglishOutput | *(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden. |
| Help | Zeigt die Informationen für den Befehl Hilfe. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Source | Gibt die Server-URL an. Die URL für nuget.org `https://api.nuget.org/v3/index.json`. Ersetzen Sie für private Feeds den Hostnamen ein, z. B. *%hostname%/api/v3*. |
| Verbosity | Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
