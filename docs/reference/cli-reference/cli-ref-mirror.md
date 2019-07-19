---
title: Befehl "nuget CLI-Spiegel"
description: Referenz für den Befehl "nuget. exe"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327667"
---
# <a name="mirror-command-nuget-cli"></a>Der Befehl „mirror“ (NuGet-CLI)

**Gilt für:** &bullet; **unterstützte Versionen** der Paket Veröffentlichung: veraltet in 3.2 +

Spiegelt ein Paket und seine Abhängigkeiten aus den angegebenen quelldepots in das Zielrepository ein.

> [!NOTE]
> Wenn Sie diesen Befehl für nuget-Versionen vor 3,2 aktivieren möchten [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), klicken Sie auf, wählen Sie die neueste `Nuget-Signed.exe` stabile Version aus, und laden `Nuget-Signed.exe` Sie `nuget.exe` Sie auf Ihren lokalen Datenträger herunter `NuGet.ServerExtensions.dll` .

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
