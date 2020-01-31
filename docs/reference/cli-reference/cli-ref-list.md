---
title: Befehl "nuget CLI List"
description: Referenz für den Befehl "nuget. exe list"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813337"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="58670-103">List-Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="58670-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="58670-104">**Gilt für:** Paket Verbrauch, Veröffentlichung &bullet; **unterstützten Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="58670-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="58670-105">Zeigt eine Liste von Paketen aus einer angegebenen Quelle an.</span><span class="sxs-lookup"><span data-stu-id="58670-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="58670-106">Wenn keine Quellen angegeben werden, werden alle Quellen verwendet, die in der globalen Konfigurationsdatei (`%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config`definiert sind.</span><span class="sxs-lookup"><span data-stu-id="58670-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="58670-107">Wenn `NuGet.Config` keine Quellen angibt, verwendet `list` den Standard Feed (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="58670-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="58670-108">Verwendungs-</span><span class="sxs-lookup"><span data-stu-id="58670-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="58670-109">Gibt an, wo die optionalen Suchbegriffe die angezeigte Liste filtern.</span><span class="sxs-lookup"><span data-stu-id="58670-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="58670-110">Suchbegriffe werden auf die Namen von Paketen, Tags und Paketbeschreibungen angewendet, genauso wie Sie Sie auf nuget.org verwenden.</span><span class="sxs-lookup"><span data-stu-id="58670-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="58670-111">Options</span><span class="sxs-lookup"><span data-stu-id="58670-111">Options</span></span>

| <span data-ttu-id="58670-112">-Option</span><span class="sxs-lookup"><span data-stu-id="58670-112">Option</span></span> | <span data-ttu-id="58670-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="58670-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="58670-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="58670-114">AllVersions</span></span> | <span data-ttu-id="58670-115">Listet alle Versionen eines Pakets auf.</span><span class="sxs-lookup"><span data-stu-id="58670-115">List all versions of a package.</span></span> <span data-ttu-id="58670-116">Standardmäßig wird nur die neueste Paketversion angezeigt.</span><span class="sxs-lookup"><span data-stu-id="58670-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="58670-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="58670-117">ConfigFile</span></span> | <span data-ttu-id="58670-118">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="58670-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="58670-119">Wenn nicht angegeben, wird `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="58670-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="58670-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="58670-120">ForceEnglishOutput</span></span> | <span data-ttu-id="58670-121">*(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="58670-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="58670-122">Hilfe</span><span class="sxs-lookup"><span data-stu-id="58670-122">Help</span></span> | <span data-ttu-id="58670-123">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="58670-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="58670-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="58670-124">IncludeDelisted</span></span> | <span data-ttu-id="58670-125">*(3.2 +)* Nicht aufgelistete Pakete anzeigen.</span><span class="sxs-lookup"><span data-stu-id="58670-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="58670-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="58670-126">NonInteractive</span></span> | <span data-ttu-id="58670-127">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="58670-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="58670-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="58670-128">PreRelease</span></span> | <span data-ttu-id="58670-129">Schließt vorab Pakete in die Liste ein.</span><span class="sxs-lookup"><span data-stu-id="58670-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="58670-130">Quelle</span><span class="sxs-lookup"><span data-stu-id="58670-130">Source</span></span> | <span data-ttu-id="58670-131">Gibt eine Liste der zu durchsuchenden Paketquellen an.</span><span class="sxs-lookup"><span data-stu-id="58670-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="58670-132">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="58670-132">Verbosity</span></span> | <span data-ttu-id="58670-133">Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*.</span><span class="sxs-lookup"><span data-stu-id="58670-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="58670-134">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="58670-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="58670-135">Beispiele</span><span class="sxs-lookup"><span data-stu-id="58670-135">Examples</span></span>

<span data-ttu-id="58670-136">Auflisten aller Pakete aus konfigurierten Feeds:</span><span class="sxs-lookup"><span data-stu-id="58670-136">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="58670-137">Auflisten von Azure-bezogenen Paketen mit detaillierter Ausführlichkeit:</span><span class="sxs-lookup"><span data-stu-id="58670-137">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="58670-138">Auflisten aller Versionen von Azure-bezogenen Paketen aus konfigurierten Feeds:</span><span class="sxs-lookup"><span data-stu-id="58670-138">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="58670-139">Listet alle Versionen von JSON-bezogenen Paketen aus der angegebenen Quelle bzw. dem Feed auf:</span><span class="sxs-lookup"><span data-stu-id="58670-139">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="58670-140">Auflisten von JSON-bezogenen Paketen aus mehreren Quellen/Feeds:</span><span class="sxs-lookup"><span data-stu-id="58670-140">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

