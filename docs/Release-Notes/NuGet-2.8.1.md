---
title: Anmerkungen zur Version von NuGet 2.8.1
description: Versionshinweise für NuGet 2.8.1 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8787aee36d31ed5d8071b35a8c243823029d135f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="a4933-103">Anmerkungen zur Version von NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="a4933-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="a4933-104">[Anmerkungen zur Version von NuGet 2.8](../release-notes/nuget-2.8.md) | [NuGet 2.8.2-Versionshinweise](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="a4933-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="a4933-105">NuGet 2.8.1 wurde am 2. April 2014 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="a4933-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="a4933-106">Wichtige Funktionen in der Version</span><span class="sxs-lookup"><span data-stu-id="a4933-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="a4933-107">Unterstützung für Windows Phone 8.1-Projekte</span><span class="sxs-lookup"><span data-stu-id="a4933-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="a4933-108">Diese Version unterstützt jetzt die folgenden neuen Ziel frameworkMoniker das Ziel Windows Phone 8.1-Projekte verwendet werden kann:</span><span class="sxs-lookup"><span data-stu-id="a4933-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="a4933-109">WindowsPhone81 / WP81 (für Windows Phone Silverlight-basierte Projekte)</span><span class="sxs-lookup"><span data-stu-id="a4933-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="a4933-110">WindowsPhoneApp81 / WPA81 (für Windows Phone-App WinRT-basierte Projekte)</span><span class="sxs-lookup"><span data-stu-id="a4933-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="a4933-111">Update der WebMatrix-Erweiterung von NuGet</span><span class="sxs-lookup"><span data-stu-id="a4933-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="a4933-112">Diese Version aktualisiert, die NuGet-Client finden in WebMatrix zum [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 und schaltet sie Funktionen wie z. B. XDT Transformationen mit.</span><span class="sxs-lookup"><span data-stu-id="a4933-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="a4933-113">Vor allem die 2.6.1 Core Update ermöglicht dem WebMatrix-Client, die NuGet-Pakete installieren, die neuere Versionen enthalten die `.nuspec` Schema, d. h. die ASP.NET NuGet-Pakete enthält.</span><span class="sxs-lookup"><span data-stu-id="a4933-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="a4933-114">Weitere Informationen zu dem Update WebMatrix-Erweiterung finden Sie unter die speziellen [Anmerkungen zu dieser Version](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="a4933-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="a4933-115">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="a4933-115">Bug Fixes</span></span>
<span data-ttu-id="a4933-116">Zusätzlich zu diesen Features enthält diese Version von NuGet Weitere Fehlerkorrekturen.</span><span class="sxs-lookup"><span data-stu-id="a4933-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="a4933-117">Es gab 16 insgesamt Probleme, die in der Version behoben.</span><span class="sxs-lookup"><span data-stu-id="a4933-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="a4933-118">Eine vollständige Liste der Arbeit Artikel feste in NuGet 2.8.1, bitte Ansicht der [NuGet Issue Tracker für diese Version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="a4933-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="a4933-119">Mit Visual Studio reshipping "14" CTP</span><span class="sxs-lookup"><span data-stu-id="a4933-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="a4933-120">In Visual Studio "14" CTP 3. 2014 Juni veröffentlicht ist NuGet 2.8.1 dem Produkt ausgeliefert.</span><span class="sxs-lookup"><span data-stu-id="a4933-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="a4933-121">Funktionen, die sie unterstützen, bleiben in Par mit anderen 2.8.1 VSIXes wie für Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="a4933-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
