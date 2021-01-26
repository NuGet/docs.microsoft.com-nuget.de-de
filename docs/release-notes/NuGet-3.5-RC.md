---
title: 3,5 RC-Versions Anmerkungen
description: Anmerkungen zu dieser Version von nuget 3,5 RC, einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780194"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="c20aa-103">Anmerkungen zu dieser Version von nuget 3,5 RC</span><span class="sxs-lookup"><span data-stu-id="c20aa-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="c20aa-104">Anmerkungen zu dieser [Version von nuget 3,5-Beta2](../release-notes/nuget-3.5-Beta2.md)  |  [Anmerkungen zu dieser Version von nuget 3,5-RTM](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="c20aa-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="c20aa-105">3,5 Release konzentriert sich auf die Verbesserung der Qualität und Leistung von nuget-Clients.</span><span class="sxs-lookup"><span data-stu-id="c20aa-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="c20aa-106">Außerdem haben wir einige Features wie Unterstützung für [Fall Back Ordner](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) -Unterstützung in `.nuspec` und mehr geliefert.</span><span class="sxs-lookup"><span data-stu-id="c20aa-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="c20aa-107">Liste der Probleme</span><span class="sxs-lookup"><span data-stu-id="c20aa-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="c20aa-108">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="c20aa-108">Bug Fixes</span></span>

* <span data-ttu-id="c20aa-109">Die Installation/Wiederherstellung eines Pakets schlägt fehl, wenn das Paket mehrere `.nuspec` Dateien enthält.</span><span class="sxs-lookup"><span data-stu-id="c20aa-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="c20aa-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="c20aa-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="c20aa-111">Das nuget-Paket fügt `.tt` Dateien dem Inhalts Ordner unabhängig von der- [#3203](https://github.com/NuGet/Home/issues/3203) hinzu.</span><span class="sxs-lookup"><span data-stu-id="c20aa-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="c20aa-112">Das nuget-Paket "csproj" (mit `project.json` ) stürzt ab, wenn keine packoptions und Besitzer in der JSON-Datei vorhanden sind [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="c20aa-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="c20aa-113">Das nuget-Paket für `project.json` ignoriert packoptions-Tags wie Zusammenfassung, Autoren, Besitzer usw.- [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="c20aa-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="c20aa-114">Das nuget-Paket ignoriert Abhängigkeiten in der Ausgabe `.nuspec` für `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="c20aa-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="c20aa-115">Wenn Sie mehrere Pakete mit Rollback aktualisieren, bleibt das Projekt in einem unterbrochenen Zustand [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="c20aa-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="c20aa-116">"Contentfiles" unter "Any" wird nicht für netstandard-Projekte hinzugefügt- [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="c20aa-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="c20aa-117">Die Bibliothek für .NET Standard kann nicht ordnungsgemäß [#3108](https://github.com/NuGet/Home/issues/3108) werden.</span><span class="sxs-lookup"><span data-stu-id="c20aa-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="c20aa-118">Datei > neues Projekt > Klassenbibliothek (portabel) schlägt in VS2015 und Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="c20aa-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="c20aa-119">Der nuget-Fehler-1.0.0-\* ist keine gültige Versions Zeichenfolge [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="c20aa-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="c20aa-120">Find-Package kann nicht angezeigt werden, aber Install-Package Works- [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="c20aa-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="c20aa-121">Fehler bei "Install-package jQuery. Validation" auf dev15- [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="c20aa-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="c20aa-122">Bei der Installation von vs 2015 Update 3 auf einem vs, der die nuget-Version verwendet 3.5.0 Fehler tritt auf [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="c20aa-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="c20aa-123">Benutzeroberfläche des Paket-Managers: zeigt keine neue Version nach dem Aktualisieren eines Pakets an [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="c20aa-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="c20aa-124">-APIKey in der Befehlszeile "Delete" wird in 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037) nicht gelesen/gesendet</span><span class="sxs-lookup"><span data-stu-id="c20aa-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="c20aa-125">Falsche Zeichenfolge: ein stabiles Release eines Pakets sollte nicht für eine vorab Abhängigkeit vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="c20aa-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="c20aa-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="c20aa-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="c20aa-127">Beim Erstellen des Projekts PCL ("net46 und Windows 10) wird die Ausnahme NullRef-Ausnahme zurückerhalten.</span><span class="sxs-lookup"><span data-stu-id="c20aa-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="c20aa-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="c20aa-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="c20aa-129">Das nuget-Update sollte eine informative Nachricht bereitstellen, wenn eine höhere Version durch die Einschränkung der Einschränkung-Version eingeschränkt ist [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="c20aa-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="c20aa-130">Das Anmelde Informations-Plug-in wurde mit Fehler-1/Fehler beim Herunterladen des Pakets beendet, wenn Anmelde Informationsanbieter mit mehreren Quellen verwendet werden [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="c20aa-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="c20aa-131">nuget-Paket-fehlende Newtonsoft.Jsin der Paketabhängigkeit [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="c20aa-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="c20aa-132">Fehler in executesynchronizedcore unter Linux/MacOS + Mono- [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="c20aa-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="c20aa-133">VS unterstützt keine Umgebungsvariablen in repositoryPath (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="c20aa-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="c20aa-134">Beheben von Barrierefreiheits Problemen: [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="c20aa-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="c20aa-135">Portable Frameworks mit mittels Bindestrich-Profilen werden abgelehnt.</span><span class="sxs-lookup"><span data-stu-id="c20aa-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="c20aa-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="c20aa-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="c20aa-137">Der nuget-Paket-Manager sollte deutlich machen, dass die Optionsliste in Paket Details nicht für `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="c20aa-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="c20aa-138">Nuget 3.3.0 Update schlägt mit einer zusätzlichen Einschränkung fehl... der in packages.config definierte Vorgang wird verhindert.</span><span class="sxs-lookup"><span data-stu-id="c20aa-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="c20aa-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="c20aa-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="c20aa-140">Das Installieren eines Pakets aus einer lokalen Quelle, die nicht vorhanden ist, löst eine falsche Nachricht aus [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="c20aa-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="c20aa-141">Filter "Upgrade vailable" zeigt Upgrades an, die gegen die Versions Einschränkung verstoßen- [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="c20aa-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="c20aa-142">Leistungsverbesserungen</span><span class="sxs-lookup"><span data-stu-id="c20aa-142">Performance Improvements</span></span>

* <span data-ttu-id="c20aa-143">Leistung: verbessern der Inhalts Modell-Ziel Framework- [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="c20aa-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="c20aa-144">Leistung: vermeiden `runtime.json` Sie das Lesen von Dateien für Wiederherstellungen, die keine RIDs [#3150](https://github.com/NuGet/Home/issues/3150)haben.</span><span class="sxs-lookup"><span data-stu-id="c20aa-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="c20aa-145">Auf CI-Computern wird die Wiederherstellung einer Beispiel-ASP.NET-Webanwendung von mehr als 15 Sekunden auf 3 Sekunden reduziert.</span><span class="sxs-lookup"><span data-stu-id="c20aa-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="c20aa-146">Leistung: init.ps1 Ladezeit [#2956](https://github.com/NuGet/Home/issues/2956)der Paket-Manager-Konsole.</span><span class="sxs-lookup"><span data-stu-id="c20aa-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="c20aa-147">Die Zeit zum Öffnen von packagemanagerconsole wurde in einigen Fällen von 132 bis 10S verbessert.</span><span class="sxs-lookup"><span data-stu-id="c20aa-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="c20aa-148">Lösen Sie reschärfere Leistungsprobleme beim nuget-Update- [#3044](https://github.com/NuGet/Home/issues/3044): in einem Beispiel Projekt wird die Zeit zum Installieren von Paketen von 140s auf 68s verkürzt.</span><span class="sxs-lookup"><span data-stu-id="c20aa-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="c20aa-149">DCRs</span><span class="sxs-lookup"><span data-stu-id="c20aa-149">DCRs</span></span>

* <span data-ttu-id="c20aa-150">Nuget muss den Benutzern mitteilen, dass ein Upgrade/Installation in einer dotnet TFM-basierten PCL Probleme verursachen könnte [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="c20aa-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="c20aa-151">Warnung bei fehlerhafter Installation/Upgrade für Projekt w/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="c20aa-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="c20aa-152">Netcoreapp11-und netstandard17-Unterstützung hinzufügen- [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="c20aa-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="c20aa-153">Drucken NuGet-Warning Header Inhalt in der Konsole in nuget.exe- [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="c20aa-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="c20aa-154">Verwenden des ASSEMBLYMETADATA-Attributs für `.nuspec` tokenersetzungen- [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="c20aa-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="c20aa-155">Entfernen Sie die gesperrte Eigenschaft aus der Sperrdatei [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="c20aa-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="c20aa-156">Symbol Pakete sollten nicht jemals in Installations-oder Update #2807 verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="c20aa-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="c20aa-157">Features</span><span class="sxs-lookup"><span data-stu-id="c20aa-157">Features</span></span>

* <span data-ttu-id="c20aa-158">Unterstützung für Fall Back Paket Ordner- [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="c20aa-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="c20aa-159">Entwerfen und implementieren Sie ein Konzept des Pakettyps, um Tool Pakete zu unterstützen- [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="c20aa-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="c20aa-160">API, um den Pfad zum Ordner für globale Pakete zu erhalten [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="c20aa-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="c20aa-161">Unterstützung für Native Pakete aktualisieren- [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="c20aa-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
