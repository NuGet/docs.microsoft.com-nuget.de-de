---
title: NuGet 3.4-Versionshinweise
description: Versionshinweise für NuGet 3.4, einschließlich der bekannten Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f2a945b628022bdcc6e69a7a4b1be6c53b65626
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820471"
---
# <a name="nuget-34-release-notes"></a>NuGet 3.4-Versionshinweise

[NuGet 3.4-RC-Versionsanmerkungen](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1-Versionshinweise](../release-notes/nuget-3.4.1.md)

NuGet 3.4 30. März 2016 freigegeben wurde, als Teil der Visual Studio 2015 Update 2 und Visual Studio 15 Preview-Version und einige Grundsätze in Köpfen erstellt wurde:

* Plattformübergreifende Unterstützung
* Leistungsverbesserungen
* Kleinere Verbesserungen der Benutzeroberfläche

Die folgenden Funktionen wurden wurden zuvor in RC hinzugefügt und aktualisiert oder für die Version 3.4 abgeschlossen:

## <a name="new-features"></a>Neue Funktionen

* NuGet-Clients unterstützen jetzt Gzip-inhaltscodierung von Repositorys
* Unterstützung für die PDB-Dateien von Paketen in Xproj-Projekten
* Unterstützung für IOS- und Android-Buildvorgänge im inhaltsdateienelement
* Unterstützung für die netstandard- und Netstandardapp-frameworkMoniker

## <a name="new-user-interface-features"></a>Neue Features der Benutzeroberfläche

* Signifikante leistungsverbesserungen besonders auf den Registerkarten installiert, Updates und konsolidieren
* Aggregatquelle "Alle Paketquellen" steht mit der richtigen Suche Ergebnis zusammenführen
* Installiert und Updates Registerkarten sind jetzt alphabetisch sortiert
* Schaltfläche "Aktualisieren", die eine zu aktualisierende-Suche erlaubt hinzugefügt
* Neueste Buildoptionen am oberen Rand der Liste Version

## <a name="updates-and-improvements"></a>Updates und Verbesserungen

* Pakete, die auf die verwiesen wird `project.json` , auf denen eine Gleitkommazahl-Version wird nicht auf jedem Build aktualisieren. Stattdessen werden sie aktualisieren nur, wenn Sie gezwungen, wiederherzustellen, bereinigen, neu erstellen oder ändern Sie `project.json`.
* Bei Verwendung der NuGet-Konfigurations-UI nicht mehr NuGet.org Repository Quellen in einer Projektkonfiguration gezwungen.
* NuGet nicht mehr wiederhergestellt Pakete in gemeinsam genutzte Projekte noch eine Sperrdatei schreibt.
* Wir haben Netzwerkausfall verbessert, und wiederholen Sie die Verarbeitung für den Server nicht erreichbar ist oder langsam zu reagieren.
* Tastatur und Maus Verhaltensweisen sind in der Visual Studio-Paket-Manager-UI verbessert.
* Wir unterstützen jetzt die neuesten `project.json` Schema in DNX.

## <a name="breaking-changes"></a>Die Lauffähigkeit der Anwendung beeinträchtigende Änderungen

* Paket-Versionsnummern sind jetzt in das Format normalisiert *wichtigen*. *kleinere*. *Patch für*-*Vorabversion* aller Haupt-und Nebenversionsnummer und Patchen werden als ganze Zahlen behandelt, und legen Sie alle führenden Nullen (0).  Diese Informationen als Zeichenfolge behandelt, und keine Änderungen angewendet werden. Diese Nummern werden durch die NuGet-Clients und bei der Suche der nuget.org-Dienstes in Abfragen verwendet.  Weitere Informationen finden Sie in der NuGet Docs unter [Vorabversion](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Bekannte Probleme

* **Problem:** Windows 10 v1511 treten möglicherweise Probleme oder sogar eine Visual Studio-Absturzes mit Powershell in Visual Studio in den folgenden Szenarien:
    * Installieren / Deinstallieren von Paketen mit ps1 / ps1-Skripts
    * Laden von Projekten, die ein Skript init.ps1 (z. B. EntityFramework) aufweisen
    * Veröffentlichen von Webinhalten

* **Problemumgehung:** stellen Sie sicher, dass die Installation der Windows 10 die neuesten Patches angewendet, Expecially Januar 2016 (KB 3124263) oder ein neueres Update verfügt.  Weitere Informationen finden Sie auf [GitHub-Problem #1638](http://github.com/nuget/home/issues/1638)

* **Problem:** NuGet v2-Protokollumleitungen sind defekt
Benutzerdefinierte NuGet-Repositorys, die Anforderungen an einen alternativen Host umleiten, beachten die Umleitungsanforderung nicht.
* **Problemumgehung:** um dieses Problem zu umgehen, konfigurieren Sie den paketrepository-URI in den Einstellungen so, dass auf den Standort des umgeleiteten Servers verweist.
Weitere Informationen finden Sie unter [GitHub Pull-Anforderung #387](https://github.com/NuGet/NuGet.Client/pull/387).

Wir weiterhin Probleme auf unserer GitHub-Problemliste zu verfolgen, die sich am befinden: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)