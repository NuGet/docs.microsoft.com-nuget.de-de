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
# <a name="nuget-22-release-notes"></a>Anmerkungen zu dieser Version von nuget 2,2

Anmerkungen zu dieser [Version von nuget 2,1](../release-notes/nuget-2.1.md)  |  [Anmerkungen zu dieser Version von nuget 2.2.1](../release-notes/nuget-2.2.1.md)

Nuget 2,2 wurde am 12. Dezember 2012 veröffentlicht.

## <a name="visual-studio-quick-launch"></a>Visual Studio-Schnellstart
Eine der neuen Features, die in Visual Studio 2012 hinzugefügt wurde, war das [Dialogfeld Schnellstart](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). Nuget 2,2 erweitert dieses Dialogfeld und ermöglicht es, das Dialogfeld "Paket-Manager" mit den Suchbegriffen zu initialisieren, die im Schnellstart eingegeben wurden. Beispielsweise enthält die Eingabe von "jQuery" in "Schnellstart" nun eine Option in den Ergebnissen, um nuget-Pakete zu suchen, die mit "jQuery" übereinstimmen.

![Nuget in Visual Studio-Schnellstart](./media/quick-launch.png)

Wenn Sie diese Option auswählen, wird die Standardsuche für nuget-Paket-Manager für den Begriff "jQuery" gestartet.

![Dialog Feld "nuget-Paket-Manager" vorab aufgefüllt](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Gesamten Ordner für Paket Inhalt angeben
Mit nuget 2,2 können Sie nun einen gesamten Ordner im- `<file>` Element der Datei angeben `.nuspec` , um den gesamten Inhalt dieses Ordners einzuschließen. Beispielsweise werden durch Folgendes bewirkt, dass alle Skripts im Ordner "Scripts" des Pakets dem Ordner "contents\scripts" hinzugefügt werden, wenn das Paket in einem Projekt installiert wird.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Update 6/24/16: leere Ordner im Ordner "Content" werden ignoriert, wenn das Paket installiert wird.**

## <a name="known-issues"></a>Bekannte Probleme

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Fehler bei der Paketinstallation für F #-Projekte bei Verwendung der Paket-Manager-Konsole
Wenn Sie versuchen, ein nuget-Paket in einem F #-Projekt mithilfe der Paket-Manager-Konsole zu installieren, wird eine InvalidOperationException ausgelöst. Wir arbeiten aktiv mit dem F #-Team zusammen, um das Problem zu beheben, aber in der Zwischenzeit besteht die Problem Umgehung darin, nuget-Pakete in F #-Projekten über das Paket-Manager-Dialogfeld von nuget anstelle der Konsole zu installieren. [Weitere Informationen finden Sie auf CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Fehlerkorrekturen
Nuget 2,2 umfasst viele Fehlerbehebungen. Eine vollständige Liste der Arbeitselemente, die in nuget 2,2 behoben wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
