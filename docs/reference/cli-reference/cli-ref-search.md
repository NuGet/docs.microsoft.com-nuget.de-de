---
title: Befehl "nuget CLI-Suche"
description: Referenz für den nuget.exe Search-Befehl
author: advay26
ms.author: t-adtand
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 8d63efefb8f14c03fbe3986d8d7eebcc3eb5bcac
ms.sourcegitcommit: 6cda91f135e58cf57a2471b0c7c4a2f748f40024
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/02/2020
ms.locfileid: "89359681"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="e7972-103">Suchbefehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="e7972-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="e7972-104">**Gilt für:** &bullet; **unterstützte Versionen** von Paketen: 5.8 und höher</span><span class="sxs-lookup"><span data-stu-id="e7972-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="e7972-105">Durchsucht eine angegebene Quelle mithilfe der angegebenen Abfrage Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="e7972-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="e7972-106">Wenn keine Quellen angegeben werden, werden alle in% APPDATA% \NuGet\NuGet.config definierten Quellen verwendet.</span><span class="sxs-lookup"><span data-stu-id="e7972-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="e7972-107">Verwendung</span><span class="sxs-lookup"><span data-stu-id="e7972-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="e7972-108">Wenn die Suchbegriffe auf die Namen von Paketen, Tags und Paketbeschreibungen angewendet werden, so wie Sie Sie in nuget.org verwenden.</span><span class="sxs-lookup"><span data-stu-id="e7972-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="e7972-109">Optionen</span><span class="sxs-lookup"><span data-stu-id="e7972-109">Options</span></span>

| <span data-ttu-id="e7972-110">Name</span><span class="sxs-lookup"><span data-stu-id="e7972-110">Name</span></span> | <span data-ttu-id="e7972-111">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="e7972-111">Description</span></span> | <span data-ttu-id="e7972-112">Verwendung</span><span class="sxs-lookup"><span data-stu-id="e7972-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="e7972-113">Vorab</span><span class="sxs-lookup"><span data-stu-id="e7972-113">PreRelease</span></span> | <span data-ttu-id="e7972-114">Vorab Versionen von Paketen sind nicht standardmäßig enthalten, können jedoch mithilfe dieses Arguments eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="e7972-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="e7972-115">-Vorabversion</span><span class="sxs-lookup"><span data-stu-id="e7972-115">-PreRelease</span></span> |
| <span data-ttu-id="e7972-116">`Source`</span><span class="sxs-lookup"><span data-stu-id="e7972-116">Source</span></span> | <span data-ttu-id="e7972-117">Bestimmte Paketquellen, die durchsucht werden sollen, anstatt die Standard Quellen in __nuget.config__ zu Abfragen</span><span class="sxs-lookup"><span data-stu-id="e7972-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="e7972-118">-Quelle `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="e7972-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="e7972-119">Take</span><span class="sxs-lookup"><span data-stu-id="e7972-119">Take</span></span> | <span data-ttu-id="e7972-120">Die Anzahl der zurück zugebende Ergebnisse.</span><span class="sxs-lookup"><span data-stu-id="e7972-120">The number of results to return.</span></span> <span data-ttu-id="e7972-121">Der Standardwert lautet 20.</span><span class="sxs-lookup"><span data-stu-id="e7972-121">The default value is 20.</span></span> | <span data-ttu-id="e7972-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="e7972-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="e7972-123">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="e7972-123">Verbosity</span></span> | <span data-ttu-id="e7972-124">Die Detailebene, die in der Ausgabe angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="e7972-124">The level of detail to display in the output.</span></span> <span data-ttu-id="e7972-125">Der Standardwert ist " _Normal_".</span><span class="sxs-lookup"><span data-stu-id="e7972-125">The default is _normal_.</span></span> <span data-ttu-id="e7972-126">(Siehe Hinweis unten)</span><span class="sxs-lookup"><span data-stu-id="e7972-126">(See the note below)</span></span>  | <span data-ttu-id="e7972-127">-Ausführlichkeit `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="e7972-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="e7972-128">Hilfe</span><span class="sxs-lookup"><span data-stu-id="e7972-128">Help</span></span> | <span data-ttu-id="e7972-129">Zeigt Hilfe Informationen für den Befehl an</span><span class="sxs-lookup"><span data-stu-id="e7972-129">Displays help information for the command</span></span> | <span data-ttu-id="e7972-130">-Hilfe</span><span class="sxs-lookup"><span data-stu-id="e7972-130">-Help</span></span> |

<span data-ttu-id="e7972-131">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e7972-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="e7972-132">Ausführlichkeits Grade:</span><span class="sxs-lookup"><span data-stu-id="e7972-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="e7972-133">_quiet_ -Paket-ID, Version</span><span class="sxs-lookup"><span data-stu-id="e7972-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="e7972-134">_Normal_ -Paket-ID, Version, Downloads, Vorschau der Beschreibung</span><span class="sxs-lookup"><span data-stu-id="e7972-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="e7972-135">_ausführlich_ : Paket-ID, Version, Downloads, vollständige Beschreibung, andere Informationen, wie z. b. die Abfrage-URL</span><span class="sxs-lookup"><span data-stu-id="e7972-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="e7972-136">Beispiele</span><span class="sxs-lookup"><span data-stu-id="e7972-136">Examples</span></span>

<span data-ttu-id="e7972-137">Suchen Sie nach *Protokollierungs*bezogenen Paketen aus Standard Quellen:</span><span class="sxs-lookup"><span data-stu-id="e7972-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="e7972-138">Suchen Sie nach *Protokollierungs*bezogenen Paketen mit ausführlicher Ausführlichkeit:</span><span class="sxs-lookup"><span data-stu-id="e7972-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="e7972-139">Suchen Sie nach *Protokollierungs*bezogenen Paketen, und zeigen Sie nur die ersten 5 Ergebnisse an:</span><span class="sxs-lookup"><span data-stu-id="e7972-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="e7972-140">Suchen Sie nach *JSON*-bezogenen Paketen, einschließlich vorab Versionen, aus der angegebenen Quelle bzw. dem Feed:</span><span class="sxs-lookup"><span data-stu-id="e7972-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="e7972-141">Suchen Sie nach *JSON*-bezogenen Paketen aus mehreren Quellen/Feeds:</span><span class="sxs-lookup"><span data-stu-id="e7972-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
