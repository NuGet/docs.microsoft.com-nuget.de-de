---
title: Befehl "nuget CLI-Spezifikation"
description: Referenz für den nuget.exe spec-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17603fa30a75c7906f867c96c5d77f31732eaa59
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622563"
---
# <a name="spec-command-nuget-cli"></a>spec-Befehl (nuget-CLI)

**Gilt für: von** der Paket Erstellung &bullet; **unterstützte Versionen:** alle

Generiert eine `.nuspec` Datei für ein neues Paket. Wenn Sie im selben Ordner wie eine Projektdatei ( `.csproj` , `.vbproj` ,) ausgeführt `.fsproj` wird, `spec` erstellt eine Tokendatei `.nuspec` . Weitere Informationen finden Sie unter [Erstellen eines Pakets](../../create-packages/creating-a-package.md).

## <a name="usage"></a>Verwendung

```cli
nuget spec [<packageID>] [options]
```

`<packageID>`dabei ist ein optionaler Paket Bezeichner, der in der Datei gespeichert werden soll `.nuspec` .

## <a name="options"></a>Optionen

- **`-AssemblyPath`**

  Gibt den Pfad zu der Assembly an, die für Metadaten verwendet werden soll.

- **`-Force`**

  Überschreibt eine vorhandene `.nuspec` Datei.


- **`-ForceEnglishOutput`**

  *(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.

- **`-?|-help`**

  Zeigt Hilfe Informationen für den Befehl an.

- **`-NonInteractive`**

  Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
