---
title: Befehl "nuget CLI-Befehl" | tapikey
description: Referenz für den Befehl "nuget.exe".
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b84d4257c580f6e734c26ebfc589be27bea10c82
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622810"
---
# <a name="setapikey-command-nuget-cli"></a>Befehl "stapikey" (nuget-CLI)

**Gilt für:** Paket Verbrauch, &bullet; **unterstützte Versionen** werden veröffentlicht: alle

Speichert einen API-Schlüssel für eine angegebene Server-URL in `NuGet.Config` , sodass er nicht für nachfolgende Befehle eingegeben werden muss.

## <a name="usage"></a>Verwendung

```cli
nuget setapikey <key> -Source <url> [options]
```

dabei `<source>` identifiziert den Server und `<key>` den Schlüssel, der gespeichert werden soll. Wenn `<source>` weggelassen wird, wird nuget.org angenommen. 

> [!NOTE]
> Der API-Schlüssel wird nicht für die Authentifizierung mit dem privaten Feed verwendet. Informationen zum Verwalten von Anmelde Informationen für die Authentifizierung bei der Quelle finden Sie unter [ `nuget sources` Befehl](../cli-reference/cli-ref-sources.md) .
> API-Schlüssel können von den einzelnen nuget-Servern abgerufen werden. Informationen zum Erstellen und Verwalten von apikeys für nuget.org finden Sie unter "Abruf [-an-API-Schlüssel](../../nuget-org/scoped-api-keys.md#acquire-an-api-key) ".

## <a name="options"></a>Optionen

- **`-ConfigFile`**

  Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.

- **`-ForceEnglishOutput`**

  *(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.

- **`-?|-help`**

  Zeigt Hilfe Informationen für den Befehl an.

- **`-NonInteractive`**

  Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.

- **`-src|-Source`**

  Server-URL, bei der der API-Schlüssel gültig ist.

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
