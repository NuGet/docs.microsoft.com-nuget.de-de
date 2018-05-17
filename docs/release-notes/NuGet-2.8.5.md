---
title: Anmerkungen zur Version von NuGet 2.8.5
description: Versionshinweise für NuGet 2.8.5 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="611d1-103">Anmerkungen zur Version von NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="611d1-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="611d1-104">[Anmerkungen zur Version des NuGet-2.8.3](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6-Versionshinweise](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="611d1-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="611d1-105">NuGet 2.8.5 wurde 30 März 2015 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="611d1-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="611d1-106">Es ist ein kleineres Update an unsere 2.8.3 VSIX mit einigen Korrekturen vorgesehen.</span><span class="sxs-lookup"><span data-stu-id="611d1-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="611d1-107">In dieser Version wurde die Unterstützung für Dialogfeld "NuGet-Paket-Manager" hinzugefügt, für die [DNX-Ziel-Framework-Moniker](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="611d1-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="611d1-108">Schließen diese neue frameworkMoniker, die unterstützt werden:</span><span class="sxs-lookup"><span data-stu-id="611d1-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="611d1-109">**core50** - ein 'base' Zielframeworkmoniker (TFM), die mit der zentrale CLR kompatibel ist.</span><span class="sxs-lookup"><span data-stu-id="611d1-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="611d1-110">**dnx452** – ein TFM spezifisch für die DNX-basierte apps, die mit der vollständigen 4.5.2 Framework-Version</span><span class="sxs-lookup"><span data-stu-id="611d1-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="611d1-111">**dnx46** – ein TFM bestimmte DNX-basierte apps, die mit der vollständigen 4.6 Version des Frameworks</span><span class="sxs-lookup"><span data-stu-id="611d1-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="611d1-112">**dnxcore50** – ein TFM bestimmte DNX-basierte apps, die mit der Core 5.0-Version des Frameworks</span><span class="sxs-lookup"><span data-stu-id="611d1-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="611d1-113">Ein Fehler behoben wurde, verhindert die von Paketen in FSharp Projekte ordnungsgemäß installiert:</span><span class="sxs-lookup"><span data-stu-id="611d1-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400