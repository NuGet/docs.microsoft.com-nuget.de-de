---
title: Befehl "nuget CLI-Befehl" | tapikey
description: Referenz für den Befehl "nuget. exe" "".
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383968"
---
# <a name="setapikey-command-nuget-cli"></a>Befehl "stapikey" (nuget-CLI)

**Gilt für:** Paket Verbrauch, Veröffentlichung &bullet; **unterstützten Versionen:** alle

Speichert einen API-Schlüssel für eine angegebene Server-URL in `NuGet.Config`, sodass er nicht für nachfolgende Befehle eingegeben werden muss.

## <a name="usage"></a>Verwendungs-

```cli
nuget setapikey <key> -Source <url> [options]
```

Dabei identifiziert `<source>` den Server, und `<key>` ist der Schlüssel oder das Kennwort, das gespeichert werden soll. Wenn `<source>` weggelassen wird, wird nuget.org angenommen.

> [!NOTE]
> Der API-Schlüssel wird nicht für die Authentifizierung mit dem privaten Feed verwendet. Informationen zum Verwalten von Anmelde Informationen für die Authentifizierung bei der Quelle finden Sie unter [`nuget sources`-Befehl](../cli-reference/cli-ref-sources.md) .

## <a name="options"></a>Options

| -Option | Beschreibung |
| --- | --- |
| ConfigFile | Die anzuwendende nuget-Konfigurationsdatei. Wenn nicht angegeben, wird `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet.|
| ForceEnglishOutput | *(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird. |
| Hilfe | Zeigt Hilfe Informationen für den Befehl an. |
| NonInteractive | Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen. |
| Ausführlichkeit | Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
