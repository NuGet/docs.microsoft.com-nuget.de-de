---
title: NuGet CLI-Suchbefehl
description: Referenz für den nuget.exe-Suchbefehl
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323660"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="654e1-103">Search-Befehl (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="654e1-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="654e1-104">**Gilt für:** Paketnutzung &bullet; **Unterstützte Versionen:** 5.8 und höher</span><span class="sxs-lookup"><span data-stu-id="654e1-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="654e1-105">Durchsucht eine bestimmte Quelle mithilfe der bereitgestellten Abfragezeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="654e1-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="654e1-106">Wenn keine Quellen angegeben werden, werden alle in %AppData%\NuGet\NuGet.Config definierten Quellen verwendet.</span><span class="sxs-lookup"><span data-stu-id="654e1-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.Config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="654e1-107">Verwendung</span><span class="sxs-lookup"><span data-stu-id="654e1-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="654e1-108">, wobei die Suchbegriffe auf die Namen von Paketen, Tags und Paketbeschreibungen genauso angewendet werden wie bei der Verwendung auf nuget.org.</span><span class="sxs-lookup"><span data-stu-id="654e1-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="654e1-109">Optionen</span><span class="sxs-lookup"><span data-stu-id="654e1-109">Options</span></span>

| <span data-ttu-id="654e1-110">Name</span><span class="sxs-lookup"><span data-stu-id="654e1-110">Name</span></span> | <span data-ttu-id="654e1-111">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="654e1-111">Description</span></span> | <span data-ttu-id="654e1-112">Verwendung</span><span class="sxs-lookup"><span data-stu-id="654e1-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="654e1-113">Prerelease</span><span class="sxs-lookup"><span data-stu-id="654e1-113">PreRelease</span></span> | <span data-ttu-id="654e1-114">Vorabversionspakete sind standardmäßig nicht enthalten, können aber mit diesem Argument eingeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="654e1-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="654e1-115">-PreRelease</span><span class="sxs-lookup"><span data-stu-id="654e1-115">-PreRelease</span></span> |
| <span data-ttu-id="654e1-116">`Source`</span><span class="sxs-lookup"><span data-stu-id="654e1-116">Source</span></span> | <span data-ttu-id="654e1-117">Bestimmte Paketquellen, die gesucht werden sollen, anstatt die Standardquellen in __nuget.config__</span><span class="sxs-lookup"><span data-stu-id="654e1-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="654e1-118">-Source `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="654e1-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="654e1-119">Take</span><span class="sxs-lookup"><span data-stu-id="654e1-119">Take</span></span> | <span data-ttu-id="654e1-120">Die Anzahl der zurückzugebende Ergebnisse.</span><span class="sxs-lookup"><span data-stu-id="654e1-120">The number of results to return.</span></span> <span data-ttu-id="654e1-121">Der Standardwert lautet 20.</span><span class="sxs-lookup"><span data-stu-id="654e1-121">The default value is 20.</span></span> | <span data-ttu-id="654e1-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="654e1-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="654e1-123">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="654e1-123">Verbosity</span></span> | <span data-ttu-id="654e1-124">Die Detailebene, die in der Ausgabe angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="654e1-124">The level of detail to display in the output.</span></span> <span data-ttu-id="654e1-125">Der Standardwert ist _normal._</span><span class="sxs-lookup"><span data-stu-id="654e1-125">The default is _normal_.</span></span> <span data-ttu-id="654e1-126">(Siehe Hinweis unten)</span><span class="sxs-lookup"><span data-stu-id="654e1-126">(See the note below)</span></span>  | <span data-ttu-id="654e1-127">-Ausführlichkeit `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="654e1-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="654e1-128">Hilfe</span><span class="sxs-lookup"><span data-stu-id="654e1-128">Help</span></span> | <span data-ttu-id="654e1-129">Zeigt Hilfeinformationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="654e1-129">Displays help information for the command</span></span> | <span data-ttu-id="654e1-130">-Help</span><span class="sxs-lookup"><span data-stu-id="654e1-130">-Help</span></span> |

<span data-ttu-id="654e1-131">Siehe auch [Umgebungsvariablen.](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="654e1-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="654e1-132">Ausführlichkeitsstufen:</span><span class="sxs-lookup"><span data-stu-id="654e1-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="654e1-133">_quiet_ – Paket-ID, Version</span><span class="sxs-lookup"><span data-stu-id="654e1-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="654e1-134">_normal_ – Paket-ID, Version, Downloads, Vorschau der Beschreibung</span><span class="sxs-lookup"><span data-stu-id="654e1-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="654e1-135">_detailed_ : Paket-ID, Version, Downloads, vollständige Beschreibung, Weitere Informationen wie die Abfrage-URL</span><span class="sxs-lookup"><span data-stu-id="654e1-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="654e1-136">Beispiele</span><span class="sxs-lookup"><span data-stu-id="654e1-136">Examples</span></span>

<span data-ttu-id="654e1-137">Suchen Sie nach *Protokollierungspaketen* aus Standardquellen:</span><span class="sxs-lookup"><span data-stu-id="654e1-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="654e1-138">Suchen Sie nach *Protokollierungspaketen* mit detaillierter Ausführlichkeit:</span><span class="sxs-lookup"><span data-stu-id="654e1-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="654e1-139">Suchen Sie nach *paketbezogenen Protokollierungspaketen,* und zeigen Sie nur die ersten fünf Ergebnisse an:</span><span class="sxs-lookup"><span data-stu-id="654e1-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="654e1-140">Suchen Sie nach *JSON-bezogenen* Paketen, einschließlich Vorabversionen, aus der angegebenen Quelle/dem angegebenen Feed:</span><span class="sxs-lookup"><span data-stu-id="654e1-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="654e1-141">Suchen Sie nach *JSON-bezogenen* Paketen aus mehreren Quellen/Feeds:</span><span class="sxs-lookup"><span data-stu-id="654e1-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
