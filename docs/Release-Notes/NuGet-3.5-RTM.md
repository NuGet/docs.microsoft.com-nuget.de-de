---
title: NuGet-3.5 Beta-Versionshinweise | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 3.5 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-3.5 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ee78ceb2ff032c05c0f8ef9a6623b94cc56ee0a9
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="4dae1-104">3.5 NuGet-Versionshinweise</span><span class="sxs-lookup"><span data-stu-id="4dae1-104">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="4dae1-105">[NuGet-3.5 RC-Versionsanmerkungen](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC-Versionsanmerkungen](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="4dae1-105">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="4dae1-106">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="4dae1-106">Bug Fixes</span></span>

* <span data-ttu-id="4dae1-107">Pack verwendet MSBuild 14,1 nicht auf das Mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="4dae1-107">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="4dae1-108">Registerkarte "Update" nicht die neueste verfügbare Version select derzeitig installierten Version - stattdessen aktualisieren wählen [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="4dae1-108">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="4dae1-109">Beheben von Absturz (Crash) nach der Authentifizierung einen privaten v2 MyGet feed und durch Klicken auf "X Weitere Ergebnisse anzeigen"- [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="4dae1-109">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="4dae1-110">Protokollmeldungen für UI - in umgekehrter Reihenfolge zu sein scheinen [#3446](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="4dae1-110">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="4dae1-111">V3.4.4 - NuGet-Wiederherstellung löst "das Format des angegebenen Pfads wird nicht unterstützt" - [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="4dae1-111">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="4dae1-112">NuGet-CmdLine 3.6 Beta berücksichtigt keine - Prop Configuration = Release – [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="4dae1-112">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="4dae1-113">Installieren Sie NuGet IKVM langsam auf großen Projekten - [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="4dae1-113">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="4dae1-114">NuGet.exe - Self-Service behält auf sich selbst zu aktualisieren – Update [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="4dae1-114">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="4dae1-115">3.5 installieren/Wiederherstellen von UNC-Freigabe hat 3.4.4 - Leistung Regression [#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="4dae1-115">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="4dae1-116">Fehler bei der Installation von Moq aus der Paket-Benutzeroberfläche für ein Projekt net451 - [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="4dae1-116">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="4dae1-117">Registerkarte "installieren" auf Projektmappenebene nicht anzeigen des Paketversion - [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="4dae1-117">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="4dae1-118">Xproj `project.json` Aktualisierung über die Registerkarte "installiert" verliert State - [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="4dae1-118">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="4dae1-119">NuGet-Pack auf `.csproj` ignoriert leere Files-Element im `.nuspec` Datei - [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="4dae1-119">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="4dae1-120">Websiteprojekten in IIS gehostete sollte nicht dazu, dass der Wiederherstellung fehl - [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="4dae1-120">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="4dae1-121">Anmeldeinformationen, die nicht von "NuGet.config" abgerufen werden, wenn v3-Endpunkt auf v2 - leitet [#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="4dae1-121">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="4dae1-122">NuGet-Pack nicht Assembly aufgelöst wird, beim Abrufen von Assemblymetadaten für portable - [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="4dae1-122">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="4dae1-123">NuGet wurde nicht gefunden. `msbuild.exe` auf Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="4dae1-123">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="4dae1-124">NuGet.exe Pack ein Pre-Release-Tag, das mit Zahlen - beginnt kann keine [#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="4dae1-124">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="4dae1-125">Installieren von NuGet-Paket erzeugt einen Fehler, die auf VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="4dae1-125">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="4dae1-126">"allowedversions" Filtern funktioniert nicht auf Projektmappenebene - [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="4dae1-126">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="4dae1-127">Wiederherstellung nach dem Zufallsprinzip schlägt fehl, mit einem Element mit demselben Schlüssel wurde bereits hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="4dae1-127">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="4dae1-128"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="4dae1-128"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="4dae1-129">Kann nicht installiert werden Nuget.Common in `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="4dae1-129">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="4dae1-130">Wenn die Benutzeroberfläche verwenden, um eine V2-Quelle zu suchen, heißt FindPackagesById zweimal für jede ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="4dae1-130">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="4dae1-131">Pakete können nicht für Projekte - abhängen [#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="4dae1-131">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="4dae1-132">NuGet.exe-Pack - Exclude dokumentiert jedoch nicht unterstützt - [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="4dae1-132">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="4dae1-133">Probleme mit dem Fehler Instanznachrichten an, wenn im Abschnitt "Inhaltsdateien" `.nuspec` ist ungültig - [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="4dae1-133">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="4dae1-134">Push sendet immer die gesamtes Paket zweimal mit authentifiziert Paketquellen - [#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="4dae1-134">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="4dae1-135">Es werden keine Informationen wurde beim Aufrufen von nuget.exe Update \*.csproj, während das Projekt keinen angegeben ein `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="4dae1-135">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="4dae1-136">`packages.config`Wiederherstellung wird nicht erneut versucht, auf 5xx-Statuscodes aus Quellen für V2 - [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="4dae1-136">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="4dae1-137">Doppelte Punkte in der Datei Src in `.nuspec` funktioniert nicht – [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="4dae1-137">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="4dae1-138">Ignorieren von Feeds mit Verschlüsselung - CoreCLR wiederherstellen muss [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="4dae1-138">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="4dae1-139">NuGet.exe push 403 - falsch zum Eingeben von Anmeldeinformationen aufzufordern - Behandlung [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="4dae1-139">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="4dae1-140">NuGet-Update durch den Paketmanager entfernt, Eigenschaften aus der `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="4dae1-140">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="4dae1-141">NuGet.PackageManagement.VisualStudio versuchen Sie es beim Laden von "NuGet.TeamFoundationServer14", aber, dass die DLL-Namen in "NuGet.TeamFoundationServer" - geändert [#2857](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="4dae1-141">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="4dae1-142">Paket-Manager, die die Benutzeroberfläche nicht werden neu angezeigt aktualisierte Version - [#2828](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="4dae1-142">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="4dae1-143">Updatepaket möchten, verwenden Sie die Paket-ID, Version statt package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="4dae1-143">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="4dae1-144">NuGet Restore Csproj sollten Fehler auf, wenn das Projekt mithilfe von Nuget ist nicht (`packages.config` oder `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="4dae1-144">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="4dae1-145">TFS-Fehler "[Datei] nicht in Ihrem Arbeitsbereich gefunden, oder Sie keine Berechtigung für den Zugriff" beim Aktualisieren oder deinstallieren, wenn TFS-quellcodeverwaltung - Projektmappe/Projekt gebunden ist [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="4dae1-145">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="4dae1-146">das Updatepaket nicht abrufen Abhängigkeiten für Pakete von nicht-Ziel - [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="4dae1-146">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="4dae1-147">Es gibt keine Möglichkeit, den Ausführlichkeitsgrad für NuGet-Paket-Manager-UI-Aktionen - Protokolle festlegen [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="4dae1-147">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="4dae1-148">die NuGet-Konfiguration ist ungültig – VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="4dae1-148">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="4dae1-149">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) funktioniert nicht – [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="4dae1-149">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="4dae1-150">NuGet 3.4.3 Version - Wert darf nicht null sein beim Erstellen des Paket - [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="4dae1-150">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="4dae1-151">Wiederherstellung verwendeten gespeicherten Anmeldeinformationen von "NuGet.config" nicht für VSTS-Feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="4dae1-151">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="4dae1-152">[Dotnet wiederherstellen]--Configfile ist relativ zum Projekt Dir anstelle der Cmd-Dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="4dae1-152">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="4dae1-153">Eine übermäßige Zuordnungen in Code von Version Vergleiche - [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="4dae1-153">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="4dae1-154">Mehrere Instanzen von nuget.exe identisch installieren möchten-Pakets in parallelen Ursachen einen double-Schreibvorgang - [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="4dae1-154">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="4dae1-155">Abhängigkeitsinformationen für mehrere Projekte Operations - nicht zwischengespeichert [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="4dae1-155">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="4dae1-156">Installieren und Aktualisieren von Downloadpaketen ohne Überprüfung der Ordner "Pakete" zuerst - [#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="4dae1-156">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="4dae1-157">Wenn Paketliste für die Quelle leer ist, kann nicht hinzugefügt werden über den Benutzeroberflächen-Quelldateien (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="4dae1-157">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="4dae1-158">Irreführende Fehler beim Installieren des Pakets, die zur Entwurfszeit Fassaden - abhängt [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="4dae1-158">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="4dae1-159">Nur erste Quelle - Installation eines Pakets aus PackageManager-Konsole mit der Einstellung "Alle" versucht [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="4dae1-159">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="4dae1-160">Neueste Beta nicht dekomprimieren ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="4dae1-160">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="4dae1-161">VS2015 Absturz beim Start mit sich selbst erstellte NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="4dae1-161">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="4dae1-162">Aktualisierungsbefehl möglicherweise etwas ausführlicher Wenn i bitten Sie ihn abgeschnitten - [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="4dae1-162">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="4dae1-163">VSIX lokal erstellten müssen die DLLs und die Dateien wie der CI-Build.</span><span class="sxs-lookup"><span data-stu-id="4dae1-163">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="4dae1-164"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="4dae1-164"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="4dae1-165">Beheben von NuGet Downgrade für die Warnungen in den Build - [#2396](https://github.com/NuGet/Home/issues/2396)</span><span class="sxs-lookup"><span data-stu-id="4dae1-165">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="4dae1-166">Wegen eines Fehlers beim Paketquelle (3 Mal) authentifizieren forever - blockiert [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="4dae1-166">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="4dae1-167">Paketinhalt wird nicht ordnungsgemäß wiederhergestellt, beim Installieren eines Pakets von Nuget v3. 3 +-mit dem Argument Feeds - NoCache, wenn das Paket enthält `.nupkg` Dateien - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="4dae1-167">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="4dae1-168">NuGet-Installation mit allen Paketquellen überein, aber Paket fehlt in der 1-Quelle und ein Fehler auftritt - [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="4dae1-168">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="4dae1-169">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt; &gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;B__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="4dae1-169">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="4dae1-170">Blöcke zu installieren, schlägt eine einzelne Datenquelle Autorisierung - [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="4dae1-170">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="4dae1-171">`.nuspec`Version Bereich sollten IncludeReferencedProjects - Version - überschreiben [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="4dae1-171">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="4dae1-172">Updatepaket super langsam - "versucht, Abhängigkeiten Informationen sammeln" - [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="4dae1-172">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="4dae1-173">Stealth Downgrades von NuGet-Paket beim Batch aktualisieren seiner Abhängigkeiten - [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="4dae1-173">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="4dae1-174">NuGet.exe Update löscht den starken Assemblynamen und privaten Attribut.</span><span class="sxs-lookup"><span data-stu-id="4dae1-174">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="4dae1-175"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="4dae1-175"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="4dae1-176">Ein relativer Dateipfad für "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="4dae1-176">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="4dae1-177">Verbesserung der Fehlermeldungen Resolver - [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="4dae1-177">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="4dae1-178">Updatepaket in v3 schlägt fehl mit Paketen, die nicht in der angegebenen Quelle - [#1013](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="4dae1-178">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="4dae1-179">Verwenden relative Pfade für Paketquellen ist problematisch verwenden - [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="4dae1-179">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="4dae1-180">Fehlende Abhängigkeit in NUPKG-Datei, die vom Projekt generiert wird, wenn indirekte Abhängigkeit mit einer niedrigeren Version Anforderung bereits - [#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="4dae1-180">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="4dae1-181">Löschen ein Projekt entsprechende UI-Fenster geschlossen, aber Umbenennen eines Projekts im UI-Fenster nicht umbenennen.</span><span class="sxs-lookup"><span data-stu-id="4dae1-181">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="4dae1-182">Beachten Sie, dass das Projekt umbenennen und Projekt entfernen-Ereignisse – PMC überwacht [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="4dae1-182">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="4dae1-183">[Willow Web Arbeitsauslastung] Hängenbleiben erstellen Razor v3 WSP - [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="4dae1-183">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="4dae1-184">Installation/Wiederherstellung eines bestimmten Pakets schlägt fehl mit "enthält Paket mehrere Nuspec-Dateien."</span><span class="sxs-lookup"><span data-stu-id="4dae1-184">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="4dae1-185"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="4dae1-185"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="4dae1-186">Kleinbuchstaben IDs & `packages.config` Szenarien – [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="4dae1-186">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="4dae1-187">[3.5 beta2] Wiederherstellen von "legacy" Paketen - paketwiederherstellung nicht [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="4dae1-187">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="4dae1-188">NuGet-Pack fügt erzwungen TT-Dateien in Inhaltsordner unabhängig davon, was - [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="4dae1-188">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="4dae1-189">Updatepaket von ASP.NET Web-app generiert die Warnung im Zusammenhang mit der Datei: Quelle - [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="4dae1-189">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="4dae1-190">NuGet-Pack Csproj (mit `project.json`) stürzt ab, wenn es keine PackOptions "und" Besitzer in JSON-Datei sind - [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="4dae1-190">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="4dae1-191">NuGet-Pack für `project.json` ignoriert PackOptions Tags wie Zusammenfassung, Autoren und Besitzer usw. - [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="4dae1-191">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="4dae1-192">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="4dae1-192">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="4dae1-193">NuGet-Pack ignoriert Abhängigkeiten in der Ausgabe `.nuspec` für `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="4dae1-193">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="4dae1-194">Aktualisieren mehrere Pakete mit Rollback lässt das Projekt in einem fehlerhaften Zustand versetzt - [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="4dae1-194">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="4dae1-195">Inhaltsdateien unter einer werden nicht hinzugefügt, für die netstandard-Projekte - [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="4dae1-195">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="4dae1-196">Bibliothek für .net Paket kann nicht standardmäßige ordnungsgemäß - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="4dae1-196">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="4dae1-197">Datei -> Neues Projekt-Klassenbibliothek (portabel) Projekt fehl in VS2015 und Dev15 - > [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="4dae1-197">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="4dae1-198">NuGet-Fehler: 1.0.0-\* ist keine gültige Versionszeichenfolge - [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="4dae1-198">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="4dae1-199">Find-Package ein Fehler auftritt, um die Anzeige "," Install-Package Works - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="4dae1-199">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="4dae1-200">Fehler bei "Install-Package jquery.validation" auf dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="4dae1-200">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="4dae1-201">Ungültiger Zielpfad - NuGet-Paket mit Xproj direktionales ist [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="4dae1-201">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="4dae1-202">Bei der installierten Visual Studio 2015 update 3 auf einem VS, die NuGet-Version 3.5.0 Fehlers - verwendet [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="4dae1-202">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="4dae1-203">"Von" Packages.config "blockiert" in `project.json` (UWP, bzw. Build integriert) Projekt - [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="4dae1-203">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="4dae1-204">Aktualisieren Sie Dotnet Cli vom Buildskript auf Preview 2-003121, der offiziellen Preview 2 ist installiert.</span><span class="sxs-lookup"><span data-stu-id="4dae1-204">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="4dae1-205"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="4dae1-205"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="4dae1-206">Paket-Manager-Benutzeroberfläche: keine neue Version angezeigt, nach dem Aktualisieren eines Pakets- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="4dae1-206">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="4dae1-207">-"Apikey" für Delete-Befehlszeile nicht Lese-/gesendet 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="4dae1-207">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="4dae1-208">Falsches Zeichenfolgenformat: eine stabile Version eines Pakets sollte keine für eine Vorabversion Abhängigkeit.</span><span class="sxs-lookup"><span data-stu-id="4dae1-208">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="4dae1-209"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="4dae1-209"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="4dae1-210">OptimizedZipPackage Cache bleibt leere Ordner - [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="4dae1-210">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="4dae1-211">Erstellen PCL (net46 und Windows 10)-Projekt Get NullRef-Ausnahme.</span><span class="sxs-lookup"><span data-stu-id="4dae1-211">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="4dae1-212"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="4dae1-212"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="4dae1-213">NuGet-Update sollten informationsmeldung bereitstellen, wenn eine höhere Version von "allowedversions"-Einschränkung - beschränkt ist [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="4dae1-213">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="4dae1-214">NuGet-v3-Restore-Fehlern – [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="4dae1-214">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="4dae1-215">Anmeldeinformationen-Plug-in wurde mit dem Fehlercode:-1 / Fehler herunterladen bei Verwendung von mehreren Quellen - Anmeldeinformationsanbieter mit package [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="4dae1-215">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="4dae1-216">`project.json`NuGet Restore bewirkt, dass neu kompiliert, wenn nichts geändert - [#2817](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="4dae1-216">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="4dae1-217">Symbole Pakete sollte jemals nicht verwendet werden, in der Installations- oder Update - [#2807](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="4dae1-217">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="4dae1-218">Visual Studio unterstützt keine Umgebungsvariablen im RepositoryPath (nuget.exe bewirkt) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="4dae1-218">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="4dae1-219">Bezeichnen Sie die unbenannten UIElements im Paket-Manager-UI für Eingabehilfen - [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="4dae1-219">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="4dae1-220">Portable Frameworks mit getrennten Profilen werden zurückgewiesen.</span><span class="sxs-lookup"><span data-stu-id="4dae1-220">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="4dae1-221"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="4dae1-221"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="4dae1-222">NuGet-Paket-Manager sollten unmissverständlich, Optionsliste in Paketen Detail nicht für gilt `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="4dae1-222">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="4dae1-223">NuGet.exe Push/Delete nicht API-Schlüssel - verwendet [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="4dae1-223">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="4dae1-224">Entfernen Sie die gesperrte Eigenschaft aus der Sperrdatei - [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="4dae1-224">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="4dae1-225">NuGet 3.3.0 Update schlägt fehl mit "eine weitere Einschränkung... definiert" Packages.config ", verhindert diesen Vorgang."</span><span class="sxs-lookup"><span data-stu-id="4dae1-225">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="4dae1-226"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="4dae1-226"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="4dae1-227">Installieren von einer lokalen Quelle, die löst nicht vorhanden ist eine gefälschte Nachricht - Paket [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="4dae1-227">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="4dae1-228">"Upgrade verfügbar" Filter zeigt Upgrades, die die versionseinschränkung - verletzen [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="4dae1-228">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="4dae1-229">Kann nicht aktualisiert werden systemeigene Pakete - [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="4dae1-229">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="4dae1-230">Features</span><span class="sxs-lookup"><span data-stu-id="4dae1-230">Features</span></span>

* <span data-ttu-id="4dae1-231">Einstellung CopyLocal auf "false" für hinzugefügten von NuGet - Verweise unterstützen [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="4dae1-231">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="4dae1-232">NuGet.exe-Unterstützung für die MSBuild-15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="4dae1-232">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="4dae1-233">Pack-Unterstützung für.`csproj`</span><span class="sxs-lookup"><span data-stu-id="4dae1-233">Pack support for .`csproj`</span></span><span data-ttu-id="4dae1-234"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="4dae1-234"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="4dae1-235">Deaktivieren Sie Handlung des Benutzers aus, wenn es werden Aktionen des Benutzers ausgeführt wird- [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="4dae1-235">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="4dae1-236">Sollte zum Hinzufügen von NuGet-Unterstützung für `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="4dae1-236">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="4dae1-237">Hinzufügen von Framework Kompatibilitäten fehlt in der NuGet 2.x (die bereits in 3.x sind) - [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="4dae1-237">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="4dae1-238">Unterstützung für alternative paketordnern - [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="4dae1-238">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="4dae1-239">Entwerfen und implementieren Sie eine Vorstellung von den Pakettyp Tool Pakete - Unterstützung [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="4dae1-239">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="4dae1-240">Hinzufügen einer API zum Abrufen des Pfads zum Paketordner globalen - [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="4dae1-240">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="4dae1-241">Aktivieren von SemVer 2.0.0 im Paket - [#3356](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="4dae1-241">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="4dae1-242">DCRs</span><span class="sxs-lookup"><span data-stu-id="4dae1-242">DCRs</span></span>

* <span data-ttu-id="4dae1-243">NuGet.exe Push - Timeoutparameter funktioniert nicht – [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="4dae1-243">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="4dae1-244">Beschreibungstext des Pakets muss auswählbare - [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="4dae1-244">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="4dae1-245">Aktivieren Sie nuget.exe erzeugt `.props` und `.targets` Dateien für `.nuproj` Projekte [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="4dae1-245">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="4dae1-246">Hinzufügen von Erweiterbarkeits-API zum Vergleichen von Importen - Frameworks [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="4dae1-246">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="4dae1-247">Abhängigkeitsoptionen ausblenden, wenn mit `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="4dae1-247">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="4dae1-248">Drucken nuget.exe-Versionsheader in ausführliche Ausgabe - [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="4dae1-248">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="4dae1-249">NuGet muss, damit Benutzer wissen, dass ein Upgrade/Installation in ein Dotnet-Tfm basierend PCL Probleme - verursachen könnte [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="4dae1-249">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="4dae1-250">Warnhinweis anzeigen, fehlerhafte installiert oder aktualisiert für das Projekt mit Tfm "Dotnet" - = [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="4dae1-250">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="4dae1-251">Beheben von Leistungsproblemen mit ReShaper und NuGet für Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="4dae1-251">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="4dae1-252">Hinzufügen von netcoreapp11 und netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="4dae1-252">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="4dae1-253">Nutzen der Vorteile AssemblyMetadata-Attribut für `.nuspec` Ersetzungen - token [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="4dae1-253">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
