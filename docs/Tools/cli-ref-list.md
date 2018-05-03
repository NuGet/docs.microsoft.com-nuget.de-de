---
title: NuGet CLI auflisten (Befehl)
description: Referenz für den nuget.exe List-Befehl
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4a44c70937e7cb49e472c53e9857e9f44d269f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="2da00-103">Auflisten (Befehl) (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2da00-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="2da00-104">**Gilt für:** Paket Verbrauchs, Veröffentlichung &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="2da00-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="2da00-105">Zeigt eine Liste der Pakete aus einer bestimmten Quelle an.</span><span class="sxs-lookup"><span data-stu-id="2da00-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="2da00-106">Wenn keine Datenquellen angegeben sind, alle Datenquellen definiert, in der Konfigurationsdatei des globalen `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config`, verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="2da00-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="2da00-107">Wenn `NuGet.Config` gibt keine Quellen `list` den Standard-Feed (nuget.org) verwendet.</span><span class="sxs-lookup"><span data-stu-id="2da00-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="2da00-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="2da00-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="2da00-109">die optionale Suchbegriffe werden, in dem die angezeigte Liste herausgefiltert.</span><span class="sxs-lookup"><span data-stu-id="2da00-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="2da00-110">Suchbegriffe werden auf die Namen der Pakete, Tags und Beschreibungen Paket angewendet werden, wie bei ihrer auf nuget.org Verwendung.</span><span class="sxs-lookup"><span data-stu-id="2da00-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="2da00-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="2da00-111">Options</span></span>

| <span data-ttu-id="2da00-112">Option</span><span class="sxs-lookup"><span data-stu-id="2da00-112">Option</span></span> | <span data-ttu-id="2da00-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="2da00-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2da00-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="2da00-114">AllVersions</span></span> | <span data-ttu-id="2da00-115">Listen Sie aller Versionen eines Pakets an auf.</span><span class="sxs-lookup"><span data-stu-id="2da00-115">List all versions of a package.</span></span> <span data-ttu-id="2da00-116">Standardmäßig wird nur die neueste Paketversion angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2da00-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="2da00-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2da00-117">ConfigFile</span></span> | <span data-ttu-id="2da00-118">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="2da00-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2da00-119">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="2da00-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2da00-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2da00-120">ForceEnglishOutput</span></span> | <span data-ttu-id="2da00-121">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="2da00-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2da00-122">Hilfe</span><span class="sxs-lookup"><span data-stu-id="2da00-122">Help</span></span> | <span data-ttu-id="2da00-123">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="2da00-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="2da00-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="2da00-124">IncludeDelisted</span></span> | <span data-ttu-id="2da00-125">*(3.2 +)*  Nicht aufgelistete Pakete angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2da00-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="2da00-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2da00-126">NonInteractive</span></span> | <span data-ttu-id="2da00-127">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="2da00-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2da00-128">Vorabversion</span><span class="sxs-lookup"><span data-stu-id="2da00-128">PreRelease</span></span> | <span data-ttu-id="2da00-129">Enthält Vorabversionen von Paketen in der Liste an.</span><span class="sxs-lookup"><span data-stu-id="2da00-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="2da00-130">Quelle</span><span class="sxs-lookup"><span data-stu-id="2da00-130">Source</span></span> | <span data-ttu-id="2da00-131">Gibt eine Liste der Pakete Quellen zu suchen.</span><span class="sxs-lookup"><span data-stu-id="2da00-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="2da00-132">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="2da00-132">Verbosity</span></span> | <span data-ttu-id="2da00-133">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="2da00-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2da00-134">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2da00-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2da00-135">Beispiele</span><span class="sxs-lookup"><span data-stu-id="2da00-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
