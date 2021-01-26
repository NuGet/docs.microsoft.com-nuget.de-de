---
title: Nuget 2.8.2 Anmerkungen zu dieser Version
description: Anmerkungen zu dieser Version von nuget 2.8.2 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780366"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="02ec5-103">Nuget 2.8.2 Anmerkungen zu dieser Version</span><span class="sxs-lookup"><span data-stu-id="02ec5-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="02ec5-104">Anmerkungen zu dieser [Version von nuget 2.8.1](../release-notes/nuget-2.8.1.md)  |  [Nuget 2.8.3 Anmerkungen](../release-notes/nuget-2.8.3.md) zu dieser Version</span><span class="sxs-lookup"><span data-stu-id="02ec5-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="02ec5-105">Nuget 2.8.2 wurde am 22. Mai 2014 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="02ec5-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="02ec5-106">Diese Version enthielt nur Änderungen an der Befehlszeile nuget.exe, das nuget. Server-Paket und andere nuget-Pakete.</span><span class="sxs-lookup"><span data-stu-id="02ec5-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="02ec5-107">Das Release enthielt keine aktualisierte Visual Studio-Erweiterung oder webmatrix-Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="02ec5-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="02ec5-108">Relevante Updates</span><span class="sxs-lookup"><span data-stu-id="02ec5-108">Notable Updates</span></span>

<span data-ttu-id="02ec5-109">Die bemerkenswertesten Updates waren in der nuget.exe-Befehlszeile und im nuget. Server-Paket (bei selbstgeh osteten nuget-Feeds).</span><span class="sxs-lookup"><span data-stu-id="02ec5-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="02ec5-110">Wichtige nuget.exe Fehlerbehebungen</span><span class="sxs-lookup"><span data-stu-id="02ec5-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="02ec5-111">nuget.exe Push schlägt fehl und führt einen Wiederholungsversuch durch.</span><span class="sxs-lookup"><span data-stu-id="02ec5-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="02ec5-112">nuget.exe Push sendet die grundlegenden Authentifizierungs Anmelde Informationen nicht ordnungsgemäß.</span><span class="sxs-lookup"><span data-stu-id="02ec5-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="02ec5-113">nuget.exe Push folgt nicht der temporären Umleitung</span><span class="sxs-lookup"><span data-stu-id="02ec5-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="02ec5-114">Wichtige Fehlerbehebung für nuget. Server</span><span class="sxs-lookup"><span data-stu-id="02ec5-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="02ec5-115">Der von "nuget. Server" zurückgegebene falsche Wert von "isabsolutelatestversion".</span><span class="sxs-lookup"><span data-stu-id="02ec5-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="02ec5-116">Aktualisierte Pakete</span><span class="sxs-lookup"><span data-stu-id="02ec5-116">Packages Updated</span></span>

<span data-ttu-id="02ec5-117">Die nuget.exe-Befehlszeilen-und nuget. Server-Fehlerbehebungen werden als nuget-Paket Aktualisierungen ausgeliefert.</span><span class="sxs-lookup"><span data-stu-id="02ec5-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="02ec5-118">Es wurden auch andere Pakete mit 2.8.2 aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="02ec5-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="02ec5-119">Im folgenden finden Sie die Liste der aktualisierten Pakete:</span><span class="sxs-lookup"><span data-stu-id="02ec5-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="02ec5-120">Nuget. Core</span><span class="sxs-lookup"><span data-stu-id="02ec5-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="02ec5-121">"Nuget. CommandLine"</span><span class="sxs-lookup"><span data-stu-id="02ec5-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="02ec5-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="02ec5-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="02ec5-123">Nuget. Build</span><span class="sxs-lookup"><span data-stu-id="02ec5-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="02ec5-124">[Nuget. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (das Paket, nicht die Erweiterung)</span><span class="sxs-lookup"><span data-stu-id="02ec5-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="02ec5-125">Alle Änderungen</span><span class="sxs-lookup"><span data-stu-id="02ec5-125">All Changes</span></span>
<span data-ttu-id="02ec5-126">In der Version wurden 10 Probleme behoben.</span><span class="sxs-lookup"><span data-stu-id="02ec5-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="02ec5-127">Eine vollständige Liste der Arbeitselemente, die in nuget-2.8.2 korrigiert sind, finden Sie in der [nuget-Problemverfolgung für diese Version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="02ec5-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
