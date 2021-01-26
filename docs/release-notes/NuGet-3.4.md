---
title: Anmerkungen zu dieser Version von nuget 3,4
description: Anmerkungen zu dieser Version von nuget 3,4 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776420"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="5c715-103">Anmerkungen zu dieser Version von nuget 3,4</span><span class="sxs-lookup"><span data-stu-id="5c715-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="5c715-104">Anmerkungen zu dieser [Version von nuget 3,4-RC](../release-notes/nuget-3.4-RC.md)  |  [Anmerkungen zu nuget-Version 3.4.1](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="5c715-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="5c715-105">Nuget 3,4 wurde als Teil von Visual Studio 2015 Update 2 und Visual Studio 15 Preview 2016 veröffentlicht und mit einigen wenigen Grundsätzen erstellt:</span><span class="sxs-lookup"><span data-stu-id="5c715-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="5c715-106">Plattformübergreifende Unterstützung</span><span class="sxs-lookup"><span data-stu-id="5c715-106">Cross-Platform support</span></span>
* <span data-ttu-id="5c715-107">Leistungsverbesserungen</span><span class="sxs-lookup"><span data-stu-id="5c715-107">Performance improvements</span></span>
* <span data-ttu-id="5c715-108">Kleinere Verbesserung der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="5c715-108">Minor UI improvements</span></span>

<span data-ttu-id="5c715-109">Die folgenden Features wurden bereits in der RC-Version hinzugefügt und wurden für die Version 3,4 aktualisiert oder abgeschlossen:</span><span class="sxs-lookup"><span data-stu-id="5c715-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="5c715-110">Neue Funktionen</span><span class="sxs-lookup"><span data-stu-id="5c715-110">New Features</span></span>

* <span data-ttu-id="5c715-111">Nuget-Clients unterstützen jetzt gzip-Inhalts Codierung aus Depots.</span><span class="sxs-lookup"><span data-stu-id="5c715-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="5c715-112">Unterstützung für pdsb von Paketen in xproj-Projekten</span><span class="sxs-lookup"><span data-stu-id="5c715-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="5c715-113">Unterstützung für IOS-und Android-Buildvorgänge im contentfiles-Element</span><span class="sxs-lookup"><span data-stu-id="5c715-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="5c715-114">Unterstützung für die FrameworkMoniker netstandard und netstandardapp</span><span class="sxs-lookup"><span data-stu-id="5c715-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="5c715-115">Neue Benutzeroberflächen Features</span><span class="sxs-lookup"><span data-stu-id="5c715-115">New User Interface Features</span></span>

* <span data-ttu-id="5c715-116">Bedeutende Leistungsverbesserungen vor allem auf den Registerkarten installiert, Updates und konsolidiert</span><span class="sxs-lookup"><span data-stu-id="5c715-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="5c715-117">Die Quelle "alle Paketquellen" ist für die ordnungsgemäße Zusammenführung der Suchergebnisse verfügbar.</span><span class="sxs-lookup"><span data-stu-id="5c715-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="5c715-118">Registerkarten "installiert" und "Updates" sind nun alphabetisch sortiert</span><span class="sxs-lookup"><span data-stu-id="5c715-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="5c715-119">Die Schaltfläche "Aktualisieren" wurde hinzugefügt, die die Aktualisierung einer Suche ermöglicht</span><span class="sxs-lookup"><span data-stu-id="5c715-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="5c715-120">Neueste Buildoptionen am Anfang der Versions Liste</span><span class="sxs-lookup"><span data-stu-id="5c715-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="5c715-121">Updates und Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="5c715-121">Updates and Improvements</span></span>

* <span data-ttu-id="5c715-122">Pakete, auf die in verwiesen wird und die eine unverankerte `project.json` Version aufweisen, werden bei jedem Build nicht aktualisiert</span><span class="sxs-lookup"><span data-stu-id="5c715-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="5c715-123">Stattdessen werden Sie nur aktualisiert, wenn Sie zum Wiederherstellen, bereinigen, Neuerstellen oder ändern gezwungen werden `project.json` .</span><span class="sxs-lookup"><span data-stu-id="5c715-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="5c715-124">nuget.org-Repository-Quellen werden nicht mehr in einer Projekt Konfiguration erzwungen, wenn Sie die nuget-Konfigurations Benutzeroberfläche verwenden.</span><span class="sxs-lookup"><span data-stu-id="5c715-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="5c715-125">Mit nuget werden Pakete nicht mehr in freigegebenen Projekten wieder hergestellt, und es wird keine Sperrdatei geschrieben.</span><span class="sxs-lookup"><span data-stu-id="5c715-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="5c715-126">Wir haben den Netzwerkfehler verbessert und die Verarbeitung für nicht erreichbare oder langsame Server erneut versucht.</span><span class="sxs-lookup"><span data-stu-id="5c715-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="5c715-127">Tastatur-und Maus Verhalten werden in der Visual Studio-Benutzeroberfläche des Paket-Managers verbessert.</span><span class="sxs-lookup"><span data-stu-id="5c715-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="5c715-128">Wir unterstützen jetzt das aktuellste `project.json` Schema in DNX.</span><span class="sxs-lookup"><span data-stu-id="5c715-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="5c715-129">Aktuelle Änderungen</span><span class="sxs-lookup"><span data-stu-id="5c715-129">Breaking Changes</span></span>

* <span data-ttu-id="5c715-130">Paket Versionsnummern werden nun in das Format " *Major*" normalisiert. *neben* Version. *Patch* - *vorab* Version   Alle Haupt-, neben-und patchvorgänge werden als ganze Zahlen behandelt, und alle führenden Nullen werden gelöscht.</span><span class="sxs-lookup"><span data-stu-id="5c715-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="5c715-131">Die Vorabinformationen werden als Zeichenfolge behandelt, und es werden keine Änderungen darauf angewendet.</span><span class="sxs-lookup"><span data-stu-id="5c715-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="5c715-132">Diese Zahlen werden in Abfragen von den nuget-Clients und der vom nuget.org-Dienst bereitgestellten Suche verwendet.</span><span class="sxs-lookup"><span data-stu-id="5c715-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="5c715-133">Weitere Informationen finden Sie in der nuget-Dokumentation unter [vorab Versionen](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="5c715-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="5c715-134">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="5c715-134">Known Issues</span></span>

* <span data-ttu-id="5c715-135">**Problem:** Windows 10 v1511 Benutzer haben möglicherweise Probleme oder sogar einen Visual Studio-Absturz mit PowerShell in Visual Studio in den folgenden Szenarien:</span><span class="sxs-lookup"><span data-stu-id="5c715-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="5c715-136">Installieren/Deinstallieren von Paketen mit install.ps1/uninstall.ps1-Skripts</span><span class="sxs-lookup"><span data-stu-id="5c715-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="5c715-137">Laden von Projekten mit einem init.ps1 Skript (wie z. b. EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="5c715-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="5c715-138">Veröffentlichen von Webinhalten</span><span class="sxs-lookup"><span data-stu-id="5c715-138">Publishing web content</span></span>

* <span data-ttu-id="5c715-139">Problem **Umgehung:** Stellen Sie sicher, dass auf Ihrer Windows 10-Installation die neuesten Patches angewendet wurden, nämlich der Januar 2016 (KB 3124263) oder ein späteres Update.</span><span class="sxs-lookup"><span data-stu-id="5c715-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="5c715-140">Weitere Informationen finden Sie unter [GitHub-Problem #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="5c715-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="5c715-141">**Problem:** NuGet v2-Protokollumleitungen sind defekt</span><span class="sxs-lookup"><span data-stu-id="5c715-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="5c715-142">Benutzerdefinierte NuGet-Repositorys, die Anforderungen an einen alternativen Host umleiten, beachten die Umleitungsanforderung nicht.</span><span class="sxs-lookup"><span data-stu-id="5c715-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="5c715-143">Problem **Umgehung:**  Um dieses Problem zu umgehen, konfigurieren Sie den Paketrepository-URI in den Einstellungen so, dass er auf den umgeleiteten Serverstandort verweist</span><span class="sxs-lookup"><span data-stu-id="5c715-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="5c715-144">Weitere Informationen finden Sie unter [GitHub Pull Request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="5c715-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="5c715-145">Wir verfolgen weiterhin Probleme in unserer GitHub-Liste mit Problemen, die unter folgenden Themen zu finden sind: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="5c715-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>