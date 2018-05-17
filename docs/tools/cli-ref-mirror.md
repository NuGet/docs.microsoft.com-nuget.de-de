---
title: NuGet-CLI-Spiegel-Befehl
description: Referenz für den nuget.exe Mirror-Befehl
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5ba13196d385abf42a5af2faa3fe6f0e80fb59d8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="mirror-command-nuget-cli"></a>Der Befehl „mirror“ (NuGet-CLI)

**Gilt für:** Verpacken Sie die Publishing &bullet; **unterstützte Versionen:** in 3.2 + veraltet

Spiegelt ein Paket und seine Abhängigkeiten aus dem angegebenen quellrepositorys im Ziel-Repository.

> [!NOTE]
> Um diesen Befehl für NuGet-Versionen vor 3.2 zu aktivieren, wechseln Sie zu [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), wählen Sie die neueste stabile Version, zum Downloadpfad `NuGet.ServerExtensions.dll` und `Nuget-Signed.exe` auf Ihre lokale Festplatte und Rename `Nuget-Signed.exe` auf `nuget.exe`.

## <a name="usage"></a>Verwendung

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

auf dem `<packageID>` ist das Paket zum Spiegeln von, oder `<configFilePath>` identifiziert die `packages.config` Datei, die Pakete zum Spiegeln von aufgeführt.

Die `<listUrlTarget>` gibt an, das Quellrepository und `<publishUrlTarget>` gibt an, die Ziel-Repository.

Wenn Ihr Zielrepository auf ist `https://machine/repo` , die ausgeführt wird [NuGet.Server in](../hosting-packages/nuget-server.md), Liste und Push-URLs `https://machine/repo/nuget` und `https://machine/repo/api/v2/package`bzw.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| "apikey" | Die API-Schlüssel für das Zielrepository. Wenn Sie nicht vorhanden ist, in der Datei "App.config" angegebenen verwendet wird (`%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)). |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| NoCache | Verhindert, dass NuGet zwischengespeicherten Pakete verwenden. Finden Sie unter [Verwaltung der globalen Pakete und der Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NOOP | Protokolliert, was erfolgt, führt jedoch die Aktionen; geht davon aus Erfolg für Push-Vorgänge. |
| Vorabversion | Schließt Vorabversionen von Paketen, in dem Spiegelungsvorgang. |
| Quelle | Eine Liste der Paketquellen zu spiegeln. Wenn keine Datenquellen angegeben sind, definiert die der Datei "App.config" (siehe "apikey" oben) verwendet werden, direktionales nuget.org keine Parameter angegeben. |
| Timeout | Gibt das Timeout in Sekunden für die auf einem Server übertragen. Der Standardwert ist 300 Sekunden (5 Minuten). |
| Version | Die Version des zu installierenden Pakets an. Wenn nicht angegeben, wird die neueste Version gespiegelt. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
