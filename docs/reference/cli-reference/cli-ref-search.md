---
title: Befehl "nuget CLI-Suche"
description: Referenz für den nuget.exe Search-Befehl
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 6f4adcdf3981e5ec0e5e88337a8c3bcdd9158ca3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779158"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="bb4bf-103">Suchbefehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="bb4bf-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="bb4bf-104">**Gilt für:** &bullet; **unterstützte Versionen** von Paketen: 5.8 und höher</span><span class="sxs-lookup"><span data-stu-id="bb4bf-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="bb4bf-105">Durchsucht eine angegebene Quelle mithilfe der angegebenen Abfrage Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="bb4bf-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="bb4bf-106">Wenn keine Quellen angegeben werden, werden alle in% APPDATA% \NuGet\NuGet.config definierten Quellen verwendet.</span><span class="sxs-lookup"><span data-stu-id="bb4bf-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="bb4bf-107">Verwendung</span><span class="sxs-lookup"><span data-stu-id="bb4bf-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="bb4bf-108">Wenn die Suchbegriffe auf die Namen von Paketen, Tags und Paketbeschreibungen angewendet werden, so wie Sie Sie in nuget.org verwenden.</span><span class="sxs-lookup"><span data-stu-id="bb4bf-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="bb4bf-109">Optionen</span><span class="sxs-lookup"><span data-stu-id="bb4bf-109">Options</span></span>

| <span data-ttu-id="bb4bf-110">Name</span><span class="sxs-lookup"><span data-stu-id="bb4bf-110">Name</span></span> | <span data-ttu-id="bb4bf-111">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="bb4bf-111">Description</span></span> | <span data-ttu-id="bb4bf-112">Verwendung</span><span class="sxs-lookup"><span data-stu-id="bb4bf-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="bb4bf-113">Vorab</span><span class="sxs-lookup"><span data-stu-id="bb4bf-113">PreRelease</span></span> | <span data-ttu-id="bb4bf-114">Vorab Versionen von Paketen sind nicht standardmäßig enthalten, können jedoch mithilfe dieses Arguments eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="bb4bf-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="bb4bf-115">-Vorabversion</span><span class="sxs-lookup"><span data-stu-id="bb4bf-115">-PreRelease</span></span> |
| <span data-ttu-id="bb4bf-116">`Source`</span><span class="sxs-lookup"><span data-stu-id="bb4bf-116">Source</span></span> | <span data-ttu-id="bb4bf-117">Bestimmte Paketquellen, die durchsucht werden sollen, anstatt die Standard Quellen in __nuget.config__ zu Abfragen</span><span class="sxs-lookup"><span data-stu-id="bb4bf-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="bb4bf-118">-Quelle `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="bb4bf-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="bb4bf-119">Take</span><span class="sxs-lookup"><span data-stu-id="bb4bf-119">Take</span></span> | <span data-ttu-id="bb4bf-120">Die Anzahl der zurück zugebende Ergebnisse.</span><span class="sxs-lookup"><span data-stu-id="bb4bf-120">The number of results to return.</span></span> <span data-ttu-id="bb4bf-121">Der Standardwert lautet 20.</span><span class="sxs-lookup"><span data-stu-id="bb4bf-121">The default value is 20.</span></span> | <span data-ttu-id="bb4bf-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="bb4bf-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="bb4bf-123">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="bb4bf-123">Verbosity</span></span> | <span data-ttu-id="bb4bf-124">Die Detailebene, die in der Ausgabe angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="bb4bf-124">The level of detail to display in the output.</span></span> <span data-ttu-id="bb4bf-125">Der Standardwert ist " _Normal_".</span><span class="sxs-lookup"><span data-stu-id="bb4bf-125">The default is _normal_.</span></span> <span data-ttu-id="bb4bf-126">(Siehe Hinweis unten)</span><span class="sxs-lookup"><span data-stu-id="bb4bf-126">(See the note below)</span></span>  | <span data-ttu-id="bb4bf-127">-Ausführlichkeit `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="bb4bf-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="bb4bf-128">Hilfe</span><span class="sxs-lookup"><span data-stu-id="bb4bf-128">Help</span></span> | <span data-ttu-id="bb4bf-129">Zeigt Hilfe Informationen für den Befehl an</span><span class="sxs-lookup"><span data-stu-id="bb4bf-129">Displays help information for the command</span></span> | <span data-ttu-id="bb4bf-130">-Hilfe</span><span class="sxs-lookup"><span data-stu-id="bb4bf-130">-Help</span></span> |

<span data-ttu-id="bb4bf-131">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="bb4bf-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="bb4bf-132">Ausführlichkeits Grade:</span><span class="sxs-lookup"><span data-stu-id="bb4bf-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="bb4bf-133">_quiet_ -Paket-ID, Version</span><span class="sxs-lookup"><span data-stu-id="bb4bf-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="bb4bf-134">_Normal_ -Paket-ID, Version, Downloads, Vorschau der Beschreibung</span><span class="sxs-lookup"><span data-stu-id="bb4bf-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="bb4bf-135">_ausführlich_ : Paket-ID, Version, Downloads, vollständige Beschreibung, andere Informationen, wie z. b. die Abfrage-URL</span><span class="sxs-lookup"><span data-stu-id="bb4bf-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="bb4bf-136">Beispiele</span><span class="sxs-lookup"><span data-stu-id="bb4bf-136">Examples</span></span>

<span data-ttu-id="bb4bf-137">Suchen Sie nach *Protokollierungs* bezogenen Paketen aus Standard Quellen:</span><span class="sxs-lookup"><span data-stu-id="bb4bf-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="bb4bf-138">Suchen Sie nach *Protokollierungs* bezogenen Paketen mit ausführlicher Ausführlichkeit:</span><span class="sxs-lookup"><span data-stu-id="bb4bf-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="bb4bf-139">Suchen Sie nach *Protokollierungs* bezogenen Paketen, und zeigen Sie nur die ersten 5 Ergebnisse an:</span><span class="sxs-lookup"><span data-stu-id="bb4bf-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="bb4bf-140">Suchen Sie nach *JSON*-bezogenen Paketen, einschließlich vorab Versionen, aus der angegebenen Quelle bzw. dem Feed:</span><span class="sxs-lookup"><span data-stu-id="bb4bf-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="bb4bf-141">Suchen Sie nach *JSON*-bezogenen Paketen aus mehreren Quellen/Feeds:</span><span class="sxs-lookup"><span data-stu-id="bb4bf-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
