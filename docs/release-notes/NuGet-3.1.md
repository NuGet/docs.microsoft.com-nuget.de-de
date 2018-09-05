---
title: Anmerkungen zu NuGet 3.1
description: Anmerkungen zu NuGet 3.1, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545346"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="bdd12-103">Anmerkungen zu NuGet 3.1</span><span class="sxs-lookup"><span data-stu-id="bdd12-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="bdd12-104">[Anmerkungen zu NuGet 3.0](../release-notes/nuget-3.0.0.md) | [Anmerkungen zu NuGet 3.1.1](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="bdd12-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="bdd12-105">NuGet 3.1 wurde als gebündelte Universal Windows Platform SDK-Erweiterung für Visual Studio 2015 27 Juli 2015 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="bdd12-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="bdd12-106">Wir übermittelt diese Version mit dem Windows-Plattform-SDK, damit die Windows-Entwicklungsumgebung NuGet plattformübergreifende Arbeit nutzen kann, die zuvor gestartet worden.</span><span class="sxs-lookup"><span data-stu-id="bdd12-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="bdd12-107">Diese Version des NuGet-Erweiterung ist nur für Visual Studio 2015 verfügbar.</span><span class="sxs-lookup"><span data-stu-id="bdd12-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="bdd12-108">Es wird empfohlen, die Entwickler, die Zugriff auf Visual Studio-Update-Katalog auf die neueste Version verfügen, die verfügbar ist, da wir immer Veröffentlichen von Updates mit Fehlerbehebungen und neuen Features sind.</span><span class="sxs-lookup"><span data-stu-id="bdd12-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="bdd12-109">NuGet Visual Studio-Erweiterung</span><span class="sxs-lookup"><span data-stu-id="bdd12-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="bdd12-110">Probleme und Funktionen in dieser Version sind auf GitHub markiert die ["transitive 3.1 RTM UWP-Unterstützung" Meilenstein](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) insgesamt schließen wir 67 Probleme in der Version 3.1.</span><span class="sxs-lookup"><span data-stu-id="bdd12-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="bdd12-111">Neue Funktionen</span><span class="sxs-lookup"><span data-stu-id="bdd12-111">New Features</span></span>

* <span data-ttu-id="bdd12-112">`project.json` Unterstützung für Windows UWP und ASP.NET 5-Unterstützung</span><span class="sxs-lookup"><span data-stu-id="bdd12-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="bdd12-113">Transitiver Paketverweise-installation</span><span class="sxs-lookup"><span data-stu-id="bdd12-113">Transitive package installation</span></span>

<span data-ttu-id="bdd12-114">Beschreibungs- und Definitionseigenschaften dieser Features an anderer Stelle in der Dokumentation zu finden.</span><span class="sxs-lookup"><span data-stu-id="bdd12-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="bdd12-115">Als veraltet markiert</span><span class="sxs-lookup"><span data-stu-id="bdd12-115">Deprecated</span></span>

<span data-ttu-id="bdd12-116">Die folgenden Funktionen sind nicht mehr für Visual Studio 2015 zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="bdd12-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="bdd12-117">Level-Lösungspakete können nicht mehr installiert werden</span><span class="sxs-lookup"><span data-stu-id="bdd12-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="bdd12-118">Die folgenden Funktionen sind nicht mehr verfügbar ist, für Visual Studio 2015 und Projekte, mit denen die `project.json` Spezifikation</span><span class="sxs-lookup"><span data-stu-id="bdd12-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="bdd12-119">`install.ps1` und `uninstall.ps1` -diese Skripts werden während der Installation des Pakets ignoriert werden, wiederherstellen, aktualisieren und deinstallieren</span><span class="sxs-lookup"><span data-stu-id="bdd12-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="bdd12-120">Konfiguration von Transformationen werden ignoriert</span><span class="sxs-lookup"><span data-stu-id="bdd12-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="bdd12-121">Inhalt wird ausgeführt, aber nicht in einem Projekt kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="bdd12-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="bdd12-122">Das Team arbeitet daran, dieses Feature erneut zu implementieren, führen die Diskussion und Fortschritt: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="bdd12-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="bdd12-123">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="bdd12-123">Known Issues</span></span>

<span data-ttu-id="bdd12-124">Es gab eine Reihe bekannter Probleme, die mit dieser Version bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="bdd12-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="bdd12-125">Installation von der Version 3.1, mit dem Windows 10 SDK wird jede Version von NuGet-Erweiterung herabgestuft, die zuvor installiert wurde</span><span class="sxs-lookup"><span data-stu-id="bdd12-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="bdd12-126">NuGet-Befehlszeile</span><span class="sxs-lookup"><span data-stu-id="bdd12-126">NuGet Command-line</span></span>

<span data-ttu-id="bdd12-127">Die NuGet-Befehlszeile ausführbare Datei wurde aktualisiert und an einen neuen verteilbarer Speicherort verschoben werden, sodass historische nuget.exe-Versionen weiterhin zur Verfügung gestellt werden können.</span><span class="sxs-lookup"><span data-stu-id="bdd12-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="bdd12-128">Sie können die 3.1 Betaversion von nuget.exe für Windows auf herunterladen: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="bdd12-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="bdd12-129">Der neue Speicherort des verteilbare befindet sich auf dem Host "dist.NuGet.org" mit einer Ordnerstruktur, die diese Vorlage folgt:</span><span class="sxs-lookup"><span data-stu-id="bdd12-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="bdd12-130">Neue Funktionen</span><span class="sxs-lookup"><span data-stu-id="bdd12-130">New Features</span></span>

* <span data-ttu-id="bdd12-131">NuGet.exe wiederherstellen können, und installieren Sie Pakete in Projekten, mit denen eine `project.json` Datei.</span><span class="sxs-lookup"><span data-stu-id="bdd12-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="bdd12-132">NuGet.exe können Herstellen einer Verbindung mit und nutzen die NuGet-v3-Protokolls an: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="bdd12-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="bdd12-133">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="bdd12-133">Known Issues</span></span> ##

1.    <span data-ttu-id="bdd12-134">Kann nicht ausgeführt werden Pack für ein `project.json` -Datei – [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="bdd12-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="bdd12-135">Wird nicht unterstützt, auf das Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="bdd12-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="bdd12-136">Ist nicht lokalisiert - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="bdd12-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="bdd12-137">Ist nicht signiert, wie die vorhandene http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="bdd12-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
