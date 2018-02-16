---
title: NuGet-CLI-Push-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für den nuget.exe Push-Befehl"
keywords: Befehl "Push"-NuGet-Push Verweis
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: df8ef42f650a20b92a281fff3e597ac8d484544e
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/14/2018
---
# <a name="push-command-nuget-cli"></a>Push-Befehl (NuGet CLI)

**Gilt für:** Verpacken Sie die Publishing &bullet; **unterstützte Versionen:** alle; erforderlich für nuget.org 4.1.0+

> [!Important]
> Pakete zum nuget.org betätigen verwenden Sie nuget.exe v4.1.0 und höher, die die erforderlichen implementiert [NuGet-Protokolle](../api/nuget-protocols.md).

Es wird ein Paket an eine Paketquelle und veröffentlicht sie.

NuGet Standardkonfiguration erhalten, indem Sie das Laden `%AppData%\NuGet\NuGet.Config`, und klicken Sie dann alle laden `Nuget.Config` oder `.nuget\Nuget.Config` Dateien ausgehend vom Stamm des Laufwerks und endet im aktuellen Verzeichnis (finden Sie unter [Konfigurieren von NuGet-Verhalten](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Verwendung

```cli
nuget push <packagePath> [options]
```

wobei `<packagePath>` identifiziert das Paket mithilfe von Push an den Server übertragen.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ApiKey | Die API-Schlüssel für das Zielrepository. Wenn Sie nicht vorhanden ist, der im angegebenen *%AppData%\NuGet\NuGet.Config* verwendet wird. |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird. |
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
