---
title: NuGet CLI auflisten (Befehl) | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für den nuget.exe List-Befehl"
keywords: NuGet-Liste Verweis Pakete auflisten (Befehl)
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7e0945b9e64a15a839f62bde0a0ef8f3d83335d4
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="31462-104">Auflisten (Befehl) (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="31462-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="31462-105">**Gilt für:** Paket Verbrauchs, Veröffentlichung &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="31462-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="31462-106">Zeigt eine Liste der Pakete aus einer bestimmten Quelle an.</span><span class="sxs-lookup"><span data-stu-id="31462-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="31462-107">Wenn keine Datenquellen angegeben sind, alle Datenquellen definiert, in der Konfigurationsdatei des globalen `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config`, verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="31462-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="31462-108">Wenn `NuGet.Config` gibt keine Quellen `list` den Standard-Feed (nuget.org) verwendet.</span><span class="sxs-lookup"><span data-stu-id="31462-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="31462-109">Verwendung</span><span class="sxs-lookup"><span data-stu-id="31462-109">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="31462-110">die optionale Suchbegriffe werden, in dem die angezeigte Liste herausgefiltert.</span><span class="sxs-lookup"><span data-stu-id="31462-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="31462-111">Suchbegriffe werden auf die Namen der Pakete, Tags und Beschreibungen Paket angewendet werden, wie bei ihrer auf nuget.org Verwendung.</span><span class="sxs-lookup"><span data-stu-id="31462-111">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="31462-112">Optionen</span><span class="sxs-lookup"><span data-stu-id="31462-112">Options</span></span>

| <span data-ttu-id="31462-113">Option</span><span class="sxs-lookup"><span data-stu-id="31462-113">Option</span></span> | <span data-ttu-id="31462-114">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="31462-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="31462-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="31462-115">AllVersions</span></span> | <span data-ttu-id="31462-116">Listen Sie aller Versionen eines Pakets an auf.</span><span class="sxs-lookup"><span data-stu-id="31462-116">List all versions of a package.</span></span> <span data-ttu-id="31462-117">Standardmäßig wird nur die neueste Paketversion angezeigt.</span><span class="sxs-lookup"><span data-stu-id="31462-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="31462-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="31462-118">ConfigFile</span></span> | <span data-ttu-id="31462-119">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="31462-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="31462-120">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="31462-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="31462-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="31462-121">ForceEnglishOutput</span></span> | <span data-ttu-id="31462-122">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="31462-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="31462-123">Hilfe</span><span class="sxs-lookup"><span data-stu-id="31462-123">Help</span></span> | <span data-ttu-id="31462-124">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="31462-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="31462-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="31462-125">IncludeDelisted</span></span> | <span data-ttu-id="31462-126">*(3.2 +)*  Nicht aufgelistete Pakete angezeigt.</span><span class="sxs-lookup"><span data-stu-id="31462-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="31462-127">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="31462-127">NonInteractive</span></span> | <span data-ttu-id="31462-128">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="31462-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="31462-129">PreRelease</span><span class="sxs-lookup"><span data-stu-id="31462-129">PreRelease</span></span> | <span data-ttu-id="31462-130">Enthält Vorabversionen von Paketen in der Liste an.</span><span class="sxs-lookup"><span data-stu-id="31462-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="31462-131">Quelle</span><span class="sxs-lookup"><span data-stu-id="31462-131">Source</span></span> | <span data-ttu-id="31462-132">Gibt eine Liste der Pakete Quellen zu suchen.</span><span class="sxs-lookup"><span data-stu-id="31462-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="31462-133">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="31462-133">Verbosity</span></span> | <span data-ttu-id="31462-134">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="31462-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="31462-135">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="31462-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="31462-136">Beispiele</span><span class="sxs-lookup"><span data-stu-id="31462-136">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
