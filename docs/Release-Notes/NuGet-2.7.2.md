---
title: Anmerkungen zur Version des NuGet-2.7.2 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 2.7.2 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-2.7.2 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8fe9acc3ad9c1c368fc750694ea523ac845995c5
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-272-release-notes"></a>Anmerkungen zur Version von NuGet 2.7.2

[Anmerkungen zur Version des NuGet-2.7.1](../release-notes/nuget-2.7.1.md) | [NuGet 2.8-Versionshinweise](../release-notes/nuget-2.8.md)

NuGet 2.7.2 wurde 11 November 2013 veröffentlicht.

## <a name="noteworthy-bug-fixes-and-features"></a>Wichtige Fehlerbehebungen und Features

### <a name="license-text"></a>Lizenz Text
Für einige Zeit hat Microsoft die NuGet-Pakete für verschiedene gängige Open Source-Bibliotheken im Rahmen der Standardvorlagen für Webanwendungsprojekte in Visual Studio enthalten. jQuery ist wahrscheinlich das bekannteste Beispiel dieses Typs der Bibliothek. Aufgrund der Support-Vertrag mit den Komponenten, die zusammen mit einem Produkt übermittelt werden, enthält die Paket-Skriptdatei unterschiedliche Lizenz Text als die Skriptdatei im selben Paket auf dem öffentlichen nuget.org-Katalog gefunden. Dieser Unterschied in Text kann verhindern, dass Updates für Sie den Vorgang fortsetzen, aufgrund der verschiedenen Lizenz Textblöcke verursacht die Skriptdateien Inhaltshash unterschiedliche Werte aufweisen (und deshalb um behandelt werden, als geändert, innerhalb des Projekts).

Um dieses Problem zu minimieren, kann NuGet 2.7.2 Skriptautoren um die Lizenz Textblock innerhalb eines Abschnitts speziell markierter einzuschließen, die wie folgt aussieht.

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

Beim Aktualisieren der Pakete mit Inhalt Dateien, die dieser Block enthält NuGet nicht verlagern Sie den Inhalt des Blocks in der Vergleich mit der Version in der NuGet Gallery und können daher löschen und aktualisieren die Inhaltsdatei aus, als ob es sich um die ursprüngliche Kopie entspricht.

Dieser Block wird durch den Text "NuGet-:) beginnen Lizenz TEXT" und "NuGet-: END Lizenz TEXT", die an einer beliebigen Stelle auf den Anfang auftreten und Endzeilen identifiziert.  Keine weiteren Formatierung Anforderungen vorhanden sind, können diese Funktion, die in jede Art von Textdatei unabhängig von der Sprache verwendet werden.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Leitet die Bindung für nicht - Framework-Assemblys hinzufügen
Für Assemblys, die Teil von .NET Framework sind, überspringt NuGet hinzufügen bindungsumleitungen in der Konfigurationsdatei der Anwendung, wenn das Paket aktualisiert. Dieses Update behebt berücksichtigt ein Rückschritt in NuGet 2.7, bei dem umleitungen für Bindungen nicht für einige ausgewählte Assemblys hinzugefügten wird, obwohl diese Assemblys nicht sind, ein Bestandteil von .NET Framework. NuGet 2.7.2 stellt die vorherigen NuGet 2.5 und 2.6 Verhalten wieder her und fügt die bindungsumleitungen hinzu.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Installieren portable Bibliotheken mit Xamarin-Tools installiert
Wenn Sie die Xamarin Entwicklungstools, die auf einem Computer installiert sind, ändern sie die Konfigurationsdaten unterstützten Frameworks, um Informationen zur Kompatibilität von vorhandenen Kombinationen der Ziel-Framework und Xamarin-Frameworks anzugeben. Mit Version 2.7.2 NuGet ist jetzt diese implizite Kompatibilitätsregeln kennen, und daher erleichtert für Entwickler, die Zielplattformen für Xamarin, die portable Bibliotheken, die Xamarin-kompatibel sind, aber nicht explizit markiert als solche in das Paket installieren Metadaten selbst.

### <a name="machine-wide-configuration-settings-honored"></a>Computerweite Einstellungen berücksichtigt
Bei Verwendung von hierarchischen "NuGet.config" Datendateien wurde der RepositoryPath-Schlüssel nicht für "NuGet.config" Dateien in das Stammverzeichnis der Projektmappe nächstgelegenen berücksichtigt wird. In Visual Studio 2013 installiert NuGet eine benutzerdefinierte Datei "NuGet.config" %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config, um die Paketquelle "Microsoft und .NET" hinzuzufügen. Daher wurde die problemumgehung für die Verwendung einer benutzerdefinierten RepositoryPath in einer Projektmappe Löschen von der Computerebene "NuGet.config" - dadurch auch musste die Paketquelle "Microsoft und .NET" entfernen. NuGet 2.7.2 berücksichtigt nun die Rangfolgeregeln für RepositoryPath bei Verwendung von hierarchischen "NuGet.config" Datendateien.

## <a name="all-changes"></a>Alle Änderungen
Eine vollständige Liste der Arbeit Elemente in behoben NuGet 2.7.2, bitte Ansicht der [NuGet Issue Tracker für diese Version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
