---
title: Befehl "nuget CLI List"
description: Referenz für den Befehl "nuget. exe list"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327737"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="b54d2-103">List-Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="b54d2-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="b54d2-104">**Gilt für:** Paket Verbrauch, &bullet; **unterstützte Versionen** werden veröffentlicht: alle</span><span class="sxs-lookup"><span data-stu-id="b54d2-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b54d2-105">Zeigt eine Liste von Paketen aus einer angegebenen Quelle an.</span><span class="sxs-lookup"><span data-stu-id="b54d2-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="b54d2-106">Wenn keine Quellen angegeben werden, werden alle Quellen verwendet, die in der globalen `%AppData%\NuGet\NuGet.Config` Konfigurationsdatei (Windows `~/.nuget/NuGet/NuGet.Config`) oder definiert sind.</span><span class="sxs-lookup"><span data-stu-id="b54d2-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="b54d2-107">Wenn `NuGet.Config` keine Quellen angibt `list` , verwendet den Standard-Feed (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="b54d2-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="b54d2-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="b54d2-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="b54d2-109">Gibt an, wo die optionalen Suchbegriffe die angezeigte Liste filtern.</span><span class="sxs-lookup"><span data-stu-id="b54d2-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="b54d2-110">Suchbegriffe werden auf die Namen von Paketen, Tags und Paketbeschreibungen angewendet, genauso wie Sie Sie auf nuget.org verwenden.</span><span class="sxs-lookup"><span data-stu-id="b54d2-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="b54d2-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="b54d2-111">Options</span></span>

| <span data-ttu-id="b54d2-112">Option</span><span class="sxs-lookup"><span data-stu-id="b54d2-112">Option</span></span> | <span data-ttu-id="b54d2-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="b54d2-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b54d2-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="b54d2-114">AllVersions</span></span> | <span data-ttu-id="b54d2-115">Listet alle Versionen eines Pakets auf.</span><span class="sxs-lookup"><span data-stu-id="b54d2-115">List all versions of a package.</span></span> <span data-ttu-id="b54d2-116">Standardmäßig wird nur die neueste Paketversion angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b54d2-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="b54d2-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b54d2-117">ConfigFile</span></span> | <span data-ttu-id="b54d2-118">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="b54d2-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b54d2-119">Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="b54d2-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b54d2-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b54d2-120">ForceEnglishOutput</span></span> | <span data-ttu-id="b54d2-121">*(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="b54d2-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b54d2-122">Help</span><span class="sxs-lookup"><span data-stu-id="b54d2-122">Help</span></span> | <span data-ttu-id="b54d2-123">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="b54d2-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="b54d2-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="b54d2-124">IncludeDelisted</span></span> | <span data-ttu-id="b54d2-125">*(3.2 +)* Nicht aufgelistete Pakete anzeigen.</span><span class="sxs-lookup"><span data-stu-id="b54d2-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="b54d2-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b54d2-126">NonInteractive</span></span> | <span data-ttu-id="b54d2-127">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="b54d2-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b54d2-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="b54d2-128">PreRelease</span></span> | <span data-ttu-id="b54d2-129">Schließt vorab Pakete in die Liste ein.</span><span class="sxs-lookup"><span data-stu-id="b54d2-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="b54d2-130">Source</span><span class="sxs-lookup"><span data-stu-id="b54d2-130">Source</span></span> | <span data-ttu-id="b54d2-131">Gibt eine Liste der zu durchsuchenden Paketquellen an.</span><span class="sxs-lookup"><span data-stu-id="b54d2-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="b54d2-132">Verbosity</span><span class="sxs-lookup"><span data-stu-id="b54d2-132">Verbosity</span></span> | <span data-ttu-id="b54d2-133">Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*.</span><span class="sxs-lookup"><span data-stu-id="b54d2-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b54d2-134">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b54d2-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b54d2-135">Beispiele</span><span class="sxs-lookup"><span data-stu-id="b54d2-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
