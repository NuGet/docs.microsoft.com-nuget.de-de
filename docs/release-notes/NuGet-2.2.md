---
title: Anmerkungen zu dieser Version von nuget 2,2
description: Anmerkungen zu dieser Version von nuget 2,2 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780432"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="d66ed-103">Anmerkungen zu dieser Version von nuget 2,2</span><span class="sxs-lookup"><span data-stu-id="d66ed-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="d66ed-104">Anmerkungen zu dieser [Version von nuget 2,1](../release-notes/nuget-2.1.md)  |  [Anmerkungen zu dieser Version von nuget 2.2.1](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="d66ed-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="d66ed-105">Nuget 2,2 wurde am 12. Dezember 2012 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="d66ed-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="d66ed-106">Visual Studio-Schnellstart</span><span class="sxs-lookup"><span data-stu-id="d66ed-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="d66ed-107">Eine der neuen Features, die in Visual Studio 2012 hinzugefügt wurde, war das [Dialogfeld Schnellstart](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="d66ed-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="d66ed-108">Nuget 2,2 erweitert dieses Dialogfeld und ermöglicht es, das Dialogfeld "Paket-Manager" mit den Suchbegriffen zu initialisieren, die im Schnellstart eingegeben wurden.</span><span class="sxs-lookup"><span data-stu-id="d66ed-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="d66ed-109">Beispielsweise enthält die Eingabe von "jQuery" in "Schnellstart" nun eine Option in den Ergebnissen, um nuget-Pakete zu suchen, die mit "jQuery" übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="d66ed-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![Nuget in Visual Studio-Schnellstart](./media/quick-launch.png)

<span data-ttu-id="d66ed-111">Wenn Sie diese Option auswählen, wird die Standardsuche für nuget-Paket-Manager für den Begriff "jQuery" gestartet.</span><span class="sxs-lookup"><span data-stu-id="d66ed-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Dialog Feld "nuget-Paket-Manager" vorab aufgefüllt](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="d66ed-113">Gesamten Ordner für Paket Inhalt angeben</span><span class="sxs-lookup"><span data-stu-id="d66ed-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="d66ed-114">Mit nuget 2,2 können Sie nun einen gesamten Ordner im- `<file>` Element der Datei angeben `.nuspec` , um den gesamten Inhalt dieses Ordners einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="d66ed-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="d66ed-115">Beispielsweise werden durch Folgendes bewirkt, dass alle Skripts im Ordner "Scripts" des Pakets dem Ordner "contents\scripts" hinzugefügt werden, wenn das Paket in einem Projekt installiert wird.</span><span class="sxs-lookup"><span data-stu-id="d66ed-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="d66ed-116">**Update 6/24/16: leere Ordner im Ordner "Content" werden ignoriert, wenn das Paket installiert wird.**</span><span class="sxs-lookup"><span data-stu-id="d66ed-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="d66ed-117">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="d66ed-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="d66ed-118">Fehler bei der Paketinstallation für F #-Projekte bei Verwendung der Paket-Manager-Konsole</span><span class="sxs-lookup"><span data-stu-id="d66ed-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="d66ed-119">Wenn Sie versuchen, ein nuget-Paket in einem F #-Projekt mithilfe der Paket-Manager-Konsole zu installieren, wird eine InvalidOperationException ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="d66ed-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="d66ed-120">Wir arbeiten aktiv mit dem F #-Team zusammen, um das Problem zu beheben, aber in der Zwischenzeit besteht die Problem Umgehung darin, nuget-Pakete in F #-Projekten über das Paket-Manager-Dialogfeld von nuget anstelle der Konsole zu installieren.</span><span class="sxs-lookup"><span data-stu-id="d66ed-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="d66ed-121">[Weitere Informationen finden Sie auf CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="d66ed-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="d66ed-122">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="d66ed-122">Bug Fixes</span></span>
<span data-ttu-id="d66ed-123">Nuget 2,2 umfasst viele Fehlerbehebungen.</span><span class="sxs-lookup"><span data-stu-id="d66ed-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="d66ed-124">Eine vollständige Liste der Arbeitselemente, die in nuget 2,2 behoben wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="d66ed-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
