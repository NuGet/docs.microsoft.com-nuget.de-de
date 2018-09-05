---
title: Anmerkungen zu NuGet 3.0 Beta
description: Anmerkungen zu NuGet 3.0 Beta, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9f9fec6a1af8dfbcfdcfa05a301ff52409521228
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550912"
---
# <a name="nuget-30-beta-release-notes"></a>Anmerkungen zu NuGet 3.0 Beta

[Anmerkungen zu NuGet 3.0 Preview](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC-Versionsanmerkungen](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 Beta wurde am 23. Februar 2015 für die Visual Studio 2015 CTP 6-Version veröffentlicht. Diese Version bedeutet, dass viel unser Team, wir haben eine Reihe von Verbesserungen von Architektur und Leistung freigeben, und wir freuen uns zum Starten der Optimierung der Leistungseinstellungen auf der nuget.org-Dienst.

Es wird dringend empfohlen, dass Sie frühere Version der Erweiterung NuGet Visual Studio 2015 deinstallieren, bevor Sie diese neue Version installieren.  Wenn Sie Probleme mit dieser Version der Erweiterung auftreten, sollten Sie Sie zum Wiederherstellen der [frühere Version](http://nuget.codeplex.com/downloads/get/909582) für die Verwendung mit Visual Studio 2015 Preview.

## <a name="visual-studio-2012"></a>Visual Studio 2012 und höher

Dieses NuGet 3.0 Beta steht in Visual Studio 2015 CTP 6-Erweiterungskatalog zu installieren. Wir arbeiten daran, Vorschau löscht sehr bald für Visual Studio 2012 und Visual Studio 2013 machen. Wir haben unsere Absicht, zuvor freigegeben [Updates für Visual Studio 2010 eingestellt](http://blog.nuget.org/20141002/visual-studio-2010.html), und wir, schwierige Entscheidung treffen.

## <a name="new-clientserver-api"></a>Neue Client/Server-API

Wir haben einige Implementierungsdetails für NuGets-Client/Server-Protokoll gearbeitet. Die Arbeit habe ist die Erstellung von "-API v3" für NuGet, das entworfen wurde, um hochverfügbarkeit für kritische Szenarien wie z. B. das Wiederherstellen von Paketen und Installieren von Paketen. Die neue API basiert auf REST und Hypermedia, und wir ausgewählt haben [JSON-LD](http://json-ld.org) als unsere Ressourcenformat.

In den NuGet 3.0 Beta-Bits sehen Sie eine neue Paketquelle, die Namen "api.nuget.org" in der Dropdownliste der Paket-Quelle.   Wenn Sie diese Paketquelle auswählen, verwenden wir unsere neue API, sondern für die Verbindung "NuGet.org". In NuGet 3.0 RC wird diese neue API-v3-basierte Paketquelle Paketquelle von v2-basierte "nuget.org" ersetzt.  Wir empfehlen, Deaktivieren aller anderen öffentlichen Paketquellen und behalten Sie Ihre einzige öffentliche paketrepository nur api.nuget.org.

Wir haben viel Zeit mit dem Erstellen von unserer API v3 sollen und weiterhin die standard-v2-API für die alten Clients, die auf öffentlichen Repository suchen zu verwalten.

## <a name="updated-ui"></a>Aktualisierte Benutzeroberfläche

Wir haben erweitert, dass die Benutzeroberfläche in dieser Version ein Kombinationsfeld zu enthalten, können Sie wählen Sie eine auszuführende Aktion, mit dem Paket und ein Kontrollkästchen im Bereich des Bildschirms die Schaltfläche "Vorschau" übernommen.  Bereich "Optionen" ist nicht mehr reduzierbare und bietet jetzt einen Hilfelink klicken, beschreibt die verfügbaren Optionen.

![Die neue NuGet UI](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Protokollierung

Es entfernt die modale Fenster mit Protokollieren von Informationen, die schnell angezeigt werden und während der Installation oder Deinstallation ausblenden.  Dieses Fenster hinzugefügt kein Wert aus, wenn Sie wirklich finden Informationen oder in der Lage zu kopieren und einzufügen, daraus möchten.  Stattdessen werden wir jetzt die gesamte Protokollierung in den Paket-Manager-Bereich des Ausgabefensters Ausgabe umleiten.  Wir denken, dass dies ist besser vertraut und ähnlich wie eine typische Buildbericht an, dem Sie untersuchen möchten.


### <a name="focus-on-performance"></a>Konzentrieren Sie sich auf die Leistung

Wir haben viele Änderungen, die Namen der Verbesserung der Leistung des NuGet-suchen und abrufen.  Das war unsere Nummer eins Problem von unseren Kunden, und wir wollten Sie sicher, dass wir es in dieser Version behoben.  Wir haben unsere Server, erstellt ein neues CDN, optimiert und verbessert die Logik, um hoffentlich liefern Ihnen weitere wichtige übereinstimmende Abfrage und schneller Suchergebnisse zur Paket.

Wenn wir über diese Phase der Entwicklung von NuGet 3.0 fortfahren, werden wir optimieren und Überwachung des Diensts "NuGet.org", um sicherzustellen, dass wir eine größere benutzerfreundlichkeit bereitzustellen.  Wir nicht möchten, die Einbindung in die Ausfallzeiten, jedoch wird werden hinzufügen und Ändern von Ressourcen im Dienst.  Achten Sie auf unserer [twitter-Feed](http://twitter.com/nuget) Einzelheiten, wenn wir die Dienstkonfiguration ändern.

## <a name="building-nuget-with-nuget"></a>Erstellen von NuGet mit NuGet

Wir haben unsere NuGet-Clients in mehreren Komponenten neu entworfen, die selbst wird in NuGet-Pakete erstellt werden. Diese erneute Verwendung unserer eigenen Bibliotheken erzwingt, dass wir zum Erstellen von Komponenten, die wieder verwendbare sind und ordnungsgemäß gepackt werden können.  Wir konnten zu eliminieren von doppelten Code haben gelernt, wie so konfigurieren Sie besser auf unserem Entwicklungsprozess, um die Notwendigkeit zum Erstellen von Paketen in der gesamten unsere Lösungen zu unterstützen.  Suchen Sie nach in Kürze einen Blogbeitrag, in denen beschäftigen wir uns wie die Codeprojekten strukturiert sind und wie unsere Buildprozess funktioniert.

## <a name="stay-tuned"></a>Bleiben Sie dran

Bitte achten Sie auf [unseren Blog](http://blog.nuget.org) für die weitere Bearbeitung sowie Ankündigungen von NuGet 3.0!
