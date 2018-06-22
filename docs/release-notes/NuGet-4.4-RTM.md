---
title: Anmerkungen zu Version 4.4 RTM von NuGet
description: Anmerkungen zu Version 4.3 RTM von NuGet, einschließlich bekannter Fehler, Fehlerkorrekturen, hinzugefügter Funktionen und DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3e969274e69de03ca9851d31a627919dcc46bb7d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821667"
---
# <a name="nuget-44-rtm-release-notes"></a><span data-ttu-id="0c78d-103">Anmerkungen zu Version 4.4 RTM von NuGet</span><span class="sxs-lookup"><span data-stu-id="0c78d-103">NuGet 4.4 RTM Release Notes</span></span>

<span data-ttu-id="0c78d-104">NuGet 4.4 RTM ist im Lieferumfang von [Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) enthalten.</span><span class="sxs-lookup"><span data-stu-id="0c78d-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="known-issues"></a><span data-ttu-id="0c78d-105">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="0c78d-105">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="0c78d-106">Probleme mit .NET Standard 2.0 mit .NET Framework und NuGet</span><span class="sxs-lookup"><span data-stu-id="0c78d-106">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="0c78d-107">.NET Standard und die dazugehörigen Tools wurden so konzipiert, dass Projekte, die für .NET Framework 4.6.1 erstellt wurden, NuGet-Pakete und -Projekte verarbeiten können, die für .NET Standard 2.0 oder früher erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="0c78d-107">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="0c78d-108">In [diesem Dokument](https://github.com/dotnet/standard/issues/481) werden die Probleme, die in diesem Szenario auftreten können, der Plan für die Behebung dieser Probleme und Problemumgehungen zusammengefasst, die Sie nach aktuellem Stand für die Tools bereitstellen können.</span><span class="sxs-lookup"><span data-stu-id="0c78d-108">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="0c78d-109">Beim Verwenden der Paket-Manager-Konsole funktioniert die EINGABETASTE ggf. nicht</span><span class="sxs-lookup"><span data-stu-id="0c78d-109">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="0c78d-110">Problem</span><span class="sxs-lookup"><span data-stu-id="0c78d-110">Issue</span></span>

<span data-ttu-id="0c78d-111">Gelegentlich kann es vorkommen, dass die EINGABETASTE in der Paket-Manager-Konsole nicht funktioniert.</span><span class="sxs-lookup"><span data-stu-id="0c78d-111">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="0c78d-112">Wenn dieses Problem auftritt, überprüfen Sie den Fortschritt für diese Korrektur und stellen Sie zusätzliche hilfreiche Informationen zu den Reproduktionsschritten bereit.</span><span class="sxs-lookup"><span data-stu-id="0c78d-112">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="0c78d-113">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="0c78d-113">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="0c78d-114">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="0c78d-114">Workaround</span></span>

<span data-ttu-id="0c78d-115">Starten Sie Visual Studio neu und öffnen Sie die Paketverwaltungskonsole, bevor Sie die Projektmappe öffnen.</span><span class="sxs-lookup"><span data-stu-id="0c78d-115">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="0c78d-116">Alternativ können Sie versuchen, die Datei `project.lock.json` zu löschen und dann erneut wiederherzustellen.</span><span class="sxs-lookup"><span data-stu-id="0c78d-116">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="0c78d-117">Sie können DotNetCLITools nicht mit dem NuGet-Paket-Manager anzeigen, hinzufügen oder aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="0c78d-117">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="0c78d-118">Problem</span><span class="sxs-lookup"><span data-stu-id="0c78d-118">Issue</span></span>

<span data-ttu-id="0c78d-119">Der NuGet-Paket-Manager zeigt die DotNetCLITools nicht an und ermöglicht auch kein Hinzufügen/Aktualisieren dieser Tools.</span><span class="sxs-lookup"><span data-stu-id="0c78d-119">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="0c78d-120">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="0c78d-120">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="0c78d-121">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="0c78d-121">Workaround</span></span>

<span data-ttu-id="0c78d-122">DotNetCLIToolReferences muss in der Projektdatei manuell bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="0c78d-122">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="0c78d-123">Die Neuzuweisung der Framework-Zielversion kann zu unvollständigen IntelliSense-Funktionen führen</span><span class="sxs-lookup"><span data-stu-id="0c78d-123">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="0c78d-124">Problem</span><span class="sxs-lookup"><span data-stu-id="0c78d-124">Issue</span></span>

<span data-ttu-id="0c78d-125">Die Neuzuweisung der Framework-Zielversion kann zu unvollständigen IntelliSense-Funktionen in Visual Studio führen.</span><span class="sxs-lookup"><span data-stu-id="0c78d-125">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="0c78d-126">Dies geschieht, wenn Sie PackageReferences als Paket-Manager-Format verwenden.</span><span class="sxs-lookup"><span data-stu-id="0c78d-126">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="0c78d-127">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="0c78d-127">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="0c78d-128">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="0c78d-128">Workaround</span></span>

<span data-ttu-id="0c78d-129">Führen Sie eine manuelle Wiederherstellung aus.</span><span class="sxs-lookup"><span data-stu-id="0c78d-129">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="0c78d-130">Ein Paket in einem .NET Core-Projekt, das eine Assembly mit einer ungültigen Signatur enthält, kann eine unendliche Wiederherstellungsschleife auslösen</span><span class="sxs-lookup"><span data-stu-id="0c78d-130">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="0c78d-131">Problem</span><span class="sxs-lookup"><span data-stu-id="0c78d-131">Issue</span></span>

<span data-ttu-id="0c78d-132">Bei der Verwendung eines Pakets mit einer Assembly, die eine ungültige Signatur enthält, oder beim Festlegen der Paketversion mit dem DateTime-Ticker tritt gelegentlich bei der automatischen Paketwiederherstellung eine Endlosschleife auf (dotnet/project-system#1457).</span><span class="sxs-lookup"><span data-stu-id="0c78d-132">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="0c78d-133">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="0c78d-133">Workaround</span></span>

<span data-ttu-id="0c78d-134">Zurzeit gibt es keine Problemumgehung.</span><span class="sxs-lookup"><span data-stu-id="0c78d-134">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="0c78d-135">Behobene Probleme mit dem NuGet 4.4 RTM-Zeitrahmen</span><span class="sxs-lookup"><span data-stu-id="0c78d-135">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="0c78d-136">In den [Anmerkungen zu der Version 4.3 RTM von NuGet](../release-notes/nuget-4.3-RTM.md) werden alle für NuGet 4.3 RTM behobenen Probleme aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="0c78d-136">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="0c78d-137">Features</span><span class="sxs-lookup"><span data-stu-id="0c78d-137">Features</span></span>

- <span data-ttu-id="0c78d-138">Unterstützung des Lightweight-Ladevorgangs für Projektmappen in PMC und von Benutzeroberflächenszenarios für NuGet PM ([#5180](https://github.com/NuGet/Home/issues/5180))</span><span class="sxs-lookup"><span data-stu-id="0c78d-138">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="0c78d-139">Das MSBuild-Packziel sollte über einen öffentlichen Hook verfügen, der Benutzerziele ausführt, bevor er selbst ausgeführt wird ([#5143](https://github.com/NuGet/Home/issues/5143))</span><span class="sxs-lookup"><span data-stu-id="0c78d-139">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="0c78d-140">Feature: Hinzufügen des dependencyVersion-Schalters zu NuGet-Installationen ([#1806](https://github.com/NuGet/Home/issues/1806))</span><span class="sxs-lookup"><span data-stu-id="0c78d-140">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="0c78d-141">uap10.0.TODO.0 sollte .NET Standard 2.0 für NuGet zugeordnet sein ([#5684](https://github.com/NuGet/Home/issues/5684))</span><span class="sxs-lookup"><span data-stu-id="0c78d-141">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="0c78d-142">Unterstützung der Visual Studio Build Tools-SKU mit MSBuild /t:restore ([#5562](https://github.com/NuGet/Home/issues/5562))</span><span class="sxs-lookup"><span data-stu-id="0c78d-142">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="0c78d-143">Bei der Wiederherstellung wird ein Fehler generiert, wenn die .NET 4.6.1-Unterstützung für .NET Standard 2.0 zwar erforderlich, aber noch nicht installiert ist ([#5325](https://github.com/NuGet/Home/issues/5325)).</span><span class="sxs-lookup"><span data-stu-id="0c78d-143">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="0c78d-144">Präfix für die Paket-ID der Benutzeroberfläche des Reservierungsclients ([#5572](https://github.com/NuGet/Home/issues/5572))</span><span class="sxs-lookup"><span data-stu-id="0c78d-144">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="0c78d-145">Übermitteln von lokalisierten NuGet-Komponenten zur Unterstützung der „dotnet.exe“-Lokalisierung ([#4336](https://github.com/NuGet/Home/issues/4336))</span><span class="sxs-lookup"><span data-stu-id="0c78d-145">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="0c78d-146">Fehler</span><span class="sxs-lookup"><span data-stu-id="0c78d-146">Bugs</span></span>

- <span data-ttu-id="0c78d-147">Unterschiedliche Schreibweisen des Projektpfads können dazu führen, dass bei der Wiederherstellung Paketverweise verloren gehen ([#5855](https://github.com/NuGet/Home/issues/5855)).</span><span class="sxs-lookup"><span data-stu-id="0c78d-147">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="0c78d-148">Verschieben von Fehlercodes mit Warnnummern in den Fehlerbereich ([#5824](https://github.com/NuGet/Home/issues/5824))</span><span class="sxs-lookup"><span data-stu-id="0c78d-148">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="0c78d-149">Irreführender Fehler, wenn bekannt ist, dass die .NET Standard-Version nicht mit dem Zielframework kompatibel ist ([#5818](https://github.com/NuGet/Home/issues/5818))</span><span class="sxs-lookup"><span data-stu-id="0c78d-149">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="0c78d-150">Testdateien mit verwirrenden Lizenzen ([#5776](https://github.com/NuGet/Home/issues/5776))</span><span class="sxs-lookup"><span data-stu-id="0c78d-150">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="0c78d-151">Fehlende Lizenzheader in End-to-End-Testvorlagen ([#5774](https://github.com/NuGet/Home/issues/5774))</span><span class="sxs-lookup"><span data-stu-id="0c78d-151">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="0c78d-152">Bei der Wiederherstellung von „packages.config“-Dateien werden Fehlermeldungen als NU1000 angezeigt ([#5743](https://github.com/NuGet/Home/issues/5743))</span><span class="sxs-lookup"><span data-stu-id="0c78d-152">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="0c78d-153">Die Installation der Datei „nuget.exe“ sollte die Funktion „DisableParallelProcessing“ auf Mono umfassen ([#5741](https://github.com/NuGet/Home/issues/5741))</span><span class="sxs-lookup"><span data-stu-id="0c78d-153">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="0c78d-154">Aufgrund einer nicht ordnungsgemäß durchgeführten Installation der Datei „nuget.exe“ wird das Zwischenspeichern deaktiviert ([#5737](https://github.com/NuGet/Home/issues/5737))</span><span class="sxs-lookup"><span data-stu-id="0c78d-154">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="0c78d-155">Visual Studio: Wenn der Befehl „restore“ für „packages.config“ ausgeführt wird, wird eine fehlerhafte Meldung angezeigt, wenn die Wiederherstellung aktiviert ist ([#5718](https://github.com/NuGet/Home/issues/5718))</span><span class="sxs-lookup"><span data-stu-id="0c78d-155">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="0c78d-156">Visual Studio: Wenn der Befehl „restore“ ausgeführt wird, wird eine verwirrende Meldung angezeigt, wenn die Wiederherstellung aktiviert ist ([#5659](https://github.com/NuGet/Home/issues/5659))</span><span class="sxs-lookup"><span data-stu-id="0c78d-156">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="0c78d-157">Die Aufgabe „GetRestoreDotnetCliTools“ löst einen Fehler aus, wenn Versionsmetadaten fehlen ([#5716](https://github.com/NuGet/Home/issues/5716))</span><span class="sxs-lookup"><span data-stu-id="0c78d-157">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="0c78d-158">dotnet</span><span class="sxs-lookup"><span data-stu-id="0c78d-158">dotnet</span></span>
  - <span data-ttu-id="0c78d-159">Der Paketbefehl „dotnetcore add“ kann leere Zeilen aus einer CSPROJ-Datei entfernen ([Nr. 5697](https://github.com/NuGet/Home/issues/5697))</span><span class="sxs-lookup"><span data-stu-id="0c78d-159">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="0c78d-160">Bei Quellnamen von Anmeldeinformationseinstellungen in der Datei „NuGet.Config“ wird die Groß- und Kleinschreibung berücksichtigt ([#5695](https://github.com/NuGet/Home/issues/5695))</span><span class="sxs-lookup"><span data-stu-id="0c78d-160">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="0c78d-161">Die Funktion „GeneratePackageOnBuild“ wurde aktiviert, und dadurch wurde der gesamte Paketverlauf gelöscht ([#5676](https://github.com/NuGet/Home/issues/5676))</span><span class="sxs-lookup"><span data-stu-id="0c78d-161">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="0c78d-162">Bei der Wiederherstellung werden alle Pakete bis auf „mono.cecil“- oder SemVer-Pakete wiederhergestellt.</span><span class="sxs-lookup"><span data-stu-id="0c78d-162">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="0c78d-163">([#5649](https://github.com/NuGet/Home/issues/5649))</span><span class="sxs-lookup"><span data-stu-id="0c78d-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="0c78d-164">Fehler und Warnungen: ungültiger Fehler, wenn eine Quelle nicht verfügbar ist</span><span class="sxs-lookup"><span data-stu-id="0c78d-164">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="0c78d-165">([#5644](https://github.com/NuGet/Home/issues/5644))</span><span class="sxs-lookup"><span data-stu-id="0c78d-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="0c78d-166">[DesignConsistency] Der Statustext für die NuGet-Installation wird in dunklen Designs nicht korrekt dargestellt.</span><span class="sxs-lookup"><span data-stu-id="0c78d-166">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="0c78d-167">([#5642](https://github.com/NuGet/Home/issues/5642))</span><span class="sxs-lookup"><span data-stu-id="0c78d-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="0c78d-168">Updates werden in der Projektmappe für alle Projekte installiert ([#5508](https://github.com/NuGet/Home/issues/5508))</span><span class="sxs-lookup"><span data-stu-id="0c78d-168">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="0c78d-169">dotnet</span><span class="sxs-lookup"><span data-stu-id="0c78d-169">dotnet</span></span>
  - <span data-ttu-id="0c78d-170">„dotnetcore pack“ verhält sich unterschiedlich je nachdem, ob „TargetFramework“ oder „TargetFrameworks“ verwendet wird ([Nr. 5281](https://github.com/NuGet/Home/issues/5281))</span><span class="sxs-lookup"><span data-stu-id="0c78d-170">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="0c78d-171">In Toolordner eingefügte DLLs geben Warnungen aus ([#5020](https://github.com/NuGet/Home/issues/5020))</span><span class="sxs-lookup"><span data-stu-id="0c78d-171">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="0c78d-172">„NuGet.ContentModel“ nutzt zu viel Speicherplatz für Zeichenfolgenvorgänge ([#4714](https://github.com/NuGet/Home/issues/4714))</span><span class="sxs-lookup"><span data-stu-id="0c78d-172">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="0c78d-173">„RuntimeEnvironmentHelper.IsLinux“ gibt TRUE für OSX zurück ([#4648](https://github.com/NuGet/Home/issues/4648))</span><span class="sxs-lookup"><span data-stu-id="0c78d-173">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="0c78d-174">„dotnet pack“ verschiebt die NUSPEC-Datei in den Ordner „obj“ anstelle von „obj\Debug“ ([#4644](https://github.com/NuGet/Home/issues/4644))</span><span class="sxs-lookup"><span data-stu-id="0c78d-174">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="0c78d-175">Ungewöhnlich langsames Paketupgrade für NuGet ([#4534](https://github.com/NuGet/Home/issues/4534))</span><span class="sxs-lookup"><span data-stu-id="0c78d-175">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="0c78d-176">Asynchrone CPs bei der Wiederherstellung von größeren Projektmappen, in denen die Option „Lightweight-Wiederherstellung von Projektmappen“ deaktiviert ist ([#4307](https://github.com/NuGet/Home/issues/4307))</span><span class="sxs-lookup"><span data-stu-id="0c78d-176">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="0c78d-177">SemVer 2.0: „nuget pack“ mit bereitgestellter Version ignoriert Metadaten (3.5.0-rtm-1938) ([#3643](https://github.com/NuGet/Home/issues/3643))</span><span class="sxs-lookup"><span data-stu-id="0c78d-177">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="0c78d-178">Das Installationspaket „Nuget.exe“ (3.0 und höher) mit der Versionsnummer und der Kennzeichnung „ExcludeVersion“ aktualisiert das Paket nicht auf eine neuere Version ([#2405](https://github.com/NuGet/Home/issues/2405))</span><span class="sxs-lookup"><span data-stu-id="0c78d-178">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="0c78d-179">Bei der Wiederherstellung von „Project.json“ sollte eine Warnung ausgelöst werden, wenn Pakete auf oberster Ebene Einschränkungen missachten ([#2358](https://github.com/NuGet/Home/issues/2358))</span><span class="sxs-lookup"><span data-stu-id="0c78d-179">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="0c78d-180">Die Konfigurationsdatei legt für die benutzerdefinierte Konfiguration nicht den Befehl „install“ fest ([#1646](https://github.com/NuGet/Home/issues/1646))</span><span class="sxs-lookup"><span data-stu-id="0c78d-180">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="0c78d-181">Bei der Installation der Datei „Nuget.exe“ wird der DisableParallelProcessing-Schalter nicht berücksichtigt ([#1556](https://github.com/NuGet/Home/issues/1556))</span><span class="sxs-lookup"><span data-stu-id="0c78d-181">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="0c78d-182">Quellen, die immer noch von „DotNet.exe“ oder „Msbuild.exe“ verwendet werden, werden deaktiviert ([#5704](https://github.com/NuGet/Home/issues/5704))</span><span class="sxs-lookup"><span data-stu-id="0c78d-182">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="0c78d-183">Fehler beim LSL-Szenario behoben ([#5685](https://github.com/NuGet/Home/issues/5685))</span><span class="sxs-lookup"><span data-stu-id="0c78d-183">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="0c78d-184">DCRs</span><span class="sxs-lookup"><span data-stu-id="0c78d-184">DCRs</span></span>

- <span data-ttu-id="0c78d-185">Unterstützung für „nuget.exe install TargetFramework“ ([#5736](https://github.com/NuGet/Home/issues/5736))</span><span class="sxs-lookup"><span data-stu-id="0c78d-185">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="0c78d-186">Hinzufügen von verschiedenen UserAgent-Zeichenfolgen für „MSBuild Task“ (.Net Core MSBuild vs. Desktop MSBuild) ([#5709](https://github.com/NuGet/Home/issues/5709))</span><span class="sxs-lookup"><span data-stu-id="0c78d-186">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="0c78d-187">„PackagePathResolver.GetPackageDirectoryName“ sollte virtuell sein ([#5700](https://github.com/NuGet/Home/issues/5700))</span><span class="sxs-lookup"><span data-stu-id="0c78d-187">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="0c78d-188">[DesignConsistency] Beim Hinzufügen eines NuGet-Pakets wird eine verwirrende Meldung angezeigt ([#5641](https://github.com/NuGet/Home/issues/5641))</span><span class="sxs-lookup"><span data-stu-id="0c78d-188">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="0c78d-189">[Warnungen und Fehler] „Nowarn“ fließt nicht auf transitive Weise durch P2P-Verweise ([#5501](https://github.com/NuGet/Home/issues/5501))</span><span class="sxs-lookup"><span data-stu-id="0c78d-189">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="0c78d-190">Lightweight-Ladevorgang für Projektmappen: Gemeinsamer Kern für die PM-Benutzeroberfläche, PMC und IVs ([#5057](https://github.com/NuGet/Home/issues/5057))</span><span class="sxs-lookup"><span data-stu-id="0c78d-190">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="0c78d-191">Lightweight-Ladevorgang für Projektmappen: PMC-Unterstützung ([#5053](https://github.com/NuGet/Home/issues/5053))</span><span class="sxs-lookup"><span data-stu-id="0c78d-191">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="0c78d-192">Hinzufügen der Unterstützung von MSBuild-Zielen vor der Wiederherstellung, die von Visual Studio ausgelöst werden ([#4781](https://github.com/NuGet/Home/issues/4781))</span><span class="sxs-lookup"><span data-stu-id="0c78d-192">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="0c78d-193">Hinzufügen eines öffentlichen Ziels zu „NuGet.targets“, auf das mithilfe von BeforeTargets verwiesen werden kann ([#4634](https://github.com/NuGet/Home/issues/4634))</span><span class="sxs-lookup"><span data-stu-id="0c78d-193">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="0c78d-194">Das Paketziel kann keine einwandfreien Inhaltsdateien mit Buildaktionen erstellen ([#4166](https://github.com/NuGet/Home/issues/4166))</span><span class="sxs-lookup"><span data-stu-id="0c78d-194">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="0c78d-195">„RestoreOperationLogger.Do“ blockiert Threadpoolthreads ([#5663](https://github.com/NuGet/Home/issues/5663))</span><span class="sxs-lookup"><span data-stu-id="0c78d-195">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="0c78d-196">Docs</span><span class="sxs-lookup"><span data-stu-id="0c78d-196">Docs</span></span>

- <span data-ttu-id="0c78d-197">Dokumentation zu den Optionen „DependencyVersion“ und „Framework“ des Befehls „install“ ([#5858](https://github.com/NuGet/Home/issues/5858))</span><span class="sxs-lookup"><span data-stu-id="0c78d-197">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="0c78d-198">Aktualisierung der Dokumentation zu NuGet-Warnungen und -Fehlern ([#5857](https://github.com/NuGet/Home/issues/5857))</span><span class="sxs-lookup"><span data-stu-id="0c78d-198">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="0c78d-199">Links zu GitHub-Problemen die in 4.4 RTM behoben wurden</span><span class="sxs-lookup"><span data-stu-id="0c78d-199">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="0c78d-200">Probleme: Liste 1</span><span class="sxs-lookup"><span data-stu-id="0c78d-200">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="0c78d-201">Probleme: Liste 2</span><span class="sxs-lookup"><span data-stu-id="0c78d-201">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="0c78d-202">Probleme: Liste 3</span><span class="sxs-lookup"><span data-stu-id="0c78d-202">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
