---
title: Anmerkungen zu NuGet 3.3
description: Anmerkungen zu NuGet 3.3, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546646"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="028f0-103">Anmerkungen zu NuGet 3.3</span><span class="sxs-lookup"><span data-stu-id="028f0-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="028f0-104">[Anmerkungen zu NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC-Versionsanmerkungen](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="028f0-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="028f0-105">NuGet 3.3 wurde am 30. November 2015 mit einer großen Anzahl von Benutzerschnittstellen-Updates und -Befehlszeilenfunktionen sowie eine Sammlung von nützlich Fehlerbehebungen für die NuGet-Clients veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="028f0-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="028f0-106">Neue Funktionen</span><span class="sxs-lookup"><span data-stu-id="028f0-106">New Features</span></span>

* <span data-ttu-id="028f0-107">Anmeldeinformationsanbieter wurden eingeführt, mit denen Befehlszeilen NuGet-Clients, um die nahtlose Zusammenarbeit mit einem authentifizierten-Feed zu können.</span><span class="sxs-lookup"><span data-stu-id="028f0-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="028f0-108">[Anweisungen zum Installieren von Visual Studio Team Services-Anmeldeinformationen Anbieter ](../api/nuget-exe-credential-providers.md) und Konfigurieren des NuGet-Pakets Clients seiner Verwendung finden Sie auf NuGet-Dokumentation.</span><span class="sxs-lookup"><span data-stu-id="028f0-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="028f0-109">Neue Features der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="028f0-109">New User Interface Features</span></span>

* <span data-ttu-id="028f0-110">Separate Registerkarten für das Durchsuchen, installiert und Updates verfügbar</span><span class="sxs-lookup"><span data-stu-id="028f0-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="028f0-111">Verfügbare Updates-Badge, der angibt, der Anzahl der Pakete mit verfügbaren updates</span><span class="sxs-lookup"><span data-stu-id="028f0-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="028f0-112">Paketbadges in der Paketliste angeben, ob das Paket installiert ist, oder ein Update verfügbar ist</span><span class="sxs-lookup"><span data-stu-id="028f0-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="028f0-113">Herunterladen Sie Anzahl und der Autor hinzugefügt, um die Liste der Pakete</span><span class="sxs-lookup"><span data-stu-id="028f0-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="028f0-114">Anzahl der höchste verfügbare Version und die Anzahl der aktuell installierten Version in der Paketliste</span><span class="sxs-lookup"><span data-stu-id="028f0-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="028f0-115">Aktionsschaltflächen können schnell installieren, aktualisieren und deinstallieren Sie auf die Liste der Pakete</span><span class="sxs-lookup"><span data-stu-id="028f0-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="028f0-116">Klarer Aktionsschaltflächen im Bereich der Paket-Details</span><span class="sxs-lookup"><span data-stu-id="028f0-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="028f0-117">Paket Aktualisierungsdatum im Bereich der Paket-Details</span><span class="sxs-lookup"><span data-stu-id="028f0-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="028f0-118">Bereich, in der Projektmappenansicht konsolidieren</span><span class="sxs-lookup"><span data-stu-id="028f0-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="028f0-119">Sortierbar Raster von Projekten und der installierten Versionsnummern in der Projektmappenansicht</span><span class="sxs-lookup"><span data-stu-id="028f0-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="028f0-120">Neue Befehlszeile Features</span><span class="sxs-lookup"><span data-stu-id="028f0-120">New Command-line Features</span></span>

<span data-ttu-id="028f0-121">In dieser Version eingeführten wir die `add` und `init` Befehle aus, um die Ordner-basierten Repositorys zu initialisieren, wie beschrieben in der [Referenz zur nuget.exe](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="028f0-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="028f0-122">Repositorys, die erstellt und verwaltet, die mit diesem Ordner-Struktur wird [bieten Sie beachtliche Leistungsvorteile](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) wie beschrieben in unserem Blog.</span><span class="sxs-lookup"><span data-stu-id="028f0-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="028f0-123">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="028f0-123">ContentFiles</span></span>

<span data-ttu-id="028f0-124">Inhalt wird nun unterstützt `project.json` zu verwalteten Projekten, die über die neue `contentFiles` Ordner und `.nuspec` `contentFiles` Element-Notation.</span><span class="sxs-lookup"><span data-stu-id="028f0-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="028f0-125">Dieser Inhalt kann direkt vom Paketersteller für Interaktionen mit Projektsystemen angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="028f0-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="028f0-126">Weitere Informationen zum Konfigurieren von "contentfiles" in einem `.nuspec` Dokument finden Sie in der [NuSpec-Referenz](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="028f0-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="028f0-127">NuGet "lokal" Cache-Verwaltung</span><span class="sxs-lookup"><span data-stu-id="028f0-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="028f0-128">Das NuGet-Befehlszeile wurde aktualisiert, um Informationen zum Verwalten des lokalen Caches auf einer Arbeitsstation gehören.</span><span class="sxs-lookup"><span data-stu-id="028f0-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="028f0-129">Weitere Informationen zu den Befehl "Locals" steht in der [NuGet-Befehlszeilenreferenz](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="028f0-129">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="028f0-130">Behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="028f0-130">Fixed Issues</span></span>

<span data-ttu-id="028f0-131">**Relevante Probleme**</span><span class="sxs-lookup"><span data-stu-id="028f0-131">**Notable Issues**</span></span>

* <span data-ttu-id="028f0-132">NuGet-Befehlszeile wiederhergestellten Unterstützung für die Wiederherstellung mit einer Projektmappe unter Mono - Pakete [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="028f0-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="028f0-133">Die vollständige Liste der in der Version 3.3 behandelten Probleme finden Sie auf GitHub unter den [3.3 Meilenstein](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="028f0-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="028f0-134">Die Liste der in der Befehlszeile 3.3-Version behobene Probleme in aufgezeichnet werden die [3.3 Befehlszeilen Meilenstein](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="028f0-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="028f0-135">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="028f0-135">Known Issues</span></span>

<span data-ttu-id="028f0-136">Wir fahren fort, um Probleme in der Liste unserer GitHub-Probleme nachzuverfolgen, die finden Sie unter: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="028f0-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>