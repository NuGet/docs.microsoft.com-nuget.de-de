---
title: Anmerkungen zu NuGet 5.0-preview
description: Anmerkungen zu NuGet-5.0-Preview, einschließlich bekannter Probleme, Fehlerbehebungen, neuen Features und DCRs.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 4b05dcb9a2960c1e3231e81d4b4c122d3a518753
ms.sourcegitcommit: 571644118e3c5a2fd818891d305b4b8de8ef21de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2019
ms.locfileid: "57225887"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="210ec-103">Anmerkungen zu NuGet 5.0 Preview</span><span class="sxs-lookup"><span data-stu-id="210ec-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="210ec-104">NuGet-5.0 Preview-Versionen</span><span class="sxs-lookup"><span data-stu-id="210ec-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="210ec-105">27 Februar 2019 - [NuGet 5.0 Preview 4](#whats-new-in-nuget-50-preview-4)</span><span class="sxs-lookup"><span data-stu-id="210ec-105">February 27, 2019 - [NuGet 5.0 Preview 4](#whats-new-in-nuget-50-preview-4)</span></span>
* <span data-ttu-id="210ec-106">13 Februar 2019 - [NuGet 5.0 Preview 3](#whats-new-in-nuget-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="210ec-106">February 13, 2019 - [NuGet 5.0 Preview 3](#whats-new-in-nuget-50-preview-3)</span></span>
* <span data-ttu-id="210ec-107">23 Januar 2019 - [NuGet 5.0 Preview 2](#whats-new-in-nuget-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="210ec-107">January 23, 2019 - [NuGet 5.0 Preview 2](#whats-new-in-nuget-50-preview-2)</span></span>

## <a name="whats-new-in-nuget-50-preview-4"></a><span data-ttu-id="210ec-108">Neuerungen in NuGet 5.0 Preview 4</span><span class="sxs-lookup"><span data-stu-id="210ec-108">What's New in NuGet 5.0 Preview 4</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="210ec-109">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="210ec-109">Issues fixed in this release</span></span>

<span data-ttu-id="210ec-110">**Fehler**</span><span class="sxs-lookup"><span data-stu-id="210ec-110">**Bugs**</span></span>

* <span data-ttu-id="210ec-111">NuGet.VisualStudio.IVsPackageInstaller - Aufruf in einem Projekt mit kein Paket verweist immer auf "Packages.config" verwendet, auch wenn der Standardwert festgelegt ist, zu "packagereference" - [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="210ec-111">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="210ec-112">PMC: Update-Paket installieren schlägt fehl ("kann nicht gefunden") für die Pakete aus der Liste entfernen.</span><span class="sxs-lookup"><span data-stu-id="210ec-112">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="210ec-113"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="210ec-113"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="210ec-114">Fügen Sie in unserem Repository und die VSIX - Hinweis zu Drittanbietern [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="210ec-114">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="210ec-115">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage sollten die neueste Version, wenn keine Version angegeben – installieren [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="210ec-115">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="210ec-116">– Interaktive Unterstützung für Dotnet Nuget Push - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="210ec-116">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="210ec-117">Wenn Sie mit der Datei wiederherstellen, sollte nicht NU1603 Warnung ausgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="210ec-117">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="210ec-118"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="210ec-118"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="210ec-119">NuGet sollten Projektpfad nicht drucken, während der Wiederherstellung mit minimaler Protokollierung - [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="210ec-119">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="210ec-120">– Interaktive Unterstützung für Dotnet-remove Paket - [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="210ec-120">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="210ec-121">Hinzufügen NuGet.Packaging.Core mit TypeForwardedTo Attrs - später wieder [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="210ec-121">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="210ec-122">Plugins_cache benötigt kürzerer Pfad für eine gute - Lösung [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="210ec-122">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="210ec-123">Pfad für die Ermittlung von Msbuild bevorzugen, wenn Benutzer bestimmte Msbuild-Version - anfordern nicht [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="210ec-123">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

<span data-ttu-id="210ec-124">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="210ec-124">**DCRs**</span></span>

* <span data-ttu-id="210ec-125">Beschränken der Anzahl von HTTP-Anforderung pro Datenquelle über die Datei "NuGet.config" - [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="210ec-125">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="210ec-126">NuGet sollten Net472 (um die Bereinigung der 16,0 Build des VSIX-Hilfe) - Ziel [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="210ec-126">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="210ec-127">PMC: Entfernen Sie OpenPackagePage-Befehl – [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="210ec-127">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="210ec-128">Stellen NetCoreApp 3.0-Karte, um NetStandard 2.1 – [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="210ec-128">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="210ec-129">Pakete, NuGet.\* netstandard2.0-Unterstützung hinzufügen [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="210ec-129">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>


## <a name="whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="210ec-130">Neuerungen in NuGet 5.0 Preview 3</span><span class="sxs-lookup"><span data-stu-id="210ec-130">What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="210ec-131">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="210ec-131">Issues fixed in this release</span></span> 

<span data-ttu-id="210ec-132">**Fehler**</span><span class="sxs-lookup"><span data-stu-id="210ec-132">**Bugs**</span></span>

* <span data-ttu-id="210ec-133">nuget.exe /?</span><span class="sxs-lookup"><span data-stu-id="210ec-133">nuget.exe /?</span></span> <span data-ttu-id="210ec-134">tragen Sie richtige Msbuild-Versionen – [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="210ec-134">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="210ec-135">NuGet.targets(498,5): error : Einen Teil des Pfads konnte nicht gefunden "/ Tmp/NuGetScratch - unter Mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="210ec-135">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="210ec-136">Wiederherstellung listet unnötigerweise den Inhalt von allen Versionen von Referenziertes Paket im Cache Machine - [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="210ec-136">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="210ec-137">Automatische Erkennung von MSBuild wählt immer 16.0, nach der Installation von Visual Studio 2019 Vorschau - [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="210ec-137">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="210ec-138">Dotnet-umgebungsaufgabenlisten-Paket für eine Lösung gibt doppelte Einträge für Framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="210ec-138">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="210ec-139">Ausnahme "ein leerer Pfad ist nicht zulässig." beim aufrufenden IVsPackageInstaller.InstallPackage auf dem alten Projekte und-Pakete Ordner ist nicht vorhanden.</span><span class="sxs-lookup"><span data-stu-id="210ec-139">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="210ec-140"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="210ec-140"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="210ec-141">MSBuild/t: Restore Ausführlichkeitsgrad muss funktionalitätsanforderungen - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="210ec-141">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="210ec-142">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="210ec-142">**DCRs**</span></span>

* <span data-ttu-id="210ec-143">Paketersteller, die zum Definieren von Ressourcen transitive Buildverhalten - ermöglichen [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="210ec-143">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="210ec-144">Aktivieren der Wiederherstellung in Visual Studio erfolgreich, wenn ein Projekt nicht Teil der Lösung ist oder wurde nicht geladen, aber es bereits wiederhergestellt wurde - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="210ec-144">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="whats-new-in-nuget-50-preview-2"></a><span data-ttu-id="210ec-145">Neuerungen in NuGet 5.0 Preview 2</span><span class="sxs-lookup"><span data-stu-id="210ec-145">What's New in NuGet 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="210ec-146">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="210ec-146">Issues fixed in this release</span></span>

<span data-ttu-id="210ec-147">**Fehler**</span><span class="sxs-lookup"><span data-stu-id="210ec-147">**Bugs**</span></span>

* <span data-ttu-id="210ec-148">Visual Studio 16.0 NuGet UI enthält unlesbare Registerkarten aufgrund von Problemen mit Farbe - [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="210ec-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="210ec-149">NuGet.Core & NuGet.Clients Dateien "License.txt" Klarstellung - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="210ec-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="210ec-150">Wiederherstellung listet globalen Paketordner unnötigerweise beim Versuch, um zu bestimmen, Typ: [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="210ec-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="210ec-151">Fehler von der Erzwingung der Sperre-Datei sollte angezeigt werden in der Fehlerliste (Fenster) - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="210ec-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="210ec-152">Beheben von Problemen mit NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="210ec-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="210ec-153">Anpassung an MSBuild aktualisieren sie den Installationsort.</span><span class="sxs-lookup"><span data-stu-id="210ec-153">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="210ec-154">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="210ec-154">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="210ec-155">NuGet.Build.Tasks.Pack muss eine entwicklungsabhängigkeit - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="210ec-155">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="210ec-156">Hinzufügen von Pack Erweiterungspunkt zum Einschließen von Debugsymbole - [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="210ec-156">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="210ec-157">Dotnet-Pack beibehalten soll Abhängigkeit Versionsbereich in NuGet-Paket erstellt.</span><span class="sxs-lookup"><span data-stu-id="210ec-157">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="210ec-158">(auch, wenn die unverankerte Version verwendet wird) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="210ec-158">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="210ec-159">Dotnet-Restore auf authentifizierte Quelle schlägt fehl, wenn es sich bei auf Benutzerebene Konfiguration auch-Quelle – hat [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="210ec-159">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="210ec-160">Pack sollten nicht nur BuildActions für Inhaltsdateien - [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="210ec-160">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="210ec-161">Verwenden eine "ProjectReference" AssetTargetFallback erfolgreich ausgeführt werden müssen, sollte eine Warnung ausgeben.</span><span class="sxs-lookup"><span data-stu-id="210ec-161">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="210ec-162"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="210ec-162"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="210ec-163">Deadlock aufgrund von Threadingprobleme beim Aufrufen von in CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="210ec-163">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="210ec-164">Dotnet add-Paket nicht die Anmeldeinformationen aus der globalen Konfiguration verwendet, für eine Datenquelle angegeben, in der lokalen Konfiguration - [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="210ec-164">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="210ec-165">Probleme mit MEF wird Threading für asynchrone Codepfade - aufgerufen [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="210ec-165">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="210ec-166">Anmeldung: Fehler zweimal und ohne Aufrufliste - [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="210ec-166">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="210ec-167">Installieren eines signierten Pakets mit nicht vertrauenswürdigen Signaturzertifikat sollte angezeigt werden Fehler: [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="210ec-167">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="210ec-168">NuGet restore noops sind nicht ordnungsgemäß, beim Verzeichnis "Obj" - 2-Projekten gemeinsam [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="210ec-168">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="210ec-169">PAT mit Dotnet-Restore unter Linux von Paketen aus authentifizierte Feeds - können keine [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="210ec-169">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="210ec-170">Dotnet-Restore versagt, wenn deaktivierte auf den gesamten Computer feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="210ec-170">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="210ec-171">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="210ec-171">**DCRs**</span></span>

* <span data-ttu-id="210ec-172">NuGet-5.0-Assemblys in .NET 4.7.2 (über die Änderung der TFM) - erfordern [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="210ec-172">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="210ec-173">NuGetLicenseData aus NuGet.Packaging sollte ein öffentlicher Typ sein.</span><span class="sxs-lookup"><span data-stu-id="210ec-173">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="210ec-174">Aktualisieren Sie die Lizenzmetadaten aus Spdx erfasst.</span><span class="sxs-lookup"><span data-stu-id="210ec-174">Update license metadata ingested from spdx.</span></span><span data-ttu-id="210ec-175"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="210ec-175"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="210ec-176">Entfernen Sie veraltete APIs für Einstellungen – [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="210ec-176">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="210ec-177">Problemumgehung Wiederherstellung Timeouts auf Systemen mit 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="210ec-177">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="210ec-178">NuGet NTLM-Authentifizierung bevorzugt, auch wenn die Anmeldeinformationen vorhanden sind, in der Datei "NuGet.config" – Filter-Auth-Typen zur Eingabe von Anmeldeinformationen - Option "Config" hinzufügen [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="210ec-178">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="210ec-179">Aktivieren Sie EmbedInteropTypes für "packagereference" (übereinstimmende Datei "Packages.config"-Funktion) - [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="210ec-179">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="210ec-180">Liste aller Probleme, die in dieser Version 5.0.0-preview2 behoben</span><span class="sxs-lookup"><span data-stu-id="210ec-180">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="210ec-181">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="210ec-181">Known issues</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="210ec-182">Von .NET Core SDK in FallbackFolders installierte Pakete werden benutzerdefiniert installiert und bestehen die Signaturüberprüfung nicht.</span><span class="sxs-lookup"><span data-stu-id="210ec-182">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="210ec-183"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="210ec-183"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="210ec-184">**Problem** bei Verwendung des dotnet.exe 2.x auf ein Projekt, mit mehreren Zielen Netcoreapp wiederherstellen 1.x und Netcoreapp 2.x, alternative Ordner so behandelt, als eine Datei mit dem feed.</span><span class="sxs-lookup"><span data-stu-id="210ec-184">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="210ec-185">Dies bedeutet, dass NuGet bei der Wiederherstellung das Paket aus dem Fallbackordner auswählt und versucht, es im globalen Paketordner zu installieren, und die übliche Signaturüberprüfung durchführt, bei der ein Fehler auftritt.</span><span class="sxs-lookup"><span data-stu-id="210ec-185">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="210ec-186">**Problemumgehung** deaktivieren Sie die Verwendung des Ordners fallback durch Festlegen der `RestoreAdditionalProjectSources` auf nichts verweist.</span><span class="sxs-lookup"><span data-stu-id="210ec-186">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="210ec-187">`<RestoreAdditionalProjectSources/>` Verwenden Sie dies mit Vorsicht, da es bewirkt, dass viele Pakete von NuGet.org heruntergeladen werden, die andernfalls aus dem Fallbackordner wiederhergestellt würden.</span><span class="sxs-lookup"><span data-stu-id="210ec-187">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
