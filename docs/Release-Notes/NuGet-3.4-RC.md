---
title: NuGet 3.4-RC-Versionsanmerkungen | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 3.4 RC einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet 3.4 RC-versionsanmerkungen, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 749068683d6e2a3fd9dd29c69d9ff50137acdd46
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-34-rc-release-notes"></a>NuGet 3.4-RC-Versionsanmerkungen

[Anmerkungen zur Version des NuGet-3.3](../release-notes/nuget-3.3.md) | [NuGet 3.4-Versionshinweise](../release-notes/nuget-3.4.md)

NuGet 3.4-RC am 3. März 2016 zusammen mit Visual Studio 2015 Update 2 RC veröffentlicht wurde und mit wenigen Grundsätze in Köpfen erstellt wurde:

* Plattformübergreifende Unterstützung
* Leistungsverbesserungen
* Kleinere Verbesserungen der Benutzeroberfläche

Die folgenden Funktionen stehen in dieser RC mit mehr für die 3.4 endgültige Version geplant wurde.

## <a name="new-features"></a>Neue Funktionen

* NuGet-Clients unterstützen jetzt Gzip-inhaltscodierung von Repositorys
* Unterstützung für die PDB-Dateien von Paketen in Xproj-Projekten
* Unterstützung für IOS- und Android-Buildvorgänge im inhaltsdateienelement
* Unterstützung für die netstandard- und Netstandardapp-frameworkMoniker

## <a name="new-user-interface-features"></a>Neue Features der Benutzeroberfläche

* Signifikante leistungsverbesserungen besonders auf den Registerkarten installiert, Updates und konsolidieren
* Installiert und Updates Registerkarten sind jetzt alphabetisch sortiert
* Schaltfläche "Aktualisieren", die eine zu aktualisierende-Suche erlaubt hinzugefügt

## <a name="updates-and-improvements"></a>Updates und Verbesserungen

* Pakete, die auf die verwiesen wird `project.json` , auf denen eine Gleitkommazahl-Version wird nicht auf jedem Build aktualisieren. Stattdessen werden sie aktualisieren nur, wenn Sie gezwungen, wiederherzustellen, bereinigen, neu erstellen oder ändern Sie `project.json`.
* Bei Verwendung der NuGet-Konfigurations-UI nicht mehr NuGet.org Repository Quellen in einer Projektkonfiguration gezwungen.
* NuGet nicht mehr wiederhergestellt Pakete in gemeinsam genutzte Projekte noch eine Sperrdatei schreibt.
* Wir haben Netzwerkausfall verbessert, und wiederholen Sie die Verarbeitung für den Server nicht erreichbar ist oder langsam zu reagieren.
* Tastatur und Maus Verhaltensweisen sind in der Visual Studio-Paket-Manager-UI verbessert.
* Wir unterstützen jetzt die neuesten `project.json` Schema in DNX.

## <a name="known-issues"></a>Bekannte Probleme

Wir weiterhin Probleme auf unserer GitHub-Problemliste zu verfolgen, die sich am befinden: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)