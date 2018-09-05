---
title: Anmerkungen zu NuGet 2.8.5
description: Anmerkungen zu dieser Version für die Einbindung von NuGet 2.8.5 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548624"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="734d7-103">Anmerkungen zu NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="734d7-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="734d7-104">[Anmerkungen zu NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [Anmerkungen zu NuGet 2.8.6](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="734d7-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="734d7-105">NuGet 2.8.5 wurde am 30. März 2015 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="734d7-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="734d7-106">Es ist eine Aktualisierung für unsere 2.8.3 vorgesehen VSIX mit einigen Korrekturen.</span><span class="sxs-lookup"><span data-stu-id="734d7-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="734d7-107">In dieser Version wurde die Unterstützung für NuGet-Paket-Manager-Dialogfeld für hinzugefügt [DNX-Zielframeworkmoniker](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="734d7-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="734d7-108">Diese neue frameworkMoniker, die unterstützt werden gehören:</span><span class="sxs-lookup"><span data-stu-id="734d7-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="734d7-109">**core50** – eine "base" target frameworkMoniker (TFM), die mit der Core CLR kompatibel ist.</span><span class="sxs-lookup"><span data-stu-id="734d7-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="734d7-110">**dnx452** – ein TFM für DNX-basierter apps, die mit der vollständigen 4.5.2 Framework-Version</span><span class="sxs-lookup"><span data-stu-id="734d7-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="734d7-111">**dnx46** – ein TFM bestimmte DNX-basierte apps, die mit der vollständigen 4.6-Version des Frameworks</span><span class="sxs-lookup"><span data-stu-id="734d7-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="734d7-112">**dnxcore50** – ein TFM bestimmte DNX-basierte apps, die mit der Core 5.0-Version des Frameworks</span><span class="sxs-lookup"><span data-stu-id="734d7-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="734d7-113">Ein Fehler wurde, verhindert hat, dass die von Paketen in Projekten der FSharp ordnungsgemäße Installation von behoben:</span><span class="sxs-lookup"><span data-stu-id="734d7-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400