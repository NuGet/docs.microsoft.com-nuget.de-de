---
title: Befehl "nuget CLI-Befehl"
description: Verweis für den nuget.exe Befehl "hinzufügen"
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 096d2f7a61a3c861ce2084368500ab8e8b21f212
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776088"
---
# <a name="add-command-nuget-cli"></a>Befehl "hinzufügen" (nuget-CLI)

**Gilt für**: &bullet; **unterstützte Versionen** der Paket Veröffentlichung: 3.3 und höher

Fügt ein angegebenes Paket zu einer nicht-http-Paketquelle (Ordner oder UNC-Pfad) in einem hierarchischen Layout hinzu, in dem Ordner für die Paket-ID und die Versionsnummer erstellt werden. Zum Beispiel:

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

Beim Wiederherstellen oder Aktualisieren der Paketquelle bietet Hierarchisches Layout eine deutlich bessere Leistung.

Um alle Dateien im Paket auf die Ziel Paketquelle zu erweitern, verwenden Sie den- `-Expand` Schalter. Dies führt in der Regel dazu, dass zusätzliche Unterordner im Ziel angezeigt werden, z `tools` `lib` . b. und.

## <a name="usage"></a>Verwendung

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

dabei `<packagePath>` steht für den Pfadnamen des Pakets, das hinzugefügt werden soll, und `<sourcePath>` gibt die Ordner basierte Paketquelle an, der das Paket hinzugefügt wird. HTTP-Quellen werden nicht unterstützt.

## <a name="options"></a>Optionen

- **`-ConfigFile`**

  Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.

- **`-Expand`**

  Fügt der Paketquelle alle Dateien im Paket hinzu.

- **`-ForceEnglishOutput`**

  *(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.
Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.

- **`-?|-help`**

  Zeigt Hilfe Informationen für den Befehl an.

- **`-NonInteractive`**

  Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.

- **`-src|-Source`**

   Gibt die Paketquelle an, bei der es sich um einen Ordner oder eine UNC-Freigabe handelt, dem die nupkg hinzugefügt wird. Http-Quellen werden nicht unterstützt.

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
