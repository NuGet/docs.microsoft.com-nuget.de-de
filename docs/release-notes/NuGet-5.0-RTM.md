---
title: Anmerkungen zu NuGet 5.0 RTM
description: Anmerkungen zu NuGet-5.0, einschließlich bekannter Probleme, Fehlerbehebungen, neuen Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 7e719a3bb5069c461820c6f884487af1eb04bf86
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610661"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="3d6a1-103">Anmerkungen zu NuGet 5.0</span><span class="sxs-lookup"><span data-stu-id="3d6a1-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="3d6a1-104">Möglichkeiten der NuGet-Verteilung:</span><span class="sxs-lookup"><span data-stu-id="3d6a1-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="3d6a1-105">NuGet-Version</span><span class="sxs-lookup"><span data-stu-id="3d6a1-105">NuGet version</span></span> | <span data-ttu-id="3d6a1-106">Verfügbar in der Visual Studio-Version</span><span class="sxs-lookup"><span data-stu-id="3d6a1-106">Available in Visual Studio version</span></span>| <span data-ttu-id="3d6a1-107">Verfügbar in .NET SDK(s)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="3d6a1-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="3d6a1-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="3d6a1-109">Visual Studio 2019 Version 16.0</span><span class="sxs-lookup"><span data-stu-id="3d6a1-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="3d6a1-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="3d6a1-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="3d6a1-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="3d6a1-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="3d6a1-112">Visual Studio 2019 version 16.0.4</span><span class="sxs-lookup"><span data-stu-id="3d6a1-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="3d6a1-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="3d6a1-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="3d6a1-114"><sup>1</sup>mit Visual Studio-2019 mit .NET Core-Workload installiert</span><span class="sxs-lookup"><span data-stu-id="3d6a1-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="3d6a1-115"><sup>2</sup>verfügbar als optionale Installation mit Visual Studio-2019 mit .NET Core-Workload</span><span class="sxs-lookup"><span data-stu-id="3d6a1-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="3d6a1-116">Zusammenfassung: Neuerungen in 5.0</span><span class="sxs-lookup"><span data-stu-id="3d6a1-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="3d6a1-117">Unterstützung für die Wiederherstellung [gefiltert Lösungen](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio-2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-117">Support for restoring [filtered solutions](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="3d6a1-118">`BuildTransitive` Ordner kann Pakete transitiv targets-und Props zum Hostprojekt mitwirken [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="3d6a1-119">Bessere Unterstützung für PackageReference-Szenarien in NuGet IVs-APIs – [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="3d6a1-120">`nuget.exe pack project.json` veraltet - [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="3d6a1-121">Gen 1-Anmeldeinformationsanbieter-Plug-in wurde ersetzt durch [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) und wird in Kürze veraltet sein – [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3d6a1-122">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="3d6a1-122">Issues fixed in this release</span></span>

<span data-ttu-id="3d6a1-123">**Fehler**</span><span class="sxs-lookup"><span data-stu-id="3d6a1-123">**Bugs**</span></span>

* <span data-ttu-id="3d6a1-124">Wenn eine NoOp-Wiederherstellung durchführen zu können, sollten Sie vermeiden \*. dgspec.json schreiben im Verzeichnis "Obj" - [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="3d6a1-125">Berechtigungen für Dateien, die in ~/.nuget erstellt werden, zu open - [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="3d6a1-126">`dotnet list package --outdated` funktioniert nicht mit Datenquellen, die Authentifizierung – [#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="3d6a1-127">NuGet.VisualStudio.IVsPackageInstaller - Aufruf in einem Projekt mit kein Paket verweist immer auf "Packages.config" verwendet, auch wenn der Standardwert festgelegt ist, zu "packagereference" - [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="3d6a1-128">PMC: Update-Paket installieren schlägt fehl ("kann nicht gefunden") für die Pakete aus der Liste entfernen.</span><span class="sxs-lookup"><span data-stu-id="3d6a1-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="3d6a1-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="3d6a1-130">Fügen Sie in unserem Repository und die VSIX - Hinweis zu Drittanbietern [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="3d6a1-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage sollten die neueste Version, wenn keine Version angegeben – installieren [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="3d6a1-132">– Interaktive Unterstützung für Dotnet Nuget Push - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="3d6a1-133">Wenn Sie mit der Datei wiederherstellen, sollte nicht NU1603 Warnung ausgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="3d6a1-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="3d6a1-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="3d6a1-135">NuGet sollten Projektpfad nicht drucken, während der Wiederherstellung mit minimaler Protokollierung - [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="3d6a1-136">– Interaktive Unterstützung für Dotnet-remove Paket - [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="3d6a1-137">Hinzufügen NuGet.Packaging.Core mit TypeForwardedTo Attrs - später wieder [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="3d6a1-138">Plugins_cache benötigt kürzerer Pfad für eine gute - Lösung [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="3d6a1-139">Pfad für die Ermittlung von Msbuild bevorzugen, wenn Benutzer bestimmte Msbuild-Version - anfordern nicht [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="3d6a1-140">`nuget.exe /?` tragen Sie richtige Msbuild-Versionen – [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="3d6a1-141">NuGet.targets(498,5): error : Einen Teil des Pfads konnte nicht gefunden "/ Tmp/NuGetScratch - unter Mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="3d6a1-142">Wiederherstellung listet unnötigerweise den Inhalt von allen Versionen von Referenziertes Paket im Cache Machine - [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="3d6a1-143">Automatische Erkennung von MSBuild wählt immer 16.0, nach der Installation von Visual Studio 2019 Vorschau - [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="3d6a1-144">Dotnet-umgebungsaufgabenlisten-Paket für eine Lösung gibt doppelte Einträge für Framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="3d6a1-145">Ausnahme "ein leerer Pfad ist nicht zulässig." beim aufrufenden IVsPackageInstaller.InstallPackage auf dem alten Projekte und-Pakete Ordner ist nicht vorhanden.</span><span class="sxs-lookup"><span data-stu-id="3d6a1-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="3d6a1-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="3d6a1-147">MSBuild/t: Restore Ausführlichkeitsgrad muss funktionalitätsanforderungen - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="3d6a1-148">Visual Studio 16.0 NuGet UI enthält unlesbare Registerkarten aufgrund von Problemen mit Farbe - [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="3d6a1-149">NuGet.Core & NuGet.Clients Dateien "License.txt" Klarstellung - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="3d6a1-150">Wiederherstellung listet globalen Paketordner unnötigerweise beim Versuch, um zu bestimmen, Typ: [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="3d6a1-151">Fehler von der Erzwingung der Sperre-Datei sollte angezeigt werden in der Fehlerliste (Fenster) - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="3d6a1-152">Beheben von Problemen mit NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="3d6a1-153">Aktualisieren die Installation von MSBuild anpassen Ort – [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="3d6a1-154">NuGet.Build.Tasks.Pack muss eine entwicklungsabhängigkeit - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="3d6a1-155">Hinzufügen von Pack Erweiterungspunkt zum Einschließen von Debugsymbole - [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="3d6a1-156">`dotnet pack` Abhängigkeit Versionsbereich in erstellte NuGet-Paket (auch, wenn die unverankerte Version verwendet wird) - beibehalten soll [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="3d6a1-157">`dotnet restore` nicht authentifizierte Quelle bei der Benutzerebene Config-Quelle – auch verfügt über [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="3d6a1-158">Pack sollten nicht nur BuildActions für Inhaltsdateien - [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="3d6a1-159">Verwenden eine "ProjectReference" AssetTargetFallback erfolgreich ausgeführt werden müssen, sollte eine Warnung ausgeben.</span><span class="sxs-lookup"><span data-stu-id="3d6a1-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="3d6a1-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="3d6a1-161">Deadlock aufgrund von Threadingprobleme beim Aufrufen von in CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="3d6a1-162">`dotnet add package` Verwenden Sie nicht für eine Datenquelle angegeben, in der lokalen Konfiguration - Anmeldeinformationen aus der globalen Konfiguration [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="3d6a1-163">Threadingprobleme mit MEF, die aufgerufen wird, auf die asynchrone Codepfade - [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="3d6a1-164">Anmeldung: Fehler zweimal und ohne Aufrufliste - [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="3d6a1-165">Installieren eines signierten Pakets mit nicht vertrauenswürdigen Signaturzertifikat sollte angezeigt werden Fehler: [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="3d6a1-166">NuGet restore noops sind nicht ordnungsgemäß, beim Verzeichnis "Obj" - 2-Projekten gemeinsam [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="3d6a1-167">Können keine PAT mit `dotnet restore` unter Linux mit Paketen aus authentifizierte Feeds - [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="3d6a1-168">Dotnet-Restore versagt, wenn deaktivierte auf den gesamten Computer feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="3d6a1-169">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="3d6a1-169">**DCRs**</span></span>

* <span data-ttu-id="3d6a1-170">Warnhinweis anzeigen, über zukünftige Entfernen von "Dotnet Pack Datei"Project.JSON"" - [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="3d6a1-171">Fügen Sie eine Warnung zu veralteten Gen1-Anmeldeinformationen-Plug-in - [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="3d6a1-172">Signierung: Aktivierte Repository zum Erzwingen einer Client-Überprüfung von jedem Paket als Repository signiert--über RepositorySignatures/5.0.0-Ressource - [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="3d6a1-173">Beschränken der Anzahl von HTTP-Anforderung pro Datenquelle über die Datei "NuGet.config" - [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="3d6a1-174">NuGet sollten Net472 (um die Bereinigung der 16,0 Build des VSIX-Hilfe) - Ziel [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="3d6a1-175">PMC: Entfernen Sie OpenPackagePage-Befehl – [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="3d6a1-176">Stellen NetCoreApp 3.0-Karte, um NetStandard 2.1 – [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="3d6a1-177">Pakete, NuGet.\* netstandard2.0-Unterstützung hinzufügen [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="3d6a1-178">Paketersteller, die zum Definieren von Ressourcen transitive Buildverhalten - ermöglichen [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="3d6a1-179">Visual Studio 2019 Lösungsfilter-Funktion unterstützt.</span><span class="sxs-lookup"><span data-stu-id="3d6a1-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="3d6a1-180">Unterstützt auch das Projekt nicht in der Projektmappe oder entladene Projekte.</span><span class="sxs-lookup"><span data-stu-id="3d6a1-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="3d6a1-181">Vollständige Lösung (per CLI oder Visual Studio) zuerst - wiederherstellen müssen [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="3d6a1-182">NuGet-5.0-Assemblys in .NET 4.7.2 (über die Änderung der TFM) - erfordern [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="3d6a1-183">NuGetLicenseData aus NuGet.Packaging sollte ein öffentlicher Typ sein.</span><span class="sxs-lookup"><span data-stu-id="3d6a1-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="3d6a1-184">Aktualisieren Sie die Lizenzmetadaten aus Spdx erfasst.</span><span class="sxs-lookup"><span data-stu-id="3d6a1-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="3d6a1-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="3d6a1-186">Entfernen Sie veraltete APIs für Einstellungen – [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="3d6a1-187">Problemumgehung Wiederherstellung Timeouts auf Systemen mit 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="3d6a1-188">NuGet NTLM-Authentifizierung bevorzugt, auch wenn die Anmeldeinformationen vorhanden sind, in der Datei "NuGet.config" – Filter-Auth-Typen zur Eingabe von Anmeldeinformationen - Option "Config" hinzufügen [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="3d6a1-189">Aktivieren Sie EmbedInteropTypes für "packagereference" (übereinstimmende Datei "Packages.config"-Funktion) - [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="3d6a1-190">**[Liste aller in diesem Release - 5.0 RTM behobene Probleme](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="3d6a1-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="3d6a1-191">Zusammenfassung: Neuerungen in 5.0.2</span><span class="sxs-lookup"><span data-stu-id="3d6a1-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="3d6a1-192">Sicherheit (über dotnet.exe "oder" mono.exe Ausführungszeit): der Ordner "Obj" sollten erstellt werden, mit den richtigen Berechtigungen [#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="3d6a1-193">NuGet.exe-Wiederherstellung unter Mono/MacOS ein Fehler auftritt, mit der benutzerdefinierten Datei "NuGet.config" und `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="3d6a1-194">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="3d6a1-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="3d6a1-195">Von .NET Core SDK in FallbackFolders installierte Pakete werden benutzerdefiniert installiert und bestehen die Signaturüberprüfung nicht.</span><span class="sxs-lookup"><span data-stu-id="3d6a1-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="3d6a1-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="3d6a1-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="3d6a1-197">Problem</span><span class="sxs-lookup"><span data-stu-id="3d6a1-197">Issue</span></span>
<span data-ttu-id="3d6a1-198">Bei Verwendung von dotnet.exe 2.x zum Wiederherstellen eines Projekts mit mehreren Zielen netcoreapp 1.x und netcoreapp 2.x wird der Fallbackordner als Dateifeed behandelt.</span><span class="sxs-lookup"><span data-stu-id="3d6a1-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="3d6a1-199">Dies bedeutet, dass NuGet bei der Wiederherstellung das Paket aus dem Fallbackordner auswählt und versucht, es im globalen Paketordner zu installieren, und die übliche Signaturüberprüfung durchführt, bei der ein Fehler auftritt.</span><span class="sxs-lookup"><span data-stu-id="3d6a1-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="3d6a1-200">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="3d6a1-200">Workaround</span></span>
<span data-ttu-id="3d6a1-201">Deaktivieren Sie die Verwendung des Ordners fallback durch Festlegen der `RestoreAdditionalProjectSources` auf nichts verweist:</span><span class="sxs-lookup"><span data-stu-id="3d6a1-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="3d6a1-202">Verwenden Sie dies mit Vorsicht, da Pakete, die aus dem fallback Ordner wiederhergestellt werden soll nun aus "NuGet.org" heruntergeladen werden.</span><span class="sxs-lookup"><span data-stu-id="3d6a1-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>
