---
title: Nuget 2.7.2 Anmerkungen zu dieser Version
description: Anmerkungen zu dieser Version von nuget 2.7.2 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7643bf930bca39684eb626fe737001bc3e3ea769
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776786"
---
# <a name="nuget-272-release-notes"></a>Nuget 2.7.2 Anmerkungen zu dieser Version

Anmerkungen zu dieser [Version von nuget 2.7.1](../release-notes/nuget-2.7.1.md)  |  [Anmerkungen zu dieser Version von nuget 2,8](../release-notes/nuget-2.8.md)

Nuget 2.7.2 wurde am 11. November 2013 veröffentlicht.

## <a name="noteworthy-bug-fixes-and-features"></a>Wichtige Fehlerbehebungen und Features

### <a name="license-text"></a>Lizenz Text
Seit einiger Zeit ist Microsoft das nuget-Paket für mehrere beliebte Open Source-Bibliotheken als Teil der Standardvorlagen für Webanwendungs Projekte in Visual Studio integriert. jQuery ist wahrscheinlich das bekannteste Beispiel für diese Art von Bibliothek. Aufgrund des Supportvertrags, der Komponenten zugeordnet ist, die zusammen mit einem Produkt übermittelt werden, enthält die Skriptdatei des Pakets einen anderen Lizenztext als die Skriptdatei, die im selben Paket im öffentlichen nuget.org-Katalog gefunden wurde. Dieser Unterschied in Text kann verhindern, dass Paket Aktualisierungen aufgrund der unterschiedlichen Lizenztext Blöcke fortgesetzt werden, was dazu führt, dass die Skriptdateien verschiedene Inhalts Hash Werte aufweisen (und daher im Projekt als geändert behandelt werden).

Um dieses Problem zu beheben, kann der Skript Ersteller mit nuget 2.7.2 den Lizenz TextBlock in einen besonders markierten Abschnitt einschließen, der wie folgt aussieht.

```
/************** NUGET: BEGIN LICENSE TEXT **************
    * The following code is licensed under the MIT license
    * Additional license information below is informational
    * only.
    ************** NUGET: END LICENSE TEXT ***************/
```

Beim Aktualisieren von Paketen mit Inhalts Dateien, die diesen Block enthalten, wird der Inhalt des Blocks von nuget nicht in den Vergleich mit der Version im nuget-Katalog eingeteilt. Daher kann die Inhalts Datei so gelöscht und aktualisiert werden, als ob Sie mit der ursprünglichen Kopie übereinstimmt.

Dieser Block wird durch den Text "nuget: begin License Text" und "nuget: End License Text" identifiziert, die an einer beliebigen Stelle in der Anfangs-und der Endlinie auftreten.  Es sind keine weiteren Formatierungs Anforderungen vorhanden, sodass diese Funktion unabhängig von der Sprache in beliebigen Textdatei Typen verwendet werden kann.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Bindungs Umleitungen für nicht-Framework-Assemblys hinzufügen
Bei Assemblys, die Teil der .NET Framework sind, überspringt nuget das Hinzufügen von Bindungs Umleitungen in die Konfigurationsdatei der Anwendung, wenn das Paket aktualisiert wird. Diese Korrektur behandelt eine Regression in nuget 2,7, bei der keine Bindungs Umleitungen für einige Assemblys hinzugefügt wurden, auch wenn diese Assemblys nicht als Teil der .NET Framework angesehen werden. Nuget 2.7.2 stellt das vorherige Verhalten von nuget 2,5 und 2,6 wieder her und fügt die Bindungs Umleitungen hinzu.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Installieren von portablen Bibliotheken mit installierter xamarin-Tools
Wenn die Entwicklungs Tools von xamarin auf einem Computer installiert sind, ändern Sie die unterstützten Frameworks-Konfigurationsdaten, um die Kompatibilität zwischen vorhandenen Ziel Framework-Kombinationen und xamarin-Frameworks anzugeben. Mit Version 2.7.2 erkennt nuget jetzt diese impliziten Kompatibilitäts Regeln und erleichtert Entwicklern, die auf xamarin-Plattformen abzielen, die Installation portabler Bibliotheken, die xamarin-kompatibel sind, aber nicht explizit als solche in den Paket Metadaten selbst gekennzeichnet sind.

### <a name="machine-wide-configuration-settings-honored"></a>Computer weite Konfigurationseinstellungen berücksichtigt
Wenn Sie hierarchische Nuget.Config Dateien verwenden, wurde der repositoryPath-Schlüssel für Nuget.Config Dateien, die dem Projektmappenstamm am nächsten liegen, nicht berücksichtigt. In Visual Studio 2013 installiert nuget eine benutzerdefinierte Nuget.Config Datei unter% Program Data% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config, um die Paketquelle "Microsoft und .net" hinzuzufügen. Daher war das Problem bei der Verwendung eines benutzerdefinierten repositoryPath in einer Lösung das Löschen der Nuget.Config auf Computer Ebene, was auch bedeutete, dass die Paketquelle "Microsoft und .net" entfernt wurde. Nuget 2.7.2 berücksichtigt jetzt die Rang folgen Regeln für repositoryPath, wenn hierarchische Nuget.Config Dateien verwendet werden.

## <a name="all-changes"></a>Alle Änderungen
Eine vollständige Liste der Arbeitselemente, die in nuget-2.7.2 behoben sind, finden Sie in der [nuget-Problemverfolgung für diese Version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
