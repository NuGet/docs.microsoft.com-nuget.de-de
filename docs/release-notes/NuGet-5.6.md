---
title: Anmerkungen zu dieser Version von nuget 5,6
description: Anmerkungen zu dieser Version von nuget 5,6, einschließlich neuer Features, Fehlerbehebungen und dcrs.
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727806"
---
# <a name="nuget-56-release-notes"></a><span data-ttu-id="94657-103">Anmerkungen zu dieser Version von nuget 5,6</span><span class="sxs-lookup"><span data-stu-id="94657-103">NuGet 5.6 Release Notes</span></span>

<span data-ttu-id="94657-104">Möglichkeiten der NuGet-Verteilung:</span><span class="sxs-lookup"><span data-stu-id="94657-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="94657-105">NuGet-Version</span><span class="sxs-lookup"><span data-stu-id="94657-105">NuGet version</span></span> | <span data-ttu-id="94657-106">Verfügbar in der Visual Studio-Version</span><span class="sxs-lookup"><span data-stu-id="94657-106">Available in Visual Studio version</span></span>| <span data-ttu-id="94657-107">Verfügbar in .NET SDK(s)</span><span class="sxs-lookup"><span data-stu-id="94657-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="94657-108">**5.6.0**</span><span class="sxs-lookup"><span data-stu-id="94657-108">**5.6.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="94657-109">Visual Studio 2019, Version 16.6</span><span class="sxs-lookup"><span data-stu-id="94657-109">Visual Studio 2019 version 16.6</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="94657-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="94657-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="94657-111"><sup>1</sup> Installiert mit Visual Studio 2019 mit .net Core-Arbeitsauslastung</span><span class="sxs-lookup"><span data-stu-id="94657-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-56"></a><span data-ttu-id="94657-112">Zusammenfassung: Neues in 5,6</span><span class="sxs-lookup"><span data-stu-id="94657-112">Summary: What's New in 5.6</span></span>

* <span data-ttu-id="94657-113">Unterstützung von vorab Paketen mit Gleit Komma Versionen.</span><span class="sxs-lookup"><span data-stu-id="94657-113">Support prerelease packages with floating versions.</span></span> <span data-ttu-id="94657-114">`Version="*-*"`, `Version="1.*-*"` und ähnlich wie in den neuesten Versionen, einschließlich vorab Versionen, innerhalb des angegebenen Bereichs [#912](https://github.com/NuGet/Home/issues/912)</span><span class="sxs-lookup"><span data-stu-id="94657-114">`Version="*-*"`, `Version="1.*-*"`, and similar float to latest versions, including prerelease versions, within specified range  - [#912](https://github.com/NuGet/Home/issues/912)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="94657-115">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="94657-115">Issues fixed in this release</span></span>

<span data-ttu-id="94657-116">**K**</span><span class="sxs-lookup"><span data-stu-id="94657-116">**Bugs:**</span></span>

* <span data-ttu-id="94657-117">`nuget push *.nupkg`schlägt fehl, wenn das snupkg- [#8148](https://github.com/NuGet/Home/issues/8148) nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="94657-117">`nuget push *.nupkg` fails when snupkg does not exist - [#8148](https://github.com/NuGet/Home/issues/8148)</span></span>

* <span data-ttu-id="94657-118">Pack und verschiedene andere Codepfade schlagen nicht abhängig vom Gebiets Schema ab.</span><span class="sxs-lookup"><span data-stu-id="94657-118">Pack, and several other code paths, fail dependent on locale.</span></span> <span data-ttu-id="94657-119">RegexOptions. CultureInvariant- [#8246](https://github.com/NuGet/Home/issues/8246) verwenden</span><span class="sxs-lookup"><span data-stu-id="94657-119">Use RegexOptions.CultureInvariant - [#8246](https://github.com/NuGet/Home/issues/8246)</span></span>

* <span data-ttu-id="94657-120">Perf: die Spezifikation der GD für entladene Projekt Szenarien sollte nicht in der Vorschau Wiederherstellung geschrieben werden- [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="94657-120">Perf: DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="94657-121">Wiederherstellung: verbessern der Leistung durch das Zwischenspeichern von Lösungs Abhängigkeits Diagrammen- [#9201](https://github.com/NuGet/Home/issues/9201)</span><span class="sxs-lookup"><span data-stu-id="94657-121">Restore: Improve performance by caching solution dependency graph spec - [#9201](https://github.com/NuGet/Home/issues/9201)</span></span>

* <span data-ttu-id="94657-122">Die pm-Benutzeroberfläche funktioniert nach der Installation eines Pakets mit der PM-Konsole nicht für SDK-Stil Projekte [#9203](https://github.com/NuGet/Home/issues/9203)</span><span class="sxs-lookup"><span data-stu-id="94657-122">PM UI doesn't work for SDK style projects after installing a package with PM Console - [#9203](https://github.com/NuGet/Home/issues/9203)</span></span>

* <span data-ttu-id="94657-123">Eingebettetes Symbol kann nicht in der PM-Benutzeroberfläche mit lokalem paketfeed angezeigt werden, abhängig von/vs \- [#9225](https://github.com/NuGet/Home/issues/9225)</span><span class="sxs-lookup"><span data-stu-id="94657-123">Embedded icon can’t be shown in PM UI with local package feed - depending on / vs \ - [#9225](https://github.com/NuGet/Home/issues/9225)</span></span>

* <span data-ttu-id="94657-124">Nugetversion. tryparameterstrict () sollte "false" zurückgeben, wenn Sie nicht analysiert werden kann [#9255](https://github.com/NuGet/Home/issues/9255)</span><span class="sxs-lookup"><span data-stu-id="94657-124">NuGetVersion.TryParseStrict() should return false if it fails to parse - [#9255](https://github.com/NuGet/Home/issues/9255)</span></span>

* <span data-ttu-id="94657-125">`nuget.exe push`Hilfe für `-source` , sollte die Verwendung des Quell namens vorschlagen, nicht die Quell-URL- [#9265](https://github.com/NuGet/Home/issues/9265)</span><span class="sxs-lookup"><span data-stu-id="94657-125">`nuget.exe push` help for `-source`, should suggest usage of source name, not source URL - [#9265](https://github.com/NuGet/Home/issues/9265)</span></span>

* <span data-ttu-id="94657-126">`dotnet nuget add package SourceUri`erstellt einen ungültigen Standardpaket Quellen Namen- [#9277](https://github.com/NuGet/Home/issues/9277)</span><span class="sxs-lookup"><span data-stu-id="94657-126">`dotnet nuget add package SourceUri`  creates bad default package source name - [#9277](https://github.com/NuGet/Home/issues/9277)</span></span>

* <span data-ttu-id="94657-127">Die Sprachausgabe gibt keine "Suche..."- Meldung beim Wechseln von Registerkarten- [#9307](https://github.com/NuGet/Home/issues/9307)</span><span class="sxs-lookup"><span data-stu-id="94657-127">Screen reader doesn't announce "Searching..." message when switching tabs - [#9307](https://github.com/NuGet/Home/issues/9307)</span></span>

* <span data-ttu-id="94657-128">Barrierefreiheit: die Farbe des Fokus Rechtecks ist nicht auf die Benutzeroberflächen-Registerkarten im Design "dunkel" [#9336](https://github.com/NuGet/Home/issues/9336)</span><span class="sxs-lookup"><span data-stu-id="94657-128">Accessibility: Focus-rectangle color is not accessible PM UI tabs in dark theme - [#9336](https://github.com/NuGet/Home/issues/9336)</span></span>

* <span data-ttu-id="94657-129">die Wiederherstellung von nuget. exe 5,5 mit MSBuild 14 oder niedriger ist nicht möglich [#9458](https://github.com/NuGet/Home/issues/9458)</span><span class="sxs-lookup"><span data-stu-id="94657-129">nuget.exe 5.5 fails to restore with MSBuild 14 or below - [#9458](https://github.com/NuGet/Home/issues/9458)</span></span>

* <span data-ttu-id="94657-130">In Wiederherstellungs Nachrichten keine Millisekunden-Zeiten protokollieren- [#8977](https://github.com/NuGet/Home/issues/8977)</span><span class="sxs-lookup"><span data-stu-id="94657-130">Don't log millisecond times in restore messages - [#8977](https://github.com/NuGet/Home/issues/8977)</span></span>

* <span data-ttu-id="94657-131">Ioutputconsole Async- [#9268](https://github.com/NuGet/Home/issues/9268) erstellen</span><span class="sxs-lookup"><span data-stu-id="94657-131">Make IOutputConsole async - [#9268](https://github.com/NuGet/Home/issues/9268)</span></span>

* <span data-ttu-id="94657-132">Die Auswahl der MSBuild-Version funktioniert in einigen nicht englischen Kulturen schlecht [#9322](https://github.com/NuGet/Home/issues/9322)</span><span class="sxs-lookup"><span data-stu-id="94657-132">MSBuild version picking works poorly on some non-english cultures - [#9322](https://github.com/NuGet/Home/issues/9322)</span></span>

* <span data-ttu-id="94657-133">Standardwert für das Format auf `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)</span><span class="sxs-lookup"><span data-stu-id="94657-133">Missing format default on `dotnet nuget list source` - [#9337](https://github.com/NuGet/Home/issues/9337)</span></span>

* <span data-ttu-id="94657-134">Perf: restoreoperationlogger weist unnötige Thread Affinität auf [#9288](https://github.com/NuGet/Home/issues/9288)</span><span class="sxs-lookup"><span data-stu-id="94657-134">Perf: RestoreOperationLogger has unnecessary thread affinity - [#9288](https://github.com/NuGet/Home/issues/9288)</span></span>

* <span data-ttu-id="94657-135">Automatisierte Erstellung von Dokumenten für `dotnet nuget` Befehle- [#9146](https://github.com/NuGet/Home/issues/9146)</span><span class="sxs-lookup"><span data-stu-id="94657-135">Automated creation of docs for `dotnet nuget` commands - [#9146](https://github.com/NuGet/Home/issues/9146)</span></span>

* <span data-ttu-id="94657-136">Standard Ausführlichkeit sollte die NOOP-Restore- [#8792](https://github.com/NuGet/Home/issues/8792) jedes Projekts nicht melden.</span><span class="sxs-lookup"><span data-stu-id="94657-136">Default verbosity should not report each project's noop restore - [#8792](https://github.com/NuGet/Home/issues/8792)</span></span>

* <span data-ttu-id="94657-137">Unterstützungs `-DependencyVersion` Parameter für `NuGet.exe update` , ähnlich wie bei der Installation von Command- [#7694](https://github.com/NuGet/Home/issues/7694)</span><span class="sxs-lookup"><span data-stu-id="94657-137">Support `-DependencyVersion` parameter for `NuGet.exe update`, similar to install command - [#7694](https://github.com/NuGet/Home/issues/7694)</span></span>


<span data-ttu-id="94657-138">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="94657-138">**DCRs:**</span></span>

* <span data-ttu-id="94657-139">Anfängliche Unterstützung für .net 5.0-Ziel Framework hinzufügen- [#9584](https://github.com/NuGet/Home/issues/9584)</span><span class="sxs-lookup"><span data-stu-id="94657-139">Add initial support for net5.0 target framework - [#9584](https://github.com/NuGet/Home/issues/9584)</span></span>

* <span data-ttu-id="94657-140">Sortieren Sie die Pakete nach ID auf der Registerkarte "Updates" der PM-Benutzeroberfläche- [#9278](https://github.com/NuGet/Home/issues/9278)</span><span class="sxs-lookup"><span data-stu-id="94657-140">Sort packages by ID in the Updates tab of the PM UI - [#9278](https://github.com/NuGet/Home/issues/9278)</span></span>


<span data-ttu-id="94657-141">**[Liste aller Probleme, die in dieser Version behoben wurden: 5,6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span><span class="sxs-lookup"><span data-stu-id="94657-141">**[List of all issues fixed in this release - 5.6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span></span>
