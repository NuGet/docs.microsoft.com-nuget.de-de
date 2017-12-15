---
title: Anmerkungen zur Version des NuGet-3.2 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 70316f35-f046-4f72-98e0-736de172e918
description: "Versionshinweise für NuGet 3.2 bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design einschließlich."
keywords: "NuGet-3.2 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 364a1ac62af25351e78df0b9a506f0919fc8fb61
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-32-release-notes"></a>3.2 NuGet-Versionshinweise

[NuGet-3.2 RC-Versionsanmerkungen](../release-notes/nuget-3.2-RC.md) | [NuGet 3.2.1-Versionshinweise](../release-notes/nuget-3.2.1.md)

NuGet-3.2 wurde veröffentlicht 16 September 2015 als eine Sammlung von Verbesserungen und Fehlerbehebungen für die 3.1.1 freigeben und steht über beide [dist.nuget.org](http://dist.nuget.org/index.html) und [Visual Studio Gallery](https://visualstudiogallery.msdn.microsoft.com/5d345edc-2e2d-4a9c-b73b-d53956dc458d?SRC=Home).

## <a name="new-features"></a>Neue Funktionen

* Projekte, die in demselben Ordner befinden, können jetzt weisen unterschiedliche `project.json` Dateien in diesem Ordner, die spezifisch für jedes Projekt.  Jedes Projekt ein, und die `project.json` Datei `{ProjectName}.project.json` NuGet Voreinstellung, um die Konfiguration für jedes Projekt entsprechend bereitstellen.  Dies wird nur unterstützt, mit Windows 10-Tools, v1. 1 installiert - [1102](https://github.com/NuGet/Home/issues/1102)
* Angeben eines eine globale NUGET_PACKAGES-Umgebungsvariable zum Angeben des Speicherorts des Ordners, gemeinsam genutzten globalen Pakete NuGet-Clients unterstützt `project.json` verwaltete Projekte mit Windows 10-Tools v1. 1.

## <a name="command-line-updates"></a>Befehlszeilen-updates

Dies ist die erste Version des Clients nuget.exe, die NuGet-v3-Server unterstützt und Wiederherstellen von Paketen für Projekte mit verwaltet eine `project.json` Datei.

Gab es eine Reihe von authentifizierten feed Problemen, die in dieser Version zur Verbesserung der Interaktionen mit dem Client behoben wurden.

* Installieren Sie / Wiederherstellung Interaktionen übermitteln nur Anmeldeinformationen für die ursprüngliche Anforderung an den authentifizierten Feed - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Push-Befehl löst keine Anmeldeinformationen aus der Konfiguration - [1248](https://github.com/NuGet/Home/issues/1248)
* Benutzer-Agent und Header werden jetzt auf NuGet-Repositorys zur Hilfe bei der nachverfolgung von Statistiken - gesendet [929](https://github.com/NuGet/Home/issues/929)

Wir haben eine Reihe von Verbesserungen, Netzwerkausfälle besser zu behandeln, bei dem Versuch, die mit einem Remoteserver NuGet-Repository zu arbeiten:

* Verbesserte Fehlermeldungen, wenn keine Verbindung zum remote-Feeds - [1238](https://github.com/NuGet/Home/issues/1238)
* NuGet Restore-Befehl ordnungsgemäß 1 zurückgeben, wenn ein Fehlerzustand auftritt - korrigiert [1186](https://github.com/NuGet/Home/issues/1186)
* Netzwerkverbindungen jetzt und wiederholen Sie dann jede 200 ms für maximal 5 Versuche eines HTTP-5xx - [1120](https://github.com/NuGet/Home/issues/1120)
* Verbesserte Behandlung von Umleitung Serverantworten während eines Befehls Push - [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source`unterstützt nun die URL oder Repository namens "NuGet.config" als Argument - [1046](https://github.com/NuGet/Home/issues/1046)
* Fehlender Pakete, die während einer Wiederherstellung auf einem Repository nicht gefunden wurden, werden jetzt als Fehler anstatt Warnungen gemeldet [1038](https://github.com/NuGet/Home/issues/1038)
* Korrigiert Multipartwebrequest Behandlung von \r\n für Unix/Linux-Szenarien – [776](https://github.com/NuGet/Home/issues/776)

Es gibt eine Reihe von Fehlerbehebungen für Probleme mit verschiedenen Befehle aus:

* Befehl "Push" ist nicht mehr einen GET-Befehl vor einen Put-Vorgang für eine Paketquelle - [1237](https://github.com/NuGet/Home/issues/1237)
* Auflisten (Befehl) wird nicht mehr wiederholt Versionsnummern - [1185](https://github.com/NuGet/Home/issues/1185)
* Paket mit dem - Build-Argument jetzt ordnungsgemäß unterstützt c# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)
* Korrigierte Probleme, die bei dem Versuch, ein f#-Projekt-Paket erstellt, mit Visual Studio 2015 - [1048](https://github.com/NuGet/Home/issues/1048)
* Stellen Sie jetzt keine-Ops wieder her, wenn Pakete bereits vorhanden: [1040](https://github.com/NuGet/Home/issues/1040)
* Verbesserte Fehlermeldungen, wenn `packages.config` Datei ist falsch formatiert - [1034](https://github.com/NuGet/Home/issues/1034)
* Restore-Befehl mit dem Switch - SolutionDirectory zur Bearbeitung von relativer Pfaden - korrigiert [992](https://github.com/NuGet/Home/issues/992)
* Aktualisierte Befehl aus, um die Projektmappe-weiten Update - Unterstützung verbessert [924](https://github.com/NuGet/Home/issues/924)

Eine vollständige Liste der Probleme in dieser Version finden Sie in der NuGet-GitHub [Befehlszeilen Meilenstein](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).

## <a name="visual-studio-extension-updates"></a>Updates für Visual Studio-Erweiterung

### <a name="new-features-in-visual-studio"></a>Neue Funktionen in Visual Studio

* Im Projektmappen-Explorer auf den Projektmappenknoten, die Pakete, die wiederhergestellt werden, ohne Erstellen der Projektmappe ermöglicht eine neue Kontextmenüelement hinzugefügt wurde ([1274](https://github.com/NuGet/Home/issues/1274)).

![Neue "Restore-Pakete" Kontextmenüelement](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Updates und Korrekturen in Visual Studio

Fehlerbehebungen für authentifizierten Feeds wurden Rollup wird erstellt und in der Erweiterung auch behandelt.  Die folgenden Elemente für die Authentifizierung wurden auch in der Erweiterung adressiert werden:

* Jetzt ordnungsgemäß behandeln v3 NuGet-Feeds ordnungsgemäß authentifiziert statt als v2 Feeds - authentifiziert [1216](https://github.com/NuGet/Home/issues/1216)
* Korrigierte Anforderung Authentifizierungsinformationen in Projekten, die mit `project.json` und zur Kommunikation mit v2-Feeds - [1082](https://github.com/NuGet/Home/issues/1082)

Netzwerkkonnektivität hatte die Benutzeroberfläche in Visual Studio betroffen, und wir dies mit der folgenden Updates behandelt:

* Verbessert die Wartung des lokalen Caches Paketversionen - [1096](https://github.com/NuGet/Home/issues/1096)
* Das Fehlerverhalten geändert, beim Verbinden mit einem v3-feed auf nicht mehr versucht, diese als Feed v2 - behandeln [1253](https://github.com/NuGet/Home/issues/1253)
* Jetzt verhindert Fehler installieren Sie beim Installieren eines Pakets mit mehreren Paketquellen - [1183](https://github.com/NuGet/Home/issues/1183)

Es verbessert die Behandlung von Interaktionen mit Buildvorgängen:

* Nun zum Erstellen von Projekten aus, wenn Pakete wiederherstellen für ein einzelnes Projekt fehlschlägt - fortsetzen [1169](https://github.com/NuGet/Home/issues/1169)
* Installieren ein Paket in ein Projekt, das von einem anderen Projekt in der Projektmappe abhängen ist erzwingt Lösung Rebuild - [981](https://github.com/NuGet/Home/issues/981)
* Fehlerhafte Paket installiert ordnungsgemäß Änderungen zu einem Projekt - korrigiert [1265](https://github.com/NuGet/Home/issues/1265)
* Versehentliche Entfernen von korrigiert die `developmentDependency` Attribut für ein Paket in `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Aufrufe von `install.ps1` verfügen jetzt über eine echte `$package.AssemblyReferences` übergebene - Objekt [1245](https://github.com/NuGet/Home/issues/1245)
* Verhindert ohne mehr die heraufstufung von Paketen in uwp-Projekten deinstalliert, während das Projekt in einem fehlerhaften Zustand - ist [1128](https://github.com/NuGet/Home/issues/1128)
* Enthält eine Mischung aus Lösungen `packages.config` und `project.json` Projekte werden jetzt ordnungsgemäß ohne ein zweites erstellt Buildvorgangs - [1122](https://github.com/NuGet/Home/issues/1122)
* App.config-Dateien ordnungsgemäß zu suchen, wenn sie verknüpft sind, oder befindet sich in einem anderen Ordner - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* Uwp-Projekte können jetzt Installationspakete nicht aufgeführte - [1109](https://github.com/NuGet/Home/issues/1109)
* Paketwiederherstellung ist jetzt zulässig, während eine Lösung nicht in einen gespeicherten Zustand - befindet [1081](https://github.com/NuGet/Home/issues/1081)

Behandlung von Updates für die Konfiguration, die Dateien wurden korrigiert:

* Entfernen nicht mehr eine Targets-Datei aus einem Paket nachfolgender Builds von übermittelt eine `project.json` verwaltetes Projekt - [1288](https://github.com/NuGet/Home/issues/1288)
* Ändern Sie "NuGet.config"-Dateien nicht mehr während ASP.NET 5-Projektmappenbuild - [1201](https://github.com/NuGet/Home/issues/1201)
* Nicht mehr ändern Versionen Einschränkung zulässig, während der paketaktualisierung - [1130](https://github.com/NuGet/Home/issues/1130)
* Sperrdateien jetzt bleiben gesperrt während des Buildvorgangs - [1127](https://github.com/NuGet/Home/issues/1127)
* Jetzt ändern `packages.config` und nicht während eines Updates - umgeschrieben wurde [585](https://github.com/NuGet/Home/issues/585)

Interaktionen mit TFS-quellcodeverwaltung verbessert:

* Installationen für Pakete, die mit TFS - gebunden sind nicht mehr fehlschlagen [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Korrigierte NuGet-Benutzeroberfläche für die Integration von TFS 2013 – ermöglichen [1071](https://github.com/NuGet/Home/issues/1071)
* Verweise auf Pakete, die wiederhergestellt werden, um einen Ordner "Pakete" - ordnungsgemäß stammen korrigiert [1004](https://github.com/NuGet/Home/issues/1004)

Schließlich verbessert wir auch diese Elemente:

* Ausführlichkeit der protokollmeldungen-reduced für `project.json` verwaltete Projekte - [1163](https://github.com/NuGet/Home/issues/1163)
* Jetzt ordnungsgemäß anzeigen von der installierten Version eines Pakets in der Benutzeroberfläche - [1061](https://github.com/NuGet/Home/issues/1061)
* Pakete mit jetzt in ihren Nuspec angegebenen Abhängigkeit-Bereiche haben Vorabversionen solcher Abhängigkeiten installiert, die für eine stabile Paketversion - [1304](https://github.com/NuGet/Home/issues/1304)

Eine vollständige Liste der Probleme für Visual Studio-Erweiterung Sie in der NuGet-GitHub finden [3,2 Meilenstein](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>Bekannte Probleme

Wir weiterhin Probleme auf unserer GitHub-Problemliste zu verfolgen, die sich am befinden: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)