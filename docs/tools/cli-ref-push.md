---
title: NuGet-CLI-Push-Befehl
description: Referenz für die nuget.exe-Push-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 125671ca3f695f82bd74f8097e590c3972003e22
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548342"
---
# <a name="push-command-nuget-cli"></a>Push-Befehl (NuGet-CLI)

**Gilt für:** Paket veröffentlichen &bullet; **unterstützte Versionen:** alle; erforderlich für nuget.org 4.1.0 oder höher

> [!Important]
> Um Pakete per Push an nuget.org übertragen müssen, verwenden Sie nuget.exe Verze 4.1.0 +, die die erforderlichen implementiert [NuGet-Protokolle](../api/nuget-protocols.md).

Überträgt ein Paket auf eine Paketquelle und veröffentlicht es.

NuGet Standardkonfiguration wird abgerufen, indem `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), laden Sie dann alle `Nuget.Config` oder `.nuget\Nuget.Config` Dateien, beginnend mit Stamm des Laufwerks und endend im aktuellen Verzeichnis (finden Sie unter [konfigurieren NuGet-Verhaltens](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Verwendung

```cli
nuget push <packagePath> [options]
```

wo `<packagePath>` identifiziert das Paket an den Server mithilfe von Push übertragen.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| "Apikey" | Die API-Schlüssel für die Ziel-Repository. Wenn nicht vorhanden ist, wird angegeben, in der Konfigurationsdatei verwendet. |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| DisableBuffering | Deaktiviert die Pufferung, wenn auf einem Server HTTP(s) übertragen werden, um Arbeitsspeicher Verwendungen zu verringern. Vorsicht: Wenn diese Option verwendet wird, integrierte Windows-Authentifizierung funktioniert möglicherweise nicht. |
| ForceEnglishOutput | *(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden. |
| Help | Zeigt die Informationen für den Befehl Hilfe. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| NoSymbols | *(3.5 und höher)*  Ist ein Symbolpaket vorhanden, es wird nicht abgelegt werden auf einem Symbolserver. |
| Source | Gibt die Server-URL an. NuGet identifiziert eine UNC- oder lokaler Ordner Quelle und einfach kopiert die Datei dort mithilfe von Push übertragen sie die Verwendung von HTTP.  Ab NuGet 3.4.2, dies ist auch ein obligatorischer Parameter, wenn die `NuGet.Config` -Datei gibt eine *DefaultPushSource* Wert (finden Sie unter [Konfigurieren des NuGet-Verhaltens](../consume-packages/configuring-nuget-behavior.md)). |
| SymbolSource | *(3.5 und höher)*  Gibt an, die Symbolserver-URL; nuget.smbsrc.net wird verwendet, wenn Sie mithilfe von Push an nuget.org übertragen |
| SymbolApiKey | *(3.5 und höher)*  Gibt den API-Schlüssel an, für die URL in angegeben `-SymbolSource`. |
| Timeout | Gibt das Timeout in Sekunden für die Übertragung auf einen Server an. Der Standardwert ist 300 Sekunden (5 Minuten). |
| Ausführlichkeit | Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*. |

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
