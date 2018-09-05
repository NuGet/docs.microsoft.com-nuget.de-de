---
title: Anmerkungen zu NuGet-Version 2.2
description: Anmerkungen zu NuGet 2.2, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545991"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="a3fdd-103">Anmerkungen zu NuGet-Version 2.2</span><span class="sxs-lookup"><span data-stu-id="a3fdd-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="a3fdd-104">[Anmerkungen zu NuGet 2.1](../release-notes/nuget-2.1.md) | [Anmerkungen zu NuGet 2.2.1](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="a3fdd-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="a3fdd-105">NuGet 2.2 wurde am 12. Dezember 2012 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="a3fdd-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="a3fdd-106">Visual Studio-Schnellstart</span><span class="sxs-lookup"><span data-stu-id="a3fdd-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="a3fdd-107">Eines der neuen Features, die in Visual Studio 2012 hinzugefügt wurde wurde die [Schnellstart Dialogfeld](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="a3fdd-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="a3fdd-108">NuGet 2.2 erweitert dieses Dialogfeld ermöglicht es, um das Dialogfeld "Paket-Manager" mit den Suchbegriffen, die in der Schnellstartleiste eingegeben zu initialisieren.</span><span class="sxs-lookup"><span data-stu-id="a3fdd-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="a3fdd-109">Jetzt eingeben von "Jquery" in der Schnellstartleiste umfasst z. B. eine Option in den Ergebnissen aus, um NuGet-Pakete, die Übereinstimmung von "Jquery" zu suchen.</span><span class="sxs-lookup"><span data-stu-id="a3fdd-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![NuGet in Visual Studio-Schnellstart](./media/quick-launch.png)

<span data-ttu-id="a3fdd-111">Nach Auswahl dieser Option wird die standard NuGet-Paket-Manager Suchfunktion für den Begriff "Jquery" gestartet.</span><span class="sxs-lookup"><span data-stu-id="a3fdd-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Vorab aufgefüllte NuGet-Paket-Manager-Dialogfeld](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="a3fdd-113">Geben Sie ganze Ordner für den Inhalt des Pakets</span><span class="sxs-lookup"><span data-stu-id="a3fdd-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="a3fdd-114">NuGet 2.2 können Sie an einen ganzen Ordner in nun der `<file>` Element der `.nuspec` hinzu, um den Inhalt dieses Ordners einzubeziehen.</span><span class="sxs-lookup"><span data-stu-id="a3fdd-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="a3fdd-115">Beispielsweise wird Folgendes dazu führen, dass alle Skripts im Ordner "Scripts" des Pakets, zu dem Ordner Contents\scripts hinzugefügt werden, wenn das Paket in einem Projekt installiert wird.</span><span class="sxs-lookup"><span data-stu-id="a3fdd-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="a3fdd-116">**Aktualisieren Sie 6/24/16: leere Ordner im Ordner "Content" werden ignoriert, wenn es sich bei der Installation des Pakets.**</span><span class="sxs-lookup"><span data-stu-id="a3fdd-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="a3fdd-117">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="a3fdd-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="a3fdd-118">Paketinstallation für f#-Projekte schlägt fehl, wenn Sie die Paket-Manager-Konsole verwenden</span><span class="sxs-lookup"><span data-stu-id="a3fdd-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="a3fdd-119">Beim Versuch, ein NuGet-Paket in ein F#-Projekt mithilfe der Paket-Manager-Konsole zu installieren, wird eine "InvalidOperationException" ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="a3fdd-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="a3fdd-120">Wir arbeiten aktiv mit dem F#-Team das Problem zu beheben, aber in der Zwischenzeit die problemumgehung besteht darin, NuGet-Pakete in F#-Projekten über das Dialogfeld "NuGet Paket-Manager" statt der Konsole zu installieren.</span><span class="sxs-lookup"><span data-stu-id="a3fdd-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="a3fdd-121">[Weitere Informationen finden Sie auf CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="a3fdd-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="a3fdd-122">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="a3fdd-122">Bug Fixes</span></span>
<span data-ttu-id="a3fdd-123">NuGet 2.2 enthält zahlreiche Programmfehlerbehebungen.</span><span class="sxs-lookup"><span data-stu-id="a3fdd-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="a3fdd-124">Eine vollständige Liste der Arbeit Elemente eine feste in NuGet 2.2, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="a3fdd-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
