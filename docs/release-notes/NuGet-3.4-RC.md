---
title: Anmerkungen zu dieser Version von nuget 3,4-RC
description: Anmerkungen zu dieser Version von nuget 3,4 RC, einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780238"
---
# <a name="nuget-34-rc-release-notes"></a>Anmerkungen zu dieser Version von nuget 3,4-RC

Anmerkungen zu dieser [Version von nuget 3,3](../release-notes/nuget-3.3.md)  |  [Anmerkungen zu dieser Version von nuget 3,4](../release-notes/nuget-3.4.md)

Nuget 3,4-RC wurde am 2016 3. März mit Visual Studio 2015 Update 2 RC veröffentlicht und mit einigen wenigen Grundsätzen erstellt:

* Plattformübergreifende Unterstützung
* Leistungsverbesserungen
* Kleinere Verbesserung der Benutzeroberfläche

In dieser RC-Version sind die folgenden Features verfügbar, die für die endgültige Version 3,4 geplant sind.

## <a name="new-features"></a>Neue Funktionen

* Nuget-Clients unterstützen jetzt gzip-Inhalts Codierung aus Depots.
* Unterstützung für pdsb von Paketen in xproj-Projekten
* Unterstützung für IOS-und Android-Buildvorgänge im contentfiles-Element
* Unterstützung für die FrameworkMoniker netstandard und netstandardapp

## <a name="new-user-interface-features"></a>Neue Benutzeroberflächen Features

* Bedeutende Leistungsverbesserungen vor allem auf den Registerkarten installiert, Updates und konsolidiert
* Registerkarten "installiert" und "Updates" sind nun alphabetisch sortiert
* Die Schaltfläche "Aktualisieren" wurde hinzugefügt, die die Aktualisierung einer Suche ermöglicht

## <a name="updates-and-improvements"></a>Updates und Verbesserungen

* Pakete, auf die in verwiesen wird und die eine unverankerte `project.json` Version aufweisen, werden bei jedem Build nicht aktualisiert Stattdessen werden Sie nur aktualisiert, wenn Sie zum Wiederherstellen, bereinigen, Neuerstellen oder ändern gezwungen werden `project.json` .
* nuget.org-Repository-Quellen werden nicht mehr in einer Projekt Konfiguration erzwungen, wenn Sie die nuget-Konfigurations Benutzeroberfläche verwenden.
* Mit nuget werden Pakete nicht mehr in freigegebenen Projekten wieder hergestellt, und es wird keine Sperrdatei geschrieben.
* Wir haben den Netzwerkfehler verbessert und die Verarbeitung für nicht erreichbare oder langsame Server erneut versucht.
* Tastatur-und Maus Verhalten werden in der Visual Studio-Benutzeroberfläche des Paket-Managers verbessert.
* Wir unterstützen jetzt das aktuellste `project.json` Schema in DNX.

## <a name="known-issues"></a>Bekannte Probleme

Wir verfolgen weiterhin Probleme in unserer GitHub-Liste mit Problemen, die unter folgenden Themen zu finden sind: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)