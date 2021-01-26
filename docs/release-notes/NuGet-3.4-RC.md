---
title: Anmerkungen zu dieser Version von nuget 3,4-RC
description: Anmerkungen zu dieser Version von nuget 3,4 RC, einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780238"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="5e9d3-103">Anmerkungen zu dieser Version von nuget 3,4-RC</span><span class="sxs-lookup"><span data-stu-id="5e9d3-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="5e9d3-104">Anmerkungen zu dieser [Version von nuget 3,3](../release-notes/nuget-3.3.md)  |  [Anmerkungen zu dieser Version von nuget 3,4](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="5e9d3-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="5e9d3-105">Nuget 3,4-RC wurde am 2016 3. März mit Visual Studio 2015 Update 2 RC veröffentlicht und mit einigen wenigen Grundsätzen erstellt:</span><span class="sxs-lookup"><span data-stu-id="5e9d3-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="5e9d3-106">Plattformübergreifende Unterstützung</span><span class="sxs-lookup"><span data-stu-id="5e9d3-106">Cross-Platform support</span></span>
* <span data-ttu-id="5e9d3-107">Leistungsverbesserungen</span><span class="sxs-lookup"><span data-stu-id="5e9d3-107">Performance improvements</span></span>
* <span data-ttu-id="5e9d3-108">Kleinere Verbesserung der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="5e9d3-108">Minor UI improvements</span></span>

<span data-ttu-id="5e9d3-109">In dieser RC-Version sind die folgenden Features verfügbar, die für die endgültige Version 3,4 geplant sind.</span><span class="sxs-lookup"><span data-stu-id="5e9d3-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="5e9d3-110">Neue Funktionen</span><span class="sxs-lookup"><span data-stu-id="5e9d3-110">New Features</span></span>

* <span data-ttu-id="5e9d3-111">Nuget-Clients unterstützen jetzt gzip-Inhalts Codierung aus Depots.</span><span class="sxs-lookup"><span data-stu-id="5e9d3-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="5e9d3-112">Unterstützung für pdsb von Paketen in xproj-Projekten</span><span class="sxs-lookup"><span data-stu-id="5e9d3-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="5e9d3-113">Unterstützung für IOS-und Android-Buildvorgänge im contentfiles-Element</span><span class="sxs-lookup"><span data-stu-id="5e9d3-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="5e9d3-114">Unterstützung für die FrameworkMoniker netstandard und netstandardapp</span><span class="sxs-lookup"><span data-stu-id="5e9d3-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="5e9d3-115">Neue Benutzeroberflächen Features</span><span class="sxs-lookup"><span data-stu-id="5e9d3-115">New User Interface Features</span></span>

* <span data-ttu-id="5e9d3-116">Bedeutende Leistungsverbesserungen vor allem auf den Registerkarten installiert, Updates und konsolidiert</span><span class="sxs-lookup"><span data-stu-id="5e9d3-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="5e9d3-117">Registerkarten "installiert" und "Updates" sind nun alphabetisch sortiert</span><span class="sxs-lookup"><span data-stu-id="5e9d3-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="5e9d3-118">Die Schaltfläche "Aktualisieren" wurde hinzugefügt, die die Aktualisierung einer Suche ermöglicht</span><span class="sxs-lookup"><span data-stu-id="5e9d3-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="5e9d3-119">Updates und Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="5e9d3-119">Updates and Improvements</span></span>

* <span data-ttu-id="5e9d3-120">Pakete, auf die in verwiesen wird und die eine unverankerte `project.json` Version aufweisen, werden bei jedem Build nicht aktualisiert</span><span class="sxs-lookup"><span data-stu-id="5e9d3-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="5e9d3-121">Stattdessen werden Sie nur aktualisiert, wenn Sie zum Wiederherstellen, bereinigen, Neuerstellen oder ändern gezwungen werden `project.json` .</span><span class="sxs-lookup"><span data-stu-id="5e9d3-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="5e9d3-122">nuget.org-Repository-Quellen werden nicht mehr in einer Projekt Konfiguration erzwungen, wenn Sie die nuget-Konfigurations Benutzeroberfläche verwenden.</span><span class="sxs-lookup"><span data-stu-id="5e9d3-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="5e9d3-123">Mit nuget werden Pakete nicht mehr in freigegebenen Projekten wieder hergestellt, und es wird keine Sperrdatei geschrieben.</span><span class="sxs-lookup"><span data-stu-id="5e9d3-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="5e9d3-124">Wir haben den Netzwerkfehler verbessert und die Verarbeitung für nicht erreichbare oder langsame Server erneut versucht.</span><span class="sxs-lookup"><span data-stu-id="5e9d3-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="5e9d3-125">Tastatur-und Maus Verhalten werden in der Visual Studio-Benutzeroberfläche des Paket-Managers verbessert.</span><span class="sxs-lookup"><span data-stu-id="5e9d3-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="5e9d3-126">Wir unterstützen jetzt das aktuellste `project.json` Schema in DNX.</span><span class="sxs-lookup"><span data-stu-id="5e9d3-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="5e9d3-127">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="5e9d3-127">Known Issues</span></span>

<span data-ttu-id="5e9d3-128">Wir verfolgen weiterhin Probleme in unserer GitHub-Liste mit Problemen, die unter folgenden Themen zu finden sind: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="5e9d3-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>