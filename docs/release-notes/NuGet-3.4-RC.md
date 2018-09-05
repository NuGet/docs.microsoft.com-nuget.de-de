---
title: Anmerkungen zu NuGet 3.4-RC
description: Anmerkungen zu NuGet 3.4 RC, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546753"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="64e4f-103">Anmerkungen zu NuGet 3.4-RC</span><span class="sxs-lookup"><span data-stu-id="64e4f-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="64e4f-104">[Anmerkungen zu NuGet 3.3](../release-notes/nuget-3.3.md) | [Anmerkungen zu NuGet 3.4](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="64e4f-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="64e4f-105">NuGet 3.4-RC am 3. März 2016 zusammen mit Visual Studio 2015 Update 2 RC veröffentlicht wurde, und mit wenigen Grundsätze in Köpfen erstellt wurde:</span><span class="sxs-lookup"><span data-stu-id="64e4f-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="64e4f-106">Plattformübergreifende Unterstützung</span><span class="sxs-lookup"><span data-stu-id="64e4f-106">Cross-Platform support</span></span>
* <span data-ttu-id="64e4f-107">Leistungsverbesserungen</span><span class="sxs-lookup"><span data-stu-id="64e4f-107">Performance improvements</span></span>
* <span data-ttu-id="64e4f-108">Kleinere Verbesserungen der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="64e4f-108">Minor UI improvements</span></span>

<span data-ttu-id="64e4f-109">Die folgenden Funktionen stehen diese RC-Version, mit mehr für die 3.4 endgültige Version geplant wurde.</span><span class="sxs-lookup"><span data-stu-id="64e4f-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="64e4f-110">Neue Funktionen</span><span class="sxs-lookup"><span data-stu-id="64e4f-110">New Features</span></span>

* <span data-ttu-id="64e4f-111">NuGet-Clients unterstützen jetzt Gzip-inhaltscodierung von Repositorys</span><span class="sxs-lookup"><span data-stu-id="64e4f-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="64e4f-112">Unterstützung für PDBs aus Paketen in Xproj-Projekten</span><span class="sxs-lookup"><span data-stu-id="64e4f-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="64e4f-113">Unterstützung für IOS- und Android-Buildvorgänge im ContentFiles-element</span><span class="sxs-lookup"><span data-stu-id="64e4f-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="64e4f-114">Unterstützung für die Framework-Moniker "Netstandard" und "netstandardapp"</span><span class="sxs-lookup"><span data-stu-id="64e4f-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="64e4f-115">Neue Features der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="64e4f-115">New User Interface Features</span></span>

* <span data-ttu-id="64e4f-116">Signifikante leistungsverbesserungen besonders auf den Registerkarten installiert, Updates und konsolidieren</span><span class="sxs-lookup"><span data-stu-id="64e4f-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="64e4f-117">Installiert und Updates Registerkarten sind jetzt alphabetisch sortiert</span><span class="sxs-lookup"><span data-stu-id="64e4f-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="64e4f-118">Schaltfläche "Aktualisieren", die eine Suche aktualisiert werden kann. hinzugefügt</span><span class="sxs-lookup"><span data-stu-id="64e4f-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="64e4f-119">Updates und Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="64e4f-119">Updates and Improvements</span></span>

* <span data-ttu-id="64e4f-120">Pakete, die auf die verwiesen wird `project.json` Gleitkommazahl deren Version wird nicht für jeden Build aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="64e4f-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="64e4f-121">Stattdessen werden sie aktualisiert nur, wenn Sie gezwungen, wiederherzustellen, bereinigen, neu erstellen oder ändern Sie `project.json`.</span><span class="sxs-lookup"><span data-stu-id="64e4f-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="64e4f-122">NuGet.org-Repository-Quellen werden in einer Projektkonfiguration nicht mehr gezwungen, bei der Verwendung der Benutzeroberfläche für der NuGet-Konfigurations.</span><span class="sxs-lookup"><span data-stu-id="64e4f-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="64e4f-123">NuGet nicht mehr stellt Pakete in freigegebene Projekten wieder her und schreibt eine Sperrdatei.</span><span class="sxs-lookup"><span data-stu-id="64e4f-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="64e4f-124">Wir Netzwerkfehler wurde verbessert, und wiederholen Sie die Behandlung von nicht erreichbar ist oder langsam, reagieren.</span><span class="sxs-lookup"><span data-stu-id="64e4f-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="64e4f-125">Tastatur und Maus Verhaltensweisen werden in der Visual Studio-Paket-Manager-UI verbessert.</span><span class="sxs-lookup"><span data-stu-id="64e4f-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="64e4f-126">Wir unterstützen jetzt die neueste Version `project.json` -Schema in DNX.</span><span class="sxs-lookup"><span data-stu-id="64e4f-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="64e4f-127">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="64e4f-127">Known Issues</span></span>

<span data-ttu-id="64e4f-128">Wir fahren fort, um Probleme in der Liste unserer GitHub-Probleme nachzuverfolgen, die finden Sie unter: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="64e4f-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>