---
title: Anmerkungen zu dieser Version von nuget 2.8.1
description: Anmerkungen zu dieser Version von nuget 2.8.1 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776763"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="60a4e-103">Anmerkungen zu dieser Version von nuget 2.8.1</span><span class="sxs-lookup"><span data-stu-id="60a4e-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="60a4e-104">Anmerkungen zu dieser [Version von nuget 2,8](../release-notes/nuget-2.8.md)  |  [Nuget 2.8.2 Anmerkungen](../release-notes/nuget-2.8.2.md) zu dieser Version</span><span class="sxs-lookup"><span data-stu-id="60a4e-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="60a4e-105">Nuget 2.8.1 wurde am 2. April 2014 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="60a4e-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="60a4e-106">Wichtige Features in der Version</span><span class="sxs-lookup"><span data-stu-id="60a4e-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="60a4e-107">Unterstützung für Windows Phone 8,1-Projekte</span><span class="sxs-lookup"><span data-stu-id="60a4e-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="60a4e-108">In dieser Version werden nun die folgenden neuen zielframeworkmoniker unterstützt, die zum Ziel Windows Phone 8,1-Projekten verwendet werden können:</span><span class="sxs-lookup"><span data-stu-id="60a4e-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="60a4e-109">WindowsPhone81/WP81 (für Silverlight-basierte Windows Phone-Projekte)</span><span class="sxs-lookup"><span data-stu-id="60a4e-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="60a4e-110">WindowsPhoneApp81/WPA81 (für WinRT-basierte Windows Phone-App-Projekte)</span><span class="sxs-lookup"><span data-stu-id="60a4e-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="60a4e-111">Aktualisieren der nuget-webmatrix-Erweiterung</span><span class="sxs-lookup"><span data-stu-id="60a4e-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="60a4e-112">Diese Version aktualisiert den nuget-Client in webmatrix an [nuget. Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 und bietet IT-Funktionen wie xdt-Transformationen.</span><span class="sxs-lookup"><span data-stu-id="60a4e-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="60a4e-113">Noch wichtiger ist, dass das 2.6.1 Core-Update dem webmatrix-Client ermöglicht, nuget-Pakete zu installieren, die neuere Versionen des `.nuspec` Schemas enthalten, einschließlich der ASP.net nuget-Pakete.</span><span class="sxs-lookup"><span data-stu-id="60a4e-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="60a4e-114">Weitere Informationen zum Update der webmatrix-Erweiterung finden Sie in den [Anmerkungen](../release-notes/nuget-2.6.1-for-WebMatrix.md)zu dieser Version.</span><span class="sxs-lookup"><span data-stu-id="60a4e-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="60a4e-115">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="60a4e-115">Bug Fixes</span></span>
<span data-ttu-id="60a4e-116">Zusätzlich zu diesen Features enthält diese Version von nuget andere Fehlerbehebungen.</span><span class="sxs-lookup"><span data-stu-id="60a4e-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="60a4e-117">In der Version wurden 16 Gesamtprobleme behandelt.</span><span class="sxs-lookup"><span data-stu-id="60a4e-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="60a4e-118">Eine vollständige Liste der Arbeitselemente, die in nuget 2.8.1 behoben sind, finden Sie in der [nuget-Problemverfolgung für diese Version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="60a4e-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="60a4e-119">Erneute Bereitstellung mit Visual Studio "14" CTP</span><span class="sxs-lookup"><span data-stu-id="60a4e-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="60a4e-120">In Visual Studio "14" CTP, das am 3. Juni 2014 veröffentlicht wurde, wird nuget 2.8.1 in der Box ausgeliefert.</span><span class="sxs-lookup"><span data-stu-id="60a4e-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="60a4e-121">Die von ihm unterstützten Funktionen bleiben mit anderen 2.8.1-vsixes, z. b. dem für Visual Studio 2013, unverändert.</span><span class="sxs-lookup"><span data-stu-id="60a4e-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
