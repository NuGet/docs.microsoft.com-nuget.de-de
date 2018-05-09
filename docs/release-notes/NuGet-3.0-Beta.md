---
title: NuGet-3,0 Beta-Anmerkungen zu dieser Version
description: Versionshinweise für NuGet 3.0 Beta, einschließlich der bekannten Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4608b196d19f95410f9fe20f6a22e31c15955b89
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-30-beta-release-notes"></a>NuGet-3,0 Beta-Anmerkungen zu dieser Version

[Anmerkungen zur Version von NuGet-3.0-Vorschau](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC-Versionsanmerkungen](../release-notes/nuget-3.0-rc.md)

NuGet-3.0 Beta wurde für die Version von Visual Studio 2015 CTP-Version 6 auf 23 Februar 2015 veröffentlicht. Diese Version bedeutet, dass viel unseres Teams wie wir eine Reihe von Architektur und Performance zur Freigabe haben, und wir freuen uns zum Starten der Optimierung der Leistungseinstellungen auf unseren nuget.org-Dienst.

Es wird dringend empfohlen, dass eine frühere Version der Erweiterung NuGet Visual Studio 2015 deinstallieren, bevor Sie diese neue Version installieren.  Wenn Sie Probleme mit dieser Version der Erweiterung auftreten, sollten Sie Sie wiederherstellen, um die [Vorgängerversionen](http://nuget.codeplex.com/downloads/get/909582) für die Verwendung mit Visual Studio 2015 Preview.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Dieses NuGet-3.0 Beta ist für die Installation in der Visual Studio 2015 CTP-Version 6 Erweiterung Gallery verfügbar. Wir arbeiten daran, löscht der Preview für Visual Studio 2012 und Visual Studio 2013 sehr schnell abzurufen. Wir haben unsere versucht, eine zuvor freigegeben [Updates für Visual Studio 2010 eingestellt](http://blog.nuget.org/20141002/visual-studio-2010.html), und wir haben diese schwierige Entscheidung vorgenommen.

## <a name="new-clientserver-api"></a>Neue Client/Server-API

Wir haben einige Implementierungsdetails für NuGet Client/Server-Protokoll gearbeitet. Unsere Arbeit ist die Erstellung von "API v3" für NuGet, das entworfen wurde, um hohe Verfügbarkeit für kritische Szenarien wie paketwiederherstellung und Installieren von Paketen. Die neue API basiert auf REST und Hypermedia und wir ausgewählt haben [JSON-LD](http://json-ld.org) als Ressourcenformat.

Die Bits NuGet 3.0 Beta finden Sie unter neue Paketquelle "api.nuget.org" in der Dropdownliste der Paket-Quelle aufgerufen.   Bei Auswahl dieser Paketquelle verwenden wir unserer neuen API zur Verbindung mit nuget.org. In NuGet 3.0 RC ersetzt dieser neuen API v3-basierte Paketquelle die Paketquelle v2-basierte "nuget.org".  Deaktivieren alle anderen öffentlichen Paketquellen sollten und behalten Sie Ihr nur öffentliche paketrepository nur api.nuget.org.

Wir haben viel Zeit in die Erstellung unserer API v3 abgelegt und weiterhin die standard-v2-API für die alten Clients zum Zugriff auf die öffentlichen Repositorys Suchvorgänge zu pflegen.

## <a name="updated-ui"></a>Aktualisierte Benutzeroberfläche

Wir haben die Benutzeroberfläche in dieser Version ein Kombinationsfeld-Steuerelement einfügen können Sie zum Auswählen einer Aktion für das Paket ausführen und die Schaltfläche "Vorschau" eines Spiegels noch ein Kontrollkästchen im Bereich des Bildschirms verbessert.  Bereich "Optionen" ist nicht mehr reduzierbare und bietet nun einen Hilfelink klicken, beschreibt die verfügbaren Optionen.

![Die neue NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Protokollierung

Es entfernt das modale Fenster mit Protokollieren von Informationen, die schnell angezeigt werden würden, und während der Installation oder Deinstallation ausblenden.  In diesem Fenster hinzugefügt kein Wert aus, wenn tatsächlich finden die Informationen, oder in der Lage, kopieren und Einfügen von ihm werden soll.  Stattdessen werden wir jetzt alle der Protokollierung in den Paket-Manager-Bereich des Ausgabefensters Ausgabe umleiten.  Wir glauben, dass dies mehr vertraut und ähnelt einer typischen buildberichtsspeicherort, die Sie untersuchen möchten.


### <a name="focus-on-performance"></a>Konzentrieren Sie sich auf die Leistung

Wir haben viele Änderungen im Namen Verbessern der Leistung von NuGet-Suchfunktionen und Abrufvorgänge vorgenommen.  Dies wurde von unseren Kunden unsere höchste relevant, und wir möchten sicher sein, dass wir sie in dieser Version behoben.  Wir haben unsere Server, erstellt einen neuen CDN optimiert und verbessert die Logik zum Übermitteln von hoffentlich treten bei Ihnen relevanter übereinstimmende Abfrage und schnellere Paket Suchergebnisse.

Wie wir über diese Phase der Entwicklung von NuGet 3.0 fortfahren, werden wir optimieren und Überwachung den nuget.org-Dienst, um sicherzustellen, dass wir eine verbesserte benutzererfahrung bereitzustellen.  Wir keine Einbindung in die Ausfallzeiten, möchten jedoch wird werden hinzufügen und Ressourcen im Dienst ändern.  Achten Sie auf unserer [twitter-Feed](http://twitter.com/nuget) Details auf, wenn es die Dienstkonfiguration ändern.

## <a name="building-nuget-with-nuget"></a>Erstellen von NuGet mit NuGet

Wir haben unsere NuGet-Clients in mehreren Komponenten neu entworfen, die selbst wird in NuGet-Pakete erstellt werden. Dieser erneuten Verwendung eines eigenen Bibliotheken erzwingt uns um Komponenten zu erstellen, die wiederholt verwendbare sind und ordnungsgemäß verpackt werden können.  Es wurden doppelte Code eliminiert und haben gelernt, wie Sie unsere Entwicklungsprozesses zur Unterstützung der Notwendigkeit zum Erstellen von Paketen in der gesamten unseren Lösungen für eine bessere Leistung konfigurieren können.  Suchen Sie nach bald einen Blogbeitrag, in denen beschäftigen wir uns wie die Codeprojekte strukturiert sind und zur Funktionsweise von unseren Build-Prozesses.

## <a name="stay-tuned"></a>Bleiben Sie dran

Bitte achten Sie auf [unserem Blog](http://blog.nuget.org) weitere Bearbeitung und Ankündigungen für NuGet 3.0!
