---
title: Anmerkungen zu Version 4.0 RC von NuGet | Microsoft-Dokumentation
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 03/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 906cc4dd-7948-4e86-a093-21df830ce8c3
description: "Anmerkungen zu Version 4.0 RTM von NuGet, einschließlich bekannter Fehler, Fehlerkorrekturen, hinzugefügter Features und DCRs."
keywords: "Anmerkungen zu Version 4.0 RTM von NuGet, Fehlerkorrekturen, bekannte Fehler, hinzugefügte Features, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2cdee8b736fa2c651da803be9a10a6114936134a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="40-rtm-release-notes"></a><span data-ttu-id="db591-104">Anmerkungen zu Version 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="db591-104">4.0 RTM Release Notes</span></span>

<span data-ttu-id="db591-105">In [Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) ist NuGet 4.0 enthalten. Dieses wurde in Qualität und Leistungsfähigkeit verbessert und erweitert die Funktionalität von Visual Studio um Unterstützung für .Net Core.</span><span class="sxs-lookup"><span data-stu-id="db591-105">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="db591-106">Die Verbesserungen in diesem Release betreffen die Unterstützung für PackageReference, NuGet-Befehle als MSBuild-Ziele, die Paketwiederherstellung im Hintergrund und vieles mehr.</span><span class="sxs-lookup"><span data-stu-id="db591-106">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="db591-107">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="db591-107">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="db591-108">Möglicher Fehler bei der NuGet-Wiederherstellung, wenn mehrere Projekte vorhanden sind, die auf ein anderes Projekt in einer Projektmappe verweisen</span><span class="sxs-lookup"><span data-stu-id="db591-108">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="db591-109">Problem:</span><span class="sxs-lookup"><span data-stu-id="db591-109">Issue:</span></span>
<span data-ttu-id="db591-110">Die NuGet-Wiederherstellung funktioniert möglicherweise nicht, wenn in einer Projektmappe Projektverweise auf das gleiche Projekt mit abweichender Groß-/Kleinschreibung oder mit anderen relativen Pfaden vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="db591-110">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="db591-111">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="db591-111">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="db591-112">Problemumgehung:</span><span class="sxs-lookup"><span data-stu-id="db591-112">Workaround:</span></span>
<span data-ttu-id="db591-113">Ändern Sie die Schreibweisen bzw. relativen Pfade so, dass sie für alle Projektverweise übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="db591-113">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="db591-114">Beim Verwenden der Paket-Manager-Konsole funktioniert die EINGABETASTE ggf. nicht</span><span class="sxs-lookup"><span data-stu-id="db591-114">While using Package Manager Console, 'Enter' key may not work</span></span>
#### <a name="issue"></a><span data-ttu-id="db591-115">Problem:</span><span class="sxs-lookup"><span data-stu-id="db591-115">Issue:</span></span>
<span data-ttu-id="db591-116">Gelegentlich kann es vorkommen, dass die EINGABETASTE in der Paket-Manager-Konsole nicht funktioniert.</span><span class="sxs-lookup"><span data-stu-id="db591-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="db591-117">Wenn dieses Problem auftritt, überprüfen Sie den Fortschritt für diese Korrektur und stellen Sie zusätzliche hilfreiche Informationen zu den Reproduktionsschritten bereit.</span><span class="sxs-lookup"><span data-stu-id="db591-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="db591-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="db591-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="db591-119">Problemumgehung:</span><span class="sxs-lookup"><span data-stu-id="db591-119">Workaround:</span></span>
<span data-ttu-id="db591-120">Starten Sie Visual Studio neu und öffnen Sie die Paketverwaltungskonsole, bevor Sie die Projektmappe öffnen.</span><span class="sxs-lookup"><span data-stu-id="db591-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="db591-121">Alternativ können Sie versuchen, die Datei `project.lock.json` zu löschen und dann erneut wiederherzustellen.</span><span class="sxs-lookup"><span data-stu-id="db591-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="db591-122">In .NET Core-Projekten kann eine Wiederherstellungsendlosschleife auftreten, wenn Sie ein Paket mit einer Assembly verwenden, die eine ungültige Signatur enthält</span><span class="sxs-lookup"><span data-stu-id="db591-122">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>
#### <a name="issue"></a><span data-ttu-id="db591-123">Problem:</span><span class="sxs-lookup"><span data-stu-id="db591-123">Issue:</span></span>
<span data-ttu-id="db591-124">Bei der Verwendung eines Pakets mit einer Assembly, die eine ungültige Signatur enthält, oder beim Festlegen der Paketversion mit dem DateTime-Ticker tritt gelegentlich bei der automatischen Paketwiederherstellung eine Endlosschleife auf.</span><span class="sxs-lookup"><span data-stu-id="db591-124">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="db591-125">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="db591-125">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="db591-126">Problemumgehung:</span><span class="sxs-lookup"><span data-stu-id="db591-126">Workaround:</span></span>
<span data-ttu-id="db591-127">Zurzeit gibt es keine Problemumgehung.</span><span class="sxs-lookup"><span data-stu-id="db591-127">There is no workaround at this time.</span></span>

### <a name="you-will-be-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="db591-128">Sie können DotNetCLITools nicht mithilfe des NuGet-Paket-Managers anzeigen, hinzufügen oder aktualisieren</span><span class="sxs-lookup"><span data-stu-id="db591-128">You will be unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>
#### <a name="issue"></a><span data-ttu-id="db591-129">Problem:</span><span class="sxs-lookup"><span data-stu-id="db591-129">Issue:</span></span>
<span data-ttu-id="db591-130">Der NuGet-Paket-Manager zeigt die DotNetCLITools nicht an und ermöglicht auch kein Hinzufügen/Aktualisieren dieser Tools.</span><span class="sxs-lookup"><span data-stu-id="db591-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="db591-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="db591-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

* #### <a name="workaround"></a><span data-ttu-id="db591-132">Problemumgehung:</span><span class="sxs-lookup"><span data-stu-id="db591-132">Workaround:</span></span>
<span data-ttu-id="db591-133">DotNetCLIToolReferences muss in der Projektdatei manuell bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="db591-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="db591-134">Bei der NuGet-Wiederherstellung tritt ein Fehler auf, wenn Sie PackageId-Eigenschaft für Projekte festlegen</span><span class="sxs-lookup"><span data-stu-id="db591-134">NuGet restore will fail when you set PackageId property for projects</span></span>
#### <a name="issue"></a><span data-ttu-id="db591-135">Problem:</span><span class="sxs-lookup"><span data-stu-id="db591-135">Issue:</span></span>
<span data-ttu-id="db591-136">Bei .NET Core-Projekten respektiert die NuGet-Wiederherstellung in Visual Studio die PackageId-Eigenschaft von Projekten nicht.</span><span class="sxs-lookup"><span data-stu-id="db591-136">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="db591-137">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="db591-137">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="db591-138">Problemumgehung:</span><span class="sxs-lookup"><span data-stu-id="db591-138">Workaround:</span></span>
<span data-ttu-id="db591-139">Führen Sie die Wiederherstellung mithilfe der Befehlszeile aus.</span><span class="sxs-lookup"><span data-stu-id="db591-139">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="db591-140">Wenn das Projekt keinen Ordner „obj“ aufweist, tritt bei der Paketwiederherstellung ggf. ein Fehler auf</span><span class="sxs-lookup"><span data-stu-id="db591-140">When your project does not have 'obj' folder, package restore may fail</span></span>
#### <a name="issue"></a><span data-ttu-id="db591-141">Problem:</span><span class="sxs-lookup"><span data-stu-id="db591-141">Issue:</span></span>
<span data-ttu-id="db591-142">Visual Studio stellt PackageReferences nicht wieder her, wenn der Ordner „obj“ gelöscht wurde.</span><span class="sxs-lookup"><span data-stu-id="db591-142">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="db591-143">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="db591-143">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="db591-144">Problemumgehung:</span><span class="sxs-lookup"><span data-stu-id="db591-144">Workaround:</span></span>
<span data-ttu-id="db591-145">Erstellen Sie den Ordner „obj“ manuell. Die Wiederherstellung sollte dann funktionieren.</span><span class="sxs-lookup"><span data-stu-id="db591-145">Create 'obj' folder manually and the restore should work.</span></span> 

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="db591-146">Beim manuellen Aktualisieren von Paketen mithilfe von „Update-Paket“ in der Konsole tritt ggf ein Fehler auf</span><span class="sxs-lookup"><span data-stu-id="db591-146">Manually updating packages using Update-Package in console may fail</span></span>
#### <a name="issue"></a><span data-ttu-id="db591-147">Problem:</span><span class="sxs-lookup"><span data-stu-id="db591-147">Issue:</span></span>
<span data-ttu-id="db591-148">Das manuelle Verwenden von „Update-Package“ in der Konsole funktioniert nur für PackageReferences-Projekte, die soeben konvertiert wurden.</span><span class="sxs-lookup"><span data-stu-id="db591-148">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="db591-149">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="db591-149">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="db591-150">Problemumgehung:</span><span class="sxs-lookup"><span data-stu-id="db591-150">Workaround:</span></span>
<span data-ttu-id="db591-151">Zurzeit gibt es keine Problemumgehung.</span><span class="sxs-lookup"><span data-stu-id="db591-151">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="db591-152">Die Neuzuweisung der Framework-Zielversion kann zu unvollständigen IntelliSense-Funktionen führen</span><span class="sxs-lookup"><span data-stu-id="db591-152">Retargeting target framework version may lead to incomplete Intellisense</span></span>
#### <a name="issue"></a><span data-ttu-id="db591-153">Problem:</span><span class="sxs-lookup"><span data-stu-id="db591-153">Issue:</span></span>
<span data-ttu-id="db591-154">Die Neuzuweisung der Framework-Zielversion kann zu unvollständigen IntelliSense-Funktionen in Visual Studio führen.</span><span class="sxs-lookup"><span data-stu-id="db591-154">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="db591-155">Dies geschieht, wenn Sie PackageReferences als Paket-Manager-Format verwenden.</span><span class="sxs-lookup"><span data-stu-id="db591-155">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="db591-156">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="db591-156">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="db591-157">Problemumgehung:</span><span class="sxs-lookup"><span data-stu-id="db591-157">Workaround:</span></span>
<span data-ttu-id="db591-158">Führen Sie eine manuelle Wiederherstellung aus.</span><span class="sxs-lookup"><span data-stu-id="db591-158">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="db591-159">`msbuild /t:restore` schlägt fehl, wenn ein Projekt, das .NET 461 als Ziel verwendet, auf ein anderes Projekt verweist, das .NET Standard verwendet</span><span class="sxs-lookup"><span data-stu-id="db591-159">`msbuild /t:restore` fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="db591-160">Problem:</span><span class="sxs-lookup"><span data-stu-id="db591-160">Issue:</span></span>
<span data-ttu-id="db591-161">Bei „msbuild /t:restore“ tritt ein Fehler auf, wenn ein auf PackageReference basierendes Projekt mit dem Ziel .NET461 auf ein anderes auf PackageReference basierendes Projekt verweist, das .NETStandard verwendet.</span><span class="sxs-lookup"><span data-stu-id="db591-161">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="db591-162">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="db591-162">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="db591-163">Problemumgehung:</span><span class="sxs-lookup"><span data-stu-id="db591-163">Workaround:</span></span>
<span data-ttu-id="db591-164">Zurzeit gibt es keine Problemumgehung.</span><span class="sxs-lookup"><span data-stu-id="db591-164">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="db591-165">Im Rahmen von NuGet 4.0 RTM behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="db591-165">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="db591-166">In den [Anmerkungen zu Version 4.0 RC von NuGet](../release-notes/nuget-4.0-RC.md) werden alle für NuGet 4.0 RC behobenen Probleme aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="db591-166">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

<span data-ttu-id="db591-167">**Fehler:**</span><span class="sxs-lookup"><span data-stu-id="db591-167">**Bug:**</span></span>

* <span data-ttu-id="db591-168">Die NuGet-Wiederherstellung in Visual Studio berücksichtigt die PackageId-Eigenschaft von Projekten nicht [#4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="db591-168">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

* <span data-ttu-id="db591-169">NuGet-Fehler „ProjectSystemCache“, wenn Pakete zum VSIX-Paket hinzugefügt werden ([#4545](https://github.com/NuGet/Home/issues/4545))</span><span class="sxs-lookup"><span data-stu-id="db591-169">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

* <span data-ttu-id="db591-170">Beim Packen wird eine Ausnahme ausgelöst, wenn IncludeSource in einem Projekt mit mehreren TFMs verwendet wird ([#4536](https://github.com/NuGet/Home/issues/4536))</span><span class="sxs-lookup"><span data-stu-id="db591-170">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

* <span data-ttu-id="db591-171">Visual Studio 2017 RC3 stürzt ab, wenn ein Update für die projektmappenweite Paketverwaltung verwendet wird ([#4474](https://github.com/NuGet/Home/issues/4474))</span><span class="sxs-lookup"><span data-stu-id="db591-171">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

* <span data-ttu-id="db591-172">Ein neu installiertes Paket kann nicht deinstalliert werden ([#4435](https://github.com/NuGet/Home/issues/4435))</span><span class="sxs-lookup"><span data-stu-id="db591-172">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

* <span data-ttu-id="db591-173">Wenn zu PackageRef migriert wird, weisen hybride Projektmappen ein merkwürdiges Verhalten bei der Wiederherstellung auf ([#4433](https://github.com/NuGet/Home/issues/4433))</span><span class="sxs-lookup"><span data-stu-id="db591-173">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

* <span data-ttu-id="db591-174">Wenn der Buildvorgang kurz nach dem Starten eines NuGet-Vorgangs (Installieren, Aktualisieren, Wiederherstellen) ausgeführt wird, kann dies zu einem Absturz von Visual Studio führen ([#4420](https://github.com/NuGet/Home/issues/4420))</span><span class="sxs-lookup"><span data-stu-id="db591-174">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

* <span data-ttu-id="db591-175">Benutzeroberfläche reagiert nicht: Deadlock beim Initialisieren von NuGet.SolutionRestoreManager.RestoreManagerPackage ([#4371](https://github.com/NuGet/Home/issues/4371))</span><span class="sxs-lookup"><span data-stu-id="db591-175">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

* <span data-ttu-id="db591-176">Der Befehl „add package“ sollte Versionen statt Elemente als Attribut hinzufügen ([#4325](https://github.com/NuGet/Home/issues/4325))</span><span class="sxs-lookup"><span data-stu-id="db591-176">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

* <span data-ttu-id="db591-177">„Dotnet Restore foo.sln“ schlägt fehl, wenn Konfigurationen in SLN dazu führen, dass Projekte im Wiederherstellungsdiagramm dupliziert werden (mit verschiedenen Konfigurationen) ([#4316](https://github.com/NuGet/Home/issues/4316))</span><span class="sxs-lookup"><span data-stu-id="db591-177">Dotnet Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

* <span data-ttu-id="db591-178">Pakete, die nur Inhalte enthalten ([#3668](https://github.com/NuGet/Home/issues/3668))</span><span class="sxs-lookup"><span data-stu-id="db591-178">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

* <span data-ttu-id="db591-179">Die Option des Selektors für das Paketformat standardmäßig deaktivieren ([#4468](https://github.com/NuGet/Home/issues/4468))</span><span class="sxs-lookup"><span data-stu-id="db591-179">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

* <span data-ttu-id="db591-180">Leistung: Das Projekt „CreateUAP_CSharp_VS.01.1.Create“ wurde zurückgesetzt, „Duration_TotalElapsedTime“ liegt bei 3.153,570 ms (149,1%) – </span><span class="sxs-lookup"><span data-stu-id="db591-180">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="db591-181">Baseline 26129,02 ([#4452](https://github.com/NuGet/Home/issues/4452))</span><span class="sxs-lookup"><span data-stu-id="db591-181">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

* <span data-ttu-id="db591-182">Leistung: Die Projektmappe „ManagedLangs_CS_DDRIT.0300.Rebuild“ wurde zurückgesetzt, „Duration_TotalElapsedTime“ liegt bei 1,5 Sekunden – </span><span class="sxs-lookup"><span data-stu-id="db591-182">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="db591-183">Baseline 26105 ([#4441](https://github.com/NuGet/Home/issues/4441))</span><span class="sxs-lookup"><span data-stu-id="db591-183">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

* <span data-ttu-id="db591-184">Die Nominierung schlägt in Projekten mit mehreren TFMs fehl ([#4419](https://github.com/NuGet/Home/issues/4419))</span><span class="sxs-lookup"><span data-stu-id="db591-184">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

* <span data-ttu-id="db591-185">Leistung: Die Projektmappe „WebForms_DDRIT.1200.Close“ wurde zurückgesetzt, „VM_ImagesInMemory_Total_devenv“ liegt bei 3,000 (0,5%) – </span><span class="sxs-lookup"><span data-stu-id="db591-185">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="db591-186">Baseline 26123,04 ([#4408](https://github.com/NuGet/Home/issues/4408))</span><span class="sxs-lookup"><span data-stu-id="db591-186">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

* <span data-ttu-id="db591-187">vsfeedback: Warnungen beim Packen, wenn netcoreapp1.1 angezielt wird ([#4397](https://github.com/NuGet/Home/issues/4397))</span><span class="sxs-lookup"><span data-stu-id="db591-187">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

* <span data-ttu-id="db591-188">„PathTooLongException“ wird ausgelöst, wenn versucht wird, ein neues NuGet-Paket zu einer leeren ASP.NET Core-Webanwendung hinzuzufügen ([#4391](https://github.com/NuGet/Home/issues/4391))</span><span class="sxs-lookup"><span data-stu-id="db591-188">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

* <span data-ttu-id="db591-189">„Pack“ wird zu häufig ausgeführt: „dotnet pack“ schlägt mit der Fehlermeldung „Im Zielabhängigkeitsdiagramm besteht eine Ringabhängigkeit im Zusammenhang mit Ziel ‚Pack‘.“ fehl ([#4381](https://github.com/NuGet/Home/issues/4381))</span><span class="sxs-lookup"><span data-stu-id="db591-189">Pack runs too often -- dotnet pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

* <span data-ttu-id="db591-190">„Pack“ wird zu häufig ausgeführt: Beim Generieren von NuGet-Paketen sind nicht alle Konfigurationen enthalten ([#4380](https://github.com/NuGet/Home/issues/4380))</span><span class="sxs-lookup"><span data-stu-id="db591-190">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

* <span data-ttu-id="db591-191">„NullReferenceException“ wird beim Hinzufügen von NuGet mit „PackageRef“ in C++-Projekten ausgelöst ([#4378](https://github.com/NuGet/Home/issues/4378))</span><span class="sxs-lookup"><span data-stu-id="db591-191">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

* <span data-ttu-id="db591-192">Barrierefreiheit: Die Sprachausgabe gibt das Kontrollkästchen nicht aus, das für das Auswählen der Projekte verwendet wird, für die die Pakete installiert werden sollen ([#4366](https://github.com/NuGet/Home/issues/4366))</span><span class="sxs-lookup"><span data-stu-id="db591-192">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

* <span data-ttu-id="db591-193">Das Herstellen einer Verbindung von NuGet für Visual Studio 2017 mit VSO- und VSTS-Feeds schlägt fehl (Visual Studio-Fehler 365798) ([#4365](https://github.com/NuGet/Home/issues/4365))</span><span class="sxs-lookup"><span data-stu-id="db591-193">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

* <span data-ttu-id="db591-194">„contentFiles“ speichert die Ausgabe am falschen Ort, wenn „PackagePath“ den Pfad als „contentFiles“ angibt ([#4348](https://github.com/NuGet/Home/issues/4348))</span><span class="sxs-lookup"><span data-stu-id="db591-194">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

* <span data-ttu-id="db591-195">Beim Packen des Ziels wird die PackageVersion-Eigenschaft mit dem Versionssuffix angefügt ([#4324](https://github.com/NuGet/Home/issues/4324))</span><span class="sxs-lookup"><span data-stu-id="db591-195">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

* <span data-ttu-id="db591-196">Das Angeben des Paketpfads funktioniert mit „dotnet pack“ nicht ([#4321](https://github.com/NuGet/Home/issues/4321))</span><span class="sxs-lookup"><span data-stu-id="db591-196">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

* <span data-ttu-id="db591-197">NuGet gibt während der Wiederherstellung einige Warnungen zu doppelten Importen aus ([#4304](https://github.com/NuGet/Home/issues/4304))</span><span class="sxs-lookup"><span data-stu-id="db591-197">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

* <span data-ttu-id="db591-198">Das Dialogfeld für das Auswählen des Formats des NuGet-Paket-Managers sieht im dunklen Design nicht gut aus ([#4300](https://github.com/NuGet/Home/issues/4300))</span><span class="sxs-lookup"><span data-stu-id="db591-198">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

* <span data-ttu-id="db591-199">Visual Studio stürzt beim Wiederherstellen des Builds ab ([#4298](https://github.com/NuGet/Home/issues/4298))</span><span class="sxs-lookup"><span data-stu-id="db591-199">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

* <span data-ttu-id="db591-200">Bei Visual Studio tritt ein Deadlock auf, wenn Sie den TFM zu Zielframeworks hinzufügen und dann speichern und einen Build durchführen</span><span class="sxs-lookup"><span data-stu-id="db591-200">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="db591-201">(in 10% der Fälle) ([#4295](https://github.com/NuGet/Home/issues/4295))</span><span class="sxs-lookup"><span data-stu-id="db591-201">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

* <span data-ttu-id="db591-202">„nuget pack“ gibt keine Meldung beim erfolgreichen Packen eines Projekts aus ([#4294](https://github.com/NuGet/Home/issues/4294))</span><span class="sxs-lookup"><span data-stu-id="db591-202">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

* <span data-ttu-id="db591-203">„PackTask“ schlägt fehl, da System.IO.Compression 4.1 nicht gefunden werden konnte ([#4290](https://github.com/NuGet/Home/issues/4290))</span><span class="sxs-lookup"><span data-stu-id="db591-203">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

* <span data-ttu-id="db591-204">„Pack“ wird zu häufig ausgeführt: „PackTask“ schlägt regelmäßig wegen Konflikten beim Dateizugriff fehl ([#4289](https://github.com/NuGet/Home/issues/4289))</span><span class="sxs-lookup"><span data-stu-id="db591-204">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

* <span data-ttu-id="db591-205">NuGet öffnet das Ausgabefenster während der Wiederherstellung im Hintergrund ([#4274](https://github.com/NuGet/Home/issues/4274))</span><span class="sxs-lookup"><span data-stu-id="db591-205">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

* <span data-ttu-id="db591-206">Beseitigen von „ServiceProvider“ als riskantes Codierungsmuster (das zu Abstürzen führen kann) ([#4268](https://github.com/NuGet/Home/issues/4268))</span><span class="sxs-lookup"><span data-stu-id="db591-206">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

* <span data-ttu-id="db591-207">Leistung/Benutzeroberfläche reagiert nicht: Verbessern der Lesevorgänge von DownloadTimeoutStream ([#4266](https://github.com/NuGet/Home/issues/4266))</span><span class="sxs-lookup"><span data-stu-id="db591-207">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

* <span data-ttu-id="db591-208">Bei Visual Studio tritt ein Deadlock auf, wenn Sie versuchen, ein Projekt zu schließen, bevor die Wiederherstellung von NuGet abgeschlossen ist ([#4257](https://github.com/NuGet/Home/issues/4257))</span><span class="sxs-lookup"><span data-stu-id="db591-208">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

* <span data-ttu-id="db591-209">Probleme mit „PackTask“ und dem Packen von `.nuspec` ([#4250](https://github.com/NuGet/Home/issues/4250))</span><span class="sxs-lookup"><span data-stu-id="db591-209">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

* <span data-ttu-id="db591-210">[vsfeedback] NuGet-Pakete können für neue Projekte nicht aufgelöst werden (Visual Studio muss neu gestartet werden) ([#4217](https://github.com/NuGet/Home/issues/4217))</span><span class="sxs-lookup"><span data-stu-id="db591-210">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

* <span data-ttu-id="db591-211">[vsfeedback] Das Dropdownmenü „Version“, das die verfügbaren Paketversionen anzeigt, bleibt nicht synchron mit dem ausgewählten NuGet-Paket ([#4198](https://github.com/NuGet/Home/issues/4198))</span><span class="sxs-lookup"><span data-stu-id="db591-211">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

* <span data-ttu-id="db591-212">Nuget.Client sollte „JoinableTaskFactory“ bei der Interaktion mit CPS verwenden, um Deadlocks zu verhindern ([#4185](https://github.com/NuGet/Home/issues/4185))</span><span class="sxs-lookup"><span data-stu-id="db591-212">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

* <span data-ttu-id="db591-213">NuGet 3.5.0 entpackt `.targets` nicht aus dem Paket ([#4171](https://github.com/NuGet/Home/issues/4171))</span><span class="sxs-lookup"><span data-stu-id="db591-213">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

* <span data-ttu-id="db591-214">„dotnet pack“ unterstützt in `.csproj` keine Titel ([#4150](https://github.com/NuGet/Home/issues/4150))</span><span class="sxs-lookup"><span data-stu-id="db591-214">dotnet pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

* <span data-ttu-id="db591-215">„Install-Package“ führt zu einer Fehlermeldung in Visual Studio 2017 RC ([#4127](https://github.com/NuGet/Home/issues/4127))</span><span class="sxs-lookup"><span data-stu-id="db591-215">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

* <span data-ttu-id="db591-216">Das Aktualisieren eines Pakets für .NET Core-Projekte scheint nicht zu funktionieren, da die Benutzeroberfläche das CPS-Update nicht erhält</span><span class="sxs-lookup"><span data-stu-id="db591-216">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="db591-217"> ([#4035](https://github.com/NuGet/Home/issues/4035))</span><span class="sxs-lookup"><span data-stu-id="db591-217"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

* <span data-ttu-id="db591-218">Verbesserung der Warnung für nicht aufgelöste Verweise ([#3955](https://github.com/NuGet/Home/issues/3955))</span><span class="sxs-lookup"><span data-stu-id="db591-218">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

* <span data-ttu-id="db591-219">„dotnet pack“: „ProjectReference“ verliert die Versionsinformationen ([#3953](https://github.com/NuGet/Home/issues/3953))</span><span class="sxs-lookup"><span data-stu-id="db591-219">dotnet pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

* <span data-ttu-id="db591-220">Regression der insgesamt verstrichenen Zeit von „Erstellen einer UWP-App“, „Erstellen eines Projekts“ und „Neuerstellen“ ([#3873](https://github.com/NuGet/Home/issues/3873))</span><span class="sxs-lookup"><span data-stu-id="db591-220">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

* <span data-ttu-id="db591-221">Die Meldung für die erfolgreiche Wiederherstellung wird auch angezeigt, wenn während der Wiederherstellung ein Fehler auftritt</span><span class="sxs-lookup"><span data-stu-id="db591-221">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="db591-222"> ([#3799](https://github.com/NuGet/Home/issues/3799))</span><span class="sxs-lookup"><span data-stu-id="db591-222"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

* <span data-ttu-id="db591-223">Erneutes Veröffentlichen von Nuget.CommandLine 3.4.4 auf nuget.org ([#2931](https://github.com/NuGet/Home/issues/2931))</span><span class="sxs-lookup"><span data-stu-id="db591-223">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

* <span data-ttu-id="db591-224">Beim Migrieren ändert sich das Projekt von `project.json` in `.csproj` und die Wiederherstellung schlägt fehl ([#4297](https://github.com/NuGet/Home/issues/4297))</span><span class="sxs-lookup"><span data-stu-id="db591-224">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

* <span data-ttu-id="db591-225">Die Wiederherstellung des neu erstellten xUnit-Testprojekts schlägt fehl ([#4296](https://github.com/NuGet/Home/issues/4296))</span><span class="sxs-lookup"><span data-stu-id="db591-225">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

* <span data-ttu-id="db591-226">Core-Projekte reagieren möglicherweise nicht, die Benutzeroberfläche wird beim Öffnen gesperrt ([#4269](https://github.com/NuGet/Home/issues/4269))</span><span class="sxs-lookup"><span data-stu-id="db591-226">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

* <span data-ttu-id="db591-227">Fehlerbehebung bei der TARGETS-Datei für Buildaufgaben ([#4267](https://github.com/NuGet/Home/issues/4267))</span><span class="sxs-lookup"><span data-stu-id="db591-227">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

* <span data-ttu-id="db591-228">Die Fehlerliste enthält einen Fehler nach dem Erstellen der Projektmappe, der das Projekt entlädt, auf das verwiesen wird ([#4208](https://github.com/NuGet/Home/issues/4208))</span><span class="sxs-lookup"><span data-stu-id="db591-228">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

* <span data-ttu-id="db591-229">MSB4057: „Das Ziel ‚_GenerateRestoreGraphProjectEntry‘ ist im Projekt nicht vorhanden.“</span><span class="sxs-lookup"><span data-stu-id="db591-229">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="db591-230"> ([#4194](https://github.com/NuGet/Home/issues/4194))</span><span class="sxs-lookup"><span data-stu-id="db591-230"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

* <span data-ttu-id="db591-231">vsfeedback: Die Benutzeroberfläche des NuGet-Managers für Projektmappen stürzt ab, wenn alle Projekte ausgewählt werden ([#4191](https://github.com/NuGet/Home/issues/4191))</span><span class="sxs-lookup"><span data-stu-id="db591-231">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

* <span data-ttu-id="db591-232">„MSBuildPath“ von „nuget.exe“ schlägt fehl, wenn ein nachgestellter Schrägstrich vorhanden ist ([#4180](https://github.com/NuGet/Home/issues/4180))</span><span class="sxs-lookup"><span data-stu-id="db591-232">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

* <span data-ttu-id="db591-233">vsfeedback: Die Wiederherstellung von NuGet gibt für das LinqToTwitter-Projekt mehrere Warnungen für Projektverweise aus ([#4156](https://github.com/NuGet/Home/issues/4156))</span><span class="sxs-lookup"><span data-stu-id="db591-233">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

* <span data-ttu-id="db591-234">Beim Packen von `.csproj` aus wird das Attribut „minClientVersion“ nicht eingeschlossen ([#4135](https://github.com/NuGet/Home/issues/4135))</span><span class="sxs-lookup"><span data-stu-id="db591-234">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

* <span data-ttu-id="db591-235">„NuGet.Build.Tasks.Pack.dll“ wird in Visual Studio 2017 als verzögert signiert (d15rel 26014.00) ([#4122](https://github.com/NuGet/Home/issues/4122))</span><span class="sxs-lookup"><span data-stu-id="db591-235">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

* <span data-ttu-id="db591-236">VSFeedback: Wiederherstellung eines Visual Studio 2015-Projekts, das mit CMake 3.7.1 generiert wurde, schlägt fehl ([#4114](https://github.com/NuGet/Home/issues/4114))</span><span class="sxs-lookup"><span data-stu-id="db591-236">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

* <span data-ttu-id="db591-237">VSFeedback: Fehler bei der Wiederherstellung können die umfangreicheren Fehlermeldungen des Builds verdecken ([#4113](https://github.com/NuGet/Home/issues/4113))</span><span class="sxs-lookup"><span data-stu-id="db591-237">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

* <span data-ttu-id="db591-238">[VSFeedback] Fehler beim Wiederherstellen von NuGet-Paketen für das Websiteprojekt: „Der Wert darf nicht NULL sein.“</span><span class="sxs-lookup"><span data-stu-id="db591-238">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="db591-239"> ([#4092](https://github.com/NuGet/Home/issues/4092))</span><span class="sxs-lookup"><span data-stu-id="db591-239"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

* <span data-ttu-id="db591-240">Bei der Migration wird eine Ausnahme beim Objektverweis in „NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker“ ausgelöst ([#4067](https://github.com/NuGet/Home/issues/4067))</span><span class="sxs-lookup"><span data-stu-id="db591-240">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

* <span data-ttu-id="db591-241">„dotnet pack“ sollte Tools mit den Versionen packen, für die das Paket erstellt wurde ([#4063](https://github.com/NuGet/Home/issues/4063))</span><span class="sxs-lookup"><span data-stu-id="db591-241">dotnet pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

* <span data-ttu-id="db591-242">Die neue Wiederherstellung im Hintergrund zeigt Millisekunden in der Statusleiste an, obwohl die Wiederherstellung mehrere Sekunden dauert ([#4036](https://github.com/NuGet/Home/issues/4036))</span><span class="sxs-lookup"><span data-stu-id="db591-242">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

* <span data-ttu-id="db591-243">Tippfehler bei „Fehler beim Auflösen aller Projektverweise...“ ([#4018](https://github.com/NuGet/Home/issues/4018))</span><span class="sxs-lookup"><span data-stu-id="db591-243">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

* <span data-ttu-id="db591-244">Aktivieren von PCM-Workflows in Szenarios mit Paketverweisen ([#4016](https://github.com/NuGet/Home/issues/4016))</span><span class="sxs-lookup"><span data-stu-id="db591-244">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

* <span data-ttu-id="db591-245">Die installierten Pakete können auf der Benutzeroberfläche des Paket-Managers nicht gefunden werden ([#4015](https://github.com/NuGet/Home/issues/4015))</span><span class="sxs-lookup"><span data-stu-id="db591-245">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

* <span data-ttu-id="db591-246">„dotnet pack“ schlägt fehl, wenn „PackagePath“ leer ist ([#3993](https://github.com/NuGet/Home/issues/3993))</span><span class="sxs-lookup"><span data-stu-id="db591-246">dotnet pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

* <span data-ttu-id="db591-247">Die Wiederherstellungsaufgabe schlägt in Szenarios mit mehreren Benutzern fehl ([#3897](https://github.com/NuGet/Home/issues/3897))</span><span class="sxs-lookup"><span data-stu-id="db591-247">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

* <span data-ttu-id="db591-248">Der Inhaltstyp kann nicht geändert werden, wenn mithilfe der NuGet-Packaufgabe gepackt wird ([#3895](https://github.com/NuGet/Home/issues/3895))</span><span class="sxs-lookup"><span data-stu-id="db591-248">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

* <span data-ttu-id="db591-249">Die Standardkopien von „ContentFiles“ sind für „MsBuild /t:pack“ falsch ([#3894](https://github.com/NuGet/Home/issues/3894))</span><span class="sxs-lookup"><span data-stu-id="db591-249">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

* <span data-ttu-id="db591-250">Bei der Installation der Paketwiederherstellung wird die Meldung für das Wiederherstellen von Paketen doppelt protokolliert ([#3785](https://github.com/NuGet/Home/issues/3785))</span><span class="sxs-lookup"><span data-stu-id="db591-250">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

* <span data-ttu-id="db591-251">Entfernen der Sicherungen: Die Wiederherstellung des Abschnitts „Runtimes“ sollte nur für das aktuelle Projekt gelten ([#3768](https://github.com/NuGet/Home/issues/3768))</span><span class="sxs-lookup"><span data-stu-id="db591-251">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

* <span data-ttu-id="db591-252">Die Packaufgabe fügt Inhaltsdateien in „content/“ und „contentFiles/“ ein ([#3718](https://github.com/NuGet/Home/issues/3718))</span><span class="sxs-lookup"><span data-stu-id="db591-252">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

* <span data-ttu-id="db591-253">„dotnet pack3“ teilt Tags zusätzlich ([#3701](https://github.com/NuGet/Home/issues/3701))</span><span class="sxs-lookup"><span data-stu-id="db591-253">dotnet pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

* <span data-ttu-id="db591-254">dotnet pack: Beim Packen von Projekten mit Paketverweisen wird eine Warnung wegen doppelten Imports ausgegeben ([#3665](https://github.com/NuGet/Home/issues/3665))</span><span class="sxs-lookup"><span data-stu-id="db591-254">dotnet pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

* <span data-ttu-id="db591-255">Die Wiederherstellungsprotokollierung wird in Visual Studio nicht immer angezeigt ([#3633](https://github.com/NuGet/Home/issues/3633))</span><span class="sxs-lookup"><span data-stu-id="db591-255">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

* <span data-ttu-id="db591-256">Der lokale Hilfetexte in NuGet erwähnt weiterhin den Paketcache ([#3592](https://github.com/NuGet/Home/issues/3592))</span><span class="sxs-lookup"><span data-stu-id="db591-256">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

* <span data-ttu-id="db591-257">„Restore3“ koppelt „PackageReferences“ mit „TargetFrameworks“</span><span class="sxs-lookup"><span data-stu-id="db591-257">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="db591-258"> ([#3504](https://github.com/NuGet/Home/issues/3504))</span><span class="sxs-lookup"><span data-stu-id="db591-258"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

* <span data-ttu-id="db591-259">NuGet wählt in der Eingabeaufforderung von VS „15“ Developer (Vorschauversion 4)</span><span class="sxs-lookup"><span data-stu-id="db591-259">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="db591-260">eine unerwartete Version von MSBuild aus ([#3408](https://github.com/NuGet/Home/issues/3408))</span><span class="sxs-lookup"><span data-stu-id="db591-260">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

* <span data-ttu-id="db591-261">TARGETS- und PROPS-Dateien sollten auch bei einer fehlerhaften Wiederherstellung geschrieben werden ([#3399](https://github.com/NuGet/Home/issues/3399))</span><span class="sxs-lookup"><span data-stu-id="db591-261">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

* <span data-ttu-id="db591-262">NuGet berücksichtigt während der Wiederherstellung nicht die gleichen Kompatibilitätsshims wie MSBuild, wenn diese über die Visual Studio 2015-Eingabeaufforderung durchgeführt wird ([#3387](https://github.com/NuGet/Home/issues/3387))</span><span class="sxs-lookup"><span data-stu-id="db591-262">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

* <span data-ttu-id="db591-263">Reaktivieren von „PackFromProjectWithDevelopmentDependencySet“ für Visual Studio 2015 ([#3272](https://github.com/NuGet/Home/issues/3272))</span><span class="sxs-lookup"><span data-stu-id="db591-263">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

* <span data-ttu-id="db591-264">Probleme bei Blend mit NuGet ([#4043](https://github.com/NuGet/Home/issues/4043))</span><span class="sxs-lookup"><span data-stu-id="db591-264">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

* <span data-ttu-id="db591-265">Integrieren von 4.0.0.2067 in CLI- und SDK-Repositorys für die Bereitstellung mit RC2 ([#4029](https://github.com/NuGet/Home/issues/4029))</span><span class="sxs-lookup"><span data-stu-id="db591-265">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

* <span data-ttu-id="db591-266">Visual Studio reagiert nicht, wenn eine neue Core-Konsolen-App erstellt und eine Projektmappe geschlossen, geöffnet und dann wieder geschlossen wird ([#4008](https://github.com/NuGet/Home/issues/4008))</span><span class="sxs-lookup"><span data-stu-id="db591-266">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

* <span data-ttu-id="db591-267">Absturz beim Öffnen des Projekts mit „d15prerel.25916.01“ ([#3982](https://github.com/NuGet/Home/issues/3982))</span><span class="sxs-lookup"><span data-stu-id="db591-267">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

* <span data-ttu-id="db591-268">Fehler bei der doc/help-Meldung für lokale Variablen von dotnet bzw. „nuget.exe“ ([#3919](https://github.com/NuGet/Home/issues/3919))</span><span class="sxs-lookup"><span data-stu-id="db591-268">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

* <span data-ttu-id="db591-269">Überprüfen von „PackTask“ nach Problemen mit vorangestellten oder nachstehenden Leerräumen ([#3906](https://github.com/NuGet/Home/issues/3906))</span><span class="sxs-lookup"><span data-stu-id="db591-269">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

* <span data-ttu-id="db591-270">„dotnet pack“ packt von „obj“ statt von „bin“ ([#3880](https://github.com/NuGet/Home/issues/3880))</span><span class="sxs-lookup"><span data-stu-id="db591-270">dotnet pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

* <span data-ttu-id="db591-271">„dotnet pack“ scheint die Version von „ProjectReference“ immer auf 1.0.0 festzulegen ([#3874](https://github.com/NuGet/Home/issues/3874))</span><span class="sxs-lookup"><span data-stu-id="db591-271">dotnet pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

* <span data-ttu-id="db591-272">„dotnet pack“ schlägt trotz Projektverweisen und <TargetFramework> fehl ([#3865](https://github.com/NuGet/Home/issues/3865))</span><span class="sxs-lookup"><span data-stu-id="db591-272">dotnet pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

* <span data-ttu-id="db591-273">„LockRecursionException“ in „ProjectSystemCache.TryGetProjectNameByShortName“ ([#3861](https://github.com/NuGet/Home/issues/3861))</span><span class="sxs-lookup"><span data-stu-id="db591-273">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

* <span data-ttu-id="db591-274">Leerräume aus MSBuild-Eigenschaften entfernen ([#3819](https://github.com/NuGet/Home/issues/3819))</span><span class="sxs-lookup"><span data-stu-id="db591-274">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

* <span data-ttu-id="db591-275">Konsolidieren der beiden Projektereignisse, die beim Laden des Projekts ausgelöst werden ([#3759](https://github.com/NuGet/Home/issues/3759))</span><span class="sxs-lookup"><span data-stu-id="db591-275">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

* <span data-ttu-id="db591-276">Die P2P-Bibliotheken in der `project.assets.json`-Datei besitzen die falsche Version ([#3748](https://github.com/NuGet/Home/issues/3748))</span><span class="sxs-lookup"><span data-stu-id="db591-276">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

* <span data-ttu-id="db591-277">Die Wiederherstellung stürzt aufgrund eines nicht reagierenden Feeds und eines nicht verfügbaren Pakets ab ([#3672](https://github.com/NuGet/Home/issues/3672))</span><span class="sxs-lookup"><span data-stu-id="db591-277">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

* <span data-ttu-id="db591-278">„nuget.exe“ reagiert bei einer großen Menge von Fehlerausgaben von MSBuild möglicherweise nicht ([#3572](https://github.com/NuGet/Home/issues/3572))</span><span class="sxs-lookup"><span data-stu-id="db591-278">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

* <span data-ttu-id="db591-279">Die Wiederherstellung während des Builds schlägt für Blend beim ersten Mal fehl, ist beim zweiten Mal jedoch erfolgreich (behobenes Visual Studio-Szenario) ([#2121](https://github.com/NuGet/Home/issues/2121))</span><span class="sxs-lookup"><span data-stu-id="db591-279">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

<span data-ttu-id="db591-280">**DCR:**</span><span class="sxs-lookup"><span data-stu-id="db591-280">**DCR:**</span></span>

* <span data-ttu-id="db591-281">Migrieren von V2 VSIX zu V3 VSIX ([#4196](https://github.com/NuGet/Home/issues/4196))</span><span class="sxs-lookup"><span data-stu-id="db591-281">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

* <span data-ttu-id="db591-282">NuGet sollte über einen Mechanismus verfügen, um den Pfad für die Sperrdatei in MSBuild abzurufen ([#3351](https://github.com/NuGet/Home/issues/3351))</span><span class="sxs-lookup"><span data-stu-id="db591-282">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

* <span data-ttu-id="db591-283">Hinzufügen von Buildobjekten zu der Kompatibilitätsprüfung und der Objektdatei des TFM ([#3296](https://github.com/NuGet/Home/issues/3296))</span><span class="sxs-lookup"><span data-stu-id="db591-283">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

* <span data-ttu-id="db591-284">Definieren einer neuen „ProjectCapability“ namens „Pack“ in den Packzielen zum Aktivieren von Paketfunktionen ([#4146](https://github.com/NuGet/Home/issues/4146))</span><span class="sxs-lookup"><span data-stu-id="db591-284">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

* <span data-ttu-id="db591-285">Ausführen von Packzielen als Postbuildziel bedingt durch die MSBuild-Eigenschaft „GeneratePackageOnBuild“ ([#4145](https://github.com/NuGet/Home/issues/4145))</span><span class="sxs-lookup"><span data-stu-id="db591-285">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

* <span data-ttu-id="db591-286">Verwenden der NuGet-Eigenschaft „RestoreProjectStyle“ zum Erstellen eines spezifischen NuGet-Projekts ([#4134](https://github.com/NuGet/Home/issues/4134))</span><span class="sxs-lookup"><span data-stu-id="db591-286">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

* <span data-ttu-id="db591-287">Anpassen der Wiederherstellung für geänderte transitive Projektverweise ([#4076](https://github.com/NuGet/Home/issues/4076))</span><span class="sxs-lookup"><span data-stu-id="db591-287">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

* <span data-ttu-id="db591-288">Hinzufügen von NuGet-Eigenschaften zur Zieldatei für Nicht-UWP-Projekte ([#4030](https://github.com/NuGet/Home/issues/4030))</span><span class="sxs-lookup"><span data-stu-id="db591-288">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

* <span data-ttu-id="db591-289">UWP-Unterstützung für „TargetPlatformVersion“ ([#3923](https://github.com/NuGet/Home/issues/3923))</span><span class="sxs-lookup"><span data-stu-id="db591-289">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

* <span data-ttu-id="db591-290">Übermitteln der Projektverweismetadaten an das NuGet-Projektsystem ([#3922](https://github.com/NuGet/Home/issues/3922))</span><span class="sxs-lookup"><span data-stu-id="db591-290">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

* <span data-ttu-id="db591-291">Hinzufügen der Benutzeroberfläche für den Packmodus ([#3921](https://github.com/NuGet/Home/issues/3921))</span><span class="sxs-lookup"><span data-stu-id="db591-291">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

* <span data-ttu-id="db591-292">Für die veraltete `.csproj`-Datei müssen „NugetTargetMoniker“ und „RuntimeIdentifiers“ im Projekt und in den Zielen festgelegt sein ([#3854](https://github.com/NuGet/Home/issues/3854))</span><span class="sxs-lookup"><span data-stu-id="db591-292">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

* <span data-ttu-id="db591-293">Das Installieren des Pakets überschneidet sich möglicherweise mit der automatischen Wiederherstellung ([#3836](https://github.com/NuGet/Home/issues/3836))</span><span class="sxs-lookup"><span data-stu-id="db591-293">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

* <span data-ttu-id="db591-294">Das Kontextmenü „QueryStatus“ wird nicht angezeigt, wenn „VSPackage“ nicht geladen wird ([#3835](https://github.com/NuGet/Home/issues/3835))</span><span class="sxs-lookup"><span data-stu-id="db591-294">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

* <span data-ttu-id="db591-295">Beim Wiederherstellen von Projektmappen und Builds werden weiterhin Dialogfelder angezeigt ([#3789](https://github.com/NuGet/Home/issues/3789))</span><span class="sxs-lookup"><span data-stu-id="db591-295">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

* <span data-ttu-id="db591-296">Isolieren der VSSDK-Version während des Projektmappenbuilds von „NuGet.Clients“ ([#3890](https://github.com/NuGet/Home/issues/3890))</span><span class="sxs-lookup"><span data-stu-id="db591-296">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

<span data-ttu-id="db591-297">**Feature:**</span><span class="sxs-lookup"><span data-stu-id="db591-297">**Feature:**</span></span>

* <span data-ttu-id="db591-298">Lokalisieren von Zeichenfolgen in „NuGet.Core.sln“ ([#2041](https://github.com/NuGet/Home/issues/2041))</span><span class="sxs-lookup"><span data-stu-id="db591-298">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

* <span data-ttu-id="db591-299">NuGet erzwingt das Laden von Webanwendungsprojekten im LSL-Modus ([#4258](https://github.com/NuGet/Home/issues/4258))</span><span class="sxs-lookup"><span data-stu-id="db591-299">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

* <span data-ttu-id="db591-300">Unterstützung für das PackageReference-Element mit der AutoReferenced-Eigenschaft, um Versionsänderungen in der Benutzeroberfläche für mit dem SDK installierte Pakete zu blockieren ([#4044](https://github.com/NuGet/Home/issues/4044))</span><span class="sxs-lookup"><span data-stu-id="db591-300">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

* <span data-ttu-id="db591-301">Ordnungsgemäßes Übermitteln von „PackageSpec.Version“ für alle Projektabhängigkeiten (PackageRef) ([#3902](https://github.com/NuGet/Home/issues/3902))</span><span class="sxs-lookup"><span data-stu-id="db591-301">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

* <span data-ttu-id="db591-302">Unterstützung für das Entfernen von Verweisen in der `.csproj`-Datei über die Befehlszeile ([#4101](https://github.com/NuGet/Home/issues/4101))</span><span class="sxs-lookup"><span data-stu-id="db591-302">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

* <span data-ttu-id="db591-303">Unterstützung für das Wiederherstellen von PackageReference-Projekten (normal und XPlat) und für den Lightweight-Ladevorgang für Projektmappen ([#4003](https://github.com/NuGet/Home/issues/4003))</span><span class="sxs-lookup"><span data-stu-id="db591-303">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

* <span data-ttu-id="db591-304">Unterstützung für das Hinzufügen von Verweisen in der `.csproj`-Datei über die Befehlszeile ([#3751](https://github.com/NuGet/Home/issues/3751))</span><span class="sxs-lookup"><span data-stu-id="db591-304">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

* <span data-ttu-id="db591-305">Unterstützung der NuGet-Wiederherstellung für den Lightweight-Ladevorgang für Projektmappen für `packages.config` oder `project.json` ([#3711](https://github.com/NuGet/Home/issues/3711))</span><span class="sxs-lookup"><span data-stu-id="db591-305">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

* <span data-ttu-id="db591-306">Unterstützung für „contentFiles“ in durch NuGet generierten Zieldateien ([#3683](https://github.com/NuGet/Home/issues/3683))</span><span class="sxs-lookup"><span data-stu-id="db591-306">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

* <span data-ttu-id="db591-307">Einrichten einer Mono-CI mithilfe von MSBuild für die Überprüfung von „nuget.exe“ unter Mac ([#3646](https://github.com/NuGet/Home/issues/3646))</span><span class="sxs-lookup"><span data-stu-id="db591-307">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

* <span data-ttu-id="db591-308">Verschieben von NuGet aus den NuGet.Core-Abhängigkeiten (V2) ([#3645](https://github.com/NuGet/Home/issues/3645))</span><span class="sxs-lookup"><span data-stu-id="db591-308">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>


## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="db591-309">Links zu GitHub-Problemen, die in RTM behoben wurden:</span><span class="sxs-lookup"><span data-stu-id="db591-309">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="db591-310">Probleme: Liste 1</span><span class="sxs-lookup"><span data-stu-id="db591-310">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RTM")  
[<span data-ttu-id="db591-311">Probleme: Liste 2</span><span class="sxs-lookup"><span data-stu-id="db591-311">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC4")  
[<span data-ttu-id="db591-312">Probleme: Liste 3</span><span class="sxs-lookup"><span data-stu-id="db591-312">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC3")  
[<span data-ttu-id="db591-313">Probleme: Liste 4</span><span class="sxs-lookup"><span data-stu-id="db591-313">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC2")  
[<span data-ttu-id="db591-314">Probleme: Liste 5</span><span class="sxs-lookup"><span data-stu-id="db591-314">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC")

