---
title: NuGet-2.2-Versionshinweise
description: Versionshinweise für NuGet-2.2 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 21f212de53da5faf1ec0762f97a840968b615b19
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822629"
---
# <a name="nuget-22-release-notes"></a>NuGet-2.2-Versionshinweise

[Anmerkungen zur Version des NuGet-2.1](../release-notes/nuget-2.1.md) | [NuGet 2.2.1-Versionshinweise](../release-notes/nuget-2.2.1.md)

NuGet-2.2 wurde 12 Dezember 2012 veröffentlicht.

## <a name="visual-studio-quick-launch"></a>Visual Studio-Schnellstart
Eine der neuen Funktionen, die in Visual Studio 2012 hinzugefügten war die [Schnellstart Dialogfeld](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). NuGet-2.2 erweitert dieses Dialogfeld so initialisieren das Dialogfeld "Paket-Manager" mit den Suchbegriffen, die in der Schnellstartleiste eingegeben haben. Beispielsweise enthält ein eingeben "Jquery" in der Schnellstartleiste jetzt eine Option in den Ergebnissen, NuGet-Pakete "Jquery" Übereinstimmung gesucht werden soll.

![NuGet in Visual Studio-Schnellstart](./media/quick-launch.png)

Nach Auswahl dieser Option wird die standardmäßige NuGet-Paket-Manager Suchfunktionen für den Begriff "Jquery" gestartet.

![Vorgegebenen NuGet-Paket-Manager-Dialogfeld](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Geben Sie ganze Ordner für den Paketinhalt
NuGet-2.2 ermöglicht Ihnen die Angabe für einen ganzen Ordner in jetzt die `<file>` Element von der `.nuspec` Datei, um den Inhalt des Ordners einzuschließen. Beispielsweise wird Folgendes dazu führen, dass alle Skripts im Ordner "Skripts" das Paket auf den Ordner Contents\scripts hinzugefügt, wenn das Paket in einem Projekt installiert wird.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Aktualisieren von 6/24/16: leere Ordner im Ordner "Content" werden ignoriert, wenn Sie das Paket zu installieren.**

## <a name="known-issues"></a>Bekannte Probleme

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Paketinstallation für f#-Projekten schlägt fehl, wenn mit der Paket-Manager-Konsole
Beim Versuch, ein NuGet-Paket in ein f#-Projekt mit der Paket-Manager-Konsole zu installieren, wird eine InvalidOperationException ausgelöst. Wir arbeiten mit dem f#-Team das Problem zu beheben, aber in der Zwischenzeit behelfslösung ist das NuGet-Pakete in F#-Projekte über das Dialogfeld "NuGet Paket-Manager" statt der Konsole zu installieren. [Weitere Informationen finden Sie auf der CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Fehlerkorrekturen
NuGet-2.2 enthält zahlreiche Programmfehlerbehebungen. Eine vollständige Liste der Arbeit Elemente eine feste in NuGet-2.2, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
