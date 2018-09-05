---
title: Anmerkungen zu NuGet 3.4
description: Anmerkungen zu NuGet 3.4, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551190"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="ab844-103">Anmerkungen zu NuGet 3.4</span><span class="sxs-lookup"><span data-stu-id="ab844-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="ab844-104">[Anmerkungen zu NuGet 3.4-RC](../release-notes/nuget-3.4-RC.md) | [Anmerkungen zu NuGet 3.4.1](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="ab844-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="ab844-105">NuGet 3.4 wurde am 30. März 2016 als Teil der Visual Studio 2015 Update 2 und Visual Studio 15 Preview-Version veröffentlicht und mit wenigen Grundsätze in Köpfen erstellt wurde:</span><span class="sxs-lookup"><span data-stu-id="ab844-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="ab844-106">Plattformübergreifende Unterstützung</span><span class="sxs-lookup"><span data-stu-id="ab844-106">Cross-Platform support</span></span>
* <span data-ttu-id="ab844-107">Leistungsverbesserungen</span><span class="sxs-lookup"><span data-stu-id="ab844-107">Performance improvements</span></span>
* <span data-ttu-id="ab844-108">Kleinere Verbesserungen der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="ab844-108">Minor UI improvements</span></span>

<span data-ttu-id="ab844-109">Die folgenden Features wurden waren zuvor hinzugefügt haben, in die RC-Version und aktualisiert oder der Version 3.4 abgeschlossen:</span><span class="sxs-lookup"><span data-stu-id="ab844-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="ab844-110">Neue Funktionen</span><span class="sxs-lookup"><span data-stu-id="ab844-110">New Features</span></span>

* <span data-ttu-id="ab844-111">NuGet-Clients unterstützen jetzt Gzip-inhaltscodierung von Repositorys</span><span class="sxs-lookup"><span data-stu-id="ab844-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="ab844-112">Unterstützung für PDBs aus Paketen in Xproj-Projekten</span><span class="sxs-lookup"><span data-stu-id="ab844-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="ab844-113">Unterstützung für IOS- und Android-Buildvorgänge im ContentFiles-element</span><span class="sxs-lookup"><span data-stu-id="ab844-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="ab844-114">Unterstützung für die Framework-Moniker "Netstandard" und "netstandardapp"</span><span class="sxs-lookup"><span data-stu-id="ab844-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="ab844-115">Neue Features der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="ab844-115">New User Interface Features</span></span>

* <span data-ttu-id="ab844-116">Signifikante leistungsverbesserungen besonders auf den Registerkarten installiert, Updates und konsolidieren</span><span class="sxs-lookup"><span data-stu-id="ab844-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="ab844-117">Aggregieren "Alle Paketquellen"-Quelle ist verfügbar, mit der richtigen Suche Ergebnis zusammenführen</span><span class="sxs-lookup"><span data-stu-id="ab844-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="ab844-118">Installiert und Updates Registerkarten sind jetzt alphabetisch sortiert</span><span class="sxs-lookup"><span data-stu-id="ab844-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="ab844-119">Schaltfläche "Aktualisieren", die eine Suche aktualisiert werden kann. hinzugefügt</span><span class="sxs-lookup"><span data-stu-id="ab844-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="ab844-120">Neueste Build-Optionen am oberen Rand der Liste der Versionen</span><span class="sxs-lookup"><span data-stu-id="ab844-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="ab844-121">Updates und Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="ab844-121">Updates and Improvements</span></span>

* <span data-ttu-id="ab844-122">Pakete, die auf die verwiesen wird `project.json` Gleitkommazahl deren Version wird nicht für jeden Build aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="ab844-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="ab844-123">Stattdessen werden sie aktualisiert nur, wenn Sie gezwungen, wiederherzustellen, bereinigen, neu erstellen oder ändern Sie `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ab844-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="ab844-124">NuGet.org-Repository-Quellen werden in einer Projektkonfiguration nicht mehr gezwungen, bei der Verwendung der Benutzeroberfläche für der NuGet-Konfigurations.</span><span class="sxs-lookup"><span data-stu-id="ab844-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="ab844-125">NuGet nicht mehr stellt Pakete in freigegebene Projekten wieder her und schreibt eine Sperrdatei.</span><span class="sxs-lookup"><span data-stu-id="ab844-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="ab844-126">Wir Netzwerkfehler wurde verbessert, und wiederholen Sie die Behandlung von nicht erreichbar ist oder langsam, reagieren.</span><span class="sxs-lookup"><span data-stu-id="ab844-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="ab844-127">Tastatur und Maus Verhaltensweisen werden in der Visual Studio-Paket-Manager-UI verbessert.</span><span class="sxs-lookup"><span data-stu-id="ab844-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="ab844-128">Wir unterstützen jetzt die neueste Version `project.json` -Schema in DNX.</span><span class="sxs-lookup"><span data-stu-id="ab844-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="ab844-129">Die Lauffähigkeit der Anwendung beeinträchtigende Änderungen</span><span class="sxs-lookup"><span data-stu-id="ab844-129">Breaking Changes</span></span>

* <span data-ttu-id="ab844-130">Paket-Versionsnummern werden jetzt in das Format normalisiert *wichtigen*. *kleinere*. *Patch*-*Vorabversion* aller Haupt-, neben- und patch werden als Zahlen behandelt, und legen Sie alle führenden Nullen auf.</span><span class="sxs-lookup"><span data-stu-id="ab844-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="ab844-131">Die vorabversionsinformationen wird als Zeichenfolge behandelt, und keine Änderungen angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="ab844-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="ab844-132">Diese Zahlen werden in Abfragen verwendet, indem Sie die NuGet-Clients und die Suche, die von der nuget.org-Dienst bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="ab844-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="ab844-133">Weitere Informationen finden Sie in der NuGet-Dokumentation unter [Vorabversion Versionen](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="ab844-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="ab844-134">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="ab844-134">Known Issues</span></span>

* <span data-ttu-id="ab844-135">**Problem:** Windows 10-v1511-Benutzern möglicherweise auftreten, Probleme oder sogar eine Visual Studio-Absturzes mithilfe von Powershell in Visual Studio in den folgenden Szenarien:</span><span class="sxs-lookup"><span data-stu-id="ab844-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="ab844-136">Installieren / Deinstallieren von Paketen, die Install. ps1 / uninstall.ps1-Skripts</span><span class="sxs-lookup"><span data-stu-id="ab844-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="ab844-137">Laden von Projekten, die ein Skript init.ps1 (z. B. EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="ab844-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="ab844-138">Veröffentlichen von Webinhalten</span><span class="sxs-lookup"><span data-stu-id="ab844-138">Publishing web content</span></span>

* <span data-ttu-id="ab844-139">**Problemumgehung:** stellen Sie sicher, dass Ihre Windows 10-Installation die neuesten Patches angewendet, Expecially der Januar 2016 (KB 3124263) oder ein neueres Update ist.</span><span class="sxs-lookup"><span data-stu-id="ab844-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="ab844-140">Weitere Informationen finden Sie auf [GitHub-Problem #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="ab844-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="ab844-141">**Problem:** NuGet v2-Protokollumleitungen sind defekt</span><span class="sxs-lookup"><span data-stu-id="ab844-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="ab844-142">Benutzerdefinierte NuGet-Repositorys, die Anforderungen an einen alternativen Host umleiten, beachten die Umleitungsanforderung nicht.</span><span class="sxs-lookup"><span data-stu-id="ab844-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="ab844-143">**Problemumgehung:** um dieses Problem zu umgehen, konfigurieren Sie den paketrepository-URI in den Einstellungen, die auf den Standort des umgeleiteten Servers verweist.</span><span class="sxs-lookup"><span data-stu-id="ab844-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="ab844-144">Weitere Informationen finden Sie unter [Pull Request auf GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="ab844-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="ab844-145">Wir fahren fort, um Probleme in der Liste unserer GitHub-Probleme nachzuverfolgen, die finden Sie unter: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="ab844-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>