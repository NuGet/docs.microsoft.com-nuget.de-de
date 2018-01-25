---
title: "NuGet CLI hinzufügen (Befehl) | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für die nuget.exe Befehl hinzufügen."
keywords: "NuGet Verweis hinzufügen, fügen Sie Paket-Befehl"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 70c86f8d240bd308224f6b7887b630cc1e953bf8
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="b81c2-104">Fügen Sie hinzu (Befehl) (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b81c2-104">add command (NuGet CLI)</span></span>

<span data-ttu-id="b81c2-105">**Gilt für**: Verpacken Sie die Publishing &bullet; **unterstützten Versionen**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="b81c2-105">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="b81c2-106">Fügt ein angegebenes Paket auf einem nicht-HTTP-Paketquelle (ein Ordner oder eine UNC-Pfad) in hierarchischer Anordnung dargestellt, bei dem Ordner, für die Paket-ID und die Version erstellt werden an.</span><span class="sxs-lookup"><span data-stu-id="b81c2-106">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="b81c2-107">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="b81c2-107">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="b81c2-108">Beim Wiederherstellen, oder für die Paketquelle aktualisieren, stellt hierarchischer Anordnung dargestellt deutlichen Leistungssteigerung führen.</span><span class="sxs-lookup"><span data-stu-id="b81c2-108">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="b81c2-109">Um alle Dateien im Paket für die Paketquelle Ziel zu erweitern, verwenden die `-Expand` wechseln.</span><span class="sxs-lookup"><span data-stu-id="b81c2-109">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="b81c2-110">Dies führt in der Regel zusätzliche Unterordner, der in das Ziel, z. B. `tools` und `lib`.</span><span class="sxs-lookup"><span data-stu-id="b81c2-110">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="b81c2-111">Verwendung</span><span class="sxs-lookup"><span data-stu-id="b81c2-111">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="b81c2-112">wobei `<packagePath>` der Pfadname für das Paket zum Hinzufügen, und `<sourcePath>` gibt an, die Ordner-basierte Paketquelle an, der das Paket hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="b81c2-112">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="b81c2-113">HTTP-Datenquellen werden nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="b81c2-113">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="b81c2-114">Optionen</span><span class="sxs-lookup"><span data-stu-id="b81c2-114">Options</span></span>

| <span data-ttu-id="b81c2-115">Option</span><span class="sxs-lookup"><span data-stu-id="b81c2-115">Option</span></span> | <span data-ttu-id="b81c2-116">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="b81c2-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b81c2-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b81c2-117">ConfigFile</span></span> | <span data-ttu-id="b81c2-118">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="b81c2-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b81c2-119">Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="b81c2-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span>| 
| <span data-ttu-id="b81c2-120">Expand</span><span class="sxs-lookup"><span data-stu-id="b81c2-120">Expand</span></span> | <span data-ttu-id="b81c2-121">Fügt alle Dateien im Paket für die Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="b81c2-121">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="b81c2-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b81c2-122">ForceEnglishOutput</span></span> | <span data-ttu-id="b81c2-123">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="b81c2-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b81c2-124">Hilfe</span><span class="sxs-lookup"><span data-stu-id="b81c2-124">Help</span></span> | <span data-ttu-id="b81c2-125">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="b81c2-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="b81c2-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b81c2-126">NonInteractive</span></span> | <span data-ttu-id="b81c2-127">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="b81c2-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b81c2-128">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="b81c2-128">Verbosity</span></span> | <span data-ttu-id="b81c2-129">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="b81c2-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b81c2-130">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b81c2-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b81c2-131">Beispiele</span><span class="sxs-lookup"><span data-stu-id="b81c2-131">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
