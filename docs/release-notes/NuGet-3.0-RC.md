---
title: Anmerkungen zu dieser Version von nuget 3,0 RC
description: Anmerkungen zu dieser Version von nuget 3,0 RC, einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776579"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="08b28-103">Anmerkungen zu dieser Version von nuget 3,0 RC</span><span class="sxs-lookup"><span data-stu-id="08b28-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="08b28-104">Anmerkungen zu dieser [Version von nuget 3,0 Beta](../release-notes/nuget-3.0-beta.md)  |  [Anmerkungen zu dieser Version von nuget 3,0 rc2](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="08b28-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="08b28-105">Nuget 3,0 RC wurde am 29. April 2015 mit der Version von Visual Studio 2015 RC veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="08b28-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="08b28-106">Diese Version enthält eine Reihe wichtiger Programmfehler Behebungen, Leistungsverbesserungen und Updates, um die neuen Frameworks zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="08b28-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="08b28-107">Er ist nur für Visual Studio 2015 verfügbar.</span><span class="sxs-lookup"><span data-stu-id="08b28-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="08b28-108">Fortsetzen des Fokus auf die Leistung</span><span class="sxs-lookup"><span data-stu-id="08b28-108">Continued Focus on Performance</span></span>

<span data-ttu-id="08b28-109">Die Stabilität und Leistung von nuget-Abfragen ist weiterhin ein heißes Thema, auf das wir uns konzentrieren.</span><span class="sxs-lookup"><span data-stu-id="08b28-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="08b28-110">Mit dieser Version sollten Sie sehr schnelle Suchvorgänge in der nuget-Benutzeroberfläche und-Website sehen.</span><span class="sxs-lookup"><span data-stu-id="08b28-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="08b28-111">Wir überwachen den Dienst und die Verwendung des Dienstanbieter, damit wir diese Vorgänge weiterhin optimieren können.</span><span class="sxs-lookup"><span data-stu-id="08b28-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="08b28-112">Wichtige Probleme gelöst</span><span class="sxs-lookup"><span data-stu-id="08b28-112">Significant Issues Resolved</span></span>

<span data-ttu-id="08b28-113">Um die nuget-Clients zu stabilisieren, haben wir viele Probleme im Rahmen dieser Version gelöst.</span><span class="sxs-lookup"><span data-stu-id="08b28-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="08b28-114">Im folgenden finden Sie eine kurze Liste einiger wichtiger Probleme, die behoben wurden:</span><span class="sxs-lookup"><span data-stu-id="08b28-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="08b28-115">Im Rahmen der Umbenennung des K-Frameworks für ASP.net 5 wurden FrameworkMoniker aktualisiert, um den [Link](https://github.com/NuGet/Home/issues/215) DNX und dnxcore zu behandeln.</span><span class="sxs-lookup"><span data-stu-id="08b28-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="08b28-116">Hilfe Dokumentation von Links im Visual Studio-UI- [Link](https://github.com/NuGet/Home/issues/232) hinzugefügt</span><span class="sxs-lookup"><span data-stu-id="08b28-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="08b28-117">Bessere Behandlung komplexer Verweise in `.nuspec` mit durch Trennzeichen getrennten frameworkverweis- [Links](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="08b28-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="08b28-118">Unterstützung für den [Link](https://github.com/NuGet/Home/issues/253) "japanische Kulturen" korrigiert</span><span class="sxs-lookup"><span data-stu-id="08b28-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="08b28-119">Aktualisierter Client, damit ASP.net 5 Projekte den [Link](https://github.com/NuGet/Home/issues/219) "neue V3-Endpunkte" verwenden können</span><span class="sxs-lookup"><span data-stu-id="08b28-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="08b28-120">Das Thema wurde aktualisiert, um den Paket Ordner [](https://github.com/NuGet/Home/issues/56) mit der Quell Code Verwaltung besser</span><span class="sxs-lookup"><span data-stu-id="08b28-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="08b28-121">Unterstützung für den [Link](https://github.com/NuGet/Home/issues/17) "Satelliten Pakete" korrigiert</span><span class="sxs-lookup"><span data-stu-id="08b28-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="08b28-122">Unterstützung für frameworkspezifische [Inhalts Dateien korrigiert](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="08b28-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="08b28-123">GitHub-Anwesenheits Überprüfung</span><span class="sxs-lookup"><span data-stu-id="08b28-123">GitHub presence overhaul</span></span>

<span data-ttu-id="08b28-124">Wir haben einige Änderungen an den [Quell Code Depots auf GitHub](http://github.com/nuget/home)vorgenommen.</span><span class="sxs-lookup"><span data-stu-id="08b28-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="08b28-125">Wenn Sie Probleme mit dem nuget-Visual Studio-Client, den PowerShell-Befehlen oder der ausführbaren Befehlszeilen Datei haben, können Sie diese Probleme protokollieren und ihren Fortschritt in unserer [GitHub-Home-Repository-Liste "Probleme](http://github.com/nuget/home/issues)" überwachen.</span><span class="sxs-lookup"><span data-stu-id="08b28-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="08b28-126">Wir verfolgen Probleme für den Katalog in unserem [GitHub nugetgallery-Repository](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="08b28-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="08b28-127">Bleiben Sie dran</span><span class="sxs-lookup"><span data-stu-id="08b28-127">Stay Tuned</span></span>

<span data-ttu-id="08b28-128">Im [Blog](http://blog.nuget.org) erhalten Sie weitere Informationen zum Fortschritt und Ankündigungen für nuget 3,0!</span><span class="sxs-lookup"><span data-stu-id="08b28-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>