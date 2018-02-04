---
title: NuGet-2.8.2-Versionshinweise | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 2.8.2 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-2.8.2 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f50bd1f0c981ef293a4d2ff425e0dffbdf58036c
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="8f069-104">NuGet-2.8.2-Versionshinweise</span><span class="sxs-lookup"><span data-stu-id="8f069-104">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="8f069-105">[Anmerkungen zur Version des NuGet-2.8.1](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3-Versionshinweise](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="8f069-105">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="8f069-106">NuGet 2.8.2 wurde am 22. Mai 2014 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="8f069-106">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="8f069-107">Dieser Version enthalten nur Änderungen an der Befehlszeile nuget.exe, das Paket NuGet.Server in und andere NuGet-Pakete.</span><span class="sxs-lookup"><span data-stu-id="8f069-107">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="8f069-108">Die Version nicht aktualisierte Visual Studio-Erweiterung oder WebMatrix-Erweiterung enthalten.</span><span class="sxs-lookup"><span data-stu-id="8f069-108">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="8f069-109">Wichtige Updates</span><span class="sxs-lookup"><span data-stu-id="8f069-109">Notable Updates</span></span>

<span data-ttu-id="8f069-110">Die wichtigste Updates wurden in der Befehlszeile nuget.exe und NuGet.Server in Pakets (für selbst gehostete NuGet-Feeds).</span><span class="sxs-lookup"><span data-stu-id="8f069-110">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="8f069-111">Wichtige nuget.exe Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="8f069-111">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="8f069-112">NuGet.exe Push schlägt fehl, und hält, und wiederholen Sie dann</span><span class="sxs-lookup"><span data-stu-id="8f069-112">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="8f069-113">NuGet.exe Push keine Anmeldeinformationen für Standardauthentifizierung ordnungsgemäß gesendet</span><span class="sxs-lookup"><span data-stu-id="8f069-113">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="8f069-114">NuGet.exe Push wird nicht temporäre Umleitung folgen.</span><span class="sxs-lookup"><span data-stu-id="8f069-114">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="8f069-115">Fehlerbehebung für wichtige NuGet.Server in</span><span class="sxs-lookup"><span data-stu-id="8f069-115">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="8f069-116">Falscher Wert für IsAbsoluteLatestVersion zurückgegebenes NuGet.Server in</span><span class="sxs-lookup"><span data-stu-id="8f069-116">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="8f069-117">Pakete aktualisiert</span><span class="sxs-lookup"><span data-stu-id="8f069-117">Packages Updated</span></span>

<span data-ttu-id="8f069-118">Die nuget.exe Befehlszeilen und NuGet.Server in Updates werden als NuGet-Paket-Updates zur Verfügung gestellt.</span><span class="sxs-lookup"><span data-stu-id="8f069-118">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="8f069-119">Andere Pakete mit 2.8.2 ebenfalls aktualisiert wurden.</span><span class="sxs-lookup"><span data-stu-id="8f069-119">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="8f069-120">So sieht die Liste der aktualisierten Pakete aus:</span><span class="sxs-lookup"><span data-stu-id="8f069-120">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="8f069-121">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="8f069-121">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="8f069-122">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="8f069-122">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="8f069-123">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="8f069-123">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="8f069-124">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="8f069-124">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="8f069-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (das Paket, nicht die Erweiterung)</span><span class="sxs-lookup"><span data-stu-id="8f069-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="8f069-126">Alle Änderungen</span><span class="sxs-lookup"><span data-stu-id="8f069-126">All Changes</span></span>
<span data-ttu-id="8f069-127">Es gab 10 Probleme, die in der Version behoben.</span><span class="sxs-lookup"><span data-stu-id="8f069-127">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="8f069-128">Eine vollständige Liste der Arbeit Artikel feste in NuGet 2.8.2, bitte Ansicht der [NuGet Issue Tracker für diese Version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="8f069-128">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
