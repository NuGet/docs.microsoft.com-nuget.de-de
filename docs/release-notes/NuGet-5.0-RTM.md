---
title: Versionshinweise zu NuGet 5.0 RTM
description: Versionshinweise für NuGet 5.0, einschließlich bekannter Probleme, Fehlerbehebungen, neuer Features und DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 19173d2be7cd66b65651655385466b40f5e08352
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901745"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="27b71-103">Versionshinweise zu NuGet 5.0</span><span class="sxs-lookup"><span data-stu-id="27b71-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="27b71-104">Möglichkeiten der NuGet-Verteilung:</span><span class="sxs-lookup"><span data-stu-id="27b71-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="27b71-105">NuGet-Version</span><span class="sxs-lookup"><span data-stu-id="27b71-105">NuGet version</span></span> | <span data-ttu-id="27b71-106">Verfügbar in der Visual Studio-Version</span><span class="sxs-lookup"><span data-stu-id="27b71-106">Available in Visual Studio version</span></span>| <span data-ttu-id="27b71-107">Verfügbar in .NET SDK(s)</span><span class="sxs-lookup"><span data-stu-id="27b71-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="27b71-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="27b71-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="27b71-109">Visual Studio 2019, Version 16.0</span><span class="sxs-lookup"><span data-stu-id="27b71-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="27b71-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="27b71-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="27b71-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="27b71-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="27b71-112">Visual Studio 2019, Version 16.0.4</span><span class="sxs-lookup"><span data-stu-id="27b71-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="27b71-113">[2.1.60x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1,</sup> [2.2.20x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="27b71-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="27b71-114"><sup>1</sup> Installation mit Visual Studio 2019 mit .NET Core-Workload</span><span class="sxs-lookup"><span data-stu-id="27b71-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="27b71-115"><sup>2</sup> Verfügbar als optionale Installation mit Visual Studio 2019 mit .NET Core-Workload</span><span class="sxs-lookup"><span data-stu-id="27b71-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="27b71-116">Zusammenfassung: Neues in Version 5.0</span><span class="sxs-lookup"><span data-stu-id="27b71-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="27b71-117">Unterstützung für die [Wiederherstellung gefilterter Lösungen](/visualstudio/ide/filtered-solutions) in Visual Studio 2019 – [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="27b71-117">Support for restoring [filtered solutions](/visualstudio/ide/filtered-solutions) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="27b71-118">`BuildTransitive` -Ordner ermöglicht Paketen das transitive Beitragen von Zielen/Props zum Hostprojekt [– #6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="27b71-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="27b71-119">Bessere Unterstützung für PackageReference-Szenarien in NuGet-IVs-APIs [– #7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="27b71-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="27b71-120">`nuget.exe pack project.json` ist veraltet – [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="27b71-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="27b71-121">Gen 1 Anmeldeinformationsanbieter-Plug-In wurde durch [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) ersetzt und wird bald veraltet sein [– #7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="27b71-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="27b71-122">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="27b71-122">Issues fixed in this release</span></span>

<span data-ttu-id="27b71-123">**Fehler**</span><span class="sxs-lookup"><span data-stu-id="27b71-123">**Bugs**</span></span>

* <span data-ttu-id="27b71-124">Vermeiden Sie bei einer NoOp-Wiederherstellung \*.dgspec.jsbeim Schreiben in das obj-Verzeichnis – [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="27b71-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="27b71-125">Berechtigungen für Dateien, die in ~/.nuget erstellt wurden, sind zu [offen – #7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="27b71-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="27b71-126">`dotnet list package --outdated` funktioniert nicht mit Quellen, die eine Authentifizierung benötigen – [#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="27b71-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="27b71-127">NuGet.VisualStudio.IVsPackageInstaller: Beim Aufrufen von für ein Projekt ohne Paketverweise wird immer packages.config verwendet, auch wenn der Standardwert auf PackageReference [-](https://github.com/NuGet/Home/issues/7005) #7005</span><span class="sxs-lookup"><span data-stu-id="27b71-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="27b71-128">PMC: Update-Package Neuinstallation schlägt bei delisteten Paketen fehl ("Paket konnte nicht gefunden werden").</span><span class="sxs-lookup"><span data-stu-id="27b71-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="27b71-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="27b71-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="27b71-130">Hinzufügen von Drittanbieterhinweisen in unserem Repository und vsix – [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="27b71-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="27b71-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage sollte die neueste Version installieren, wenn keine Version angegeben ist – [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="27b71-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="27b71-132">--interactive-Unterstützung für dotnet nuget push – [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="27b71-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="27b71-133">Beim Wiederherstellen mit einer Sperrdatei sollte keine NU1603-Warnung ausgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="27b71-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="27b71-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="27b71-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="27b71-135">NuGet sollte während der Wiederherstellung keinen Projektpfad mit minimaler Protokollierung drucken [– #7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="27b71-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="27b71-136">--interactive-Unterstützung für dotnet remove package – [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="27b71-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="27b71-137">Fügen Sie NuGet.Packaging.Core mit TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="27b71-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="27b71-138">plugins_cache benötigt einen kürzeren Pfad, um gut zu funktionieren [– #7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="27b71-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="27b71-139">Pfad für msbuild-Ermittlung bevorzugen, wenn der Benutzer nicht nach einer bestimmten msbuild-Version gefragt hat [– #7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="27b71-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="27b71-140">`nuget.exe /?` sollte die richtigen msbuild-Versionen [auflisten – #7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="27b71-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="27b71-141">NuGet.targets(498,5): Error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="27b71-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="27b71-142">restore listet unnötigerweise den Inhalt aller Versionen des Pakets, auf das verwiesen wird, im Computercache [auf– #7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="27b71-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="27b71-143">Die automatische MSBuild-Erkennung wählt nach der Installation von VS 2019 Preview immer 16.0 aus [– #7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="27b71-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="27b71-144">dotnet list-Paket für eine Projektmappe gibt doppelte Einträge für Framework aus [– #7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="27b71-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="27b71-145">Ausnahme "Leerer Pfadname ist nicht zulässig", wenn IVsPackageInstaller.InstallPackage in alten Projekten und Paketordnern aufgerufen wird, ist nicht vorhanden.</span><span class="sxs-lookup"><span data-stu-id="27b71-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="27b71-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="27b71-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="27b71-147">msbuild /t:restore minimaler Ausführlichkeit sollte minimaler sein – [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="27b71-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="27b71-148">Die NuGet-Benutzeroberfläche von VS 16.0 verfügt aufgrund von Farbproblemen über nicht lesbare [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="27b71-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="27b71-149">NuGet.Core & NuGet.Clients License.txt – [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="27b71-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="27b71-150">Bei der Wiederherstellung wird unnötigerweise ein globaler Paketordner enumeriert, um den Typ zu bestimmen [– #7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="27b71-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="27b71-151">Fehler bei der Erzwingung von Sperrdatei sollten im Fenster "Fehlerliste" angezeigt werden [– #7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="27b71-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="27b71-152">Beheben NuGet.ConfigUrationsprobleme [– #7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="27b71-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="27b71-153">Anpassen an MSBuild, indem der Installationsspeicherort aktualisiert [wird – #7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="27b71-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="27b71-154">NuGet.Build.Tasks.Pack sollte eine Entwicklungsabhängigkeit sein – [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="27b71-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="27b71-155">Hinzufügen eines Paketerweiterungspunkts zum Hinzufügen von [Debugsymbolen – #7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="27b71-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="27b71-156">`dotnet pack` sollte den Abhängigkeitsversionsbereich im erstellten nupkg beibehalten (auch wenn eine unverankerte Version [verwendet wird): #7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="27b71-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="27b71-157">`dotnet restore` schlägt bei der authentifizierten Quelle fehl, wenn die Konfiguration auf Benutzerebene auch die Quelle [-#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="27b71-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="27b71-158">Pack sollte den Satz von BuildActions für Inhaltsdateien nicht einschränken – [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="27b71-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="27b71-159">Die Verwendung eines ProjectReference-Werts, für den AssetTargetFallback erfolgreich sein muss, sollte warnen.</span><span class="sxs-lookup"><span data-stu-id="27b71-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="27b71-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="27b71-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="27b71-161">Deadlock aufgrund von Threadingproblemen beim Aufrufen von CPS (CommonProjectSystem) [– #7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="27b71-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="27b71-162">`dotnet add package` verwendet keine Anmeldeinformationen aus der globalen Konfiguration für eine quelle, die in der lokalen Konfiguration angegeben [ist – #6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="27b71-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="27b71-163">Threadingprobleme beim Aufrufen von MEF für asynchrone Codepfade – [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="27b71-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="27b71-164">Signierung: Fehler zweimal und ohne Aufrufliste gemeldet [– #6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="27b71-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="27b71-165">Beim Installieren eines signierten Pakets mit einem nicht vertrauenswürdigen Signaturzertifikat sollte ein Fehler angezeigt [werden: #6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="27b71-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="27b71-166">NuGet stellt NoOps nicht ordnungsgemäß wieder auf, wenn zwei Projekte obj-Verzeichnis [gemeinsam nutzen – #6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="27b71-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="27b71-167">PAT kann nicht mit `dotnet restore` unter Linux mit Paketen aus authentifizierten Feeds verwendet werden [– #5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="27b71-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="27b71-168">dotnet restore schlägt aufgrund eines deaktivierten computerweiten Feeds fehl – [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="27b71-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="27b71-169">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="27b71-169">**DCRs**</span></span>

* <span data-ttu-id="27b71-170">Warnung vor zukünftigem Entfernen von "dotnet pack project.json" [– #7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="27b71-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="27b71-171">Hinzufügen einer Veraltungswarnung für das Gen1-Anmeldeinformations-Plug-In [– #7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="27b71-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="27b71-172">Signierung: Aktiviertes Repository, um die Clientüberprüfung jedes Pakets als Repository zu erfordern, das signiert ist – über die Ressource RepositorySignatures/5.0.0 – [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="27b71-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="27b71-173">Beschränken der HTTP-Anforderungsnummer pro Quelle über NuGet.Config [– #4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="27b71-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="27b71-174">NuGet sollte auf Net472 ausgerichtet sein (um den 16.0-Build der VSIX zu bereinigen) – [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="27b71-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="27b71-175">PMC: OpenPackagePage-Befehl entfernen [– #7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="27b71-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="27b71-176">Zuordnen von NetCoreApp 3.0 zu NetStandard 2.1 [– #7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="27b71-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="27b71-177">Hinzufügen von netstandard2.0-Unterstützung zu NuGet.\*-Paketen [– #6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="27b71-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="27b71-178">Zulassen, dass Paketautoren transitives Verhalten für Buildressourcen definieren – [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="27b71-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="27b71-179">Unterstützung des Features "VS 2019-Lösungsfilter".</span><span class="sxs-lookup"><span data-stu-id="27b71-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="27b71-180">Unterstützt auch Projekte, die nicht in projektmappen oder entladenen Projekten verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="27b71-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="27b71-181">Erste Wiederherstellung der vollständigen Lösung (über CLI oder VS) [– #5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="27b71-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="27b71-182">NuGet 5.0-Assemblys erfordern .NET 4.7.2 (über TFM-Änderung) [– #7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="27b71-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="27b71-183">NuGetLicenseData von NuGet.Packaging sollte ein öffentlicher Typ sein.</span><span class="sxs-lookup"><span data-stu-id="27b71-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="27b71-184">Aktualisieren sie die lizenzmetadaten, die von der -Datei erfasst wurden.</span><span class="sxs-lookup"><span data-stu-id="27b71-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="27b71-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="27b71-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="27b71-186">Veraltete Einstellungs-APIs entfernen – [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="27b71-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="27b71-187">Problemumgehung für Wiederherstellungstimeouts auf Systemen mit 1 CPU [– #6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="27b71-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="27b71-188">NuGet bevorzugt die NTLM-Authentifizierung, auch wenn anmeldeinformationen in NuGet.config vorhanden sind– Option "Konfiguration hinzufügen" zum Filtern von Authentifizierungstypen nach Anmeldeinformationen – [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="27b71-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="27b71-189">Aktivieren von EmbedInteropTypes für PackageReference (Packages.Config-Funktion) – [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="27b71-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="27b71-190">**[Liste aller in diesem Release behobenen Probleme: 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="27b71-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="27b71-191">Zusammenfassung: Neues in Version 5.0.2</span><span class="sxs-lookup"><span data-stu-id="27b71-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="27b71-192">Sicherheit (bei Ausführung über dotnet.exe oder mono.exe): Der Ordner obj sollte mit [](https://github.com/NuGet/Home/issues/7908) den richtigen Berechtigungen #7908</span><span class="sxs-lookup"><span data-stu-id="27b71-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="27b71-193">nuget.exe wiederherzustellen unter mono/macOS schlägt mit benutzerdefinierten nuget.config `PackageSignatureValidity: False` [](https://github.com/NuGet/Home/issues/8011) und #8011</span><span class="sxs-lookup"><span data-stu-id="27b71-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="27b71-194">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="27b71-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="27b71-195">Von .NET Core SDK in FallbackFolders installierte Pakete werden benutzerdefiniert installiert und bestehen die Signaturüberprüfung nicht.</span><span class="sxs-lookup"><span data-stu-id="27b71-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="27b71-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="27b71-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="27b71-197">Problem</span><span class="sxs-lookup"><span data-stu-id="27b71-197">Issue</span></span>
<span data-ttu-id="27b71-198">Bei Verwendung von dotnet.exe 2.x zum Wiederherstellen eines Projekts mit mehreren Zielen netcoreapp 1.x und netcoreapp 2.x wird der Fallbackordner als Dateifeed behandelt.</span><span class="sxs-lookup"><span data-stu-id="27b71-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="27b71-199">Dies bedeutet, dass NuGet bei der Wiederherstellung das Paket aus dem Fallbackordner auswählt und versucht, es im globalen Paketordner zu installieren, und die übliche Signaturüberprüfung durchführt, bei der ein Fehler auftritt.</span><span class="sxs-lookup"><span data-stu-id="27b71-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="27b71-200">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="27b71-200">Workaround</span></span>
<span data-ttu-id="27b71-201">Deaktivieren Sie die Verwendung des Fallbackordners, indem Sie auf `RestoreAdditionalProjectSources` nichts festlegen:</span><span class="sxs-lookup"><span data-stu-id="27b71-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="27b71-202">Verwenden Sie dies mit Vorsicht, da Pakete, die aus dem Fallbackordner wiederhergestellt werden würden, jetzt von NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="27b71-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>