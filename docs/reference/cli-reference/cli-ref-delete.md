---
title: Befehl "nuget CLI Delete"
description: Referenz für den Befehl "nuget. exe Delete"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327837"
---
# <a name="delete-command-nuget-cli"></a>DELETE-Befehl (nuget-CLI)

**Gilt für:** &bullet; **unterstützte Versionen** der Paket Veröffentlichung: alle

Löscht ein Paket aus einer Paketquelle oder hebt die Auflistung auf. Bei nuget.org wird das Paket durch den DELETE-Befehl [nicht mehr aufgelistet](../../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Verwendung

```cli
nuget delete <packageID> <packageVersion> [options]
```

`<packageID>` dabeiidentifizierenSiedasgenauePaket,dasgelöschtoderdieAuflistungder`<packageVersion>` Auflistung entfernt werden soll. Das genaue Verhalten hängt von der Quelle ab. Für lokale Ordner wird das Paket beispielsweise gelöscht. für nuget.org wird das Paket nicht aufgelistet.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ApiKey | Der API-Schlüssel für das Zielrepository. Wenn kein Wert vorhanden ist, wird der in der Konfigurationsdatei angegebene verwendet. |
| ConfigFile | Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.|
| ForceEnglishOutput | *(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird. |
| Help | Zeigt Hilfe Informationen für den Befehl an. |
| NonInteractive | Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen. |
| Source | Gibt die Server-URL an. Die URL für nuget.org ist `https://api.nuget.org/v3/index.json`. Ersetzen Sie für private Feeds den Hostnamen, z. b. " *% Hostname%/API/v3*". |
| Verbosity | Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
