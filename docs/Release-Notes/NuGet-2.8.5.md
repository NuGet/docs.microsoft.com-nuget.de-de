---
title: Anmerkungen zur Version des NuGet-2.8.5 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 2.8.5 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-2.8.5 versionsanmerkungen aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ace56284e56f24394d49c0598ec3604b62caaf67
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="8c512-104">Anmerkungen zur Version von NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="8c512-104">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="8c512-105">[Anmerkungen zur Version des NuGet-2.8.3](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6-Versionshinweise](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="8c512-105">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="8c512-106">NuGet 2.8.5 wurde 30 März 2015 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="8c512-106">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="8c512-107">Es ist ein kleineres Update an unsere 2.8.3 VSIX mit einigen Korrekturen vorgesehen.</span><span class="sxs-lookup"><span data-stu-id="8c512-107">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="8c512-108">In dieser Version wurde die Unterstützung für Dialogfeld "NuGet-Paket-Manager" hinzugefügt, für die [DNX-Ziel-Framework-Moniker](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="8c512-108">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="8c512-109">Schließen diese neue frameworkMoniker, die unterstützt werden:</span><span class="sxs-lookup"><span data-stu-id="8c512-109">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="8c512-110">**core50** - ein 'base' Zielframeworkmoniker (TFM), die mit der zentrale CLR kompatibel ist.</span><span class="sxs-lookup"><span data-stu-id="8c512-110">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="8c512-111">**dnx452** – ein TFM spezifisch für die DNX-basierte apps, die mit der vollständigen 4.5.2 Framework-Version</span><span class="sxs-lookup"><span data-stu-id="8c512-111">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="8c512-112">**dnx46** – ein TFM bestimmte DNX-basierte apps, die mit der vollständigen 4.6 Version des Frameworks</span><span class="sxs-lookup"><span data-stu-id="8c512-112">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="8c512-113">**dnxcore50** – ein TFM bestimmte DNX-basierte apps, die mit der Core 5.0-Version des Frameworks</span><span class="sxs-lookup"><span data-stu-id="8c512-113">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="8c512-114">Ein Fehler behoben wurde, verhindert die von Paketen in FSharp Projekte ordnungsgemäß installiert:</span><span class="sxs-lookup"><span data-stu-id="8c512-114">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

<span data-ttu-id="8c512-115">https://nuget.codeplex.com/workitem/4400</span><span class="sxs-lookup"><span data-stu-id="8c512-115">https://nuget.codeplex.com/workitem/4400</span></span>