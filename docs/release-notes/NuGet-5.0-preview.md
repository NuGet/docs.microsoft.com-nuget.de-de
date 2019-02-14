---
title: Anmerkungen zu NuGet 5.0-preview
description: Anmerkungen zu NuGet-5.0-Preview, einschließlich bekannter Probleme, Fehlerbehebungen, neuen Features und DCRs.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 5889ea52f993fa8fe841f8eb83b6da659cdede93
ms.sourcegitcommit: 1ab750ff17e55c763d646c50e7630138804ce8b8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/14/2019
ms.locfileid: "56247658"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="3ac46-103">Anmerkungen zu NuGet 5.0 Preview</span><span class="sxs-lookup"><span data-stu-id="3ac46-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="3ac46-104">NuGet-5.0 Preview-Versionen</span><span class="sxs-lookup"><span data-stu-id="3ac46-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="3ac46-105">13 Februar 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="3ac46-105">February 13, 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span></span>
* <span data-ttu-id="3ac46-106">23 Januar 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="3ac46-106">January 23, 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span></span>

## <a name="summary-whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="3ac46-107">Zusammenfassung: Neuerungen in NuGet 5.0 Preview 3</span><span class="sxs-lookup"><span data-stu-id="3ac46-107">Summary: What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3ac46-108">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="3ac46-108">Issues fixed in this release</span></span> 

<span data-ttu-id="3ac46-109">**Bugs:**</span><span class="sxs-lookup"><span data-stu-id="3ac46-109">**Bugs:**</span></span>

* <span data-ttu-id="3ac46-110">nuget.exe /?</span><span class="sxs-lookup"><span data-stu-id="3ac46-110">nuget.exe /?</span></span> <span data-ttu-id="3ac46-111">tragen Sie richtige Msbuild-Versionen – [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="3ac46-111">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="3ac46-112">NuGet.targets(498,5): error : Einen Teil des Pfads konnte nicht gefunden "/ Tmp/NuGetScratch - unter Mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="3ac46-112">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="3ac46-113">Wiederherstellung listet unnötigerweise den Inhalt von allen Versionen von Referenziertes Paket im Cache Machine - [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="3ac46-113">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="3ac46-114">Automatische Erkennung von MSBuild wählt immer 16.0, nach der Installation von Visual Studio 2019 Vorschau - [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="3ac46-114">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="3ac46-115">Dotnet-umgebungsaufgabenlisten-Paket für eine Lösung gibt doppelte Einträge für Framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="3ac46-115">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="3ac46-116">Ausnahme "ein leerer Pfad ist nicht zulässig." beim aufrufenden IVsPackageInstaller.InstallPackage auf dem alten Projekte und-Pakete Ordner ist nicht vorhanden.</span><span class="sxs-lookup"><span data-stu-id="3ac46-116">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="3ac46-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="3ac46-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="3ac46-118">MSBuild/t: Restore Ausführlichkeitsgrad muss funktionalitätsanforderungen - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="3ac46-118">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="3ac46-119">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="3ac46-119">**DCRs**</span></span>

* <span data-ttu-id="3ac46-120">Paketersteller, die zum Definieren von Ressourcen transitive Buildverhalten - ermöglichen [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="3ac46-120">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="3ac46-121">Aktivieren der Wiederherstellung in Visual Studio erfolgreich, wenn ein Projekt nicht Teil der Lösung ist oder wurde nicht geladen, aber es bereits wiederhergestellt wurde - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="3ac46-121">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="3ac46-122">Zusammenfassung: Neuerungen in 5.0 Preview 2</span><span class="sxs-lookup"><span data-stu-id="3ac46-122">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3ac46-123">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="3ac46-123">Issues fixed in this release</span></span>

<span data-ttu-id="3ac46-124">**Bugs:**</span><span class="sxs-lookup"><span data-stu-id="3ac46-124">**Bugs:**</span></span>

* <span data-ttu-id="3ac46-125">Visual Studio 16.0 NuGet UI enthält unlesbare Registerkarten aufgrund von Problemen mit Farbe - [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="3ac46-125">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="3ac46-126">NuGet.Core & NuGet.Clients Dateien "License.txt" Klarstellung - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="3ac46-126">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="3ac46-127">Wiederherstellung listet globalen Paketordner unnötigerweise beim Versuch, um zu bestimmen, Typ: [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="3ac46-127">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="3ac46-128">Fehler von der Erzwingung der Sperre-Datei sollte angezeigt werden in der Fehlerliste (Fenster) - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="3ac46-128">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="3ac46-129">Beheben von Problemen mit NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="3ac46-129">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="3ac46-130">Anpassung an MSBuild aktualisieren sie den Installationsort.</span><span class="sxs-lookup"><span data-stu-id="3ac46-130">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="3ac46-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="3ac46-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="3ac46-132">NuGet.Build.Tasks.Pack muss eine entwicklungsabhängigkeit - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="3ac46-132">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="3ac46-133">Hinzufügen von Pack Erweiterungspunkt zum Einschließen von Debugsymbole - [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="3ac46-133">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="3ac46-134">Dotnet-Pack beibehalten soll Abhängigkeit Versionsbereich in NuGet-Paket erstellt.</span><span class="sxs-lookup"><span data-stu-id="3ac46-134">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="3ac46-135">(auch, wenn die unverankerte Version verwendet wird) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="3ac46-135">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="3ac46-136">Dotnet-Restore auf authentifizierte Quelle schlägt fehl, wenn es sich bei auf Benutzerebene Konfiguration auch-Quelle – hat [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="3ac46-136">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="3ac46-137">Pack sollten nicht nur BuildActions für Inhaltsdateien - [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="3ac46-137">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="3ac46-138">Verwenden eine "ProjectReference" AssetTargetFallback erfolgreich ausgeführt werden müssen, sollte eine Warnung ausgeben.</span><span class="sxs-lookup"><span data-stu-id="3ac46-138">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="3ac46-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="3ac46-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="3ac46-140">Deadlock aufgrund von Threadingprobleme beim Aufrufen von in CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="3ac46-140">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="3ac46-141">Dotnet add-Paket nicht die Anmeldeinformationen aus der globalen Konfiguration verwendet, für eine Datenquelle angegeben, in der lokalen Konfiguration - [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="3ac46-141">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="3ac46-142">Probleme mit MEF wird Threading für asynchrone Codepfade - aufgerufen [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="3ac46-142">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="3ac46-143">Anmeldung: Fehler zweimal und ohne Aufrufliste - [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="3ac46-143">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="3ac46-144">Installieren eines signierten Pakets mit nicht vertrauenswürdigen Signaturzertifikat sollte angezeigt werden Fehler: [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="3ac46-144">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="3ac46-145">NuGet restore noops sind nicht ordnungsgemäß, beim Verzeichnis "Obj" - 2-Projekten gemeinsam [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="3ac46-145">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="3ac46-146">PAT mit Dotnet-Restore unter Linux von Paketen aus authentifizierte Feeds - können keine [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="3ac46-146">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="3ac46-147">Dotnet-Restore versagt, wenn deaktivierte auf den gesamten Computer feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="3ac46-147">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="3ac46-148">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="3ac46-148">**DCRs**</span></span>

* <span data-ttu-id="3ac46-149">NuGet-5.0-Assemblys in .NET 4.7.2 (über die Änderung der TFM) - erfordern [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="3ac46-149">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="3ac46-150">NuGetLicenseData aus NuGet.Packaging sollte ein öffentlicher Typ sein.</span><span class="sxs-lookup"><span data-stu-id="3ac46-150">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="3ac46-151">Aktualisieren Sie die Lizenzmetadaten aus Spdx erfasst.</span><span class="sxs-lookup"><span data-stu-id="3ac46-151">Update license metadata ingested from spdx.</span></span><span data-ttu-id="3ac46-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="3ac46-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="3ac46-153">Entfernen Sie veraltete APIs für Einstellungen – [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="3ac46-153">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="3ac46-154">Problemumgehung Wiederherstellung Timeouts auf Systemen mit 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="3ac46-154">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="3ac46-155">NuGet NTLM-Authentifizierung bevorzugt, auch wenn die Anmeldeinformationen vorhanden sind, in der Datei "NuGet.config" – Filter-Auth-Typen zur Eingabe von Anmeldeinformationen - Option "Config" hinzufügen [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="3ac46-155">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="3ac46-156">Aktivieren Sie EmbedInteropTypes für "packagereference" (übereinstimmende Datei "Packages.config"-Funktion) - [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="3ac46-156">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="3ac46-157">Liste aller Probleme, die in dieser Version 5.0.0-preview2 behoben</span><span class="sxs-lookup"><span data-stu-id="3ac46-157">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="3ac46-158">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="3ac46-158">Known issues</span></span>

#### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="3ac46-159">„dotnet nuget push --interactive“ löst auf dem Mac eine Fehlermeldung aus.</span><span class="sxs-lookup"><span data-stu-id="3ac46-159">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="3ac46-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="3ac46-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>
<span data-ttu-id="3ac46-161">**Problem** der `--interactive` Argument wird von der Dotnet-Cli nicht weitergeleitet werden und führt zu dem Fehler `error: Missing value for option 'interactive'` 
 **Problemumgehung** jeden anderen Dotnet-Befehl ausführen, mit der Option "Interaktiv", wie z. B. `dotnet restore --interactive` und authentifizieren.</span><span class="sxs-lookup"><span data-stu-id="3ac46-161">**Issue** The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`
**Workaround** Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="3ac46-162">Die Authentifizierung könnte dann möglicherweise vom Anmeldeinformationsanbieter zwischengespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="3ac46-162">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="3ac46-163">Führen Sie anschließend `dotnet nuget push` aus.</span><span class="sxs-lookup"><span data-stu-id="3ac46-163">Then run `dotnet nuget push`.</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="3ac46-164">Von .NET Core SDK in FallbackFolders installierte Pakete werden benutzerdefiniert installiert und bestehen die Signaturüberprüfung nicht.</span><span class="sxs-lookup"><span data-stu-id="3ac46-164">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="3ac46-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="3ac46-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="3ac46-166">**Problem** bei Verwendung des dotnet.exe 2.x auf ein Projekt, mit mehreren Zielen Netcoreapp wiederherstellen 1.x und Netcoreapp 2.x, alternative Ordner so behandelt, als eine Datei mit dem feed.</span><span class="sxs-lookup"><span data-stu-id="3ac46-166">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="3ac46-167">Dies bedeutet, dass NuGet bei der Wiederherstellung das Paket aus dem Fallbackordner auswählt und versucht, es im globalen Paketordner zu installieren, und die übliche Signaturüberprüfung durchführt, bei der ein Fehler auftritt.</span><span class="sxs-lookup"><span data-stu-id="3ac46-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="3ac46-168">**Problemumgehung** deaktivieren Sie die Verwendung des Ordners fallback durch Festlegen der `RestoreAdditionalProjectSources` auf nichts verweist.</span><span class="sxs-lookup"><span data-stu-id="3ac46-168">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="3ac46-169">`<RestoreAdditionalProjectSources/>` Verwenden Sie dies mit Vorsicht, da es bewirkt, dass viele Pakete von NuGet.org heruntergeladen werden, die andernfalls aus dem Fallbackordner wiederhergestellt würden.</span><span class="sxs-lookup"><span data-stu-id="3ac46-169">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
