---
title: 3,5 Beta2-Anmerkungen zu dieser Version
description: Anmerkungen zu dieser Version von nuget 3,5 Beta 2 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776395"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="24f01-103">Anmerkungen zu dieser Version von nuget 3,5 Beta2</span><span class="sxs-lookup"><span data-stu-id="24f01-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="24f01-104">Anmerkungen zu dieser [Version von nuget 3,5-Beta Version](../release-notes/nuget-3.5-Beta.md)  |  [Anmerkungen zu dieser Version von nuget 3,5-RC](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="24f01-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="24f01-105">Nuget 3,5 Beta 2 RTM wurde am 27. Juni 2016 für Visual Studio 2013 und nuget.exe veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="24f01-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="24f01-106">Vollständiges Änderungsprotokoll</span><span class="sxs-lookup"><span data-stu-id="24f01-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="24f01-107">Liste der Probleme</span><span class="sxs-lookup"><span data-stu-id="24f01-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="24f01-108">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="24f01-108">Bug Fixes</span></span>

* <span data-ttu-id="24f01-109">Aktualisierte Fehlermeldung: fehlende Unterstützung für Kenn Wort Entschlüsselungen in .net Core für authentifizierte Feeds- [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="24f01-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="24f01-110">Der Paket-Manager-Konsolen Get-Package schlägt fehl, wenn das .net Core-Projekt geöffnet ist [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="24f01-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="24f01-111">Korrigieren Sie die falsche Behandlung von 403 in einem nuget-Push-Befehl [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="24f01-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="24f01-112">Beheben Sie Probleme beim Deinstallieren von Paketen in einer Lösung, die an die TFS-Quell Code Verwaltung gebunden ist, wenn disablesourcecontrolintegration auf true festgelegt ist [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="24f01-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="24f01-113">Korrigieren Sie die Paketaktualisierung, um nicht Ziel Pakete zu berücksichtigen- [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="24f01-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="24f01-114">Verwenden Sie den ausführlichkeits Grad von MSBuild zum Festlegen der Protokollierungs Stufe für Benutzeroberflächen Aktionen des nuget-Paket-Managers [#2705](https://github.com/NuGet/Home/issues/2705) -</span><span class="sxs-lookup"><span data-stu-id="24f01-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="24f01-115">Korrigieren der nuget-Konfiguration ist ein ungültiger Fehler in Website Projekten-vs 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="24f01-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="24f01-116">Beheben von Paket Problemen bei der Aufnahme von `.csproj` Inhalts Dateien [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="24f01-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="24f01-117">Defaultpushsource in `NuGetDefaults.Config` ( `ProgramData\NuGet` ) funktioniert nicht [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="24f01-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="24f01-118">Problembehebung in nuget 3.4.3 Release-value darf bei der Paket Erstellung nicht NULL sein- [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="24f01-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="24f01-119">RESTORE verwendet gespeicherte Anmelde Informationen aus Nuget.Config für VSTS-Feeds [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="24f01-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="24f01-120">Leistungs-Korrektur übermäßig viele Zuordnungen in Versions Vergleichs Code- [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="24f01-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="24f01-121">Beheben Sie Probleme, wenn mehrere Instanzen von nuget.exe versuchen, das gleiche Paket parallel zu installieren [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="24f01-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="24f01-122">Leistungs-Cache Abhängigkeitsinformationen für Vorgänge mit mehreren Projekten: [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="24f01-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="24f01-123">Behebung von Problemen, bei denen Paketquellen aus den Einstellungen nicht hinzugefügt werden, wenn die Quell Liste leer ist [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="24f01-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="24f01-124">Korrektur eines irreführenden Fehlers beim Versuch, ein Paket zu installieren, das von Entwurfszeit Fassaden abhängt [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="24f01-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="24f01-125">Wenn Sie ein Paket über die packagemanager-Konsole mit der Einstellung "All" installieren, wird nur die erste Quelle [#2557](https://github.com/NuGet/Home/issues/2557) versucht.</span><span class="sxs-lookup"><span data-stu-id="24f01-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="24f01-126">Beheben von Problemen mit Paketen, die über Dateien mit Schreibzeiten in Zukunft verfügen (Mono)- [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="24f01-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="24f01-127">Ausnahme anzeigen, wenn beim Suchen nach Projekten in "Update Command- [#2418](https://github.com/NuGet/Home/issues/2418) " ein Fehler auftritt</span><span class="sxs-lookup"><span data-stu-id="24f01-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="24f01-128">Der Paket Inhalt wird bei der Installation eines Pakets aus einem nuget v 3.3 +-Feed mit dem Argument NoCache, wenn das Paketdateien enthält, nicht ordnungsgemäß wieder hergestellt `.nupkg` [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="24f01-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="24f01-129">Beheben Sie das Problem mit der Paketinstallation (alle Quellen), wenn das Paket in 1 Quelle fehlt [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="24f01-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="24f01-130">Installations Blöcke, wenn eine einzelne Quelle die Autorisierung nicht besteht- [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="24f01-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="24f01-131">`.nuspec`Versions Bereich sollte-includereferencedprojects Version- [#1983](https://github.com/NuGet/Home/issues/1983) überschreiben</span><span class="sxs-lookup"><span data-stu-id="24f01-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="24f01-132">Nuget 3.3.0 Update schlägt mit einer zusätzlichen Einschränkung fehl... der in packages.config definierte Vorgang wird verhindert.</span><span class="sxs-lookup"><span data-stu-id="24f01-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="24f01-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="24f01-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="24f01-134">nuget.exe Update löscht den starken Namen der Assembly und das private-Attribut.</span><span class="sxs-lookup"><span data-stu-id="24f01-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="24f01-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="24f01-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="24f01-136">Beheben von Problemen mit dem relativen Dateipfad für "defaultpushsource"- [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="24f01-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="24f01-137">Verbessern der Fehlermeldungen des Update Resolvers- [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="24f01-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="24f01-138">Features und Behavior Changes</span><span class="sxs-lookup"><span data-stu-id="24f01-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="24f01-139">nuget.exe Push-Timeout-Parameter funktioniert nicht [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="24f01-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="24f01-140">nuget.exe Restore erzeugt keine `.props` `.targets` -und-Dateien für `.nuproj` Projekte (Regression in v 3.4.3.855)- [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="24f01-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="24f01-141">Benötigen Erweiterbarkeits-API zum Vergleichen von Frameworks mit Importen- [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="24f01-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="24f01-142">Abhängigkeits Optionen beim Verwenden von `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486) ausblenden</span><span class="sxs-lookup"><span data-stu-id="24f01-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="24f01-143">Ausgabe nuget.exe Versions Headers in detaillierter Ausgabe [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="24f01-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="24f01-144">Nuget sollte Unterstützung für/Runtimes/{Rid}/nativeassets/{txm}/- [#2782](https://github.com/NuGet/Home/issues/2782) hinzufügen</span><span class="sxs-lookup"><span data-stu-id="24f01-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>