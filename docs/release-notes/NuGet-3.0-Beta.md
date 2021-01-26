---
title: Anmerkungen zu dieser Version von nuget 3,0 Beta
description: Anmerkungen zu dieser Version von nuget 3,0 Beta einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7970c3d81c724edc743d7b2d38c4c157237a0271
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776628"
---
# <a name="nuget-30-beta-release-notes"></a>Anmerkungen zu dieser Version von nuget 3,0 Beta

Anmerkungen zu dieser [Version von nuget 3,0 Preview](../release-notes/nuget-3.0-preview.md)  |  [Anmerkungen zu dieser Version von nuget 3,0 RC](../release-notes/nuget-3.0-rc.md)

Nuget 3,0 Beta wurde am 23. Februar 2015 für die Version Visual Studio 2015 CTP 6 veröffentlicht. Diese Version ist für unser Team sehr viel zu tun, da wir eine Reihe von Verbesserungen an Architektur und Leistung haben, und wir freuen uns, die Leistungseinstellungen in unserem nuget.org-Dienst zu optimieren.

Es wird dringend empfohlen, dass Sie vor der Installation dieser neuen Version eine frühere Version der nuget Visual Studio 2015-Erweiterung deinstallieren.  Wenn Sie Probleme mit dieser Version der Erweiterung haben, empfehlen wir, dass Sie die [vorherige Version](http://nuget.codeplex.com/downloads/get/909582) für die Verwendung mit Visual Studio 2015 Preview wiederherstellen.

## <a name="visual-studio-2012"></a>Visual Studio 2012 und höher

Diese nuget 3,0 Beta-Version ist für die Installation im Visual Studio 2015 CTP 6-Erweiterungs Katalog verfügbar. Wir arbeiten daran, die Vorschau für Visual Studio 2012 zu erhalten, und Visual Studio 2013 sehr bald. Wir haben unsere Absicht bereits zum [Beenden von Updates für Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)freigegeben, und wir haben diese schwierige Entscheidung getroffen.

## <a name="new-clientserver-api"></a>Neue Client/Server-API

Wir arbeiten an einigen Implementierungsdetails für das Client/Server-Protokoll von nuget. Die Arbeit, die wir erledigt haben, ist das Erstellen von "API v3" für nuget, das um hohe Verfügbarkeit für kritische Szenarien wie die Paket Wiederherstellung und die Installation von Paketen entworfen wurde. Die neue API basiert auf Rest und Hypermedia, und wir haben [JSON-LD](http://json-ld.org) als Ressourcen Format ausgewählt.

In den nuget 3,0 Beta-Bits wird in der Dropdown Liste Paketquelle eine neue Paketquelle namens "API.nuget.org" angezeigt.   Wenn Sie diese Paketquelle auswählen, verwenden wir stattdessen unsere neue API, um eine Verbindung mit nuget.org herzustellen. In nuget 3,0 RC ersetzt diese neue API-v3-basierte Paketquelle die V2-basierte Paketquelle "nuget.org".  Es wird empfohlen, alle anderen öffentlichen Paketquellen zu deaktivieren und nur API.nuget.org als das einzige öffentliche Paketrepository zu belassen.

Wir haben viel Zeit für das entwickeln unserer V3-API und für alte Clients, die auf das öffentliche Repository zugreifen möchten, weiterhin die Standard-v2-API beibehalten.

## <a name="updated-ui"></a>Aktualisierte Benutzeroberfläche

Wir haben die Benutzeroberfläche in dieser Version um ein Kombinations Feld erweitert, mit dem Sie eine Aktion auswählen können, die mit dem Paket ausgeführt werden soll, und die Vorschau Schaltfläche in ein Kontrollkästchen im Optionsbereich des Bildschirms übergeht.  Der Optionsbereich ist nicht mehr redusible und bietet jetzt einen Hilfelink, der die verfügbaren Optionen beschreibt.

![Die neue nuget-Benutzeroberfläche](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Vorgangs Protokollierung

Wir haben das modale Fenster mit Protokollinformationen entfernt, die beim Installieren oder Deinstallieren von schnell angezeigt und ausgeblendet werden.  In diesem Fenster wurde kein Wert hinzugefügt, wenn Sie die Informationen wirklich anzeigen oder kopieren und einfügen können.  Stattdessen wird die gesamte Ausgabe Protokollierung in den Bereich Paket-Manager des Ausgabe Fensters umgeleitet.  Wir sind der Ansicht, dass dies bequemer ist und einem typischen Buildbericht ähnelt, den Sie überprüfen möchten.


### <a name="focus-on-performance"></a>Fokus auf Leistung

Wir haben viele Änderungen am Namen der Verbesserung der Leistung von nuget-suchen und-Abruf Vorgängen vorgenommen.  Dies war unsere einzige Angelegenheit unserer Kunden, und wir wollten sicher sein, dass wir Sie in dieser Version behandelt haben.  Wir haben unsere Server optimiert, ein neues CDN erstellt und die Abfrage Übereinstimmungs Logik verbessert, um Ihnen die Bereitstellung relevanterer und schnellerer Ergebnisse der Paket Suche zu ermöglichen.

Bei der Durchführung dieser Phase der Entwicklung von nuget 3,0 werden wir den nuget.org-Dienst optimieren und überwachen, um sicherzustellen, dass wir eine bessere Leistung bieten.  Wir planen keine Ausfallzeiten, sondern werden Ressourcen im Dienst hinzufügen und ändern.  Beachten Sie den Twitter- [Feed](http://twitter.com/nuget) , um Details dazu zu erhalten, wann die Dienst Konfiguration geändert wird.

## <a name="building-nuget-with-nuget"></a>Nuget mit nuget entwickeln

Wir haben unsere nuget-Clients nun in verschiedene Komponenten integriert, die in nuget-Pakete integriert werden. Diese erneute Verwendung unserer eigenen Bibliotheken zwingt uns, Komponenten zu erstellen, die wiederverwendbar sind und ordnungsgemäß verpackt werden können.  Wir konnten duplizierten Code eliminieren und wissen, wie Sie den Entwicklungsprozess besser konfigurieren können, um das Erstellen von Paketen während unserer Lösungen zu unterstützen.  Suchen Sie nach einem Blogbeitrag, in dem erläutert wird, wie die Code Projekte strukturiert sind und wie unser Buildprozess funktioniert.

## <a name="stay-tuned"></a>Bleiben Sie dran

Im [Blog](http://blog.nuget.org) erhalten Sie weitere Informationen zum Fortschritt und Ankündigungen für nuget 3,0!
