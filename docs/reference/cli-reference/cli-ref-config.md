---
title: Befehl "nuget CLI config"
description: Referenz für den Befehl "nuget.exe config"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7d0c1c51f40cba9a5b69f209ffbd995451bfeb9f
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622875"
---
# <a name="config-command-nuget-cli"></a>config-Befehl (nuget-CLI)

**Gilt für:** alle &bullet; **unterstützten Versionen**: alle

Ruft nuget-Konfigurationswerte ab oder legt Sie fest. Weitere Informationen finden Sie unter [Allgemeine nuget-Konfigurationen](../../consume-packages/configuring-nuget-behavior.md). Ausführliche Informationen zu zulässigen Schlüsselnamen finden Sie in der [nuget-Konfigurationsdatei Referenz](../nuget-config-file.md).

## <a name="usage"></a>Verwendung

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

`<name>` `<value>` dabei geben Sie ein Schlüssel-Wert-Paar an, das in der Konfiguration festgelegt werden soll. Sie können beliebig viele Paare angeben. Um einen Wert zu entfernen, geben Sie den Namen und das Vorzeichen an, `=` aber keinen Wert.

Zulässige Schlüsselnamen finden Sie in der [nuget-Konfigurationsdatei Referenz](../nuget-config-file.md).

In nuget 3.4 und höher `<value>` kann [Umgebungsvariablen](cli-ref-environment-variables.md)verwenden.

## <a name="options"></a>Optionen


- **`AsPath`**

  Gibt den Konfigurations Wert als Pfad zurück, der ignoriert `-Set` wird, wenn verwendet wird.

- **`-ConfigFile`**

  Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.

- **`-ForceEnglishOutput`**

  *(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.

- **`-?|-help`**

  Zeigt Hilfe Informationen für den Befehl an.

- **`-NonInteractive`**

  Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.

- **`-Set`**

  Eine für mehr Schlüssel-Wert-Paare, die in der Konfiguration festgelegt werden sollen.

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

### <a name="examples"></a>Beispiele

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
