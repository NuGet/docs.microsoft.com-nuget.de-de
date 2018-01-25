---
title: Anmerkungen zur Version des NuGet-1.7 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 1.7 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-1.7 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7b16bea8c6bcc77f814dd32a43b895b5e656c95d
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-17-release-notes"></a>1.7 NuGet-Versionshinweise

[Anmerkungen zur Version des NuGet-1.6](../release-notes/nuget-1.6.md) | [NuGet 1.8-Versionshinweise](../release-notes/nuget-1.8.md)

NuGet-1.7 wurde am 4. April 2012 veröffentlicht.

## <a name="known-installation-issue"></a>Bekannte Problem
Wenn Sie Visual Studio 2010 SP1 ausführen, kann ein Installationsfehler auftreten beim Upgrade von NuGet ausführen, wenn Sie eine ältere Version installiert haben.

Die problemumgehung besteht darin, einfach NuGet deinstallieren und installieren Sie es aus dem Katalog der VS-Erweiterung.  Weitere Informationen finden Sie unter [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

Hinweis: Wenn Visual Studio lässt Sie beim Deinstallieren der Erweiterung (die Schaltfläche "Deinstallieren" deaktiviert ist), müssen Sie wahrscheinlich zum Neustart von Visual Studio, die mit "Als Administrator ausführen".

## <a name="features"></a>Features

### <a name="support-opening-readmetxt-file-after-installation"></a>Öffnen von Datei "Readme.txt" nach der Installation des unterstützt
Neues in 1.7, wenn das Paket enthält eine `readme.txt` Datei im Stammverzeichnis des Pakets, NuGet wird diese Datei automatisch geöffnet, nach dem Installieren des Pakets abgeschlossen wurde.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Anzeigen von Vorabversionen von Paketen in das Dialogfeld "Verwalten von NuGet-Pakete"
Das Dialogfeld "NuGet-Pakete verwalten" enthält nun eine Dropdown-Liste die Option zum Anzeigen von Vorabversionen von Paketen bereitstellt.

![Anzeigen von Vorabversionen von Paketen](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Zeigen Sie Schaltfläche Paketwiederherstellung an, wenn Paketdateien fehlen
Wenn Sie die Paket-Manager-Konsole öffnen oder die Manager-NuGet-Pakete Dialogfeld, NuGet wird überprüft, ob die aktuelle Projektmappe Package Restore-Modus aktiviert wurde und alle Paketdateien fehlen die `packages` Ordner. Wenn beide Bedingungen erfüllt sind, wird von NuGet Sie werden benachrichtigt, und zeigt eine einfache Wiederherstellungsschaltfläche. Klicken auf diese Schaltfläche löst NuGet, um die fehlende Pakete wiederherzustellen.

![Schaltfläche zum Wiederherstellen von Paket im Dialogfeld "](./media/packagerestore-dialog.png)

![Schaltfläche zum Wiederherstellen von Paket auf der Konsole](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Hinzufügen von Projektmappen auf Dokumentebene "Packages.config"-Datei
In früheren Versionen von NuGet jedes Projekt verfügt über eine `packages.config` Datei der protokolliert wird, welche NuGet-Pakete in diesem Projekt installiert sind. Es wurde jedoch keine ähnlichen Datei auf Projektmappenebene Projektmappenebene Pakete des. Daher gab es keine Möglichkeit zum Wiederherstellen von Paketen für Projektmappen auf Dokumentebene.
Dieses Feature wird jetzt in NuGet 1.7 implementiert. Der Projektmappenebene `packages.config` Datei befindet sich unter dem `.nuget` Unterordner Lösung root und speichert nur Projektmappenebene Pakete.

### <a name="remove-new-package-command"></a>Entfernen Sie New-Paket-Befehl
Das neue Paket-Befehl wurde aufgrund mit geringer Nutzung entfernt. Entwickler recommended nuget.exe oder praktisch NuGet-Paket-Explorer verwenden, um Pakete zu erstellen.

## <a name="bug-fixes"></a>Fehlerkorrekturen
NuGet-1.7 verfügt über viele Paketwiederherstellung Workflow und Netzwerkquelle/Steuerelementszenarien behoben.

Eine vollständige Liste der Arbeit Elemente in behoben NuGet 1.7, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
