---
title: Befehl "nuget CLI-Befehl"
description: Referenz für den Befehl "nuget. exe Add"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327857"
---
# <a name="add-command-nuget-cli"></a>Der Befehl „add““ (NuGet-CLI)

**Gilt für**: &bullet; **unterstützte Versionen**der Paket Veröffentlichung: 3.3+

Fügt ein angegebenes Paket zu einer nicht-http-Paketquelle (Ordner oder UNC-Pfad) in einem hierarchischen Layout hinzu, in dem Ordner für die Paket-ID und die Versionsnummer erstellt werden. Beispiel:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Beim Wiederherstellen oder Aktualisieren der Paketquelle bietet Hierarchisches Layout eine deutlich bessere Leistung.

Um alle Dateien im Paket auf die Ziel Paketquelle zu erweitern, verwenden Sie den `-Expand` -Schalter. Dies führt in der Regel dazu, dass zusätzliche Unterordner im Ziel angezeigt `tools` werden `lib`, z. b. und.

## <a name="usage"></a>Verwendung

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

Dabei steht für den Pfadnamen des Pakets, das hinzugefügt `<sourcePath>` werden soll, und gibt die Ordner basierte Paketquelle an, der das Paket hinzugefügt wird. `<packagePath>` HTTP-Quellen werden nicht unterstützt.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.|
| Expand | Fügt der Paketquelle alle Dateien im Paket hinzu. |
| ForceEnglishOutput | *(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird. |
| Help | Zeigt Hilfe Informationen für den Befehl an. |
| NonInteractive | Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen. |
| Verbosity | Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
