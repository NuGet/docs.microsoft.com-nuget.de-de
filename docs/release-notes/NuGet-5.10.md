---
title: Versionshinweise zu NuGet 5.10
description: Versionshinweise für NuGet 5.10, einschließlich neuer Features, Fehlerbehebungen und DCRs.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356498"
---
# <a name="nuget-510-release-notes"></a><span data-ttu-id="e1a48-103">Versionshinweise zu NuGet 5.10</span><span class="sxs-lookup"><span data-stu-id="e1a48-103">NuGet 5.10 Release Notes</span></span>

<span data-ttu-id="e1a48-104">Möglichkeiten der NuGet-Verteilung:</span><span class="sxs-lookup"><span data-stu-id="e1a48-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="e1a48-105">NuGet-Version</span><span class="sxs-lookup"><span data-stu-id="e1a48-105">NuGet version</span></span> | <span data-ttu-id="e1a48-106">Verfügbar in der Visual Studio-Version</span><span class="sxs-lookup"><span data-stu-id="e1a48-106">Available in Visual Studio version</span></span> | <span data-ttu-id="e1a48-107">Verfügbar in .NET SDK(s)</span><span class="sxs-lookup"><span data-stu-id="e1a48-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="e1a48-108">**5.10.0**</span><span class="sxs-lookup"><span data-stu-id="e1a48-108">**5.10.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="e1a48-109">Visual Studio 2019 Version 16.10</span><span class="sxs-lookup"><span data-stu-id="e1a48-109">Visual Studio 2019 version 16.10</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="e1a48-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="e1a48-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |

<span data-ttu-id="e1a48-111"><sup>1</sup> Installiert mit Visual Studio 2019 mit .NET Core-Workload</span><span class="sxs-lookup"><span data-stu-id="e1a48-111"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>
  
> [!NOTE]
> <span data-ttu-id="e1a48-112">Visual Studio 16.10, MSBuild 16.10 und .NET 5.0.300 und höher erfordert NuGet.exe 5.10 oder höher.</span><span class="sxs-lookup"><span data-stu-id="e1a48-112">Visual Studio 16.10, MSBuild 16.10, and .NET 5.0.300+ requires NuGet.exe 5.10 or later.</span></span>

## <a name="summary-whats-new-in-510"></a><span data-ttu-id="e1a48-113">Zusammenfassung: Neuerungen in 5.10</span><span class="sxs-lookup"><span data-stu-id="e1a48-113">Summary: What's New in 5.10</span></span>

* <span data-ttu-id="e1a48-114">Signierung: Implementieren des Befehls dotnet trusted-signers [– #8053](https://github.com/NuGet/Home/issues/8053)</span><span class="sxs-lookup"><span data-stu-id="e1a48-114">Signing: implement dotnet trusted-signers command - [#8053](https://github.com/NuGet/Home/issues/8053)</span></span>

* <span data-ttu-id="e1a48-115">Deaktivieren der Standardvalidierung unter Linux, aber standardmäßig unter Windows aktiviert – [#10713](https://github.com/NuGet/Home/issues/10713)</span><span class="sxs-lookup"><span data-stu-id="e1a48-115">Make default validation disabled on Linux, but enabled by default on Windows - [#10713](https://github.com/NuGet/Home/issues/10713)</span></span>

* <span data-ttu-id="e1a48-116">Hinzufügen einer ENV-Variablen für die Überprüfung der Paketsignierung unter .NET 5 und linux/MAC – [#10742](https://github.com/NuGet/Home/issues/10742)</span><span class="sxs-lookup"><span data-stu-id="e1a48-116">Add an ENV Variable for Package Signing Verification on .NET 5+ Linux/MAC - [#10742](https://github.com/NuGet/Home/issues/10742)</span></span>

* <span data-ttu-id="e1a48-117">Verbessern der Leistung bei der Installation neuer Pakete für große Lösungen [– #10166](https://github.com/NuGet/Home/issues/10166)</span><span class="sxs-lookup"><span data-stu-id="e1a48-117">Improve install new package performance for large solutions - [#10166](https://github.com/NuGet/Home/issues/10166)</span></span>

* <span data-ttu-id="e1a48-118">Fügen Sie den Projekttyp `nfproj` der Liste der unterstütztenProjectExtensions für die NuGet CLI hinzu.</span><span class="sxs-lookup"><span data-stu-id="e1a48-118">Add the project type `nfproj` to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="e1a48-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="e1a48-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="e1a48-120">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="e1a48-120">Issues fixed in this release</span></span>

* <span data-ttu-id="e1a48-121">Unterdrücken des <requireLicenseAcceptance> Elements beim Packen eines Projekts [– #5133](https://github.com/NuGet/Home/issues/5133)</span><span class="sxs-lookup"><span data-stu-id="e1a48-121">Suppress the <requireLicenseAcceptance> element when packing a project - [#5133](https://github.com/NuGet/Home/issues/5133)</span></span>

* <span data-ttu-id="e1a48-122">[CPVM] Vorschauwarnung sollte auf dotnet cli angezeigt werden – [#10226](https://github.com/NuGet/Home/issues/10226)</span><span class="sxs-lookup"><span data-stu-id="e1a48-122">[CPVM] preview warning should be shown on dotnet cli - [#10226](https://github.com/NuGet/Home/issues/10226)</span></span>

* <span data-ttu-id="e1a48-123">Aktualisieren Sie die Hintergrund- und Vordergrundfarbtoken der PMUI auf CommonDocumentColors [– #10608](https://github.com/NuGet/Home/issues/10608)</span><span class="sxs-lookup"><span data-stu-id="e1a48-123">Update the background and foreground color tokens of the PMUI to CommonDocumentColors - [#10608](https://github.com/NuGet/Home/issues/10608)</span></span>

* <span data-ttu-id="e1a48-124">[Fehler Bash] Fehler "Vorgang vom Benutzer abgebrochen" wird im Fenster Fehlerliste angezeigt, wenn auf der PM-Benutzeroberfläche schnell zwischen Registerkarten gewechselt wird [– #10671](https://github.com/NuGet/Home/issues/10671)</span><span class="sxs-lookup"><span data-stu-id="e1a48-124">[Bug Bash] Error “operation canceled by user” show in Error List window when switching between tabs quickly in PM UI - [#10671](https://github.com/NuGet/Home/issues/10671)</span></span>

* <span data-ttu-id="e1a48-125">PM-Benutzeroberfläche: Verbessern der Paketinstallationsleistung auf Projektmappenebene [– #10210](https://github.com/NuGet/Home/issues/10210)</span><span class="sxs-lookup"><span data-stu-id="e1a48-125">PM UI:  Improve package installation performance on the solution level - [#10210](https://github.com/NuGet/Home/issues/10210)</span></span>

* <span data-ttu-id="e1a48-126">Ersetzen Von GetService durch GetServiceAsync überall in NuGet.Clients [– #3784](https://github.com/NuGet/Home/issues/3784)</span><span class="sxs-lookup"><span data-stu-id="e1a48-126">Replace GetService with GetServiceAsync everywhere in NuGet.Clients - [#3784](https://github.com/NuGet/Home/issues/3784)</span></span>

* <span data-ttu-id="e1a48-127">NuGet.exe Paketleistungsproblem mit `..` relativem Pfad – [#5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="e1a48-127">NuGet.exe pack performance problem with `..` relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>

* <span data-ttu-id="e1a48-128">Die Leistung von "nuget pack" sinkt mit zunehmenden Ebenen in den Quellpfaden [– #5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="e1a48-128">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>

* <span data-ttu-id="e1a48-129">NuGet erzeugt beim Packen von nuspec mit doppelten Dateien keinen Fehler.</span><span class="sxs-lookup"><span data-stu-id="e1a48-129">NuGet doesn't error when packaging nuspec with duplicate files.</span></span><span data-ttu-id="e1a48-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span><span class="sxs-lookup"><span data-stu-id="e1a48-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span></span>

* <span data-ttu-id="e1a48-131">NuGet-Paket "Das angegebene DateTimeOffset kann nicht in einen Zip-Dateizeitstempel konvertiert werden" [– #7001](https://github.com/NuGet/Home/issues/7001)</span><span class="sxs-lookup"><span data-stu-id="e1a48-131">NuGet pack "The DateTimeOffset specified cannot be converted into a Zip file timestamp" - [#7001](https://github.com/NuGet/Home/issues/7001)</span></span>

* <span data-ttu-id="e1a48-132">Zeitstempel der Datei des gepackten Pakets werden durch die Zeitzone verschoben [– #7395](https://github.com/NuGet/Home/issues/7395)</span><span class="sxs-lookup"><span data-stu-id="e1a48-132">Timestamps of file of packed package is shifted by the timezone - [#7395](https://github.com/NuGet/Home/issues/7395)</span></span>

* <span data-ttu-id="e1a48-133">NU1004 sollte umsetzbarere Informationen enthalten – [#7696](https://github.com/NuGet/Home/issues/7696)</span><span class="sxs-lookup"><span data-stu-id="e1a48-133">NU1004 should contain more actionable information  - [#7696](https://github.com/NuGet/Home/issues/7696)</span></span>

* <span data-ttu-id="e1a48-134">[Fehler Bash] [Testfehler] Die leere/falsch formatierte Sperrdatei sollte nicht aktualisiert werden, wenn "dotnet restore --use-lock-file --locked-mode" ausgeführt wird [– #8640](https://github.com/NuGet/Home/issues/8640)</span><span class="sxs-lookup"><span data-stu-id="e1a48-134">[Bug Bash][Test Failure] The empty/malformed lock file should not be updated when running ‘dotnet restore --use-lock-file --locked-mode’ - [#8640](https://github.com/NuGet/Home/issues/8640)</span></span>

* <span data-ttu-id="e1a48-135">NuGetVersionRange ermöglicht die Analyse logisch falscher Bereiche – [#9145](https://github.com/NuGet/Home/issues/9145)</span><span class="sxs-lookup"><span data-stu-id="e1a48-135">NuGetVersionRange allows logically incorrect ranges to be parsed - [#9145](https://github.com/NuGet/Home/issues/9145)</span></span>

* <span data-ttu-id="e1a48-136">Die PM-Benutzeroberfläche kann keine unterscheidbare Hintergrundfarbe zwischen ausgewählten und mit dem Mauszeiger zeigenden Paketquellen anzeigen – [#9538](https://github.com/NuGet/Home/issues/9538)</span><span class="sxs-lookup"><span data-stu-id="e1a48-136">PM UI can’t show distinguishable background color between selected and hovered package sources - [#9538](https://github.com/NuGet/Home/issues/9538)</span></span>

* <span data-ttu-id="e1a48-137">Kontrollkästchen zum Auswählen von Projekten, auf die installiert werden soll, wird nicht von der Sprachausgabe gelesen – [#9578](https://github.com/NuGet/Home/issues/9578)</span><span class="sxs-lookup"><span data-stu-id="e1a48-137">Checkbox for selecting projects to install to isn't being read by screen reader - [#9578](https://github.com/NuGet/Home/issues/9578)</span></span>

* <span data-ttu-id="e1a48-138">Die Standardauswahl der Dropdownliste "Versionen des Detailbereichs" sollte auf den Registerkarten "Installiert/Updates" installiert/LatestStable sein [– #9887](https://github.com/NuGet/Home/issues/9887)</span><span class="sxs-lookup"><span data-stu-id="e1a48-138">Details Pane Versions Dropdown default selection should be Installed/LatestStable on Installed/Updates tabs - [#9887](https://github.com/NuGet/Home/issues/9887)</span></span>

* <span data-ttu-id="e1a48-139">Entfernen Sie das Problemumgehungskonto für einige .NET 5 SDKs-Berichte TargetPlatformMoniker von ` ,Version= `  -  [#9913](https://github.com/NuGet/Home/issues/9913)</span><span class="sxs-lookup"><span data-stu-id="e1a48-139">Remove workaround account for some .NET 5 SDKs report TargetPlatformMoniker of ` ,Version= ` - [#9913](https://github.com/NuGet/Home/issues/9913)</span></span>

* <span data-ttu-id="e1a48-140">dotnet nuget verify is too quiet – [#10316](https://github.com/NuGet/Home/issues/10316)</span><span class="sxs-lookup"><span data-stu-id="e1a48-140">dotnet nuget verify is too quiet - [#10316](https://github.com/NuGet/Home/issues/10316)</span></span>

* <span data-ttu-id="e1a48-141">VersionRange kann keine einstelligen Bereiche analysieren [– #10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="e1a48-141">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>

* <span data-ttu-id="e1a48-142">Vs Solution Manager löst während des Debuggens eine NULL-Ausnahme für [aus – #10352](https://github.com/NuGet/Home/issues/10352)</span><span class="sxs-lookup"><span data-stu-id="e1a48-142">VS Solution manager throws null exception for during debugging - [#10352](https://github.com/NuGet/Home/issues/10352)</span></span>

* <span data-ttu-id="e1a48-143">Verschieben von CLI-Ausnahmemeldungen in Zeichenfolgenressourcendateien [– #10392](https://github.com/NuGet/Home/issues/10392)</span><span class="sxs-lookup"><span data-stu-id="e1a48-143">Move CLI exception messages to String Resource files - [#10392](https://github.com/NuGet/Home/issues/10392)</span></span>

* <span data-ttu-id="e1a48-144">Entfernen von intakten Code (TabItemButtonAutomationPeer) [– #10435](https://github.com/NuGet/Home/issues/10435)</span><span class="sxs-lookup"><span data-stu-id="e1a48-144">Remove dead code (TabItemButtonAutomationPeer) - [#10435](https://github.com/NuGet/Home/issues/10435)</span></span>

* <span data-ttu-id="e1a48-145">Kontextmenü aktualisieren sollte zum ersten ausgewählten Element [scrollen – #10498](https://github.com/NuGet/Home/issues/10498)</span><span class="sxs-lookup"><span data-stu-id="e1a48-145">Update context menu should scroll to first selected item - [#10498](https://github.com/NuGet/Home/issues/10498)</span></span>

* <span data-ttu-id="e1a48-146">Projektmappen-PMUI-Details mit überlappender horizontaler Leiste [– #10533](https://github.com/NuGet/Home/issues/10533)</span><span class="sxs-lookup"><span data-stu-id="e1a48-146">Solution PMUI Details has overlapping horizontal bar - [#10533](https://github.com/NuGet/Home/issues/10533)</span></span>

* <span data-ttu-id="e1a48-147">Signierung: Primäre Signaturdetails werden nicht angezeigt, wenn das Zertifikat abgelaufen ist und der Zeitstempel nicht vertrauenswürdig ist [– #10535](https://github.com/NuGet/Home/issues/10535)</span><span class="sxs-lookup"><span data-stu-id="e1a48-147">Signing:  primary signature details not displayed when certificate expired and timestamp untrusted - [#10535](https://github.com/NuGet/Home/issues/10535)</span></span>

* <span data-ttu-id="e1a48-148">Wenn keine Quellen aktiviert sind, wird verhindert, dass die PM-Benutzeroberfläche angezeigt wird [– #10541](https://github.com/NuGet/Home/issues/10541)</span><span class="sxs-lookup"><span data-stu-id="e1a48-148">Having no enabled sources prevents the PM UI from showing - [#10541](https://github.com/NuGet/Home/issues/10541)</span></span>

* <span data-ttu-id="e1a48-149">Paketmetadaten (Details, Veraltet) werden manchmal nicht aus nuget.org in CodeSpaces abgerufen – [#10549](https://github.com/NuGet/Home/issues/10549)</span><span class="sxs-lookup"><span data-stu-id="e1a48-149">Package Metadata (details, deprecation) are sometimes not pulled from nuget.org in CodeSpaces - [#10549](https://github.com/NuGet/Home/issues/10549)</span></span>

* <span data-ttu-id="e1a48-150">PmUI-Initialisierung schlägt mit Ausnahme während der Debugsitzung fehl – [#10559](https://github.com/NuGet/Home/issues/10559)</span><span class="sxs-lookup"><span data-stu-id="e1a48-150">PMUI initialization fails with exception during debug session - [#10559](https://github.com/NuGet/Home/issues/10559)</span></span>

* <span data-ttu-id="e1a48-151">NuGet-Wiederherstellung führt zu einem Fehler bei der Paketintegritätsprüfung im Big-Endian-System [– #10567](https://github.com/NuGet/Home/issues/10567)</span><span class="sxs-lookup"><span data-stu-id="e1a48-151">nuget restore results in a package integrity check failure on big endian system - [#10567](https://github.com/NuGet/Home/issues/10567)</span></span>

* <span data-ttu-id="e1a48-152">FormatException wird anstelle von PackagingException ausgelöst – [#10595](https://github.com/NuGet/Home/issues/10595)</span><span class="sxs-lookup"><span data-stu-id="e1a48-152">FormatException is thrown instead of PackagingException - [#10595](https://github.com/NuGet/Home/issues/10595)</span></span>

* <span data-ttu-id="e1a48-153">CPVM – Parallelitätsprobleme im Graph-Walking-Algorithmus [– #10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="e1a48-153">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>

* <span data-ttu-id="e1a48-154">Hinzufügen von Telemetriedaten zur PMC-PowerShell-Version [– #10609](https://github.com/NuGet/Home/issues/10609)</span><span class="sxs-lookup"><span data-stu-id="e1a48-154">Add PMC powershell version telemetry - [#10609](https://github.com/NuGet/Home/issues/10609)</span></span>

* <span data-ttu-id="e1a48-155">Verbessern der NuGetVersion-Sortierleistung [– #10611](https://github.com/NuGet/Home/issues/10611)</span><span class="sxs-lookup"><span data-stu-id="e1a48-155">Improve NuGetVersion sort performance - [#10611](https://github.com/NuGet/Home/issues/10611)</span></span>

* <span data-ttu-id="e1a48-156">Trusted Signers Add verfügt über inkonsistente Argumente [– #10647](https://github.com/NuGet/Home/issues/10647)</span><span class="sxs-lookup"><span data-stu-id="e1a48-156">Trusted-signers Add has inconsistent arguments - [#10647](https://github.com/NuGet/Home/issues/10647)</span></span>

* <span data-ttu-id="e1a48-157">Vs2019 v16.9.0: Durch das Wechseln von Registerkarten in NuGet Paket-Manager von "Updates" zu "Installiert" wird der Frame nicht aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="e1a48-157">Vs2019 v16.9.0: Switching tabs in NuGet Package Manager from "Updates" to "Installed" doesn't update the frame.</span></span><span data-ttu-id="e1a48-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span><span class="sxs-lookup"><span data-stu-id="e1a48-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span></span>

* <span data-ttu-id="e1a48-159">Entfernen Sie "v" aus der Versionsnummer in PMUI [– #10677](https://github.com/NuGet/Home/issues/10677)</span><span class="sxs-lookup"><span data-stu-id="e1a48-159">Remove the "v" from the version number in PMUI - [#10677](https://github.com/NuGet/Home/issues/10677)</span></span>

* <span data-ttu-id="e1a48-160">INuGetProjectService.GetInstalledPackagesAsync löst aus, bevor der CPS-Projektsystemvorschlag empfangen wird – [#10681](https://github.com/NuGet/Home/issues/10681)</span><span class="sxs-lookup"><span data-stu-id="e1a48-160">INuGetProjectService.GetInstalledPackagesAsync throws before receiving CPS project system nomination - [#10681](https://github.com/NuGet/Home/issues/10681)</span></span>

* <span data-ttu-id="e1a48-161">Eingebettete Symbole führen dazu, dass der Zugriff von der Quelle "Microsoft Visual Studio Offlinepakete" auf der Registerkarte Durchsuchen verweigert wird [– #10687](https://github.com/NuGet/Home/issues/10687)</span><span class="sxs-lookup"><span data-stu-id="e1a48-161">Embedded Icons cause Access Denied from source "Microsoft Visual Studio Offline Packages" on Browse tab - [#10687](https://github.com/NuGet/Home/issues/10687)</span></span>

* <span data-ttu-id="e1a48-162">INuGetProjectService.GetInstalledPackagesAsync löst aus, wenn MSBuildProjectExtensionsPath nicht festgelegt ist – [#10739](https://github.com/NuGet/Home/issues/10739)</span><span class="sxs-lookup"><span data-stu-id="e1a48-162">INuGetProjectService.GetInstalledPackagesAsync throws when MSBuildProjectExtensionsPath is not set - [#10739](https://github.com/NuGet/Home/issues/10739)</span></span>

* <span data-ttu-id="e1a48-163">"dotnet nuget remove source nuget.org" funktioniert nicht zum ersten Mal – [#10745](https://github.com/NuGet/Home/issues/10745)</span><span class="sxs-lookup"><span data-stu-id="e1a48-163">"dotnet nuget remove source nuget.org" doesn't work the first time - [#10745](https://github.com/NuGet/Home/issues/10745)</span></span>

* <span data-ttu-id="e1a48-164">NuGet blockiert einen Threadpoolthread in einer asynchronen Methode, die einen synchronen Aufruf des UI-Threads vornimmt – [#10775](https://github.com/NuGet/Home/issues/10775)</span><span class="sxs-lookup"><span data-stu-id="e1a48-164">Nuget blocks a threadpool thread in an async method making a synchronous call to the UI thread - [#10775](https://github.com/NuGet/Home/issues/10775)</span></span>

* <span data-ttu-id="e1a48-165">Tools -> Options -> NuGet Paket-Manager String is truncated - [#10779](https://github.com/NuGet/Home/issues/10779)</span><span class="sxs-lookup"><span data-stu-id="e1a48-165">Tools -> Options -> NuGet Package Manager string is truncated - [#10779](https://github.com/NuGet/Home/issues/10779)</span></span>

* <span data-ttu-id="e1a48-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` ist un toter Code und beeinträchtigt die Leistung [– #10790](https://github.com/NuGet/Home/issues/10790)</span><span class="sxs-lookup"><span data-stu-id="e1a48-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` is dead code and hurting performance - [#10790](https://github.com/NuGet/Home/issues/10790)</span></span>

* <span data-ttu-id="e1a48-167">Eingebettetes Symbol in NuGet SDK-Paketen verwenden – [#10795](https://github.com/NuGet/Home/issues/10795)</span><span class="sxs-lookup"><span data-stu-id="e1a48-167">Use embedded icon in NuGet SDK packages - [#10795](https://github.com/NuGet/Home/issues/10795)</span></span>

* <span data-ttu-id="e1a48-168">Aktualisieren der LIZENZIERUNGX-Lizenzliste [– #10806](https://github.com/NuGet/Home/issues/10806)</span><span class="sxs-lookup"><span data-stu-id="e1a48-168">Update the SPDX license list - [#10806](https://github.com/NuGet/Home/issues/10806)</span></span>

<span data-ttu-id="e1a48-169">**[Liste aller in diesem Release behobenen Probleme: 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span><span class="sxs-lookup"><span data-stu-id="e1a48-169">**[List of all issues fixed in this release - 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span></span>
  
<span data-ttu-id="e1a48-170">**[Liste der Commits in dieser Version : 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span><span class="sxs-lookup"><span data-stu-id="e1a48-170">**[List of commits in this release - 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span></span>
  
### <a name="community-contributions"></a><span data-ttu-id="e1a48-171">Beiträge aus der Community</span><span class="sxs-lookup"><span data-stu-id="e1a48-171">Community contributions</span></span>

<span data-ttu-id="e1a48-172">Vielen Dank an alle Mitwirkenden, die dieses NuGet-Release super gemacht haben!</span><span class="sxs-lookup"><span data-stu-id="e1a48-172">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="e1a48-173">Wer</span><span class="sxs-lookup"><span data-stu-id="e1a48-173">Who</span></span>|<span data-ttu-id="e1a48-174">Prs</span><span class="sxs-lookup"><span data-stu-id="e1a48-174">PRs</span></span>|<span data-ttu-id="e1a48-175">Probleme</span><span class="sxs-lookup"><span data-stu-id="e1a48-175">Issues</span></span>|
|----|----|----|
[<span data-ttu-id="e1a48-176">im NS-Z-201</span><span class="sxs-lookup"><span data-stu-id="e1a48-176">louis-z</span></span>](https://github.com/louis-z) | [<span data-ttu-id="e1a48-177">3991</span><span class="sxs-lookup"><span data-stu-id="e1a48-177">3991</span></span>](https://github.com/NuGet/NuGet.Client/pull/3991) | <span data-ttu-id="e1a48-178">VersionRange kann keine einstelligen Bereiche analysieren [– #10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="e1a48-178">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>
[<span data-ttu-id="e1a48-179">omajid</span><span class="sxs-lookup"><span data-stu-id="e1a48-179">omajid</span></span>](https://github.com/omajid) | [<span data-ttu-id="e1a48-180">3860</span><span class="sxs-lookup"><span data-stu-id="e1a48-180">3860</span></span>](https://github.com/NuGet/NuGet.Client/pull/3860) | <span data-ttu-id="e1a48-181">NuGet.Client build.sh ist fehlerhaft [– #10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="e1a48-181">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="e1a48-182">Nirmal4G</span><span class="sxs-lookup"><span data-stu-id="e1a48-182">Nirmal4G</span></span>](https://github.com/Nirmal4G) | [<span data-ttu-id="e1a48-183">3623</span><span class="sxs-lookup"><span data-stu-id="e1a48-183">3623</span></span>](https://github.com/NuGet/NuGet.Client/pull/3623) | <span data-ttu-id="e1a48-184">NuGet.Client build.sh ist fehlerhaft [– #10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="e1a48-184">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="e1a48-185">BlackGad</span><span class="sxs-lookup"><span data-stu-id="e1a48-185">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="e1a48-186">3953</span><span class="sxs-lookup"><span data-stu-id="e1a48-186">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="e1a48-187">Die Leistung von "nuget pack" sinkt mit zunehmenden Ebenen in den Quellpfaden [– #5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="e1a48-187">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>
[<span data-ttu-id="e1a48-188">BlackGad</span><span class="sxs-lookup"><span data-stu-id="e1a48-188">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="e1a48-189">3953</span><span class="sxs-lookup"><span data-stu-id="e1a48-189">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="e1a48-190">NuGet.exe Paketleistungsproblem mit .</span><span class="sxs-lookup"><span data-stu-id="e1a48-190">NuGet.exe pack performance problem with ..</span></span> <span data-ttu-id="e1a48-191">relativer Pfad [– #5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="e1a48-191">relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>
[<span data-ttu-id="e1a48-192">djin-krysakuc</span><span class="sxs-lookup"><span data-stu-id="e1a48-192">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="e1a48-193">3940</span><span class="sxs-lookup"><span data-stu-id="e1a48-193">3940</span></span>](https://github.com/NuGet/NuGet.Client/pull/3940) | <span data-ttu-id="e1a48-194">CPVM – Parallelitätsprobleme im Graph-Walking-Algorithmus [– #10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="e1a48-194">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>
[<span data-ttu-id="e1a48-195">jossimoes</span><span class="sxs-lookup"><span data-stu-id="e1a48-195">josesimoes</span></span>](https://github.com/josesimoes) | [<span data-ttu-id="e1a48-196">3943</span><span class="sxs-lookup"><span data-stu-id="e1a48-196">3943</span></span>](https://github.com/NuGet/NuGet.Client/pull/3943) | <span data-ttu-id="e1a48-197">Fügen Sie den Projekttyp nfproj zur Liste der unterstütztenProjectExtensions für die NuGet-CLI hinzu.</span><span class="sxs-lookup"><span data-stu-id="e1a48-197">Add the project type nfproj to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="e1a48-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="e1a48-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

## <a name="feedback-welcome"></a><span data-ttu-id="e1a48-199">Feedback willkommen</span><span class="sxs-lookup"><span data-stu-id="e1a48-199">Feedback welcome</span></span>

<span data-ttu-id="e1a48-200">Ihr Feedback ist uns sehr wichtig.</span><span class="sxs-lookup"><span data-stu-id="e1a48-200">Your feedback is important to us.</span></span>  <span data-ttu-id="e1a48-201">Wenn Probleme mit diesem Release auftreten, überprüfen Sie unsere [GitHub-Probleme](https://github.com/NuGet/Home/issues) und Visual Studio-Entwicklercommunity [auf](https://developercommunity.visualstudio.com/) vorhandene Probleme.</span><span class="sxs-lookup"><span data-stu-id="e1a48-201">If there are any problems with this release, check our [GitHub Issues](https://github.com/NuGet/Home/issues) and [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) for existing issues.</span></span>  <span data-ttu-id="e1a48-202">Melden Sie bei neuen Problemen in NuGet ein [GitHub-Problem.](https://github.com/NuGet/Home/issues/new)</span><span class="sxs-lookup"><span data-stu-id="e1a48-202">For new issues within NuGet, please report a [GitHub Issue](https://github.com/NuGet/Home/issues/new).</span></span>
<span data-ttu-id="e1a48-203">Informieren Sie uns bei allgemeinen Problemen [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) mit NuGet über die Option Problem melden in Ihrer bevorzugten IDE unter Hilfe > **Problem melden.**</span><span class="sxs-lookup"><span data-stu-id="e1a48-203">For general NuGet experience issues, let us know via the [Report a Problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) option found in your favorite IDE under **Help > Report a Problem**.</span></span>
