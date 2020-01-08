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
# <a name="nuget-17-release-notes"></a>Anmerkungen zu dieser Version von nuget 1,7

Anmerkungen zu [nuget 1,6](../release-notes/nuget-1.6.md) | Anmerkungen zur [nuget](../release-notes/nuget-1.8.md) -Version 1,8

Nuget 1,7 wurde am 4. April 2012 veröffentlicht.

## <a name="known-installation-issue"></a>Bekanntes Installationsproblem
Wenn Sie Visual Studio 2010 SP1 ausführen, tritt möglicherweise ein Installationsfehler auf, wenn Sie versuchen, ein Upgrade für nuget auszuführen, wenn Sie eine ältere Version installiert haben.

Die Problem Umgehung besteht darin, dass Sie nuget einfach deinstallieren und anschließend aus dem vs-Erweiterungs Katalog installieren.  Weitere Informationen finden Sie unter <https://support.microsoft.com/kb/2581019>.

Hinweis: Wenn Visual Studio die Deinstallation der Erweiterung nicht zulässt (die Schaltfläche "deinstallieren" ist deaktiviert), müssen Sie Visual Studio wahrscheinlich mit "als Administrator ausführen" neu starten.

## <a name="features"></a>Features

### <a name="support-opening-readmetxt-file-after-installation"></a>Das Öffnen der Datei "Infodatei. txt" nach der Installation
Neu in 1,7, wenn Ihr Paket eine `readme.txt`-Datei im Stamm des Pakets enthält, wird diese Datei von nuget automatisch geöffnet, nachdem die Installation des Pakets abgeschlossen ist.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Vorab Versionen von Paketen im Dialogfeld "nuget-Pakete verwalten" anzeigen
Das Dialogfeld nuget-Pakete verwalten enthält jetzt eine Dropdown Liste, die die Option zum Anzeigen von vorab Paketen bereitstellt.

![Vorabversions Pakete werden angezeigt.](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Schaltfläche "Paket Wiederherstellung" anzeigen, wenn Paketdateien fehlen
Wenn Sie die Paket-Manager-Konsole oder das Manager-Dialogfeld "nuget-Pakete" öffnen, überprüft nuget, ob die aktuelle Lösung den Paket Wiederherstellungs Modus aktiviert hat und ob Paketdateien im Ordner "`packages`" fehlen. Wenn diese beiden Bedingungen erfüllt sind, werden Sie von nuget benachrichtigt, und es wird eine bequeme Schaltfläche Wiederherstellen angezeigt. Wenn Sie auf diese Schaltfläche klicken, wird nuget zum Wiederherstellen aller fehlenden Pakete hinzu kommen.

![Schaltfläche Paket Wiederherstellung im Dialogfeld](./media/packagerestore-dialog.png)

![Schaltfläche Paket Wiederherstellung in der Konsole](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Projektmappendatei "Packages. config" hinzufügen
In früheren Versionen von nuget verfügt jedes Projekt über eine `packages.config`-Datei, die nachverfolgt, welche nuget-Pakete in diesem Projekt installiert werden. Es gab jedoch keine ähnliche Datei auf Lösungsebene, um Pakete auf Projektmappenebene nachzuverfolgen. Folglich gab es keine Möglichkeit, Pakete auf Projektmappenebene wiederherzustellen.
Diese Funktion ist jetzt in nuget 1,7 implementiert. Die `packages.config` Datei auf Projektmappenebene wird unter dem Ordner "`.nuget`" unter dem Projektmappenstamm abgelegt und speichert nur Pakete auf Projektmappenebene.

### <a name="remove-new-package-command"></a>Befehl "New-Package" entfernen
Aufgrund der geringen Auslastung wurde der New-Package-Befehl entfernt. Entwickler sollten nuget. exe oder den praktischen nuget-Paket-Explorer verwenden, um Pakete zu erstellen.

## <a name="bug-fixes"></a>Fehlerkorrekturen
Nuget 1,7 hat viele Fehler im Zusammenhang mit dem Paket Wiederherstellungs Workflow und den Netzwerk-/Quellcodeverwaltungs-Szenarien behoben.

Eine vollständige Liste der Arbeitselemente, die in nuget 1,7 behoben wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
