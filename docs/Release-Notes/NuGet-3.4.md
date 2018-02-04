---
title: NuGet 3.4-Versionshinweise | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 3.4, einschließlich der bekannten Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet 3.4 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 515fb888aca2a8eb138c8fea1fb5b3f5a8f4e275
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="f4bd5-104">NuGet 3.4-Versionshinweise</span><span class="sxs-lookup"><span data-stu-id="f4bd5-104">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="f4bd5-105">[NuGet 3.4-RC-Versionsanmerkungen](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1-Versionshinweise](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="f4bd5-105">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="f4bd5-106">NuGet 3.4 30. März 2016 freigegeben wurde, als Teil der Visual Studio 2015 Update 2 und Visual Studio 15 Preview-Version und einige Grundsätze in Köpfen erstellt wurde:</span><span class="sxs-lookup"><span data-stu-id="f4bd5-106">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

*  <span data-ttu-id="f4bd5-107">Plattformübergreifende Unterstützung</span><span class="sxs-lookup"><span data-stu-id="f4bd5-107">Cross-Platform support</span></span>
*  <span data-ttu-id="f4bd5-108">Leistungsverbesserungen</span><span class="sxs-lookup"><span data-stu-id="f4bd5-108">Performance improvements</span></span>
*  <span data-ttu-id="f4bd5-109">Kleinere Verbesserungen der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="f4bd5-109">Minor UI improvements</span></span>

<span data-ttu-id="f4bd5-110">Die folgenden Funktionen wurden wurden zuvor in RC hinzugefügt und aktualisiert oder für die Version 3.4 abgeschlossen:</span><span class="sxs-lookup"><span data-stu-id="f4bd5-110">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="f4bd5-111">Neue Funktionen</span><span class="sxs-lookup"><span data-stu-id="f4bd5-111">New Features</span></span>

* <span data-ttu-id="f4bd5-112">NuGet-Clients unterstützen jetzt Gzip-inhaltscodierung von Repositorys</span><span class="sxs-lookup"><span data-stu-id="f4bd5-112">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="f4bd5-113">Unterstützung für die PDB-Dateien von Paketen in Xproj-Projekten</span><span class="sxs-lookup"><span data-stu-id="f4bd5-113">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="f4bd5-114">Unterstützung für IOS- und Android-Buildvorgänge im inhaltsdateienelement</span><span class="sxs-lookup"><span data-stu-id="f4bd5-114">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="f4bd5-115">Unterstützung für die netstandard- und Netstandardapp-frameworkMoniker</span><span class="sxs-lookup"><span data-stu-id="f4bd5-115">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="f4bd5-116">Neue Features der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="f4bd5-116">New User Interface Features</span></span>

* <span data-ttu-id="f4bd5-117">Signifikante leistungsverbesserungen besonders auf den Registerkarten installiert, Updates und konsolidieren</span><span class="sxs-lookup"><span data-stu-id="f4bd5-117">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="f4bd5-118">Aggregatquelle "Alle Paketquellen" steht mit der richtigen Suche Ergebnis zusammenführen</span><span class="sxs-lookup"><span data-stu-id="f4bd5-118">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="f4bd5-119">Installiert und Updates Registerkarten sind jetzt alphabetisch sortiert</span><span class="sxs-lookup"><span data-stu-id="f4bd5-119">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="f4bd5-120">Schaltfläche "Aktualisieren", die eine zu aktualisierende-Suche erlaubt hinzugefügt</span><span class="sxs-lookup"><span data-stu-id="f4bd5-120">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="f4bd5-121">Neueste Buildoptionen am oberen Rand der Liste Version</span><span class="sxs-lookup"><span data-stu-id="f4bd5-121">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="f4bd5-122">Updates und Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="f4bd5-122">Updates and Improvements</span></span>

* <span data-ttu-id="f4bd5-123">Pakete, die auf die verwiesen wird `project.json` , auf denen eine Gleitkommazahl-Version wird nicht auf jedem Build aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="f4bd5-123">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="f4bd5-124">Stattdessen werden sie aktualisieren nur, wenn Sie gezwungen, wiederherzustellen, bereinigen, neu erstellen oder ändern Sie `project.json`.</span><span class="sxs-lookup"><span data-stu-id="f4bd5-124">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="f4bd5-125">Bei Verwendung der NuGet-Konfigurations-UI nicht mehr NuGet.org Repository Quellen in einer Projektkonfiguration gezwungen.</span><span class="sxs-lookup"><span data-stu-id="f4bd5-125">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="f4bd5-126">NuGet nicht mehr wiederhergestellt Pakete in gemeinsam genutzte Projekte noch eine Sperrdatei schreibt.</span><span class="sxs-lookup"><span data-stu-id="f4bd5-126">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="f4bd5-127">Wir haben Netzwerkausfall verbessert, und wiederholen Sie die Verarbeitung für den Server nicht erreichbar ist oder langsam zu reagieren.</span><span class="sxs-lookup"><span data-stu-id="f4bd5-127">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="f4bd5-128">Tastatur und Maus Verhaltensweisen sind in der Visual Studio-Paket-Manager-UI verbessert.</span><span class="sxs-lookup"><span data-stu-id="f4bd5-128">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="f4bd5-129">Wir unterstützen jetzt die neuesten `project.json` Schema in DNX.</span><span class="sxs-lookup"><span data-stu-id="f4bd5-129">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="f4bd5-130">Die Lauffähigkeit der Anwendung beeinträchtigende Änderungen</span><span class="sxs-lookup"><span data-stu-id="f4bd5-130">Breaking Changes</span></span>

* <span data-ttu-id="f4bd5-131">Paket-Versionsnummern sind jetzt in das Format normalisiert *wichtigen*. *kleinere*. *Patch für*-*Vorabversion* aller Haupt-und Nebenversionsnummer und Patchen werden als ganze Zahlen behandelt, und legen Sie alle führenden Nullen (0).</span><span class="sxs-lookup"><span data-stu-id="f4bd5-131">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="f4bd5-132">Diese Informationen als Zeichenfolge behandelt, und keine Änderungen angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="f4bd5-132">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="f4bd5-133">Diese Nummern werden durch die NuGet-Clients und bei der Suche der nuget.org-Dienstes in Abfragen verwendet.</span><span class="sxs-lookup"><span data-stu-id="f4bd5-133">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="f4bd5-134">Weitere Informationen finden Sie in der NuGet Docs unter [Vorabversion](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="f4bd5-134">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="f4bd5-135">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="f4bd5-135">Known Issues</span></span>

* <span data-ttu-id="f4bd5-136">**Problem:** Windows 10 v1511 treten möglicherweise Probleme oder sogar eine Visual Studio-Absturzes mit Powershell in Visual Studio in den folgenden Szenarien:</span><span class="sxs-lookup"><span data-stu-id="f4bd5-136">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="f4bd5-137">Installieren / Deinstallieren von Paketen mit ps1 / ps1-Skripts</span><span class="sxs-lookup"><span data-stu-id="f4bd5-137">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="f4bd5-138">Laden von Projekten, die ein Skript init.ps1 (z. B. EntityFramework) aufweisen</span><span class="sxs-lookup"><span data-stu-id="f4bd5-138">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="f4bd5-139">Veröffentlichen von Webinhalten</span><span class="sxs-lookup"><span data-stu-id="f4bd5-139">Publishing web content</span></span>

* <span data-ttu-id="f4bd5-140">**Problemumgehung:** stellen Sie sicher, dass die Installation der Windows 10 die neuesten Patches angewendet, Expecially Januar 2016 (KB 3124263) oder ein neueres Update verfügt.</span><span class="sxs-lookup"><span data-stu-id="f4bd5-140">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="f4bd5-141">Weitere Informationen finden Sie auf [GitHub-Problem #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="f4bd5-141">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="f4bd5-142">**Problem:** NuGet v2-Protokollumleitungen sind defekt</span><span class="sxs-lookup"><span data-stu-id="f4bd5-142">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="f4bd5-143">Benutzerdefinierte NuGet-Repositorys, die Anforderungen an einen alternativen Host umleiten, beachten die Umleitungsanforderung nicht.</span><span class="sxs-lookup"><span data-stu-id="f4bd5-143">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="f4bd5-144">**Problemumgehung:** um dieses Problem zu umgehen, konfigurieren Sie den paketrepository-URI in den Einstellungen so, dass auf den Standort des umgeleiteten Servers verweist.</span><span class="sxs-lookup"><span data-stu-id="f4bd5-144">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="f4bd5-145">Weitere Informationen finden Sie unter [GitHub Pull-Anforderung #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="f4bd5-145">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="f4bd5-146">Wir weiterhin Probleme auf unserer GitHub-Problemliste zu verfolgen, die sich am befinden: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="f4bd5-146">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>