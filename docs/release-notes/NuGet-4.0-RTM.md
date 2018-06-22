---
title: Anmerkungen zu Version 4.0 RC von NuGet
description: Anmerkungen zu Version 4.0 RTM von NuGet, einschließlich bekannter Fehler, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: f1c5408f75966068e8fa11e63118426bbf562047
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2018
ms.locfileid: "32045086"
---
# <a name="nuget-40-rtm-release-notes"></a><span data-ttu-id="81cff-103">Anmerkungen zu Version 4.0 RTM von NuGet</span><span class="sxs-lookup"><span data-stu-id="81cff-103">NuGet 4.0 RTM Release Notes</span></span>

<span data-ttu-id="81cff-104">In [Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) ist NuGet 4.0 enthalten. Dieses wurde in Qualität und Leistungsfähigkeit verbessert und erweitert die Funktionalität von Visual Studio um Unterstützung für .Net Core.</span><span class="sxs-lookup"><span data-stu-id="81cff-104">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="81cff-105">Die Verbesserungen in diesem Release betreffen die Unterstützung für PackageReference, NuGet-Befehle als MSBuild-Ziele, die Paketwiederherstellung im Hintergrund und vieles mehr.</span><span class="sxs-lookup"><span data-stu-id="81cff-105">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="81cff-106">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="81cff-106">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="81cff-107">Möglicher Fehler bei der NuGet-Wiederherstellung, wenn mehrere Projekte vorhanden sind, die auf ein anderes Projekt in einer Projektmappe verweisen</span><span class="sxs-lookup"><span data-stu-id="81cff-107">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="81cff-108">Problem</span><span class="sxs-lookup"><span data-stu-id="81cff-108">Issue</span></span>

<span data-ttu-id="81cff-109">Die NuGet-Wiederherstellung funktioniert möglicherweise nicht, wenn in einer Projektmappe Projektverweise auf das gleiche Projekt mit abweichender Groß-/Kleinschreibung oder mit anderen relativen Pfaden vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="81cff-109">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="81cff-110">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="81cff-110">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="81cff-111">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="81cff-111">Workaround</span></span>

<span data-ttu-id="81cff-112">Ändern Sie die Schreibweisen bzw. relativen Pfade so, dass sie für alle Projektverweise übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="81cff-112">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="81cff-113">Beim Verwenden der Paket-Manager-Konsole funktioniert die EINGABETASTE ggf. nicht</span><span class="sxs-lookup"><span data-stu-id="81cff-113">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="81cff-114">Problem</span><span class="sxs-lookup"><span data-stu-id="81cff-114">Issue</span></span>

<span data-ttu-id="81cff-115">Gelegentlich kann es vorkommen, dass die EINGABETASTE in der Paket-Manager-Konsole nicht funktioniert.</span><span class="sxs-lookup"><span data-stu-id="81cff-115">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="81cff-116">Wenn dieses Problem auftritt, überprüfen Sie den Fortschritt für diese Korrektur und stellen Sie zusätzliche hilfreiche Informationen zu den Reproduktionsschritten bereit.</span><span class="sxs-lookup"><span data-stu-id="81cff-116">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="81cff-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="81cff-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="81cff-118">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="81cff-118">Workaround</span></span>

<span data-ttu-id="81cff-119">Starten Sie Visual Studio neu und öffnen Sie die Paketverwaltungskonsole, bevor Sie die Projektmappe öffnen.</span><span class="sxs-lookup"><span data-stu-id="81cff-119">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="81cff-120">Alternativ können Sie versuchen, die Datei `project.lock.json` zu löschen und dann erneut wiederherzustellen.</span><span class="sxs-lookup"><span data-stu-id="81cff-120">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="81cff-121">In .NET Core-Projekten kann eine Wiederherstellungsendlosschleife auftreten, wenn Sie ein Paket mit einer Assembly verwenden, die eine ungültige Signatur enthält</span><span class="sxs-lookup"><span data-stu-id="81cff-121">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>

#### <a name="issue"></a><span data-ttu-id="81cff-122">Problem</span><span class="sxs-lookup"><span data-stu-id="81cff-122">Issue</span></span>

<span data-ttu-id="81cff-123">Bei der Verwendung eines Pakets mit einer Assembly, die eine ungültige Signatur enthält, oder beim Festlegen der Paketversion mit dem DateTime-Ticker tritt gelegentlich bei der automatischen Paketwiederherstellung eine Endlosschleife auf.</span><span class="sxs-lookup"><span data-stu-id="81cff-123">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="81cff-124">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="81cff-124">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="81cff-125">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="81cff-125">Workaround</span></span>

<span data-ttu-id="81cff-126">Zurzeit gibt es keine Problemumgehung.</span><span class="sxs-lookup"><span data-stu-id="81cff-126">There is no workaround at this time.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="81cff-127">Sie können DotNetCLITools nicht mit dem NuGet-Paket-Manager anzeigen, hinzufügen oder aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="81cff-127">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="81cff-128">Problem</span><span class="sxs-lookup"><span data-stu-id="81cff-128">Issue</span></span>

<span data-ttu-id="81cff-129">Der NuGet-Paket-Manager zeigt die DotNetCLITools nicht an und ermöglicht auch kein Hinzufügen/Aktualisieren dieser Tools.</span><span class="sxs-lookup"><span data-stu-id="81cff-129">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="81cff-130">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="81cff-130">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="81cff-131">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="81cff-131">Workaround</span></span>

<span data-ttu-id="81cff-132">DotNetCLIToolReferences muss in der Projektdatei manuell bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="81cff-132">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="81cff-133">Bei der NuGet-Wiederherstellung tritt ein Fehler auf, wenn Sie PackageId-Eigenschaft für Projekte festlegen</span><span class="sxs-lookup"><span data-stu-id="81cff-133">NuGet restore will fail when you set PackageId property for projects</span></span>

#### <a name="issue"></a><span data-ttu-id="81cff-134">Problem</span><span class="sxs-lookup"><span data-stu-id="81cff-134">Issue</span></span>

<span data-ttu-id="81cff-135">Bei .NET Core-Projekten respektiert die NuGet-Wiederherstellung in Visual Studio die PackageId-Eigenschaft von Projekten nicht.</span><span class="sxs-lookup"><span data-stu-id="81cff-135">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="81cff-136">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="81cff-136">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="81cff-137">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="81cff-137">Workaround</span></span>

<span data-ttu-id="81cff-138">Führen Sie die Wiederherstellung mithilfe der Befehlszeile aus.</span><span class="sxs-lookup"><span data-stu-id="81cff-138">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="81cff-139">Wenn das Projekt keinen Ordner „obj“ aufweist, tritt bei der Paketwiederherstellung ggf. ein Fehler auf</span><span class="sxs-lookup"><span data-stu-id="81cff-139">When your project does not have 'obj' folder, package restore may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="81cff-140">Problem</span><span class="sxs-lookup"><span data-stu-id="81cff-140">Issue</span></span>

<span data-ttu-id="81cff-141">Visual Studio stellt PackageReferences nicht wieder her, wenn der Ordner „obj“ gelöscht wurde.</span><span class="sxs-lookup"><span data-stu-id="81cff-141">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="81cff-142">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="81cff-142">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="81cff-143">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="81cff-143">Workaround</span></span>

<span data-ttu-id="81cff-144">Erstellen Sie den Ordner „obj“ manuell. Die Wiederherstellung sollte dann funktionieren.</span><span class="sxs-lookup"><span data-stu-id="81cff-144">Create 'obj' folder manually and the restore should work.</span></span>

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="81cff-145">Beim manuellen Aktualisieren von Paketen mithilfe von „Update-Paket“ in der Konsole tritt ggf ein Fehler auf</span><span class="sxs-lookup"><span data-stu-id="81cff-145">Manually updating packages using Update-Package in console may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="81cff-146">Problem</span><span class="sxs-lookup"><span data-stu-id="81cff-146">Issue</span></span>

<span data-ttu-id="81cff-147">Das manuelle Verwenden von „Update-Package“ in der Konsole funktioniert nur für PackageReferences-Projekte, die soeben konvertiert wurden.</span><span class="sxs-lookup"><span data-stu-id="81cff-147">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="81cff-148">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="81cff-148">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="81cff-149">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="81cff-149">Workaround</span></span>

<span data-ttu-id="81cff-150">Zurzeit gibt es keine Problemumgehung.</span><span class="sxs-lookup"><span data-stu-id="81cff-150">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="81cff-151">Die Neuzuweisung der Framework-Zielversion kann zu unvollständigen IntelliSense-Funktionen führen</span><span class="sxs-lookup"><span data-stu-id="81cff-151">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="81cff-152">Problem</span><span class="sxs-lookup"><span data-stu-id="81cff-152">Issue</span></span>

<span data-ttu-id="81cff-153">Die Neuzuweisung der Framework-Zielversion kann zu unvollständigen IntelliSense-Funktionen in Visual Studio führen.</span><span class="sxs-lookup"><span data-stu-id="81cff-153">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="81cff-154">Dies geschieht, wenn Sie PackageReferences als Paket-Manager-Format verwenden.</span><span class="sxs-lookup"><span data-stu-id="81cff-154">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="81cff-155">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="81cff-155">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="81cff-156">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="81cff-156">Workaround</span></span>

<span data-ttu-id="81cff-157">Führen Sie eine manuelle Wiederherstellung aus.</span><span class="sxs-lookup"><span data-stu-id="81cff-157">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="81cff-158">Fehler von „msbuild /t:restore“ , wenn ein Projekt, das .NET461 als Ziel verwendet, auf ein anderes Projekt verweist, das .NETStandard verwendet</span><span class="sxs-lookup"><span data-stu-id="81cff-158">msbuild /t:restore fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="81cff-159">Problem</span><span class="sxs-lookup"><span data-stu-id="81cff-159">Issue</span></span>

<span data-ttu-id="81cff-160">Bei „msbuild /t:restore“ tritt ein Fehler auf, wenn ein auf PackageReference basierendes Projekt mit dem Ziel .NET461 auf ein anderes auf PackageReference basierendes Projekt verweist, das .NETStandard verwendet.</span><span class="sxs-lookup"><span data-stu-id="81cff-160">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="81cff-161">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="81cff-161">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="81cff-162">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="81cff-162">Workaround</span></span>

<span data-ttu-id="81cff-163">Zurzeit gibt es keine Problemumgehung.</span><span class="sxs-lookup"><span data-stu-id="81cff-163">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="81cff-164">Im Rahmen von NuGet 4.0 RTM behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="81cff-164">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="81cff-165">In den [Anmerkungen zu Version 4.0 RC von NuGet](../release-notes/nuget-4.0-RC.md) werden alle für NuGet 4.0 RC behobenen Probleme aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="81cff-165">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

### <a name="features"></a><span data-ttu-id="81cff-166">Features</span><span class="sxs-lookup"><span data-stu-id="81cff-166">Features</span></span>

- <span data-ttu-id="81cff-167">Lokalisieren von Zeichenfolgen in „NuGet.Core.sln“ ([#2041](https://github.com/NuGet/Home/issues/2041))</span><span class="sxs-lookup"><span data-stu-id="81cff-167">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

- <span data-ttu-id="81cff-168">NuGet erzwingt das Laden von Webanwendungsprojekten im LSL-Modus ([#4258](https://github.com/NuGet/Home/issues/4258))</span><span class="sxs-lookup"><span data-stu-id="81cff-168">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

- <span data-ttu-id="81cff-169">Unterstützung für das PackageReference-Element mit der AutoReferenced-Eigenschaft, um Versionsänderungen in der Benutzeroberfläche für mit dem SDK installierte Pakete zu blockieren ([#4044](https://github.com/NuGet/Home/issues/4044))</span><span class="sxs-lookup"><span data-stu-id="81cff-169">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

- <span data-ttu-id="81cff-170">Ordnungsgemäßes Übermitteln von „PackageSpec.Version“ für alle Projektabhängigkeiten (PackageRef) ([#3902](https://github.com/NuGet/Home/issues/3902))</span><span class="sxs-lookup"><span data-stu-id="81cff-170">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

- <span data-ttu-id="81cff-171">Unterstützung für das Entfernen von Verweisen in der `.csproj`-Datei über die Befehlszeile ([#4101](https://github.com/NuGet/Home/issues/4101))</span><span class="sxs-lookup"><span data-stu-id="81cff-171">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

- <span data-ttu-id="81cff-172">Unterstützung für das Wiederherstellen von PackageReference-Projekten (normal und XPlat) und für den Lightweight-Ladevorgang für Projektmappen ([#4003](https://github.com/NuGet/Home/issues/4003))</span><span class="sxs-lookup"><span data-stu-id="81cff-172">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

- <span data-ttu-id="81cff-173">Unterstützung für das Hinzufügen von Verweisen in der `.csproj`-Datei über die Befehlszeile ([#3751](https://github.com/NuGet/Home/issues/3751))</span><span class="sxs-lookup"><span data-stu-id="81cff-173">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

- <span data-ttu-id="81cff-174">Unterstützung der NuGet-Wiederherstellung für den Lightweight-Ladevorgang für Projektmappen für `packages.config` oder `project.json` ([#3711](https://github.com/NuGet/Home/issues/3711))</span><span class="sxs-lookup"><span data-stu-id="81cff-174">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

- <span data-ttu-id="81cff-175">Unterstützung für „contentFiles“ in durch NuGet generierten Zieldateien ([#3683](https://github.com/NuGet/Home/issues/3683))</span><span class="sxs-lookup"><span data-stu-id="81cff-175">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

- <span data-ttu-id="81cff-176">Einrichten einer Mono-CI mithilfe von MSBuild für die Überprüfung von „nuget.exe“ unter Mac ([#3646](https://github.com/NuGet/Home/issues/3646))</span><span class="sxs-lookup"><span data-stu-id="81cff-176">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

- <span data-ttu-id="81cff-177">Verschieben von NuGet aus den NuGet.Core-Abhängigkeiten (V2) ([#3645](https://github.com/NuGet/Home/issues/3645))</span><span class="sxs-lookup"><span data-stu-id="81cff-177">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>

### <a name="bugs"></a><span data-ttu-id="81cff-178">Fehler</span><span class="sxs-lookup"><span data-stu-id="81cff-178">Bugs</span></span>

- <span data-ttu-id="81cff-179">Die NuGet-Wiederherstellung in Visual Studio berücksichtigt die PackageId-Eigenschaft von Projekten nicht [#4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="81cff-179">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

- <span data-ttu-id="81cff-180">NuGet-Fehler „ProjectSystemCache“, wenn Pakete zum VSIX-Paket hinzugefügt werden ([#4545](https://github.com/NuGet/Home/issues/4545))</span><span class="sxs-lookup"><span data-stu-id="81cff-180">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

- <span data-ttu-id="81cff-181">Beim Packen wird eine Ausnahme ausgelöst, wenn IncludeSource in einem Projekt mit mehreren TFMs verwendet wird ([#4536](https://github.com/NuGet/Home/issues/4536))</span><span class="sxs-lookup"><span data-stu-id="81cff-181">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

- <span data-ttu-id="81cff-182">Visual Studio 2017 RC3 stürzt ab, wenn ein Update für die projektmappenweite Paketverwaltung verwendet wird ([#4474](https://github.com/NuGet/Home/issues/4474))</span><span class="sxs-lookup"><span data-stu-id="81cff-182">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

- <span data-ttu-id="81cff-183">Ein neu installiertes Paket kann nicht deinstalliert werden ([#4435](https://github.com/NuGet/Home/issues/4435))</span><span class="sxs-lookup"><span data-stu-id="81cff-183">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

- <span data-ttu-id="81cff-184">Wenn zu PackageRef migriert wird, weisen hybride Projektmappen ein merkwürdiges Verhalten bei der Wiederherstellung auf ([#4433](https://github.com/NuGet/Home/issues/4433))</span><span class="sxs-lookup"><span data-stu-id="81cff-184">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

- <span data-ttu-id="81cff-185">Wenn der Buildvorgang kurz nach dem Starten eines NuGet-Vorgangs (Installieren, Aktualisieren, Wiederherstellen) ausgeführt wird, kann dies zu einem Absturz von Visual Studio führen ([#4420](https://github.com/NuGet/Home/issues/4420))</span><span class="sxs-lookup"><span data-stu-id="81cff-185">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

- <span data-ttu-id="81cff-186">Benutzeroberfläche reagiert nicht: Deadlock beim Initialisieren von NuGet.SolutionRestoreManager.RestoreManagerPackage ([#4371](https://github.com/NuGet/Home/issues/4371))</span><span class="sxs-lookup"><span data-stu-id="81cff-186">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

- <span data-ttu-id="81cff-187">Der Befehl „add package“ sollte Versionen statt Elemente als Attribut hinzufügen ([#4325](https://github.com/NuGet/Home/issues/4325))</span><span class="sxs-lookup"><span data-stu-id="81cff-187">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

- <span data-ttu-id="81cff-188">dotnet</span><span class="sxs-lookup"><span data-stu-id="81cff-188">dotnet</span></span>
  - <span data-ttu-id="81cff-189">„dotnet Restore foo.sln“ schlägt fehl, wenn Konfigurationen in SLN dazu führen, dass Projekte im Wiederherstellungsdiagramm dupliziert werden (mit verschiedenen Konfigurationen) ([#4316](https://github.com/NuGet/Home/issues/4316))</span><span class="sxs-lookup"><span data-stu-id="81cff-189">dotnetcore Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

- <span data-ttu-id="81cff-190">Pakete, die nur Inhalte enthalten ([#3668](https://github.com/NuGet/Home/issues/3668))</span><span class="sxs-lookup"><span data-stu-id="81cff-190">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

- <span data-ttu-id="81cff-191">Die Option des Selektors für das Paketformat standardmäßig deaktivieren ([#4468](https://github.com/NuGet/Home/issues/4468))</span><span class="sxs-lookup"><span data-stu-id="81cff-191">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

- <span data-ttu-id="81cff-192">Leistung: Das Projekt „CreateUAP_CSharp_VS.01.1.Create“ wurde zurückgesetzt, „Duration_TotalElapsedTime“ liegt bei 3.153,570 ms (149,1%) – </span><span class="sxs-lookup"><span data-stu-id="81cff-192">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="81cff-193">Baseline 26129,02 ([#4452](https://github.com/NuGet/Home/issues/4452))</span><span class="sxs-lookup"><span data-stu-id="81cff-193">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

- <span data-ttu-id="81cff-194">Leistung: Die Projektmappe „ManagedLangs_CS_DDRIT.0300.Rebuild“ wurde zurückgesetzt, „Duration_TotalElapsedTime“ liegt bei 1,5 Sekunden – </span><span class="sxs-lookup"><span data-stu-id="81cff-194">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="81cff-195">Baseline 26105 ([#4441](https://github.com/NuGet/Home/issues/4441))</span><span class="sxs-lookup"><span data-stu-id="81cff-195">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

- <span data-ttu-id="81cff-196">Die Nominierung schlägt in Projekten mit mehreren TFMs fehl ([#4419](https://github.com/NuGet/Home/issues/4419))</span><span class="sxs-lookup"><span data-stu-id="81cff-196">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

- <span data-ttu-id="81cff-197">Leistung: Die Projektmappe „WebForms_DDRIT.1200.Close“ wurde zurückgesetzt, „VM_ImagesInMemory_Total_devenv“ liegt bei 3,000 (0,5%) – </span><span class="sxs-lookup"><span data-stu-id="81cff-197">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="81cff-198">Baseline 26123,04 ([#4408](https://github.com/NuGet/Home/issues/4408))</span><span class="sxs-lookup"><span data-stu-id="81cff-198">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

- <span data-ttu-id="81cff-199">vsfeedback: Warnungen beim Packen, wenn netcoreapp1.1 angezielt wird ([#4397](https://github.com/NuGet/Home/issues/4397))</span><span class="sxs-lookup"><span data-stu-id="81cff-199">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

- <span data-ttu-id="81cff-200">„PathTooLongException“ wird ausgelöst, wenn versucht wird, ein neues NuGet-Paket zu einer leeren ASP.NET Core-Webanwendung hinzuzufügen ([#4391](https://github.com/NuGet/Home/issues/4391))</span><span class="sxs-lookup"><span data-stu-id="81cff-200">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

- <span data-ttu-id="81cff-201">„Pack“ wird zu häufig ausgeführt (dotnet)</span><span class="sxs-lookup"><span data-stu-id="81cff-201">Pack runs too often -- dotnet</span></span>
  - <span data-ttu-id="81cff-202">„dotnetcore pack“ schlägt mit der Fehlermeldung „Im Zielabhängigkeitsdiagramm besteht eine Ringabhängigkeit im Zusammenhang mit Ziel ‚Pack‘.“ fehl ([#4381](https://github.com/NuGet/Home/issues/4381))</span><span class="sxs-lookup"><span data-stu-id="81cff-202">dotnetcore pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

- <span data-ttu-id="81cff-203">„Pack“ wird zu häufig ausgeführt: Beim Generieren von NuGet-Paketen sind nicht alle Konfigurationen enthalten ([#4380](https://github.com/NuGet/Home/issues/4380))</span><span class="sxs-lookup"><span data-stu-id="81cff-203">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

- <span data-ttu-id="81cff-204">„NullReferenceException“ wird beim Hinzufügen von NuGet mit „PackageRef“ in C++-Projekten ausgelöst ([#4378](https://github.com/NuGet/Home/issues/4378))</span><span class="sxs-lookup"><span data-stu-id="81cff-204">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

- <span data-ttu-id="81cff-205">Barrierefreiheit: Die Sprachausgabe gibt das Kontrollkästchen nicht aus, das für das Auswählen der Projekte verwendet wird, für die die Pakete installiert werden sollen ([#4366](https://github.com/NuGet/Home/issues/4366))</span><span class="sxs-lookup"><span data-stu-id="81cff-205">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

- <span data-ttu-id="81cff-206">Das Herstellen einer Verbindung von NuGet für Visual Studio 2017 mit VSO- und VSTS-Feeds schlägt fehl (Visual Studio-Fehler 365798) ([#4365](https://github.com/NuGet/Home/issues/4365))</span><span class="sxs-lookup"><span data-stu-id="81cff-206">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

- <span data-ttu-id="81cff-207">„contentFiles“ speichert die Ausgabe am falschen Ort, wenn „PackagePath“ den Pfad als „contentFiles“ angibt ([#4348](https://github.com/NuGet/Home/issues/4348))</span><span class="sxs-lookup"><span data-stu-id="81cff-207">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

- <span data-ttu-id="81cff-208">Beim Packen des Ziels wird die PackageVersion-Eigenschaft mit dem Versionssuffix angefügt ([#4324](https://github.com/NuGet/Home/issues/4324))</span><span class="sxs-lookup"><span data-stu-id="81cff-208">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

- <span data-ttu-id="81cff-209">Das Angeben des Paketpfads funktioniert mit „dotnet pack“ nicht ([#4321](https://github.com/NuGet/Home/issues/4321))</span><span class="sxs-lookup"><span data-stu-id="81cff-209">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

- <span data-ttu-id="81cff-210">NuGet gibt während der Wiederherstellung einige Warnungen zu doppelten Importen aus ([#4304](https://github.com/NuGet/Home/issues/4304))</span><span class="sxs-lookup"><span data-stu-id="81cff-210">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

- <span data-ttu-id="81cff-211">Das Dialogfeld für das Auswählen des Formats des NuGet-Paket-Managers sieht im dunklen Design nicht gut aus ([#4300](https://github.com/NuGet/Home/issues/4300))</span><span class="sxs-lookup"><span data-stu-id="81cff-211">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

- <span data-ttu-id="81cff-212">Visual Studio stürzt beim Wiederherstellen des Builds ab ([#4298](https://github.com/NuGet/Home/issues/4298))</span><span class="sxs-lookup"><span data-stu-id="81cff-212">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

- <span data-ttu-id="81cff-213">Bei Visual Studio tritt ein Deadlock auf, wenn Sie den TFM zu Zielframeworks hinzufügen und dann speichern und einen Build durchführen</span><span class="sxs-lookup"><span data-stu-id="81cff-213">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="81cff-214">(in 10% der Fälle) ([#4295](https://github.com/NuGet/Home/issues/4295))</span><span class="sxs-lookup"><span data-stu-id="81cff-214">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

- <span data-ttu-id="81cff-215">„nuget pack“ gibt keine Meldung beim erfolgreichen Packen eines Projekts aus ([#4294](https://github.com/NuGet/Home/issues/4294))</span><span class="sxs-lookup"><span data-stu-id="81cff-215">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

- <span data-ttu-id="81cff-216">„PackTask“ schlägt fehl, da System.IO.Compression 4.1 nicht gefunden werden konnte ([#4290](https://github.com/NuGet/Home/issues/4290))</span><span class="sxs-lookup"><span data-stu-id="81cff-216">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

- <span data-ttu-id="81cff-217">„Pack“ wird zu häufig ausgeführt: „PackTask“ schlägt regelmäßig wegen Konflikten beim Dateizugriff fehl ([#4289](https://github.com/NuGet/Home/issues/4289))</span><span class="sxs-lookup"><span data-stu-id="81cff-217">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

- <span data-ttu-id="81cff-218">NuGet öffnet das Ausgabefenster während der Wiederherstellung im Hintergrund ([#4274](https://github.com/NuGet/Home/issues/4274))</span><span class="sxs-lookup"><span data-stu-id="81cff-218">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

- <span data-ttu-id="81cff-219">Beseitigen von „ServiceProvider“ als riskantes Codierungsmuster (das zu Abstürzen führen kann) ([#4268](https://github.com/NuGet/Home/issues/4268))</span><span class="sxs-lookup"><span data-stu-id="81cff-219">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

- <span data-ttu-id="81cff-220">Leistung/Benutzeroberfläche reagiert nicht: Verbessern der Lesevorgänge von DownloadTimeoutStream ([#4266](https://github.com/NuGet/Home/issues/4266))</span><span class="sxs-lookup"><span data-stu-id="81cff-220">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

- <span data-ttu-id="81cff-221">Bei Visual Studio tritt ein Deadlock auf, wenn Sie versuchen, ein Projekt zu schließen, bevor die Wiederherstellung von NuGet abgeschlossen ist ([#4257](https://github.com/NuGet/Home/issues/4257))</span><span class="sxs-lookup"><span data-stu-id="81cff-221">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

- <span data-ttu-id="81cff-222">Probleme mit „PackTask“ und dem Packen von `.nuspec` ([#4250](https://github.com/NuGet/Home/issues/4250))</span><span class="sxs-lookup"><span data-stu-id="81cff-222">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

- <span data-ttu-id="81cff-223">[vsfeedback] NuGet-Pakete können für neue Projekte nicht aufgelöst werden (Visual Studio muss neu gestartet werden) ([#4217](https://github.com/NuGet/Home/issues/4217))</span><span class="sxs-lookup"><span data-stu-id="81cff-223">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

- <span data-ttu-id="81cff-224">[vsfeedback] Das Dropdownmenü „Version“, das die verfügbaren Paketversionen anzeigt, bleibt nicht synchron mit dem ausgewählten NuGet-Paket ([#4198](https://github.com/NuGet/Home/issues/4198))</span><span class="sxs-lookup"><span data-stu-id="81cff-224">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

- <span data-ttu-id="81cff-225">Nuget.Client sollte „JoinableTaskFactory“ bei der Interaktion mit CPS verwenden, um Deadlocks zu verhindern ([#4185](https://github.com/NuGet/Home/issues/4185))</span><span class="sxs-lookup"><span data-stu-id="81cff-225">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

- <span data-ttu-id="81cff-226">NuGet 3.5.0 entpackt `.targets` nicht aus dem Paket ([#4171](https://github.com/NuGet/Home/issues/4171))</span><span class="sxs-lookup"><span data-stu-id="81cff-226">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

- <span data-ttu-id="81cff-227">dotnet</span><span class="sxs-lookup"><span data-stu-id="81cff-227">dotnet</span></span>
  - <span data-ttu-id="81cff-228">„dotnetcore pack“ unterstützt in `.csproj` -  keine Titel ([#4150](https://github.com/NuGet/Home/issues/4150))</span><span class="sxs-lookup"><span data-stu-id="81cff-228">dotnetcore pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

- <span data-ttu-id="81cff-229">„Install-Package“ führt zu einer Fehlermeldung in Visual Studio 2017 RC ([#4127](https://github.com/NuGet/Home/issues/4127))</span><span class="sxs-lookup"><span data-stu-id="81cff-229">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

- <span data-ttu-id="81cff-230">Das Aktualisieren eines Pakets für .NET Core-Projekte scheint nicht zu funktionieren, da die Benutzeroberfläche das CPS-Update nicht erhält</span><span class="sxs-lookup"><span data-stu-id="81cff-230">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="81cff-231"> ([#4035](https://github.com/NuGet/Home/issues/4035))</span><span class="sxs-lookup"><span data-stu-id="81cff-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

- <span data-ttu-id="81cff-232">Verbesserung der Warnung für nicht aufgelöste Verweise ([#3955](https://github.com/NuGet/Home/issues/3955))</span><span class="sxs-lookup"><span data-stu-id="81cff-232">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

- <span data-ttu-id="81cff-233">dotnet</span><span class="sxs-lookup"><span data-stu-id="81cff-233">dotnet</span></span>
  - <span data-ttu-id="81cff-234">„dotnetcore pack“: „ProjectReference“ verliert die Versionsinformationen ([#3953](https://github.com/NuGet/Home/issues/3953))</span><span class="sxs-lookup"><span data-stu-id="81cff-234">dotnetcore pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

- <span data-ttu-id="81cff-235">Regression der insgesamt verstrichenen Zeit von „Erstellen einer UWP-App“, „Erstellen eines Projekts“ und „Neuerstellen“ ([#3873](https://github.com/NuGet/Home/issues/3873))</span><span class="sxs-lookup"><span data-stu-id="81cff-235">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

- <span data-ttu-id="81cff-236">Die Meldung für die erfolgreiche Wiederherstellung wird auch angezeigt, wenn während der Wiederherstellung ein Fehler auftritt</span><span class="sxs-lookup"><span data-stu-id="81cff-236">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="81cff-237"> ([#3799](https://github.com/NuGet/Home/issues/3799))</span><span class="sxs-lookup"><span data-stu-id="81cff-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

- <span data-ttu-id="81cff-238">Erneutes Veröffentlichen von Nuget.CommandLine 3.4.4 auf nuget.org ([#2931](https://github.com/NuGet/Home/issues/2931))</span><span class="sxs-lookup"><span data-stu-id="81cff-238">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

- <span data-ttu-id="81cff-239">Beim Migrieren ändert sich das Projekt von `project.json` in `.csproj` und die Wiederherstellung schlägt fehl ([#4297](https://github.com/NuGet/Home/issues/4297))</span><span class="sxs-lookup"><span data-stu-id="81cff-239">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

- <span data-ttu-id="81cff-240">Die Wiederherstellung des neu erstellten xUnit-Testprojekts schlägt fehl ([#4296](https://github.com/NuGet/Home/issues/4296))</span><span class="sxs-lookup"><span data-stu-id="81cff-240">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

- <span data-ttu-id="81cff-241">Core-Projekte reagieren möglicherweise nicht, die Benutzeroberfläche wird beim Öffnen gesperrt ([#4269](https://github.com/NuGet/Home/issues/4269))</span><span class="sxs-lookup"><span data-stu-id="81cff-241">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

- <span data-ttu-id="81cff-242">Fehlerbehebung bei der TARGETS-Datei für Buildaufgaben ([#4267](https://github.com/NuGet/Home/issues/4267))</span><span class="sxs-lookup"><span data-stu-id="81cff-242">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

- <span data-ttu-id="81cff-243">Die Fehlerliste enthält einen Fehler nach dem Erstellen der Projektmappe, der das Projekt entlädt, auf das verwiesen wird ([#4208](https://github.com/NuGet/Home/issues/4208))</span><span class="sxs-lookup"><span data-stu-id="81cff-243">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

- <span data-ttu-id="81cff-244">MSB4057: „Das Ziel ‚_GenerateRestoreGraphProjectEntry‘ ist im Projekt nicht vorhanden.“</span><span class="sxs-lookup"><span data-stu-id="81cff-244">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="81cff-245"> ([#4194](https://github.com/NuGet/Home/issues/4194))</span><span class="sxs-lookup"><span data-stu-id="81cff-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

- <span data-ttu-id="81cff-246">vsfeedback: Die Benutzeroberfläche des NuGet-Managers für Projektmappen stürzt ab, wenn alle Projekte ausgewählt werden ([#4191](https://github.com/NuGet/Home/issues/4191))</span><span class="sxs-lookup"><span data-stu-id="81cff-246">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

- <span data-ttu-id="81cff-247">„MSBuildPath“ von „nuget.exe“ schlägt fehl, wenn ein nachgestellter Schrägstrich vorhanden ist ([#4180](https://github.com/NuGet/Home/issues/4180))</span><span class="sxs-lookup"><span data-stu-id="81cff-247">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

- <span data-ttu-id="81cff-248">vsfeedback: Die Wiederherstellung von NuGet gibt für das LinqToTwitter-Projekt mehrere Warnungen für Projektverweise aus ([#4156](https://github.com/NuGet/Home/issues/4156))</span><span class="sxs-lookup"><span data-stu-id="81cff-248">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

- <span data-ttu-id="81cff-249">Beim Packen von `.csproj` aus wird das Attribut „minClientVersion“ nicht eingeschlossen ([#4135](https://github.com/NuGet/Home/issues/4135))</span><span class="sxs-lookup"><span data-stu-id="81cff-249">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

- <span data-ttu-id="81cff-250">„NuGet.Build.Tasks.Pack.dll“ wird in Visual Studio 2017 als verzögert signiert (d15rel 26014.00) ([#4122](https://github.com/NuGet/Home/issues/4122))</span><span class="sxs-lookup"><span data-stu-id="81cff-250">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

- <span data-ttu-id="81cff-251">VSFeedback: Wiederherstellung eines Visual Studio 2015-Projekts, das mit CMake 3.7.1 generiert wurde, schlägt fehl ([#4114](https://github.com/NuGet/Home/issues/4114))</span><span class="sxs-lookup"><span data-stu-id="81cff-251">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

- <span data-ttu-id="81cff-252">VSFeedback: Fehler bei der Wiederherstellung können die umfangreicheren Fehlermeldungen des Builds verdecken ([#4113](https://github.com/NuGet/Home/issues/4113))</span><span class="sxs-lookup"><span data-stu-id="81cff-252">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

- <span data-ttu-id="81cff-253">[VSFeedback] Fehler beim Wiederherstellen von NuGet-Paketen für das Websiteprojekt: „Der Wert darf nicht NULL sein.“</span><span class="sxs-lookup"><span data-stu-id="81cff-253">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="81cff-254"> ([#4092](https://github.com/NuGet/Home/issues/4092))</span><span class="sxs-lookup"><span data-stu-id="81cff-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

- <span data-ttu-id="81cff-255">Bei der Migration wird eine Ausnahme beim Objektverweis in „NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker“ ausgelöst ([#4067](https://github.com/NuGet/Home/issues/4067))</span><span class="sxs-lookup"><span data-stu-id="81cff-255">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

- <span data-ttu-id="81cff-256">dotnet</span><span class="sxs-lookup"><span data-stu-id="81cff-256">dotnet</span></span>
  - <span data-ttu-id="81cff-257">„dotnetcore pack“ sollte Tools mit den Versionen packen, für die das Paket erstellt wurde ([#4063](https://github.com/NuGet/Home/issues/4063))</span><span class="sxs-lookup"><span data-stu-id="81cff-257">dotnetcore pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

- <span data-ttu-id="81cff-258">Die neue Wiederherstellung im Hintergrund zeigt Millisekunden in der Statusleiste an, obwohl die Wiederherstellung mehrere Sekunden dauert ([#4036](https://github.com/NuGet/Home/issues/4036))</span><span class="sxs-lookup"><span data-stu-id="81cff-258">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

- <span data-ttu-id="81cff-259">Tippfehler bei „Fehler beim Auflösen aller Projektverweise...“ ([#4018](https://github.com/NuGet/Home/issues/4018))</span><span class="sxs-lookup"><span data-stu-id="81cff-259">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

- <span data-ttu-id="81cff-260">Aktivieren von PCM-Workflows in Szenarios mit Paketverweisen ([#4016](https://github.com/NuGet/Home/issues/4016))</span><span class="sxs-lookup"><span data-stu-id="81cff-260">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

- <span data-ttu-id="81cff-261">Die installierten Pakete können auf der Benutzeroberfläche des Paket-Managers nicht gefunden werden ([#4015](https://github.com/NuGet/Home/issues/4015))</span><span class="sxs-lookup"><span data-stu-id="81cff-261">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

- <span data-ttu-id="81cff-262">dotnet</span><span class="sxs-lookup"><span data-stu-id="81cff-262">dotnet</span></span>
  - <span data-ttu-id="81cff-263">„dotnetcore pack“ schlägt fehl, wenn „PackagePath“ leer ist ([#3993](https://github.com/NuGet/Home/issues/3993))</span><span class="sxs-lookup"><span data-stu-id="81cff-263">dotnetcore pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

- <span data-ttu-id="81cff-264">Die Wiederherstellungsaufgabe schlägt in Szenarios mit mehreren Benutzern fehl ([#3897](https://github.com/NuGet/Home/issues/3897))</span><span class="sxs-lookup"><span data-stu-id="81cff-264">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

- <span data-ttu-id="81cff-265">Der Inhaltstyp kann nicht geändert werden, wenn mithilfe der NuGet-Packaufgabe gepackt wird ([#3895](https://github.com/NuGet/Home/issues/3895))</span><span class="sxs-lookup"><span data-stu-id="81cff-265">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

- <span data-ttu-id="81cff-266">Die Standardkopien von „ContentFiles“ sind für „MsBuild /t:pack“ falsch ([#3894](https://github.com/NuGet/Home/issues/3894))</span><span class="sxs-lookup"><span data-stu-id="81cff-266">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

- <span data-ttu-id="81cff-267">Bei der Installation der Paketwiederherstellung wird die Meldung für das Wiederherstellen von Paketen doppelt protokolliert ([#3785](https://github.com/NuGet/Home/issues/3785))</span><span class="sxs-lookup"><span data-stu-id="81cff-267">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

- <span data-ttu-id="81cff-268">Entfernen der Sicherungen: Die Wiederherstellung des Abschnitts „Runtimes“ sollte nur für das aktuelle Projekt gelten ([#3768](https://github.com/NuGet/Home/issues/3768))</span><span class="sxs-lookup"><span data-stu-id="81cff-268">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

- <span data-ttu-id="81cff-269">Die Packaufgabe fügt Inhaltsdateien in „content/“ und „contentFiles/“ ein ([#3718](https://github.com/NuGet/Home/issues/3718))</span><span class="sxs-lookup"><span data-stu-id="81cff-269">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

- <span data-ttu-id="81cff-270">dotnet</span><span class="sxs-lookup"><span data-stu-id="81cff-270">dotnet</span></span>
  - <span data-ttu-id="81cff-271">„dotnetcore pack3“ teilt Tags zusätzlich ([#3701](https://github.com/NuGet/Home/issues/3701))</span><span class="sxs-lookup"><span data-stu-id="81cff-271">dotnetcore pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

- <span data-ttu-id="81cff-272">dotnet</span><span class="sxs-lookup"><span data-stu-id="81cff-272">dotnet</span></span>
  - <span data-ttu-id="81cff-273">„dotnetcore pack“: Beim Packen von Projekten mit Paketverweisen wird eine Warnung wegen doppelten Imports ausgegeben ([#3665](https://github.com/NuGet/Home/issues/3665))</span><span class="sxs-lookup"><span data-stu-id="81cff-273">dotnetcore pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

- <span data-ttu-id="81cff-274">Die Wiederherstellungsprotokollierung wird in Visual Studio nicht immer angezeigt ([#3633](https://github.com/NuGet/Home/issues/3633))</span><span class="sxs-lookup"><span data-stu-id="81cff-274">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

- <span data-ttu-id="81cff-275">Der lokale Hilfetexte in NuGet erwähnt weiterhin den Paketcache ([#3592](https://github.com/NuGet/Home/issues/3592))</span><span class="sxs-lookup"><span data-stu-id="81cff-275">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

- <span data-ttu-id="81cff-276">„Restore3“ koppelt „PackageReferences“ mit „TargetFrameworks“</span><span class="sxs-lookup"><span data-stu-id="81cff-276">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="81cff-277"> ([#3504](https://github.com/NuGet/Home/issues/3504))</span><span class="sxs-lookup"><span data-stu-id="81cff-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

- <span data-ttu-id="81cff-278">NuGet wählt in der Eingabeaufforderung von VS „15“ Developer (Vorschauversion 4)</span><span class="sxs-lookup"><span data-stu-id="81cff-278">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="81cff-279">eine unerwartete Version von MSBuild aus ([#3408](https://github.com/NuGet/Home/issues/3408))</span><span class="sxs-lookup"><span data-stu-id="81cff-279">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

- <span data-ttu-id="81cff-280">TARGETS- und PROPS-Dateien sollten auch bei einer fehlerhaften Wiederherstellung geschrieben werden ([#3399](https://github.com/NuGet/Home/issues/3399))</span><span class="sxs-lookup"><span data-stu-id="81cff-280">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

- <span data-ttu-id="81cff-281">NuGet berücksichtigt während der Wiederherstellung nicht die gleichen Kompatibilitätsshims wie MSBuild, wenn diese über die Visual Studio 2015-Eingabeaufforderung durchgeführt wird ([#3387](https://github.com/NuGet/Home/issues/3387))</span><span class="sxs-lookup"><span data-stu-id="81cff-281">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

- <span data-ttu-id="81cff-282">Reaktivieren von „PackFromProjectWithDevelopmentDependencySet“ für Visual Studio 2015 ([#3272](https://github.com/NuGet/Home/issues/3272))</span><span class="sxs-lookup"><span data-stu-id="81cff-282">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

- <span data-ttu-id="81cff-283">Probleme bei Blend mit NuGet ([#4043](https://github.com/NuGet/Home/issues/4043))</span><span class="sxs-lookup"><span data-stu-id="81cff-283">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

- <span data-ttu-id="81cff-284">Integrieren von 4.0.0.2067 in CLI- und SDK-Repositorys für die Bereitstellung mit RC2 ([#4029](https://github.com/NuGet/Home/issues/4029))</span><span class="sxs-lookup"><span data-stu-id="81cff-284">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

- <span data-ttu-id="81cff-285">Visual Studio reagiert nicht, wenn eine neue Core-Konsolen-App erstellt und eine Projektmappe geschlossen, geöffnet und dann wieder geschlossen wird ([#4008](https://github.com/NuGet/Home/issues/4008))</span><span class="sxs-lookup"><span data-stu-id="81cff-285">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

- <span data-ttu-id="81cff-286">Absturz beim Öffnen des Projekts mit „d15prerel.25916.01“ ([#3982](https://github.com/NuGet/Home/issues/3982))</span><span class="sxs-lookup"><span data-stu-id="81cff-286">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

- <span data-ttu-id="81cff-287">Fehler bei der doc/help-Meldung für lokale Variablen von dotnet bzw. „nuget.exe“ ([#3919](https://github.com/NuGet/Home/issues/3919))</span><span class="sxs-lookup"><span data-stu-id="81cff-287">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

- <span data-ttu-id="81cff-288">Überprüfen von „PackTask“ nach Problemen mit vorangestellten oder nachstehenden Leerräumen ([#3906](https://github.com/NuGet/Home/issues/3906))</span><span class="sxs-lookup"><span data-stu-id="81cff-288">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

- <span data-ttu-id="81cff-289">dotnet</span><span class="sxs-lookup"><span data-stu-id="81cff-289">dotnet</span></span>
  - <span data-ttu-id="81cff-290">„dotnetcore pack“ packt aus „obj“, nicht aus „bin“ ([#3880](https://github.com/NuGet/Home/issues/3880))</span><span class="sxs-lookup"><span data-stu-id="81cff-290">dotnetcore pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

- <span data-ttu-id="81cff-291">dotnet</span><span class="sxs-lookup"><span data-stu-id="81cff-291">dotnet</span></span>
  - <span data-ttu-id="81cff-292">„dotnetcore pack“ scheint die Version von „ProjectReference“ immer auf 1.0.0 festzulegen ([#3874](https://github.com/NuGet/Home/issues/3874))</span><span class="sxs-lookup"><span data-stu-id="81cff-292">dotnetcore pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

- <span data-ttu-id="81cff-293">dotnet</span><span class="sxs-lookup"><span data-stu-id="81cff-293">dotnet</span></span>
  - <span data-ttu-id="81cff-294">„dotnetcore pack“ schlägt trotz Projektverweisen und <TargetFramework> -  fehl ([#3865](https://github.com/NuGet/Home/issues/3865))</span><span class="sxs-lookup"><span data-stu-id="81cff-294">dotnetcore pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

- <span data-ttu-id="81cff-295">„LockRecursionException“ in „ProjectSystemCache.TryGetProjectNameByShortName“ ([#3861](https://github.com/NuGet/Home/issues/3861))</span><span class="sxs-lookup"><span data-stu-id="81cff-295">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

- <span data-ttu-id="81cff-296">Leerräume aus MSBuild-Eigenschaften entfernen ([#3819](https://github.com/NuGet/Home/issues/3819))</span><span class="sxs-lookup"><span data-stu-id="81cff-296">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

- <span data-ttu-id="81cff-297">Konsolidieren der beiden Projektereignisse, die beim Laden des Projekts ausgelöst werden ([#3759](https://github.com/NuGet/Home/issues/3759))</span><span class="sxs-lookup"><span data-stu-id="81cff-297">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

- <span data-ttu-id="81cff-298">Die P2P-Bibliotheken in der `project.assets.json`-Datei besitzen die falsche Version ([#3748](https://github.com/NuGet/Home/issues/3748))</span><span class="sxs-lookup"><span data-stu-id="81cff-298">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

- <span data-ttu-id="81cff-299">Die Wiederherstellung stürzt aufgrund eines nicht reagierenden Feeds und eines nicht verfügbaren Pakets ab ([#3672](https://github.com/NuGet/Home/issues/3672))</span><span class="sxs-lookup"><span data-stu-id="81cff-299">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

- <span data-ttu-id="81cff-300">„nuget.exe“ reagiert bei einer großen Menge von Fehlerausgaben von MSBuild möglicherweise nicht ([#3572](https://github.com/NuGet/Home/issues/3572))</span><span class="sxs-lookup"><span data-stu-id="81cff-300">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

- <span data-ttu-id="81cff-301">Die Wiederherstellung während des Builds schlägt für Blend beim ersten Mal fehl, ist beim zweiten Mal jedoch erfolgreich (behobenes Visual Studio-Szenario) ([#2121](https://github.com/NuGet/Home/issues/2121))</span><span class="sxs-lookup"><span data-stu-id="81cff-301">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

### <a name="dcrs"></a><span data-ttu-id="81cff-302">DCRs</span><span class="sxs-lookup"><span data-stu-id="81cff-302">DCRs</span></span>

- <span data-ttu-id="81cff-303">Migrieren von V2 VSIX zu V3 VSIX ([#4196](https://github.com/NuGet/Home/issues/4196))</span><span class="sxs-lookup"><span data-stu-id="81cff-303">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

- <span data-ttu-id="81cff-304">NuGet sollte über einen Mechanismus verfügen, um den Pfad für die Sperrdatei in MSBuild abzurufen ([#3351](https://github.com/NuGet/Home/issues/3351))</span><span class="sxs-lookup"><span data-stu-id="81cff-304">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

- <span data-ttu-id="81cff-305">Hinzufügen von Buildobjekten zu der Kompatibilitätsprüfung und der Objektdatei des TFM ([#3296](https://github.com/NuGet/Home/issues/3296))</span><span class="sxs-lookup"><span data-stu-id="81cff-305">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

- <span data-ttu-id="81cff-306">Definieren einer neuen „ProjectCapability“ namens „Pack“ in den Packzielen zum Aktivieren von Paketfunktionen ([#4146](https://github.com/NuGet/Home/issues/4146))</span><span class="sxs-lookup"><span data-stu-id="81cff-306">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

- <span data-ttu-id="81cff-307">Ausführen von Packzielen als Postbuildziel bedingt durch die MSBuild-Eigenschaft „GeneratePackageOnBuild“ ([#4145](https://github.com/NuGet/Home/issues/4145))</span><span class="sxs-lookup"><span data-stu-id="81cff-307">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

- <span data-ttu-id="81cff-308">Verwenden der NuGet-Eigenschaft „RestoreProjectStyle“ zum Erstellen eines spezifischen NuGet-Projekts ([#4134](https://github.com/NuGet/Home/issues/4134))</span><span class="sxs-lookup"><span data-stu-id="81cff-308">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

- <span data-ttu-id="81cff-309">Anpassen der Wiederherstellung für geänderte transitive Projektverweise ([#4076](https://github.com/NuGet/Home/issues/4076))</span><span class="sxs-lookup"><span data-stu-id="81cff-309">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

- <span data-ttu-id="81cff-310">Hinzufügen von NuGet-Eigenschaften zur Zieldatei für Nicht-UWP-Projekte ([#4030](https://github.com/NuGet/Home/issues/4030))</span><span class="sxs-lookup"><span data-stu-id="81cff-310">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

- <span data-ttu-id="81cff-311">UWP-Unterstützung für „TargetPlatformVersion“ ([#3923](https://github.com/NuGet/Home/issues/3923))</span><span class="sxs-lookup"><span data-stu-id="81cff-311">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

- <span data-ttu-id="81cff-312">Übermitteln der Projektverweismetadaten an das NuGet-Projektsystem ([#3922](https://github.com/NuGet/Home/issues/3922))</span><span class="sxs-lookup"><span data-stu-id="81cff-312">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

- <span data-ttu-id="81cff-313">Hinzufügen der Benutzeroberfläche für den Packmodus ([#3921](https://github.com/NuGet/Home/issues/3921))</span><span class="sxs-lookup"><span data-stu-id="81cff-313">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

- <span data-ttu-id="81cff-314">Für die veraltete `.csproj`-Datei müssen „NugetTargetMoniker“ und „RuntimeIdentifiers“ im Projekt und in den Zielen festgelegt sein ([#3854](https://github.com/NuGet/Home/issues/3854))</span><span class="sxs-lookup"><span data-stu-id="81cff-314">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

- <span data-ttu-id="81cff-315">Das Installieren des Pakets überschneidet sich möglicherweise mit der automatischen Wiederherstellung ([#3836](https://github.com/NuGet/Home/issues/3836))</span><span class="sxs-lookup"><span data-stu-id="81cff-315">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

- <span data-ttu-id="81cff-316">Das Kontextmenü „QueryStatus“ wird nicht angezeigt, wenn „VSPackage“ nicht geladen wird ([#3835](https://github.com/NuGet/Home/issues/3835))</span><span class="sxs-lookup"><span data-stu-id="81cff-316">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

- <span data-ttu-id="81cff-317">Beim Wiederherstellen von Projektmappen und Builds werden weiterhin Dialogfelder angezeigt ([#3789](https://github.com/NuGet/Home/issues/3789))</span><span class="sxs-lookup"><span data-stu-id="81cff-317">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

- <span data-ttu-id="81cff-318">Isolieren der VSSDK-Version während des Projektmappenbuilds von „NuGet.Clients“ ([#3890](https://github.com/NuGet/Home/issues/3890))</span><span class="sxs-lookup"><span data-stu-id="81cff-318">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="81cff-319">Links zu GitHub-Problemen, die in RTM behoben wurden:</span><span class="sxs-lookup"><span data-stu-id="81cff-319">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="81cff-320">Probleme: Liste 1</span><span class="sxs-lookup"><span data-stu-id="81cff-320">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[<span data-ttu-id="81cff-321">Probleme: Liste 2</span><span class="sxs-lookup"><span data-stu-id="81cff-321">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[<span data-ttu-id="81cff-322">Probleme: Liste 3</span><span class="sxs-lookup"><span data-stu-id="81cff-322">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[<span data-ttu-id="81cff-323">Probleme: Liste 4</span><span class="sxs-lookup"><span data-stu-id="81cff-323">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[<span data-ttu-id="81cff-324">Probleme: Liste 5</span><span class="sxs-lookup"><span data-stu-id="81cff-324">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
