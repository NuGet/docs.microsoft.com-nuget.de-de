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
# <a name="nuget-17-release-notes"></a>Anmerkungen zu NuGet-Version 1.7

[Anmerkungen zu NuGet 1.6](../release-notes/nuget-1.6.md) | [Anmerkungen zu NuGet 1.8](../release-notes/nuget-1.8.md)

NuGet 1.7 wurde am 4. April 2012 veröffentlicht.

## <a name="known-installation-issue"></a>Problem für bekannte Installationsprobleme
Wenn Sie Visual Studio 2010 SP1 ausführen, können Sie ein Installationsfehler auftreten, beim Versuch, NuGet aktualisieren, wenn Sie eine ältere Version installiert haben.

Die problemumgehung besteht darin, einfach NuGet zuerst deinstallieren und installieren Sie es aus dem Katalog der VS-Erweiterung.  Weitere Informationen finden Sie unter [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

Hinweis: Wenn Visual Studio ist es nicht zulässig, die die Erweiterung deinstallieren (die Schaltfläche "Deinstallieren" deaktiviert ist), müssen Sie wahrscheinlich zum Neustart von Visual Studio mithilfe von "Ausführen als Administrator."

## <a name="features"></a>Features

### <a name="support-opening-readmetxt-file-after-installation"></a>Unterstützung für das Öffnen von Datei "Readme.txt" nach der installation
Neues in 1.7, wenn das Paket enthält eine `readme.txt` Datei im Stammverzeichnis des NuGet-Pakets wird diese Datei automatisch geöffnet, nach dem Installieren des Pakets abgeschlossen wurde.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Anzeigen von Vorabversionen von Paketen im Dialogfeld "Verwalten von NuGet-Pakete"
Das Dialogfeld "NuGet-Pakete verwalten" enthält jetzt eine Dropdownliste die Option zum Anzeigen von Vorabversionen von Paketen bereitstellt.

![Anzeigen von Vorabversionen von Paketen](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Schaltfläche "Paketwiederherstellung" angezeigt, wenn Paketdateien fehlen
Wenn Sie die Paket-Manager-Konsole öffnen oder das Dialogfeld für die Manager-NuGet-Pakete, NuGet überprüft, ob die aktuelle Projektmappe den Paketwiederherstellung-Modus aktiviert ist und alle Paketdateien fehlen die `packages` Ordner. Wenn beide Bedingungen erfüllt sind, wird NuGet Sie werden benachrichtigt, und zeigt eine einfache Schaltfläche "Wiederherstellen". Auf diese Schaltfläche klicken, löst NuGet aus, um alle fehlenden Pakete wiederherstellen.

![Paket Schaltfläche "Wiederherstellen" im Dialogfeld "](./media/packagerestore-dialog.png)

![Paket Schaltfläche "Wiederherstellen" in-Konsole](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Hinzufügen der Datei auf Projektmappenebene "Packages.config"
In früheren Versionen von NuGet, jedes Projekt verfügt über eine `packages.config` Datei der protokolliert wird, welche NuGet-Pakete in diesem Projekt installiert werden. Allerdings gab es keine ähnliche Datei auf Projektmappenebene zu verfolgen-Pakete auf Projektmappenebene. Daher gab es keine Möglichkeit, die auf lösungsebene Pakete wiederhergestellt werden.
Diese Funktion ist jetzt in NuGet 1.7 implementiert. Auf der lösungsebene `packages.config` Datei befindet sich unter der `.nuget` Unterordner der Projektmappe root an, und wird nur auf Projektmappenebene-Pakete speichern.

### <a name="remove-new-package-command"></a>Befehl "New-Package" entfernen
Der New-paketbefehl wurde aufgrund von mit geringer Auslastung entfernt. Entwicklern werden empfohlen, um nuget.exe oder den praktischen NuGet-Paket-Explorer verwenden, um Pakete zu erstellen.

## <a name="bug-fixes"></a>Fehlerkorrekturen
NuGet 1.7 wurde behoben, dass viele Fehler bei der Paketwiederherstellung Workflow und die Szenarien für Netzwerk/Source-Steuerelement.

Eine vollständige Liste der Arbeit Elemente eine feste in NuGet 1.7. Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
