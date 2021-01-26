---
title: Nuget 2.8.5 Anmerkungen zu dieser Version
description: Anmerkungen zu dieser Version von nuget 2.8.5 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780353"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="1a354-103">Nuget 2.8.5 Anmerkungen zu dieser Version</span><span class="sxs-lookup"><span data-stu-id="1a354-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="1a354-104">[Nuget 2.8.3 Anmerkungen](../release-notes/nuget-2.8.3.md)  |  zu dieser Version [Nuget 2.8.6 Anmerkungen](../release-notes/nuget-2.8.6.md) zu dieser Version</span><span class="sxs-lookup"><span data-stu-id="1a354-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="1a354-105">Nuget 2.8.5 wurde am 30. März 2015 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="1a354-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="1a354-106">Es handelt sich um ein kleineres Update für unsere 2.8.3 VSIX mit einigen gezielten Korrekturen.</span><span class="sxs-lookup"><span data-stu-id="1a354-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="1a354-107">In dieser Version wurde das Dialogfeld Unterstützung für den nuget-Paket-Manager für [DNX-zielframeworkmoniker](https://github.com/aspnet/dnx)hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="1a354-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="1a354-108">Zu diesen neuen frameworkmonikern, die unterstützt werden, gehören:</span><span class="sxs-lookup"><span data-stu-id="1a354-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="1a354-109">**core50** -ein Base-FrameworkMoniker (Target Framework Moniker, TFM), der mit der Core CLR kompatibel ist.</span><span class="sxs-lookup"><span data-stu-id="1a354-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="1a354-110">**dnx452** -ein für DNX-basierte apps spezifischer TFM-Code, der die vollständige 4.5.2-Version des Frameworks verwendet.</span><span class="sxs-lookup"><span data-stu-id="1a354-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="1a354-111">**dnx46** -ein für DNX-basierte apps spezifischer TFM-Code, der die Vollversion 4,6 des Frameworks verwendet.</span><span class="sxs-lookup"><span data-stu-id="1a354-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="1a354-112">**dnxcore50** -ein für DNX-basierte apps spezifischer TFM-Code, der die Core 5,0-Version des Frameworks verwendet</span><span class="sxs-lookup"><span data-stu-id="1a354-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="1a354-113">Ein Fehler wurde behoben, der verhindert hat, dass Pakete ordnungsgemäß in FSharp-Projekte installiert wurden:</span><span class="sxs-lookup"><span data-stu-id="1a354-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400