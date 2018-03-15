---
title: NuGet-CLI-Spiegel-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für den nuget.exe Mirror-Befehl"
keywords: NuGet-Spiegel-Verweis, Mirror-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0c1969cc04b2e2cead5e9dadf9739fdabdf65f6c
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="mirror-command-nuget-cli"></a>Mirror-Befehl (NuGet CLI)

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
| ApiKey | Die API-Schlüssel für das Zielrepository. Wenn Sie nicht vorhanden ist, in der Datei "App.config" angegebenen verwendet wird (`%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)). |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| NoCache | Verhindert, dass NuGet Pakete aus lokalen Caches. |
| NOOP | Protokolliert, was erfolgt, führt jedoch die Aktionen; geht davon aus Erfolg für Push-Vorgänge. |
| PreRelease | Schließt Vorabversionen von Paketen, in dem Spiegelungsvorgang. |
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
