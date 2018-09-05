---
title: NuGet-CLI-Spiegel-Befehl
description: Referenz für die nuget.exe-Spiegel-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550205"
---
# <a name="mirror-command-nuget-cli"></a>Der Befehl „mirror“ (NuGet-CLI)

**Gilt für:** Paket veröffentlichen &bullet; **unterstützte Versionen:** in 3.2 und höher als veraltet markiert

Spiegelt ein Paket und dessen Abhängigkeiten aus den Repositorys für die angegebene Quelle zum Ziel-Repository.

> [!NOTE]
> Um diesen Befehl für NuGet-Versionen vor 3.2 zu aktivieren, wechseln Sie zu [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), wählen Sie das neueste stabile Release, zum Downloadpfad `NuGet.ServerExtensions.dll` und `Nuget-Signed.exe` auf Ihrem lokalen Datenträger und benennen Sie `Nuget-Signed.exe` zu `nuget.exe`.

## <a name="usage"></a>Verwendung

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

in denen `<packageID>` ist das Paket zu spiegeln, oder `<configFilePath>` identifiziert die `packages.config` Datei, die die Pakete, spiegeln auflistet.

Die `<listUrlTarget>` gibt an, das Quell-Repository und `<publishUrlTarget>` gibt an, die Ziel-Repository.

Wenn Ihr Zielrepository auf ist `https://machine/repo` , die ausgeführt wird [NuGet.Server in](../hosting-packages/nuget-server.md), Liste und Push-URLs `https://machine/repo/nuget` und `https://machine/repo/api/v2/package`bzw.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| "Apikey" | Die API-Schlüssel für die Ziel-Repository. Wenn nicht vorhanden ist, angegeben in der Konfigurationsdatei verwendet wird (`%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)). |
| Hilfe | Zeigt die Informationen für den Befehl Hilfe. |
| NoCache | Verhindert, dass NuGet zwischengespeicherte Pakete verwenden. Finden Sie unter [Verwalten der globalen Paketordner und Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NOOP | Protokolliert, was geschehen, jedoch nicht die Aktionen ausgeführt wird; geht davon aus Erfolg für Push-Vorgänge. |
| Vorabversion | Schließt Vorabversionen von Paketen in der datenbankspiegelungs-Vorgang an. |
| Quelle | Eine Liste der Paketquellen zu spiegeln. Wenn keine Quellen angegeben werden, die definiert, die Config-Datei (siehe "apikey" oben) verwendet werden, standardmäßig auf nuget.org, wenn keine angegeben werden. |
| Timeout | Gibt das Timeout in Sekunden für die Übertragung auf einen Server an. Der Standardwert ist 300 Sekunden (5 Minuten). |
| Version | Die Version des zu installierenden Pakets an. Wenn nicht angegeben, wird die neueste Version gespiegelt. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
