---
title: Befehl "nuget CLI List"
description: Referenz für den Befehl "nuget.exe List"
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 55ccf0d86ad6df8001e7401d430ec29cd7a154c3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780061"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="d1a92-103">List-Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="d1a92-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="d1a92-104">**Gilt für:** Paket Verbrauch, &bullet; **unterstützte Versionen** werden veröffentlicht: alle</span><span class="sxs-lookup"><span data-stu-id="d1a92-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d1a92-105">Zeigt eine Liste von Paketen aus einer angegebenen Quelle an.</span><span class="sxs-lookup"><span data-stu-id="d1a92-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="d1a92-106">Wenn keine Quellen angegeben werden, werden alle Quellen verwendet, die in der globalen Konfigurationsdatei `%AppData%\NuGet\NuGet.Config` (Windows) oder definiert sind `~/.nuget/NuGet/NuGet.Config` .</span><span class="sxs-lookup"><span data-stu-id="d1a92-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="d1a92-107">Wenn `NuGet.Config` keine Quellen angibt, `list` verwendet den Standard-Feed (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="d1a92-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="d1a92-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="d1a92-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="d1a92-109">Gibt an, wo die optionalen Suchbegriffe die angezeigte Liste filtern.</span><span class="sxs-lookup"><span data-stu-id="d1a92-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="d1a92-110">[Suchbegriffe](../../consume-packages/finding-and-choosing-packages.md#search-syntax) werden auf die Namen von Paketen, Tags und Paketbeschreibungen angewendet, genauso wie Sie Sie auf nuget.org verwenden.</span><span class="sxs-lookup"><span data-stu-id="d1a92-110">[Search terms](../../consume-packages/finding-and-choosing-packages.md#search-syntax) are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span> 

## <a name="options"></a><span data-ttu-id="d1a92-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="d1a92-111">Options</span></span>

- **`-AllVersions`**

  <span data-ttu-id="d1a92-112">Listet alle Versionen eines Pakets auf.</span><span class="sxs-lookup"><span data-stu-id="d1a92-112">List all versions of a package.</span></span> <span data-ttu-id="d1a92-113">Standardmäßig wird nur die neueste Paketversion angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d1a92-113">By default, only the latest package version is displayed.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="d1a92-114">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="d1a92-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d1a92-115">Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="d1a92-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="d1a92-116">*(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.</span><span class="sxs-lookup"><span data-stu-id="d1a92-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="d1a92-117">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="d1a92-117">Displays help information for the command.</span></span>

- **`-IncludeDelisted`**

  <span data-ttu-id="d1a92-118">*(3.2 +)* Nicht aufgelistete Pakete anzeigen.</span><span class="sxs-lookup"><span data-stu-id="d1a92-118">*(3.2+)* Display unlisted packages.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="d1a92-119">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="d1a92-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="d1a92-120">Schließt vorab Pakete in die Liste ein.</span><span class="sxs-lookup"><span data-stu-id="d1a92-120">Includes prerelease packages in the list.</span></span>

- **`-Source`**

  <span data-ttu-id="d1a92-121">Die zu durchsuchende Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="d1a92-121">The package source to search.</span></span> <span data-ttu-id="d1a92-122">Sie können mehrere Quellen angeben, indem Sie die Option mehrmals verwenden `-Source` .</span><span class="sxs-lookup"><span data-stu-id="d1a92-122">You can specify multiple sources by using the `-Source` option multiple times.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="d1a92-123">Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="d1a92-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="d1a92-124">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d1a92-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d1a92-125">Beispiele</span><span class="sxs-lookup"><span data-stu-id="d1a92-125">Examples</span></span>

<span data-ttu-id="d1a92-126">Auflisten aller Pakete aus konfigurierten Feeds:</span><span class="sxs-lookup"><span data-stu-id="d1a92-126">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="d1a92-127">Auflisten von Azure-bezogenen Paketen mit detaillierter Ausführlichkeit:</span><span class="sxs-lookup"><span data-stu-id="d1a92-127">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="d1a92-128">Auflisten aller Versionen von Azure-bezogenen Paketen aus konfigurierten Feeds:</span><span class="sxs-lookup"><span data-stu-id="d1a92-128">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="d1a92-129">Listet alle Versionen von JSON-bezogenen Paketen aus der angegebenen Quelle bzw. dem Feed auf:</span><span class="sxs-lookup"><span data-stu-id="d1a92-129">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="d1a92-130">Auflisten von JSON-bezogenen Paketen aus mehreren Quellen/Feeds:</span><span class="sxs-lookup"><span data-stu-id="d1a92-130">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```
