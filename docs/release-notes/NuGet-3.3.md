---
title: Anmerkungen zu dieser Version von nuget 3,3
description: Anmerkungen zu dieser Version von nuget 3,3 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 482c03a4f6ca39edf317b6ef8d535e79b53d5d16
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317039"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="ac169-103">Anmerkungen zu dieser Version von nuget 3,3</span><span class="sxs-lookup"><span data-stu-id="ac169-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="ac169-104">[Versions Anmerkungen](../release-notes/nuget-3.2.1.md) | zu nuget 3.2.1[nuget 3,4-RC Anmerkungen](../release-notes/nuget-3.4-RC.md) zu dieser Version</span><span class="sxs-lookup"><span data-stu-id="ac169-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="ac169-105">Nuget 3,3 wurde am 30. November 2015 mit einer erheblichen Anzahl von Benutzeroberflächen Updates und Befehlszeilen Features sowie eine Sammlung nützlicher Korrekturen für die nuget-Clients veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="ac169-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="ac169-106">Neue Funktionen</span><span class="sxs-lookup"><span data-stu-id="ac169-106">New Features</span></span>

* <span data-ttu-id="ac169-107">Es wurden Anmelde Informationsanbieter eingeführt, mit denen nuget-Befehlszeilen Clients nahtlos mit einem authentifizierten Feed arbeiten können.</span><span class="sxs-lookup"><span data-stu-id="ac169-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="ac169-108">[Anweisungen zum Installieren des Visual Studio Team Services](../api/nuget-exe-credential-providers.md) Anmelde Informationsanbieters und zum Konfigurieren der zu verwendenden nuget-Clients finden Sie unter nuget-Dokumentation.</span><span class="sxs-lookup"><span data-stu-id="ac169-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="ac169-109">Neue Benutzeroberflächen Features</span><span class="sxs-lookup"><span data-stu-id="ac169-109">New User Interface Features</span></span>

* <span data-ttu-id="ac169-110">Getrennte Registerkarten zum Durchsuchen, installieren und aktualisieren</span><span class="sxs-lookup"><span data-stu-id="ac169-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="ac169-111">Verfügbarer Hinweis "Updates" gibt die Anzahl der Pakete mit verfügbaren Updates an</span><span class="sxs-lookup"><span data-stu-id="ac169-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="ac169-112">Paket Ausweise in der Paketliste, um anzugeben, ob das Paket installiert ist oder ein Update verfügbar ist</span><span class="sxs-lookup"><span data-stu-id="ac169-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="ac169-113">Download Anzahl und Autor zur Paketliste hinzugefügt</span><span class="sxs-lookup"><span data-stu-id="ac169-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="ac169-114">Höchste verfügbare Versionsnummer und aktuell installierte Versionsnummer in der Paketliste</span><span class="sxs-lookup"><span data-stu-id="ac169-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="ac169-115">Aktions Schaltflächen für die schnelle Installation, Aktualisierung und Deinstallation in der Paketliste</span><span class="sxs-lookup"><span data-stu-id="ac169-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="ac169-116">Klarere Aktions Schaltflächen im Paket Detailbereich</span><span class="sxs-lookup"><span data-stu-id="ac169-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="ac169-117">Paket Aktualisierungsdatum im Paket Detailbereich</span><span class="sxs-lookup"><span data-stu-id="ac169-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="ac169-118">Bereich "konsolidieren" in der Lösungs Ansicht</span><span class="sxs-lookup"><span data-stu-id="ac169-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="ac169-119">Sortier bares Raster von Projekten und installierten Versionsnummern in der projektmappenansicht</span><span class="sxs-lookup"><span data-stu-id="ac169-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="ac169-120">Neue Befehlszeilen Funktionen</span><span class="sxs-lookup"><span data-stu-id="ac169-120">New Command-line Features</span></span>

<span data-ttu-id="ac169-121">In dieser Version haben wir die `add` Befehle `init` und eingeführt, um Ordner basierte Depots zu initialisieren, wie in der Referenz zu " [nuget. exe](../reference/nuget-exe-cli-reference.md)" beschrieben.</span><span class="sxs-lookup"><span data-stu-id="ac169-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="ac169-122">Mit dieser Ordnerstruktur erstellte und erhaltene Depots [bieten bedeutende Leistungsvorteile](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) , die in unserem Blog beschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="ac169-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="ac169-123">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="ac169-123">ContentFiles</span></span>

<span data-ttu-id="ac169-124">Der Inhalt wird nun in `project.json` verwalteten Projekten durch die neue `contentFiles` Ordner- `.nuspec` und `contentFiles` Element Notation unterstützt.</span><span class="sxs-lookup"><span data-stu-id="ac169-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="ac169-125">Dieser Inhalt kann vom Paket Ersteller für Interaktionen mit Projekt Systemen direkt angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="ac169-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="ac169-126">Weitere Informationen zum Konfigurieren von contentfiles in einem `.nuspec` Dokument finden Sie in der [nuspec-Referenz](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="ac169-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="ac169-127">Lokale nuget-Cache Verwaltung</span><span class="sxs-lookup"><span data-stu-id="ac169-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="ac169-128">Die nuget-Befehlszeile wurde aktualisiert und enthält Informationen zum Verwalten der lokalen Caches auf einer Arbeitsstation.</span><span class="sxs-lookup"><span data-stu-id="ac169-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="ac169-129">Weitere Informationen zum Befehl "Locals" finden Sie in der [nuget-Befehlszeilen Referenz](../reference/cli-reference/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="ac169-129">More information about the locals command is available in the [NuGet command-line reference](../reference/cli-reference/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="ac169-130">Behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="ac169-130">Fixed Issues</span></span>

<span data-ttu-id="ac169-131">**Relevante Probleme**</span><span class="sxs-lookup"><span data-stu-id="ac169-131">**Notable Issues**</span></span>

* <span data-ttu-id="ac169-132">[1543](https://github.com/NuGet/Home/issues/1543) in der nuget-Befehlszeilen Wiederherstellung wiederhergestellte Unterstützung für die Wiederherstellung von Paketen mit einer Projektmappendatei</span><span class="sxs-lookup"><span data-stu-id="ac169-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="ac169-133">Eine umfassende Liste der Probleme, die in Version 3,3 behoben wurden, finden Sie auf GitHub unter dem [3,3-Meilenstein](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="ac169-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="ac169-134">Die Liste der Probleme, die in der 3,3-Befehlszeilen Freigabe behoben wurden, wird im [3,3-Befehlszeilen Meilenstein](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)aufgezeichnet.</span><span class="sxs-lookup"><span data-stu-id="ac169-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="ac169-135">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="ac169-135">Known Issues</span></span>

<span data-ttu-id="ac169-136">Wir verfolgen weiterhin Probleme in unserer GitHub-Liste mit Problemen, die unter folgenden Themen zu finden sind:[http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="ac169-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>