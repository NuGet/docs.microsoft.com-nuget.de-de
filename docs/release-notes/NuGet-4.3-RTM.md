---
title: Anmerkungen zu Version 4.3 RTM von NuGet
description: Anmerkungen zu Version 4.3 RTM von NuGet, einschließlich bekannter Fehler, Fehlerkorrekturen, hinzugefügter Funktionen und DCRs.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 72d707cb9bacd8abbac873ee10b2fd00f233d3cc
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432477"
---
# <a name="nuget-43-release-notes"></a><span data-ttu-id="b7ea4-103">Versionshinweise zu NuGet 4.3</span><span class="sxs-lookup"><span data-stu-id="b7ea4-103">NuGet 4.3 Release Notes</span></span>

<span data-ttu-id="b7ea4-104">NuGet 4.3 RTM ist im Lieferumfang von [Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) enthalten, fügt die Unterstützung von neuen Szenarios wie .NET Standard 2.0 und .NET Core 2.0 hinzu, enthält viele wichtige Fehlerbehebungen und verbessert die Leistung.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="b7ea4-105">In diesem Release sind außerdem einige Verbesserungen enthalten, wie u.a. die Unterstützung von Version 2.0.0 der semantischen Versionierung und die MSBuild-Integration von NuGet-Warnungen und -Fehlern.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-105">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="summary-whats-new-in-430"></a><span data-ttu-id="b7ea4-106">Zusammenfassung: Neuerungen in Version 4.3.0</span><span class="sxs-lookup"><span data-stu-id="b7ea4-106">Summary: What's New in 4.3.0</span></span>

## <a name="summary-whats-new-in-431"></a><span data-ttu-id="b7ea4-107">Zusammenfassung: Neuerungen in Version 4.3.1</span><span class="sxs-lookup"><span data-stu-id="b7ea4-107">Summary: What's New in 4.3.1</span></span>

* <span data-ttu-id="b7ea4-108">Sicherheitsfix: Die Berechtigungen für Dateien, die in ~/.nuget erstellt werden, sind nicht restriktiv genug ([#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)).</span><span class="sxs-lookup"><span data-stu-id="b7ea4-108">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>
* <span data-ttu-id="b7ea4-109">Sicherheitsfix: Dateien innerhalb von NUPKGs können einen relativen Pfad über dem NUPKG-Verzeichnis besitzen ([#7906](https://github.com/NuGet/Home/issues/7906)).</span><span class="sxs-lookup"><span data-stu-id="b7ea4-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="b7ea4-110">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="b7ea4-110">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="b7ea4-111">Die NuGet-Wiederherstellung behandelt deaktivierte Paketquellen in einigen Fällen so, als wären sie aktiviert</span><span class="sxs-lookup"><span data-stu-id="b7ea4-111">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="b7ea4-112">Problem</span><span class="sxs-lookup"><span data-stu-id="b7ea4-112">Issue</span></span>

<span data-ttu-id="b7ea4-113">Mit den folgenden Wiederherstellungsbefehlszeilen werden deaktivierte Paketquellen so behandelt, als wären sie aktiviert.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-113">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="b7ea4-114">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="b7ea4-114">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="b7ea4-115">`dotnet restore` (muss entweder mit dem in Visual Studio mitgelieferten Programm „dotnet.exe“ oder dem gleichnamigen Programm aus dem NetCore SDK 2.0.0 verwendet werden)</span><span class="sxs-lookup"><span data-stu-id="b7ea4-115">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="b7ea4-116">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="b7ea4-116">Workaround</span></span>

1. <span data-ttu-id="b7ea4-117">Verwenden Sie Visual Studio (2017 15.3 oder höher) oder „NuGet.exe“ (v4.3.0 oder höher).</span><span class="sxs-lookup"><span data-stu-id="b7ea4-117">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="b7ea4-118">Löschen Sie die deaktivierte Paketquelle, und verwenden Sie weiterhin „msbuild“ oder „dotnet.exe“.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-118">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="b7ea4-119">Für Ihre Projektmappe können Sie das Element „Clear“ in der Datei „NuGet.config“ verwenden und anschließend die notwendigen Paketquellen für diese Projektmappe definieren.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-119">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="b7ea4-120">Beim Verwenden der Paket-Manager-Konsole funktioniert die EINGABETASTE ggf. nicht</span><span class="sxs-lookup"><span data-stu-id="b7ea4-120">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="b7ea4-121">Problem</span><span class="sxs-lookup"><span data-stu-id="b7ea4-121">Issue</span></span>

<span data-ttu-id="b7ea4-122">Gelegentlich kann es vorkommen, dass die EINGABETASTE in der Paket-Manager-Konsole nicht funktioniert.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-122">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="b7ea4-123">Wenn dieses Problem auftritt, überprüfen Sie den Fortschritt für diese Korrektur und stellen Sie zusätzliche hilfreiche Informationen zu den Reproduktionsschritten bereit.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-123">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="b7ea4-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="b7ea4-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="b7ea4-125">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="b7ea4-125">Workaround</span></span>

<span data-ttu-id="b7ea4-126">Starten Sie Visual Studio neu und öffnen Sie die Paketverwaltungskonsole, bevor Sie die Projektmappe öffnen.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-126">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="b7ea4-127">Alternativ können Sie versuchen, die Datei `project.lock.json` zu löschen und dann erneut wiederherzustellen.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-127">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="b7ea4-128">Sie können DotNetCLITools nicht mit dem NuGet-Paket-Manager anzeigen, hinzufügen oder aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-128">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="b7ea4-129">Problem</span><span class="sxs-lookup"><span data-stu-id="b7ea4-129">Issue</span></span>

<span data-ttu-id="b7ea4-130">Der NuGet-Paket-Manager zeigt die DotNetCLITools nicht an und ermöglicht auch kein Hinzufügen/Aktualisieren dieser Tools.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="b7ea4-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="b7ea4-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="b7ea4-132">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="b7ea4-132">Workaround</span></span>

<span data-ttu-id="b7ea4-133">DotNetCLIToolReferences muss in der Projektdatei manuell bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="b7ea4-134">Die Neuzuweisung der Framework-Zielversion kann zu unvollständigen IntelliSense-Funktionen führen</span><span class="sxs-lookup"><span data-stu-id="b7ea4-134">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="b7ea4-135">Problem</span><span class="sxs-lookup"><span data-stu-id="b7ea4-135">Issue</span></span>

<span data-ttu-id="b7ea4-136">Die Neuzuweisung der Framework-Zielversion kann zu unvollständigen IntelliSense-Funktionen in Visual Studio führen.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-136">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="b7ea4-137">Dies geschieht, wenn Sie PackageReferences als Paket-Manager-Format verwenden.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-137">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="b7ea4-138">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="b7ea4-138">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="b7ea4-139">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="b7ea4-139">Workaround</span></span>

<span data-ttu-id="b7ea4-140">Führen Sie eine manuelle Wiederherstellung aus.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-140">Do a manual restore.</span></span>

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="b7ea4-141">Behobene Probleme mit dem NuGet 4.3 RTM-Zeitrahmen</span><span class="sxs-lookup"><span data-stu-id="b7ea4-141">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="b7ea4-142">In den [Anmerkungen zu der Version 4.0 RTM von NuGet](../release-notes/nuget-4.0-RTM.md) werden alle für NuGet 4.0 RTM behobenen Probleme aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-142">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

### <a name="features"></a><span data-ttu-id="b7ea4-143">Features</span><span class="sxs-lookup"><span data-stu-id="b7ea4-143">Features</span></span>

- <span data-ttu-id="b7ea4-144">Verbesserung der Wiederherstellungsleistung für NuGet: eine intelligentere NoOp-Version für Befehlszeilenwiederherstellungen und Visual Studio ([#5080](https://github.com/NuGet/Home/issues/5080))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-144">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

- <span data-ttu-id="b7ea4-145">.NET Core 2.0: Die Visual Studio- bzw. Dotnet-CLI sollte mithilfe einer vorhandenen NuGet-Funktion geöffnet werden: FallBack-Ordner ([#4939](https://github.com/NuGet/Home/issues/4939))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-145">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

- <span data-ttu-id="b7ea4-146">.NET Core 2.0: Benutzer können bestimmte Wiederherstellungswarnungen ignorieren oder auf einen Fehler erweitern ([#4898](https://github.com/NuGet/Home/issues/4898))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-146">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

- <span data-ttu-id="b7ea4-147">.NET Core 2.0: lokalisierte CLI-Assemblys ([#4896](https://github.com/NuGet/Home/issues/4896))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-147">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

- <span data-ttu-id="b7ea4-148">NET Core 2.0: Registrierung aller Warnungen bzw. Fehler in Objektdateien, einschließlich PackageTargetFallback ([#4895](https://github.com/NuGet/Home/issues/4895))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-148">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

- <span data-ttu-id="b7ea4-149">Aktivieren der TFM-Unterstützung: NetStandard2.0, Tizen ([#4892](https://github.com/NuGet/Home/issues/4892))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-149">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

- <span data-ttu-id="b7ea4-150">Reduzierung der Anzahl von NuGet.Core- und NuGet.Client-Projekten und somit auch von DLLs ([#2446](https://github.com/NuGet/Home/issues/2446))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-150">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

- <span data-ttu-id="b7ea4-151">Hinzufügen der Möglichkeit, NuGet-Warnungen als Fehler zu markieren ([#2395](https://github.com/NuGet/Home/issues/2395))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-151">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>

### <a name="bugs"></a><span data-ttu-id="b7ea4-152">Fehler</span><span class="sxs-lookup"><span data-stu-id="b7ea4-152">Bugs</span></span>

- <span data-ttu-id="b7ea4-153">„MSBuild /t:pack“ schlägt mit dem DevelopmentDependency-Parameter fehl und wird nicht von der PackTask-Aufgabe unterstützt ([#5584](https://github.com/NuGet/Home/issues/5584))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-153">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

- <span data-ttu-id="b7ea4-154">Verzeichnisstruktur für vereinfachte Inhaltsdateien, wenn nicht das Windows-Verzeichnistrennzeichen am Ende von „PackagePath“ hinzugefügt wird ([#4795](https://github.com/NuGet/Home/issues/4795))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-154">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

- <span data-ttu-id="b7ea4-155">.NET Core-Projekte unterstützen die Einstellung „developmentDependency“ nicht ([#4694](https://github.com/NuGet/Home/issues/4694))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-155">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

- <span data-ttu-id="b7ea4-156">„RestoreManagerPackage“ wird synchron geladen, wodurch der Benutzeroberflächenthread blockiert und ein Deadlock für Visual Studio eingetreten ist ([#4679](https://github.com/NuGet/Home/issues/4679))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-156">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

- <span data-ttu-id="b7ea4-157">dotnet</span><span class="sxs-lookup"><span data-stu-id="b7ea4-157">dotnet</span></span>
  - <span data-ttu-id="b7ea4-158">„dotnet restore“ (und daher auch „msbuild /t:restore“) überspringt Projekte mit einer expliziten Abhängigkeit von einem Projektmappenprojekt ([Nr. 4578](https://github.com/NuGet/Home/issues/4578))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-158">dotnetcore Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

- <span data-ttu-id="b7ea4-159">Wenn Ihre Projektmappe Verweise auf dasselbe Projekt enthält, funktioniert die Wiederherstellung möglicherweise nicht, wenn die Groß- und Kleinschreibung geändert wird.</span><span class="sxs-lookup"><span data-stu-id="b7ea4-159">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="b7ea4-160">Ebenfalls kommt es nicht zu einer Wiederherstellung, wenn verschiedene relative Pfade vorhanden sind, bei denen es allerdings keine Abweichungen im Hinblick auf Groß- und Kleinschreibung gibt ([#4574](https://github.com/NuGet/Home/issues/4574))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-160">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

- <span data-ttu-id="b7ea4-161">Ausführbare Dateien, die aus NuGet-Paketen wiederhergestellt werden, können mit .NET Core 2.0 nicht mehr ausgeführt werden ([#4424](https://github.com/NuGet/Home/issues/4424))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-161">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

- <span data-ttu-id="b7ea4-162">In der „NuGet.exe“-Datei gehen bei der Analyse der Projektmappendatei Details zur Ausnahme verloren ([#4411](https://github.com/NuGet/Home/issues/4411))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-162">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

- <span data-ttu-id="b7ea4-163">Das Paket speichert Inhaltsdateien an einem falschen Speicherort, wenn „ContentTargetFolders“ einen Pfad unter Windows enthält, der mit einem Schrägstrich („/“) endet ([#4407](https://github.com/NuGet/Home/issues/4407))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-163">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

- <span data-ttu-id="b7ea4-164">„DotNetCliToolReference“ kann für ein Toolpaket, das netcoreapp1.1 anzielt, nicht wiederhergestellt werden ([#4396](https://github.com/NuGet/Home/issues/4396))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-164">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

- <span data-ttu-id="b7ea4-165">Die aktualisierte NuGet-CLI behält die veraltete Bedingung für die Paketversion in einer Projektdatei bei (C++) ([#2449](https://github.com/NuGet/Home/issues/2449))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-165">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

### <a name="dcrs"></a><span data-ttu-id="b7ea4-166">DCRs</span><span class="sxs-lookup"><span data-stu-id="b7ea4-166">DCRs</span></span>

- <span data-ttu-id="b7ea4-167">„DotnetCliToolTargetFramework“ wird aus der CPS-Notation gelesen ([#5397](https://github.com/NuGet/Home/issues/5397))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-167">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

- <span data-ttu-id="b7ea4-168">Die Überprüfung von TPMinV sollte für UWP im Projektstil funktionieren ([#4763](https://github.com/NuGet/Home/issues/4763))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-168">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

- <span data-ttu-id="b7ea4-169">Verbesserung der Benutzeroberflächenbeschreibung für AutoReferenced-Pakete ([#4471](https://github.com/NuGet/Home/issues/4471))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-169">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

- <span data-ttu-id="b7ea4-170">Bei der NuGet-Wiederherstellung werden kompilierte Objekte aus dem Runtimebereich ausgewählt</span><span class="sxs-lookup"><span data-stu-id="b7ea4-170">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="b7ea4-171">([#4207](https://github.com/NuGet/Home/issues/4207))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

- <span data-ttu-id="b7ea4-172">Abhängigkeitsanalysen werden in der Sperrdatei gespeichert ([#1599](https://github.com/NuGet/Home/issues/1599))</span><span class="sxs-lookup"><span data-stu-id="b7ea4-172">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="links-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="b7ea4-173">Links zu GitHub-Problemen die in 4.3 RTM behoben wurden</span><span class="sxs-lookup"><span data-stu-id="b7ea4-173">Links to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="b7ea4-174">Probleme: Liste</span><span class="sxs-lookup"><span data-stu-id="b7ea4-174">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
