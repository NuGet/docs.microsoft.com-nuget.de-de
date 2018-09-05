---
title: Anmerkungen zu NuGet-Version 1.7
description: Anmerkungen zu NuGet 1.7, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 07cd541ef215d2a1bacc45995a22dadb6dfeac6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551466"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="14b8a-103">Anmerkungen zu NuGet-Version 1.7</span><span class="sxs-lookup"><span data-stu-id="14b8a-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="14b8a-104">[Anmerkungen zu NuGet 1.6](../release-notes/nuget-1.6.md) | [Anmerkungen zu NuGet 1.8](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="14b8a-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="14b8a-105">NuGet 1.7 wurde am 4. April 2012 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="14b8a-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="14b8a-106">Problem für bekannte Installationsprobleme</span><span class="sxs-lookup"><span data-stu-id="14b8a-106">Known Installation Issue</span></span>
<span data-ttu-id="14b8a-107">Wenn Sie Visual Studio 2010 SP1 ausführen, können Sie ein Installationsfehler auftreten, beim Versuch, NuGet aktualisieren, wenn Sie eine ältere Version installiert haben.</span><span class="sxs-lookup"><span data-stu-id="14b8a-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="14b8a-108">Die problemumgehung besteht darin, einfach NuGet zuerst deinstallieren und installieren Sie es aus dem Katalog der VS-Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="14b8a-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="14b8a-109">Weitere Informationen finden Sie unter [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).</span><span class="sxs-lookup"><span data-stu-id="14b8a-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="14b8a-110">Hinweis: Wenn Visual Studio ist es nicht zulässig, die die Erweiterung deinstallieren (die Schaltfläche "Deinstallieren" deaktiviert ist), müssen Sie wahrscheinlich zum Neustart von Visual Studio mithilfe von "Ausführen als Administrator."</span><span class="sxs-lookup"><span data-stu-id="14b8a-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="14b8a-111">Features</span><span class="sxs-lookup"><span data-stu-id="14b8a-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="14b8a-112">Unterstützung für das Öffnen von Datei "Readme.txt" nach der installation</span><span class="sxs-lookup"><span data-stu-id="14b8a-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="14b8a-113">Neues in 1.7, wenn das Paket enthält eine `readme.txt` Datei im Stammverzeichnis des NuGet-Pakets wird diese Datei automatisch geöffnet, nach dem Installieren des Pakets abgeschlossen wurde.</span><span class="sxs-lookup"><span data-stu-id="14b8a-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="14b8a-114">Anzeigen von Vorabversionen von Paketen im Dialogfeld "Verwalten von NuGet-Pakete"</span><span class="sxs-lookup"><span data-stu-id="14b8a-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="14b8a-115">Das Dialogfeld "NuGet-Pakete verwalten" enthält jetzt eine Dropdownliste die Option zum Anzeigen von Vorabversionen von Paketen bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="14b8a-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Anzeigen von Vorabversionen von Paketen](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="14b8a-117">Schaltfläche "Paketwiederherstellung" angezeigt, wenn Paketdateien fehlen</span><span class="sxs-lookup"><span data-stu-id="14b8a-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="14b8a-118">Wenn Sie die Paket-Manager-Konsole öffnen oder das Dialogfeld für die Manager-NuGet-Pakete, NuGet überprüft, ob die aktuelle Projektmappe den Paketwiederherstellung-Modus aktiviert ist und alle Paketdateien fehlen die `packages` Ordner.</span><span class="sxs-lookup"><span data-stu-id="14b8a-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="14b8a-119">Wenn beide Bedingungen erfüllt sind, wird NuGet Sie werden benachrichtigt, und zeigt eine einfache Schaltfläche "Wiederherstellen".</span><span class="sxs-lookup"><span data-stu-id="14b8a-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="14b8a-120">Auf diese Schaltfläche klicken, löst NuGet aus, um alle fehlenden Pakete wiederherstellen.</span><span class="sxs-lookup"><span data-stu-id="14b8a-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Paket Schaltfläche "Wiederherstellen" im Dialogfeld "](./media/packagerestore-dialog.png)

![Paket Schaltfläche "Wiederherstellen" in-Konsole](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="14b8a-123">Hinzufügen der Datei auf Projektmappenebene "Packages.config"</span><span class="sxs-lookup"><span data-stu-id="14b8a-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="14b8a-124">In früheren Versionen von NuGet, jedes Projekt verfügt über eine `packages.config` Datei der protokolliert wird, welche NuGet-Pakete in diesem Projekt installiert werden.</span><span class="sxs-lookup"><span data-stu-id="14b8a-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="14b8a-125">Allerdings gab es keine ähnliche Datei auf Projektmappenebene zu verfolgen-Pakete auf Projektmappenebene.</span><span class="sxs-lookup"><span data-stu-id="14b8a-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="14b8a-126">Daher gab es keine Möglichkeit, die auf lösungsebene Pakete wiederhergestellt werden.</span><span class="sxs-lookup"><span data-stu-id="14b8a-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="14b8a-127">Diese Funktion ist jetzt in NuGet 1.7 implementiert.</span><span class="sxs-lookup"><span data-stu-id="14b8a-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="14b8a-128">Auf der lösungsebene `packages.config` Datei befindet sich unter der `.nuget` Unterordner der Projektmappe root an, und wird nur auf Projektmappenebene-Pakete speichern.</span><span class="sxs-lookup"><span data-stu-id="14b8a-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="14b8a-129">Befehl "New-Package" entfernen</span><span class="sxs-lookup"><span data-stu-id="14b8a-129">Remove New-Package command</span></span>
<span data-ttu-id="14b8a-130">Der New-paketbefehl wurde aufgrund von mit geringer Auslastung entfernt.</span><span class="sxs-lookup"><span data-stu-id="14b8a-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="14b8a-131">Entwicklern werden empfohlen, um nuget.exe oder den praktischen NuGet-Paket-Explorer verwenden, um Pakete zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="14b8a-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="14b8a-132">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="14b8a-132">Bug Fixes</span></span>
<span data-ttu-id="14b8a-133">NuGet 1.7 wurde behoben, dass viele Fehler bei der Paketwiederherstellung Workflow und die Szenarien für Netzwerk/Source-Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="14b8a-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="14b8a-134">Eine vollständige Liste der Arbeit Elemente eine feste in NuGet 1.7. Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="14b8a-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
