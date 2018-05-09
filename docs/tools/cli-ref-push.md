---
title: NuGet-CLI-Push-Befehl
description: Referenz für den nuget.exe Push-Befehl
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 959b539fc20bc47f38946cb660375a6652582a0d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="push-command-nuget-cli"></a>Push-Befehl (NuGet CLI)

**Gilt für:** Verpacken Sie die Publishing &bullet; **unterstützte Versionen:** alle; erforderlich für nuget.org 4.1.0+

> [!Important]
> Pakete zum nuget.org betätigen verwenden Sie nuget.exe v4.1.0 und höher, die die erforderlichen implementiert [NuGet-Protokolle](../api/nuget-protocols.md).

Es wird ein Paket an eine Paketquelle und veröffentlicht sie.

NuGet Standardkonfiguration erhalten, indem Sie das Laden `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), laden Sie dann alle `Nuget.Config` oder `.nuget\Nuget.Config` Dateien ausgehend vom Stamm des Laufwerks und endet im aktuellen Verzeichnis (finden Sie unter [konfigurieren NuGet-Verhalten](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Verwendung

```cli
nuget push <packagePath> [options]
```

wobei `<packagePath>` identifiziert das Paket mithilfe von Push an den Server übertragen.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| "apikey" | Die API-Schlüssel für das Zielrepository. Wenn Sie nicht vorhanden ist, wird in der Datei "App.config" angegebenen verwendet. |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| DisableBuffering | Deaktiviert die Pufferung, wenn an einem HTTP-/HTTPS-Server per Push übertragen, um Arbeitsspeicher Verwendungen zu verringern. Vorsicht: Wenn diese Option verwendet wird, integrierte Windows-Authentifizierung funktionieren möglicherweise nicht. |
| ForceEnglishOutput | *(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| NoSymbols | *(3.5 +)*  Ist ein Symbolpaket vorhanden, er wird nicht abgelegt werden an einen anderen Symbolserver. |
| Quelle | Gibt die Server-URL an. NuGet gibt einen UNC- oder lokalen Ordner Quelle und einfach die Datei statt Programmstapel abzulegen HTTP mit kopiert.  Darüber hinaus starting mit NuGet 3.4.2 ist dies ein erforderlicher Parameter, wenn der `NuGet.Config` Datei gibt eine *DefaultPushSource* Wert (finden Sie unter [NuGet Konfigurieren von Verhalten](../consume-packages/configuring-nuget-behavior.md)). |
| SymbolSource | *(3.5 +)*  Gibt die Symbol-URL, bei dem nuget.smbsrc.net wird verwendet, wenn an nuget.org per Push übertragen |
| SymbolApiKey | *(3.5 +)*  Gibt den API-Schlüssel an, für die URL im angegebenen `-SymbolSource`. |
| Timeout | Gibt das Timeout in Sekunden für die auf einem Server übertragen. Der Standardwert ist 300 Sekunden (5 Minuten). |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*. |

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

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
