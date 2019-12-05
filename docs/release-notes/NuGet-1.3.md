---
title: Anmerkungen zu dieser Version von nuget 1,3
description: Anmerkungen zu dieser Version von nuget 1,3 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 45d5caa46d532670e370b81f675663b3c5aaaa95
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825262"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="57e7c-103">Anmerkungen zu dieser Version von nuget 1,3</span><span class="sxs-lookup"><span data-stu-id="57e7c-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="57e7c-104">Anmerkungen zu [nuget 1,2](../release-notes/nuget-1.2.md) | Anmerkungen zur [nuget](../release-notes/nuget-1.4.md) -Version 1,4</span><span class="sxs-lookup"><span data-stu-id="57e7c-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="57e7c-105">Nuget 1,3 wurde am 25. April 2011 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="57e7c-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="57e7c-106">Neue Features</span><span class="sxs-lookup"><span data-stu-id="57e7c-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="57e7c-107">Optimierte Paket Erstellung mit Symbol Server Integration</span><span class="sxs-lookup"><span data-stu-id="57e7c-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="57e7c-108">Das nuget-Team arbeitet mit den Leuten auf [SymbolSource.org](http://www.symbolsource.org/) zusammen, um eine ganz einfache Möglichkeit zum Veröffentlichen von Quellen und PDB zusammen mit dem Paket zu bieten.</span><span class="sxs-lookup"><span data-stu-id="57e7c-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="57e7c-109">Dies ermöglicht es den Benutzern des Pakets, den Einzelschritt in die Quelle Ihres Pakets im Debugger zu überspringen.</span><span class="sxs-lookup"><span data-stu-id="57e7c-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="57e7c-110">Weitere Informationen finden Sie unter [Erstellen und Veröffentlichen eines Symbol Pakets](../create-packages/symbol-packages.md) auf einfache Art und Weise, wie Sie nuget-Pakete mit Quellen veröffentlichen können.</span><span class="sxs-lookup"><span data-stu-id="57e7c-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="57e7c-111">Sie können sich auch eine Live Demonstration dieses Features als Teil von nuget eingehend unter Mix11 ansehen.</span><span class="sxs-lookup"><span data-stu-id="57e7c-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="57e7c-112">Diese Funktion wird ab der 20-minütigen Markierung des Videos vollständig veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="57e7c-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="57e7c-113">`Open-PackagePage` -Befehl</span><span class="sxs-lookup"><span data-stu-id="57e7c-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="57e7c-114">Mit diesem Befehl können Sie in der Paket-Manager-Konsole problemlos zur Projektseite für ein Paket gelangen.</span><span class="sxs-lookup"><span data-stu-id="57e7c-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="57e7c-115">Außerdem bietet es Optionen zum Öffnen der Lizenz-URL und der Seite "Missbrauch melden" für das Paket.</span><span class="sxs-lookup"><span data-stu-id="57e7c-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="57e7c-116">Die Syntax für den Befehl lautet wie folgt:</span><span class="sxs-lookup"><span data-stu-id="57e7c-116">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="57e7c-117">Die `-PassThru`-Option wird verwendet, um den Wert der angegebenen URL zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="57e7c-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="57e7c-118">Beispiele:</span><span class="sxs-lookup"><span data-stu-id="57e7c-118">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="57e7c-119">Öffnet einen Browser mit der Projekt-URL, die im Ninject-Paket angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="57e7c-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="57e7c-120">Öffnet einen Browser mit der Lizenz-URL, die im Ninject-Paket angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="57e7c-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="57e7c-121">Öffnet einen Browser mit der URL in der aktuellen Paketquelle, die zum Melden von Missbrauch für das angegebene Paket verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="57e7c-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="57e7c-122">Weist die Lizenz-URL der Variablen zu, $URL, ohne die URL in einem Browser zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="57e7c-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="57e7c-123">Leistungsverbesserungen</span><span class="sxs-lookup"><span data-stu-id="57e7c-123">Performance Improvements</span></span>

<span data-ttu-id="57e7c-124">Mit nuget 1,3 werden zahlreiche Leistungsverbesserungen eingeführt.</span><span class="sxs-lookup"><span data-stu-id="57e7c-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="57e7c-125">Mit nuget 1,3 wird vermieden, dass die gleiche Version eines Pakets mehrmals heruntergeladen wird, indem ein lokaler Cache pro Benutzer eingeschlossen wird.</span><span class="sxs-lookup"><span data-stu-id="57e7c-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="57e7c-126">Der Cache kann über das Dialogfeld "Paket-Manager-Einstellungen" aufgerufen und gelöscht werden:</span><span class="sxs-lookup"><span data-stu-id="57e7c-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Dialog Feld "nuget-Optionen" mit Paket Cache Einstellungen](./media/nuget-options.png)

<span data-ttu-id="57e7c-128">Weitere Leistungsverbesserungen umfassen das Hinzufügen von Unterstützung für die HTTP-Komprimierung und die Verbesserung der Paket Installations Geschwindigkeit in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="57e7c-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="57e7c-129">In Visual Studio und "nuget. exe" wird dieselbe Liste von Paketquellen verwendet.</span><span class="sxs-lookup"><span data-stu-id="57e7c-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="57e7c-130">Vor nuget 1,3 wurden die von "nuget. exe" und dem nuget Visual Studio-Add-in verwendeten Paketquellen nicht an derselben Stelle gespeichert.</span><span class="sxs-lookup"><span data-stu-id="57e7c-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="57e7c-131">Nuget 1,3 verwendet nun dieselbe Liste an beiden stellen.</span><span class="sxs-lookup"><span data-stu-id="57e7c-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="57e7c-132">Die Liste wird in `NuGet.Config` gespeichert und im Ordner AppData gespeichert.</span><span class="sxs-lookup"><span data-stu-id="57e7c-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="57e7c-133">"nuget. exe" ignoriert Dateien und Ordner, die standardmäßig mit "." beginnen.</span><span class="sxs-lookup"><span data-stu-id="57e7c-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="57e7c-134">Damit nuget gut mit Quell Code Verwaltungssystemen wie Subversion und mercurial funktioniert, ignoriert nuget. exe Ordner und Dateien, die mit dem Zeichen "." beginnen, wenn Pakete erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="57e7c-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="57e7c-135">Dies kann überschrieben werden, indem zwei neue Flags verwendet werden:</span><span class="sxs-lookup"><span data-stu-id="57e7c-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="57e7c-136">__-Nodefaultexcludes__ wird verwendet, um diese Einstellung zu überschreiben und alle Dateien einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="57e7c-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="57e7c-137">__-Exclude__ wird verwendet, um andere Dateien/Ordner hinzuzufügen, die mit einem Muster ausgeschlossen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="57e7c-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="57e7c-138">Um z. b. alle Dateien mit der Dateierweiterung ". bak" auszuschließen.</span><span class="sxs-lookup"><span data-stu-id="57e7c-138">For example, to exclude all files with the '.bak' file extension</span></span>

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="57e7c-139">_Hinweis: das Muster ist standardmäßig nicht rekursiv._</span><span class="sxs-lookup"><span data-stu-id="57e7c-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="57e7c-140">Unterstützung für WiX-Projekte und .net Micro Framework</span><span class="sxs-lookup"><span data-stu-id="57e7c-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="57e7c-141">Dank der Communitybeiträge unterstützt nuget sowohl WiX-Projekttypen als auch das .net Micro Framework.</span><span class="sxs-lookup"><span data-stu-id="57e7c-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="57e7c-142">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="57e7c-142">Bug Fixes</span></span>

<span data-ttu-id="57e7c-143">Eine vollständige Liste der Fehlerbehebungen finden Sie in der [nuget-Problemverfolgung für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="57e7c-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="57e7c-144">Fehlerbehebungen erwähnenswert</span><span class="sxs-lookup"><span data-stu-id="57e7c-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="57e7c-145">Pakete mit Quelldateien können sowohl in Websites als auch in Webanwendungs Projekten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="57e7c-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="57e7c-146">Bei Websites werden Quelldateien in den `App_Code` Ordner kopiert.</span><span class="sxs-lookup"><span data-stu-id="57e7c-146">For Websites, source files are copied into the `App_Code` folder</span></span>
