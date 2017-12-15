---
title: 3.5 Anmerkungen zu dieser Version RC | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 75a9b496-5762-48b6-922f-fdddf1369c45
description: "Versionshinweise für NuGet 3.5 RC einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-3.5 RC-versionsanmerkungen, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 09d566de6f53bc0f0ddd8049143dc647f3075671
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
#<a name="35-rc-release-notes"></a>3.5 Anmerkungen zu dieser Version RC

[Anmerkungen zur Version von NuGet 3.5 Beta2](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Anmerkungen zu dieser Version](../release-notes/nuget-3.5-RTM.md)

Version 3.5 konzentriert sich auf die Verbesserung der Qualität und Leistung von NuGet-Clients. Darüber hinaus haben wir einige Funktionen wie die Unterstützung für geliefert [alternative Ordner](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) -Unterstützung in `.nuspec` und vieles mehr.

[Liste der Probleme](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5 RC")

## <a name="bug-fixes"></a>Fehlerkorrekturen

* Installation/Wiederherstellung eines Pakets schlägt fehl mit "Paket enthält mehrere `.nuspec` Dateien." - [#3231](https://github.com/NuGet/Home/issues/3231)

* NuGet-Pack erzwungen fügt `.tt` Dateien Inhaltsordner unabhängig davon, was - [#3203](https://github.com/NuGet/Home/issues/3203)

* NuGet-Pack Csproj (mit `project.json`) stürzt ab, wenn es keine PackOptions "und" Besitzer in JSON-Datei sind - [#3180](https://github.com/NuGet/Home/issues/3180)

* NuGet-Pack für `project.json` ignoriert PackOptions Tags wie Zusammenfassung, Autoren und Besitzer usw. - [#3161](https://github.com/NuGet/Home/issues/3161)

* NuGet-Pack ignoriert Abhängigkeiten in der Ausgabe `.nuspec` für `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Aktualisieren mehrere Pakete mit Rollback lässt das Projekt in einem fehlerhaften Zustand versetzt - [#3139](https://github.com/NuGet/Home/issues/3139)

* Inhaltsdateien unter einer werden nicht hinzugefügt, für die netstandard-Projekte - [#3118](https://github.com/NuGet/Home/issues/3118)

* Bibliothek für .net Paket kann nicht standardmäßige ordnungsgemäß - [#3108](https://github.com/NuGet/Home/issues/3108)

* Datei -> Neues Projekt-Klassenbibliothek (portabel) Projekt fehl in VS2015 und Dev15 - > [#3094](https://github.com/NuGet/Home/issues/3094)

* NuGet-Fehler: 1.0.0-* ist keine gültige Versionszeichenfolge - [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package ein Fehler auftritt, um die Anzeige "," Install-Package Works - [#3068](https://github.com/NuGet/Home/issues/3068)

* Fehler bei "Install-Package jquery.validation" auf dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* Bei der installierten Visual Studio 2015 update 3 auf einem VS, die NuGet-Version 3.5.0 Fehlers - verwendet [#3053](https://github.com/NuGet/Home/issues/3053)

* Paket-Manager-Benutzeroberfläche: keine neue Version angezeigt, nach dem Aktualisieren eines Pakets- [#3041](https://github.com/NuGet/Home/issues/3041)

* -"Apikey" für Delete-Befehlszeile nicht Lese-/gesendet 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Falsches Zeichenfolgenformat: eine stabile Version eines Pakets sollte keine für eine Vorabversion Abhängigkeit. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Erstellen PCL (net46 und Windows 10)-Projekt Get NullRef-Ausnahme. - [#3014](https://github.com/NuGet/Home/issues/3014)

* NuGet-Update sollten informationsmeldung bereitstellen, wenn eine höhere Version von "allowedversions"-Einschränkung - beschränkt ist [#3013](https://github.com/NuGet/Home/issues/3013)

* Anmeldeinformationen-Plug-in wurde mit dem Fehlercode:-1 / Fehler herunterladen bei Verwendung von mehreren Quellen - Anmeldeinformationsanbieter mit package [#2885](https://github.com/NuGet/Home/issues/2885)

* NuGet-Pack - Newtonsoft.Json fehlende paketabhängigkeit - [#2876](https://github.com/NuGet/Home/issues/2876)

* Fehler in ExecuteSynchronizedCore auf Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)

* Visual Studio unterstützt keine Umgebungsvariablen im RepositoryPath (nuget.exe bewirkt) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Beheben Sie Probleme mit dem Zugriff - [#2745](https://github.com/NuGet/Home/issues/2745)

* Portable Frameworks mit getrennten Profilen werden zurückgewiesen. - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet-Paket-Manager sollten unmissverständlich, Optionsliste in Paketen Detail nicht für gilt `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0 Update schlägt fehl mit "eine weitere Einschränkung... definiert" Packages.config ", verhindert diesen Vorgang." - [#1816](https://github.com/NuGet/Home/issues/1816)

* Installieren von einer lokalen Quelle, die löst nicht vorhanden ist eine gefälschte Nachricht - Paket [#1674](https://github.com/NuGet/Home/issues/1674)

* "Verfügbare Upgrade" Filter zeigt Upgrades, die die versionseinschränkung - verletzen [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Leistungsverbesserungen

* : Leistungsverbesserung ContentModel Ziel-Framework analysieren - [#3162](https://github.com/NuGet/Home/issues/3162)

* Leistung: Vermeiden Sie lesen `runtime.json` Dateien für die Wiederherstellung, die keine RIDs [#3150](https://github.com/NuGet/Home/issues/3150). Bei CI-Computer, die einer Stichprobe, die eine Aktualisierung 15 Sekunden bis 3 Sek. ASP.NET-Webanwendung reduziert wiederhergestellt werden.

* Leistung: Package Manager Console init.ps1 Ladezeit [#2956](https://github.com/NuGet/Home/issues/2956). Zeit zum Öffnen von PackageManagerConsole verbessert in einigen Fällen von 132s in 10.

* Lösen Sie ReSharper Leistungsprobleme in NuGet-Update - [#3044](https://github.com/NuGet/Home/issues/3044): für ein Beispielprojekt Zeit zum Installieren der Pakete von 140s auf reduziert 68s.

## <a name="dcrs"></a>Archivierung von dcrs Design

* NuGet muss, damit Benutzer wissen, dass ein Upgrade/Installation in ein Dotnet-Tfm basierend PCL Probleme - verursachen könnte [#3138](https://github.com/NuGet/Home/issues/3138)

* Warnhinweis anzeigen, fehlerhafte installiert oder aktualisiert für das Projekt mit Tfm "Dotnet" - = [#3137](https://github.com/NuGet/Home/issues/3137)

* Hinzufügen von netcoreapp11 und netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Drucken von NuGet-Warnung Headerinhalt in die Konsole in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)

* Nutzen der Vorteile AssemblyMetadata-Attribut für `.nuspec` Ersetzungen - token [#2851](https://github.com/NuGet/Home/issues/2851)

* Entfernen Sie die gesperrte Eigenschaft aus der Sperrdatei - [#2379](https://github.com/NuGet/Home/issues/2379)

* Symbolpakete sollten nicht jemals Installation verwendet werden, oder aktualisieren #2807

## <a name="features"></a>Features

* Unterstützung für alternative paketordnern - [#2899](https://github.com/NuGet/Home/issues/2899)

* Entwerfen und implementieren Sie eine Vorstellung von den Pakettyp Tool Pakete - Unterstützung [#2476](https://github.com/NuGet/Home/issues/2476)

* -API, um den Pfad zu dem Ordner "globale Pakete" - abzurufen [#2403](https://github.com/NuGet/Home/issues/2403)

* Systemeigene Updatepakete Support - [#1291](https://github.com/NuGet/Home/issues/1291)
