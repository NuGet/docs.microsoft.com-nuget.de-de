---
title: Befehl "nuget CLI List"
description: Referenz für den Befehl "nuget.exe List"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 91886dbbdcdb24648289d6f6efbe1f87e4099fff
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623070"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="551de-103">List-Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="551de-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="551de-104">**Gilt für:** Paket Verbrauch, &bullet; **unterstützte Versionen** werden veröffentlicht: alle</span><span class="sxs-lookup"><span data-stu-id="551de-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="551de-105">Zeigt eine Liste von Paketen aus einer angegebenen Quelle an.</span><span class="sxs-lookup"><span data-stu-id="551de-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="551de-106">Wenn keine Quellen angegeben werden, werden alle Quellen verwendet, die in der globalen Konfigurationsdatei `%AppData%\NuGet\NuGet.Config` (Windows) oder definiert sind `~/.nuget/NuGet/NuGet.Config` .</span><span class="sxs-lookup"><span data-stu-id="551de-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="551de-107">Wenn `NuGet.Config` keine Quellen angibt, `list` verwendet den Standard-Feed (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="551de-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="551de-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="551de-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="551de-109">Gibt an, wo die optionalen Suchbegriffe die angezeigte Liste filtern.</span><span class="sxs-lookup"><span data-stu-id="551de-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="551de-110">[Suchbegriffe](/nuget/consume-packages/finding-and-choosing-packages#search-syntax) werden auf die Namen von Paketen, Tags und Paketbeschreibungen angewendet, genauso wie Sie Sie auf nuget.org verwenden.</span><span class="sxs-lookup"><span data-stu-id="551de-110">[Search terms](/nuget/consume-packages/finding-and-choosing-packages#search-syntax) are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span> 

## <a name="options"></a><span data-ttu-id="551de-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="551de-111">Options</span></span>

- **`-AllVersions`**

  <span data-ttu-id="551de-112">Listet alle Versionen eines Pakets auf.</span><span class="sxs-lookup"><span data-stu-id="551de-112">List all versions of a package.</span></span> <span data-ttu-id="551de-113">Standardmäßig wird nur die neueste Paketversion angezeigt.</span><span class="sxs-lookup"><span data-stu-id="551de-113">By default, only the latest package version is displayed.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="551de-114">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="551de-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="551de-115">Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="551de-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="551de-116">*(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.</span><span class="sxs-lookup"><span data-stu-id="551de-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="551de-117">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="551de-117">Displays help information for the command.</span></span>

- **`-IncludeDelisted`**

  <span data-ttu-id="551de-118">*(3.2 +)* Nicht aufgelistete Pakete anzeigen.</span><span class="sxs-lookup"><span data-stu-id="551de-118">*(3.2+)* Display unlisted packages.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="551de-119">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="551de-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="551de-120">Schließt vorab Pakete in die Liste ein.</span><span class="sxs-lookup"><span data-stu-id="551de-120">Includes prerelease packages in the list.</span></span>

- **`-Source`**

  <span data-ttu-id="551de-121">Gibt eine Liste der zu durchsuchenden Paketquellen an.</span><span class="sxs-lookup"><span data-stu-id="551de-121">Specifies a list of packages sources to search.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="551de-122">Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="551de-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="551de-123">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="551de-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="551de-124">Beispiele</span><span class="sxs-lookup"><span data-stu-id="551de-124">Examples</span></span>

<span data-ttu-id="551de-125">Auflisten aller Pakete aus konfigurierten Feeds:</span><span class="sxs-lookup"><span data-stu-id="551de-125">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="551de-126">Auflisten von Azure-bezogenen Paketen mit detaillierter Ausführlichkeit:</span><span class="sxs-lookup"><span data-stu-id="551de-126">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="551de-127">Auflisten aller Versionen von Azure-bezogenen Paketen aus konfigurierten Feeds:</span><span class="sxs-lookup"><span data-stu-id="551de-127">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="551de-128">Listet alle Versionen von JSON-bezogenen Paketen aus der angegebenen Quelle bzw. dem Feed auf:</span><span class="sxs-lookup"><span data-stu-id="551de-128">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="551de-129">Auflisten von JSON-bezogenen Paketen aus mehreren Quellen/Feeds:</span><span class="sxs-lookup"><span data-stu-id="551de-129">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```
