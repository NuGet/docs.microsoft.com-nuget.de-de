---
title: Anmerkungen zu dieser Version von nuget 1,7
description: Anmerkungen zu dieser Version von nuget 1,7 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a98da76038582202396c8da96f8eae166e6096f6
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383318"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="af146-103">Anmerkungen zu dieser Version von nuget 1,7</span><span class="sxs-lookup"><span data-stu-id="af146-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="af146-104">Anmerkungen zu [nuget 1,6](../release-notes/nuget-1.6.md) | Anmerkungen zur [nuget](../release-notes/nuget-1.8.md) -Version 1,8</span><span class="sxs-lookup"><span data-stu-id="af146-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="af146-105">Nuget 1,7 wurde am 4. April 2012 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="af146-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="af146-106">Bekanntes Installationsproblem</span><span class="sxs-lookup"><span data-stu-id="af146-106">Known Installation Issue</span></span>
<span data-ttu-id="af146-107">Wenn Sie Visual Studio 2010 SP1 ausführen, tritt möglicherweise ein Installationsfehler auf, wenn Sie versuchen, ein Upgrade für nuget auszuführen, wenn Sie eine ältere Version installiert haben.</span><span class="sxs-lookup"><span data-stu-id="af146-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="af146-108">Die Problem Umgehung besteht darin, dass Sie nuget einfach deinstallieren und anschließend aus dem vs-Erweiterungs Katalog installieren.</span><span class="sxs-lookup"><span data-stu-id="af146-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="af146-109">Weitere Informationen finden Sie unter <https://support.microsoft.com/kb/2581019>.</span><span class="sxs-lookup"><span data-stu-id="af146-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="af146-110">Hinweis: Wenn Visual Studio die Deinstallation der Erweiterung nicht zulässt (die Schaltfläche "deinstallieren" ist deaktiviert), müssen Sie Visual Studio wahrscheinlich mit "als Administrator ausführen" neu starten.</span><span class="sxs-lookup"><span data-stu-id="af146-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="af146-111">Features</span><span class="sxs-lookup"><span data-stu-id="af146-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="af146-112">Das Öffnen der Datei "Infodatei. txt" nach der Installation</span><span class="sxs-lookup"><span data-stu-id="af146-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="af146-113">Neu in 1,7, wenn Ihr Paket eine `readme.txt`-Datei im Stamm des Pakets enthält, wird diese Datei von nuget automatisch geöffnet, nachdem die Installation des Pakets abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="af146-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="af146-114">Vorab Versionen von Paketen im Dialogfeld "nuget-Pakete verwalten" anzeigen</span><span class="sxs-lookup"><span data-stu-id="af146-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="af146-115">Das Dialogfeld nuget-Pakete verwalten enthält jetzt eine Dropdown Liste, die die Option zum Anzeigen von vorab Paketen bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="af146-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Vorabversions Pakete werden angezeigt.](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="af146-117">Schaltfläche "Paket Wiederherstellung" anzeigen, wenn Paketdateien fehlen</span><span class="sxs-lookup"><span data-stu-id="af146-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="af146-118">Wenn Sie die Paket-Manager-Konsole oder das Manager-Dialogfeld "nuget-Pakete" öffnen, überprüft nuget, ob die aktuelle Lösung den Paket Wiederherstellungs Modus aktiviert hat und ob Paketdateien im Ordner "`packages`" fehlen.</span><span class="sxs-lookup"><span data-stu-id="af146-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="af146-119">Wenn diese beiden Bedingungen erfüllt sind, werden Sie von nuget benachrichtigt, und es wird eine bequeme Schaltfläche Wiederherstellen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="af146-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="af146-120">Wenn Sie auf diese Schaltfläche klicken, wird nuget zum Wiederherstellen aller fehlenden Pakete hinzu kommen.</span><span class="sxs-lookup"><span data-stu-id="af146-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Schaltfläche Paket Wiederherstellung im Dialogfeld](./media/packagerestore-dialog.png)

![Schaltfläche Paket Wiederherstellung in der Konsole](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="af146-123">Projektmappendatei "Packages. config" hinzufügen</span><span class="sxs-lookup"><span data-stu-id="af146-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="af146-124">In früheren Versionen von nuget verfügt jedes Projekt über eine `packages.config`-Datei, die nachverfolgt, welche nuget-Pakete in diesem Projekt installiert werden.</span><span class="sxs-lookup"><span data-stu-id="af146-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="af146-125">Es gab jedoch keine ähnliche Datei auf Lösungsebene, um Pakete auf Projektmappenebene nachzuverfolgen.</span><span class="sxs-lookup"><span data-stu-id="af146-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="af146-126">Folglich gab es keine Möglichkeit, Pakete auf Projektmappenebene wiederherzustellen.</span><span class="sxs-lookup"><span data-stu-id="af146-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="af146-127">Diese Funktion ist jetzt in nuget 1,7 implementiert.</span><span class="sxs-lookup"><span data-stu-id="af146-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="af146-128">Die `packages.config` Datei auf Projektmappenebene wird unter dem Ordner "`.nuget`" unter dem Projektmappenstamm abgelegt und speichert nur Pakete auf Projektmappenebene.</span><span class="sxs-lookup"><span data-stu-id="af146-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="af146-129">Befehl "New-Package" entfernen</span><span class="sxs-lookup"><span data-stu-id="af146-129">Remove New-Package command</span></span>
<span data-ttu-id="af146-130">Aufgrund der geringen Auslastung wurde der New-Package-Befehl entfernt.</span><span class="sxs-lookup"><span data-stu-id="af146-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="af146-131">Entwickler sollten nuget. exe oder den praktischen nuget-Paket-Explorer verwenden, um Pakete zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="af146-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="af146-132">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="af146-132">Bug Fixes</span></span>
<span data-ttu-id="af146-133">Nuget 1,7 hat viele Fehler im Zusammenhang mit dem Paket Wiederherstellungs Workflow und den Netzwerk-/Quellcodeverwaltungs-Szenarien behoben.</span><span class="sxs-lookup"><span data-stu-id="af146-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="af146-134">Eine vollständige Liste der Arbeitselemente, die in nuget 1,7 behoben wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="af146-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
