---
title: Befehl "nuget CLI-Spezifikation"
description: Referenz für den nuget.exe spec-Befehl
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b7780ee5d2e722da5e1623f44709059dd9aa3d45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779146"
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
