---
title: Anmerkungen zu NuGet 2.8.2
description: Anmerkungen zu dieser Version für die Einbindung von NuGet 2.8.2 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551147"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="f2d03-103">Anmerkungen zu NuGet 2.8.2</span><span class="sxs-lookup"><span data-stu-id="f2d03-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="f2d03-104">[Anmerkungen zu NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [Anmerkungen zu NuGet 2.8.3](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="f2d03-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="f2d03-105">NuGet 2.8.2 wurde am 22. Mai 2014 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="f2d03-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="f2d03-106">Dieser Release enthalten nur Änderungen an der Befehlszeile nuget.exe, das Paket "NuGet.Server" und andere NuGet-Pakete.</span><span class="sxs-lookup"><span data-stu-id="f2d03-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="f2d03-107">Die Version es sich nicht um eine aktualisierte Erweiterung für Visual Studio oder WebMatrix-Erweiterung enthalten.</span><span class="sxs-lookup"><span data-stu-id="f2d03-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="f2d03-108">Wichtige Updates</span><span class="sxs-lookup"><span data-stu-id="f2d03-108">Notable Updates</span></span>

<span data-ttu-id="f2d03-109">Die wichtigsten Updates wurden in der Befehlszeile nuget.exe und das Paket "NuGet.Server" (für selbst gehostete NuGet-Feeds).</span><span class="sxs-lookup"><span data-stu-id="f2d03-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="f2d03-110">Wichtige nuget.exe-Fehlerbehebungen</span><span class="sxs-lookup"><span data-stu-id="f2d03-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="f2d03-111">NuGet.exe Push schlägt fehl, und behält die Wiederholung</span><span class="sxs-lookup"><span data-stu-id="f2d03-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="f2d03-112">NuGet.exe Push keine Anmeldeinformationen für Standardauthentifizierung ordnungsgemäß gesendet</span><span class="sxs-lookup"><span data-stu-id="f2d03-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="f2d03-113">NuGet.exe Push wird nicht temporäre Umleitung folgen.</span><span class="sxs-lookup"><span data-stu-id="f2d03-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="f2d03-114">Programmfehlerbehebung für wichtige "NuGet.Server"</span><span class="sxs-lookup"><span data-stu-id="f2d03-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="f2d03-115">Falscher Wert für "NuGet.Server" zurückgegebenes IsAbsoluteLatestVersion</span><span class="sxs-lookup"><span data-stu-id="f2d03-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="f2d03-116">Pakete aktualisiert</span><span class="sxs-lookup"><span data-stu-id="f2d03-116">Packages Updated</span></span>

<span data-ttu-id="f2d03-117">Die Befehlszeile nuget.exe und "NuGet.Server" Korrekturen werden als NuGet-Paket-Updates ausgeliefert.</span><span class="sxs-lookup"><span data-stu-id="f2d03-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="f2d03-118">Andere Pakete, die mit 2.8.2 auch aktualisiert wurden.</span><span class="sxs-lookup"><span data-stu-id="f2d03-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="f2d03-119">So sieht die Liste der aktualisierten Pakete aus:</span><span class="sxs-lookup"><span data-stu-id="f2d03-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="f2d03-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="f2d03-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="f2d03-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="f2d03-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="f2d03-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="f2d03-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="f2d03-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="f2d03-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="f2d03-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (das Paket, nicht die Erweiterung)</span><span class="sxs-lookup"><span data-stu-id="f2d03-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="f2d03-125">Alle Änderungen</span><span class="sxs-lookup"><span data-stu-id="f2d03-125">All Changes</span></span>
<span data-ttu-id="f2d03-126">Es waren 10 in der Release behobenen Problemen.</span><span class="sxs-lookup"><span data-stu-id="f2d03-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="f2d03-127">Eine vollständige Liste der Arbeit Elemente eine feste NuGet 2.8.2, bitte Ansicht der [NuGet Issue Tracker für diese Version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="f2d03-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
