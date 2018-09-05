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
# <a name="add-command-nuget-cli"></a><span data-ttu-id="41700-103">Der Befehl „add““ (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="41700-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="41700-104">**Gilt für**: Paket veröffentlichen &bullet; **unterstützten Versionen**: 3.3 und höher</span><span class="sxs-lookup"><span data-stu-id="41700-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="41700-105">Fügt ein angegebenes Paket mit einer nicht-HTTP-Paket-Datenquelle (ein Ordner oder eine UNC-Pfad) in hierarchischer Anordnung, in dem Ordner für das Paket-ID und Version erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="41700-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="41700-106">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="41700-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="41700-107">Beim Wiederherstellen oder für die Paketquelle aktualisiert, stellt in hierarchischer Anordnung erheblich besseren Leistung bereit.</span><span class="sxs-lookup"><span data-stu-id="41700-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="41700-108">Um alle Dateien im Paket für die Ziel-Paketquelle zu erweitern, verwenden die `-Expand` wechseln.</span><span class="sxs-lookup"><span data-stu-id="41700-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="41700-109">Dies führt in der Regel zusätzliche Unterordner im Ziel angezeigt werden, z. B. `tools` und `lib`.</span><span class="sxs-lookup"><span data-stu-id="41700-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="41700-110">Verwendung</span><span class="sxs-lookup"><span data-stu-id="41700-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="41700-111">wo `<packagePath>` der Pfadname für das Paket zum Hinzufügen, und `<sourcePath>` gibt an, die Ordner-basierten Paketquelle zu dem das Paket hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="41700-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="41700-112">HTTP-Quellen werden nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="41700-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="41700-113">Optionen</span><span class="sxs-lookup"><span data-stu-id="41700-113">Options</span></span>

| <span data-ttu-id="41700-114">Option</span><span class="sxs-lookup"><span data-stu-id="41700-114">Option</span></span> | <span data-ttu-id="41700-115">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="41700-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="41700-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="41700-116">ConfigFile</span></span> | <span data-ttu-id="41700-117">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="41700-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="41700-118">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="41700-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="41700-119">Expand</span><span class="sxs-lookup"><span data-stu-id="41700-119">Expand</span></span> | <span data-ttu-id="41700-120">Fügt alle Dateien im Paket für die Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="41700-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="41700-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="41700-121">ForceEnglishOutput</span></span> | <span data-ttu-id="41700-122">*(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="41700-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="41700-123">Hilfe</span><span class="sxs-lookup"><span data-stu-id="41700-123">Help</span></span> | <span data-ttu-id="41700-124">Zeigt die Informationen für den Befehl Hilfe.</span><span class="sxs-lookup"><span data-stu-id="41700-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="41700-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="41700-125">NonInteractive</span></span> | <span data-ttu-id="41700-126">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="41700-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="41700-127">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="41700-127">Verbosity</span></span> | <span data-ttu-id="41700-128">Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="41700-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="41700-129">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="41700-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="41700-130">Beispiele</span><span class="sxs-lookup"><span data-stu-id="41700-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
