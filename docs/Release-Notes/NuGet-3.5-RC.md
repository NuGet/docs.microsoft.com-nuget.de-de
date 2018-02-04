---
title: 3.5 Anmerkungen zu dieser Version RC | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 3.5 RC einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-3.5 RC-versionsanmerkungen, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fdb84da5f1648ce4508afe6ddcf04bddd41284d3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="2fdc6-104">Anmerkungen dieser Version von NuGet 3.5 RC</span><span class="sxs-lookup"><span data-stu-id="2fdc6-104">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="2fdc6-105">[Anmerkungen zur Version von NuGet 3.5 Beta2](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Anmerkungen zu dieser Version](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-105">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="2fdc6-106">Version 3.5 konzentriert sich auf die Verbesserung der Qualität und Leistung von NuGet-Clients.</span><span class="sxs-lookup"><span data-stu-id="2fdc6-106">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="2fdc6-107">Darüber hinaus haben wir einige Funktionen wie die Unterstützung für geliefert [alternative Ordner](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) -Unterstützung in `.nuspec` und vieles mehr.</span><span class="sxs-lookup"><span data-stu-id="2fdc6-107">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="2fdc6-108">Probleme: Liste</span><span class="sxs-lookup"><span data-stu-id="2fdc6-108">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5 RC")

## <a name="bug-fixes"></a><span data-ttu-id="2fdc6-109">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="2fdc6-109">Bug Fixes</span></span>

* <span data-ttu-id="2fdc6-110">Installation/Wiederherstellung eines Pakets schlägt fehl mit "Paket enthält mehrere `.nuspec` Dateien."</span><span class="sxs-lookup"><span data-stu-id="2fdc6-110">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="2fdc6-111"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-111"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="2fdc6-112">NuGet-Pack erzwungen fügt `.tt` Dateien Inhaltsordner unabhängig davon, was - [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-112">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="2fdc6-113">NuGet-Pack Csproj (mit `project.json`) stürzt ab, wenn es keine PackOptions "und" Besitzer in JSON-Datei sind - [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-113">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="2fdc6-114">NuGet-Pack für `project.json` ignoriert PackOptions Tags wie Zusammenfassung, Autoren und Besitzer usw. - [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-114">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="2fdc6-115">NuGet-Pack ignoriert Abhängigkeiten in der Ausgabe `.nuspec` für `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-115">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="2fdc6-116">Aktualisieren mehrere Pakete mit Rollback lässt das Projekt in einem fehlerhaften Zustand versetzt - [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-116">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="2fdc6-117">Inhaltsdateien unter einer werden nicht hinzugefügt, für die netstandard-Projekte - [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-117">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="2fdc6-118">Bibliothek für .net Paket kann nicht standardmäßige ordnungsgemäß - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-118">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="2fdc6-119">Datei -> Neues Projekt-Klassenbibliothek (portabel) Projekt fehl in VS2015 und Dev15 - > [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-119">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="2fdc6-120">NuGet-Fehler: 1.0.0-\* ist keine gültige Versionszeichenfolge - [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-120">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="2fdc6-121">Find-Package ein Fehler auftritt, um die Anzeige "," Install-Package Works - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-121">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="2fdc6-122">Fehler bei "Install-Package jquery.validation" auf dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-122">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="2fdc6-123">Bei der installierten Visual Studio 2015 update 3 auf einem VS, die NuGet-Version 3.5.0 Fehlers - verwendet [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-123">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="2fdc6-124">Paket-Manager-Benutzeroberfläche: keine neue Version angezeigt, nach dem Aktualisieren eines Pakets- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-124">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="2fdc6-125">-"Apikey" für Delete-Befehlszeile nicht Lese-/gesendet 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-125">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="2fdc6-126">Falsches Zeichenfolgenformat: eine stabile Version eines Pakets sollte keine für eine Vorabversion Abhängigkeit.</span><span class="sxs-lookup"><span data-stu-id="2fdc6-126">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="2fdc6-127"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-127"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="2fdc6-128">Erstellen PCL (net46 und Windows 10)-Projekt Get NullRef-Ausnahme.</span><span class="sxs-lookup"><span data-stu-id="2fdc6-128">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="2fdc6-129"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-129"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="2fdc6-130">NuGet-Update sollten informationsmeldung bereitstellen, wenn eine höhere Version von "allowedversions"-Einschränkung - beschränkt ist [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-130">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="2fdc6-131">Anmeldeinformationen-Plug-in wurde mit dem Fehlercode:-1 / Fehler herunterladen bei Verwendung von mehreren Quellen - Anmeldeinformationsanbieter mit package [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-131">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="2fdc6-132">NuGet-Pack - Newtonsoft.Json fehlende paketabhängigkeit - [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-132">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="2fdc6-133">Fehler in ExecuteSynchronizedCore auf Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-133">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="2fdc6-134">Visual Studio unterstützt keine Umgebungsvariablen im RepositoryPath (nuget.exe bewirkt) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-134">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="2fdc6-135">Beheben Sie Probleme mit dem Zugriff - [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-135">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="2fdc6-136">Portable Frameworks mit getrennten Profilen werden zurückgewiesen.</span><span class="sxs-lookup"><span data-stu-id="2fdc6-136">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="2fdc6-137"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-137"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="2fdc6-138">NuGet-Paket-Manager sollten unmissverständlich, Optionsliste in Paketen Detail nicht für gilt `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-138">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="2fdc6-139">NuGet 3.3.0 Update schlägt fehl mit "eine weitere Einschränkung... definiert" Packages.config ", verhindert diesen Vorgang."</span><span class="sxs-lookup"><span data-stu-id="2fdc6-139">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="2fdc6-140"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-140"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="2fdc6-141">Installieren von einer lokalen Quelle, die löst nicht vorhanden ist eine gefälschte Nachricht - Paket [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-141">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="2fdc6-142">"Verfügbare Upgrade" Filter zeigt Upgrades, die die versionseinschränkung - verletzen [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-142">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="2fdc6-143">Leistungsverbesserungen</span><span class="sxs-lookup"><span data-stu-id="2fdc6-143">Performance Improvements</span></span>

* <span data-ttu-id="2fdc6-144">: Leistungsverbesserung ContentModel Ziel-Framework analysieren - [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-144">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="2fdc6-145">Leistung: Vermeiden Sie lesen `runtime.json` Dateien für die Wiederherstellung, die keine RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="2fdc6-145">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="2fdc6-146">Bei CI-Computer, die einer Stichprobe, die eine Aktualisierung 15 Sekunden bis 3 Sek. ASP.NET-Webanwendung reduziert wiederhergestellt werden.</span><span class="sxs-lookup"><span data-stu-id="2fdc6-146">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="2fdc6-147">Leistung: Package Manager Console init.ps1 Ladezeit [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="2fdc6-147">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="2fdc6-148">Zeit zum Öffnen von PackageManagerConsole verbessert in einigen Fällen von 132s in 10.</span><span class="sxs-lookup"><span data-stu-id="2fdc6-148">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="2fdc6-149">Lösen Sie ReSharper Leistungsprobleme in NuGet-Update - [#3044](https://github.com/NuGet/Home/issues/3044): für ein Beispielprojekt Zeit zum Installieren der Pakete von 140s auf reduziert 68s.</span><span class="sxs-lookup"><span data-stu-id="2fdc6-149">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="2fdc6-150">DCRs</span><span class="sxs-lookup"><span data-stu-id="2fdc6-150">DCRs</span></span>

* <span data-ttu-id="2fdc6-151">NuGet muss, damit Benutzer wissen, dass ein Upgrade/Installation in ein Dotnet-Tfm basierend PCL Probleme - verursachen könnte [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-151">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="2fdc6-152">Warnhinweis anzeigen, fehlerhafte installiert oder aktualisiert für das Projekt mit Tfm "Dotnet" - = [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-152">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="2fdc6-153">Hinzufügen von netcoreapp11 und netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-153">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="2fdc6-154">Drucken von NuGet-Warnung Headerinhalt in die Konsole in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-154">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="2fdc6-155">Nutzen der Vorteile AssemblyMetadata-Attribut für `.nuspec` Ersetzungen - token [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-155">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="2fdc6-156">Entfernen Sie die gesperrte Eigenschaft aus der Sperrdatei - [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-156">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="2fdc6-157">Symbolpakete sollten nicht jemals Installation verwendet werden, oder aktualisieren #2807</span><span class="sxs-lookup"><span data-stu-id="2fdc6-157">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="2fdc6-158">Features</span><span class="sxs-lookup"><span data-stu-id="2fdc6-158">Features</span></span>

* <span data-ttu-id="2fdc6-159">Unterstützung für alternative paketordnern - [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-159">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="2fdc6-160">Entwerfen und implementieren Sie eine Vorstellung von den Pakettyp Tool Pakete - Unterstützung [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-160">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="2fdc6-161">-API, um den Pfad zu dem Ordner "globale Pakete" - abzurufen [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-161">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="2fdc6-162">Systemeigene Updatepakete Support - [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="2fdc6-162">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
