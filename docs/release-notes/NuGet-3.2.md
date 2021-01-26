---
title: Anmerkungen zu dieser Version von nuget 3,2
description: Anmerkungen zu dieser Version von nuget 3,2 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 38a56b1572770b02ff09135a3b0290742ca80f41
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780304"
---
# <a name="nuget-32-release-notes"></a>Anmerkungen zu dieser Version von nuget 3,2

Anmerkungen zu dieser [Version von nuget 3,2-RC](../release-notes/nuget-3.2-RC.md)  |  [Anmerkungen zu dieser Version von nuget 3.2.1](../release-notes/nuget-3.2.1.md)

Nuget 3,2 wurde am 16. September 2015 als Sammlung von Verbesserungen und Korrekturen für die Version 3.1.1 veröffentlicht und ist sowohl in [Dist.nuget.org](http://dist.nuget.org/index.html) als auch in der [Visual Studio Gallery](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015)verfügbar.

## <a name="new-features"></a>Neue Funktionen

* Projekte, die sich im selben Ordner befinden, können jetzt verschiedene `project.json` Dateien in diesem Ordner aufweisen, die für jedes projektspezifisch sind.  Benennen Sie die Datei für jedes Projekt, `project.json` `{ProjectName}.project.json` und nuget wird diese Konfiguration für jedes Projekt entsprechend bevorzugen.  Dies wird nur mit installiertem Windows 10 Tools v 1.1 unterstützt:  [1102](https://github.com/NuGet/Home/issues/1102)
* Nuget-Clients unterstützen die Angabe einer globalen NUGET_PACKAGES-Umgebungsvariablen, um den Speicherort des freigegebenen globalen Paket Ordners anzugeben, der in `project.json` verwalteten Projekten mit Windows 10 Tools v 1.1 verwendet wird.

## <a name="command-line-updates"></a>Aktualisierungen der Befehlszeile

Dies ist die erste Version des nuget.exe Clients, der die nuget-V3-Server unterstützt und Pakete für Projekte wiederherstellt, die mit einer Datei verwaltet werden `project.json` .

Es gab eine Reihe von authentifizierten Feed-Problemen, die in dieser Version behoben wurden, um Interaktionen mit dem Client zu verbessern.

* Bei der Installation/Wiederherstellung werden nur Anmelde Informationen für die anfängliche Anforderung an den authentifizierten Feed gesendet- [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Der Push-Befehl löst keine Anmelde Informationen aus der Konfiguration aus- [1248](https://github.com/NuGet/Home/issues/1248)
* Benutzer-Agent und Header werden nun an nuget-Repository übermittelt, um die Statistik Nachverfolgung zu unterstützen: [929](https://github.com/NuGet/Home/issues/929)

Wir haben eine Reihe von Verbesserungen vorgenommen, um Netzwerkausfälle bei der Arbeit mit einem Remote-nuget-Repository besser zu behandeln:

* Verbesserte Fehlermeldungen, wenn keine Verbindung mit Remote Feeds hergestellt werden kann- [1238](https://github.com/NuGet/Home/issues/1238)
* Der nuget-Wiederherstellungs Befehl wurde korrigiert, um 1 ordnungsgemäß zurückzugeben, wenn ein Fehlerzustand auftritt: [1186](https://github.com/NuGet/Home/issues/1186)
* Wiederholen Sie jetzt alle 200 MS Netzwerkverbindungen für maximal fünf Versuche im Fall von http 5xx-Fehlern- [1120](https://github.com/NuGet/Home/issues/1120)
* Verbesserte Behandlung von Server Umleitungs Antworten während eines Push-Befehls- [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` unterstützt jetzt entweder die URL oder den Repository-Namen aus Nuget.Config als Argument- [1046](https://github.com/NuGet/Home/issues/1046)
* Fehlende Pakete, die während einer Wiederherstellung nicht in einem Repository gespeichert wurden, werden jetzt als Fehler und nicht als Warnungen [1038](https://github.com/NuGet/Home/issues/1038) gemeldet.
* Korrigierte multipartwebrequest-Behandlung von \r\n für UNIX/Linux-Szenarien: [776](https://github.com/NuGet/Home/issues/776)

Es gibt eine Reihe von Korrekturen für Probleme mit verschiedenen Befehlen:

* Der Push-Befehl führt einen get-Befehl nicht mehr vor einem Put-Befehl für eine Paketquelle aus- [1237](https://github.com/NuGet/Home/issues/1237)
* Der List-Befehl wiederholt nicht mehr die Versionsnummern- [1185](https://github.com/NuGet/Home/issues/1185)
* Pack mit dem Argument-Build unterstützt jetzt c# 6,0- [1107](https://github.com/NuGet/Home/issues/1107) ordnungsgemäß.
* Korrigierte Probleme beim Packen eines F #-Projekts, das mit Visual Studio 2015- [1048](https://github.com/NuGet/Home/issues/1048) erstellt wurde
* Restore Now No-OPS, wenn bereits Pakete vorhanden sind- [1040](https://github.com/NuGet/Home/issues/1040)
* Verbesserte Fehlermeldungen, wenn die `packages.config` Datei falsch formatiert ist: [1034](https://github.com/NuGet/Home/issues/1034)
* Restore-Befehl mit dem Schalter "-SolutionDirectory" korrigiert, um mit relativen Pfaden zu arbeiten- [992](https://github.com/NuGet/Home/issues/992)
* Verbesserter aktualisierter Befehl zur Unterstützung des Lösungs weiten Updates- [924](https://github.com/NuGet/Home/issues/924)

Eine umfassende Liste der Probleme, die in dieser Version behoben wurden, finden Sie im nuget GitHub [-Befehlszeilen Meilenstein](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).

## <a name="visual-studio-extension-updates"></a>Updates für Visual Studio-Erweiterungen

### <a name="new-features-in-visual-studio"></a>Neue Features in Visual Studio

* Dem Projektmappen-Explorer auf dem Projektmappenknoten wurde ein neues Kontextmenü Element hinzugefügt, das das Wiederherstellen von Paketen ermöglicht, ohne die Projekt Mappe zu entwickeln ([1274](https://github.com/NuGet/Home/issues/1274)).

![Neues Kontextmenü Element "Pakete wiederherstellen"](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Updates und Korrekturen in Visual Studio

Die Korrekturen für authentifizierte Feeds wurden in der Erweiterung ebenfalls eingeführt und behoben.  Die folgenden Authentifizierungs Elemente wurden ebenfalls in der Erweiterung adressiert:

* Ordnungsgemäße Behandlung von authentifizierten nuget V3-Feeds anstelle von V2-authentifizierten Feeds- [1216](https://github.com/NuGet/Home/issues/1216)
* Korrigierte Anforderung für Anmelde Informationen für die Authentifizierung in Projekten mit `project.json` und Kommunikation mit V2-Feeds- [1082](https://github.com/NuGet/Home/issues/1082)

Die Netzwerk Konnektivität hat sich auf die Benutzeroberfläche in Visual Studio ausgewirkt, und wir haben dies mit den folgenden Korrekturen behoben:

* Verbesserte Wartung des lokalen Caches der Paketversionen- [1096](https://github.com/NuGet/Home/issues/1096)
* Das Fehler Verhalten beim Herstellen einer Verbindung mit einem v3-Feed wurde geändert, um nicht mehr zu versuchen, ihn als V2-Feed zu behandeln- [1253](https://github.com/NuGet/Home/issues/1253)
* Verhindern von Installationsfehlern bei der Installation eines Pakets mit mehreren Paketquellen: [1183](https://github.com/NuGet/Home/issues/1183)

Wir haben die Handhabung von Interaktionen mit Buildvorgängen verbessert:

* Projekt Erstellung wird nun fortgesetzt, wenn die Wiederherstellung von Paketen für ein einzelnes Projekt fehlschlägt- [1169](https://github.com/NuGet/Home/issues/1169)
* Wenn Sie ein Paket in ein Projekt installieren, das von einem anderen Projekt in der Projekt Mappe abhängt, erzwingen Sie eine Lösungs Neuerstellung- [981](https://github.com/NuGet/Home/issues/981)
* Fehlerhafte Paketinstallation korrigiert, um Änderungen an einem Projekt ordnungsgemäß zurückzusetzen- [1265](https://github.com/NuGet/Home/issues/1265)
* Unbeabsichtigtes Entfernen des `developmentDependency` Attributs für ein Paket in `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263) korrigiert
* Für Aufrufe von wird `install.ps1` jetzt ein ordnungsgemäßes `$package.AssemblyReferences` Objekt übermittelt- [1245](https://github.com/NuGet/Home/issues/1245)
* Verhindert nicht mehr das Deinstallieren von Paketen in UWP-Projekten, während sich das Projekt in einem ungültigen Zustand befindet: [1128](https://github.com/NuGet/Home/issues/1128)
* Projektmappen, die eine Mischung aus `packages.config` -und-Projekten enthalten, `project.json` werden jetzt ordnungsgemäß erstellt, ohne dass ein zweiter build1122 Vorgang [](https://github.com/NuGet/Home/issues/1122)
* Ordnungsgemäße Suche nach app.config Dateien, wenn Sie verknüpft sind oder sich in einem anderen Ordner befinden: [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* UWP-Projekte können nun nicht aufgelistete Pakete installieren- [1109](https://github.com/NuGet/Home/issues/1109)
* Die Paket Wiederherstellung ist jetzt zulässig, während sich eine Projekt Mappe nicht in einem gespeicherten Zustand befindet: [1081](https://github.com/NuGet/Home/issues/1081)

Die Verarbeitung von Updates an Konfigurationsdateien wurde korrigiert:

* Entfernen einer aus einem Paket übermittelten Zieldatei in nachfolgenden Builds eines `project.json` verwalteten Projekts: [1288](https://github.com/NuGet/Home/issues/1288)
* Ändern Sie Nuget.Config Dateien nicht mehr während des ASP.net 5-Projektmappenbuilds- [1201](https://github.com/NuGet/Home/issues/1201)
* Die Einschränkung der zulässigen Versionen wird während des Paket Updates nicht mehr geändert- [1130](https://github.com/NuGet/Home/issues/1130)
* Sperrdateien bleiben während des Builds gesperrt- [1127](https://github.com/NuGet/Home/issues/1127)
* Jetzt ändern `packages.config` und nicht umschreiben während der Updates- [585](https://github.com/NuGet/Home/issues/585)

Interaktionen mit der TFS-Quell Code Verwaltung werden verbessert:

* Nicht mehr fehlerhafte Installationen für Pakete, die an TFS gebunden sind- [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Korrigierte nuget-Benutzeroberfläche, um TFS 2013-Integration zuzulassen- [1071](https://github.com/NuGet/Home/issues/1071)
* Korrigierte Verweise auf Pakete, die ordnungsgemäß wieder hergestellt werden, stammen aus dem [1004](https://github.com/NuGet/Home/issues/1004) Ordner "Packages"

Außerdem haben wir die folgenden Elemente verbessert:

* Ausführlichkeit von Protokollmeldungen für `project.json` verwaltete Projekte reduziert- [1163](https://github.com/NuGet/Home/issues/1163)
* Die installierte Version eines Pakets wird nun ordnungsgemäß auf der Benutzeroberfläche angezeigt: [1061](https://github.com/NuGet/Home/issues/1061)
* Pakete mit Abhängigkeits Bereichen, die in der nuspec-Spezifikation angegeben sind, verfügen jetzt über vorab Versionen dieser Abhängigkeiten, die für eine stabile Paketversion installiert sind: [1304](https://github.com/NuGet/Home/issues/1304)

Eine umfassende Liste der Probleme, die für die Visual Studio-Erweiterung behoben wurden, finden Sie im nuget GitHub [3,2-Meilenstein](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2) .

## <a name="known-issues"></a>Bekannte Probleme

Wir verfolgen weiterhin Probleme in unserer GitHub-Liste mit Problemen, die unter folgenden Themen zu finden sind: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)