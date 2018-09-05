---
title: Anmerkungen dieser Version von NuGet 3.0 RC
description: Anmerkungen zu NuGet 3.0 RC, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551718"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="f3c59-103">Anmerkungen dieser Version von NuGet 3.0 RC</span><span class="sxs-lookup"><span data-stu-id="f3c59-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="f3c59-104">[Anmerkungen zu NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 – Versionshinweise](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="f3c59-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="f3c59-105">NuGet 3.0 RC wurde mit dem Visual Studio 2015 RC-Release vom 29. April 2015 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="f3c59-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="f3c59-106">Diese Version enthält eine Reihe von wichtiger Programmfehlerbehebungen, leistungsverbesserungen und Upgrades zur Unterstützung der neuen Frameworks.</span><span class="sxs-lookup"><span data-stu-id="f3c59-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="f3c59-107">Es ist nur für Visual Studio 2015 verfügbar.</span><span class="sxs-lookup"><span data-stu-id="f3c59-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="f3c59-108">Mittelpunkt und Leistung</span><span class="sxs-lookup"><span data-stu-id="f3c59-108">Continued Focus on Performance</span></span>

<span data-ttu-id="f3c59-109">Stabilität und Leistung von Abfragen von NuGet weiterhin ein wichtiges Thema, dem auf konzentrieren wir uns sind.</span><span class="sxs-lookup"><span data-stu-id="f3c59-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="f3c59-110">In dieser Version sollten Sie beginnen, um sehr schnelle Suchvorgänge in der NuGet UI und die Website anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="f3c59-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="f3c59-111">Wird überwacht der Dienst und wie Sie den Dienst verwenden, damit wir optimieren diese Vorgänge fortgesetzt werden kann.</span><span class="sxs-lookup"><span data-stu-id="f3c59-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="f3c59-112">Wichtige Probleme gelöst wurden</span><span class="sxs-lookup"><span data-stu-id="f3c59-112">Significant Issues Resolved</span></span>

<span data-ttu-id="f3c59-113">Um die NuGet-Clients zu stabilisieren, behoben wir viele Probleme, als Teil dieses Release.</span><span class="sxs-lookup"><span data-stu-id="f3c59-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="f3c59-114">Hier ist nur eine kurze Liste einiger wichtiger Probleme behoben:</span><span class="sxs-lookup"><span data-stu-id="f3c59-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="f3c59-115">Im Rahmen der Umbenennung von K-Framework für ASP.NET 5, frameworkMoniker aktualisiert, um das Verarbeiten von Dnx und Dnxcore [Link](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="f3c59-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="f3c59-116">In der Hilfe zu über Links im Visual Studio-Benutzeroberfläche hinzugefügt [Link](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="f3c59-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="f3c59-117">Bessere Behandlung von komplexen Verweise in `.nuspec` mit durch Trennzeichen getrennte frameworkverweise [Link](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="f3c59-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="f3c59-118">Unterstützung für japanische Kulturen festen [Link](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="f3c59-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="f3c59-119">Aktualisierten Client, um neue v3-Endpunkte verwenden, die ASP.NET 5-Projekte ermöglichen [Link](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="f3c59-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="f3c59-120">Ordner "Pakete" aktualisiert und eine bessere Handle in die quellcodeverwaltung [Link](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="f3c59-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="f3c59-121">Unterstützung für satellitenpakete festen [Link](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="f3c59-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="f3c59-122">Unterstützung für Inhaltsdateien frameworkspezifische korrigiert [Link](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="f3c59-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="f3c59-123">Überarbeitung der GitHub-Präsenz</span><span class="sxs-lookup"><span data-stu-id="f3c59-123">GitHub presence overhaul</span></span>

<span data-ttu-id="f3c59-124">Wir haben einige Änderungen an unseren [source auf GitHub-Repositorys](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="f3c59-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="f3c59-125">Wenn Sie Probleme mit NuGet Visual Studio-Client, der Powershell-Befehle oder der Befehlszeile haben ausführbare können Sie diese Probleme zu melden und ihren Fortschritt überwachen unsere [Startseite des GitHub-Repository-Problemliste](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="f3c59-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="f3c59-126">Verfolgen wir Probleme für den Katalog in unserer [Repository von GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="f3c59-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="f3c59-127">Bleiben Sie dran</span><span class="sxs-lookup"><span data-stu-id="f3c59-127">Stay Tuned</span></span>

<span data-ttu-id="f3c59-128">Bitte achten Sie auf [unseren Blog](http://blog.nuget.org) für die weitere Bearbeitung sowie Ankündigungen von NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="f3c59-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>