---
title: Anmerkungen zu NuGet 3.5 Beta
description: Anmerkungen zu NuGet 3.5, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d8df2cb51ddcc03fb3922d9e9def17b39fccc661
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550683"
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="ad199-103">Anmerkungen zu NuGet 3.5</span><span class="sxs-lookup"><span data-stu-id="ad199-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="ad199-104">[Anmerkungen zu NuGet 3.5-RC](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC-Versionsanmerkungen](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="ad199-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="ad199-105">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="ad199-105">Bug Fixes</span></span>

* <span data-ttu-id="ad199-106">Pack verwendet nicht MSBuild 14.1 unter Mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="ad199-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="ad199-107">Registerkarte "Updates" nicht wählen Sie die neueste verfügbare Version zu aktualisieren, wählen Sie derzeit installierte Version - stattdessen [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="ad199-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="ad199-108">Beheben der Absturz nach einer privaten v2 MyGet-feed zu authentifizieren, und klicken auf "X mehr Ergebnisse anzeigen"- [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="ad199-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="ad199-109">Protokollmeldungen für UI - in umgekehrter Reihenfolge zu sein scheinen [#3446](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="ad199-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="ad199-110">V3.4.4 - Nuget-Wiederherstellung löst "Format für den angegebenen Pfad wird nicht unterstützt" - [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="ad199-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="ad199-111">NuGet-Befehlszeile 3.6 Beta berücksichtigt keine - Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="ad199-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="ad199-112">NuGet IKVM langsam zu installieren, auf großen Projekt - [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="ad199-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="ad199-113">NuGet.exe - Self-Service wird auf sich selbst zu aktualisieren – Update [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="ad199-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="ad199-114">3.5 installieren/Wiederherstellen von UNC-Freigabe ist Regression aus 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="ad199-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="ad199-115">Fehler bei der Installation von Moq aus der Paket-Verwaltungsoberfläche für ein Projekt "net451" - [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="ad199-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="ad199-116">Install-Registerkarte auf Projektmappenebene keine Version des Pakets - anzeigen [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="ad199-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="ad199-117">Xproj `project.json` Update aus der Registerkarte "installiert" verliert die Status - [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="ad199-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="ad199-118">NuGet Pack auf `.csproj` ignoriert leere Dateien-Element im `.nuspec` -Datei – [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="ad199-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="ad199-119">Websiteprojekten in IIS gehostete sollte nicht dazu, dass der Wiederherstellung ein Fehler auftritt – [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="ad199-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="ad199-120">Anmeldeinformationen, die nicht aus der Datei "NuGet.config" abgerufen werden, wenn v3-Endpunkts auf v2 - umleitet [#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="ad199-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="ad199-121">NuGet Pack nicht Assembly aufgelöst wird, beim Abrufen von Metadaten für übertragbare Assembly - [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="ad199-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="ad199-122">NuGet wurde nicht gefunden. `msbuild.exe` unter Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="ad199-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="ad199-123">NuGet.exe-Pack kann kein vorab veröffentlichtes-Tag der beginnt mit einer Anzahl - [#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="ad199-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="ad199-124">Installation des NuGet-Pakets ein Fehler auftritt, auf VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="ad199-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="ad199-125">AllowedVersions Filtern nicht funktioniert auf Projektmappenebene - [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="ad199-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="ad199-126">Wiederherstellung nach dem Zufallsprinzip schlägt fehl, mit einem Element mit demselben Schlüssel wurde bereits hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="ad199-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="ad199-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="ad199-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="ad199-128">Kann nicht installiert werden Nuget.Common in `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="ad199-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="ad199-129">Wenn die Benutzeroberfläche verwendet, um eine V2-Quelle zu suchen, heißt FindPackagesById zweimal für jeden ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="ad199-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="ad199-130">Pakete können nicht-Projekte – hängen [#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="ad199-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="ad199-131">NuGet.exe-Pack - Exclude ist dokumentiert, ist jedoch nicht unterstützt – [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="ad199-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="ad199-132">Probleme mit Fehler Instanznachrichten an, wenn im Abschnitt "ContentFiles" `.nuspec` ist ungültig: [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="ad199-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="ad199-133">Pushbenachrichtigungen sendet immer die gesamtes Paket zweimal mit authentifizierte Paketquellen - [#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="ad199-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="ad199-134">Es sind keine Informationen wurde angegeben, beim Aufrufen von nuget.exe-Update \*.csproj, während das Projekt keine `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="ad199-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="ad199-135">`packages.config` Wiederherstellung wird nicht erneut versucht, auf den Statuscode 5xx in V2-Quellen – [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="ad199-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="ad199-136">Doppelter Punkt im Datei-Src in `.nuspec` funktioniert nicht – [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="ad199-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="ad199-137">CoreCLR-wiederhergestellt werden soll, um Feeds mit der Verschlüsselung – ignorieren [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="ad199-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="ad199-138">NuGet.exe-push 403 - falsch Aufforderung zur Eingabe von Anmeldeinformationen - Behandlung [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="ad199-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="ad199-139">NuGet-Update über die Paket-Manager entfernt, Eigenschaften aus der `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="ad199-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="ad199-140">NuGet.PackageManagement.VisualStudio versuchen Sie es beim Laden von "NuGet.TeamFoundationServer14" geändert, denn DLL-Namen auf "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="ad199-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="ad199-141">Paket-Manager-Benutzeroberfläche neu zeigen keine aktualisierte Version - [#2828](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="ad199-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="ad199-142">Update-Package möchten, verwenden Sie die Paket-ID, Version statt package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="ad199-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="ad199-143">NuGet-Wiederherstellung Csproj sollten Fehler, wenn das Projekt Nuget verwenden, ist nicht (`packages.config` oder `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="ad199-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="ad199-144">TFS-Fehler "[Datei] nicht in Ihrem Arbeitsbereich gefunden, oder Sie sind nicht berechtigt, darauf zuzugreifen" beim Aktualisieren oder deinstallieren, wenn die Projektmappe oder eines Projekts an TFS-quellcodeverwaltung - gebunden ist [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="ad199-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="ad199-145">Update-Paket keine Abhängigkeiten für Pakete, nicht-Ziel abrufen [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="ad199-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="ad199-146">Es gibt keine Möglichkeit festzulegende Protokolle Ausführlichkeitsgrad für Nuget-Paket-Manager-UI-Aktionen – [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="ad199-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="ad199-147">NuGet-Konfiguration ist ungültig: Visual Studio 2015 VSIX (3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="ad199-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="ad199-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) funktioniert nicht – [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="ad199-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="ad199-149">Version von NuGet 3.4.3 - Wert abrufen darf nicht null sein beim Erstellen des Paket - [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="ad199-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="ad199-150">Wiederherstellung verwendet gespeicherte Anmeldeinformationen aus der Datei "NuGet.config" nicht für VSTS-Feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="ad199-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="ad199-151">[Dotnet-Restore]--Configfile ist relativ zum Projekt Dir anstelle der Cmd-Dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="ad199-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="ad199-152">Übermäßig viele Zuordnungen im Code von Version-Vergleichs - [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="ad199-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="ad199-153">Mehrere Instanzen von nuget.exe gleich installieren möchten-Paket in parallelen bewirkt, dass einen double-Schreibvorgang - [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="ad199-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="ad199-154">Informationen zu den Abhängigkeiten ist nicht für mehrere Projekte – Vorgänge – zwischengespeichert [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="ad199-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="ad199-155">Installieren und aktualisieren Sie die Downloadpakete ohne Überprüfung der Ordner "Pakete" zuerst - [#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="ad199-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="ad199-156">Wenn die Liste der Pakete-Quelle leer ist, kann nicht Paketquelle Benutzeroberfläche hinzugefügt (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="ad199-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="ad199-157">Irreführender Fehler, wenn Sie versuchen, das Paket zu installieren, von denen abhängt, während der Entwurfszeit Fassaden - [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="ad199-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="ad199-158">Installieren eines Pakets von PackageManager-Konsole mit der Einstellung "Alle" aus versucht nur erste Quelle - [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="ad199-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="ad199-159">Neueste Betaversion nicht Entzippen ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="ad199-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="ad199-160">Absturz von Visual Studio 2015 beim Start mit selbst erstellten NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="ad199-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="ad199-161">Befehl "Update" ist möglicherweise ein wenig ausführlicher, wenn i Datenbankanmeldeinformationen... – werden Fragen [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="ad199-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="ad199-162">Lokal erstellten VSIX müssen dieselben DLLs und Dateien wie der CI-Build.</span><span class="sxs-lookup"><span data-stu-id="ad199-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="ad199-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="ad199-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="ad199-164">Beheben Sie Warnungen für NuGet-Herabstufung im Build - [#2396](https://github.com/NuGet/Home/issues/2396)</span><span class="sxs-lookup"><span data-stu-id="ad199-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="ad199-165">Paketquelle (3 Mal) authentifizieren nicht unbegrenzt - blockiert [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="ad199-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="ad199-166">Paketinhalt wird nicht ordnungsgemäß wiederhergestellt, beim Installieren eines Pakets aus einem Nuget-Version 3.3 +-mit dem Argument Feeds - NoCache, wenn das Paket enthält `.nupkg` Dateien – [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="ad199-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="ad199-167">Installieren von NuGet mit alle Paketquellen, aber das Paket umfasst keine aus Quelle 1 ein Fehler auftritt – [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="ad199-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="ad199-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt; &gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;B__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="ad199-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="ad199-169">Installieren Sie Blöcke, fällt eine einzelne Quelle Authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="ad199-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="ad199-170">`.nuspec` Bereich sollten außer Kraft setzen - IncludeReferencedProjects Version – Version [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="ad199-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="ad199-171">Update-Package extrem langsam: "Es wurde versucht zum Sammeln von Informationen von Abhängigkeiten" - [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="ad199-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="ad199-172">Geschützter Downgrades von NuGet-Paket beim Batch - Abhängigkeiten aktualisieren [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="ad199-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="ad199-173">NuGet.exe-Update löscht die Assembly starke Namen und das Private-Attribut.</span><span class="sxs-lookup"><span data-stu-id="ad199-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="ad199-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="ad199-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="ad199-175">Relativen Pfad für "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="ad199-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="ad199-176">Verbesserung der Fehlermeldungen Resolver - [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="ad199-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="ad199-177">V3-Update-Paket ein Fehler auftritt, mit Paketen, die nicht in der angegebenen Quelle - [#1013](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="ad199-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="ad199-178">Das verwenden relativer Pfade für die Paketquellen ist problematisch, Verwendung von - [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="ad199-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="ad199-179">Fehlende Abhängigkeit in NUPKG-Datei aus Projekt generiert wird, wenn indirekte Abhängigkeit mit einer niedrigeren versionsanforderung bereits - [#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="ad199-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="ad199-180">Löschen ein Projekt wird die entsprechende Benutzeroberfläche-Fenster geschlossen, aber Umbenennen eines Projekts UI-Fenster nicht umbenannt.</span><span class="sxs-lookup"><span data-stu-id="ad199-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="ad199-181">Beachten Sie, dass die PMC umbenennen und Projekt entfernen-Ereignisse – überwacht [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="ad199-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="ad199-182">[Willow-Web-Workload] Hängt, erstellen Razor v3 WSP - [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="ad199-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="ad199-183">Installation/Wiederherstellung eines bestimmten Pakets schlägt fehl mit "enthält Paket mehrere Nuspec-Dateien."</span><span class="sxs-lookup"><span data-stu-id="ad199-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="ad199-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="ad199-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="ad199-185">Kleinbuchstaben IDs & `packages.config` Szenarien – [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="ad199-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="ad199-186">[3.5-beta2] Wiederherstellen von Paketen nicht wiederherstellen "legacy" Pakete - [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="ad199-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="ad199-187">NuGet Pack fügt das TT-Dateien zum Ordner "Content" unabhängig davon, was - [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="ad199-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="ad199-188">Update-Package, ASP.NET Web-App generiert die Warnung im Zusammenhang mit der Datei: Source - [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="ad199-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="ad199-189">NuGet Pack Csproj (mit `project.json`) stürzt ab, wenn es keine PackOptions und Besitzer in der JSON-Datei sind - [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="ad199-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="ad199-190">NuGet Pack für `project.json` ignoriert PackOptions Tags wie Zusammenfassung, Autoren und Besitzer usw. – [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="ad199-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="ad199-191">"NullReferenceException" über NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="ad199-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="ad199-192">NuGet Pack werden die Abhängigkeiten in der Ausgabe ignoriert `.nuspec` für `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="ad199-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="ad199-193">Aktualisieren mehrere Pakete mit Rollback lässt das Projekt in einem unterbrochenen Zustand - [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="ad199-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="ad199-194">"Contentfiles", unter einer werden nicht hinzugefügt werden, für die Netstandard-Projekte – [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="ad199-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="ad199-195">Kann nicht gepackt werden Library für .net Standard ordnungsgemäß - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="ad199-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="ad199-196">Datei -> Neues Projekt -> Klassenbibliothek (portabel) ein Fehler auftritt-Projekt in Visual Studio 2015 und Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="ad199-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="ad199-197">NuGet-Fehler: 1.0.0-\* ist keine gültige Versionszeichenfolge - [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="ad199-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="ad199-198">Find-Package ein Fehler auftritt, anzeigen, aber funktioniert für Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="ad199-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="ad199-199">Fehler bei "Install-Package jquery.validation" auf dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="ad199-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="ad199-200">Ungültiger Zielpfad - NuGet-Paket von Xproj Standardwert ist [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="ad199-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="ad199-201">Bei der installierten Visual Studio 2015 update 3 für einen im Vergleich, der verwendet NuGet 3.5.0-Versionsfehler tritt auf, - [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="ad199-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="ad199-202">"Von" Packages.config "blockiert" in `project.json` (UWP, bzw.-Build integriert)-Projekt – [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="ad199-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="ad199-203">Aktualisieren Sie die Dotnet-Cli, die vom Buildskript, um Preview 2-003121, die in der offiziellen Preview 2-Build ist installiert.</span><span class="sxs-lookup"><span data-stu-id="ad199-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="ad199-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="ad199-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="ad199-205">Paket-Manager-Benutzeroberfläche: neue Version nicht angezeigt werden, nach dem Aktualisieren eines Pakets- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="ad199-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="ad199-206">-"Apikey" Befehlszeile für Delete-Befehl nicht Lese-/gesendet 3.5.0-Beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="ad199-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="ad199-207">Falsches Zeichenfolgenformat: eine stabile Version eines Pakets müssen sich nicht auf einer Vorabversion Abhängigkeit.</span><span class="sxs-lookup"><span data-stu-id="ad199-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="ad199-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="ad199-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="ad199-209">OptimizedZipPackage Cache bewirkt, dass leere Ordner - [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="ad199-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="ad199-210">Erstellen die PCL (net46 und Windows 10)-Projekt Get NullRef-Ausnahme.</span><span class="sxs-lookup"><span data-stu-id="ad199-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="ad199-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="ad199-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="ad199-212">NuGet-Updates sollten informationsmeldung bereitstellen, wenn eine höhere Version durch Einschränkung der AllowedVersions - eingeschränkt ist [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="ad199-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="ad199-213">Probleme mit NuGet v3 der datenbankwiederherstellung - [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="ad199-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="ad199-214">Anmeldeinformationen-Plug-in wurde mit Fehler-1 beendet / Fehler beim Herunterladen bei Verwendung der Anmeldeinformationsanbieter mit mehreren Quellen – package [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="ad199-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="ad199-215">`project.json` NuGet-Wiederherstellung führt dazu, dass eine Neukompilierung, wenn nichts geändert – [#2817](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="ad199-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="ad199-216">Symbolpakete sollte nicht immer in installieren oder Aktualisieren von - verwendet [#2807](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="ad199-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="ad199-217">Visual Studio unterstützt keine Umgebungsvariablen im RepositoryPath (nuget.exe bewirkt) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="ad199-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="ad199-218">Bezeichnung der noch nicht gekennzeichneten UIElements im Paket-Manager-UI für die Barrierefreiheit - [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="ad199-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="ad199-219">Portable-Frameworks mit Bindestrichen Profile werden abgelehnt.</span><span class="sxs-lookup"><span data-stu-id="ad199-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="ad199-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="ad199-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="ad199-221">NuGet-Paket-Manager sollten diese Optionsliste in Paketen zu verdeutlichen, Detail nicht für gilt, `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="ad199-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="ad199-222">NuGet.exe-Push/Delete-API-Schlüssel – nicht verwendet, [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="ad199-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="ad199-223">Entfernen Sie die gesperrte Eigenschaft aus der Sperrdatei - [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="ad199-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="ad199-224">NuGet 3.3.0-Aktualisierung ein Fehler auftritt, mit "... eine zusätzliche Einschränkung definiert" Packages.config "wird verhindert, dass dieser Vorgang."</span><span class="sxs-lookup"><span data-stu-id="ad199-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="ad199-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="ad199-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="ad199-226">Installieren des Pakets aus einer lokalen Quelle, die nicht vorhanden ist löst einer gefälschten Nachricht - [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="ad199-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="ad199-227">"Upgrade verfügbar"-Filter werden Upgrades, bei denen die versionseinschränkung - verletzen [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="ad199-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="ad199-228">Kann nicht aktualisiert werden native Pakete - [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="ad199-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="ad199-229">Features</span><span class="sxs-lookup"><span data-stu-id="ad199-229">Features</span></span>

* <span data-ttu-id="ad199-230">Einstellung CopyLocal auf "false" für hinzugefügt, die von NuGet - Verweise unterstützen [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="ad199-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="ad199-231">NuGet.exe-Unterstützung für MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="ad199-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="ad199-232">Unterstützung für.`csproj`</span><span class="sxs-lookup"><span data-stu-id="ad199-232">Pack support for .`csproj`</span></span><span data-ttu-id="ad199-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="ad199-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="ad199-234">Benutzeraktion zu deaktivieren, wenn Benutzer Aktionen ausgeführt wird – [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="ad199-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="ad199-235">NuGet sollten Hinzufügen von Unterstützung für `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="ad199-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="ad199-236">Hinzufügen des Framework Probleme mit der fehlt in NuGet 2.x (die bereits in 3.x sind) - [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="ad199-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="ad199-237">Unterstützung für den fallback-Paket-Ordner - [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="ad199-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="ad199-238">Entwerfen und implementieren Sie eine Vorstellung von Pakettyp Tool Pakete, unterstützen [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="ad199-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="ad199-239">Hinzufügen einer API zum Abrufen des Pfads zu dem Ordner mit globalen Paketen - [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="ad199-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="ad199-240">Aktivieren von SemVer 2.0.0 im Paket - [von #3356](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="ad199-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="ad199-241">DCRs</span><span class="sxs-lookup"><span data-stu-id="ad199-241">DCRs</span></span>

* <span data-ttu-id="ad199-242">NuGet.exe-Push - Timeout-Parameter funktioniert nicht – [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="ad199-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="ad199-243">Beschreibungstext des Pakets muss auswählbare - [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="ad199-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="ad199-244">Aktivieren von nuget.exe erzeugt `.props` und `.targets` -Dateien für `.nuproj` Projekte [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="ad199-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="ad199-245">Hinzufügen-Erweiterbarkeits-API-Frameworks mit Imports - vergleichen [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="ad199-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="ad199-246">Abhängigkeitsoptionen ausblenden, wenn mit `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="ad199-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="ad199-247">Drucken Sie nuget.exe-Version-Header in der ausführlichen Ausgabe - [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="ad199-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="ad199-248">NuGet muss, damit Benutzer wissen, dass in einem Dotnet Tfm-basierte aktualisieren bzw. installieren PCL-Fehlern – verursachen [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="ad199-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="ad199-249">Ungültige installieren/aktualisieren für Projekt mit Tfm warnen = "Dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="ad199-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="ad199-250">Beheben von Leistungsproblemen mit ReShaper und NuGet für Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="ad199-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="ad199-251">Hinzufügen von Unterstützung für netcoreapp11 und netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="ad199-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="ad199-252">AssemblyMetadata-Attribut für nutzen `.nuspec` Ersetzungen - token [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="ad199-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
