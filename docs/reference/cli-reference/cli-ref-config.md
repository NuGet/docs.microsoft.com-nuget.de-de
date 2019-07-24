---
title: Befehl "nuget CLI config"
description: Referenz für den Befehl "nuget. exe config"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 384e708187a747221de103720cc51af07acf713e
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433320"
---
# <a name="config-command-nuget-cli"></a>config-Befehl (nuget-CLI)

**Gilt für:** alle &bullet; **unterstützten Versionen**: alle

Ruft nuget-Konfigurationswerte ab oder legt Sie fest. Weitere Informationen finden Sie unter [Allgemeine nuget-Konfigurationen](../../consume-packages/configuring-nuget-behavior.md). Ausführliche Informationen zu zulässigen Schlüsselnamen finden Sie in der [nuget-Konfigurationsdatei Referenz](../nuget-config-file.md).

## <a name="usage"></a>Verwendung

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

`<name>` dabeigebenSieeinSchlüssel-Wert-Paaran,dasinderKonfiguration`<value>` festgelegt werden soll. Sie können beliebig viele Paare angeben. Um einen Wert zu entfernen, geben Sie den Namen `=` und das Vorzeichen an, aber keinen Wert.

Zulässige Schlüsselnamen finden Sie in der [nuget-Konfigurationsdatei Referenz](../nuget-config-file.md).

In nuget 3.4 und `<value>` höher kann [Umgebungsvariablen](cli-ref-environment-variables.md)verwenden.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| AsPath | Gibt den Konfigurations Wert als Pfad zurück, der ignoriert `-Set` wird, wenn verwendet wird. |
| ConfigFile | Die zu ändernde nuget-Konfigurationsdatei. Wenn nichts angegeben ist, wird die Standarddatei verwendet`%AppData%\NuGet\NuGet.Config` : (Windows) `~/.config/NuGet/NuGet.Config` oder (Mac/Linux) `~/.nuget/NuGet/NuGet.Config` oder (variiert je nach Betriebssystem Verteilung).|
| ForceEnglishOutput | *(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird. |
| Help | Zeigt Hilfe Informationen für den Befehl an. |
| NonInteractive | Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen. |
| Verbosity | Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

### <a name="examples"></a>Beispiele

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
