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
# <a name="nuget-22-release-notes"></a>Anmerkungen zu NuGet-Version 2.2

[Anmerkungen zu NuGet 2.1](../release-notes/nuget-2.1.md) | [Anmerkungen zu NuGet 2.2.1](../release-notes/nuget-2.2.1.md)

NuGet 2.2 wurde am 12. Dezember 2012 veröffentlicht.

## <a name="visual-studio-quick-launch"></a>Visual Studio-Schnellstart
Eines der neuen Features, die in Visual Studio 2012 hinzugefügt wurde wurde die [Schnellstart Dialogfeld](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). NuGet 2.2 erweitert dieses Dialogfeld ermöglicht es, um das Dialogfeld "Paket-Manager" mit den Suchbegriffen, die in der Schnellstartleiste eingegeben zu initialisieren. Jetzt eingeben von "Jquery" in der Schnellstartleiste umfasst z. B. eine Option in den Ergebnissen aus, um NuGet-Pakete, die Übereinstimmung von "Jquery" zu suchen.

![NuGet in Visual Studio-Schnellstart](./media/quick-launch.png)

Nach Auswahl dieser Option wird die standard NuGet-Paket-Manager Suchfunktion für den Begriff "Jquery" gestartet.

![Vorab aufgefüllte NuGet-Paket-Manager-Dialogfeld](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Geben Sie ganze Ordner für den Inhalt des Pakets
NuGet 2.2 können Sie an einen ganzen Ordner in nun der `<file>` Element der `.nuspec` hinzu, um den Inhalt dieses Ordners einzubeziehen. Beispielsweise wird Folgendes dazu führen, dass alle Skripts im Ordner "Scripts" des Pakets, zu dem Ordner Contents\scripts hinzugefügt werden, wenn das Paket in einem Projekt installiert wird.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Aktualisieren Sie 6/24/16: leere Ordner im Ordner "Content" werden ignoriert, wenn es sich bei der Installation des Pakets.**

## <a name="known-issues"></a>Bekannte Probleme

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Paketinstallation für f#-Projekte schlägt fehl, wenn Sie die Paket-Manager-Konsole verwenden
Beim Versuch, ein NuGet-Paket in ein F#-Projekt mithilfe der Paket-Manager-Konsole zu installieren, wird eine "InvalidOperationException" ausgelöst. Wir arbeiten aktiv mit dem F#-Team das Problem zu beheben, aber in der Zwischenzeit die problemumgehung besteht darin, NuGet-Pakete in F#-Projekten über das Dialogfeld "NuGet Paket-Manager" statt der Konsole zu installieren. [Weitere Informationen finden Sie auf CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Fehlerkorrekturen
NuGet 2.2 enthält zahlreiche Programmfehlerbehebungen. Eine vollständige Liste der Arbeit Elemente eine feste in NuGet 2.2, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
