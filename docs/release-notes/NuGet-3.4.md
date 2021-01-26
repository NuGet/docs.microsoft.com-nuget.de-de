---
title: Anmerkungen zu dieser Version von nuget 3,4
description: Anmerkungen zu dieser Version von nuget 3,4 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776420"
---
# <a name="nuget-34-release-notes"></a>Anmerkungen zu dieser Version von nuget 3,4

Anmerkungen zu dieser [Version von nuget 3,4-RC](../release-notes/nuget-3.4-RC.md)  |  [Anmerkungen zu nuget-Version 3.4.1](../release-notes/nuget-3.4.1.md)

Nuget 3,4 wurde als Teil von Visual Studio 2015 Update 2 und Visual Studio 15 Preview 2016 veröffentlicht und mit einigen wenigen Grundsätzen erstellt:

* Plattformübergreifende Unterstützung
* Leistungsverbesserungen
* Kleinere Verbesserung der Benutzeroberfläche

Die folgenden Features wurden bereits in der RC-Version hinzugefügt und wurden für die Version 3,4 aktualisiert oder abgeschlossen:

## <a name="new-features"></a>Neue Funktionen

* Nuget-Clients unterstützen jetzt gzip-Inhalts Codierung aus Depots.
* Unterstützung für pdsb von Paketen in xproj-Projekten
* Unterstützung für IOS-und Android-Buildvorgänge im contentfiles-Element
* Unterstützung für die FrameworkMoniker netstandard und netstandardapp

## <a name="new-user-interface-features"></a>Neue Benutzeroberflächen Features

* Bedeutende Leistungsverbesserungen vor allem auf den Registerkarten installiert, Updates und konsolidiert
* Die Quelle "alle Paketquellen" ist für die ordnungsgemäße Zusammenführung der Suchergebnisse verfügbar.
* Registerkarten "installiert" und "Updates" sind nun alphabetisch sortiert
* Die Schaltfläche "Aktualisieren" wurde hinzugefügt, die die Aktualisierung einer Suche ermöglicht
* Neueste Buildoptionen am Anfang der Versions Liste

## <a name="updates-and-improvements"></a>Updates und Verbesserungen

* Pakete, auf die in verwiesen wird und die eine unverankerte `project.json` Version aufweisen, werden bei jedem Build nicht aktualisiert Stattdessen werden Sie nur aktualisiert, wenn Sie zum Wiederherstellen, bereinigen, Neuerstellen oder ändern gezwungen werden `project.json` .
* nuget.org-Repository-Quellen werden nicht mehr in einer Projekt Konfiguration erzwungen, wenn Sie die nuget-Konfigurations Benutzeroberfläche verwenden.
* Mit nuget werden Pakete nicht mehr in freigegebenen Projekten wieder hergestellt, und es wird keine Sperrdatei geschrieben.
* Wir haben den Netzwerkfehler verbessert und die Verarbeitung für nicht erreichbare oder langsame Server erneut versucht.
* Tastatur-und Maus Verhalten werden in der Visual Studio-Benutzeroberfläche des Paket-Managers verbessert.
* Wir unterstützen jetzt das aktuellste `project.json` Schema in DNX.

## <a name="breaking-changes"></a>Aktuelle Änderungen

* Paket Versionsnummern werden nun in das Format " *Major*" normalisiert. *neben* Version. *Patch* - *vorab* Version   Alle Haupt-, neben-und patchvorgänge werden als ganze Zahlen behandelt, und alle führenden Nullen werden gelöscht.  Die Vorabinformationen werden als Zeichenfolge behandelt, und es werden keine Änderungen darauf angewendet. Diese Zahlen werden in Abfragen von den nuget-Clients und der vom nuget.org-Dienst bereitgestellten Suche verwendet.  Weitere Informationen finden Sie in der nuget-Dokumentation unter [vorab Versionen](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Bekannte Probleme

* **Problem:** Windows 10 v1511 Benutzer haben möglicherweise Probleme oder sogar einen Visual Studio-Absturz mit PowerShell in Visual Studio in den folgenden Szenarien:
    * Installieren/Deinstallieren von Paketen mit install.ps1/uninstall.ps1-Skripts
    * Laden von Projekten mit einem init.ps1 Skript (wie z. b. EntityFramework)
    * Veröffentlichen von Webinhalten

* Problem **Umgehung:** Stellen Sie sicher, dass auf Ihrer Windows 10-Installation die neuesten Patches angewendet wurden, nämlich der Januar 2016 (KB 3124263) oder ein späteres Update.  Weitere Informationen finden Sie unter [GitHub-Problem #1638](http://github.com/nuget/home/issues/1638)

* **Problem:** NuGet v2-Protokollumleitungen sind defekt
Benutzerdefinierte NuGet-Repositorys, die Anforderungen an einen alternativen Host umleiten, beachten die Umleitungsanforderung nicht.
* Problem **Umgehung:**  Um dieses Problem zu umgehen, konfigurieren Sie den Paketrepository-URI in den Einstellungen so, dass er auf den umgeleiteten Serverstandort verweist
Weitere Informationen finden Sie unter [GitHub Pull Request #387](https://github.com/NuGet/NuGet.Client/pull/387).

Wir verfolgen weiterhin Probleme in unserer GitHub-Liste mit Problemen, die unter folgenden Themen zu finden sind: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)