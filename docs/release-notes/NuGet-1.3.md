---
title: Anmerkungen zu NuGet 1.3
description: Anmerkungen zu NuGet 1.3, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551350"
---
# <a name="nuget-13-release-notes"></a>Anmerkungen zu NuGet 1.3

[Anmerkungen zu NuGet 1.2](../release-notes/nuget-1.2.md) | [Anmerkungen zu NuGet 1.4](../release-notes/nuget-1.4.md)

NuGet 1.3 wurde 25 April 2011 veröffentlicht.

## <a name="new-features"></a>Neue Funktionen

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Optimierte Paketerstellung mit Symbol-Server-integration

Das NuGet-Team eine Partnerschaft eingegangen, mit den Leuten bei [SymbolSource.org](http://www.symbolsource.org/) bieten eine ganz einfache Möglichkeit der Veröffentlichung von Ihren Quellen und der PDB Datei zusammen mit Ihrem Paket. Dieser Funktion können Consumer des Pakets die Quelle für das Paket im Debugger schrittweise. Weitere Informationen finden Sie in [erstellen und Veröffentlichen eines Symbolpakets](../create-packages/symbol-packages.md) eine einfache Methode zum Veröffentlichen von NuGet-Pakete mit Datenquellen. Sie können auch eine live-Demonstration dieser Funktion als Teil des NuGet-Pakets im Detail sprechen MIX11 ansehen. Dieses Feature wird vollständig veranschaulicht. an der Marke 20-minütige des Videos ab.

### <a name="open-packagepage-command"></a>`Open-PackagePage` Befehl

Mit diesem Befehl erleichtert es, um das Projekt – Seite für ein Paket aus, in der Paket-Manager-Konsole zu erhalten. Darüber hinaus Optionen, um die Lizenz-URL und den Missbrauch Berichtsseite für das Paket zu öffnen.
Die Syntax für den Befehl lautet:

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

Die `-PassThru` Option wird verwendet, um den Wert der angegebenen URL zurück.

Beispiele:

    PM> Open-PackagePage Ninject

Öffnet einen Browser mit der im Ninject-Paket angegebenen Projekt-URL.

    PM> Open-PackagePage Ninject -License

Öffnet einen Browser mit der im Ninject-Paket angegebenen Lizenz-URL.

    PM> Open-PackagePage Ninject -ReportAbuse

Öffnet einen Browser für die URL auf der aktuellen Paketquelle, die zum Melden von Missbrauch für das angegebene Paket.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Die URL der Variablen zugewiesen, $url, ohne die URL in einem Browser öffnen.

### <a name="performance-improvements"></a>Leistungsverbesserungen

NuGet 1.3 werden viele der leistungsverbesserungen eingeführt. NuGet 1.3 verhindert das Herunterladen von mehrere Male mit einem pro Benutzer lokalen Cache für der gleichen Version eines Pakets. Der Cache zugegriffen, und über das Dialogfeld "Paket-Manager-Einstellungen" deaktiviert werden kann:

![NuGet-Dialogfeld "Optionen" mit Cache-Paketeinstellungen](./media/nuget-options.png)

Andere leistungsoptimierungen gehören das Hinzufügen von Unterstützung für HTTP-Komprimierung, und Verbessern der Geschwindigkeit der Paket-Installation in Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio und nuget.exe verwendet die gleiche Liste von Paketquellen

Vor dem NuGet-1.3 die Liste der Paketquellen von nuget.exe und dem NuGet Visual Studio-Add-In verwendet wurden nicht gespeichert am selben Ort. NuGet 1.3 verwendet jetzt die gleiche Liste an beiden Orten. Die Liste wird gespeichert, `NuGet.Config` und im Ordner "AppData" gespeichert.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>NuGet.exe ignoriert Dateien und Ordnern, die mit '.' in der Standardeinstellung

Um NuGet mit Quellcodeverwaltungssystemen wie Subversion und Mercurial arbeiten zu können, nuget.exe ignoriert, Ordner und Dateien, die mit der '.' Zeichen beim Erstellen von Paketen. Dies kann mit zwei neuen Flags überschrieben werden:

* __-NoDefaultExcludes__ wird verwendet, um diese Einstellung überschreiben, und schließen Sie alle Dateien.
* __-Ausschließen__ wird verwendet, um andere Dateien bzw. Ordner ausschließen, unter Verwendung eines Musters hinzufügen. Um beispielsweise alle Dateien mit der Dateierweiterung '. bak' ausschließen

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Hinweis: das Muster ist nicht standardmäßig rekursiv._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Unterstützung für WiX-Projekten und .NET Micro Framework

Unser Dank gilt den Community-Beiträge unterstützt NuGet WiX-Projekttypen als auch das .NET Micro Framework.

## <a name="bug-fixes"></a>Fehlerkorrekturen

Eine vollständige Liste der Fehlerbehebungen, lesen Sie die [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Fehlerkorrekturen Beachten

* Pakete mit den Quelldateien funktioniert in beide Websites und Web Application Projects.
Für Websites, Quelldateien kopiert werden, in der `App_Code` Ordner
