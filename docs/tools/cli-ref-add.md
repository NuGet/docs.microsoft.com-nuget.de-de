---
title: Befehl "hinzufügen" NuGet-CLI
description: Referenz für die nuget.exe Befehl hinzufügen
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545833"
---
# <a name="add-command-nuget-cli"></a>Der Befehl „add““ (NuGet-CLI)

**Gilt für**: Paket veröffentlichen &bullet; **unterstützten Versionen**: 3.3 und höher

Fügt ein angegebenes Paket mit einer nicht-HTTP-Paket-Datenquelle (ein Ordner oder eine UNC-Pfad) in hierarchischer Anordnung, in dem Ordner für das Paket-ID und Version erstellt werden. Zum Beispiel:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Beim Wiederherstellen oder für die Paketquelle aktualisiert, stellt in hierarchischer Anordnung erheblich besseren Leistung bereit.

Um alle Dateien im Paket für die Ziel-Paketquelle zu erweitern, verwenden die `-Expand` wechseln. Dies führt in der Regel zusätzliche Unterordner im Ziel angezeigt werden, z. B. `tools` und `lib`.

## <a name="usage"></a>Verwendung

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

wo `<packagePath>` der Pfadname für das Paket zum Hinzufügen, und `<sourcePath>` gibt an, die Ordner-basierten Paketquelle zu dem das Paket hinzugefügt werden. HTTP-Quellen werden nicht unterstützt.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| Expand | Fügt alle Dateien im Paket für die Paketquelle. |
| ForceEnglishOutput | *(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden. |
| Hilfe | Zeigt die Informationen für den Befehl Hilfe. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Ausführlichkeit | Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
