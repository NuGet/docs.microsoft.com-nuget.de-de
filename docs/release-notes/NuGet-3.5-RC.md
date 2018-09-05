---
title: 3.5 RC-Versionsanmerkungen
description: Anmerkungen zu NuGet 3.5 RC, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548537"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="d1459-103">Anmerkungen dieser Version von NuGet 3.5 RC</span><span class="sxs-lookup"><span data-stu-id="d1459-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="d1459-104">[Anmerkungen zu NuGet 3.5-Beta2](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5 – Anmerkungen zu dieser Version RTM](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="d1459-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="d1459-105">3.5 Version konzentriert sich auf die Verbesserung der Qualität und Leistung von NuGet-Clients.</span><span class="sxs-lookup"><span data-stu-id="d1459-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="d1459-106">Darüber hinaus haben wir einige Funktionen wie Unterstützung für ausgeliefert [Fallback-Ordnern](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) -Unterstützung in `.nuspec` und vieles mehr.</span><span class="sxs-lookup"><span data-stu-id="d1459-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="d1459-107">Probleme: Liste</span><span class="sxs-lookup"><span data-stu-id="d1459-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="d1459-108">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="d1459-108">Bug Fixes</span></span>

* <span data-ttu-id="d1459-109">Installation/Wiederherstellung eines Pakets schlägt fehl mit "-Paket enthält mehrere `.nuspec` Dateien."</span><span class="sxs-lookup"><span data-stu-id="d1459-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="d1459-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="d1459-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="d1459-111">NuGet Pack erzwungen fügt `.tt` Dateien zum Ordner "Content" unabhängig davon, was - [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="d1459-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="d1459-112">NuGet Pack Csproj (mit `project.json`) stürzt ab, wenn es keine PackOptions und Besitzer in der JSON-Datei sind - [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="d1459-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="d1459-113">NuGet Pack für `project.json` ignoriert PackOptions Tags wie Zusammenfassung, Autoren und Besitzer usw. – [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="d1459-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="d1459-114">NuGet Pack werden die Abhängigkeiten in der Ausgabe ignoriert `.nuspec` für `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="d1459-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="d1459-115">Aktualisieren mehrere Pakete mit Rollback lässt das Projekt in einem unterbrochenen Zustand - [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="d1459-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="d1459-116">"Contentfiles", unter einer werden nicht hinzugefügt werden, für die Netstandard-Projekte – [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="d1459-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="d1459-117">Kann nicht gepackt werden Library für .net Standard ordnungsgemäß - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="d1459-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="d1459-118">Datei -> Neues Projekt -> Klassenbibliothek (portabel) ein Fehler auftritt-Projekt in Visual Studio 2015 und Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="d1459-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="d1459-119">NuGet-Fehler: 1.0.0-\* ist keine gültige Versionszeichenfolge - [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="d1459-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="d1459-120">Find-Package ein Fehler auftritt, anzeigen, aber funktioniert für Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="d1459-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="d1459-121">Fehler bei "Install-Package jquery.validation" auf dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="d1459-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="d1459-122">Bei der installierten Visual Studio 2015 update 3 für einen im Vergleich, der verwendet NuGet 3.5.0-Versionsfehler tritt auf, - [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="d1459-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="d1459-123">Paket-Manager-Benutzeroberfläche: neue Version nicht angezeigt werden, nach dem Aktualisieren eines Pakets- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="d1459-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="d1459-124">-"Apikey" Befehlszeile für Delete-Befehl nicht Lese-/gesendet 3.5.0-Beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="d1459-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="d1459-125">Falsches Zeichenfolgenformat: eine stabile Version eines Pakets müssen sich nicht auf einer Vorabversion Abhängigkeit.</span><span class="sxs-lookup"><span data-stu-id="d1459-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="d1459-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="d1459-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="d1459-127">Erstellen die PCL (net46 und Windows 10)-Projekt Get NullRef-Ausnahme.</span><span class="sxs-lookup"><span data-stu-id="d1459-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="d1459-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="d1459-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="d1459-129">NuGet-Updates sollten informationsmeldung bereitstellen, wenn eine höhere Version durch Einschränkung der AllowedVersions - eingeschränkt ist [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="d1459-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="d1459-130">Anmeldeinformationen-Plug-in wurde mit Fehler-1 beendet / Fehler beim Herunterladen bei Verwendung der Anmeldeinformationsanbieter mit mehreren Quellen – package [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="d1459-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="d1459-131">NuGet Pack - Paket-Abhängigkeit fehlt "newtonsoft.JSON" - [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="d1459-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="d1459-132">Fehler in ExecuteSynchronizedCore auf Linux/MacOS "+" Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="d1459-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="d1459-133">Visual Studio unterstützt keine Umgebungsvariablen im RepositoryPath (nuget.exe bewirkt) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="d1459-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="d1459-134">Beheben Sie Probleme mit der Barrierefreiheit - [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="d1459-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="d1459-135">Portable-Frameworks mit Bindestrichen Profile werden abgelehnt.</span><span class="sxs-lookup"><span data-stu-id="d1459-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="d1459-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="d1459-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="d1459-137">NuGet-Paket-Manager sollten diese Optionsliste in Paketen zu verdeutlichen, Detail nicht für gilt, `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="d1459-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="d1459-138">NuGet 3.3.0-Aktualisierung ein Fehler auftritt, mit "... eine zusätzliche Einschränkung definiert" Packages.config "wird verhindert, dass dieser Vorgang."</span><span class="sxs-lookup"><span data-stu-id="d1459-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="d1459-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="d1459-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="d1459-140">Installieren des Pakets aus einer lokalen Quelle, die nicht vorhanden ist löst einer gefälschten Nachricht - [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="d1459-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="d1459-141">Filter für "Verfügbare Upgrade" zeigt, Upgrades, bei denen die versionseinschränkung - verletzen [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="d1459-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="d1459-142">Leistungsverbesserungen</span><span class="sxs-lookup"><span data-stu-id="d1459-142">Performance Improvements</span></span>

* <span data-ttu-id="d1459-143">: Leistungsverbesserung "ContentModel" Target Framework Analyse - [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="d1459-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="d1459-144">Leistung: Vermeiden Sie lesen `runtime.json` Dateien für Wiederherstellungen, denen keine RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="d1459-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="d1459-145">Auf CI-Computern Wiederherstellen eines Beispiels, die ASP.NET Web-Anwendung von 15 Sekunden auf 3 Sekunden reduziert.</span><span class="sxs-lookup"><span data-stu-id="d1459-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="d1459-146">Leistung: Paket-Manager-Konsole init.ps1 Ladezeit [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="d1459-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="d1459-147">Zeit in Anspruch PackageManagerConsole verbessert in einigen Fällen von 132s 10 Sekunden.</span><span class="sxs-lookup"><span data-stu-id="d1459-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="d1459-148">Lösen von Leistungsproblemen von ReSharper in NuGet-Update - [#3044](https://github.com/NuGet/Home/issues/3044): für ein Beispielprojekt Zeit zum Installieren von Paketen von 140s auf reduziert 68s.</span><span class="sxs-lookup"><span data-stu-id="d1459-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="d1459-149">DCRs</span><span class="sxs-lookup"><span data-stu-id="d1459-149">DCRs</span></span>

* <span data-ttu-id="d1459-150">NuGet muss, damit Benutzer wissen, dass in einem Dotnet Tfm-basierte aktualisieren bzw. installieren PCL-Fehlern – verursachen [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="d1459-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="d1459-151">Ungültige installieren/aktualisieren für Projekt mit Tfm warnen = "Dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="d1459-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="d1459-152">Hinzufügen von Unterstützung für netcoreapp11 und netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="d1459-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="d1459-153">NuGet-Warning-Header Inhalte an die Konsole in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="d1459-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="d1459-154">AssemblyMetadata-Attribut für nutzen `.nuspec` Ersetzungen - token [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="d1459-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="d1459-155">Entfernen Sie die gesperrte Eigenschaft aus der Sperrdatei - [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="d1459-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="d1459-156">Symbolpakete sollte nicht immer in Installation, die verwendet werden, oder Aktualisieren von #2807</span><span class="sxs-lookup"><span data-stu-id="d1459-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="d1459-157">Features</span><span class="sxs-lookup"><span data-stu-id="d1459-157">Features</span></span>

* <span data-ttu-id="d1459-158">Unterstützung für den fallback-Paket-Ordner - [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="d1459-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="d1459-159">Entwerfen und implementieren Sie eine Vorstellung von Pakettyp Tool Pakete, unterstützen [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="d1459-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="d1459-160">-API, um den Pfad zu dem Ordner mit globalen Paketen - abzurufen [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="d1459-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="d1459-161">Native Pakete update-Support - [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="d1459-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
