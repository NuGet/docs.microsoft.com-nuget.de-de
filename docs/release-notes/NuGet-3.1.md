---
title: Anmerkungen zu dieser Version von nuget 3,1
description: Anmerkungen zu dieser Version von nuget 3,1 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776538"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="15530-103">Anmerkungen zu dieser Version von nuget 3,1</span><span class="sxs-lookup"><span data-stu-id="15530-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="15530-104">Anmerkungen zu dieser [Version von nuget 3,0](../release-notes/nuget-3.0.0.md)  |  [Anmerkungen zu nuget 3.1.1](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="15530-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="15530-105">Nuget 3,1 wurde am 27. Juli 2015 als gebündelte Erweiterung zum universelle Windows-Plattform SDK für Visual Studio 2015 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="15530-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="15530-106">Wir haben diese Version mit dem Windows Platform SDK geliefert, damit die Windows-Entwicklungsumgebung die plattformübergreifende nuget-Arbeit nutzen kann, die zuvor gestartet wurde.</span><span class="sxs-lookup"><span data-stu-id="15530-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="15530-107">Diese nuget-Erweiterungs Version ist nur für Visual Studio 2015 verfügbar.</span><span class="sxs-lookup"><span data-stu-id="15530-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="15530-108">Wir empfehlen Entwicklern, die Zugriff auf das Visual Studio Gallery-Update haben, auf die neueste Version, die verfügbar ist, da wir immer Updates mit Fehlerbehebungen und neuen Features veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="15530-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="15530-109">Nuget Visual Studio-Erweiterung</span><span class="sxs-lookup"><span data-stu-id="15530-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="15530-110">Probleme und Features in dieser Version sind auf GitHub mit dem [Meilenstein "3,1 RTM UWP transitiv Support"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  gekennzeichnet. Wir haben 67-Probleme in der 3,1-Version geschlossen.</span><span class="sxs-lookup"><span data-stu-id="15530-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="15530-111">Neue Funktionen</span><span class="sxs-lookup"><span data-stu-id="15530-111">New Features</span></span>

* <span data-ttu-id="15530-112">`project.json` Unterstützung für Windows UWP-und ASP.net 5-Unterstützung</span><span class="sxs-lookup"><span data-stu-id="15530-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="15530-113">Transitive Paketinstallation</span><span class="sxs-lookup"><span data-stu-id="15530-113">Transitive package installation</span></span>

<span data-ttu-id="15530-114">Beschreibungen und Definitionen dieser Features finden Sie an anderer Stelle in der Dokumentation.</span><span class="sxs-lookup"><span data-stu-id="15530-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="15530-115">Als veraltet markiert</span><span class="sxs-lookup"><span data-stu-id="15530-115">Deprecated</span></span>

<span data-ttu-id="15530-116">Die folgenden Features sind für Visual Studio 2015 nicht mehr verfügbar:</span><span class="sxs-lookup"><span data-stu-id="15530-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="15530-117">Pakete auf Projektmappenebene können nicht mehr installiert werden.</span><span class="sxs-lookup"><span data-stu-id="15530-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="15530-118">Die folgenden Features sind für Visual Studio 2015 und Projekte, die die Spezifikation verwenden, nicht mehr verfügbar. `project.json`</span><span class="sxs-lookup"><span data-stu-id="15530-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="15530-119">`install.ps1``uninstall.ps1`diese Skripts werden während der Installation, Wiederherstellung, Aktualisierung und Deinstallation von Paketen ignoriert.</span><span class="sxs-lookup"><span data-stu-id="15530-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="15530-120">Konfigurations Transformationen werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="15530-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="15530-121">Inhalt wird übernommen, aber nicht in ein Projekt kopiert.</span><span class="sxs-lookup"><span data-stu-id="15530-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="15530-122">Das Team arbeitet daran, dieses Feature erneut zu implementieren, und befolgt die Diskussion und den Fortschritt unter: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="15530-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="15530-123">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="15530-123">Known Issues</span></span>

<span data-ttu-id="15530-124">Diese Version enthält eine Reihe bekannter Probleme.</span><span class="sxs-lookup"><span data-stu-id="15530-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="15530-125">Durch die Installation der Version 3,1 mit dem Windows 10 SDK wird eine beliebige Version der zuvor installierten nuget-Erweiterung herabgestuft.</span><span class="sxs-lookup"><span data-stu-id="15530-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="15530-126">Nuget-Befehlszeile</span><span class="sxs-lookup"><span data-stu-id="15530-126">NuGet Command-line</span></span>

<span data-ttu-id="15530-127">Die ausführbare nuget-Befehlszeilen Datei wurde aktualisiert und an einen neuen verteilbaren Speicherort verschoben, damit historische Versionen von nuget.exe weiterhin verfügbar gemacht werden können.</span><span class="sxs-lookup"><span data-stu-id="15530-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="15530-128">Sie können die 3,1 Beta Version von nuget.exe für Windows herunterladen unter: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="15530-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="15530-129">Der neue verteilbare Speicherort befindet sich auf dem dist.nuget.org-Host mit einer Ordnerstruktur, die dieser Vorlage folgt:</span><span class="sxs-lookup"><span data-stu-id="15530-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a><span data-ttu-id="15530-130">Neue Funktionen</span><span class="sxs-lookup"><span data-stu-id="15530-130">New Features</span></span>

* <span data-ttu-id="15530-131">nuget.exe können Pakete in Projekten, die eine Datei verwenden, wiederherstellen und installieren `project.json` .</span><span class="sxs-lookup"><span data-stu-id="15530-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="15530-132">nuget.exe können eine Verbindung mit dem nuget V3-Protokoll herstellen und es nutzen unter: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="15530-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="15530-133">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="15530-133">Known Issues</span></span> ##

1.    <span data-ttu-id="15530-134">Das Paket kann nicht für eine Datei ausgeführt werden `project.json` : [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="15530-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="15530-135">Wird in Mono- [1059](https://github.com/NuGet/Home/issues/1059) nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="15530-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="15530-136">Ist nicht lokalisiert- [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="15530-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="15530-137">Ist nicht signiert, genau wie das vorhandene http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="15530-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
