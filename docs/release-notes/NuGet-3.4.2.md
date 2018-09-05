---
title: Anmerkungen zu NuGet 3.4.2
description: Anmerkungen zu dieser Version für die Einbindung von NuGet 3.4.2 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549150"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="b74b9-103">Anmerkungen zu NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="b74b9-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="b74b9-104">[Anmerkungen zu NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [Anmerkungen zu NuGet 3.4.3](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="b74b9-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="b74b9-105">NuGet 3.4.2 wurde am 8. April 2016, mehrere Probleme zu beheben, die in den 3.4 und 3.4.1 identifiziert wurden veröffentlicht freizugeben.</span><span class="sxs-lookup"><span data-stu-id="b74b9-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="b74b9-106">NuGet.exe 3.4.2 RC ist jetzt verfügbar</span><span class="sxs-lookup"><span data-stu-id="b74b9-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="b74b9-107">Sie können den Release Candidate von nuget.exe 3.4.2 [hier](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="b74b9-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="b74b9-108">Updates und Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="b74b9-108">Updates and Improvements</span></span>

* <span data-ttu-id="b74b9-109">Wir haben die Leistung von Updates in ein bestimmtes Szenario, erheblich verbessert, in dem Updates für Pakete mit Tiefen Abhängigkeitsdiagrammen eine sehr lange gedauert, und nicht reagiert Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b74b9-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="b74b9-110">NuGet-Wiederherstellung ohne Netzwerkdatenverkehr ist 2,5-Mal-3-Mal schneller in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b74b9-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="b74b9-111">Zusätzlich zu dieser Änderung haben wir ein Problem behoben, in denen wurden wir das Netzwerk erreichen zweimal, wenn in der Visual Studio-Benutzeroberfläche zählen das Update abgerufen.</span><span class="sxs-lookup"><span data-stu-id="b74b9-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="b74b9-112">Dies war für einige Erfahrung im 3.4/3.4.1 Timeout Probleme Kunden teilweise verantwortlich.</span><span class="sxs-lookup"><span data-stu-id="b74b9-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="b74b9-113">Unterstützung für die Einstellung für "no_proxy"</span><span class="sxs-lookup"><span data-stu-id="b74b9-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="b74b9-114">Fehlerbehebungen</span><span class="sxs-lookup"><span data-stu-id="b74b9-114">Fixes</span></span>

* <span data-ttu-id="b74b9-115">Wurde "NuGet.org" Quelle nach der Aktualisierung auf 3.4.1 im NuGet-Einstellungen oder der Konfiguration fehlt behoben ein Problem.</span><span class="sxs-lookup"><span data-stu-id="b74b9-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="b74b9-116">Ein Problem behoben, in dem eine Änderung zur Groß-und Kleinschreibung zu FindPackagesById 3.4.1 Artifactory unterbrochen.</span><span class="sxs-lookup"><span data-stu-id="b74b9-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="b74b9-117">Ein Problem mit FIPS, die aufgrund von Fehlern bei der NuGet-Wiederherstellung von nuget.exe korrigiert.</span><span class="sxs-lookup"><span data-stu-id="b74b9-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="b74b9-118">Korrektur eines Absturzes, beim Durchsuchen von Datenquellen mit ungültige Symbol-URL.</span><span class="sxs-lookup"><span data-stu-id="b74b9-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="b74b9-119">Korrigiert: Probleme mit dem Zusammenführen von Versionen und Einträge aus "Alle Quellen".</span><span class="sxs-lookup"><span data-stu-id="b74b9-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="b74b9-120">Bekannte Probleme in 3.4.2 X86-Windows-Befehlszeile (RC)</span><span class="sxs-lookup"><span data-stu-id="b74b9-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="b74b9-121">Diese Probleme werden die Anfang der nächsten Woche vor der stoßen wir auf die RTM-Version behoben werden.</span><span class="sxs-lookup"><span data-stu-id="b74b9-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="b74b9-122">Ausgeführte Nuget-Wiederherstellung in einer Projektmappe fehl, wenn in einer niedrigeren Ordnerhierarchie als die Projektdateien die Projektmappendatei platziert wird.</span><span class="sxs-lookup"><span data-stu-id="b74b9-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="b74b9-123">Ausführen von Nuget-Delete-Befehl für ein Paket mit dem V2-Feed schlägt fehl.</span><span class="sxs-lookup"><span data-stu-id="b74b9-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="b74b9-124">Verwenden Sie stattdessen V3-Feeds.</span><span class="sxs-lookup"><span data-stu-id="b74b9-124">Use V3 feed instead.</span></span>


<span data-ttu-id="b74b9-125">Die vollständige Liste der Korrekturen und Verbesserungen in dieser Version, sehen Sie sich die Liste der Probleme [hier](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="b74b9-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>