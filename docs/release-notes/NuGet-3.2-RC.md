---
title: Anmerkungen dieser Version von NuGet 3.2 RC
description: Anmerkungen zu NuGet 3.2 RC, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: eafdedc3ad022a6794dbeb390de87d7f317e28f1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551497"
---
# <a name="nuget-32-rc-release-notes"></a>Anmerkungen dieser Version von NuGet 3.2 RC

[Anmerkungen zu NuGet 3.1.1](../release-notes/nuget-3.1.1.md) | [Anmerkungen zu NuGet 3.2](../release-notes/nuget-3.2.md)

NuGet 3.2 Release Candidate wurde veröffentlicht am 2. September 2015 als eine Sammlung von Verbesserungen und Fehlerbehebungen für die 3.1.1 freizugeben.  Darüber hinaus sind die ersten Releases, die zuerst auf das neue "dist.NuGet.org" Repository veröffentlicht werden.

## <a name="new-features"></a>Neue Funktionen

* Projekte, die sich im selben Ordner befinden, können jetzt haben andere `project.json` Dateien in diesem Ordner für jedes Projekt spezifisch.  Benennen Sie für jedes Projekt, das `project.json` Datei `{ProjectName}.project.json` und NuGet ordnungsgemäß verweist und Sie entsprechend die, dass der Inhalt für jedes Projekt verwendet.  Dies unterstützt ein neues Feature [1102](https://github.com/NuGet/Home/issues/1102)
* `NuGet.Config` unterstützt jetzt eine GlobalPackagesFolder als relativer Pfad - [1062](https://github.com/NuGet/Home/issues/1062)

## <a name="command-line-updates"></a>Befehlszeilen-updates

Dies ist die erste Version des nuget.exe-Clients, die die NuGet-v3-Server unterstützt und Wiederherstellen von Paketen für Projekte mit verwaltet eine `project.json` Datei.

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a>Gab es eine Anzahl von authentifizierten feed behandelten Probleme werden in dieser Version um die Interaktionen mit dem Client zu verbessern.

* Installation / Wiederherstellung Interaktionen nur Anmeldeinformationen für die ursprüngliche Anforderung an den authentifizierten Feed - übermitteln [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Push-Befehl löst nicht die Anmeldeinformationen aus der Konfiguration - [1248](https://github.com/NuGet/Home/issues/1248)
* Benutzer-Agent und Header werden in NuGet-Repositorys zur nachverfolgung der Statistik - Unterstützung jetzt übermittelt [929](https://github.com/NuGet/Home/issues/929)

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a>Wir haben eine Reihe von Verbesserungen an Netzwerkfehler besser zu behandeln, bei dem Versuch, die Arbeit mit einem Remoterepository von NuGet vorgenommen:

* Verbesserte Fehlermeldungen, wenn keine Verbindung zum remote-Feeds - [1238](https://github.com/NuGet/Home/issues/1238)
* NuGet Restore-Befehl ordnungsgemäß 1 zurückgeben, wenn ein Fehlerzustand auftritt - korrigiert [1186](https://github.com/NuGet/Home/issues/1186)
* Jetzt wiederholen Netzwerkverbindungen alle 200 ms für bis zu 5 Versuche im Fall von HTTP-5xx-Fehlern – [1120](https://github.com/NuGet/Home/issues/1120)
* Verbesserte Behandlung von Umleitung Serverantworten während einer Push-Befehl – [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` unterstützt jetzt entweder "URL" oder "Repository-Namen aus der Datei" NuGet.config "als Argument - [1046](https://github.com/NuGet/Home/issues/1046)
* Fehlende Pakete, die auf ein Repository nicht, während einer Wiederherstellung gefunden wurden werden jetzt als Fehler anstatt Warnungen gemeldet [1038](https://github.com/NuGet/Home/issues/1038)
* Korrigiert Multipartwebrequest Behandlung \r\n für Unix/Linux-Szenarien – [776](https://github.com/NuGet/Home/issues/776)

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a>Es gibt eine Anzahl von Korrekturen für Probleme mit verschiedenen Befehlen:

* Push-Befehl ist nicht mehr vor eines PUT-AUFRUFS für eine Paketquelle - GET [1237](https://github.com/NuGet/Home/issues/1237)
* List-Befehl wird nicht mehr wiederholt Versionsnummern - [1185](https://github.com/NuGet/Home/issues/1185)
* Pack mit dem - Build-Argument jetzt ordnungsgemäß unterstützt C# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)
* Korrigierte Probleme, die versuchen, eine f#-Projekt packen, die mit Visual Studio 2015 – erstellt [1048](https://github.com/NuGet/Home/issues/1048)
* Jetzt keine Funktion wiederherstellen, wenn bereits Pakete vorhanden sind - [1040](https://github.com/NuGet/Home/issues/1040)
* Verbesserte Fehlermeldungen, wenn `packages.config` Datei ist falsch formatiert: [1034](https://github.com/NuGet/Home/issues/1034)
* Befehl "Restore" mit korrigiert `-SolutionDirectory` wechseln Sie zur Arbeit mit relativen Pfade - [992](https://github.com/NuGet/Home/issues/992)
* Aktualisierte Befehl aus, um die Projektmappe-weiten-Update - Unterstützung verbessert [924](https://github.com/NuGet/Home/issues/924)

Eine vollständige Liste der in dieser Release behobenen Problemen finden Sie im NuGet GitHub [Befehlszeilen Meilenstein](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).

## <a name="visual-studio-extension-updates"></a>Updates für Visual Studio-Erweiterung

### <a name="new-features-in-visual-studio"></a>Neue Features in Visual Studio

* Im Projektmappen-Explorer auf den Projektmappenknoten, die Pakete wiederhergestellt werden, ohne die Erstellung der Lösung ermöglicht neue Kontextmenüelement hinzugefügt wurde ([1274](https://github.com/NuGet/Home/issues/1274)).

![Neue "Pakete wiederherstellen" Kontextmenüelement](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Updates und Korrekturen in Visual Studio

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a>Die Korrekturen für authentifizierte Feeds wurden Rollup und in der Erweiterung ebenfalls behoben.  Die folgenden Elemente für die Authentifizierung wurden auch in der Erweiterung adressiert werden:

* Jetzt ordnungsgemäß zum Behandeln von Version 3 von NuGet Feeds ordnungsgemäß authentifiziert anstelle von v2 Feeds - authentifiziert [1216](https://github.com/NuGet/Home/issues/1216)
* Korrigierte Anforderung für Authentifizierungsanmeldeinformationen in Projekten mithilfe von `project.json` und die Kommunikation mit v2-Feeds - [1082](https://github.com/NuGet/Home/issues/1082)

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a>Netzwerkkonnektivität musste die Benutzeroberfläche in Visual Studio beeinflusst und es behandelt die folgenden Fixes:

* Verbessert die Wartung des lokalen Caches von Paketversionen - [1096](https://github.com/NuGet/Home/issues/1096)
* Das Verhalten bei Fehlern geändert, Herstellen der Verbindung mit einem v3-feed an nicht mehr versuchen, dies als v2 - Feed zu behandeln [1253](https://github.com/NuGet/Home/issues/1253)
* Jetzt verhindert Fehler installieren, beim Installieren eines Pakets mit mehrerer Paketquellen - [1183](https://github.com/NuGet/Home/issues/1183)

Wir haben die Behandlung von Interaktionen mit Buildvorgängen verbessert:

* Nachdem Sie den Vorgang fortsetzen, um Projekte zu erstellen, wenn Pakete wiederhergestellt werden, für ein einzelnes Projekt ein Fehler auftritt – [1169](https://github.com/NuGet/Home/issues/1169)
* Installiert ein Paket in ein Projekt, das von einem anderen Projekt in der Projektmappe abhängig ist, erzwingt eine Neuerstellung des Projektmappen - [981](https://github.com/NuGet/Home/issues/981)
* Korrigiert fehlerhafte Paketinstallationen ordnungsgemäß Änderungen zu einem Projekt - [1265](https://github.com/NuGet/Home/issues/1265)
* Häufungen von korrigiert die `developmentDependency` Attribut für ein Paket in `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Aufrufe von `install.ps1` verfügen nun über eine ordnungsgemäße `$package.AssemblyReferences` übergebene - Objekt [1245](https://github.com/NuGet/Home/issues/1245)
* Verhindert ohne mehr die heraufstufung von Paketen in UWP-Projekten deinstalliert, während das Projekt in einem fehlerhaften Zustand - ist [1128](https://github.com/NuGet/Home/issues/1128)
* Enthält eine Mischung aus Lösungen `packages.config` und `project.json` Projekte werden jetzt ordnungsgemäß ohne ein zweites erstellt Buildvorgangs - [1122](https://github.com/NuGet/Home/issues/1122)
* "App.config"-Dateien ordnungsgemäß zu suchen, wenn sie verknüpft sind, oder befindet sich in einem anderen Ordner - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* UWP-Projekte können nun installieren, nicht aufgelistete Pakete - [1109](https://github.com/NuGet/Home/issues/1109)
* Wiederherstellen von Paketen ist jetzt zulässig, während eine Projektmappe nicht in einem gespeicherten Zustand - ist [1081](https://github.com/NuGet/Home/issues/1081)


Behandeln von Updates an der Konfiguration, die Dateien wurden korrigiert:

* Entfernen nicht mehr einer Targets-Datei aus einem Paket auf nachfolgende Builds von übermittelt eine `project.json` verwaltetes Projekt - [1288](https://github.com/NuGet/Home/issues/1288)
* Datei "NuGet.config"-Dateien nicht mehr ändern, während der projektmappenerstellung für ASP.NET 5 - [1201](https://github.com/NuGet/Home/issues/1201)
* Nicht mehr ändern Versionen Einschränkung zulässig, während der paketaktualisierung - [1130](https://github.com/NuGet/Home/issues/1130)
* Lock-Dateien jetzt bleiben gesperrt während des Buildvorgangs - [1127](https://github.com/NuGet/Home/issues/1127)
* Jetzt ändern `packages.config` und umgeschrieben wurde nicht während des Updates – [585](https://github.com/NuGet/Home/issues/585)


Interaktionen mit TFS-quellcodeverwaltung verbessert:

* Fehler bei nicht mehr installiert für Pakete, die mit TFS - gebunden sind [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Korrigierte NuGet-Benutzeroberfläche für die Integration von TFS 2013 – ermöglichen [1071](https://github.com/NuGet/Home/issues/1071)
* Verweise auf Pakete wiederhergestellt werden, um einen Ordner "Pakete" - ordnungsgemäß stammen korrigiert [1004](https://github.com/NuGet/Home/issues/1004)

Schließlich verbessert wir auch Folgendes:

* Ausführlichkeit der protokollmeldungen für verringert `project.json` zu verwalteten Projekten - [1163](https://github.com/NuGet/Home/issues/1163)
* Jetzt ordnungsgemäß anzeigen, von der installierten Version eines Pakets in der Benutzeroberfläche – [1061](https://github.com/NuGet/Home/issues/1061)


Eine vollständige Liste der Probleme, die für die Visual Studio-Erweiterung Sie im NuGet GitHub finden [3.2 Meilenstein](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>Bekannte Probleme

Wir fahren fort, um Probleme in der Liste unserer GitHub-Probleme nachzuverfolgen, die finden Sie unter: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)