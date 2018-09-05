---
title: NuGet-CLI-Befehl "Setapikey"
description: Referenz für die nuget.exe-Befehl "Setapikey"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549219"
---
# <a name="setapikey-command-nuget-cli"></a>Befehl "Setapikey" (NuGet-CLI)

**Gilt für:** -paketverbrauch, Veröffentlichung &bullet; **unterstützte Versionen:** alle

Speichert einen API-Schlüssel für einen bestimmten Server-URL in `NuGet.Config` so, dass er nicht für nachfolgende Befehle eingegeben werden.

## <a name="usage"></a>Verwendung

```cli
nuget setapikey <key> -Source <url> [options]
```

wo `<source>` identifiziert den Server und `<key>` ist der Schlüssel oder das Kennwort zu speichern. Wenn `<source>` wird ausgelassen, wird "NuGet.org" begonnen.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| ForceEnglishOutput | *(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden. |
| Hilfe | Zeigt die Informationen für den Befehl Hilfe. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Ausführlichkeit | Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
