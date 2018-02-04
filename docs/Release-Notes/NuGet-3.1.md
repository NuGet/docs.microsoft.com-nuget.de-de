---
title: Anmerkungen zur Version des NuGet-3.1 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 3.1 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-3.1 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a7aa43b8701b3bbef8f6ebce9a5d636ee1bc6abe
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="1c9c3-104">NuGet-Version 3.1 Hinweise</span><span class="sxs-lookup"><span data-stu-id="1c9c3-104">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="1c9c3-105">[Anmerkungen zur Version des NuGet-3.0](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1-Versionshinweise](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="1c9c3-105">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="1c9c3-106">NuGet-3.1 wurde 27 Juli 2015 als gebündelte Universal Windows Platform SDK-Erweiterung für Visual Studio 2015 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-106">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="1c9c3-107">Diese Version mit der Windows-Plattform-SDK von uns bereitgestellten, damit der Windows-entwicklungserfahrung NuGet plattformübergreifende Arbeit nutzen konnte, die zuvor gestartete.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-107">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="1c9c3-108">Diese Version des NuGet-Erweiterung ist nur für Visual Studio 2015 verfügbar.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="1c9c3-109">Es wird empfohlen, die Entwickler, die Zugriff auf die Visual Studio Gallery-Update auf die neueste Version verfügen, die verfügbar ist, ist es immer Veröffentlichen von Updates mit Fehlerkorrekturen und neue Funktionen sind.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-109">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="1c9c3-110">NuGet Visual Studio-Erweiterung</span><span class="sxs-lookup"><span data-stu-id="1c9c3-110">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="1c9c3-111">Probleme und Funktionen in dieser Version sind auf GitHub markiert die ["3.1 transitiv RTM uwp-Support" Meilenstein](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) insgesamt wir 67 Probleme in der Version 3.1 geschlossen.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-111">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="1c9c3-112">Neue Funktionen</span><span class="sxs-lookup"><span data-stu-id="1c9c3-112">New Features</span></span>

* <span data-ttu-id="1c9c3-113">`project.json`Unterstützung für Windows-UWP und ASP.NET 5 Unterstützung</span><span class="sxs-lookup"><span data-stu-id="1c9c3-113">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="1c9c3-114">Transitiv Paketinstallation</span><span class="sxs-lookup"><span data-stu-id="1c9c3-114">Transitive package installation</span></span>

<span data-ttu-id="1c9c3-115">Beschreibung "und" Definition dieser Funktionen können an anderer Stelle in der Dokumentation gefunden werden.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-115">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="1c9c3-116">Als veraltet markiert</span><span class="sxs-lookup"><span data-stu-id="1c9c3-116">Deprecated</span></span>

<span data-ttu-id="1c9c3-117">Die folgenden Funktionen sind nicht mehr für Visual Studio 2015 verfügbar:</span><span class="sxs-lookup"><span data-stu-id="1c9c3-117">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="1c9c3-118">Level-Lösungspakete können nicht mehr installiert werden</span><span class="sxs-lookup"><span data-stu-id="1c9c3-118">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="1c9c3-119">Die folgenden Funktionen sind nicht mehr verfügbar, für die Visual Studio 2015 und Projekte, mit denen die `project.json` Spezifikation</span><span class="sxs-lookup"><span data-stu-id="1c9c3-119">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="1c9c3-120">`install.ps1`und `uninstall.ps1` -diese Skripts während der Paketinstallation ignoriert werden, stellen Sie wieder her, aktualisieren und deinstallieren</span><span class="sxs-lookup"><span data-stu-id="1c9c3-120">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="1c9c3-121">Konfiguration Transformationen werden ignoriert</span><span class="sxs-lookup"><span data-stu-id="1c9c3-121">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="1c9c3-122">Inhalt wird ausgeführt, aber nicht in ein Projekt kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-122">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="1c9c3-123">Das Team arbeitet daran, diese Funktion erneut implementieren, führen die Diskussion und aktueller Fortschritt: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="1c9c3-123">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="1c9c3-124">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="1c9c3-124">Known Issues</span></span>

<span data-ttu-id="1c9c3-125">Es wurden einige bekannte Probleme in dieser Version übermittelt.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-125">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="1c9c3-126">Installation der mit dem Windows 10-SDK-Version 3.1 downgrade wird Version des NuGet-Erweiterung, die zuvor installiert wurde</span><span class="sxs-lookup"><span data-stu-id="1c9c3-126">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="1c9c3-127">NuGet-Befehlszeile</span><span class="sxs-lookup"><span data-stu-id="1c9c3-127">NuGet Command-line</span></span>

<span data-ttu-id="1c9c3-128">Ausführbare Befehlszeilendatei "NuGet" wurde aktualisiert und an einem neuen verteilbarer Speicherort verschoben werden, sodass frühere Versionen des nuget.exe fortgesetzt werden können, zur Verfügung gestellt werden.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-128">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="1c9c3-129">Sie können die 3.1 Beta-Version von nuget.exe für Windows herunterladen: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="1c9c3-129">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="1c9c3-130">Die neue Position des verteilbare befindet sich auf dem Host dist.nuget.org mit eine Ordnerstruktur, die mit dieser Vorlage folgt:</span><span class="sxs-lookup"><span data-stu-id="1c9c3-130">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="1c9c3-131">Neue Funktionen</span><span class="sxs-lookup"><span data-stu-id="1c9c3-131">New Features</span></span>

* <span data-ttu-id="1c9c3-132">NuGet.exe können wiederherstellen und Installieren von Paketen in-Projekte, mit denen eine `project.json` Datei.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-132">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="1c9c3-133">NuGet.exe können Herstellen einer Verbindung mit und nutzen Sie das NuGet-v3-Protokolls an: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="1c9c3-133">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="1c9c3-134">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="1c9c3-134">Known Issues</span></span> ##

1.    <span data-ttu-id="1c9c3-135">Kann nicht ausgeführt werden Pack für ein `project.json` Datei - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="1c9c3-135">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="1c9c3-136">Wird nicht unterstützt, auf das Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="1c9c3-136">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="1c9c3-137">Ist nicht lokalisiert - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="1c9c3-137">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="1c9c3-138">Ist nicht signiert, wie die vorhandene http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="1c9c3-138">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
