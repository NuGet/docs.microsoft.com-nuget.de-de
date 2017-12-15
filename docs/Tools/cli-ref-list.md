---
title: NuGet CLI auflisten (Befehl) | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: "Referenz für den nuget.exe List-Befehl"
keywords: NuGet-Liste Verweis Pakete auflisten (Befehl)
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="ab9d7-104">Auflisten (Befehl) (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ab9d7-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="ab9d7-105">**Gilt für:** Paket Verbrauchs, Veröffentlichung &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="ab9d7-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ab9d7-106">Zeigt eine Liste der Pakete aus einer bestimmten Quelle an.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="ab9d7-107">Wenn keine Datenquellen angegeben sind, alle Datenquellen definiert, in der Konfigurationsdatei des globalen `%AppData%\NuGet\NuGet.Config`, verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="ab9d7-108">Wenn `NuGet.Config` gibt keine Quellen `list` den Standard-Feed (nuget.org) verwendet.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="ab9d7-109">Verwendung</span><span class="sxs-lookup"><span data-stu-id="ab9d7-109">Usage</span></span>

```
nuget list [search terms] [options]
```

<span data-ttu-id="ab9d7-110">die optionale Suchbegriffe werden, in dem die angezeigte Liste herausgefiltert.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="ab9d7-111">Suchbegriffe werden auf die Namen der Pakete, Tags und Beschreibungen des Pakets angewendet.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-111">Search terms are applied to the names of packages, tags, and package descriptions.</span></span>

## <a name="options"></a><span data-ttu-id="ab9d7-112">Optionen</span><span class="sxs-lookup"><span data-stu-id="ab9d7-112">Options</span></span>
| <span data-ttu-id="ab9d7-113">Option</span><span class="sxs-lookup"><span data-stu-id="ab9d7-113">Option</span></span> | <span data-ttu-id="ab9d7-114">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="ab9d7-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ab9d7-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="ab9d7-115">AllVersions</span></span> | <span data-ttu-id="ab9d7-116">Listen Sie aller Versionen eines Pakets an auf.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-116">List all versions of a package.</span></span> <span data-ttu-id="ab9d7-117">Standardmäßig wird nur die neueste Paketversion angezeigt.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="ab9d7-118">"ConfigFile" hinzu</span><span class="sxs-lookup"><span data-stu-id="ab9d7-118">ConfigFile</span></span> | <span data-ttu-id="ab9d7-119">*(2,5 +)*  Das NuGet-Konfigurationsdatei angewendet.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-119">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="ab9d7-120">Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="ab9d7-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ab9d7-121">ForceEnglishOutput</span></span> | <span data-ttu-id="ab9d7-122">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ab9d7-123">Hilfe</span><span class="sxs-lookup"><span data-stu-id="ab9d7-123">Help</span></span> | <span data-ttu-id="ab9d7-124">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="ab9d7-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="ab9d7-125">IncludeDelisted</span></span> | <span data-ttu-id="ab9d7-126">*(3.2 +)*  Nicht aufgelistete Pakete angezeigt.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="ab9d7-127">Nicht interaktive</span><span class="sxs-lookup"><span data-stu-id="ab9d7-127">NonInteractive</span></span> | <span data-ttu-id="ab9d7-128">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ab9d7-129">Vorabversion</span><span class="sxs-lookup"><span data-stu-id="ab9d7-129">PreRelease</span></span> | <span data-ttu-id="ab9d7-130">Enthält Vorabversionen von Paketen in der Liste an.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="ab9d7-131">Quelle</span><span class="sxs-lookup"><span data-stu-id="ab9d7-131">Source</span></span> | <span data-ttu-id="ab9d7-132">Gibt eine Liste der Pakete Quellen zu suchen.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="ab9d7-133">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="ab9d7-133">Verbosity</span></span> | <span data-ttu-id="ab9d7-134">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *detaillierte (2.5 und höher)*.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="ab9d7-135">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ab9d7-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ab9d7-136">Beispiele</span><span class="sxs-lookup"><span data-stu-id="ab9d7-136">Examples</span></span>

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
