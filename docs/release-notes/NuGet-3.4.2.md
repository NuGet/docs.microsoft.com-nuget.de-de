---
title: Anmerkungen zu NuGet 3.4.2
description: Anmerkungen zu dieser Version für die Einbindung von NuGet 3.4.2 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549150"
---
# <a name="nuget-342-release-notes"></a>Anmerkungen zu NuGet 3.4.2

[Anmerkungen zu NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [Anmerkungen zu NuGet 3.4.3](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2 wurde am 8. April 2016, mehrere Probleme zu beheben, die in den 3.4 und 3.4.1 identifiziert wurden veröffentlicht freizugeben.

## <a name="nugetexe-342-rc-is-now-available"></a>NuGet.exe 3.4.2 RC ist jetzt verfügbar

Sie können den Release Candidate von nuget.exe 3.4.2 [hier](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Updates und Verbesserungen

* Wir haben die Leistung von Updates in ein bestimmtes Szenario, erheblich verbessert, in dem Updates für Pakete mit Tiefen Abhängigkeitsdiagrammen eine sehr lange gedauert, und nicht reagiert Visual Studio.
* NuGet-Wiederherstellung ohne Netzwerkdatenverkehr ist 2,5-Mal-3-Mal schneller in Visual Studio.
* Zusätzlich zu dieser Änderung haben wir ein Problem behoben, in denen wurden wir das Netzwerk erreichen zweimal, wenn in der Visual Studio-Benutzeroberfläche zählen das Update abgerufen. Dies war für einige Erfahrung im 3.4/3.4.1 Timeout Probleme Kunden teilweise verantwortlich.
* Unterstützung für die Einstellung für "no_proxy"

## <a name="fixes"></a>Fehlerbehebungen

* Wurde "NuGet.org" Quelle nach der Aktualisierung auf 3.4.1 im NuGet-Einstellungen oder der Konfiguration fehlt behoben ein Problem.
* Ein Problem behoben, in dem eine Änderung zur Groß-und Kleinschreibung zu FindPackagesById 3.4.1 Artifactory unterbrochen.
* Ein Problem mit FIPS, die aufgrund von Fehlern bei der NuGet-Wiederherstellung von nuget.exe korrigiert.
* Korrektur eines Absturzes, beim Durchsuchen von Datenquellen mit ungültige Symbol-URL.
* Korrigiert: Probleme mit dem Zusammenführen von Versionen und Einträge aus "Alle Quellen".

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Bekannte Probleme in 3.4.2 X86-Windows-Befehlszeile (RC)

Diese Probleme werden die Anfang der nächsten Woche vor der stoßen wir auf die RTM-Version behoben werden.

*  Ausgeführte Nuget-Wiederherstellung in einer Projektmappe fehl, wenn in einer niedrigeren Ordnerhierarchie als die Projektdateien die Projektmappendatei platziert wird.
*  Ausführen von Nuget-Delete-Befehl für ein Paket mit dem V2-Feed schlägt fehl. Verwenden Sie stattdessen V3-Feeds.


Die vollständige Liste der Korrekturen und Verbesserungen in dieser Version, sehen Sie sich die Liste der Probleme [hier](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).