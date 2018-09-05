---
title: NuGet-CLI-Befehl "auflisten"
description: Referenz für die nuget.exe-List-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549800"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="6738c-103">List-Befehl (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="6738c-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="6738c-104">**Gilt für:** -paketverbrauch, Veröffentlichung &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="6738c-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="6738c-105">Zeigt eine Liste der Pakete aus einer vorgegebenen Quelle an.</span><span class="sxs-lookup"><span data-stu-id="6738c-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="6738c-106">Wenn keine Quellen angegeben werden, werden alle Quellen in die globale XML-Konfigurationsdatei definiert `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config`, verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="6738c-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="6738c-107">Wenn `NuGet.Config` keine Quellen, dann gibt `list` der standardfeed (nuget.org) verwendet.</span><span class="sxs-lookup"><span data-stu-id="6738c-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="6738c-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="6738c-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="6738c-109">die optionale Suchbegriffe werden, in der angezeigten Liste gefiltert.</span><span class="sxs-lookup"><span data-stu-id="6738c-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="6738c-110">Suchbegriffe werden auf die Namen der Pakete, Tags und Beschreibungen von Paket angewendet, wie sie sind, wenn sie auf "NuGet.org" zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="6738c-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="6738c-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="6738c-111">Options</span></span>

| <span data-ttu-id="6738c-112">Option</span><span class="sxs-lookup"><span data-stu-id="6738c-112">Option</span></span> | <span data-ttu-id="6738c-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="6738c-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6738c-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="6738c-114">AllVersions</span></span> | <span data-ttu-id="6738c-115">Listen Sie aller Versionen eines Pakets an auf.</span><span class="sxs-lookup"><span data-stu-id="6738c-115">List all versions of a package.</span></span> <span data-ttu-id="6738c-116">Standardmäßig wird nur die aktuelle Paketversion angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6738c-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="6738c-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="6738c-117">ConfigFile</span></span> | <span data-ttu-id="6738c-118">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="6738c-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6738c-119">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="6738c-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="6738c-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="6738c-120">ForceEnglishOutput</span></span> | <span data-ttu-id="6738c-121">*(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="6738c-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="6738c-122">Hilfe</span><span class="sxs-lookup"><span data-stu-id="6738c-122">Help</span></span> | <span data-ttu-id="6738c-123">Zeigt die Informationen für den Befehl Hilfe.</span><span class="sxs-lookup"><span data-stu-id="6738c-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="6738c-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="6738c-124">IncludeDelisted</span></span> | <span data-ttu-id="6738c-125">*(3.2 und höher)*  Nicht aufgelistete Pakete anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="6738c-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="6738c-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="6738c-126">NonInteractive</span></span> | <span data-ttu-id="6738c-127">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="6738c-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="6738c-128">Vorabversion</span><span class="sxs-lookup"><span data-stu-id="6738c-128">PreRelease</span></span> | <span data-ttu-id="6738c-129">Schließt Vorabversionen von Paketen in der Liste aus.</span><span class="sxs-lookup"><span data-stu-id="6738c-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="6738c-130">Quelle</span><span class="sxs-lookup"><span data-stu-id="6738c-130">Source</span></span> | <span data-ttu-id="6738c-131">Gibt eine Liste der Paketquellen zu suchen.</span><span class="sxs-lookup"><span data-stu-id="6738c-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="6738c-132">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="6738c-132">Verbosity</span></span> | <span data-ttu-id="6738c-133">Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="6738c-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="6738c-134">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6738c-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="6738c-135">Beispiele</span><span class="sxs-lookup"><span data-stu-id="6738c-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
