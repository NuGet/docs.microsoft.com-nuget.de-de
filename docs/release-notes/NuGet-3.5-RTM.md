---
title: Anmerkungen zu Version 3.5 RTM von NuGet
description: Anmerkungen zu dieser Version von nuget 3,5 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776348"
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="02987-103">Anmerkungen zu dieser Version von nuget 3,5</span><span class="sxs-lookup"><span data-stu-id="02987-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="02987-104">Anmerkungen zu dieser [Version von nuget 3,5-RC](../release-notes/nuget-3.5-RC.md)  |  [Anmerkungen zu dieser Version von nuget 4,0 RC](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="02987-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="02987-105">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="02987-105">Bug Fixes</span></span>

* <span data-ttu-id="02987-106">Das Paket verwendet MSBuild 14,1 nicht auf Mono- [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="02987-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="02987-107">Registerkarte "Aktualisieren" wählt nicht die aktuellste verfügbare Version zum Aktualisieren aus. Wählen Sie stattdessen die aktuell installierte [#3498](https://github.com/NuGet/Home/issues/3498) Version</span><span class="sxs-lookup"><span data-stu-id="02987-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="02987-108">Beheben Sie den Absturz nach dem Authentifizieren eines privaten v2-myget-Feeds, und klicken Sie auf "x weitere Ergebnisse anzeigen"- [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="02987-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="02987-109">Protokollmeldungen sind anscheinend in umgekehrter Reihenfolge für die Benutzeroberfläche [#3446](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="02987-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="02987-110">v 3.4.4-nuget-Wiederherstellung löst das Format "das angegebene Pfad Format wird nicht unterstützt"- [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="02987-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="02987-111">Nuget-cmdline 3,6 Beta hat keine Unterstützung für "-prop Configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="02987-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="02987-112">Nuget-Unternehmen: langsame Installation auf einem großen Projekt [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="02987-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="02987-113">nuget.exe Update-Self behält die Aktualisierung selbst bei [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="02987-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="02987-114">3,5 die Installation/Wiederherstellung über die UNC-Freigabe hat eine Leistungs Regression von 3.4.4- [#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="02987-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="02987-115">Fehler beim Installieren von "muq" über die Benutzeroberfläche der Paketverwaltung für ein net451-Projekt [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="02987-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="02987-116">Registerkarte "installieren" auf Projektmappenebene zeigt die Version des Pakets nicht an [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="02987-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="02987-117">xproj- `project.json` Update von installierter Registerkarte verliert Status- [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="02987-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="02987-118">Das nuget-Paket unter `.csproj` ignoriert ein leeres Files-Element in `.nuspec` file- [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="02987-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="02987-119">In IIS gehostete Website Projekte sollten nicht zu einem Fehler bei der Wiederherstellung führen [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="02987-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="02987-120">Anmelde Informationen, die nicht von Nuget.Config abgerufen werden, wenn der V3-Endpunkt zu v2- [#3179](https://github.com/NuGet/Home/issues/3179) umgeleitet</span><span class="sxs-lookup"><span data-stu-id="02987-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="02987-121">Das nuget-Paket kann die Assembly beim Abrufen von portablen Assemblymetadaten nicht auflösen- [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="02987-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="02987-122">Nuget kann `msbuild.exe` auf Mono- [#3085](https://github.com/NuGet/Home/issues/3085) nicht finden</span><span class="sxs-lookup"><span data-stu-id="02987-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="02987-123">nuget.exe Pack lässt kein vorab Veröffentlichungstag zu, das mit Zahlen beginnt [#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="02987-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="02987-124">Fehler beim Installieren des nuget-Pakets auf VS2015E- [#1298](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="02987-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="02987-125">der "Zuweisung-Filter" funktioniert auf Projektmappenebene nicht [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="02987-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="02987-126">Die Wiederherstellung nach dem Zufallsprinzip schlägt fehl, wenn ein Element mit demselben Schlüssel bereits hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="02987-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="02987-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="02987-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="02987-128">Nuget kann nicht installiert werden. common in `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="02987-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="02987-129">Wenn Sie die Benutzeroberfläche zum Durchsuchen einer v2-Quelle verwenden, wird findpackagesbyid für jede ID zweimal aufgerufen [#2517](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="02987-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="02987-130">Pakete können nicht von Projekten abhängen [#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="02987-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="02987-131">nuget.exe Pack-Exclude ist dokumentiert, wird jedoch nicht unterstützt [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="02987-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="02987-132">Probleme mit Fehlermeldungen, wenn der Abschnitt "contentfiles" von `.nuspec` ungültig ist- [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="02987-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="02987-133">Push sendet das gesamte Paket immer zweimal mit den authentifizierten Paketquellen [#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="02987-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="02987-134">Beim Aufrufen von nuget.exe Update \*. csproj wurden keine Informationen angegeben, während das Projekt keine `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="02987-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="02987-135">`packages.config` bei der Wiederherstellung wird der 5XX-Statuscode aus V2-Quellen nicht wiederholt [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="02987-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="02987-136">Der doppelte Punkt in der Datei src in `.nuspec` funktioniert nicht [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="02987-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="02987-137">Die CoreCLR-Wiederherstellung muss Feeds mit Verschlüsselung ignorieren [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="02987-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="02987-138">nuget.exe Push 403-Behandlung-falsche Eingabe von Anmelde Informationen [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="02987-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="02987-139">Das nuget-Update über den Paket-Manager entfernt Eigenschaften aus dem `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="02987-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="02987-140">Nuget. packagemanagement. VisualStudio versucht, "nuget. TeamFoundationServer14" zu laden, aber der DLL-Name wurde in "nuget. TeamFoundationServer" geändert- [#2857](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="02987-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="02987-141">Die Benutzeroberfläche des Paket-Managers zeigt keine neu aktualisierte Version [#2828](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="02987-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="02987-142">Update-Paket versucht, PackageID, Version anstelle von Package. Version- [#2771](https://github.com/NuGet/Home/issues/2771) zu verwenden</span><span class="sxs-lookup"><span data-stu-id="02987-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="02987-143">beim nuget-Wiederherstellungs-csproj sollte ein Fehler auftreten, wenn das Projekt keine nuget `packages.config` -(oder `project.json` )- [#2766](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="02987-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="02987-144">Der TFS-Fehler "[Datei] wurde in Ihrem Arbeitsbereich nicht gefunden, oder Sie haben keine Zugriffsberechtigung" während des Upgrades oder der Deinstallation, wenn Projekt Mappe/Projekt an TFS-Quell Code Verwaltung gebunden ist [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="02987-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="02987-145">Das Update Paket erhält keine Abhängigkeiten von nicht Ziel Paketen- [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="02987-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="02987-146">Es gibt keine Möglichkeit, den ausführlichkeits Grad der Protokolle für UI-Aktionen des nuget-Paket-Managers festzulegen- [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="02987-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="02987-147">die nuget-Konfiguration ist ungültig: vs 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="02987-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="02987-148">Defaultpushsource in `NuGetDefaults.Config` ( `ProgramData\NuGet` ) funktioniert nicht [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="02987-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="02987-149">nuget 3.4.3 Release: der Wert für "Get" darf bei der Paketbuild- [#2648](https://github.com/NuGet/Home/issues/2648) nicht NULL sein</span><span class="sxs-lookup"><span data-stu-id="02987-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="02987-150">RESTORE verwendet keine gespeicherten Anmelde Informationen aus Nuget.Config für VSTS-Feeds [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="02987-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="02987-151">[dotnet Restore]: "configfile" ist relativ zu "Project dir" statt "cmd dir- [#2639](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="02987-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="02987-152">Übermäßige Zuordnungen in Versions Vergleichs Code- [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="02987-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="02987-153">Mehrere Instanzen von nuget.exe versuchen, das gleiche Paket parallel zu installieren, verursachen einen doppelten Schreib [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="02987-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="02987-154">Abhängigkeitsinformationen werden nicht für Vorgänge mit mehreren Projekten zwischengespeichert- [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="02987-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="02987-155">Installieren und Aktualisieren von Download Paketen, ohne den Ordner "Packages" [#2618](https://github.com/NuGet/Home/issues/2618) zuerst zu überprüfen</span><span class="sxs-lookup"><span data-stu-id="02987-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="02987-156">Wenn die Paketquellen Liste leer ist, kann die Paketquelle nicht über die Benutzeroberfläche hinzugefügt werden (nuget 3.4. x)- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="02987-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="02987-157">Irreführender Fehler beim Versuch, ein Paket zu installieren, das von Entwurfszeit Fassaden abhängt [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="02987-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="02987-158">Wenn Sie ein Paket über die packagemanager-Konsole mit der Einstellung "All" installieren, wird nur die erste Quelle [#2557](https://github.com/NuGet/Home/issues/2557) versucht.</span><span class="sxs-lookup"><span data-stu-id="02987-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="02987-159">Die neueste Beta Version entzippt modernhttpclient- [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="02987-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="02987-160">VS2015 stürzt beim Start mit selbst erstellten nuget 3.4.1- [#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="02987-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="02987-161">Der Aktualisierungs Befehl kann etwas ausführlicher sein, wenn ich ihn Anfrage...- [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="02987-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="02987-162">Die lokal erstellten VSIX-Dateien sollten dieselben DLLs und Dateien wie der CI-Build aufweisen.</span><span class="sxs-lookup"><span data-stu-id="02987-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="02987-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="02987-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="02987-164">Beheben von nuget-Downgrade-Warnungen im Build- [#2396](https://github.com/NuGet/Home/issues/2396)</span><span class="sxs-lookup"><span data-stu-id="02987-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="02987-165">Fehler beim Authentifizieren der Paketquelle (dreimal) ist dauerhaft blockiert- [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="02987-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="02987-166">Der Paket Inhalt wird bei der Installation eines Pakets aus einem nuget v 3.3 +-Feed mit dem Argument NoCache, wenn das Paketdateien enthält, nicht ordnungsgemäß wieder hergestellt `.nupkg` [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="02987-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="02987-167">Nuget-Installation mit allen Paketquellen, aber ein Paket fehlt in 1 Quelle, schlägt fehl [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="02987-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="02987-168">[Perfwatson] Uidelay: nuget.packagemanagement.visualstudio.dll! Nuget. packagemanagement. VisualStudio. vsmsbuildnugetprojectsystem + \* lt; &gt; c__DisplayClass_0 + &lt; &lt; adressenz &gt; b__ &gt; d. [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="02987-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="02987-169">Installations Blöcke, wenn eine einzelne Quelle die Autorisierung nicht besteht- [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="02987-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="02987-170">`.nuspec`Versions Bereich sollte-includereferencedprojects Version- [#1983](https://github.com/NuGet/Home/issues/1983) überschreiben</span><span class="sxs-lookup"><span data-stu-id="02987-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="02987-171">Update-Package super langsam: "Es wird versucht, Abhängigkeitsinformationen zu erfassen"- [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="02987-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="02987-172">Nuget-Paket für das herunter Skalierungen von Batches beim Aktualisieren der Abhängigkeiten von Batch- [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="02987-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="02987-173">nuget.exe Update löscht den starken Namen der Assembly und das private-Attribut.</span><span class="sxs-lookup"><span data-stu-id="02987-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="02987-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="02987-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="02987-175">Relativer Dateipfad für "defaultpushsource"- [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="02987-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="02987-176">Verbessern von Auflösungs Fehlermeldungen- [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="02987-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="02987-177">Update-Package in V3 schlägt fehl, wenn Pakete nicht in der angegebenen Quelle [#1013](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="02987-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="02987-178">Die Verwendung relativer Pfade für Paketquellen ist problematisch für die Verwendung- [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="02987-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="02987-179">Fehlende Abhängigkeit in der vom Projekt generierten nupkg-Datei, wenn die indirekte Abhängigkeit bereits mit einer niedrigeren Versions Anforderung vorhanden ist [#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="02987-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="02987-180">Wenn Sie ein Projekt löschen, wird das zugehörige Benutzeroberflächen Fenster geschlossen, aber beim Umbenennen eines Projekts wird das Benutzeroberflächen Fenster nicht umbenannt</span><span class="sxs-lookup"><span data-stu-id="02987-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="02987-181">Beachten Sie, dass die PMC auf Projekt Umbenennungen und Projekt Entfernungs Ereignisse lauscht [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="02987-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="02987-182">[Willow Web-Arbeitsauslastung] Erstellen von Razor V3-WSP-hängen- [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="02987-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="02987-183">Die Installation/Wiederherstellung eines bestimmten Pakets schlägt fehl, wenn "Paket enthält mehrere nuspec-Dateien".</span><span class="sxs-lookup"><span data-stu-id="02987-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="02987-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="02987-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="02987-185">& Szenarios für Kleinbuchstaben `packages.config` - [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="02987-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="02987-186">[3,5-Beta2] Bei der Paket Wiederherstellung können "Legacy Pakete" nicht wieder hergestellt werden [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="02987-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="02987-187">Das nuget-Paket fügt die TT-Dateien in einem Inhalts Ordner hinzu, unabhängig davon, was [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="02987-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="02987-188">Update-Package of ASP.net Web App generiert eine Warnung im Zusammenhang mit der Datei: Quelle- [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="02987-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="02987-189">Das nuget-Paket "csproj" (mit `project.json` ) stürzt ab, wenn keine packoptions und Besitzer in der JSON-Datei vorhanden sind [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="02987-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="02987-190">Das nuget-Paket für `project.json` ignoriert packoptions-Tags wie Zusammenfassung, Autoren, Besitzer usw.- [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="02987-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="02987-191">NullReferenceException über nuget. Packaging. physicalpackagefile. GetStream- [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="02987-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="02987-192">Das nuget-Paket ignoriert Abhängigkeiten in der Ausgabe `.nuspec` für `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="02987-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="02987-193">Wenn Sie mehrere Pakete mit Rollback aktualisieren, bleibt das Projekt in einem unterbrochenen Zustand [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="02987-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="02987-194">"Contentfiles" unter "Any" wird nicht für netstandard-Projekte hinzugefügt- [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="02987-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="02987-195">Die Bibliothek für .NET Standard kann nicht ordnungsgemäß [#3108](https://github.com/NuGet/Home/issues/3108) werden.</span><span class="sxs-lookup"><span data-stu-id="02987-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="02987-196">Datei > neues Projekt > Klassenbibliothek (portabel) schlägt in VS2015 und Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="02987-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="02987-197">der nuget-Fehler-1.0.0-\* ist keine gültige Versions Zeichenfolge [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="02987-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="02987-198">Find-Package kann nicht angezeigt werden, aber Install-Package Works- [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="02987-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="02987-199">Fehler bei "Install-package jQuery. Validation" auf dev15- [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="02987-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="02987-200">Das nuget-Paket von xproj ist standardmäßig auf einen ungültigen Zielpfad [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="02987-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="02987-201">Bei der Installation von vs 2015 Update 3 auf einem vs, der die nuget-Version verwendet 3.5.0 Fehler tritt auf [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="02987-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="02987-202">"Blockiert durch packages.config" in `project.json` (UWP, a. k. a Build Integrated) Project- [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="02987-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="02987-203">Aktualisieren Sie die dotnet-CLI, die vom Buildskript installiert wurde, auf Preview2-003121, also den offiziellen Preview2-Build.</span><span class="sxs-lookup"><span data-stu-id="02987-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="02987-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="02987-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="02987-205">Benutzeroberfläche des Paket-Managers: zeigt keine neue Version nach dem Aktualisieren eines Pakets an [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="02987-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="02987-206">-APIKey in der Befehlszeile "Delete" wird in 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037) nicht gelesen/gesendet</span><span class="sxs-lookup"><span data-stu-id="02987-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="02987-207">Falsche Zeichenfolge: ein stabiles Release eines Pakets sollte nicht für eine vorab Abhängigkeit vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="02987-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="02987-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="02987-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="02987-209">Der optimizedzippackage-Cache verlässt leere Ordner- [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="02987-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="02987-210">Beim Erstellen des Projekts PCL ("net46 und Windows 10) wird die Ausnahme NullRef-Ausnahme zurückerhalten.</span><span class="sxs-lookup"><span data-stu-id="02987-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="02987-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="02987-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="02987-212">Das nuget-Update sollte eine informative Nachricht bereitstellen, wenn eine höhere Version durch die Einschränkung der Einschränkung-Version eingeschränkt ist [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="02987-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="02987-213">Probleme beim Wiederherstellen von nuget V3- [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="02987-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="02987-214">Das Anmelde Informations-Plug-in wurde mit Fehler-1/Fehler beim Herunterladen des Pakets beendet, wenn Anmelde Informationsanbieter mit mehreren Quellen verwendet werden [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="02987-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="02987-215">`project.json`die nuget [#2817](https://github.com/NuGet/Home/issues/2817) -Wiederherstellung verursacht eine Neukompilierung, wenn nichts geändert wurde</span><span class="sxs-lookup"><span data-stu-id="02987-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="02987-216">Symbol Pakete sollten nicht jemals in install-oder Update- [#2807](https://github.com/NuGet/Home/issues/2807) verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="02987-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="02987-217">VS unterstützt keine Umgebungsvariablen in repositoryPath (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="02987-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="02987-218">Bezeichnen Sie die unbezeichneten UIElements in der Benutzeroberfläche des Paket-Managers für Barrierefreiheit- [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="02987-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="02987-219">Portable Frameworks mit mittels Bindestrich-Profilen werden abgelehnt.</span><span class="sxs-lookup"><span data-stu-id="02987-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="02987-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="02987-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="02987-221">Der nuget-Paket-Manager sollte deutlich machen, dass die Optionsliste in Paket Details nicht für `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="02987-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="02987-222">nuget.exe Push/DELETE verwendet keinen API-Schlüssel [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="02987-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="02987-223">Entfernen Sie die gesperrte Eigenschaft aus der Sperrdatei [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="02987-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="02987-224">Nuget 3.3.0 Update schlägt mit einer zusätzlichen Einschränkung fehl... der in packages.config definierte Vorgang wird verhindert.</span><span class="sxs-lookup"><span data-stu-id="02987-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="02987-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="02987-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="02987-226">Das Installieren eines Pakets aus einer lokalen Quelle, die nicht vorhanden ist, löst eine falsche Nachricht aus [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="02987-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="02987-227">Filter "Upgrade available" zeigt Upgrades an, die gegen die Versions Einschränkung verstoßen- [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="02987-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="02987-228">Systemeigene Pakete können nicht aktualisiert werden- [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="02987-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="02987-229">Features</span><span class="sxs-lookup"><span data-stu-id="02987-229">Features</span></span>

* <span data-ttu-id="02987-230">Unterstützung beim Festlegen von CopyLocal auf false bei von nuget- [#329](https://github.com/NuGet/Home/issues/329) hinzugefügten verweisen</span><span class="sxs-lookup"><span data-stu-id="02987-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="02987-231">nuget.exe-Unterstützung für MSBuild 15- [#1937](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="02987-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="02987-232">Paket Unterstützung für.`csproj`</span><span class="sxs-lookup"><span data-stu-id="02987-232">Pack support for .`csproj`</span></span><span data-ttu-id="02987-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="02987-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="02987-234">Benutzeraktion deaktivieren, wenn Benutzeraktionen ausgeführt werden [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="02987-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="02987-235">Nuget sollte Unterstützung für `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782) hinzufügen</span><span class="sxs-lookup"><span data-stu-id="02987-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="02987-236">Hinzufügen von frameworkkompatibilitäten, die in nuget 2. x fehlen (die bereits in 3. x vorhanden sind): [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="02987-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="02987-237">Unterstützung für Fall Back Paket Ordner- [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="02987-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="02987-238">Entwerfen und implementieren Sie ein Konzept des Pakettyps, um Tool Pakete zu unterstützen- [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="02987-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="02987-239">Fügen Sie eine API hinzu, um den Pfad zum Ordner für globale Pakete zu erhalten [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="02987-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="02987-240">Semver 2.0.0 in Pack- [#3356](https://github.com/NuGet/Home/issues/3356) aktivieren</span><span class="sxs-lookup"><span data-stu-id="02987-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="02987-241">DCRs</span><span class="sxs-lookup"><span data-stu-id="02987-241">DCRs</span></span>

* <span data-ttu-id="02987-242">nuget.exe Push-Timeout-Parameter funktioniert nicht [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="02987-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="02987-243">Der Paket Beschreibungstext sollte auswählbar sein- [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="02987-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="02987-244">Aktivieren Sie nuget.exe, um `.props` -und- `.targets` Dateien für Projekte zu entwickeln `.nuproj` [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="02987-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="02987-245">Hinzufügen der Erweiterbarkeits-API zum Vergleichen von Frameworks mit Importen- [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="02987-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="02987-246">Abhängigkeits Optionen beim Verwenden von `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486) ausblenden</span><span class="sxs-lookup"><span data-stu-id="02987-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="02987-247">Ausgabe nuget.exe Versions Headers in detaillierter Ausgabe [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="02987-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="02987-248">Nuget muss den Benutzern mitteilen, dass ein Upgrade/Installation in einer dotnet TFM-basierten PCL Probleme verursachen könnte [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="02987-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="02987-249">Warnung bei fehlerhafter Installation/Upgrade für Projekt w/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="02987-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="02987-250">Beheben von Leistungsproblemen mit reshaper und nuget für Update- [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="02987-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="02987-251">Netcoreapp11-und netstandard17-Unterstützung hinzufügen- [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="02987-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="02987-252">Verwenden des ASSEMBLYMETADATA-Attributs für `.nuspec` tokenersetzungen- [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="02987-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
