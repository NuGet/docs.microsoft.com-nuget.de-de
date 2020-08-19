---
title: Befehl "nuget CLI-Spiegel"
description: Verweis auf den Befehl nuget.exe Spiegelung
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a7247aeb21418e78dbfe9be15c2e7cd152aa3f4a
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622966"
---
# <a name="mirror-command-nuget-cli"></a>Spiegel Befehl (nuget-CLI)

**Gilt für:** &bullet; **unterstützte Versionen** der Paket Veröffentlichung: veraltet in 3.2 +

Spiegelt ein Paket und seine Abhängigkeiten aus den angegebenen quelldepots in das Zielrepository ein.

> [!NOTE]
> NuGet.ServerExtensions.dll und NuGet-Signed.exe, die diesen Befehl zuvor in nuget 2. x unterstützten (durch Umbenennen von NuGet-Signed.exe in nuget.exe), sind nicht mehr zum Herunterladen verfügbar. Wenn Sie einen ähnlichen Befehl wie diesen verwenden möchten, versuchen Sie es mit [nugetmirror](https://www.nuget.org/packages/NuGetMirror/).

## <a name="usage"></a>Verwendung

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

`<packageID>`gibt an, wo das zu spiegelnde Paket ist, oder `<configFilePath>` identifiziert die Datei, die `packages.config` die zu spiegelnden Pakete auflistet.

Der `<listUrlTarget>` gibt das Quellrepository an und `<publishUrlTarget>` gibt das Zielrepository an.

Wenn das Zielrepository auf dem ausgeführt wird, auf dem `https://machine/repo` [nuget. Server](../../hosting-packages/nuget-server.md)ausgeführt wird, werden die Listen-und pushurls `https://machine/repo/nuget` `https://machine/repo/api/v2/package` bzw.

## <a name="options"></a>Optionen

- **`-ApiKey`**

  Der API-Schlüssel für das Zielrepository. Wenn Sie nicht vorhanden ist, wird die in der Konfigurationsdatei angegebene verwendet ( `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).

- **`-Help`**

  Zeigt Hilfe Informationen für den Befehl an.

- **`-NoCache`**

  Verhindert, dass nuget zwischengespeicherte Pakete verwendet. Weitere Informationen finden Sie [unter Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-Noop`**

  Protokolliert, was geschehen würde, führt die Aktionen jedoch nicht aus. nimmt die erfolgreiche Ausführung von pushvorgängen an.

- **`-PreRelease`**

  Schließt vorab Pakete in den Spiegelungs Vorgang ein.

- **`-Source`**

  Eine Liste der zu spiegelnden Paketquellen. Wenn keine Quellen angegeben sind, werden die in der Konfigurationsdatei definierten (siehe APIKey oben) verwendet, wobei "nuget.org" verwendet wird, wenn keine Daten angegeben sind.

- **`-Timeout`**

  Gibt den Timeout Wert (in Sekunden) für das Push an einen Server an. Der Standardwert beträgt 300 Sekunden (5 Minuten).

- **`-Version`**

  Die Version des zu installierenden Pakets. Wenn nicht angegeben, wird die aktuelle Version gespiegelt.

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
