---
title: Anmerkungen zur Version des NuGet-1.7 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: df7becc6-993d-4d06-8495-a0c26748bdfa
description: "Versionshinweise für NuGet 1.7 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-1.7 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 420b40576cb3862f0e4406966f9ccca9fd1f39a1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="5a0dc-104">1.7 NuGet-Versionshinweise</span><span class="sxs-lookup"><span data-stu-id="5a0dc-104">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="5a0dc-105">[Anmerkungen zur Version des NuGet-1.6](../release-notes/nuget-1.6.md) | [NuGet 1.8-Versionshinweise](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="5a0dc-105">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="5a0dc-106">NuGet-1.7 wurde am 4. April 2012 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="5a0dc-106">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="5a0dc-107">Bekannte Problem</span><span class="sxs-lookup"><span data-stu-id="5a0dc-107">Known Installation Issue</span></span>
<span data-ttu-id="5a0dc-108">Wenn Sie Visual Studio 2010 SP1 ausführen, kann ein Installationsfehler auftreten beim Upgrade von NuGet ausführen, wenn Sie eine ältere Version installiert haben.</span><span class="sxs-lookup"><span data-stu-id="5a0dc-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="5a0dc-109">Die problemumgehung besteht darin, einfach NuGet deinstallieren und installieren Sie es aus dem Katalog der VS-Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="5a0dc-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="5a0dc-110">Finden Sie unter [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) für Weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="5a0dc-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="5a0dc-111">Hinweis: Wenn Visual Studio lässt Sie beim Deinstallieren der Erweiterung (die Schaltfläche "Deinstallieren" deaktiviert ist), müssen Sie wahrscheinlich zum Neustart von Visual Studio, die mit "Als Administrator ausführen".</span><span class="sxs-lookup"><span data-stu-id="5a0dc-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="5a0dc-112">Features</span><span class="sxs-lookup"><span data-stu-id="5a0dc-112">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="5a0dc-113">Öffnen von Datei "Readme.txt" nach der Installation des unterstützt</span><span class="sxs-lookup"><span data-stu-id="5a0dc-113">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="5a0dc-114">Neues in 1.7, wenn das Paket enthält eine `readme.txt` Datei im Stammverzeichnis des Pakets, NuGet wird diese Datei automatisch geöffnet, nach dem Installieren des Pakets abgeschlossen wurde.</span><span class="sxs-lookup"><span data-stu-id="5a0dc-114">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="5a0dc-115">Anzeigen von Vorabversionen von Paketen in das Dialogfeld "Verwalten von NuGet-Pakete"</span><span class="sxs-lookup"><span data-stu-id="5a0dc-115">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="5a0dc-116">Das Dialogfeld "NuGet-Pakete verwalten" enthält nun eine Dropdown-Liste die Option zum Anzeigen von Vorabversionen von Paketen bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="5a0dc-116">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Anzeigen von Vorabversionen von Paketen](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="5a0dc-118">Zeigen Sie Schaltfläche Paketwiederherstellung an, wenn Paketdateien fehlen</span><span class="sxs-lookup"><span data-stu-id="5a0dc-118">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="5a0dc-119">Wenn Sie die Paket-Manager-Konsole öffnen oder die Manager-NuGet-Pakete Dialogfeld, NuGet wird überprüft, ob die aktuelle Projektmappe Package Restore-Modus aktiviert wurde und alle Paketdateien fehlen die `packages` Ordner.</span><span class="sxs-lookup"><span data-stu-id="5a0dc-119">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="5a0dc-120">Wenn beide Bedingungen erfüllt sind, wird von NuGet Sie werden benachrichtigt, und zeigt eine einfache Wiederherstellungsschaltfläche.</span><span class="sxs-lookup"><span data-stu-id="5a0dc-120">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="5a0dc-121">Klicken auf diese Schaltfläche löst NuGet, um die fehlende Pakete wiederherzustellen.</span><span class="sxs-lookup"><span data-stu-id="5a0dc-121">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Schaltfläche zum Wiederherstellen von Paket im Dialogfeld "](./media/packagerestore-dialog.png)

![Schaltfläche zum Wiederherstellen von Paket auf der Konsole](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="5a0dc-124">Hinzufügen von Projektmappen auf Dokumentebene "Packages.config"-Datei</span><span class="sxs-lookup"><span data-stu-id="5a0dc-124">Add solution-level packages.config file</span></span>
<span data-ttu-id="5a0dc-125">In früheren Versionen von NuGet jedes Projekt verfügt über eine `packages.config` Datei der protokolliert wird, welche NuGet-Pakete in diesem Projekt installiert sind.</span><span class="sxs-lookup"><span data-stu-id="5a0dc-125">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="5a0dc-126">Es wurde jedoch keine ähnlichen Datei auf Projektmappenebene Projektmappenebene Pakete des.</span><span class="sxs-lookup"><span data-stu-id="5a0dc-126">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="5a0dc-127">Daher gab es keine Möglichkeit zum Wiederherstellen von Paketen für Projektmappen auf Dokumentebene.</span><span class="sxs-lookup"><span data-stu-id="5a0dc-127">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="5a0dc-128">Dieses Feature wird jetzt in NuGet 1.7 implementiert.</span><span class="sxs-lookup"><span data-stu-id="5a0dc-128">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="5a0dc-129">Der Projektmappenebene `packages.config` Datei befindet sich unter dem `.nuget` Unterordner Lösung root und speichert nur Projektmappenebene Pakete.</span><span class="sxs-lookup"><span data-stu-id="5a0dc-129">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="5a0dc-130">Entfernen Sie New-Paket-Befehl</span><span class="sxs-lookup"><span data-stu-id="5a0dc-130">Remove New-Package command</span></span>
<span data-ttu-id="5a0dc-131">Das neue Paket-Befehl wurde aufgrund mit geringer Nutzung entfernt.</span><span class="sxs-lookup"><span data-stu-id="5a0dc-131">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="5a0dc-132">Entwickler recommended nuget.exe oder praktisch NuGet-Paket-Explorer verwenden, um Pakete zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="5a0dc-132">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="5a0dc-133">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="5a0dc-133">Bug Fixes</span></span>
<span data-ttu-id="5a0dc-134">NuGet-1.7 verfügt über viele Paketwiederherstellung Workflow und Netzwerkquelle/Steuerelementszenarien behoben.</span><span class="sxs-lookup"><span data-stu-id="5a0dc-134">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="5a0dc-135">Eine vollständige Liste der Arbeit Elemente in behoben NuGet 1.7, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="5a0dc-135">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
