---
title: 3.5 RC-Versionsanmerkungen
description: Anmerkungen zu NuGet 3.5 RC, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548537"
---
# <a name="nuget-35-rc-release-notes"></a>Anmerkungen dieser Version von NuGet 3.5 RC

[Anmerkungen zu NuGet 3.5-Beta2](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5 – Anmerkungen zu dieser Version RTM](../release-notes/nuget-3.5-RTM.md)

3.5 Version konzentriert sich auf die Verbesserung der Qualität und Leistung von NuGet-Clients. Darüber hinaus haben wir einige Funktionen wie Unterstützung für ausgeliefert [Fallback-Ordnern](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) -Unterstützung in `.nuspec` und vieles mehr.

[Probleme: Liste](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Fehlerkorrekturen

* Installation/Wiederherstellung eines Pakets schlägt fehl mit "-Paket enthält mehrere `.nuspec` Dateien." - [#3231](https://github.com/NuGet/Home/issues/3231)

* NuGet Pack erzwungen fügt `.tt` Dateien zum Ordner "Content" unabhängig davon, was - [#3203](https://github.com/NuGet/Home/issues/3203)

* NuGet Pack Csproj (mit `project.json`) stürzt ab, wenn es keine PackOptions und Besitzer in der JSON-Datei sind - [#3180](https://github.com/NuGet/Home/issues/3180)

* NuGet Pack für `project.json` ignoriert PackOptions Tags wie Zusammenfassung, Autoren und Besitzer usw. – [#3161](https://github.com/NuGet/Home/issues/3161)

* NuGet Pack werden die Abhängigkeiten in der Ausgabe ignoriert `.nuspec` für `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Aktualisieren mehrere Pakete mit Rollback lässt das Projekt in einem unterbrochenen Zustand - [#3139](https://github.com/NuGet/Home/issues/3139)

* "Contentfiles", unter einer werden nicht hinzugefügt werden, für die Netstandard-Projekte – [#3118](https://github.com/NuGet/Home/issues/3118)

* Kann nicht gepackt werden Library für .net Standard ordnungsgemäß - [#3108](https://github.com/NuGet/Home/issues/3108)

* Datei -> Neues Projekt -> Klassenbibliothek (portabel) ein Fehler auftritt-Projekt in Visual Studio 2015 und Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* NuGet-Fehler: 1.0.0-* ist keine gültige Versionszeichenfolge - [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package ein Fehler auftritt, anzeigen, aber funktioniert für Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Fehler bei "Install-Package jquery.validation" auf dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* Bei der installierten Visual Studio 2015 update 3 für einen im Vergleich, der verwendet NuGet 3.5.0-Versionsfehler tritt auf, - [#3053](https://github.com/NuGet/Home/issues/3053)

* Paket-Manager-Benutzeroberfläche: neue Version nicht angezeigt werden, nach dem Aktualisieren eines Pakets- [#3041](https://github.com/NuGet/Home/issues/3041)

* -"Apikey" Befehlszeile für Delete-Befehl nicht Lese-/gesendet 3.5.0-Beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Falsches Zeichenfolgenformat: eine stabile Version eines Pakets müssen sich nicht auf einer Vorabversion Abhängigkeit. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Erstellen die PCL (net46 und Windows 10)-Projekt Get NullRef-Ausnahme. - [#3014](https://github.com/NuGet/Home/issues/3014)

* NuGet-Updates sollten informationsmeldung bereitstellen, wenn eine höhere Version durch Einschränkung der AllowedVersions - eingeschränkt ist [#3013](https://github.com/NuGet/Home/issues/3013)

* Anmeldeinformationen-Plug-in wurde mit Fehler-1 beendet / Fehler beim Herunterladen bei Verwendung der Anmeldeinformationsanbieter mit mehreren Quellen – package [#2885](https://github.com/NuGet/Home/issues/2885)

* NuGet Pack - Paket-Abhängigkeit fehlt "newtonsoft.JSON" - [#2876](https://github.com/NuGet/Home/issues/2876)

* Fehler in ExecuteSynchronizedCore auf Linux/MacOS "+" Mono - [#2860](https://github.com/NuGet/Home/issues/2860)

* Visual Studio unterstützt keine Umgebungsvariablen im RepositoryPath (nuget.exe bewirkt) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Beheben Sie Probleme mit der Barrierefreiheit - [#2745](https://github.com/NuGet/Home/issues/2745)

* Portable-Frameworks mit Bindestrichen Profile werden abgelehnt. - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet-Paket-Manager sollten diese Optionsliste in Paketen zu verdeutlichen, Detail nicht für gilt, `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0-Aktualisierung ein Fehler auftritt, mit "... eine zusätzliche Einschränkung definiert" Packages.config "wird verhindert, dass dieser Vorgang." - [#1816](https://github.com/NuGet/Home/issues/1816)

* Installieren des Pakets aus einer lokalen Quelle, die nicht vorhanden ist löst einer gefälschten Nachricht - [#1674](https://github.com/NuGet/Home/issues/1674)

* Filter für "Verfügbare Upgrade" zeigt, Upgrades, bei denen die versionseinschränkung - verletzen [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Leistungsverbesserungen

* : Leistungsverbesserung "ContentModel" Target Framework Analyse - [#3162](https://github.com/NuGet/Home/issues/3162)

* Leistung: Vermeiden Sie lesen `runtime.json` Dateien für Wiederherstellungen, denen keine RIDs [#3150](https://github.com/NuGet/Home/issues/3150). Auf CI-Computern Wiederherstellen eines Beispiels, die ASP.NET Web-Anwendung von 15 Sekunden auf 3 Sekunden reduziert.

* Leistung: Paket-Manager-Konsole init.ps1 Ladezeit [#2956](https://github.com/NuGet/Home/issues/2956). Zeit in Anspruch PackageManagerConsole verbessert in einigen Fällen von 132s 10 Sekunden.

* Lösen von Leistungsproblemen von ReSharper in NuGet-Update - [#3044](https://github.com/NuGet/Home/issues/3044): für ein Beispielprojekt Zeit zum Installieren von Paketen von 140s auf reduziert 68s.

## <a name="dcrs"></a>DCRs

* NuGet muss, damit Benutzer wissen, dass in einem Dotnet Tfm-basierte aktualisieren bzw. installieren PCL-Fehlern – verursachen [#3138](https://github.com/NuGet/Home/issues/3138)

* Ungültige installieren/aktualisieren für Projekt mit Tfm warnen = "Dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)

* Hinzufügen von Unterstützung für netcoreapp11 und netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* NuGet-Warning-Header Inhalte an die Konsole in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)

* AssemblyMetadata-Attribut für nutzen `.nuspec` Ersetzungen - token [#2851](https://github.com/NuGet/Home/issues/2851)

* Entfernen Sie die gesperrte Eigenschaft aus der Sperrdatei - [#2379](https://github.com/NuGet/Home/issues/2379)

* Symbolpakete sollte nicht immer in Installation, die verwendet werden, oder Aktualisieren von #2807

## <a name="features"></a>Features

* Unterstützung für den fallback-Paket-Ordner - [#2899](https://github.com/NuGet/Home/issues/2899)

* Entwerfen und implementieren Sie eine Vorstellung von Pakettyp Tool Pakete, unterstützen [#2476](https://github.com/NuGet/Home/issues/2476)

* -API, um den Pfad zu dem Ordner mit globalen Paketen - abzurufen [#2403](https://github.com/NuGet/Home/issues/2403)

* Native Pakete update-Support - [#1291](https://github.com/NuGet/Home/issues/1291)
