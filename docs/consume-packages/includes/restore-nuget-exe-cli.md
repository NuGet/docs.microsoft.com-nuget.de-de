---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860575"
---
<span data-ttu-id="d67e7-101">Verwenden Sie zum Wiederherstellen den Befehl [restore](../../reference/cli-reference/cli-ref-restore.md). Mit diesem Befehl werden alle Pakete heruntergeladen und installiert, die im Ordner *packages* fehlen.</span><span class="sxs-lookup"><span data-stu-id="d67e7-101">Use the [restore](../../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="d67e7-102">Verwenden Sie für Projekte, die zu PackageReference migriert wurden, stattdessen [msbuild -t:restore](../package-restore.md#restore-using-msbuild) zum Wiederherstellen von Paketen.</span><span class="sxs-lookup"><span data-stu-id="d67e7-102">For projects migrated to PackageReference, use [msbuild -t:restore](../package-restore.md#restore-using-msbuild) to restore packages instead.</span></span>

<span data-ttu-id="d67e7-103">`restore` fügt Pakete nur zum Datenträger hinzu, die Abhängigkeiten eines Projekts werden nicht geändert.</span><span class="sxs-lookup"><span data-stu-id="d67e7-103">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="d67e7-104">Um Projektabhängigkeiten wiederherzustellen, ändern Sie `packages.config`, und verwenden Sie anschließend den Befehl `restore`.</span><span class="sxs-lookup"><span data-stu-id="d67e7-104">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="d67e7-105">Öffnen Sie wie bei anderen `nuget.exe`-CLI-Befehlen zunächst eine Befehlszeile, und wechseln Sie zu dem Verzeichnis, das die Projektdatei enthält.</span><span class="sxs-lookup"><span data-stu-id="d67e7-105">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="d67e7-106">Wiederherstellen eines Pakets mit `restore`:</span><span class="sxs-lookup"><span data-stu-id="d67e7-106">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```