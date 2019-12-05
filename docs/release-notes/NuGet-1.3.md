---
title: Anmerkungen zu dieser Version von nuget 1,3
description: Anmerkungen zu dieser Version von nuget 1,3 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 45d5caa46d532670e370b81f675663b3c5aaaa95
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825262"
---
# <a name="nuget-13-release-notes"></a>Anmerkungen zu dieser Version von nuget 1,3

Anmerkungen zu [nuget 1,2](../release-notes/nuget-1.2.md) | Anmerkungen zur [nuget](../release-notes/nuget-1.4.md) -Version 1,4

Nuget 1,3 wurde am 25. April 2011 veröffentlicht.

## <a name="new-features"></a>Neue Features

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Optimierte Paket Erstellung mit Symbol Server Integration

Das nuget-Team arbeitet mit den Leuten auf [SymbolSource.org](http://www.symbolsource.org/) zusammen, um eine ganz einfache Möglichkeit zum Veröffentlichen von Quellen und PDB zusammen mit dem Paket zu bieten. Dies ermöglicht es den Benutzern des Pakets, den Einzelschritt in die Quelle Ihres Pakets im Debugger zu überspringen. Weitere Informationen finden Sie unter [Erstellen und Veröffentlichen eines Symbol Pakets](../create-packages/symbol-packages.md) auf einfache Art und Weise, wie Sie nuget-Pakete mit Quellen veröffentlichen können. Sie können sich auch eine Live Demonstration dieses Features als Teil von nuget eingehend unter Mix11 ansehen. Diese Funktion wird ab der 20-minütigen Markierung des Videos vollständig veranschaulicht.

### <a name="open-packagepage-command"></a>`Open-PackagePage` -Befehl

Mit diesem Befehl können Sie in der Paket-Manager-Konsole problemlos zur Projektseite für ein Paket gelangen. Außerdem bietet es Optionen zum Öffnen der Lizenz-URL und der Seite "Missbrauch melden" für das Paket.
Die Syntax für den Befehl lautet wie folgt:

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

Die `-PassThru`-Option wird verwendet, um den Wert der angegebenen URL zurückzugeben.

Beispiele:

    PM> Open-PackagePage Ninject

Öffnet einen Browser mit der Projekt-URL, die im Ninject-Paket angegeben ist.

    PM> Open-PackagePage Ninject -License

Öffnet einen Browser mit der Lizenz-URL, die im Ninject-Paket angegeben ist.

    PM> Open-PackagePage Ninject -ReportAbuse

Öffnet einen Browser mit der URL in der aktuellen Paketquelle, die zum Melden von Missbrauch für das angegebene Paket verwendet wird.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Weist die Lizenz-URL der Variablen zu, $URL, ohne die URL in einem Browser zu öffnen.

### <a name="performance-improvements"></a>Leistungsverbesserungen

Mit nuget 1,3 werden zahlreiche Leistungsverbesserungen eingeführt. Mit nuget 1,3 wird vermieden, dass die gleiche Version eines Pakets mehrmals heruntergeladen wird, indem ein lokaler Cache pro Benutzer eingeschlossen wird. Der Cache kann über das Dialogfeld "Paket-Manager-Einstellungen" aufgerufen und gelöscht werden:

![Dialog Feld "nuget-Optionen" mit Paket Cache Einstellungen](./media/nuget-options.png)

Weitere Leistungsverbesserungen umfassen das Hinzufügen von Unterstützung für die HTTP-Komprimierung und die Verbesserung der Paket Installations Geschwindigkeit in Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>In Visual Studio und "nuget. exe" wird dieselbe Liste von Paketquellen verwendet.

Vor nuget 1,3 wurden die von "nuget. exe" und dem nuget Visual Studio-Add-in verwendeten Paketquellen nicht an derselben Stelle gespeichert. Nuget 1,3 verwendet nun dieselbe Liste an beiden stellen. Die Liste wird in `NuGet.Config` gespeichert und im Ordner AppData gespeichert.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>"nuget. exe" ignoriert Dateien und Ordner, die standardmäßig mit "." beginnen.

Damit nuget gut mit Quell Code Verwaltungssystemen wie Subversion und mercurial funktioniert, ignoriert nuget. exe Ordner und Dateien, die mit dem Zeichen "." beginnen, wenn Pakete erstellt werden. Dies kann überschrieben werden, indem zwei neue Flags verwendet werden:

* __-Nodefaultexcludes__ wird verwendet, um diese Einstellung zu überschreiben und alle Dateien einzuschließen.
* __-Exclude__ wird verwendet, um andere Dateien/Ordner hinzuzufügen, die mit einem Muster ausgeschlossen werden sollen. Um z. b. alle Dateien mit der Dateierweiterung ". bak" auszuschließen.

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Hinweis: das Muster ist standardmäßig nicht rekursiv._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Unterstützung für WiX-Projekte und .net Micro Framework

Dank der Communitybeiträge unterstützt nuget sowohl WiX-Projekttypen als auch das .net Micro Framework.

## <a name="bug-fixes"></a>Fehlerkorrekturen

Eine vollständige Liste der Fehlerbehebungen finden Sie in der [nuget-Problemverfolgung für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Fehlerbehebungen erwähnenswert

* Pakete mit Quelldateien können sowohl in Websites als auch in Webanwendungs Projekten verwendet werden.
Bei Websites werden Quelldateien in den `App_Code` Ordner kopiert.
