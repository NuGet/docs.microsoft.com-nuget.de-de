---
title: NuGet-2.8.2-Versionshinweise
description: Versionshinweise für NuGet 2.8.2 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a004c250d60a4ed1ca8dede1e83b2a68e10299bf
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="ae210-103">NuGet-2.8.2-Versionshinweise</span><span class="sxs-lookup"><span data-stu-id="ae210-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="ae210-104">[Anmerkungen zur Version des NuGet-2.8.1](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3-Versionshinweise](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="ae210-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="ae210-105">NuGet 2.8.2 wurde am 22. Mai 2014 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="ae210-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="ae210-106">Dieser Version enthalten nur Änderungen an der Befehlszeile nuget.exe, das Paket NuGet.Server in und andere NuGet-Pakete.</span><span class="sxs-lookup"><span data-stu-id="ae210-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="ae210-107">Die Version nicht aktualisierte Visual Studio-Erweiterung oder WebMatrix-Erweiterung enthalten.</span><span class="sxs-lookup"><span data-stu-id="ae210-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="ae210-108">Wichtige Updates</span><span class="sxs-lookup"><span data-stu-id="ae210-108">Notable Updates</span></span>

<span data-ttu-id="ae210-109">Die wichtigste Updates wurden in der Befehlszeile nuget.exe und NuGet.Server in Pakets (für selbst gehostete NuGet-Feeds).</span><span class="sxs-lookup"><span data-stu-id="ae210-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="ae210-110">Wichtige nuget.exe Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="ae210-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="ae210-111">NuGet.exe Push schlägt fehl, und hält, und wiederholen Sie dann</span><span class="sxs-lookup"><span data-stu-id="ae210-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="ae210-112">NuGet.exe Push keine Anmeldeinformationen für Standardauthentifizierung ordnungsgemäß gesendet</span><span class="sxs-lookup"><span data-stu-id="ae210-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="ae210-113">NuGet.exe Push wird nicht temporäre Umleitung folgen.</span><span class="sxs-lookup"><span data-stu-id="ae210-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="ae210-114">Fehlerbehebung für wichtige NuGet.Server in</span><span class="sxs-lookup"><span data-stu-id="ae210-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="ae210-115">Falscher Wert für IsAbsoluteLatestVersion zurückgegebenes NuGet.Server in</span><span class="sxs-lookup"><span data-stu-id="ae210-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="ae210-116">Pakete aktualisiert</span><span class="sxs-lookup"><span data-stu-id="ae210-116">Packages Updated</span></span>

<span data-ttu-id="ae210-117">Die nuget.exe Befehlszeilen und NuGet.Server in Updates werden als NuGet-Paket-Updates zur Verfügung gestellt.</span><span class="sxs-lookup"><span data-stu-id="ae210-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="ae210-118">Andere Pakete mit 2.8.2 ebenfalls aktualisiert wurden.</span><span class="sxs-lookup"><span data-stu-id="ae210-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="ae210-119">So sieht die Liste der aktualisierten Pakete aus:</span><span class="sxs-lookup"><span data-stu-id="ae210-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="ae210-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="ae210-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="ae210-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="ae210-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="ae210-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="ae210-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="ae210-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="ae210-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="ae210-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (das Paket, nicht die Erweiterung)</span><span class="sxs-lookup"><span data-stu-id="ae210-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="ae210-125">Alle Änderungen</span><span class="sxs-lookup"><span data-stu-id="ae210-125">All Changes</span></span>
<span data-ttu-id="ae210-126">Es gab 10 Probleme, die in der Version behoben.</span><span class="sxs-lookup"><span data-stu-id="ae210-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="ae210-127">Eine vollständige Liste der Arbeit Artikel feste in NuGet 2.8.2, bitte Ansicht der [NuGet Issue Tracker für diese Version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="ae210-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
