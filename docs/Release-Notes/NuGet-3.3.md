---
title: Anmerkungen zur Version des NuGet-3.3 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 4110a36a-cffe-4038-8da4-e841bce6e94b
description: "Versionshinweise für NuGet 3.3 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-3.3 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f35f7621db324957b0af8329cf9faa11493835e2
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="2ba0c-104">3.3 NuGet-Versionshinweise</span><span class="sxs-lookup"><span data-stu-id="2ba0c-104">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="2ba0c-105">[Anmerkungen zur Version des NuGet-3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC-Versionsanmerkungen](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="2ba0c-105">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="2ba0c-106">NuGet-3.3 wurde am 30. November 2015 mit einer erheblichen Anzahl von benutzerschnittstellenupdates und Befehlszeilen-Funktionen sowie eine Auflistung von nützlich Korrekturen für den NuGet-Clients freigegeben.</span><span class="sxs-lookup"><span data-stu-id="2ba0c-106">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="2ba0c-107">Neue Funktionen</span><span class="sxs-lookup"><span data-stu-id="2ba0c-107">New Features</span></span>

* <span data-ttu-id="2ba0c-108">Anmeldeinformationsanbieter wurden eingeführt, die NuGet-Befehlszeilen-Clients in der Lage, um die nahtlose Zusammenarbeit mit einem authentifizierten Feed sein können.</span><span class="sxs-lookup"><span data-stu-id="2ba0c-108">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="2ba0c-109">[Anweisungen zum Installieren der Visual Studio Team Services-Anmeldeinformationen Anbieter ](../API/nuget-exe-Credential-Providers.md) und konfigurieren Sie die NuGet Clients zur Verwendung finden Sie auf der NuGet Docs.</span><span class="sxs-lookup"><span data-stu-id="2ba0c-109">[Instructions on how to install the Visual Studio Team Services credential provider ](../API/nuget-exe-Credential-Providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="2ba0c-110">Neue Features der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="2ba0c-110">New User Interface Features</span></span>

* <span data-ttu-id="2ba0c-111">Registerkarten für separate durchsuchen, installiert und Updates verfügbar</span><span class="sxs-lookup"><span data-stu-id="2ba0c-111">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="2ba0c-112">Verfügbare Badge, der angibt, der Anzahl der Pakete mit verfügbaren Updates aktualisiert</span><span class="sxs-lookup"><span data-stu-id="2ba0c-112">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="2ba0c-113">Paket Signale in der Liste der Pakete an, wenn das Paket installiert ist, oder ein Update verfügbar ist</span><span class="sxs-lookup"><span data-stu-id="2ba0c-113">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="2ba0c-114">Herunterladen Sie Anzahl und der Autor hinzugefügt wird, um die Liste der Pakete</span><span class="sxs-lookup"><span data-stu-id="2ba0c-114">Download count and author added to the package list</span></span>
* <span data-ttu-id="2ba0c-115">Höchste verfügbare Versionsnummer und der derzeit installierten Version Zahl auf die Paketliste</span><span class="sxs-lookup"><span data-stu-id="2ba0c-115">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="2ba0c-116">Aktionsschaltflächen schnelle Installation zu aktualisieren und Deinstallieren von aus der Liste der Pakete</span><span class="sxs-lookup"><span data-stu-id="2ba0c-116">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="2ba0c-117">Klarer Aktionsschaltflächen im Paket-Detail-Bereich</span><span class="sxs-lookup"><span data-stu-id="2ba0c-117">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="2ba0c-118">Paket Aktualisierungsdatum im Paket-Detail-Bereich</span><span class="sxs-lookup"><span data-stu-id="2ba0c-118">Package update date on the package detail panel</span></span>
* <span data-ttu-id="2ba0c-119">Konsolidieren Sie Bereich im Projektmappen-Ansicht</span><span class="sxs-lookup"><span data-stu-id="2ba0c-119">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="2ba0c-120">Sortierbares Raster von Projekten und installierten Versionsnummern für die Lösung-Sicht</span><span class="sxs-lookup"><span data-stu-id="2ba0c-120">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="2ba0c-121">Neue Befehlszeilen-Funktionen</span><span class="sxs-lookup"><span data-stu-id="2ba0c-121">New Command-line Features</span></span>

<span data-ttu-id="2ba0c-122">In dieser Version eingeführten wir die `add` und `init` Befehle aus, um die Ordner-basierte Repositorys zu initialisieren, wie beschrieben in der [nuget.exe Verweis](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="2ba0c-122">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="2ba0c-123">Repositorys, die erstellt und verwaltet, die mit diesem Ordner-Struktur wird [bieten Sie beachtliche Leistungsvorteile](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) wie beschrieben in unserem Blog.</span><span class="sxs-lookup"><span data-stu-id="2ba0c-123">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="2ba0c-124">Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="2ba0c-124">ContentFiles</span></span>

<span data-ttu-id="2ba0c-125">Inhalt wird jetzt unterstützt `project.json` verwaltete Projekte über die neue `contentFiles` Ordner und `.nuspec` `contentFiles` Element Notation.</span><span class="sxs-lookup"><span data-stu-id="2ba0c-125">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="2ba0c-126">Dieser Inhalt kann direkt vom Paketersteller für Interaktionen mit Projektsystemen angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="2ba0c-126">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="2ba0c-127">Weitere Informationen zum Konfigurieren der Inhaltsdateien in einem `.nuspec` Dokument befindet sich der [.nuspec Verweis](../schema/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="2ba0c-127">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../schema/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="2ba0c-128">NuGet "lokal" Cache-Verwaltung</span><span class="sxs-lookup"><span data-stu-id="2ba0c-128">NuGet Locals Cache Management</span></span>

<span data-ttu-id="2ba0c-129">Die NuGet-Befehlszeile wurde aktualisiert, um Informationen zum Verwalten des lokalen Caches auf einer Arbeitsstation enthalten.</span><span class="sxs-lookup"><span data-stu-id="2ba0c-129">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="2ba0c-130">Weitere Informationen zum Befehl "lokal" steht in der [NuGet-Befehlszeilenreferenz](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="2ba0c-130">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="2ba0c-131">Behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="2ba0c-131">Fixed Issues</span></span>

<span data-ttu-id="2ba0c-132">**Relevante Probleme**</span><span class="sxs-lookup"><span data-stu-id="2ba0c-132">**Notable Issues**</span></span>

* <span data-ttu-id="2ba0c-133">NuGet-Befehlszeilen wiederhergestellten-Unterstützung für die Wiederherstellung-Paketen mit einer Projektmappendatei auf Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="2ba0c-133">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="2ba0c-134">Die vollständige Liste der in der 3.3-Version behobene Probleme finden Sie auf GitHub unter der [3.3 Meilenstein](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="2ba0c-134">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="2ba0c-135">Die Liste der in der Befehlszeile 3.3-Version behobene Probleme werden aufgezeichnet, der [3.3 Befehlszeilen Meilenstein](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="2ba0c-135">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="2ba0c-136">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="2ba0c-136">Known Issues</span></span>

<span data-ttu-id="2ba0c-137">Wir weiterhin Probleme auf unserer GitHub-Problemliste zu verfolgen, die sich am befinden: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="2ba0c-137">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>