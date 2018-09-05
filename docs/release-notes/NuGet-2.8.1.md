---
title: Anmerkungen zu NuGet 2.8.1
description: Anmerkungen zu dieser Version für die Einbindung von NuGet 2.8.1 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545238"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="48cfe-103">Anmerkungen zu NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="48cfe-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="48cfe-104">[Anmerkungen zu NuGet 2.8](../release-notes/nuget-2.8.md) | [Anmerkungen zu NuGet 2.8.2](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="48cfe-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="48cfe-105">NuGet 2.8.1 wurde am 2. April 2014 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="48cfe-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="48cfe-106">Wichtige Features in der Version</span><span class="sxs-lookup"><span data-stu-id="48cfe-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="48cfe-107">Unterstützung für Windows Phone 8.1-Projekte</span><span class="sxs-lookup"><span data-stu-id="48cfe-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="48cfe-108">Diese Version unterstützt jetzt die folgenden neuen Target frameworkMoniker das Ziel Windows Phone 8.1-Projekten verwendet werden kann:</span><span class="sxs-lookup"><span data-stu-id="48cfe-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="48cfe-109">WindowsPhone81 / WP81 (für Windows Phone Silverlight-basierte Projekte)</span><span class="sxs-lookup"><span data-stu-id="48cfe-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="48cfe-110">WindowsPhoneApp81 / WPA81 (für WinRT-basierten Windows Phone-App-Projekte)</span><span class="sxs-lookup"><span data-stu-id="48cfe-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="48cfe-111">Update der NuGet WebMatrix-Erweiterung</span><span class="sxs-lookup"><span data-stu-id="48cfe-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="48cfe-112">Diese Version aktualisiert die NuGet-Client finden Sie in WebMatrix zum [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 und mit es bietet Ihnen z. B. mithilfe von XDT-Transformationen.</span><span class="sxs-lookup"><span data-stu-id="48cfe-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="48cfe-113">Noch wichtiger ist, dass die 2.6.1 Core Update ermöglicht, dem WebMatrix-Client, die NuGet-Pakete zu installieren, die neuere Versionen enthalten die `.nuspec` -Schema, das die ASP.NET NuGet-Pakete enthält.</span><span class="sxs-lookup"><span data-stu-id="48cfe-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="48cfe-114">Weitere Informationen zu dem Update der WebMatrix-Erweiterung finden Sie die speziellen [Anmerkungen zu dieser Version](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="48cfe-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="48cfe-115">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="48cfe-115">Bug Fixes</span></span>
<span data-ttu-id="48cfe-116">Neben diesen Features enthält diese Version von NuGet andere Fehlerkorrekturen.</span><span class="sxs-lookup"><span data-stu-id="48cfe-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="48cfe-117">Gab es 16 insgesamt in den Release behobenen Problemen.</span><span class="sxs-lookup"><span data-stu-id="48cfe-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="48cfe-118">Eine vollständige Liste der Arbeit Elemente eine feste NuGet 2.8.1, bitte Ansicht der [NuGet Issue Tracker für diese Version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="48cfe-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="48cfe-119">Werden mit Visual Studio "14" CTP-Version</span><span class="sxs-lookup"><span data-stu-id="48cfe-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="48cfe-120">In Visual Studio "14" CTP-Version am 3. Juni-2014 veröffentlicht wird NuGet 2.8.1 gelieferten.</span><span class="sxs-lookup"><span data-stu-id="48cfe-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="48cfe-121">Die Funktionen, die sie unterstützen bleiben in Par mit anderen 2.8.1 VSIXes wie für Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="48cfe-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
