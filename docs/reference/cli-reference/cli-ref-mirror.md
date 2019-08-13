---
title: Befehl "nuget CLI-Spiegel"
description: Referenz für den Befehl "nuget. exe"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 81866172bfbf55c42ee96c213c0117f1f986235c
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959714"
---
# <a name="mirror-command-nuget-cli"></a>Der Befehl „mirror“ (NuGet-CLI)

**Gilt für:** &bullet; **unterstützte Versionen** der Paket Veröffentlichung: veraltet in 3.2 +

Spiegelt ein Paket und seine Abhängigkeiten aus den angegebenen quelldepots in das Zielrepository ein.

> [!NOTE]
> "Nuget. Server Extensions. dll" und "NuGet-Signed. exe", die zuvor diesen Befehl in nuget 2. x unterstützten (durch Umbenennen von "NuGet-Signed. exe" in "nuget. exe"), sind nicht mehr zum Download verfügbar. Wenn Sie einen ähnlichen Befehl wie diesen verwenden möchten, versuchen Sie es mit [nugetmirror](https://www.nuget.org/packages/NuGetMirror/).

## <a name="usage"></a>Verwendung

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

gibt `<packageID>` an, wo das zu spiegelnde `<configFilePath>` Paket ist `packages.config` , oder identifiziert die Datei, die die zu spiegelnden Pakete auflistet.

Der `<listUrlTarget>` gibt das Quellrepository an und `<publishUrlTarget>` gibt das Zielrepository an.

Wenn Ihr Zielrepository auf ist `https://machine/repo` , die ausgeführt wird [NuGet.Server in](../../hosting-packages/nuget-server.md), Liste und Push-URLs `https://machine/repo/nuget` und `https://machine/repo/api/v2/package`bzw.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ApiKey | Der API-Schlüssel für das Zielrepository. Wenn Sie nicht vorhanden ist, wird die in der Konfigurationsdatei angegebene verwendet`%AppData%\NuGet\NuGet.Config` ((Windows) `~/.nuget/NuGet/NuGet.Config` oder (Mac/Linux)). |
| Help | Zeigt Hilfe Informationen für den Befehl an. |
| NoCache | Verhindert, dass nuget zwischengespeicherte Pakete verwendet. Weitere Informationen finden Sie [unter Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NOOP | Protokolliert, was geschehen würde, führt die Aktionen jedoch nicht aus. nimmt die erfolgreiche Ausführung von pushvorgängen an. |
| Vorab | Schließt vorab Pakete in den Spiegelungs Vorgang ein. |
| Source | Eine Liste der zu spiegelnden Paketquellen. Wenn keine Quellen angegeben sind, werden die in der Konfigurationsdatei definierten (siehe APIKey oben) verwendet, wobei "nuget.org" verwendet wird, wenn keine Daten angegeben sind. |
| Timeout | Gibt den Timeout Wert (in Sekunden) für das Push an einen Server an. Der Standardwert ist 300 Sekunden (5 Minuten). |
| Version | Die Version des zu installierenden Pakets. Wenn nicht angegeben, wird die aktuelle Version gespiegelt. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
