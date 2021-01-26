---
title: Befehl "nuget CLI Delete"
description: Verweis auf den nuget.exe DELETE-Befehl
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 96c75366ae69b34f5cd1f55feb53087b5d0ea324
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775955"
---
# <a name="delete-command-nuget-cli"></a>DELETE-Befehl (nuget-CLI)

**Gilt für:** &bullet; **unterstützte Versionen** der Paket Veröffentlichung: alle

Löscht ein Paket aus einer Paketquelle oder hebt die Auflistung auf. Bei nuget.org wird das Paket durch den DELETE-Befehl [nicht mehr aufgelistet](../../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Verwendung

```cli
nuget delete <packageID> <packageVersion> [options]
```

dabei `<packageID>` `<packageVersion>` identifizieren Sie das genaue Paket, das gelöscht oder die Auflistung der Auflistung entfernt werden soll. Das genaue Verhalten hängt von der Quelle ab. Für lokale Ordner wird das Paket beispielsweise gelöscht. für nuget.org wird das Paket nicht aufgelistet.

## <a name="options"></a>Optionen

- **`-ApiKey`**

  Der API-Schlüssel für das Zielrepository. Wenn kein Wert vorhanden ist, wird der in der Konfigurationsdatei angegebene verwendet.

- **`-ConfigFile`**

  Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.

- **`-ForceEnglishOutput`**

  *(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.

- **`-?|-help`**

  Zeigt Hilfe Informationen für den Befehl an.

- **`-NonInteractive`**

  Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.

 - **`-np|-NoPrompt`**

   Beim Löschen nicht auffordern.

 - **`-NoServiceEndpoint`** Fügt "API/v2/Packages" nicht an die Quell-URL an.

- **`-src|-Source`**

  Gibt die Server-URL an. Die URL für nuget.org ist `https://api.nuget.org/v3/index.json` . Ersetzen Sie für private Feeds den Hostnamen, z. b. " *% Hostname%/API/v3*".

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
