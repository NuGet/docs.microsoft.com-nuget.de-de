---
title: Anmerkungen zu Version 4.5 RTM von NuGet
description: Anmerkungen zu NuGet 4.5 RTM, einschließlich bekannter Fehler, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 321aedb471bc6f86e9c03878093b199267e31195
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496581"
---
# <a name="nuget-45-release-notes"></a><span data-ttu-id="cb16d-103">Versionshinweise zu NuGet 4.5</span><span class="sxs-lookup"><span data-stu-id="cb16d-103">NuGet 4.5 Release Notes</span></span>

<span data-ttu-id="cb16d-104">[NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe) ist im Lieferumfang von [Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) enthalten.</span><span class="sxs-lookup"><span data-stu-id="cb16d-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="summary-whats-new-in-450"></a><span data-ttu-id="cb16d-105">Zusammenfassung: Neuerungen in Version 4.5.0</span><span class="sxs-lookup"><span data-stu-id="cb16d-105">Summary: What's New in 4.5.0</span></span>

## <a name="summary-whats-new-in-452"></a><span data-ttu-id="cb16d-106">Zusammenfassung: Neuerungen in Version 4.5.2</span><span class="sxs-lookup"><span data-stu-id="cb16d-106">Summary: What's New in 4.5.2</span></span>

* <span data-ttu-id="cb16d-107">Sicherheitsfix: Die Berechtigungen für Dateien, die in ~/.nuget erstellt werden, sind nicht restriktiv genug ([#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)).</span><span class="sxs-lookup"><span data-stu-id="cb16d-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-453"></a><span data-ttu-id="cb16d-108">Zusammenfassung: Neuerungen in Version 4.5.3</span><span class="sxs-lookup"><span data-stu-id="cb16d-108">Summary: What's New in 4.5.3</span></span>

* <span data-ttu-id="cb16d-109">Sicherheitsfix: Dateien innerhalb von NUPKGs können einen relativen Pfad über dem NUPKG-Verzeichnis besitzen ([#7906](https://github.com/NuGet/Home/issues/7906)).</span><span class="sxs-lookup"><span data-stu-id="cb16d-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="cb16d-110">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="cb16d-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="cb16d-111">Probleme mit .NET Standard 2.0 mit .NET Framework und NuGet</span><span class="sxs-lookup"><span data-stu-id="cb16d-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="cb16d-112">.NET Standard und die dazugehörigen Tools wurden so konzipiert, dass Projekte, die für .NET Framework 4.6.1 erstellt wurden, NuGet-Pakete und -Projekte verarbeiten können, die für .NET Standard 2.0 oder früher erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="cb16d-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="cb16d-113">In [diesem Dokument](https://github.com/dotnet/standard/issues/481) werden die Probleme, die in diesem Szenario auftreten können, der Plan für die Behebung dieser Probleme und Problemumgehungen zusammengefasst, die Sie nach aktuellem Stand für die Tools bereitstellen können.</span><span class="sxs-lookup"><span data-stu-id="cb16d-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="cb16d-114">Sie können DotNetCLITools nicht mit dem NuGet-Paket-Manager anzeigen, hinzufügen oder aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="cb16d-114">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="cb16d-115">Problem</span><span class="sxs-lookup"><span data-stu-id="cb16d-115">Issue</span></span>

<span data-ttu-id="cb16d-116">Der NuGet-Paket-Manager zeigt die DotNetCLITools nicht an und ermöglicht auch kein Hinzufügen/Aktualisieren dieser Tools.</span><span class="sxs-lookup"><span data-stu-id="cb16d-116">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="cb16d-117">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="cb16d-117">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="cb16d-118">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="cb16d-118">Workaround</span></span>

<span data-ttu-id="cb16d-119">DotNetCLIToolReferences muss in der Projektdatei manuell bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="cb16d-119">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="cb16d-120">Die Neuzuweisung der Framework-Zielversion kann zu unvollständigen IntelliSense-Funktionen führen</span><span class="sxs-lookup"><span data-stu-id="cb16d-120">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="cb16d-121">Problem</span><span class="sxs-lookup"><span data-stu-id="cb16d-121">Issue</span></span>

<span data-ttu-id="cb16d-122">Die Neuzuweisung der Framework-Zielversion kann zu unvollständigen IntelliSense-Funktionen in Visual Studio führen.</span><span class="sxs-lookup"><span data-stu-id="cb16d-122">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="cb16d-123">Dies geschieht, wenn Sie PackageReferences als Paket-Manager-Format verwenden.</span><span class="sxs-lookup"><span data-stu-id="cb16d-123">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="cb16d-124">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="cb16d-124">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="cb16d-125">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="cb16d-125">Workaround</span></span>

<span data-ttu-id="cb16d-126">Führen Sie eine manuelle Wiederherstellung aus.</span><span class="sxs-lookup"><span data-stu-id="cb16d-126">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="cb16d-127">Ein Paket in einem .NET Core-Projekt, das eine Assembly mit einer ungültigen Signatur enthält, kann eine unendliche Wiederherstellungsschleife auslösen</span><span class="sxs-lookup"><span data-stu-id="cb16d-127">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="cb16d-128">Problem</span><span class="sxs-lookup"><span data-stu-id="cb16d-128">Issue</span></span>

<span data-ttu-id="cb16d-129">Bei der Verwendung eines Pakets mit einer Assembly, die eine ungültige Signatur enthält, oder beim Festlegen der Paketversion mit dem DateTime-Ticker tritt gelegentlich bei der automatischen Paketwiederherstellung eine Endlosschleife auf ([dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457)).</span><span class="sxs-lookup"><span data-stu-id="cb16d-129">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="cb16d-130">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="cb16d-130">Workaround</span></span>

<span data-ttu-id="cb16d-131">Zurzeit gibt es keine Problemumgehung.</span><span class="sxs-lookup"><span data-stu-id="cb16d-131">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="cb16d-132">Behobene Probleme für den NuGet 4.5 RTM-Zeitrahmen</span><span class="sxs-lookup"><span data-stu-id="cb16d-132">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="cb16d-133">In den [Anmerkungen zu NuGet 4.4 RTM](../release-notes/nuget-4.4-RTM.md) finden Sie die in NuGet RTM 4.4 behobenen Probleme.</span><span class="sxs-lookup"><span data-stu-id="cb16d-133">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="cb16d-134">Features</span><span class="sxs-lookup"><span data-stu-id="cb16d-134">Features</span></span>

- <span data-ttu-id="cb16d-135">Deaktivieren des automatischen Übertragens von Symbolpaketen per Push ([#6113](https://github.com/NuGet/Home/issues/6113))</span><span class="sxs-lookup"><span data-stu-id="cb16d-135">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="cb16d-136">Fehler</span><span class="sxs-lookup"><span data-stu-id="cb16d-136">Bugs</span></span>

- <span data-ttu-id="cb16d-137">[Regression] in 15.5p1: Portable0.0 wurde übersprungen ([#6105](https://github.com/NuGet/Home/issues/6105))</span><span class="sxs-lookup"><span data-stu-id="cb16d-137">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="cb16d-138">Nach der Wiederherstellung fehlen Objekte aus Paketen ([#5995](https://github.com/NuGet/Home/issues/5995))</span><span class="sxs-lookup"><span data-stu-id="cb16d-138">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="cb16d-139">Anbieter von Pluginanmeldeinformationen funktionieren nicht mit URIs, die Leerräume enthalten ([#5982](https://github.com/NuGet/Home/issues/5982))</span><span class="sxs-lookup"><span data-stu-id="cb16d-139">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="cb16d-140">Wenn das Wiederherstellen eines Pakets fehlgeschlagen ist, sollten Fehler in der Ausgabe auch dann ausgegeben werden, wenn der geringste Ausführlichkeitsgrad aktiviert ist ([#5658](https://github.com/NuGet/Home/issues/5658))</span><span class="sxs-lookup"><span data-stu-id="cb16d-140">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="cb16d-141">dotnet</span><span class="sxs-lookup"><span data-stu-id="cb16d-141">dotnet</span></span>
  - <span data-ttu-id="cb16d-142">„dotnetcore restore“ auf Projektmappenebene folgt nicht „ProjectReference“, wenn „ReferenceOutputAssembly“ auf FALSE festgelegt ist, was zu zufälligen Buildfehlern führt ([Nr. 5490](https://github.com/NuGet/Home/issues/5490))</span><span class="sxs-lookup"><span data-stu-id="cb16d-142">dotnetcore restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="cb16d-143">Die automatische Vervollständigung funktioniert in PMC mit Objektmethoden nicht ordnungsgemäß ([#4800](https://github.com/NuGet/Home/issues/4800))</span><span class="sxs-lookup"><span data-stu-id="cb16d-143">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="cb16d-144">Das Wiederherstellen von „nuget.exe“ mit Visual Studio 2015-Toolset schlägt fehl ([#4713](https://github.com/NuGet/Home/issues/4713))</span><span class="sxs-lookup"><span data-stu-id="cb16d-144">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="cb16d-145">Leistung: Die Instanziierung von PMC ist in Visual Studio 2017 ressourcenintensiv ([#4205](https://github.com/NuGet/Home/issues/4205))</span><span class="sxs-lookup"><span data-stu-id="cb16d-145">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="cb16d-146">Es dauert lange, Abhängigkeitsinformationen bei einer langsamen Verbindung abzurufen ([#4089](https://github.com/NuGet/Home/issues/4089))</span><span class="sxs-lookup"><span data-stu-id="cb16d-146">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="cb16d-147">Der Befehl zur Deinstallation eines Pakets mit -RemoveDependencies schlägt fehl, wenn mehrere Pakete eine gemeinsame Abhängigkeit haben ([#4026](https://github.com/NuGet/Home/issues/4026))</span><span class="sxs-lookup"><span data-stu-id="cb16d-147">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="cb16d-148">„NuGet.Core.nupkg“ auf die Veröffentlichung vorbereiten ([#3581](https://github.com/NuGet/Home/issues/3581))</span><span class="sxs-lookup"><span data-stu-id="cb16d-148">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="cb16d-149">Das NuGet-Paket löst die ID des Verzeichnisnamens auf, wenn -IncludeProjectReferences für die CSPROJ-Datei und „project.json“ verwendet wird ([#3566](https://github.com/NuGet/Home/issues/3566))</span><span class="sxs-lookup"><span data-stu-id="cb16d-149">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="cb16d-150">Der Typinitialisierer für „NuGet.ProxyCache“ hat eine Ausnahme ausgelöst ([#3144](https://github.com/NuGet/Home/issues/3144))</span><span class="sxs-lookup"><span data-stu-id="cb16d-150">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="cb16d-151">Problem beim Wiederherstellen von NuGet mit Kudu ([#3087](https://github.com/NuGet/Home/issues/3087))</span><span class="sxs-lookup"><span data-stu-id="cb16d-151">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="cb16d-152">UI-Client zeigt weder Fehler noch Warnungen an, wenn die Suche vor Registrierungsblobs durchgeführt wird ([#2149](https://github.com/NuGet/Home/issues/2149))</span><span class="sxs-lookup"><span data-stu-id="cb16d-152">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="cb16d-153">Get-Packages-Updates generiert eine falsche Abfrage ([#2135](https://github.com/NuGet/Home/issues/2135))</span><span class="sxs-lookup"><span data-stu-id="cb16d-153">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="cb16d-154">Links zu GitHub-Problemen die in 4.5 RTM behoben wurden</span><span class="sxs-lookup"><span data-stu-id="cb16d-154">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="cb16d-155">Liste der Probleme</span><span class="sxs-lookup"><span data-stu-id="cb16d-155">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
