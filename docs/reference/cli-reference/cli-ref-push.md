---
title: Befehl "nuget CLI Push"
description: Referenz für den nuget.exe Push-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d53a2e7f41219e68e59b195d1d5a9d1f62ad7c63
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622844"
---
# <a name="push-command-nuget-cli"></a>Push-Befehl (nuget-CLI)

**Gilt für:** &bullet; **unterstützte Versionen** der Paket Veröffentlichung: alle; 4.1.0 + erforderlich für nuget.org

> [!Important]
> Um Pakete per Push an nuget.org zu überführen, müssen Sie nuget.exe v 4.1.0 + verwenden, das die erforderlichen [nuget-Protokolle](../../api/nuget-protocols.md)implementiert.

Überträgt ein Paket an eine Paketquelle und veröffentlicht es.

Die nuget-Standardkonfiguration wird durch Laden `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) abgerufen, und anschließend werden alle-oder-Dateien geladen, die `Nuget.Config` `.nuget\Nuget.Config` vom Stamm des Laufwerks stammen und im aktuellen Verzeichnis enden (siehe [Allgemeine nuget-Konfigurationen](../../consume-packages/configuring-nuget-behavior.md)).

## <a name="usage"></a>Verwendung

```cli
nuget push <packagePath> [options]
```

Gibt an, wo `<packagePath>` das Paket angibt, das per Push an den Server über

## <a name="options"></a>Optionen

- **`-ApiKey`**

  Der API-Schlüssel für das Zielrepository. Wenn kein Wert vorhanden ist, wird der in der Konfigurationsdatei angegebene verwendet.

- **`-ConfigFile`**

  Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.

- **`-DisableBuffering`**

  Deaktiviert die Pufferung beim Push an einen HTTP (s)-Server, um Speicher Verwendungen zu verringern. Vorsicht: Wenn diese Option verwendet wird, funktioniert die integrierte Windows-Authentifizierung möglicherweise nicht.

- **`-ForceEnglishOutput`**

  *(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.

- **`-?|-help`**

  Zeigt Hilfe Informationen für den Befehl an.

- **`-NonInteractive`**

  Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.

- **`-NoServiceEndpoint`**

  Fügt nicht `api/v2/packages` an die Quell-URL an.

- **`-NoSymbols`**

  *(3.5* und höher) Wenn ein Symbol Paket vorhanden ist, wird es nicht auf einen Symbol Server übermittelt.

- **`-src|-Source`**

  Gibt die Server-URL an. Nuget identifiziert eine UNC-oder lokale Ordner Quelle und kopiert die Datei dort, anstatt Sie per HTTP zu pushen.  Ab nuget 3.4.2 handelt es sich hierbei um einen obligatorischen Parameter, es sei denn, die `NuGet.Config` Datei gibt einen *defaultpushsource* -Wert an (Weitere Informationen finden Sie unter [Konfigurieren des nuget-Verhaltens](../../consume-packages/configuring-nuget-behavior.md)).

- **`-SkipDuplicate`**

  *(5.1 +)* Wenn ein Paket und eine Version bereits vorhanden sind, überspringen Sie es, und fahren Sie mit dem nächsten Paket im Push fort, falls vorhanden.

- **`-SymbolSource`**

  *(3.5* und höher) Gibt die Symbol Server-URL an. nuget.smbsrc.net wird beim Push an nuget.org verwendet.

- **`-SymbolApiKey`**

  *(3.5* und höher) Gibt den API-Schlüssel für die URL an, die in angegeben ist `-SymbolSource` .

- **`-Timeout`**

  Gibt den Timeout Wert (in Sekunden) für das Push an einen Server an. Der Standardwert beträgt 300 Sekunden (5 Minuten).

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .


Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
