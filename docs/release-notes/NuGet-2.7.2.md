---
title: Anmerkungen zu NuGet 2.7.2
description: Anmerkungen zu dieser Version für die Einbindung von NuGet 2.7.2 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3e63944a05f66d5dadf17c5d4b91d3bc4478bb33
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550069"
---
# <a name="nuget-272-release-notes"></a>Anmerkungen zu NuGet 2.7.2

[Anmerkungen zu NuGet 2.7.1](../release-notes/nuget-2.7.1.md) | [Anmerkungen zu NuGet 2.8](../release-notes/nuget-2.8.md)

NuGet 2.7.2 wurde am 11 November 2013 veröffentlicht.

## <a name="noteworthy-bug-fixes-and-features"></a>Wichtige Fehlerbehebungen und Features

### <a name="license-text"></a>Lizenz-Text
Für einige Zeit hat Microsoft die NuGet-Pakete für mehrere beliebte Open Source-Bibliotheken im Rahmen der Standardvorlagen für Webanwendungsprojekte in Visual Studio enthalten. jQuery ist wahrscheinlich das bekannteste Beispiel dieser Art von Bibliothek. Aufgrund der Support-Vertrag zugeordneten Komponenten, die zusammen mit einem Produkt übermittelt werden, enthält die Skript-Datei des Pakets unterschiedliche Lizenz Text als die Skriptdatei finden Sie im gleichen Paket auf den öffentlichen Katalog auf nuget.org. Dieser Unterschied im Text-Format kann verhindern, dass paketupdates Sie den Vorgang fortsetzen, durch die andere Lizenzen Textblöcke, verursacht die Skriptdateien Inhaltshash für unterschiedliche Werte aufweisen (und innerhalb des Projekts aus diesem Grund zum behandelt werden, als geändert).

Um dieses Problem zu beheben, kann NuGet 2.7.2 den Autor des Skripts, um die Lizenz Textblock in einem speziell markierten Abschnitt einzuschließen, die wie folgt aussieht.

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

Beim Aktualisieren der Pakete mit Inhalt Dateien, die dieses Blocks NuGet nicht berücksichtigen den Inhalt des Blocks in den Vergleich mit der Version auf der NuGet Gallery und können daher löschen und aktualisieren die Inhaltsdatei, als ob sie die ursprüngliche Version übereinstimmt.

Dieser Block wird durch den Text "NUGET: beginnen Lizenz TEXT" und "NUGET: END-Lizenz TEXT", die an einer beliebigen Stelle auf den Anfang auftreten und Endzeilen identifiziert.  Keine weiteren Formatierungsoptionen Anforderungen vorhanden sind, können dieses Feature in jeder Art von Textdatei unabhängig von der Sprache verwendet werden.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Leitet die Bindung für nicht - Framework-Assemblys hinzufügen
Für Assemblys, die Teil von .NET Framework sind, lässt NuGet hinzufügen bindungsumleitungen in der Konfigurationsdatei der Anwendung an, beim Aktualisieren des Pakets. Dieses Update behandelt betrachtet eine Regression in NuGet 2.7, bei dem bindungsumleitungen nicht für einige Assemblys hinzugefügten wird, obwohl diese Assemblys nicht sind, Teil von .NET Framework. NuGet 2.7.2 wird wiederhergestellt, der vorherige NuGet 2.5 und 2.6 Verhalten und fügt die bindungsumleitungen.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Installieren von portablen Bibliotheken mit Xamarin-Tools installiert
Wenn die Xamarin Tools für die Entwicklung auf einem Computer installiert sind, ändern sie die unterstützten Frameworks Konfigurationsdaten Geben Sie die Kompatibilität zwischen vorhandenen Kombinationen der Ziel-Framework und Xamarin-Frameworks. Mit Version 2.7.2 NuGet ist jetzt über diese implizite Kompatibilitätsregeln, und daher macht es leicht für Entwickler, die für Xamarin-Plattformen, die portable Bibliotheken, die Xamarin-kompatibel sind, aber nicht explizit markiert als solche in das Paket installieren Metadaten selbst.

### <a name="machine-wide-configuration-settings-honored"></a>Computerweite Einstellungen berücksichtigt
Wenn hierarchische Nuget.Config-Dateien verwenden zu können, wurde der RepositoryPath-Schlüssel für die Datei "NuGet.config"-Dateien, die dem Projektmappenstamm am nächsten nicht berücksichtigt. In Visual Studio 2013 installiert NuGet eine benutzerdefinierte Datei "NuGet.config" unter %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config, um die Paketquelle "Microsoft und .NET" hinzuzufügen. Daher war die problemumgehung für die Verwendung einer benutzerdefinierten RepositoryPath in einer Projektmappe der Computerebene "NuGet.config" - gelöscht werden. Dies bedeutete auch auf die Paketquelle "Microsoft und .NET" zu entfernen. 2.7.2 berücksichtigt nun die Rangfolgeregeln für RepositoryPath bei Verwendung des hierarchische Nuget.Config-Dateien.

## <a name="all-changes"></a>Alle Änderungen
Eine vollständige Liste der Arbeit Elemente eine feste NuGet 2.7.2, bitte Ansicht der [NuGet Issue Tracker für diese Version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
