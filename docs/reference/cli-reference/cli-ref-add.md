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
# <a name="add-command-nuget-cli"></a><span data-ttu-id="a3c7c-103">Der Befehl „add““ (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="a3c7c-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="a3c7c-104">**Gilt für**: &bullet; **unterstützte Versionen**der Paket Veröffentlichung: 3.3+</span><span class="sxs-lookup"><span data-stu-id="a3c7c-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="a3c7c-105">Fügt ein angegebenes Paket zu einer nicht-http-Paketquelle (Ordner oder UNC-Pfad) in einem hierarchischen Layout hinzu, in dem Ordner für die Paket-ID und die Versionsnummer erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="a3c7c-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="a3c7c-106">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="a3c7c-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="a3c7c-107">Beim Wiederherstellen oder Aktualisieren der Paketquelle bietet Hierarchisches Layout eine deutlich bessere Leistung.</span><span class="sxs-lookup"><span data-stu-id="a3c7c-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="a3c7c-108">Um alle Dateien im Paket auf die Ziel Paketquelle zu erweitern, verwenden Sie den `-Expand` -Schalter.</span><span class="sxs-lookup"><span data-stu-id="a3c7c-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="a3c7c-109">Dies führt in der Regel dazu, dass zusätzliche Unterordner im Ziel angezeigt `tools` werden `lib`, z. b. und.</span><span class="sxs-lookup"><span data-stu-id="a3c7c-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="a3c7c-110">Verwendung</span><span class="sxs-lookup"><span data-stu-id="a3c7c-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="a3c7c-111">Dabei steht für den Pfadnamen des Pakets, das hinzugefügt `<sourcePath>` werden soll, und gibt die Ordner basierte Paketquelle an, der das Paket hinzugefügt wird. `<packagePath>`</span><span class="sxs-lookup"><span data-stu-id="a3c7c-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="a3c7c-112">HTTP-Quellen werden nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="a3c7c-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="a3c7c-113">Optionen</span><span class="sxs-lookup"><span data-stu-id="a3c7c-113">Options</span></span>

| <span data-ttu-id="a3c7c-114">Option</span><span class="sxs-lookup"><span data-stu-id="a3c7c-114">Option</span></span> | <span data-ttu-id="a3c7c-115">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="a3c7c-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a3c7c-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a3c7c-116">ConfigFile</span></span> | <span data-ttu-id="a3c7c-117">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="a3c7c-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a3c7c-118">Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="a3c7c-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a3c7c-119">Expand</span><span class="sxs-lookup"><span data-stu-id="a3c7c-119">Expand</span></span> | <span data-ttu-id="a3c7c-120">Fügt der Paketquelle alle Dateien im Paket hinzu.</span><span class="sxs-lookup"><span data-stu-id="a3c7c-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="a3c7c-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a3c7c-121">ForceEnglishOutput</span></span> | <span data-ttu-id="a3c7c-122">*(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="a3c7c-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a3c7c-123">Help</span><span class="sxs-lookup"><span data-stu-id="a3c7c-123">Help</span></span> | <span data-ttu-id="a3c7c-124">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="a3c7c-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="a3c7c-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a3c7c-125">NonInteractive</span></span> | <span data-ttu-id="a3c7c-126">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="a3c7c-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a3c7c-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="a3c7c-127">Verbosity</span></span> | <span data-ttu-id="a3c7c-128">Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*.</span><span class="sxs-lookup"><span data-stu-id="a3c7c-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a3c7c-129">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a3c7c-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a3c7c-130">Beispiele</span><span class="sxs-lookup"><span data-stu-id="a3c7c-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
