---
title: NuGet CLI hinzufügen (Befehl)
description: Referenz für die nuget.exe Befehl hinzufügen.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4a4201a321ffe0f7fb61f4e98012a1a2d7d8fda4
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="07e04-103">Fügen Sie hinzu (Befehl) (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="07e04-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="07e04-104">**Gilt für**: Verpacken Sie die Publishing &bullet; **unterstützten Versionen**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="07e04-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="07e04-105">Fügt ein angegebenes Paket auf einem nicht-HTTP-Paketquelle (ein Ordner oder eine UNC-Pfad) in hierarchischer Anordnung dargestellt, bei dem Ordner, für die Paket-ID und die Version erstellt werden an.</span><span class="sxs-lookup"><span data-stu-id="07e04-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="07e04-106">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="07e04-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="07e04-107">Beim Wiederherstellen, oder für die Paketquelle aktualisieren, stellt hierarchischer Anordnung dargestellt deutlichen Leistungssteigerung führen.</span><span class="sxs-lookup"><span data-stu-id="07e04-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="07e04-108">Um alle Dateien im Paket für die Paketquelle Ziel zu erweitern, verwenden die `-Expand` wechseln.</span><span class="sxs-lookup"><span data-stu-id="07e04-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="07e04-109">Dies führt in der Regel zusätzliche Unterordner, der in das Ziel, z. B. `tools` und `lib`.</span><span class="sxs-lookup"><span data-stu-id="07e04-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="07e04-110">Verwendung</span><span class="sxs-lookup"><span data-stu-id="07e04-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="07e04-111">wobei `<packagePath>` der Pfadname für das Paket zum Hinzufügen, und `<sourcePath>` gibt an, die Ordner-basierte Paketquelle an, der das Paket hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="07e04-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="07e04-112">HTTP-Datenquellen werden nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="07e04-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="07e04-113">Optionen</span><span class="sxs-lookup"><span data-stu-id="07e04-113">Options</span></span>

| <span data-ttu-id="07e04-114">Option</span><span class="sxs-lookup"><span data-stu-id="07e04-114">Option</span></span> | <span data-ttu-id="07e04-115">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="07e04-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="07e04-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="07e04-116">ConfigFile</span></span> | <span data-ttu-id="07e04-117">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="07e04-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="07e04-118">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="07e04-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="07e04-119">Expand</span><span class="sxs-lookup"><span data-stu-id="07e04-119">Expand</span></span> | <span data-ttu-id="07e04-120">Fügt alle Dateien im Paket für die Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="07e04-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="07e04-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="07e04-121">ForceEnglishOutput</span></span> | <span data-ttu-id="07e04-122">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="07e04-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="07e04-123">Hilfe</span><span class="sxs-lookup"><span data-stu-id="07e04-123">Help</span></span> | <span data-ttu-id="07e04-124">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="07e04-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="07e04-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="07e04-125">NonInteractive</span></span> | <span data-ttu-id="07e04-126">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="07e04-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="07e04-127">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="07e04-127">Verbosity</span></span> | <span data-ttu-id="07e04-128">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="07e04-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="07e04-129">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="07e04-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="07e04-130">Beispiele</span><span class="sxs-lookup"><span data-stu-id="07e04-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
