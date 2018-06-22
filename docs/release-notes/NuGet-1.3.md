---
title: 1.3 NuGet-Versionshinweise
description: Versionshinweise für NuGet 1.3 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c0284fe0afb11bf6465897132cccd160674ea3e1
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821147"
---
# <a name="nuget-13-release-notes"></a>1.3 NuGet-Versionshinweise

[Anmerkungen zur Version von NuGet 1.2](../release-notes/nuget-1.2.md) | [NuGet 1.4-Versionshinweise](../release-notes/nuget-1.4.md)

NuGet 1.3 wurde 25 April 2011 veröffentlicht.

## <a name="new-features"></a>Neue Funktionen

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Optimierte Paketerstellung mit Symbol-Server-integration

Das NuGet-Team uns, mit der Mitarbeiter bei [SymbolSource.org](http://www.symbolsource.org/) eine sehr einfache Art veröffentlichen Ihre Datenquellen und die PDB-Datei zusammen mit dem Paket anbieten. Dieser Funktion können Consumer des Pakets die Quelle für das Paket im Debugger schrittweise. Weitere Informationen finden Sie unter [erstellen und veröffentlichen ein Symbolpaket](../create-packages/symbol-packages.md) die einfache Methode zum Veröffentlichen von NuGet-Pakete mit Datenquellen. Sie können auch eine live-Demonstration dieses Features im Rahmen des NuGet-ausführlich auf Mix11 wenden Sie sich ansehen. Diese Funktion wird vollständig veranschaulicht beginnend mit der Markierung 20-minütige des Videos.

### <a name="open-packagepage-command"></a>`Open-PackagePage` Befehl

Dieser Befehl vereinfacht, um die Seite "Projekt" für ein Paket aus, in der Paket-Manager-Konsole zu erhalten. Darüber hinaus Optionen, um die Lizenz-URL und den Missbrauch Berichtsseite für das Paket zu öffnen.
Die Syntax für den Befehl lautet:

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

Die `-PassThru` Option wird verwendet, um den Wert der angegebenen URL zurück.

Beispiele:

    PM> Open-PackagePage Ninject

Öffnet einen Browser mit der im Ninject-Paket angegebenen Projekt-URL.

    PM> Open-PackagePage Ninject -License

Öffnet einen Browser mit der im Ninject-Paket angegebenen Lizenz-URL.

    PM> Open-PackagePage Ninject -ReportAbuse

Öffnet einen Browser für die URL auf der aktuellen Paketquelle zum Melden des Missbrauchs des angegebenen Pakets verwendet.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Weist die Lizenz-URL der Variablen, $url, ohne die URL in einem Browser öffnen.

### <a name="performance-improvements"></a>Leistungsverbesserungen

NuGet-1.3 führt viele leistungsverbesserungen. NuGet-1.3 wird vermieden, Herunterladen von mehrmals von einschließlich eines pro Benutzer lokaler Caches für die gleiche Version eines Pakets. Der Cache zugegriffen, und über das Dialogfeld mit Paket-Manager deaktiviert werden kann:

![NuGet-Dialogfeld "Optionen" mit Paket-Cache-Einstellungen](./media/nuget-options.png)

Andere leistungsverbesserungen gehören Hinzufügen der Unterstützung für HTTP-Komprimierung und Verbessern der Geschwindigkeit der Paket-Installation in Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio und nuget.exe verwendet dieselbe Liste der Paketquellen überein

Vor dem NuGet-1.3 die Liste der Paketquellen von nuget.exe und die NuGet-Visual Studio-Add-In verwendet wurden nicht gespeichert am gleichen Ort. NuGet-1.3 verwendet jetzt die gleiche Liste an beiden Orten. Die Liste wird gespeichert, `NuGet.Config` und im Ordner "Anwendungsdaten" gespeichert.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>NuGet.exe ignoriert Dateien und Ordnern, die beginnen mit "." standardmäßig

Um solche Subversion und Mercurial Arbeit mit Quellcode-Verwaltungssysteme NuGet zu machen, nuget.exe ignoriert, Ordner und Dateien, die mit beginnt die '.' Zeichen beim Erstellen von Paketen. Dies kann mit zwei neuen Flags überschrieben werden:

* __-NoDefaultExcludes__ wird verwendet, um diese Einstellung überschreiben, und schließen Sie alle Dateien.
* __-Ausschließen von__ wird verwendet, um weitere Dateien/Ordner ausschließen, die Verwendung eines Musters hinzufügen. Um beispielsweise alle Dateien mit der Erweiterung ". bak" ausschließen

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Hinweis: das Muster ist nicht standardmäßig rekursiv._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Unterstützung für WiX-Projekte und Micro .NET Framework

Dank Beiträge aus der Community enthält NuGet-Unterstützung für WiX-Projekttypen sowie Micro .NET Framework.

## <a name="bug-fixes"></a>Fehlerkorrekturen

Eine vollständige Liste von Fehlerbehebungen, besuchen Sie die [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Fehlerkorrekturen erwähnenswerte

* Pakete mit Quelldateien arbeiten beide Websites und Webanwendungsprojekte.
Für Websites, Quelldateien kopiert werden, in der `App_Code` Ordner
