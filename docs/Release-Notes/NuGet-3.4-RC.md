---
title: NuGet 3.4-RC-Versionsanmerkungen | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 239d3d95-5a72-4fac-8389-b6deac27884d
description: "Versionshinweise für NuGet 3.4 RC einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet 3.4 RC-versionsanmerkungen, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 86c37d516eede2ac5e6e5e842f687a8f3b17c0a4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="7955d-104">NuGet 3.4-RC-Versionsanmerkungen</span><span class="sxs-lookup"><span data-stu-id="7955d-104">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="7955d-105">[Anmerkungen zur Version des NuGet-3.3](../release-notes/nuget-3.3.md) | [NuGet 3.4-Versionshinweise](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="7955d-105">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="7955d-106">NuGet 3.4-RC am 3. März 2016 zusammen mit Visual Studio 2015 Update 2 RC veröffentlicht wurde und mit wenigen Grundsätze in Köpfen erstellt wurde:</span><span class="sxs-lookup"><span data-stu-id="7955d-106">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

*  <span data-ttu-id="7955d-107">Plattformübergreifende Unterstützung</span><span class="sxs-lookup"><span data-stu-id="7955d-107">Cross-Platform support</span></span>
*  <span data-ttu-id="7955d-108">Leistungsverbesserungen</span><span class="sxs-lookup"><span data-stu-id="7955d-108">Performance improvements</span></span>
*  <span data-ttu-id="7955d-109">Kleinere Verbesserungen der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="7955d-109">Minor UI improvements</span></span>

<span data-ttu-id="7955d-110">Die folgenden Funktionen stehen in dieser RC mit mehr für die 3.4 endgültige Version geplant wurde.</span><span class="sxs-lookup"><span data-stu-id="7955d-110">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="7955d-111">Neue Funktionen</span><span class="sxs-lookup"><span data-stu-id="7955d-111">New Features</span></span>

* <span data-ttu-id="7955d-112">NuGet-Clients unterstützen jetzt Gzip-inhaltscodierung von Repositorys</span><span class="sxs-lookup"><span data-stu-id="7955d-112">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="7955d-113">Unterstützung für die PDB-Dateien von Paketen in Xproj-Projekten</span><span class="sxs-lookup"><span data-stu-id="7955d-113">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="7955d-114">Unterstützung für IOS- und Android-Buildvorgänge im inhaltsdateienelement</span><span class="sxs-lookup"><span data-stu-id="7955d-114">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="7955d-115">Unterstützung für die netstandard- und Netstandardapp-frameworkMoniker</span><span class="sxs-lookup"><span data-stu-id="7955d-115">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="7955d-116">Neue Features der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="7955d-116">New User Interface Features</span></span>

* <span data-ttu-id="7955d-117">Signifikante leistungsverbesserungen besonders auf den Registerkarten installiert, Updates und konsolidieren</span><span class="sxs-lookup"><span data-stu-id="7955d-117">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="7955d-118">Installiert und Updates Registerkarten sind jetzt alphabetisch sortiert</span><span class="sxs-lookup"><span data-stu-id="7955d-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="7955d-119">Schaltfläche "Aktualisieren", die eine zu aktualisierende-Suche erlaubt hinzugefügt</span><span class="sxs-lookup"><span data-stu-id="7955d-119">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="7955d-120">Updates und Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="7955d-120">Updates and Improvements</span></span>

* <span data-ttu-id="7955d-121">Pakete, die auf die verwiesen wird `project.json` , auf denen eine Gleitkommazahl-Version wird nicht auf jedem Build aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="7955d-121">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="7955d-122">Stattdessen werden sie aktualisieren nur, wenn Sie gezwungen, wiederherzustellen, bereinigen, neu erstellen oder ändern Sie `project.json`.</span><span class="sxs-lookup"><span data-stu-id="7955d-122">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="7955d-123">Bei Verwendung der NuGet-Konfigurations-UI nicht mehr NuGet.org Repository Quellen in einer Projektkonfiguration gezwungen.</span><span class="sxs-lookup"><span data-stu-id="7955d-123">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="7955d-124">NuGet nicht mehr wiederhergestellt Pakete in gemeinsam genutzte Projekte noch eine Sperrdatei schreibt.</span><span class="sxs-lookup"><span data-stu-id="7955d-124">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="7955d-125">Wir haben Netzwerkausfall verbessert, und wiederholen Sie die Verarbeitung für den Server nicht erreichbar ist oder langsam zu reagieren.</span><span class="sxs-lookup"><span data-stu-id="7955d-125">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="7955d-126">Tastatur und Maus Verhaltensweisen sind in der Visual Studio-Paket-Manager-UI verbessert.</span><span class="sxs-lookup"><span data-stu-id="7955d-126">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="7955d-127">Wir unterstützen jetzt die neuesten `project.json` Schema in DNX.</span><span class="sxs-lookup"><span data-stu-id="7955d-127">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="7955d-128">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="7955d-128">Known Issues</span></span>

<span data-ttu-id="7955d-129">Wir weiterhin Probleme auf unserer GitHub-Problemliste zu verfolgen, die sich am befinden: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="7955d-129">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>