---
title: 1.3 NuGet-Versionshinweise
description: Versionshinweise für NuGet 1.3 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c0284fe0afb11bf6465897132cccd160674ea3e1
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="60cd4-103">1.3 NuGet-Versionshinweise</span><span class="sxs-lookup"><span data-stu-id="60cd4-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="60cd4-104">[Anmerkungen zur Version von NuGet 1.2](../release-notes/nuget-1.2.md) | [NuGet 1.4-Versionshinweise](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="60cd4-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="60cd4-105">NuGet 1.3 wurde 25 April 2011 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="60cd4-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="60cd4-106">Neue Funktionen</span><span class="sxs-lookup"><span data-stu-id="60cd4-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="60cd4-107">Optimierte Paketerstellung mit Symbol-Server-integration</span><span class="sxs-lookup"><span data-stu-id="60cd4-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="60cd4-108">Das NuGet-Team uns, mit der Mitarbeiter bei [SymbolSource.org](http://www.symbolsource.org/) eine sehr einfache Art veröffentlichen Ihre Datenquellen und die PDB-Datei zusammen mit dem Paket anbieten.</span><span class="sxs-lookup"><span data-stu-id="60cd4-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="60cd4-109">Dieser Funktion können Consumer des Pakets die Quelle für das Paket im Debugger schrittweise.</span><span class="sxs-lookup"><span data-stu-id="60cd4-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="60cd4-110">Weitere Informationen finden Sie unter [erstellen und veröffentlichen ein Symbolpaket](../create-packages/symbol-packages.md) die einfache Methode zum Veröffentlichen von NuGet-Pakete mit Datenquellen.</span><span class="sxs-lookup"><span data-stu-id="60cd4-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="60cd4-111">Sie können auch eine live-Demonstration dieses Features im Rahmen des NuGet-ausführlich auf Mix11 wenden Sie sich ansehen.</span><span class="sxs-lookup"><span data-stu-id="60cd4-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="60cd4-112">Diese Funktion wird vollständig veranschaulicht beginnend mit der Markierung 20-minütige des Videos.</span><span class="sxs-lookup"><span data-stu-id="60cd4-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="60cd4-113">`Open-PackagePage` Befehl</span><span class="sxs-lookup"><span data-stu-id="60cd4-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="60cd4-114">Dieser Befehl vereinfacht, um die Seite "Projekt" für ein Paket aus, in der Paket-Manager-Konsole zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="60cd4-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="60cd4-115">Darüber hinaus Optionen, um die Lizenz-URL und den Missbrauch Berichtsseite für das Paket zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="60cd4-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="60cd4-116">Die Syntax für den Befehl lautet:</span><span class="sxs-lookup"><span data-stu-id="60cd4-116">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="60cd4-117">Die `-PassThru` Option wird verwendet, um den Wert der angegebenen URL zurück.</span><span class="sxs-lookup"><span data-stu-id="60cd4-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="60cd4-118">Beispiele:</span><span class="sxs-lookup"><span data-stu-id="60cd4-118">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="60cd4-119">Öffnet einen Browser mit der im Ninject-Paket angegebenen Projekt-URL.</span><span class="sxs-lookup"><span data-stu-id="60cd4-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="60cd4-120">Öffnet einen Browser mit der im Ninject-Paket angegebenen Lizenz-URL.</span><span class="sxs-lookup"><span data-stu-id="60cd4-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="60cd4-121">Öffnet einen Browser für die URL auf der aktuellen Paketquelle zum Melden des Missbrauchs des angegebenen Pakets verwendet.</span><span class="sxs-lookup"><span data-stu-id="60cd4-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="60cd4-122">Weist die Lizenz-URL der Variablen, $url, ohne die URL in einem Browser öffnen.</span><span class="sxs-lookup"><span data-stu-id="60cd4-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="60cd4-123">Leistungsverbesserungen</span><span class="sxs-lookup"><span data-stu-id="60cd4-123">Performance Improvements</span></span>

<span data-ttu-id="60cd4-124">NuGet-1.3 führt viele leistungsverbesserungen.</span><span class="sxs-lookup"><span data-stu-id="60cd4-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="60cd4-125">NuGet-1.3 wird vermieden, Herunterladen von mehrmals von einschließlich eines pro Benutzer lokaler Caches für die gleiche Version eines Pakets.</span><span class="sxs-lookup"><span data-stu-id="60cd4-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="60cd4-126">Der Cache zugegriffen, und über das Dialogfeld mit Paket-Manager deaktiviert werden kann:</span><span class="sxs-lookup"><span data-stu-id="60cd4-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![NuGet-Dialogfeld "Optionen" mit Paket-Cache-Einstellungen](./media/nuget-options.png)

<span data-ttu-id="60cd4-128">Andere leistungsverbesserungen gehören Hinzufügen der Unterstützung für HTTP-Komprimierung und Verbessern der Geschwindigkeit der Paket-Installation in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="60cd4-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="60cd4-129">Visual Studio und nuget.exe verwendet dieselbe Liste der Paketquellen überein</span><span class="sxs-lookup"><span data-stu-id="60cd4-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="60cd4-130">Vor dem NuGet-1.3 die Liste der Paketquellen von nuget.exe und die NuGet-Visual Studio-Add-In verwendet wurden nicht gespeichert am gleichen Ort.</span><span class="sxs-lookup"><span data-stu-id="60cd4-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="60cd4-131">NuGet-1.3 verwendet jetzt die gleiche Liste an beiden Orten.</span><span class="sxs-lookup"><span data-stu-id="60cd4-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="60cd4-132">Die Liste wird gespeichert, `NuGet.Config` und im Ordner "Anwendungsdaten" gespeichert.</span><span class="sxs-lookup"><span data-stu-id="60cd4-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="60cd4-133">NuGet.exe ignoriert Dateien und Ordnern, die beginnen mit "." standardmäßig</span><span class="sxs-lookup"><span data-stu-id="60cd4-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="60cd4-134">Um solche Subversion und Mercurial Arbeit mit Quellcode-Verwaltungssysteme NuGet zu machen, nuget.exe ignoriert, Ordner und Dateien, die mit beginnt die '.' Zeichen beim Erstellen von Paketen.</span><span class="sxs-lookup"><span data-stu-id="60cd4-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="60cd4-135">Dies kann mit zwei neuen Flags überschrieben werden:</span><span class="sxs-lookup"><span data-stu-id="60cd4-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="60cd4-136">__-NoDefaultExcludes__ wird verwendet, um diese Einstellung überschreiben, und schließen Sie alle Dateien.</span><span class="sxs-lookup"><span data-stu-id="60cd4-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="60cd4-137">__-Ausschließen von__ wird verwendet, um weitere Dateien/Ordner ausschließen, die Verwendung eines Musters hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="60cd4-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="60cd4-138">Um beispielsweise alle Dateien mit der Erweiterung ". bak" ausschließen</span><span class="sxs-lookup"><span data-stu-id="60cd4-138">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="60cd4-139">_Hinweis: das Muster ist nicht standardmäßig rekursiv._</span><span class="sxs-lookup"><span data-stu-id="60cd4-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="60cd4-140">Unterstützung für WiX-Projekte und Micro .NET Framework</span><span class="sxs-lookup"><span data-stu-id="60cd4-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="60cd4-141">Dank Beiträge aus der Community enthält NuGet-Unterstützung für WiX-Projekttypen sowie Micro .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="60cd4-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="60cd4-142">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="60cd4-142">Bug Fixes</span></span>

<span data-ttu-id="60cd4-143">Eine vollständige Liste von Fehlerbehebungen, besuchen Sie die [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="60cd4-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="60cd4-144">Fehlerkorrekturen erwähnenswerte</span><span class="sxs-lookup"><span data-stu-id="60cd4-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="60cd4-145">Pakete mit Quelldateien arbeiten beide Websites und Webanwendungsprojekte.</span><span class="sxs-lookup"><span data-stu-id="60cd4-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="60cd4-146">Für Websites, Quelldateien kopiert werden, in der `App_Code` Ordner</span><span class="sxs-lookup"><span data-stu-id="60cd4-146">For Websites, source files are copied into the `App_Code` folder</span></span>
