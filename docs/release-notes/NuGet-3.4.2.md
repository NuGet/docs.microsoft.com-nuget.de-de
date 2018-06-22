---
title: Anmerkungen zur Version von NuGet 3.4.2
description: Versionshinweise für NuGet 3.4.2 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 88d29a84e280433663ab6c1c04ae16e1329420f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819665"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="a59b1-103">Anmerkungen zur Version von NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="a59b1-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="a59b1-104">[Anmerkungen zur Version des NuGet-3.4.1](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3-Versionshinweise](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="a59b1-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="a59b1-105">NuGet 3.4.2 am 8. April 2016, um mehrere Probleme zu beheben, die in den 3.4 und 3.4.1 identifiziert wurden veröffentlicht wurde freigegeben.</span><span class="sxs-lookup"><span data-stu-id="a59b1-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="a59b1-106">NuGet.exe 3.4.2 RC ist jetzt verfügbar</span><span class="sxs-lookup"><span data-stu-id="a59b1-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="a59b1-107">Sie können dem Release Candidate von nuget.exe 3.4.2 herunterladen [hier](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="a59b1-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="a59b1-108">Updates und Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="a59b1-108">Updates and Improvements</span></span>

* <span data-ttu-id="a59b1-109">Wir haben die Leistung von Updates in einem bestimmten Szenario erheblich verbessert, in dem Updates für die Pakete mit umfassenden Abhängigkeitsdiagramme sehr lange dauerte und nicht reagiert Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a59b1-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="a59b1-110">NuGet Restore ohne Netzwerkdatenverkehr ist 2.5 x – 3 X schneller innerhalb von Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a59b1-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="a59b1-111">Zusätzlich zu dieser Änderung haben wir das Problem behoben, in denen wurden wir im Netzwerk Erreichens zweimal beim Abrufen des Updates in der Visual Studio-Benutzeroberfläche zu zählen.</span><span class="sxs-lookup"><span data-stu-id="a59b1-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="a59b1-112">Dies war teilweise für einige Erfahrung im 3.4/3.4.1 Timeout Probleme Kunden verantwortlich.</span><span class="sxs-lookup"><span data-stu-id="a59b1-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="a59b1-113">Unterstützung für No_proxy-Einstellung</span><span class="sxs-lookup"><span data-stu-id="a59b1-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="a59b1-114">Fehlerbehebungen</span><span class="sxs-lookup"><span data-stu-id="a59b1-114">Fixes</span></span>

* <span data-ttu-id="a59b1-115">Ein Problem behoben, bei denen war nuget.org Quelle nach dem Update auf 3.4.1 im NuGet-Einstellungen oder der Konfiguration fehlt.</span><span class="sxs-lookup"><span data-stu-id="a59b1-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="a59b1-116">Ein Problem behoben, in denen eine Änderung Schreibweise FindPackagesById in 3.4.1 Artifactory unterbrochen.</span><span class="sxs-lookup"><span data-stu-id="a59b1-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="a59b1-117">Beheben Sie ein Problem mit FIPS, die NuGet-Wiederherstellung mit nuget.exe Fehler verursacht hat.</span><span class="sxs-lookup"><span data-stu-id="a59b1-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="a59b1-118">Korrektur eines Absturzes, wenn Sie Quellen mit Symbol "ungültig" URL zu durchsuchen.</span><span class="sxs-lookup"><span data-stu-id="a59b1-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="a59b1-119">Behobene Probleme mit dem Zusammenführen von Versionen und Einträge aus "Alle Quellen".</span><span class="sxs-lookup"><span data-stu-id="a59b1-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="a59b1-120">Bekannte Probleme in 3.4.2 Windows X86 Commandline (RC)</span><span class="sxs-lookup"><span data-stu-id="a59b1-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="a59b1-121">Diese Probleme werden die Anfang der nächsten Woche bevor wir RTM erreicht behoben werden.</span><span class="sxs-lookup"><span data-stu-id="a59b1-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="a59b1-122">Ausgeführte NuGet-Wiederherstellung zu einem Lösungsvorschlag schlägt fehl, wenn die Projektmappendatei, die in einer niedrigeren Ordnerhierarchie als die Projektdateien platziert wird.</span><span class="sxs-lookup"><span data-stu-id="a59b1-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="a59b1-123">NuGet-Delete-Befehl wird für ein Paket mit dem Feed V2 ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="a59b1-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="a59b1-124">Verwenden Sie stattdessen V3-Feeds.</span><span class="sxs-lookup"><span data-stu-id="a59b1-124">Use V3 feed instead.</span></span>


<span data-ttu-id="a59b1-125">Die vollständige Liste der Korrekturen und Verbesserungen in dieser Version, sehen Sie sich die Liste der Probleme [hier](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="a59b1-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>