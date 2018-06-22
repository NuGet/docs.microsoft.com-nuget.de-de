---
title: 1.7 NuGet-Versionshinweise
description: Versionshinweise für NuGet 1.7 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 81db81642ac21b7dd41f5940dfba919d0871ec01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820926"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="ae1bb-103">1.7 NuGet-Versionshinweise</span><span class="sxs-lookup"><span data-stu-id="ae1bb-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="ae1bb-104">[Anmerkungen zur Version des NuGet-1.6](../release-notes/nuget-1.6.md) | [NuGet 1.8-Versionshinweise](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="ae1bb-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="ae1bb-105">NuGet-1.7 wurde am 4. April 2012 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="ae1bb-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="ae1bb-106">Bekannte Problem</span><span class="sxs-lookup"><span data-stu-id="ae1bb-106">Known Installation Issue</span></span>
<span data-ttu-id="ae1bb-107">Wenn Sie Visual Studio 2010 SP1 ausführen, kann ein Installationsfehler auftreten beim Upgrade von NuGet ausführen, wenn Sie eine ältere Version installiert haben.</span><span class="sxs-lookup"><span data-stu-id="ae1bb-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="ae1bb-108">Die problemumgehung besteht darin, einfach NuGet deinstallieren und installieren Sie es aus dem Katalog der VS-Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="ae1bb-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="ae1bb-109">Weitere Informationen finden Sie unter [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).</span><span class="sxs-lookup"><span data-stu-id="ae1bb-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="ae1bb-110">Hinweis: Wenn Visual Studio lässt Sie beim Deinstallieren der Erweiterung (die Schaltfläche "Deinstallieren" deaktiviert ist), müssen Sie wahrscheinlich zum Neustart von Visual Studio, die mit "Als Administrator ausführen".</span><span class="sxs-lookup"><span data-stu-id="ae1bb-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="ae1bb-111">Features</span><span class="sxs-lookup"><span data-stu-id="ae1bb-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="ae1bb-112">Öffnen von Datei "Readme.txt" nach der Installation des unterstützt</span><span class="sxs-lookup"><span data-stu-id="ae1bb-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="ae1bb-113">Neues in 1.7, wenn das Paket enthält eine `readme.txt` Datei im Stammverzeichnis des Pakets, NuGet wird diese Datei automatisch geöffnet, nach dem Installieren des Pakets abgeschlossen wurde.</span><span class="sxs-lookup"><span data-stu-id="ae1bb-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="ae1bb-114">Anzeigen von Vorabversionen von Paketen in das Dialogfeld "Verwalten von NuGet-Pakete"</span><span class="sxs-lookup"><span data-stu-id="ae1bb-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="ae1bb-115">Das Dialogfeld "NuGet-Pakete verwalten" enthält nun eine Dropdown-Liste die Option zum Anzeigen von Vorabversionen von Paketen bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="ae1bb-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Anzeigen von Vorabversionen von Paketen](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="ae1bb-117">Zeigen Sie Schaltfläche Paketwiederherstellung an, wenn Paketdateien fehlen</span><span class="sxs-lookup"><span data-stu-id="ae1bb-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="ae1bb-118">Wenn Sie die Paket-Manager-Konsole öffnen oder die Manager-NuGet-Pakete Dialogfeld, NuGet wird überprüft, ob die aktuelle Projektmappe Package Restore-Modus aktiviert wurde und alle Paketdateien fehlen die `packages` Ordner.</span><span class="sxs-lookup"><span data-stu-id="ae1bb-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="ae1bb-119">Wenn beide Bedingungen erfüllt sind, wird von NuGet Sie werden benachrichtigt, und zeigt eine einfache Wiederherstellungsschaltfläche.</span><span class="sxs-lookup"><span data-stu-id="ae1bb-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="ae1bb-120">Klicken auf diese Schaltfläche löst NuGet, um die fehlende Pakete wiederherzustellen.</span><span class="sxs-lookup"><span data-stu-id="ae1bb-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Schaltfläche zum Wiederherstellen von Paket im Dialogfeld "](./media/packagerestore-dialog.png)

![Schaltfläche zum Wiederherstellen von Paket auf der Konsole](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="ae1bb-123">Hinzufügen von Projektmappen auf Dokumentebene "Packages.config"-Datei</span><span class="sxs-lookup"><span data-stu-id="ae1bb-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="ae1bb-124">In früheren Versionen von NuGet jedes Projekt verfügt über eine `packages.config` Datei der protokolliert wird, welche NuGet-Pakete in diesem Projekt installiert sind.</span><span class="sxs-lookup"><span data-stu-id="ae1bb-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="ae1bb-125">Es wurde jedoch keine ähnlichen Datei auf Projektmappenebene Projektmappenebene Pakete des.</span><span class="sxs-lookup"><span data-stu-id="ae1bb-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="ae1bb-126">Daher gab es keine Möglichkeit zum Wiederherstellen von Paketen für Projektmappen auf Dokumentebene.</span><span class="sxs-lookup"><span data-stu-id="ae1bb-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="ae1bb-127">Dieses Feature wird jetzt in NuGet 1.7 implementiert.</span><span class="sxs-lookup"><span data-stu-id="ae1bb-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="ae1bb-128">Der Projektmappenebene `packages.config` Datei befindet sich unter dem `.nuget` Unterordner Lösung root und speichert nur Projektmappenebene Pakete.</span><span class="sxs-lookup"><span data-stu-id="ae1bb-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="ae1bb-129">Entfernen Sie New-Paket-Befehl</span><span class="sxs-lookup"><span data-stu-id="ae1bb-129">Remove New-Package command</span></span>
<span data-ttu-id="ae1bb-130">Das neue Paket-Befehl wurde aufgrund mit geringer Nutzung entfernt.</span><span class="sxs-lookup"><span data-stu-id="ae1bb-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="ae1bb-131">Entwickler recommended nuget.exe oder praktisch NuGet-Paket-Explorer verwenden, um Pakete zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="ae1bb-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="ae1bb-132">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="ae1bb-132">Bug Fixes</span></span>
<span data-ttu-id="ae1bb-133">NuGet-1.7 verfügt über viele Paketwiederherstellung Workflow und Netzwerkquelle/Steuerelementszenarien behoben.</span><span class="sxs-lookup"><span data-stu-id="ae1bb-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="ae1bb-134">Eine vollständige Liste der Arbeit Elemente in behoben NuGet 1.7, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="ae1bb-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
