---
title: Befehl "nuget CLI-Befehl"
description: Verweis für den nuget.exe Befehl "hinzufügen"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 89d268946243e8eae07e482db48e809a15260c38
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622901"
---
# <a name="add-command-nuget-cli"></a>Befehl "hinzufügen" (nuget-CLI)

**Gilt für**: &bullet; **unterstützte Versionen**der Paket Veröffentlichung: 3.3 und höher

Fügt ein angegebenes Paket zu einer nicht-http-Paketquelle (Ordner oder UNC-Pfad) in einem hierarchischen Layout hinzu, in dem Ordner für die Paket-ID und die Versionsnummer erstellt werden. Beispiel:

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
