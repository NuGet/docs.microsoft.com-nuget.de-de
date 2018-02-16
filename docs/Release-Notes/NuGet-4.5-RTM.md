---
title: Anmerkungen zu NuGet 4.5 RTM | Microsoft-Dokumentation
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 12/4/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Anmerkungen zu NuGet 4.5 RTM, einschließlich bekannter Fehler, Fehlerkorrekturen, hinzugefügter Features und DCRs."
keywords: "Anmerkungen zu NuGet 4.5 RTM, Fehlerkorrekturen, bekannte Fehler, hinzugefügte Features, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: e4727d46812cbfeb2e7094ddf28bf4e738e8aeea
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-45-rtm-release-notes"></a><span data-ttu-id="6bbfe-104">Anmerkungen zu Version 4.5 RTM von NuGet</span><span class="sxs-lookup"><span data-stu-id="6bbfe-104">NuGet 4.5 RTM Release Notes</span></span>

<span data-ttu-id="6bbfe-105">[NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe) ist im Lieferumfang von [Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) enthalten.</span><span class="sxs-lookup"><span data-stu-id="6bbfe-105">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="known-issues"></a><span data-ttu-id="6bbfe-106">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="6bbfe-106">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="6bbfe-107">Probleme mit .NET Standard 2.0 mit .NET Framework und NuGet</span><span class="sxs-lookup"><span data-stu-id="6bbfe-107">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="6bbfe-108">.NET Standard und die dazugehörigen Tools wurden so konzipiert, dass Projekte, die für .NET Framework 4.6.1 erstellt wurden, NuGet-Pakete und -Projekte verarbeiten können, die für .NET Standard 2.0 oder früher erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="6bbfe-108">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="6bbfe-109">In [diesem Dokument](https://github.com/dotnet/standard/issues/481) werden die Probleme, die in diesem Szenario auftreten können, der Plan für die Behebung dieser Probleme und Problemumgehungen zusammengefasst, die Sie nach aktuellem Stand für die Tools bereitstellen können.</span><span class="sxs-lookup"><span data-stu-id="6bbfe-109">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="6bbfe-110">Sie können DotNetCLITools nicht mit dem NuGet-Paket-Manager anzeigen, hinzufügen oder aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="6bbfe-110">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="6bbfe-111">Problem</span><span class="sxs-lookup"><span data-stu-id="6bbfe-111">Issue</span></span>

<span data-ttu-id="6bbfe-112">Der NuGet-Paket-Manager zeigt die DotNetCLITools nicht an und ermöglicht auch kein Hinzufügen/Aktualisieren dieser Tools.</span><span class="sxs-lookup"><span data-stu-id="6bbfe-112">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="6bbfe-113">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="6bbfe-113">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="6bbfe-114">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="6bbfe-114">Workaround</span></span>

<span data-ttu-id="6bbfe-115">DotNetCLIToolReferences muss in der Projektdatei manuell bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="6bbfe-115">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="6bbfe-116">Die Neuzuweisung der Framework-Zielversion kann zu unvollständigen IntelliSense-Funktionen führen</span><span class="sxs-lookup"><span data-stu-id="6bbfe-116">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="6bbfe-117">Problem</span><span class="sxs-lookup"><span data-stu-id="6bbfe-117">Issue</span></span>

<span data-ttu-id="6bbfe-118">Die Neuzuweisung der Framework-Zielversion kann zu unvollständigen IntelliSense-Funktionen in Visual Studio führen.</span><span class="sxs-lookup"><span data-stu-id="6bbfe-118">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="6bbfe-119">Dies geschieht, wenn Sie PackageReferences als Paket-Manager-Format verwenden.</span><span class="sxs-lookup"><span data-stu-id="6bbfe-119">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="6bbfe-120">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="6bbfe-120">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="6bbfe-121">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="6bbfe-121">Workaround</span></span>

<span data-ttu-id="6bbfe-122">Führen Sie eine manuelle Wiederherstellung aus.</span><span class="sxs-lookup"><span data-stu-id="6bbfe-122">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="6bbfe-123">Ein Paket in einem .NET Core-Projekt, das eine Assembly mit einer ungültigen Signatur enthält, kann eine unendliche Wiederherstellungsschleife auslösen</span><span class="sxs-lookup"><span data-stu-id="6bbfe-123">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="6bbfe-124">Problem</span><span class="sxs-lookup"><span data-stu-id="6bbfe-124">Issue</span></span>

<span data-ttu-id="6bbfe-125">Bei der Verwendung eines Pakets mit einer Assembly, die eine ungültige Signatur enthält, oder beim Festlegen der Paketversion mit dem DateTime-Ticker tritt gelegentlich bei der automatischen Paketwiederherstellung eine Endlosschleife auf ([dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457)).</span><span class="sxs-lookup"><span data-stu-id="6bbfe-125">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="6bbfe-126">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="6bbfe-126">Workaround</span></span>

<span data-ttu-id="6bbfe-127">Zurzeit gibt es keine Problemumgehung.</span><span class="sxs-lookup"><span data-stu-id="6bbfe-127">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="6bbfe-128">Behobene Probleme für den NuGet 4.5 RTM-Zeitrahmen</span><span class="sxs-lookup"><span data-stu-id="6bbfe-128">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="6bbfe-129">In den [Anmerkungen zu NuGet 4.4 RTM](../release-notes/nuget-4.4-RTM.md) finden Sie die in NuGet RTM 4.4 behobenen Probleme.</span><span class="sxs-lookup"><span data-stu-id="6bbfe-129">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="6bbfe-130">Features</span><span class="sxs-lookup"><span data-stu-id="6bbfe-130">Features</span></span>

- <span data-ttu-id="6bbfe-131">Deaktivieren des automatischen Übertragens von Symbolpaketen per Push ([#6113](https://github.com/NuGet/Home/issues/6113))</span><span class="sxs-lookup"><span data-stu-id="6bbfe-131">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="6bbfe-132">Fehler</span><span class="sxs-lookup"><span data-stu-id="6bbfe-132">Bugs</span></span>

- <span data-ttu-id="6bbfe-133">[Regression] in 15.5p1: Portable0.0 wurde übersprungen ([#6105](https://github.com/NuGet/Home/issues/6105))</span><span class="sxs-lookup"><span data-stu-id="6bbfe-133">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="6bbfe-134">Nach der Wiederherstellung fehlen Objekte aus Paketen ([#5995](https://github.com/NuGet/Home/issues/5995))</span><span class="sxs-lookup"><span data-stu-id="6bbfe-134">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="6bbfe-135">Anbieter von Pluginanmeldeinformationen funktionieren nicht mit URIs, die Leerräume enthalten ([#5982](https://github.com/NuGet/Home/issues/5982))</span><span class="sxs-lookup"><span data-stu-id="6bbfe-135">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="6bbfe-136">Wenn das Wiederherstellen eines Pakets fehlgeschlagen ist, sollten Fehler in der Ausgabe auch dann ausgegeben werden, wenn der geringste Ausführlichkeitsgrad aktiviert ist ([#5658](https://github.com/NuGet/Home/issues/5658))</span><span class="sxs-lookup"><span data-stu-id="6bbfe-136">If package failed to restore, error should be printed i the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="6bbfe-137">Die .NET-Wiederherstellung auf Projektmappenebene folgt nicht ProjectReference, wenn ReferenceOutputAssembly auf FALSE festgelegt ist, was zu zufälligen Buildfehlern führt ([#5490](https://github.com/NuGet/Home/issues/5490))</span><span class="sxs-lookup"><span data-stu-id="6bbfe-137">dotnet restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="6bbfe-138">Die automatische Vervollständigung funktioniert in PMC mit Objektmethoden nicht ordnungsgemäß ([#4800](https://github.com/NuGet/Home/issues/4800))</span><span class="sxs-lookup"><span data-stu-id="6bbfe-138">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="6bbfe-139">Das Wiederherstellen von „nuget.exe“ mit Visual Studio 2015-Toolset schlägt fehl ([#4713](https://github.com/NuGet/Home/issues/4713))</span><span class="sxs-lookup"><span data-stu-id="6bbfe-139">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="6bbfe-140">Leistung: Die Instanziierung von PMC ist in Visual Studio 2017 ressourcenintensiv ([#4205](https://github.com/NuGet/Home/issues/4205))</span><span class="sxs-lookup"><span data-stu-id="6bbfe-140">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="6bbfe-141">Es dauert lange, Abhängigkeitsinformationen bei einer langsamen Verbindung abzurufen ([#4089](https://github.com/NuGet/Home/issues/4089))</span><span class="sxs-lookup"><span data-stu-id="6bbfe-141">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="6bbfe-142">Der Befehl zur Deinstallation eines Pakets mit -RemoveDependencies schlägt fehl, wenn mehrere Pakete eine gemeinsame Abhängigkeit haben ([#4026](https://github.com/NuGet/Home/issues/4026))</span><span class="sxs-lookup"><span data-stu-id="6bbfe-142">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="6bbfe-143">„NuGet.Core.nupkg“ auf die Veröffentlichung vorbereiten ([#3581](https://github.com/NuGet/Home/issues/3581))</span><span class="sxs-lookup"><span data-stu-id="6bbfe-143">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="6bbfe-144">Das NuGet-Paket löst die ID des Verzeichnisnamens auf, wenn -IncludeProjectReferences für die CSPROJ-Datei und „project.json“ verwendet wird ([#3566](https://github.com/NuGet/Home/issues/3566))</span><span class="sxs-lookup"><span data-stu-id="6bbfe-144">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="6bbfe-145">Der Typinitialisierer für „NuGet.ProxyCache“ hat eine Ausnahme ausgelöst ([#3144](https://github.com/NuGet/Home/issues/3144))</span><span class="sxs-lookup"><span data-stu-id="6bbfe-145">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="6bbfe-146">Problem beim Wiederherstellen von NuGet mit Kudu ([#3087](https://github.com/NuGet/Home/issues/3087))</span><span class="sxs-lookup"><span data-stu-id="6bbfe-146">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="6bbfe-147">UI-Client zeigt weder Fehler noch Warnungen an, wenn die Suche vor Registrierungsblobs durchgeführt wird ([#2149](https://github.com/NuGet/Home/issues/2149))</span><span class="sxs-lookup"><span data-stu-id="6bbfe-147">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="6bbfe-148">Get-Packages-Updates generiert eine falsche Abfrage ([#2135](https://github.com/NuGet/Home/issues/2135))</span><span class="sxs-lookup"><span data-stu-id="6bbfe-148">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="6bbfe-149">Links zu GitHub-Problemen die in 4.5 RTM behoben wurden</span><span class="sxs-lookup"><span data-stu-id="6bbfe-149">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="6bbfe-150">Liste der Probleme</span><span class="sxs-lookup"><span data-stu-id="6bbfe-150">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
