---
title: Anmerkungen zu Version 4.0 RC von NuGet | Microsoft-Dokumentation
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/17/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Anmerkungen zu NuGet 4.0 RC, einschließlich bekannter Fehler, Fehlerkorrekturen, hinzugefügter Features und DCRs."
keywords: "Anmerkungen zu NuGet 4.0 RC, Fehlerkorrekturen, bekannte Fehler, hinzugefügte Features, DCRs"
ms.reviewer:
- kraigb
ms.openlocfilehash: 9156f75edc9cf72cbb1d122f01d8a071ed56a124
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-40-rc-release-notes"></a><span data-ttu-id="1a875-104">Anmerkungen zu Version 4.0 RC von NuGet</span><span class="sxs-lookup"><span data-stu-id="1a875-104">NuGet 4.0 RC Release Notes</span></span>

[<span data-ttu-id="1a875-105">Anmerkungen zu Version 3.5 RTM von NuGet</span><span class="sxs-lookup"><span data-stu-id="1a875-105">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="1a875-106">[NuGet 4.0 RC für Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) konzentriert sich auf das Hinzufügen der Unterstützung für .NET Core-Szenarios sowie auf das Behandeln von wichtigem Kundenfeedback und auf das Verbessern der Leistung für zahlreiche Szenarios.</span><span class="sxs-lookup"><span data-stu-id="1a875-106">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="1a875-107">Die Verbesserungen in diesem Release betreffen die Unterstützung für PackageReference, NuGet-Befehle als MSBuild-Ziele, die Paketwiederherstellung im Hintergrund und vieles mehr.</span><span class="sxs-lookup"><span data-stu-id="1a875-107">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="1a875-108">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="1a875-108">Bug Fixes</span></span>

- <span data-ttu-id="1a875-109">Verhaltensänderungen in `dotnet pack --version-suffix foo` ([#3838](https://github.com/NuGet/Home/issues/3838))</span><span class="sxs-lookup"><span data-stu-id="1a875-109">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

- <span data-ttu-id="1a875-110">Das Wiederherstellen von „nuget.exe“ auf einem Computer mit VS „15“ schlägt fehl ([#3834](https://github.com/NuGet/Home/issues/3834))</span><span class="sxs-lookup"><span data-stu-id="1a875-110">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

- <span data-ttu-id="1a875-111">„Datei > Neues Projekt“ in .NET Core sollte den Build während der Wiederherstellung blockieren ([#3780](https://github.com/NuGet/Home/issues/3780))</span><span class="sxs-lookup"><span data-stu-id="1a875-111">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

- <span data-ttu-id="1a875-112">ASP.NET Core-Apps, die von Visual Studio 2015 zu VS „15“ migriert wurden, können nicht wiederhergestellt werden</span><span class="sxs-lookup"><span data-stu-id="1a875-112">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="1a875-113"> ([#3773](https://github.com/NuGet/Home/issues/3773))</span><span class="sxs-lookup"><span data-stu-id="1a875-113"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

- <span data-ttu-id="1a875-114">[Testfehler] Das Paket „jQuery Validation“ kann über die PM-Benutzeroberfläche nicht deinstalliert werden ([#3755](https://github.com/NuGet/Home/issues/3755))</span><span class="sxs-lookup"><span data-stu-id="1a875-114">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

- <span data-ttu-id="1a875-115">Wenn ein Paket für ein UWP-`project.json`-Projekt installiert wird, sollten übergeordnete Projekte ebenfalls wiederhergestellt werden ([#3731](https://github.com/NuGet/Home/issues/3731))</span><span class="sxs-lookup"><span data-stu-id="1a875-115">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

- <span data-ttu-id="1a875-116">Ändern der NuGet-Ziele, um die Paketquellen mit hohem statt normalem Ausführlichkeitsgrad zu protokollieren ([#3719](https://github.com/NuGet/Home/issues/3719))</span><span class="sxs-lookup"><span data-stu-id="1a875-116">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

- <span data-ttu-id="1a875-117">„dotnet pack3“ sollte standardmäßig eine XML-Dokumentation enthalten ([#3698](https://github.com/NuGet/Home/issues/3698))</span><span class="sxs-lookup"><span data-stu-id="1a875-117">dotnet pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

- <span data-ttu-id="1a875-118">Das Batchupdate über die Benutzeroberfläche schlägt fehl, wenn die Quelle ohne das Paket zuerst aufgeführt und „Alle Quellen“ ausgewählt ist ([#3696](https://github.com/NuGet/Home/issues/3696))</span><span class="sxs-lookup"><span data-stu-id="1a875-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

- <span data-ttu-id="1a875-119">Der NuGet-Befehl „pack“ schließt nicht alle Dateien ein ([#3678](https://github.com/NuGet/Home/issues/3678))</span><span class="sxs-lookup"><span data-stu-id="1a875-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

- <span data-ttu-id="1a875-120">OOM-Problem ([#3661](https://github.com/NuGet/Home/issues/3661))</span><span class="sxs-lookup"><span data-stu-id="1a875-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

- <span data-ttu-id="1a875-121">Der Abschnitt „ProjectFileDependencyGroups“ der Ressourcendatei sollte Bibliotheksnamen für Projekte verwenden ([#3611](https://github.com/NuGet/Home/issues/3611))</span><span class="sxs-lookup"><span data-stu-id="1a875-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

- <span data-ttu-id="1a875-122">„dotnet restore“ und das Wiederherstellen von Verzeichnissen ([#3517](https://github.com/NuGet/Home/issues/3517))</span><span class="sxs-lookup"><span data-stu-id="1a875-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

- <span data-ttu-id="1a875-123">Restore3-Fehler werden als Warnungen statt als Fehler protokolliert ([#3503](https://github.com/NuGet/Home/issues/3503))</span><span class="sxs-lookup"><span data-stu-id="1a875-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

- <span data-ttu-id="1a875-124">TFS-Fehler: „Das Element [Datei] wurde in Ihrem Arbeitsbereich nicht gefunden, oder Sie besitzen keine entsprechende Zugriffsberechtigung.“ ([#2805](https://github.com/NuGet/Home/issues/2805))</span><span class="sxs-lookup"><span data-stu-id="1a875-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

- <span data-ttu-id="1a875-125">Durch das Eingeben von „nuget <packagename>“ in das Suchfeld des Visual Studio-Schnellstarts wird das Präfix „nuget“ beibehalten ([#2719](https://github.com/NuGet/Home/issues/2719))</span><span class="sxs-lookup"><span data-stu-id="1a875-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

- <span data-ttu-id="1a875-126">System.Xml.XmlException: Unbekanntes Stammelement im Bereich der Kerneigenschaften.</span><span class="sxs-lookup"><span data-stu-id="1a875-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="1a875-127">Zeile 2, Position 2</span><span class="sxs-lookup"><span data-stu-id="1a875-127">Line 2, position 2.</span></span><span data-ttu-id="1a875-128"> ([#2718](https://github.com/NuGet/Home/issues/2718))</span><span class="sxs-lookup"><span data-stu-id="1a875-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

- <span data-ttu-id="1a875-129">Die `.nuspec`-Datei mit &lt;- oder &gt;-Escapezeichen in Textfeldern führt keine Builds mehr aus ([#2651](https://github.com/NuGet/Home/issues/2651))</span><span class="sxs-lookup"><span data-stu-id="1a875-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

- <span data-ttu-id="1a875-130">Beim Löschen von „nuget.exe“ wird nicht zum Eingeben der Anmeldeinformationen aufgefordert (im nicht interaktiven Modus) ([#2626](https://github.com/NuGet/Home/issues/2626))</span><span class="sxs-lookup"><span data-stu-id="1a875-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

- <span data-ttu-id="1a875-131">Beim Löschen von „nuget.exe“ wird grundlos eine Warnung bezüglich des API-Schlüssels für lokale Quellen ausgegeben ([#2625](https://github.com/NuGet/Home/issues/2625))</span><span class="sxs-lookup"><span data-stu-id="1a875-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

- <span data-ttu-id="1a875-132">Schlechte Fehlerbehandlung beim Installieren von Entity Framework (Vorabpaket) ([#2566](https://github.com/NuGet/Home/issues/2566))</span><span class="sxs-lookup"><span data-stu-id="1a875-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

- <span data-ttu-id="1a875-133">Visual Studio stürzt ab, nachdem die Auswahl im Paket-Manager geändert wurde ([#2551](https://github.com/NuGet/Home/issues/2551))</span><span class="sxs-lookup"><span data-stu-id="1a875-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

- <span data-ttu-id="1a875-134">Die Wiederherstellung von dotnet führt ID-Suchvorgänge in lokalen Repositorys mit flachen Listen durch, bei denen die Groß-/Kleinschreibung berücksichtigt wird, wenn übergreifende Versionen verwendet werden ([#2516](https://github.com/NuGet/Home/issues/2516))</span><span class="sxs-lookup"><span data-stu-id="1a875-134">Dotnet restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

- <span data-ttu-id="1a875-135">Die Löschfunktion von „nuget.exe“ funktioniert im V2-Feed nicht ([#2509](https://github.com/NuGet/Home/issues/2509))</span><span class="sxs-lookup"><span data-stu-id="1a875-135">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

- <span data-ttu-id="1a875-136">Die Pushbenachrichtigung für ein Timeout von „nuget.exe“ benötigt eine bessere Fehlermeldung ([#2503](https://github.com/NuGet/Home/issues/2503))</span><span class="sxs-lookup"><span data-stu-id="1a875-136">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

- <span data-ttu-id="1a875-137">Die Toolwiederherstellung schlägt ohne die richtigen Importe ohne Warnung fehl</span><span class="sxs-lookup"><span data-stu-id="1a875-137">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="1a875-138"> ([#2462](https://github.com/NuGet/Home/issues/2462))</span><span class="sxs-lookup"><span data-stu-id="1a875-138"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

- <span data-ttu-id="1a875-139">NuGet fordert dazu auf, Anmeldeinformationen einzugeben, wenn ein privater Feed vorhanden ist, auch wenn die Installation über nuget.org vorgenommen wird ([#2346](https://github.com/NuGet/Home/issues/2346))</span><span class="sxs-lookup"><span data-stu-id="1a875-139">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

- <span data-ttu-id="1a875-140">Das Paket „ApplicationInsights 2.0“ wird aufgeführt, ist aber noch nicht vorhanden ([#2317](https://github.com/NuGet/Home/issues/2317))</span><span class="sxs-lookup"><span data-stu-id="1a875-140">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

- <span data-ttu-id="1a875-141">UIDelay in VS „15“ (Branch für Vorschauversion 5) ([#3500](https://github.com/NuGet/Home/issues/3500))</span><span class="sxs-lookup"><span data-stu-id="1a875-141">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

- <span data-ttu-id="1a875-142">Das erste OnBuild-Ereignis für die Wiederherstellung fehlt während des Builds für UWP ([#3489](https://github.com/NuGet/Home/issues/3489))</span><span class="sxs-lookup"><span data-stu-id="1a875-142">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

- <span data-ttu-id="1a875-143">PowerShell 5 beschädigt die Installation von Entity Framework?</span><span class="sxs-lookup"><span data-stu-id="1a875-143">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="1a875-144"> ([#3312](https://github.com/NuGet/Home/issues/3312))</span><span class="sxs-lookup"><span data-stu-id="1a875-144"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

- <span data-ttu-id="1a875-145">Quelle zur ausführlichen Protokollierung hinzufügen (für 3.5 berücksichtigen) ([#3294](https://github.com/NuGet/Home/issues/3294))</span><span class="sxs-lookup"><span data-stu-id="1a875-145">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

- <span data-ttu-id="1a875-146">Der NoCache-Parameter wird in Version 3.4 und höher des NuGet-Clients nicht berücksichtigt ([#3074](https://github.com/NuGet/Home/issues/3074))</span><span class="sxs-lookup"><span data-stu-id="1a875-146">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

- <span data-ttu-id="1a875-147">Wenn ein Anbieter für Anmeldeinformationen in Visual Studio nicht geladen werden kann, soll NuGet nicht unterbrochen werden ([#2422](https://github.com/NuGet/Home/issues/2422))</span><span class="sxs-lookup"><span data-stu-id="1a875-147">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>

## <a name="features"></a><span data-ttu-id="1a875-148">Features</span><span class="sxs-lookup"><span data-stu-id="1a875-148">Features</span></span>

- <span data-ttu-id="1a875-149">CI einrichten, um x86 auszuführen ([#3868](https://github.com/NuGet/Home/issues/3868))</span><span class="sxs-lookup"><span data-stu-id="1a875-149">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

- <span data-ttu-id="1a875-150">Automatische Wiederherstellung 3/3: nicht blockierende Benutzeroberfläche ([#3658](https://github.com/NuGet/Home/issues/3658))</span><span class="sxs-lookup"><span data-stu-id="1a875-150">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

- <span data-ttu-id="1a875-151">Automatische Wiederherstellung 2/3: Hintergrundwiederherstellung auf Nominierung ([#3657](https://github.com/NuGet/Home/issues/3657))</span><span class="sxs-lookup"><span data-stu-id="1a875-151">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

- <span data-ttu-id="1a875-152">Projektverweise wiederherstellen, um dem Buildverhalten zu entsprechen (Rekursion) ([#3615](https://github.com/NuGet/Home/issues/3615))</span><span class="sxs-lookup"><span data-stu-id="1a875-152">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

- <span data-ttu-id="1a875-153">DPL-Unterstützung in VS „15“ (minbar) ([#3614](https://github.com/NuGet/Home/issues/3614))</span><span class="sxs-lookup"><span data-stu-id="1a875-153">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

- <span data-ttu-id="1a875-154">Einstellungsdatei in Programme verschieben ([#3613](https://github.com/NuGet/Home/issues/3613))</span><span class="sxs-lookup"><span data-stu-id="1a875-154">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

- <span data-ttu-id="1a875-155">Generierte Wiederherstellungseigenschaften und -ziele benötigen zielübergreifende Unterstützung bei der Beteiligung ([#3496](https://github.com/NuGet/Home/issues/3496))</span><span class="sxs-lookup"><span data-stu-id="1a875-155">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

- <span data-ttu-id="1a875-156">NuGet-Unterstützung für die Wiederherstellung für PackageTargetFallback (zuvor: Imports) ([#3494](https://github.com/NuGet/Home/issues/3494))</span><span class="sxs-lookup"><span data-stu-id="1a875-156">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

- <span data-ttu-id="1a875-157">Implementierung von ToolsRef ([#3472](https://github.com/NuGet/Home/issues/3472))</span><span class="sxs-lookup"><span data-stu-id="1a875-157">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

- <span data-ttu-id="1a875-158">Restore3 für eine RID ([#3465](https://github.com/NuGet/Home/issues/3465))</span><span class="sxs-lookup"><span data-stu-id="1a875-158">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

- <span data-ttu-id="1a875-159">Die NuGet-Benutzeroberfläche sollte das Hinzufügen/Entfernen/Aktualisieren von PackageRefs ermöglichen ([#3457](https://github.com/NuGet/Home/issues/3457))</span><span class="sxs-lookup"><span data-stu-id="1a875-159">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

- <span data-ttu-id="1a875-160">Automatische Wiederherstellung 1/3: Implementieren der Nominierungs-API über das Zwischenspeichern der Wiederherstellungsinformationen des Projekts ([#3456](https://github.com/NuGet/Home/issues/3456))</span><span class="sxs-lookup"><span data-stu-id="1a875-160">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

- <span data-ttu-id="1a875-161">[0] NuGet-Wiederherstellungsaufgaben und -ziele ([#2994](https://github.com/NuGet/Home/issues/2994))</span><span class="sxs-lookup"><span data-stu-id="1a875-161">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

- <span data-ttu-id="1a875-162">[1] Aktivieren der Wiederherstellung auf Projektmappenebene in MSBuild ([#2993](https://github.com/NuGet/Home/issues/2993))</span><span class="sxs-lookup"><span data-stu-id="1a875-162">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

- <span data-ttu-id="1a875-163">Unterstützung der öffentlichen Erweiterbarkeit des Anbieters für Anmeldeinformationen in Visual Studio ([#2909](https://github.com/NuGet/Home/issues/2909))</span><span class="sxs-lookup"><span data-stu-id="1a875-163">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

- <span data-ttu-id="1a875-164">Rekursive NuGet-Wiederherstellung ([#2533](https://github.com/NuGet/Home/issues/2533))</span><span class="sxs-lookup"><span data-stu-id="1a875-164">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

- <span data-ttu-id="1a875-165">Microsoft.TeamFoundation.Client kann auf dev15 nicht geladen werden, die Version von Microsoft.TeamFoundation.Client muss für VS „15“ (Vorschauversion) auf 15.0 aktualisiert werden ([#2392](https://github.com/NuGet/Home/issues/2392))</span><span class="sxs-lookup"><span data-stu-id="1a875-165">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

- <span data-ttu-id="1a875-166">Das C++-Paket für das UWP-C++-Projekt in VS „15“ (Vorschauversion) kann nicht installiert werden ([#2369](https://github.com/NuGet/Home/issues/2369))</span><span class="sxs-lookup"><span data-stu-id="1a875-166">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

- <span data-ttu-id="1a875-167">Die NUPKG-Datei muss den Ordner „\buildCrossTargeting\“ unterstützen und `.targets` / `.props` für den zielübergreifenden MSBuild-Bereich importieren</span><span class="sxs-lookup"><span data-stu-id="1a875-167">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="1a875-168"> ([#3499](https://github.com/NuGet/Home/issues/3499))</span><span class="sxs-lookup"><span data-stu-id="1a875-168"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

- <span data-ttu-id="1a875-169">Entwurf von ToolsReference ([#3462](https://github.com/NuGet/Home/issues/3462))</span><span class="sxs-lookup"><span data-stu-id="1a875-169">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

- <span data-ttu-id="1a875-170">Korrigieren der NuGet-Benutzeroberfläche, um die Wiederherstellung von w/ PackageReferences in `.csproj` zu unterstützen ([#3455](https://github.com/NuGet/Home/issues/3455))</span><span class="sxs-lookup"><span data-stu-id="1a875-170">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

- <span data-ttu-id="1a875-171">Hinzufügen der Schaltfläche „Cache löschen“ zu den Einstellungen des Paket-Managers von Visual Studio ([#3289](https://github.com/NuGet/Home/issues/3289))</span><span class="sxs-lookup"><span data-stu-id="1a875-171">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="1a875-172">DCRs</span><span class="sxs-lookup"><span data-stu-id="1a875-172">DCRs</span></span>

- <span data-ttu-id="1a875-173">Die Wiederherstellung von Projektmappen sollte während der automatischen Wiederherstellung blockiert werden</span><span class="sxs-lookup"><span data-stu-id="1a875-173">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="1a875-174"> ([#3797](https://github.com/NuGet/Home/issues/3797))</span><span class="sxs-lookup"><span data-stu-id="1a875-174"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

- <span data-ttu-id="1a875-175">Die Installation von .NET Core über die Benutzeroberfläche des NuGet-Paket-Managers wird für jeden TFM statt nur für diejenigen durchgeführt, die vom Paket unterstützt werden ([#3721](https://github.com/NuGet/Home/issues/3721))</span><span class="sxs-lookup"><span data-stu-id="1a875-175">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

- <span data-ttu-id="1a875-176">Die Wiederherstellung der Nominierungs-API muss ebenfalls DotNetCliToolsReferences unterstützen</span><span class="sxs-lookup"><span data-stu-id="1a875-176">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="1a875-177"> ([#3702](https://github.com/NuGet/Home/issues/3702))</span><span class="sxs-lookup"><span data-stu-id="1a875-177"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

- <span data-ttu-id="1a875-178">VSIX (VS „15“) als Systemkomponente markieren ([#3700](https://github.com/NuGet/Home/issues/3700))</span><span class="sxs-lookup"><span data-stu-id="1a875-178">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

- <span data-ttu-id="1a875-179">Vom Verweis auf MS.VS.Services.Client zu MS.VS.Services.Client.Interactive migrieren ([#3670](https://github.com/NuGet/Home/issues/3670))</span><span class="sxs-lookup"><span data-stu-id="1a875-179">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

- <span data-ttu-id="1a875-180">$(RestoreLegacyPackagesDirectory) sollte von der Wiederherstellung als Projektebene berücksichtigt werden ([#3618](https://github.com/NuGet/Home/issues/3618))</span><span class="sxs-lookup"><span data-stu-id="1a875-180">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

- <span data-ttu-id="1a875-181">Die Wiederherstellung des Projekts mit einem einzelnen Zielframework sollte keine Eigenschaften erfordern ([#3588](https://github.com/NuGet/Home/issues/3588))</span><span class="sxs-lookup"><span data-stu-id="1a875-181">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

- <span data-ttu-id="1a875-182">Der Befehl „dotnet restore3 foo.csproj“ sollte</span><span class="sxs-lookup"><span data-stu-id="1a875-182">dotnet restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="1a875-183">wie bei „dotnet build“ den Abhängigkeiten der Projektverweise folgen und diese ebenfalls wiederherstellen</span><span class="sxs-lookup"><span data-stu-id="1a875-183">Like build.</span></span><span data-ttu-id="1a875-184"> ([#3577](https://github.com/NuGet/Home/issues/3577))</span><span class="sxs-lookup"><span data-stu-id="1a875-184"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

- <span data-ttu-id="1a875-185">"type": "platform": Abhängigkeiten werden als "type":"package" in der Sperrdatei dargestellt ([#2695](https://github.com/NuGet/Home/issues/2695))</span><span class="sxs-lookup"><span data-stu-id="1a875-185">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

- <span data-ttu-id="1a875-186">Der ausführliche Modus von „nuget.exe“ sollte die URL für den Download anzeigen ([#2629](https://github.com/NuGet/Home/issues/2629))</span><span class="sxs-lookup"><span data-stu-id="1a875-186">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

- <span data-ttu-id="1a875-187">Verschieben von NuGet.Xplat zu Microsoft.NetCore.App und netcoreapp1.0 ([#2483](https://github.com/NuGet/Home/issues/2483))</span><span class="sxs-lookup"><span data-stu-id="1a875-187">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

- <span data-ttu-id="1a875-188">Push: Es sollte möglich sein, den Symbolserver zu überschreiben, wenn etwas über mithilfe von Push über die Befehlszeile übertragen wird ([#2348](https://github.com/NuGet/Home/issues/2348))</span><span class="sxs-lookup"><span data-stu-id="1a875-188">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

- <span data-ttu-id="1a875-189">Konsolidieren von Code für das Suchen von globalen Paketpfaden ([#2296](https://github.com/NuGet/Home/issues/2296))</span><span class="sxs-lookup"><span data-stu-id="1a875-189">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

- <span data-ttu-id="1a875-190">Ein besserer Name als „suppressParent“ ist erforderlich ([#2196](https://github.com/NuGet/Home/issues/2196))</span><span class="sxs-lookup"><span data-stu-id="1a875-190">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

- <span data-ttu-id="1a875-191">Bestimmen des Abhängigkeitsnamens von `project.json`, der für MSBuild-Projekte verwendet werden soll ([#1914](https://github.com/NuGet/Home/issues/1914))</span><span class="sxs-lookup"><span data-stu-id="1a875-191">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

- <span data-ttu-id="1a875-192">Unterstützung für SemVer 2.0.0 zu NuGet.Core hinzufügen ([#3383](https://github.com/NuGet/Home/issues/3383))</span><span class="sxs-lookup"><span data-stu-id="1a875-192">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

- <span data-ttu-id="1a875-193">Transitive Abhängigkeiten von NUPKG-Dateien mit `.targets`-Dateien in MSBuild zulassen ([#3342](https://github.com/NuGet/Home/issues/3342))</span><span class="sxs-lookup"><span data-stu-id="1a875-193">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

- <span data-ttu-id="1a875-194">Der NuGet-Befehl „restore“ ist über die Befehlszeile wesentlich langsamer als in Visual Studio ([#3330](https://github.com/NuGet/Home/issues/3330))</span><span class="sxs-lookup"><span data-stu-id="1a875-194">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

- <span data-ttu-id="1a875-195">Beim Vergleich von Paket-ID und Version sollte die Groß-/Kleinschreibung nicht berücksichtigt werden ([#2522](https://github.com/NuGet/Home/issues/2522))</span><span class="sxs-lookup"><span data-stu-id="1a875-195">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

- <span data-ttu-id="1a875-196">Die Option „NoCache“ funktioniert nicht für auf `packages.config` basierende Wiederherstellungen und Installation (GlobalPackagesFolder) ([#1406](https://github.com/NuGet/Home/issues/1406))</span><span class="sxs-lookup"><span data-stu-id="1a875-196">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

- <span data-ttu-id="1a875-197">Die Ressourcen „FindPackageByIdResource“ benötigen einen Standardkontext und eine Protokollierung für den Cache ([#1357](https://github.com/NuGet/Home/issues/1357))</span><span class="sxs-lookup"><span data-stu-id="1a875-197">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
