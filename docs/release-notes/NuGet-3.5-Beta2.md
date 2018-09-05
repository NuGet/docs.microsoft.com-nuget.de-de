---
title: '3.5 Beta 2: Anmerkungen zu dieser Version'
description: Anmerkungen zu NuGet 3.5 Beta 2, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b47939e2fafc11823c41a849b3c58bbf0800ada
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551990"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="830e8-103">Anmerkungen zu NuGet 3.5 Beta 2</span><span class="sxs-lookup"><span data-stu-id="830e8-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="830e8-104">[Anmerkungen zu NuGet 3.5-Beta](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC-Versionsanmerkungen](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="830e8-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="830e8-105">RTM von NuGet 3.5 Beta 2 wurde am 27. Juni 2016 für Visual Studio 2013 und nuget.exe veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="830e8-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="830e8-106">Vollständigen Änderungsprotokoll</span><span class="sxs-lookup"><span data-stu-id="830e8-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="830e8-107">Probleme: Liste</span><span class="sxs-lookup"><span data-stu-id="830e8-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="830e8-108">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="830e8-108">Bug Fixes</span></span>

* <span data-ttu-id="830e8-109">Aktualisierte Fehlermeldung Mangel an Unterstützung für Kennwort Decrpytion in .NET Core für authentifizierte Feeds - [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="830e8-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="830e8-110">Paket-Manager-Console-Get-Package schlägt fehl, wenn .NET Core-Projekt geöffnet ist – [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="830e8-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="830e8-111">Korrektur der falschen Verarbeitung des 403 in NuGet Push-Befehl [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="830e8-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="830e8-112">Beheben von Problemen bei der Deinstallation von Paketen in einer Projektmappe, die an TFS-quellcodeverwaltung gebunden werden, wenn DisableSourceControlIntegration festgelegt ist auf "true" - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="830e8-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="830e8-113">Beheben Sie die paketaktualisierung Konto nicht-Zielpakete. – berücksichtigen [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="830e8-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="830e8-114">Mit MSBuild-Ausführlichkeit fest Protokollierung Stufe für Nuget-Paket-Manager UI-Aktionen – [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="830e8-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="830e8-115">Korrektur von NuGet-Konfiguration ist ungültig Fehler in Websiteprojekte – VS 2015 VSIX (3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="830e8-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="830e8-116">Beheben Sie Probleme Pack `.csproj` bei Inhaltsdateien enthaltenen - [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="830e8-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="830e8-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) funktioniert nicht – [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="830e8-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="830e8-118">Korrigieren von Problem in Nuget 3.4.3 Release - Wert darf nicht null bei der paketerstellung - [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="830e8-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="830e8-119">Wiederherstellung verwendet gespeicherte Anmeldeinformationen aus der Datei "NuGet.config" für VSTS-Feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="830e8-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="830e8-120">Leistung - übermäßige Zuordnungen für die Korrektur in Code von Version-Vergleichs - [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="830e8-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="830e8-121">Beheben von Problemen, wenn mehrere Instanzen von nuget.exe versucht wird, zum Installieren des gleichen Pakets parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="830e8-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="830e8-122">Leistung - Cache von Abhängigkeitsinformationen für Vorgänge mit mehreren Projekten - [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="830e8-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="830e8-123">Problem wurde behoben, das Paket Quellen kann nicht aus den Einstellungen hinzugefügt werden, wenn Quellliste leer ist [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="830e8-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="830e8-124">Irreführende Fehler zu beheben, beim Versuch, Paket zu installieren, von denen abhängt, während der Entwurfszeit Fassaden - [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="830e8-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="830e8-125">Installieren eines Pakets von PackageManager-Konsole mit der Einstellung "Alle" aus versucht nur erste Quelle - [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="830e8-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="830e8-126">Beheben von Problemen mit Paketen, die Dateien in der Zukunft mit Schreibzugriff (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="830e8-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="830e8-127">Ausnahme angezeigt wird, wenn ein Fehler Suchen von Projekten in der Updatebefehl vorliegt – [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="830e8-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="830e8-128">Paketinhalt wird nicht ordnungsgemäß wiederhergestellt, beim Installieren eines Pakets aus einem Nuget-Version 3.3 +-mit dem Argument Feeds - NoCache, wenn das Paket enthält `.nupkg` Dateien – [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="830e8-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="830e8-129">Problem mit dem Paket installieren (alle Quellen) aus, wenn von der Quelle der 1 - Paket fehlt [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="830e8-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="830e8-130">Installieren Sie Blöcke, fällt eine einzelne Quelle Authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="830e8-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="830e8-131">`.nuspec` Bereich sollten außer Kraft setzen - IncludeReferencedProjects Version – Version [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="830e8-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="830e8-132">NuGet 3.3.0-Aktualisierung ein Fehler auftritt, mit "... eine zusätzliche Einschränkung definiert" Packages.config "wird verhindert, dass dieser Vorgang."</span><span class="sxs-lookup"><span data-stu-id="830e8-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="830e8-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="830e8-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="830e8-134">NuGet.exe-Update löscht die Assembly starke Namen und das Private-Attribut.</span><span class="sxs-lookup"><span data-stu-id="830e8-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="830e8-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="830e8-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="830e8-136">Beheben von Problemen mit relativen Pfad für "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="830e8-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="830e8-137">Verbesserung der Fehlermeldungen für Update-Resolver - [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="830e8-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="830e8-138">Features und Verhaltensänderungen</span><span class="sxs-lookup"><span data-stu-id="830e8-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="830e8-139">NuGet.exe-Push - Timeout-Parameter funktioniert nicht – [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="830e8-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="830e8-140">NuGet.exe erstellt keine `.props` und `.targets` -Dateien für `.nuproj` Projekte (Regression im v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="830e8-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="830e8-141">Erweiterbarkeits-API-Frameworks mit Imports - vergleichen benötigen [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="830e8-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="830e8-142">Abhängigkeitsoptionen ausblenden, wenn mit `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="830e8-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="830e8-143">Drucken Sie nuget.exe-Version-Header in der ausführlichen Ausgabe - [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="830e8-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="830e8-144">NuGet sollten Hinzufügen von Unterstützung für {löschen} /runtimes/ /nativeassets/ {Txm} & gt; – [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="830e8-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>