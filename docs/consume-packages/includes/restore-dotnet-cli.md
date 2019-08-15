---
ms.openlocfilehash: 9764479d88cc8d87a9f455e64bd46ae8de15055d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860610"
---
<span data-ttu-id="960a6-101">Verwenden Sie den Befehl [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), der Pakete wiederherstellt, die in der Projektdatei aufgelistet sind (siehe [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="960a6-101">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="960a6-102">In .NET Core 2.0 und höher erfolgt die Wiederherstellung automatisch mit `dotnet build` und `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="960a6-102">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="960a6-103">Ab NuGet 4.0 wird derselbe Code ausgeführt wie für `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="960a6-103">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="960a6-104">Öffnen Sie wie bei anderen `dotnet`-CLI-Befehlen zunächst eine Befehlszeile, und wechseln Sie zu dem Verzeichnis, das die Projektdatei enthält.</span><span class="sxs-lookup"><span data-stu-id="960a6-104">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="960a6-105">Wiederherstellen eines Pakets mit `dotnet restore`:</span><span class="sxs-lookup"><span data-stu-id="960a6-105">To restore a package using `dotnet restore`:</span></span>

```cli
dotnet restore 
```