---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860575"
---
Verwenden Sie zum Wiederherstellen den Befehl [restore](../../reference/cli-reference/cli-ref-restore.md). Mit diesem Befehl werden alle Pakete heruntergeladen und installiert, die im Ordner *packages* fehlen.

Verwenden Sie für Projekte, die zu PackageReference migriert wurden, stattdessen [msbuild -t:restore](../package-restore.md#restore-using-msbuild) zum Wiederherstellen von Paketen.

`restore` fügt Pakete nur zum Datenträger hinzu, die Abhängigkeiten eines Projekts werden nicht geändert. Um Projektabhängigkeiten wiederherzustellen, ändern Sie `packages.config`, und verwenden Sie anschließend den Befehl `restore`.

Öffnen Sie wie bei anderen `nuget.exe`-CLI-Befehlen zunächst eine Befehlszeile, und wechseln Sie zu dem Verzeichnis, das die Projektdatei enthält.

Wiederherstellen eines Pakets mit `restore`:

```cli
nuget restore MySolution.sln
```