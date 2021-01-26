---
title: Anmerkungen zu dieser Version von nuget 5,5
description: Anmerkungen zu dieser Version von nuget 5,5, einschließlich neuer Features, Fehlerbehebungen und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0fde67dd03c31e986ed89f2f8627608e279ef908
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780112"
---
# <a name="nuget-55-release-notes"></a><span data-ttu-id="e512d-103">Anmerkungen zu dieser Version von nuget 5,5</span><span class="sxs-lookup"><span data-stu-id="e512d-103">NuGet 5.5 Release Notes</span></span>

<span data-ttu-id="e512d-104">Möglichkeiten der NuGet-Verteilung:</span><span class="sxs-lookup"><span data-stu-id="e512d-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="e512d-105">NuGet-Version</span><span class="sxs-lookup"><span data-stu-id="e512d-105">NuGet version</span></span> | <span data-ttu-id="e512d-106">Verfügbar in der Visual Studio-Version</span><span class="sxs-lookup"><span data-stu-id="e512d-106">Available in Visual Studio version</span></span>| <span data-ttu-id="e512d-107">Verfügbar in .NET SDK(s)</span><span class="sxs-lookup"><span data-stu-id="e512d-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="e512d-108">**5.5.0**</span><span class="sxs-lookup"><span data-stu-id="e512d-108">**5.5.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="e512d-109">Visual Studio 2019 Version 16.5</span><span class="sxs-lookup"><span data-stu-id="e512d-109">Visual Studio 2019 version 16.5</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="e512d-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="e512d-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="e512d-111"><sup>1</sup> Installiert mit Visual Studio 2019 mit .net Core-Arbeitsauslastung</span><span class="sxs-lookup"><span data-stu-id="e512d-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-55"></a><span data-ttu-id="e512d-112">Zusammenfassung: Neues in 5,5</span><span class="sxs-lookup"><span data-stu-id="e512d-112">Summary: What's New in 5.5</span></span>

* <span data-ttu-id="e512d-113">Verbesserte Barrierefreiheit und Bildschirm Lesefunktion für die Benutzeroberfläche des nuget-Paket-Managers in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e512d-113">Improved accessibility and screen reader experience for the NuGet package manager UI in Visual Studio</span></span>
    * <span data-ttu-id="e512d-114">Barrierefreiheits Probleme bei der Bildschirm Lese Umgebung, fehlende AltText-und barrierefreie Namen für installierte TextBox,- [#9059](https://github.com/NuGet/Home/issues/9059)</span><span class="sxs-lookup"><span data-stu-id="e512d-114">Accessibility issues in Screen Reader experiences, missing altText and accessible name for Installed textbox, etc., - [#9059](https://github.com/NuGet/Home/issues/9059)</span></span>
    * <span data-ttu-id="e512d-115">Barrierefreiheits Probleme in der Sprachausgabe in der Paketliste- [#9077](https://github.com/NuGet/Home/issues/9077)</span><span class="sxs-lookup"><span data-stu-id="e512d-115">Accessibility issues in Screen Reader experiences in Packages List - [#9077](https://github.com/NuGet/Home/issues/9077)</span></span>
    * <span data-ttu-id="e512d-116">Barrierefreiheits Probleme im Zusammenhang mit "Durchsuchen", "installieren", "Aktualisieren"-Registerkarten- [#9078](https://github.com/NuGet/Home/issues/9078)</span><span class="sxs-lookup"><span data-stu-id="e512d-116">Accessibility issues in Screen Reader experiences related to "browse","install","update" Tabs - [#9078](https://github.com/NuGet/Home/issues/9078)</span></span>
    * <span data-ttu-id="e512d-117">Die Sprachausgabe gibt keine Link Bezeichnung "blank", "No Dependencies", "nuget. org", "mit" an [#9157](https://github.com/NuGet/Home/issues/9157)</span><span class="sxs-lookup"><span data-stu-id="e512d-117">Narrator does not announce "Blank","No Dependencies","nuget.org","MIT" link label [#9157](https://github.com/NuGet/Home/issues/9157)</span></span>

* <span data-ttu-id="e512d-118">Unterstützung für eigenständige Symbole in der Visual Studio-Paket-Manager-Benutzeroberfläche für Pakete, die auf lokalen Feeds gehostet werden [#8189](https://github.com/NuGet/Home/issues/8189)</span><span class="sxs-lookup"><span data-stu-id="e512d-118">Support for surfacing self-contained icons in Visual Studio package manager UI for packages hosted on local feeds - [#8189](https://github.com/NuGet/Home/issues/8189)</span></span>

* <span data-ttu-id="e512d-119">Erheblich verbesserte Leistung bei der nicht-op `RestoreUseStaticGraphEvaluation` -Wiederherstellung, bei der Auswertungen durch Aufrufen von MSBuild static Graph APIs- [8791](https://github.com/NuGet/Home/issues/8791) beschleunigt werden.</span><span class="sxs-lookup"><span data-stu-id="e512d-119">Significantly improved no-op restore performance using `RestoreUseStaticGraphEvaluation` which speeds up evaluations by calling MSBuild Static Graph APIs - [8791](https://github.com/NuGet/Home/issues/8791)</span></span>

* <span data-ttu-id="e512d-120">Verbesserte dotnet.exe Zuverlässigkeit durch plattformübergreifende Authentifizierungs-Plug-ins</span><span class="sxs-lookup"><span data-stu-id="e512d-120">Improved dotnet.exe reliability with cross-platform authentication plugins</span></span>
    * <span data-ttu-id="e512d-121">DotNet Restore Fehler mit "TaskCanceledException- [#7842](https://github.com/NuGet/Home/issues/7842)</span><span class="sxs-lookup"><span data-stu-id="e512d-121">dotnet restore failing with TaskCanceledException - [#7842](https://github.com/NuGet/Home/issues/7842)</span></span>
    * <span data-ttu-id="e512d-122">Plug-in: "eine Aufgabe wurde abgebrochen": Problem bei der ADO-Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="e512d-122">Plugin:  "A task was cancelled" - problem with ADO authentication due to this.</span></span><span data-ttu-id="e512d-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span><span class="sxs-lookup"><span data-stu-id="e512d-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span></span>

* <span data-ttu-id="e512d-124">`dotnet nuget <add|remove|update|disable|enable|list> source`Befehls [#4126](https://github.com/NuGet/Home/issues/4126) hinzufügen</span><span class="sxs-lookup"><span data-stu-id="e512d-124">add `dotnet nuget <add|remove|update|disable|enable|list> source` command - [#4126](https://github.com/NuGet/Home/issues/4126)</span></span>

* <span data-ttu-id="e512d-125">Suport für die `--skip-duplicate`  Verwendung von dotnet nuget Push- [#8778](https://github.com/NuGet/Home/issues/8778)</span><span class="sxs-lookup"><span data-stu-id="e512d-125">Suport for `--skip-duplicate`  using dotnet nuget push - [#8778](https://github.com/NuGet/Home/issues/8778)</span></span>

* <span data-ttu-id="e512d-126">Unterstützung `packages.config` mit MSBuild/Restore- [#8506](https://github.com/NuGet/Home/issues/8506)</span><span class="sxs-lookup"><span data-stu-id="e512d-126">Support `packages.config` with msbuild /restore - [#8506](https://github.com/NuGet/Home/issues/8506)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="e512d-127">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="e512d-127">Issues fixed in this release</span></span>

<span data-ttu-id="e512d-128">**Fehler**</span><span class="sxs-lookup"><span data-stu-id="e512d-128">**Bugs**</span></span>

* <span data-ttu-id="e512d-129">Self-Updater mit v3-APIs neu arbeiten- [#4197](https://github.com/NuGet/Home/issues/4197)</span><span class="sxs-lookup"><span data-stu-id="e512d-129">Rework Self-Updater with V3 Apis - [#4197](https://github.com/NuGet/Home/issues/4197)</span></span>

* <span data-ttu-id="e512d-130">Falsche Paket Abhängigkeits Version, wenn die Version der Paketabhängigkeit auf "\*" festgelegt ist [#6697](https://github.com/NuGet/Home/issues/6697)</span><span class="sxs-lookup"><span data-stu-id="e512d-130">Wrong package dependency version If package dependency version is set to '\*' - [#6697](https://github.com/NuGet/Home/issues/6697)</span></span>

* <span data-ttu-id="e512d-131">Errorunsafepackageentry-Fehlermeldung verweist nicht auf die Ursache des Problems [#7505](https://github.com/NuGet/Home/issues/7505)</span><span class="sxs-lookup"><span data-stu-id="e512d-131">ErrorUnsafePackageEntry error message is not pointing to source of problem - [#7505](https://github.com/NuGet/Home/issues/7505)</span></span>

* <span data-ttu-id="e512d-132">Die Sperrdatei wird in "\*"-Szenarios nicht berücksichtigt [#8073](https://github.com/NuGet/Home/issues/8073)</span><span class="sxs-lookup"><span data-stu-id="e512d-132">Lock file is not honored in "\*" scenarios  - [#8073](https://github.com/NuGet/Home/issues/8073)</span></span>

* <span data-ttu-id="e512d-133">NuGet.exe wird nicht in die neueste Version eines Pakets aufgelöst, wenn \* in packagereferenziert wird (MSBuild/dotnet/vs Restore do)- [#8432](https://github.com/NuGet/Home/issues/8432)</span><span class="sxs-lookup"><span data-stu-id="e512d-133">NuGet.exe does not resolve to the latest version of a package when using \* in PackageReference (MSBuild/Dotnet/VS restore do) - [#8432](https://github.com/NuGet/Home/issues/8432)</span></span>

* <span data-ttu-id="e512d-134">DotNet List-Paket mit Multi-Ziel-WPF-Projekt [#8463](https://github.com/NuGet/Home/issues/8463)</span><span class="sxs-lookup"><span data-stu-id="e512d-134">dotnet list package with multi targeting WPF project - [#8463](https://github.com/NuGet/Home/issues/8463)</span></span>

* <span data-ttu-id="e512d-135">Verbessern der hilfsdienstprogramme (CPU-Auslastung verringern)- [#8653](https://github.com/NuGet/Home/issues/8653)</span><span class="sxs-lookup"><span data-stu-id="e512d-135">Improve ConcurrencyUtilities (reduce CPU usage) - [#8653](https://github.com/NuGet/Home/issues/8653)</span></span>

* <span data-ttu-id="e512d-136">Die DG-Spezifikation für entladene Projekt Szenarien sollte nicht in der Vorschau Wiederherstellung geschrieben werden- [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="e512d-136">DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="e512d-137">Die Visual Studio nuget-Pakete (restoremanagerpackage) müssen automatisch für projektmappenbuildereignisse geladen werden [#8796](https://github.com/NuGet/Home/issues/8796)</span><span class="sxs-lookup"><span data-stu-id="e512d-137">The Visual Studio NuGet packages (RestoreManagerPackage) needs to auto load on solution build events - [#8796](https://github.com/NuGet/Home/issues/8796)</span></span>

* <span data-ttu-id="e512d-138">Deadlock in VSSETTINGS init- [#8842](https://github.com/NuGet/Home/issues/8842)</span><span class="sxs-lookup"><span data-stu-id="e512d-138">Deadlock in VSSettings init - [#8842](https://github.com/NuGet/Home/issues/8842)</span></span>

* <span data-ttu-id="e512d-139">Die VisualStudio-Toolbox wird nicht aus einem nuget-Paket aufgefüllt, wenn ein Projekt in einem Projektmappenordner abgelegt wird [#8868](https://github.com/NuGet/Home/issues/8868)</span><span class="sxs-lookup"><span data-stu-id="e512d-139">VisualStudio ToolBox is not populated from a NuGet package if a project is placed in a solution folder - [#8868](https://github.com/NuGet/Home/issues/8868)</span></span>

* <span data-ttu-id="e512d-140">VS: Fehler bei der Wiederherstellung der Lösung aufgrund von Racebedingungen: [#8881](https://github.com/NuGet/Home/issues/8881)</span><span class="sxs-lookup"><span data-stu-id="e512d-140">VS:  solution restore perpetually fails due to race condition - [#8881](https://github.com/NuGet/Home/issues/8881)</span></span>

* <span data-ttu-id="e512d-141">Konstante "wird geladen.." auf der Registerkarte "installiert" und "suchen</span><span class="sxs-lookup"><span data-stu-id="e512d-141">Constant "loading.." on installed tab, and "searching</span></span> <term><span data-ttu-id="e512d-142">.. "auf der Registerkarte" Updates "- [#8890](https://github.com/NuGet/Home/issues/8890)</span><span class="sxs-lookup"><span data-stu-id="e512d-142">.." on updates tab - [#8890](https://github.com/NuGet/Home/issues/8890)</span></span>

* <span data-ttu-id="e512d-143">Fehlende eingebettete Symbole in der vs-pm-Benutzeroberfläche nach Ablauf des Caches- [#9069](https://github.com/NuGet/Home/issues/9069)</span><span class="sxs-lookup"><span data-stu-id="e512d-143">Missing Embedded Icons in VS PM UI after cache expires - [#9069](https://github.com/NuGet/Home/issues/9069)</span></span>

* <span data-ttu-id="e512d-144">Start der PM-Benutzeroberfläche starten- [#9112](https://github.com/NuGet/Home/issues/9112)</span><span class="sxs-lookup"><span data-stu-id="e512d-144">FireAndForget PM UI startup - [#9112](https://github.com/NuGet/Home/issues/9112)</span></span>

* <span data-ttu-id="e512d-145">Restore: die includebug. include (...)-Implementierung ist falsch [#9167](https://github.com/NuGet/Home/issues/9167)</span><span class="sxs-lookup"><span data-stu-id="e512d-145">Restore: IncludeExcludeFiles.Equals(...) implementation is incorrect - [#9167](https://github.com/NuGet/Home/issues/9167)</span></span>

* <span data-ttu-id="e512d-146">Restore: packagespec. Clone () erstellt ungleiche Klon- [#9211](https://github.com/NuGet/Home/issues/9211)</span><span class="sxs-lookup"><span data-stu-id="e512d-146">Restore: PackageSpec.Clone() creates unequal clone - [#9211](https://github.com/NuGet/Home/issues/9211)</span></span>

* <span data-ttu-id="e512d-147">Die Fehlerliste wird angezeigt, wenn die Option "immer Fehlerliste anzeigen, wenn der Build mit Fehlern abgeschlossen ist" nicht aktiviert ist [#8190](https://github.com/NuGet/Home/issues/8190)</span><span class="sxs-lookup"><span data-stu-id="e512d-147">Error list shown although "Always show Error List if build finishes with errors" is not checked - [#8190](https://github.com/NuGet/Home/issues/8190)</span></span>

* <span data-ttu-id="e512d-148">Die statische Graph-Wiederherstellung sollte kein leeres SolutionPath- [#9061](https://github.com/NuGet/Home/issues/9061) bestehen.</span><span class="sxs-lookup"><span data-stu-id="e512d-148">Static Graph restore should not pass empty SolutionPath - [#9061](https://github.com/NuGet/Home/issues/9061)</span></span>

* <span data-ttu-id="e512d-149">Restore: für jedes Projekt 4 mal berechnete Abschlüsse- [#9042](https://github.com/NuGet/Home/issues/9042)</span><span class="sxs-lookup"><span data-stu-id="e512d-149">Restore: closure computed for each project 4 times - [#9042](https://github.com/NuGet/Home/issues/9042)</span></span>

* <span data-ttu-id="e512d-150">Restore: dependencygraphspec. Load (...) benötigt keine jobject- [#9040](https://github.com/NuGet/Home/issues/9040)</span><span class="sxs-lookup"><span data-stu-id="e512d-150">Restore: DependencyGraphSpec.Load(...) does not need JObject - [#9040](https://github.com/NuGet/Home/issues/9040)</span></span>

* <span data-ttu-id="e512d-151">Restore: große Zeichen folgen, die auf dem großen Objekt Heap (Loh) erstellt wurden, [#9031](https://github.com/NuGet/Home/issues/9031)</span><span class="sxs-lookup"><span data-stu-id="e512d-151">Restore: large strings created on large object heap (LOH) - [#9031](https://github.com/NuGet/Home/issues/9031)</span></span>

* <span data-ttu-id="e512d-152">Benutzerdefinierte nuget.exe in neuerem Mono kann aufgrund des MSBuild-SDK-Resolvers unterbrechen- [8848](https://github.com/NuGet/Home/issues/8848)</span><span class="sxs-lookup"><span data-stu-id="e512d-152">Custom nuget.exe on newer mono might break due to the MSBuild SDK Resolver - [8848](https://github.com/NuGet/Home/issues/8848)</span></span>

* <span data-ttu-id="e512d-153">Restore schlägt fehl, wenn nuget.dgspec.json "von einem anderen Prozess verwendet wird"- [8692](https://github.com/NuGet/Home/issues/8692)</span><span class="sxs-lookup"><span data-stu-id="e512d-153">restore fails when nuget.dgspec.json is "used by another process" - [8692](https://github.com/NuGet/Home/issues/8692)</span></span>

<span data-ttu-id="e512d-154">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="e512d-154">**DCRs**</span></span>

* <span data-ttu-id="e512d-155">Die Logik in _GetRestoreProjectStyle sollte in einer Aufgabe [#8804](https://github.com/NuGet/Home/issues/8804)</span><span class="sxs-lookup"><span data-stu-id="e512d-155">Logic in _GetRestoreProjectStyle should be in a task - [#8804](https://github.com/NuGet/Home/issues/8804)</span></span>

* <span data-ttu-id="e512d-156">Standardmäßig veraltete Informationen auf der Registerkarte "installiert" hinzufügen [#8541](https://github.com/NuGet/Home/issues/8541)</span><span class="sxs-lookup"><span data-stu-id="e512d-156">Add deprecation information by default on the installed tab - [#8541](https://github.com/NuGet/Home/issues/8541)</span></span>

<span data-ttu-id="e512d-157">**[Liste aller Probleme, die in dieser Version behoben wurden: 5,5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span><span class="sxs-lookup"><span data-stu-id="e512d-157">**[List of all issues fixed in this release - 5.5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span></span>
