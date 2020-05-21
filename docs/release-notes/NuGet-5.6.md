---
title: Anmerkungen zu dieser Version von nuget 5,6
description: Anmerkungen zu dieser Version von nuget 5,6, einschließlich neuer Features, Fehlerbehebungen und dcrs.
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727806"
---
# <a name="nuget-56-release-notes"></a>Anmerkungen zu dieser Version von nuget 5,6

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version| Verfügbar in .NET SDK(s)|
|:---|:---|:---|
| [**5.6.0**](https://nuget.org/downloads) | [Visual Studio 2019, Version 16.6](https://visualstudio.microsoft.com/downloads/) | [3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Installiert mit Visual Studio 2019 mit .net Core-Arbeitsauslastung

## <a name="summary-whats-new-in-56"></a>Zusammenfassung: Neues in 5,6

* Unterstützung von vorab Paketen mit Gleit Komma Versionen. `Version="*-*"`, `Version="1.*-*"` und ähnlich wie in den neuesten Versionen, einschließlich vorab Versionen, innerhalb des angegebenen Bereichs [#912](https://github.com/NuGet/Home/issues/912)

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

**K**

* `nuget push *.nupkg`schlägt fehl, wenn das snupkg- [#8148](https://github.com/NuGet/Home/issues/8148) nicht vorhanden ist.

* Pack und verschiedene andere Codepfade schlagen nicht abhängig vom Gebiets Schema ab. RegexOptions. CultureInvariant- [#8246](https://github.com/NuGet/Home/issues/8246) verwenden

* Perf: die Spezifikation der GD für entladene Projekt Szenarien sollte nicht in der Vorschau Wiederherstellung geschrieben werden- [#8793](https://github.com/NuGet/Home/issues/8793)

* Wiederherstellung: verbessern der Leistung durch das Zwischenspeichern von Lösungs Abhängigkeits Diagrammen- [#9201](https://github.com/NuGet/Home/issues/9201)

* Die pm-Benutzeroberfläche funktioniert nach der Installation eines Pakets mit der PM-Konsole nicht für SDK-Stil Projekte [#9203](https://github.com/NuGet/Home/issues/9203)

* Eingebettetes Symbol kann nicht in der PM-Benutzeroberfläche mit lokalem paketfeed angezeigt werden, abhängig von/vs \- [#9225](https://github.com/NuGet/Home/issues/9225)

* Nugetversion. tryparameterstrict () sollte "false" zurückgeben, wenn Sie nicht analysiert werden kann [#9255](https://github.com/NuGet/Home/issues/9255)

* `nuget.exe push`Hilfe für `-source` , sollte die Verwendung des Quell namens vorschlagen, nicht die Quell-URL- [#9265](https://github.com/NuGet/Home/issues/9265)

* `dotnet nuget add package SourceUri`erstellt einen ungültigen Standardpaket Quellen Namen- [#9277](https://github.com/NuGet/Home/issues/9277)

* Die Sprachausgabe gibt keine "Suche..."- Meldung beim Wechseln von Registerkarten- [#9307](https://github.com/NuGet/Home/issues/9307)

* Barrierefreiheit: die Farbe des Fokus Rechtecks ist nicht auf die Benutzeroberflächen-Registerkarten im Design "dunkel" [#9336](https://github.com/NuGet/Home/issues/9336)

* die Wiederherstellung von nuget. exe 5,5 mit MSBuild 14 oder niedriger ist nicht möglich [#9458](https://github.com/NuGet/Home/issues/9458)

* In Wiederherstellungs Nachrichten keine Millisekunden-Zeiten protokollieren- [#8977](https://github.com/NuGet/Home/issues/8977)

* Ioutputconsole Async- [#9268](https://github.com/NuGet/Home/issues/9268) erstellen

* Die Auswahl der MSBuild-Version funktioniert in einigen nicht englischen Kulturen schlecht [#9322](https://github.com/NuGet/Home/issues/9322)

* Standardwert für das Format auf `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)

* Perf: restoreoperationlogger weist unnötige Thread Affinität auf [#9288](https://github.com/NuGet/Home/issues/9288)

* Automatisierte Erstellung von Dokumenten für `dotnet nuget` Befehle- [#9146](https://github.com/NuGet/Home/issues/9146)

* Standard Ausführlichkeit sollte die NOOP-Restore- [#8792](https://github.com/NuGet/Home/issues/8792) jedes Projekts nicht melden.

* Unterstützungs `-DependencyVersion` Parameter für `NuGet.exe update` , ähnlich wie bei der Installation von Command- [#7694](https://github.com/NuGet/Home/issues/7694)


**DCRs**

* Anfängliche Unterstützung für .net 5.0-Ziel Framework hinzufügen- [#9584](https://github.com/NuGet/Home/issues/9584)

* Sortieren Sie die Pakete nach ID auf der Registerkarte "Updates" der PM-Benutzeroberfläche- [#9278](https://github.com/NuGet/Home/issues/9278)


**[Liste aller Probleme, die in dieser Version behoben wurden: 5,6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**
