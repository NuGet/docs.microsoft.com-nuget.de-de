---
title: 3.5 Anmerkungen zu dieser Beta 2-Version
description: Versionshinweise für NuGet 3.5 Beta 2, einschließlich der bekannten Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08bbae00a3e63c2a1ff42d5cc04981eb02966850
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822343"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="95036-103">NuGet-3.5 Beta 2-Anmerkungen zu dieser Version</span><span class="sxs-lookup"><span data-stu-id="95036-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="95036-104">[NuGet-Version 3.5 Beta Hinweise](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC-Versionsanmerkungen](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="95036-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="95036-105">NuGet-3.5 Beta 2 RTM wurde 27. Juni 2016 für Visual Studio 2013 und nuget.exe freigegeben.</span><span class="sxs-lookup"><span data-stu-id="95036-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="95036-106">Vollständige Änderungsprotokoll</span><span class="sxs-lookup"><span data-stu-id="95036-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="95036-107">Probleme: Liste</span><span class="sxs-lookup"><span data-stu-id="95036-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="95036-108">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="95036-108">Bug Fixes</span></span>

* <span data-ttu-id="95036-109">Aktualisierte Fehlermeldung keine Unterstützung für Kennwort Decrpytion im .NET-Kern für authentifizierten Feeds - [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="95036-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="95036-110">Package Manager Console Get-Package fehlschlägt, wenn .NET Core-Projekt öffnen - [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="95036-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="95036-111">Korrektur der falschen Verarbeitung des 403 in NuGet-Befehl "Push" [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="95036-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="95036-112">Beheben von Problemen bei der Deinstallation von Paketen in einer Projektmappe zur TFS-quellcodeverwaltung gebunden werden, wenn DisableSourceControlIntegration festgelegt ist auf "true" - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="95036-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="95036-113">Korrigieren Sie die paketaktualisierung Konto nicht Ziel Pakete - übernehmen [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="95036-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="95036-114">Mithilfe der Ausführlichkeit der MSBuild fest Protokollierung Stufe für NuGet-Paket-Manager-UI-Aktionen - [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="95036-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="95036-115">Korrektur NuGet-Konfiguration ist ungültige Fehlermeldung in Websiteprojekten – VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="95036-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="95036-116">Beheben von Problemen von Pack von `.csproj` Wenn Inhaltsdateien enthaltenen - [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="95036-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="95036-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) funktioniert nicht – [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="95036-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="95036-118">Beheben des Problem in Nuget 3.4.3 Version - Wert darf nicht null bei der paketerstellung - [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="95036-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="95036-119">Wiederherstellung verwendet gespeicherte Anmeldeinformationen von "NuGet.config" für VSTS-Feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="95036-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="95036-120">Leistung - übermäßige Zuordnungen für die Korrektur in Code von Version Vergleiche - [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="95036-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="95036-121">Beheben von Problemen, wenn mehrere Instanzen von nuget.exe versucht, zum Installieren des gleichen Pakets parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="95036-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="95036-122">Leistung - Cache Abhängigkeitsinformationen für Vorgänge mit mehreren Projekten - [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="95036-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="95036-123">Beheben des Problems Paket Datenquellen kann nicht in "Einstellungen" hinzugefügt werden, wenn Quellliste leer ist [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="95036-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="95036-124">Korrigieren Sie irreführende Fehler beim Installieren des Pakets, die zur Entwurfszeit Fassaden - abhängig [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="95036-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="95036-125">Nur erste Quelle - Installation eines Pakets aus PackageManager-Konsole mit der Einstellung "Alle" versucht [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="95036-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="95036-126">Beheben von Problemen mit Paketen mit Dateien in der Zukunft Schreibzeiten (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="95036-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="95036-127">Ausnahme angezeigt, bei ein Fehler Suchen von Projekten in Updatebefehl - [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="95036-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="95036-128">Paketinhalt wird nicht ordnungsgemäß wiederhergestellt, beim Installieren eines Pakets von Nuget v3. 3 +-mit dem Argument Feeds - NoCache, wenn das Paket enthält `.nupkg` Dateien - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="95036-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="95036-129">Korrektur Problem mit dem Paket installieren (alle Quellen) aus, wenn von 1 Source - Paket fehlt [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="95036-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="95036-130">Blöcke zu installieren, schlägt eine einzelne Datenquelle Autorisierung - [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="95036-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="95036-131">`.nuspec` Version Bereich sollten IncludeReferencedProjects - Version - überschreiben [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="95036-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="95036-132">NuGet 3.3.0 Update schlägt fehl mit "eine weitere Einschränkung... definiert" Packages.config ", verhindert diesen Vorgang."</span><span class="sxs-lookup"><span data-stu-id="95036-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="95036-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="95036-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="95036-134">NuGet.exe Update löscht den starken Assemblynamen und privaten Attribut.</span><span class="sxs-lookup"><span data-stu-id="95036-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="95036-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="95036-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="95036-136">Beheben von Problemen mit relativen Pfad für "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="95036-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="95036-137">Verbesserung der Fehlermeldungen für Update-Resolver - [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="95036-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="95036-138">Features und Verhaltensänderungen</span><span class="sxs-lookup"><span data-stu-id="95036-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="95036-139">NuGet.exe Push - Timeoutparameter funktioniert nicht – [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="95036-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="95036-140">NuGet.exe Wiederherstellung keine erzeugt `.props` und `.targets` Dateien für `.nuproj` Projekte (Regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="95036-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="95036-141">Erweiterbarkeits-API zum Vergleichen von Importen - Frameworks benötigen [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="95036-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="95036-142">Abhängigkeitsoptionen ausblenden, wenn mit `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="95036-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="95036-143">Drucken nuget.exe-Versionsheader in ausführliche Ausgabe - [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="95036-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="95036-144">Sollte zum Hinzufügen von NuGet-Unterstützung für /runtimes/ {rid} /nativeassets/ {Txm} / - [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="95036-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>