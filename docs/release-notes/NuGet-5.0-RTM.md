---
title: Anmerkungen zu dieser Version von nuget 5,0 RTM
description: Anmerkungen zu dieser Version von nuget 5,0 einschließlich bekannter Probleme, Fehlerbehebungen, neuer Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 637db1ae128ce020c33e54e56148c848a5f905a5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776226"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="16a10-103">Anmerkungen zu dieser Version von nuget 5,0</span><span class="sxs-lookup"><span data-stu-id="16a10-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="16a10-104">Möglichkeiten der NuGet-Verteilung:</span><span class="sxs-lookup"><span data-stu-id="16a10-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="16a10-105">NuGet-Version</span><span class="sxs-lookup"><span data-stu-id="16a10-105">NuGet version</span></span> | <span data-ttu-id="16a10-106">Verfügbar in der Visual Studio-Version</span><span class="sxs-lookup"><span data-stu-id="16a10-106">Available in Visual Studio version</span></span>| <span data-ttu-id="16a10-107">Verfügbar in .NET SDK(s)</span><span class="sxs-lookup"><span data-stu-id="16a10-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="16a10-108">**verfügbar**</span><span class="sxs-lookup"><span data-stu-id="16a10-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="16a10-109">Visual Studio 2019, Version 16.0</span><span class="sxs-lookup"><span data-stu-id="16a10-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="16a10-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="16a10-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="16a10-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="16a10-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="16a10-112">Visual Studio 2019 Version 16.0.4</span><span class="sxs-lookup"><span data-stu-id="16a10-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="16a10-113">[2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="16a10-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="16a10-114"><sup>1</sup> Installiert mit Visual Studio 2019 mit .net Core-Arbeitsauslastung</span><span class="sxs-lookup"><span data-stu-id="16a10-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="16a10-115"><sup>2</sup> Verfügbar als optionale Installation mit Visual Studio 2019 mit .net Core-Arbeitsauslastung</span><span class="sxs-lookup"><span data-stu-id="16a10-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="16a10-116">Zusammenfassung: Neues in 5,0</span><span class="sxs-lookup"><span data-stu-id="16a10-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="16a10-117">Unterstützung für die Wiederherstellung von [gefilterten Lösungen](/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019- [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="16a10-117">Support for restoring [filtered solutions](/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="16a10-118">`BuildTransitive` mit dem Ordner können Pakete transitiv Ziele/Eigenschaften zum Host Projekt beitragen [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="16a10-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="16a10-119">Bessere Unterstützung für packagereferenzierungsszenarien in nuget IVS-APIs- [#7005](https://github.com/NuGet/Home/issues/7005) [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="16a10-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="16a10-120">`nuget.exe pack project.json` ist veraltet- [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="16a10-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="16a10-121">Das Plug-in für die Anmelde Informationsanbieter-Plug-in wurde von Generation [2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) abgelöst und wird in Kürze als veraltet eingestuft- [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="16a10-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="16a10-122">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="16a10-122">Issues fixed in this release</span></span>

<span data-ttu-id="16a10-123">**Fehler**</span><span class="sxs-lookup"><span data-stu-id="16a10-123">**Bugs**</span></span>

* <span data-ttu-id="16a10-124">Vermeiden Sie bei einer NOOP-Wiederherstellung \* .dgspec.jsim Verzeichnis "obj", [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="16a10-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="16a10-125">Berechtigungen für Dateien, die in ~/.nuget erstellt werden, sind zu offen [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="16a10-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="16a10-126">`dotnet list package --outdated`funktioniert nicht mit Quellen, die Authentifizierung- [#7605](https://github.com/NuGet/Home/issues/7605) benötigen.</span><span class="sxs-lookup"><span data-stu-id="16a10-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="16a10-127">Nuget. VisualStudio. ivspackageinstaller-der Aufruf von für ein Projekt ohne Paket Verweise verwendet immer packages.config, auch wenn der Standardwert auf packagerereferences- [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="16a10-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="16a10-128">PMC: Update-Package erneute Installation ("das Paket wurde nicht gefunden") für getrennte Pakete fehlgeschlagen.</span><span class="sxs-lookup"><span data-stu-id="16a10-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="16a10-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="16a10-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="16a10-130">Hinzufügen eines Drittanbieter Hinweises in unserem Repository und VSIX- [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="16a10-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="16a10-131">"Nuget. VisualStudio. ivspackageinstaller. INSTALLPACKAGE" sollte die neueste Version installieren, wenn keine Version angegeben ist [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="16a10-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="16a10-132">--interaktive Unterstützung für dotnet nuget Push- [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="16a10-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="16a10-133">Bei der Wiederherstellung mit der Sperrdatei sollte NU1603 Warning nicht ausgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="16a10-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="16a10-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="16a10-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="16a10-135">Nuget sollte den Projektpfad während der Wiederherstellung nicht mit minimaler Protokollierung drucken [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="16a10-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="16a10-136">--interaktive Unterstützung für dotnet Remove Package- [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="16a10-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="16a10-137">Fügen Sie "nuget. Packaging. Core" mit typeforwardto attrs- [#7768](https://github.com/NuGet/Home/issues/7768) hinzu.</span><span class="sxs-lookup"><span data-stu-id="16a10-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="16a10-138">plugins_cache einen kürzeren Pfad zum Arbeiten benötigen [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="16a10-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="16a10-139">Pfad für MSBuild-Ermittlung bevorzugen, wenn der Benutzer keine bestimmte MSBuild-Version angefordert hat [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="16a10-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="16a10-140">`nuget.exe /?` sollte die korrekten MSBuild-Versionen auflisten- [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="16a10-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="16a10-141">Nuget. targets (498, 5): Fehler: ein Teil des Pfads "/tmp/NuGetScratch-on Mono- [#7793](https://github.com/NuGet/Home/issues/7793) wurde nicht gefunden.</span><span class="sxs-lookup"><span data-stu-id="16a10-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="16a10-142">Restore listet den Inhalt aller Versionen des Pakets, auf das verwiesen wird, im Computer Cache auf. [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="16a10-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="16a10-143">Die automatische MSBuild-Erkennung wählt nach der Installation von vs 2019 Preview- [#7621](https://github.com/NuGet/Home/issues/7621) immer 16,0 aus.</span><span class="sxs-lookup"><span data-stu-id="16a10-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="16a10-144">Das dotnet List-Paket für eine Lösung gibt doppelte Einträge für Framework- [#7607](https://github.com/NuGet/Home/issues/7607) aus.</span><span class="sxs-lookup"><span data-stu-id="16a10-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="16a10-145">Ausnahme "leerer Pfadname ist nicht zulässig" beim Aufrufen von ivspackageinstaller. INSTALLPACKAGE für alte Projekte, und der Ordner "Packages" ist nicht vorhanden.</span><span class="sxs-lookup"><span data-stu-id="16a10-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="16a10-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="16a10-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="16a10-147">MSBuild/t: Minimale Ausführlichkeit der Wiederherstellung sollte minimal sein [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="16a10-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="16a10-148">Die nuget-Benutzeroberfläche von vs 16,0 verfügt über unlesbare Registerkarten aufgrund von Farb Problemen [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="16a10-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="16a10-149">Nuget. Core & nuget. Clients License.txt Klärung- [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="16a10-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="16a10-150">Restore listet den globalen Paket Ordner auf, wenn versucht wird, Type- [#7596](https://github.com/NuGet/Home/issues/7596) zu bestimmen.</span><span class="sxs-lookup"><span data-stu-id="16a10-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="16a10-151">Fehler bei der Erzwingung von Sperrdateien sollten in Fehlerliste Fenster angezeigt werden [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="16a10-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="16a10-152">Beheben Sie NuGet.Configurationsprobleme- [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="16a10-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="16a10-153">Anpassen an MSBuild Aktualisieren des Installations Speicher Orts [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="16a10-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="16a10-154">"Nuget. Build. Tasks. Pack" sollte eine Entwicklungs Abhängigkeit [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="16a10-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="16a10-155">Hinzufügen des Paket Erweiterungs Punkts zum Einschließen von Debugsymbolen- [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="16a10-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="16a10-156">`dotnet pack` sollte den Abhängigkeits Versions Bereich in der erstellten nupkg beibehalten (auch wenn die unverankerte Version verwendet wird)- [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="16a10-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="16a10-157">`dotnet restore` schlägt an der authentifizierten Quelle fehl, wenn die config-Datei der Benutzerebene ebenfalls über die Quelle [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="16a10-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="16a10-158">Paket sollte den Satz von buildactions für Inhalts Dateien nicht einschränken- [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="16a10-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="16a10-159">Wenn Sie eine projectreferenzierung verwenden, bei der "assettargetfallback" ausgeführt werden muss, sollte gewarnt werden.</span><span class="sxs-lookup"><span data-stu-id="16a10-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="16a10-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="16a10-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="16a10-161">Deadlock aufgrund von Threading Problemen beim Aufrufen von CPS (commonprojectsystem)- [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="16a10-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="16a10-162">`dotnet add package` verwendet keine Anmelde Informationen aus der globalen Konfiguration für eine in der lokalen Konfiguration angegebene Quelle- [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="16a10-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="16a10-163">Threading Probleme mit MEF, die für Async-Codepfade aufgerufen werden- [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="16a10-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="16a10-164">Signierung: der Fehler wird zweimal und ohne aufrufsstapel [#6455](https://github.com/NuGet/Home/issues/6455) gemeldet.</span><span class="sxs-lookup"><span data-stu-id="16a10-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="16a10-165">Beim Installieren eines signierten Pakets mit nicht vertrauenswürdigem Signaturzertifikat sollte Fehler [#6318](https://github.com/NuGet/Home/issues/6318) angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="16a10-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="16a10-166">Nuget Restore nicht ordnungsgemäß, wenn zwei Projekte das obj-Verzeichnis gemeinsam nutzen [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="16a10-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="16a10-167">Pat mit `dotnet restore` unter Linux kann nicht mit Paketen aus authentifizierten Feeds verwendet werden [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="16a10-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="16a10-168">DotNet Restore Fehler aufgrund eines deaktivierten Computer weiten Feeds- [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="16a10-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="16a10-169">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="16a10-169">**DCRs**</span></span>

* <span data-ttu-id="16a10-170">Warnung zur zukünftigen Entfernung von "dotnet Pack project.json"- [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="16a10-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="16a10-171">Fügen Sie eine veralnungs Warnung für das Gen1 Anmelde Informationen-Plug-in hinzu [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="16a10-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="16a10-172">Signieren: aktiviertes Repository, das die Client Überprüfung jedes Pakets als durch das Repository signiertes Repository erfordert, über RepositorySignatures/5.0.0 Resource- [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="16a10-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="16a10-173">beschränken Sie die HTTP-Anforderungs Nummer pro Quelle über NuGet.Config- [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="16a10-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="16a10-174">Nuget sollte auf Net472 abzielen (um die Bereinigung des 16,0-Builds der VSIX zu erleichtern)- [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="16a10-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="16a10-175">PMC: openpackagepage-Befehls [#7384](https://github.com/NuGet/Home/issues/7384) entfernen</span><span class="sxs-lookup"><span data-stu-id="16a10-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="16a10-176">Erstellen von netcoreapp 3,0 mit netstandard 2,1- [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="16a10-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="16a10-177">Hinzufügen von netstandard 2.0-Unterstützung zu nuget. \* Packages- [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="16a10-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="16a10-178">Ermöglicht es Paket Autoren, das transitiv Verhalten von buildassets zu definieren- [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="16a10-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="16a10-179">Unterstützung des vs 2019-Lösungs Filter Features.</span><span class="sxs-lookup"><span data-stu-id="16a10-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="16a10-180">Unterstützt auch Projekte, die nicht in einer Projekt Mappe oder entladen wurden.</span><span class="sxs-lookup"><span data-stu-id="16a10-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="16a10-181">Die komplette Lösung (über CLI oder vs) muss zuerst wieder hergestellt werden [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="16a10-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="16a10-182">Nuget 5,0-Assemblys für die Verwendung von .NET 4.7.2 (über TFM-Änderung): [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="16a10-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="16a10-183">Nugetlicencdata aus nuget. Packaging sollte ein öffentlicher Typ sein.</span><span class="sxs-lookup"><span data-stu-id="16a10-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="16a10-184">Aktualisieren Sie die Lizenz Metadaten, die von spdx erfasst wurden.</span><span class="sxs-lookup"><span data-stu-id="16a10-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="16a10-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="16a10-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="16a10-186">Entfernen veralteter Einstellungs-APIs- [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="16a10-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="16a10-187">Problem Umgehung Wiederherstellungs Timeouts für Systeme mit einer CPU- [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="16a10-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="16a10-188">Nuget bevorzugt die NTLM-Authentifizierung, auch wenn in NuGet.config Option "config" Anmelde Informationen vorhanden sind, um Authentifizierung-Typen nach Anmelde Informationen zu filtern [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="16a10-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="16a10-189">Embedinteroptypes für packagereferenzierung aktivieren (übereinstimmende Packages.Config Funktion)- [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="16a10-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="16a10-190">**[Liste aller in dieser Version behobene Probleme-5,0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="16a10-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="16a10-191">Zusammenfassung: Neues in 5.0.2</span><span class="sxs-lookup"><span data-stu-id="16a10-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="16a10-192">Sicherheit (bei Ausführen über dotnet.exe oder mono.exe): der Ordner "obj" sollte mit den richtigen Berechtigungen erstellt werden [#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="16a10-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="16a10-193">nuget.exe Restore on Mono/MacOS schlägt mit benutzerdefiniertem nuget.config und `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span><span class="sxs-lookup"><span data-stu-id="16a10-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="16a10-194">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="16a10-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="16a10-195">Von .NET Core SDK in FallbackFolders installierte Pakete werden benutzerdefiniert installiert und bestehen die Signaturüberprüfung nicht.</span><span class="sxs-lookup"><span data-stu-id="16a10-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="16a10-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="16a10-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="16a10-197">Problem</span><span class="sxs-lookup"><span data-stu-id="16a10-197">Issue</span></span>
<span data-ttu-id="16a10-198">Bei Verwendung von dotnet.exe 2.x zum Wiederherstellen eines Projekts mit mehreren Zielen netcoreapp 1.x und netcoreapp 2.x wird der Fallbackordner als Dateifeed behandelt.</span><span class="sxs-lookup"><span data-stu-id="16a10-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="16a10-199">Dies bedeutet, dass NuGet bei der Wiederherstellung das Paket aus dem Fallbackordner auswählt und versucht, es im globalen Paketordner zu installieren, und die übliche Signaturüberprüfung durchführt, bei der ein Fehler auftritt.</span><span class="sxs-lookup"><span data-stu-id="16a10-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="16a10-200">Problemumgehung</span><span class="sxs-lookup"><span data-stu-id="16a10-200">Workaround</span></span>
<span data-ttu-id="16a10-201">Deaktivieren Sie die Verwendung des Fall Back Ordners, indem `RestoreAdditionalProjectSources` Sie auf "Nothing" festlegen:</span><span class="sxs-lookup"><span data-stu-id="16a10-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="16a10-202">Verwenden Sie dies mit Vorsicht, da Pakete, die aus dem Fall Back Ordner wieder hergestellt werden, jetzt von NuGet.org heruntergeladen werden.</span><span class="sxs-lookup"><span data-stu-id="16a10-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>