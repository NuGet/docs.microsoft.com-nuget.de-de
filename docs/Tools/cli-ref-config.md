---
title: NuGet-CLI-Befehl "Config" | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für den Befehl \"nuget.exe Config\""
keywords: NuGet-Config-Verweis, Befehl "Config"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 34d156a29207122bac3c21c3307cbe7373b5f031
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="config-command-nuget-cli"></a>Befehl "Config" (NuGet CLI)

**Gilt für:** alle &bullet; **unterstützten Versionen**: alle

Ruft ab, oder legt ihn fest NuGet Konfigurationswerte. Zusätzliche Nutzung, finden Sie unter [Konfigurieren von NuGet-Verhalten](../consume-packages/configuring-nuget-behavior.md). Ausführliche Informationen zu zulässigen Schlüsselnamen, finden Sie in der [NuGet-Config-Dateiverweis](../reference/nuget-config-file.md).

## <a name="usage"></a>Verwendung

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

wobei `<name>` und `<value>` Geben Sie ein Schlüssel-Wert-Paar in der Konfiguration festgelegt werden. Sie können nach Bedarf beliebig viele Paare angeben. Um einen Wert zu entfernen, geben Sie den Namen und die `=` anmelden, aber keinen Wert.

Zulässige Schlüsselnamen, finden Sie unter der [NuGet-Config-Dateiverweis](../reference/nuget-config-file.md).

Im NuGet 3.4 + `<value>` können [Umgebungsvariablen](cli-ref-environment-variables.md).

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| AsPath | Config-Datei der Wert als ein Pfad Gibt ignoriert, wenn `-Set` verwendet wird. |
| ConfigFile | Die NuGet-Konfigurationsdatei zu ändern. Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird. |
| ForceEnglishOutput | *(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

### <a name="examples"></a>Beispiele

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
