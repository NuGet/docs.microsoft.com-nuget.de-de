---
title: Nuget 3.4.2 Anmerkungen zu dieser Version
description: Anmerkungen zu dieser Version von nuget 3.4.2 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780250"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="d0996-103">Nuget 3.4.2 Anmerkungen zu dieser Version</span><span class="sxs-lookup"><span data-stu-id="d0996-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="d0996-104">Anmerkungen zu nuget- [Version 3.4.1](../release-notes/nuget-3.4.1.md)  |  [Nuget 3.4.3 Anmerkungen](../release-notes/nuget-3.4.3.md) zu dieser Version</span><span class="sxs-lookup"><span data-stu-id="d0996-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="d0996-105">Nuget 3.4.2 wurde am 8. April 2016 veröffentlicht, um verschiedene Probleme zu beheben, die in der Version 3,4 und 3.4.1 identifiziert wurden.</span><span class="sxs-lookup"><span data-stu-id="d0996-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="d0996-106">nuget.exe 3.4.2 RC ist jetzt verfügbar.</span><span class="sxs-lookup"><span data-stu-id="d0996-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="d0996-107">Sie können den Release Candidate nuget.exe 3.4.2 [hier](https://dist.nuget.org/index.html)herunterladen.</span><span class="sxs-lookup"><span data-stu-id="d0996-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="d0996-108">Updates und Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="d0996-108">Updates and Improvements</span></span>

* <span data-ttu-id="d0996-109">Wir haben die Leistung von Updates in einem bestimmten Szenario erheblich verbessert, bei dem Updates von Paketen mit Deep-Abhängigkeits Diagrammen sehr lange gedauert haben und Visual Studio nicht reagiert haben.</span><span class="sxs-lookup"><span data-stu-id="d0996-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="d0996-110">die nuget-Wiederherstellung ohne Netzwerk Datenverkehr erfolgt in Visual Studio 2,5 x – 3X schneller.</span><span class="sxs-lookup"><span data-stu-id="d0996-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="d0996-111">Zusätzlich zu dieser Änderung haben wir ein Problem behoben, bei dem das Netzwerk zweimal beim Abrufen der Update Anzahl in der vs-Benutzeroberfläche aufgetreten ist.</span><span class="sxs-lookup"><span data-stu-id="d0996-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="d0996-112">Dies war teilweise verantwortlich für einige Timeout Probleme, die Kunden in 3.4/3.4.1 hatten.</span><span class="sxs-lookup"><span data-stu-id="d0996-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="d0996-113">Unterstützung für no_proxy Einstellung hinzugefügt</span><span class="sxs-lookup"><span data-stu-id="d0996-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="d0996-114">Fehlerbehebungen</span><span class="sxs-lookup"><span data-stu-id="d0996-114">Fixes</span></span>

* <span data-ttu-id="d0996-115">Es wurde ein Problem behoben, bei dem nuget.org source in den nuget-Einstellungen oder-Konfigurationen nach dem Aktualisieren auf 3.4.1 fehlt.</span><span class="sxs-lookup"><span data-stu-id="d0996-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="d0996-116">Es wurde ein Problem behoben, bei dem eine Änderung der Groß-/Kleinschreibung von "findpackagesbyid" in 3.4.1 in</span><span class="sxs-lookup"><span data-stu-id="d0996-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="d0996-117">Es wurde ein Problem mit dem Fehler behoben, das eine nuget-Wiederherstellung mit nuget.exe verursacht hat.</span><span class="sxs-lookup"><span data-stu-id="d0996-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="d0996-118">Beim Durchsuchen von Quellen mit ungültiger Symbol-URL wurde ein Absturz korrigiert.</span><span class="sxs-lookup"><span data-stu-id="d0996-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="d0996-119">Behobene Probleme beim Zusammenführen von Versionen und Einträgen aus "alle Quellen".</span><span class="sxs-lookup"><span data-stu-id="d0996-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="d0996-120">Bekannte Probleme in 3.4.2 Windows x86 commandline (RC)</span><span class="sxs-lookup"><span data-stu-id="d0996-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="d0996-121">Diese Probleme werden frühzeitig in der nächsten Woche behoben, bevor RTM getroffen wird.</span><span class="sxs-lookup"><span data-stu-id="d0996-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="d0996-122">Das Ausführen der nuget-Wiederherstellung für eine Lösung schlägt fehl, wenn die Projektmappendatei in einer niedrigeren Ordnerhierarchie platziert wird als die Projektdateien.</span><span class="sxs-lookup"><span data-stu-id="d0996-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="d0996-123">Das Ausführen des Befehls "nuget löschen" für ein Paket mit dem V2-Feed schlägt fehl.</span><span class="sxs-lookup"><span data-stu-id="d0996-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="d0996-124">Verwenden Sie stattdessen den V3-Feed.</span><span class="sxs-lookup"><span data-stu-id="d0996-124">Use V3 feed instead.</span></span>


<span data-ttu-id="d0996-125">Eine umfassende Liste der Fehlerbehebungen und Verbesserungen in dieser Version finden Sie in der Liste [der Probleme.](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)</span><span class="sxs-lookup"><span data-stu-id="d0996-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>