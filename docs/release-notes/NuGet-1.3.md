---
title: Anmerkungen zu NuGet 1.3
description: Anmerkungen zu NuGet 1.3, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551350"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="43d90-103">Anmerkungen zu NuGet 1.3</span><span class="sxs-lookup"><span data-stu-id="43d90-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="43d90-104">[Anmerkungen zu NuGet 1.2](../release-notes/nuget-1.2.md) | [Anmerkungen zu NuGet 1.4](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="43d90-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="43d90-105">NuGet 1.3 wurde 25 April 2011 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="43d90-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="43d90-106">Neue Funktionen</span><span class="sxs-lookup"><span data-stu-id="43d90-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="43d90-107">Optimierte Paketerstellung mit Symbol-Server-integration</span><span class="sxs-lookup"><span data-stu-id="43d90-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="43d90-108">Das NuGet-Team eine Partnerschaft eingegangen, mit den Leuten bei [SymbolSource.org](http://www.symbolsource.org/) bieten eine ganz einfache Möglichkeit der Veröffentlichung von Ihren Quellen und der PDB Datei zusammen mit Ihrem Paket.</span><span class="sxs-lookup"><span data-stu-id="43d90-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="43d90-109">Dieser Funktion können Consumer des Pakets die Quelle für das Paket im Debugger schrittweise.</span><span class="sxs-lookup"><span data-stu-id="43d90-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="43d90-110">Weitere Informationen finden Sie in [erstellen und Veröffentlichen eines Symbolpakets](../create-packages/symbol-packages.md) eine einfache Methode zum Veröffentlichen von NuGet-Pakete mit Datenquellen.</span><span class="sxs-lookup"><span data-stu-id="43d90-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="43d90-111">Sie können auch eine live-Demonstration dieser Funktion als Teil des NuGet-Pakets im Detail sprechen MIX11 ansehen.</span><span class="sxs-lookup"><span data-stu-id="43d90-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="43d90-112">Dieses Feature wird vollständig veranschaulicht. an der Marke 20-minütige des Videos ab.</span><span class="sxs-lookup"><span data-stu-id="43d90-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="43d90-113">`Open-PackagePage` Befehl</span><span class="sxs-lookup"><span data-stu-id="43d90-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="43d90-114">Mit diesem Befehl erleichtert es, um das Projekt – Seite für ein Paket aus, in der Paket-Manager-Konsole zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="43d90-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="43d90-115">Darüber hinaus Optionen, um die Lizenz-URL und den Missbrauch Berichtsseite für das Paket zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="43d90-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="43d90-116">Die Syntax für den Befehl lautet:</span><span class="sxs-lookup"><span data-stu-id="43d90-116">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="43d90-117">Die `-PassThru` Option wird verwendet, um den Wert der angegebenen URL zurück.</span><span class="sxs-lookup"><span data-stu-id="43d90-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="43d90-118">Beispiele:</span><span class="sxs-lookup"><span data-stu-id="43d90-118">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="43d90-119">Öffnet einen Browser mit der im Ninject-Paket angegebenen Projekt-URL.</span><span class="sxs-lookup"><span data-stu-id="43d90-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="43d90-120">Öffnet einen Browser mit der im Ninject-Paket angegebenen Lizenz-URL.</span><span class="sxs-lookup"><span data-stu-id="43d90-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="43d90-121">Öffnet einen Browser für die URL auf der aktuellen Paketquelle, die zum Melden von Missbrauch für das angegebene Paket.</span><span class="sxs-lookup"><span data-stu-id="43d90-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="43d90-122">Die URL der Variablen zugewiesen, $url, ohne die URL in einem Browser öffnen.</span><span class="sxs-lookup"><span data-stu-id="43d90-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="43d90-123">Leistungsverbesserungen</span><span class="sxs-lookup"><span data-stu-id="43d90-123">Performance Improvements</span></span>

<span data-ttu-id="43d90-124">NuGet 1.3 werden viele der leistungsverbesserungen eingeführt.</span><span class="sxs-lookup"><span data-stu-id="43d90-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="43d90-125">NuGet 1.3 verhindert das Herunterladen von mehrere Male mit einem pro Benutzer lokalen Cache für der gleichen Version eines Pakets.</span><span class="sxs-lookup"><span data-stu-id="43d90-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="43d90-126">Der Cache zugegriffen, und über das Dialogfeld "Paket-Manager-Einstellungen" deaktiviert werden kann:</span><span class="sxs-lookup"><span data-stu-id="43d90-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![NuGet-Dialogfeld "Optionen" mit Cache-Paketeinstellungen](./media/nuget-options.png)

<span data-ttu-id="43d90-128">Andere leistungsoptimierungen gehören das Hinzufügen von Unterstützung für HTTP-Komprimierung, und Verbessern der Geschwindigkeit der Paket-Installation in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="43d90-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="43d90-129">Visual Studio und nuget.exe verwendet die gleiche Liste von Paketquellen</span><span class="sxs-lookup"><span data-stu-id="43d90-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="43d90-130">Vor dem NuGet-1.3 die Liste der Paketquellen von nuget.exe und dem NuGet Visual Studio-Add-In verwendet wurden nicht gespeichert am selben Ort.</span><span class="sxs-lookup"><span data-stu-id="43d90-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="43d90-131">NuGet 1.3 verwendet jetzt die gleiche Liste an beiden Orten.</span><span class="sxs-lookup"><span data-stu-id="43d90-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="43d90-132">Die Liste wird gespeichert, `NuGet.Config` und im Ordner "AppData" gespeichert.</span><span class="sxs-lookup"><span data-stu-id="43d90-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="43d90-133">NuGet.exe ignoriert Dateien und Ordnern, die mit '.' in der Standardeinstellung</span><span class="sxs-lookup"><span data-stu-id="43d90-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="43d90-134">Um NuGet mit Quellcodeverwaltungssystemen wie Subversion und Mercurial arbeiten zu können, nuget.exe ignoriert, Ordner und Dateien, die mit der '.' Zeichen beim Erstellen von Paketen.</span><span class="sxs-lookup"><span data-stu-id="43d90-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="43d90-135">Dies kann mit zwei neuen Flags überschrieben werden:</span><span class="sxs-lookup"><span data-stu-id="43d90-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="43d90-136">__-NoDefaultExcludes__ wird verwendet, um diese Einstellung überschreiben, und schließen Sie alle Dateien.</span><span class="sxs-lookup"><span data-stu-id="43d90-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="43d90-137">__-Ausschließen__ wird verwendet, um andere Dateien bzw. Ordner ausschließen, unter Verwendung eines Musters hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="43d90-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="43d90-138">Um beispielsweise alle Dateien mit der Dateierweiterung '. bak' ausschließen</span><span class="sxs-lookup"><span data-stu-id="43d90-138">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="43d90-139">_Hinweis: das Muster ist nicht standardmäßig rekursiv._</span><span class="sxs-lookup"><span data-stu-id="43d90-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="43d90-140">Unterstützung für WiX-Projekten und .NET Micro Framework</span><span class="sxs-lookup"><span data-stu-id="43d90-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="43d90-141">Unser Dank gilt den Community-Beiträge unterstützt NuGet WiX-Projekttypen als auch das .NET Micro Framework.</span><span class="sxs-lookup"><span data-stu-id="43d90-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="43d90-142">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="43d90-142">Bug Fixes</span></span>

<span data-ttu-id="43d90-143">Eine vollständige Liste der Fehlerbehebungen, lesen Sie die [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="43d90-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="43d90-144">Fehlerkorrekturen Beachten</span><span class="sxs-lookup"><span data-stu-id="43d90-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="43d90-145">Pakete mit den Quelldateien funktioniert in beide Websites und Web Application Projects.</span><span class="sxs-lookup"><span data-stu-id="43d90-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="43d90-146">Für Websites, Quelldateien kopiert werden, in der `App_Code` Ordner</span><span class="sxs-lookup"><span data-stu-id="43d90-146">For Websites, source files are copied into the `App_Code` folder</span></span>
