---
title: NuGet-CLI-Befehl "Config"
description: Referenz für den Befehl "nuget.exe-Config"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0497c7b99a2de6bee37d6d0ead8b055578e60b7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426074"
---
# <a name="config-command-nuget-cli"></a>Befehl "Config" (NuGet-CLI)

**Gilt für:** alle &bullet; **unterstützten Versionen**: alle

Übernimmt oder bestimmt die NuGet-Konfigurationswerte. Zusätzliche Nutzung, finden Sie unter [häufig auftretenden NuGet Konfigurationen](../consume-packages/configuring-nuget-behavior.md). Ausführliche Informationen zu zulässigen Schlüsselnamen, finden Sie in der [NuGet Config-Dateiverweis](../reference/nuget-config-file.md).

## <a name="usage"></a>Verwendung

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

wo `<name>` und `<value>` Geben Sie ein Schlüssel-Wert-Paar in der Konfiguration festgelegt werden. Sie können so viele wie gewünscht angeben. Um einen Wert zu entfernen, geben Sie den Namen und die `=` anmelden, aber keinen Wert.

Zulässige Schlüsselnamen, finden Sie unter den [NuGet Config-Dateiverweis](../reference/nuget-config-file.md).

In NuGet 3.4 und höher `<value>` können [Umgebungsvariablen](cli-ref-environment-variables.md).

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| AsPath | Gibt zurück, die Konfigurationsdatei als Pfad ignoriert, wenn `-Set` verwendet wird. |
| ConfigFile | Die NuGet-Konfigurationsdatei ändern. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| ForceEnglishOutput | *(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden. |
| Help | Zeigt die Informationen für den Befehl Hilfe. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Verbosity | Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

### <a name="examples"></a>Beispiele

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
