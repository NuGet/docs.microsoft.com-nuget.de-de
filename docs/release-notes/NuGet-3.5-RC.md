---
title: 3,5 RC-Versions Anmerkungen
description: Anmerkungen zu dieser Version von nuget 3,5 RC, einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780194"
---
# <a name="nuget-35-rc-release-notes"></a>Anmerkungen zu dieser Version von nuget 3,5 RC

Anmerkungen zu dieser [Version von nuget 3,5-Beta2](../release-notes/nuget-3.5-Beta2.md)  |  [Anmerkungen zu dieser Version von nuget 3,5-RTM](../release-notes/nuget-3.5-RTM.md)

3,5 Release konzentriert sich auf die Verbesserung der Qualität und Leistung von nuget-Clients. Außerdem haben wir einige Features wie Unterstützung für [Fall Back Ordner](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) -Unterstützung in `.nuspec` und mehr geliefert.

[Liste der Probleme](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Fehlerkorrekturen

* Die Installation/Wiederherstellung eines Pakets schlägt fehl, wenn das Paket mehrere `.nuspec` Dateien enthält. - [#3231](https://github.com/NuGet/Home/issues/3231)

* Das nuget-Paket fügt `.tt` Dateien dem Inhalts Ordner unabhängig von der- [#3203](https://github.com/NuGet/Home/issues/3203) hinzu.

* Das nuget-Paket "csproj" (mit `project.json` ) stürzt ab, wenn keine packoptions und Besitzer in der JSON-Datei vorhanden sind [#3180](https://github.com/NuGet/Home/issues/3180)

* Das nuget-Paket für `project.json` ignoriert packoptions-Tags wie Zusammenfassung, Autoren, Besitzer usw.- [#3161](https://github.com/NuGet/Home/issues/3161)

* Das nuget-Paket ignoriert Abhängigkeiten in der Ausgabe `.nuspec` für `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Wenn Sie mehrere Pakete mit Rollback aktualisieren, bleibt das Projekt in einem unterbrochenen Zustand [#3139](https://github.com/NuGet/Home/issues/3139)

* "Contentfiles" unter "Any" wird nicht für netstandard-Projekte hinzugefügt- [#3118](https://github.com/NuGet/Home/issues/3118)

* Die Bibliothek für .NET Standard kann nicht ordnungsgemäß [#3108](https://github.com/NuGet/Home/issues/3108) werden.

* Datei > neues Projekt > Klassenbibliothek (portabel) schlägt in VS2015 und Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* Der nuget-Fehler-1.0.0-* ist keine gültige Versions Zeichenfolge [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package kann nicht angezeigt werden, aber Install-Package Works- [#3068](https://github.com/NuGet/Home/issues/3068)

* Fehler bei "Install-package jQuery. Validation" auf dev15- [#3061](https://github.com/NuGet/Home/issues/3061)

* Bei der Installation von vs 2015 Update 3 auf einem vs, der die nuget-Version verwendet 3.5.0 Fehler tritt auf [#3053](https://github.com/NuGet/Home/issues/3053)

* Benutzeroberfläche des Paket-Managers: zeigt keine neue Version nach dem Aktualisieren eines Pakets an [#3041](https://github.com/NuGet/Home/issues/3041)

* -APIKey in der Befehlszeile "Delete" wird in 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037) nicht gelesen/gesendet

* Falsche Zeichenfolge: ein stabiles Release eines Pakets sollte nicht für eine vorab Abhängigkeit vorhanden sein. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Beim Erstellen des Projekts PCL ("net46 und Windows 10) wird die Ausnahme NullRef-Ausnahme zurückerhalten. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Das nuget-Update sollte eine informative Nachricht bereitstellen, wenn eine höhere Version durch die Einschränkung der Einschränkung-Version eingeschränkt ist [#3013](https://github.com/NuGet/Home/issues/3013)

* Das Anmelde Informations-Plug-in wurde mit Fehler-1/Fehler beim Herunterladen des Pakets beendet, wenn Anmelde Informationsanbieter mit mehreren Quellen verwendet werden [#2885](https://github.com/NuGet/Home/issues/2885)

* nuget-Paket-fehlende Newtonsoft.Jsin der Paketabhängigkeit [#2876](https://github.com/NuGet/Home/issues/2876)

* Fehler in executesynchronizedcore unter Linux/MacOS + Mono- [#2860](https://github.com/NuGet/Home/issues/2860)

* VS unterstützt keine Umgebungsvariablen in repositoryPath (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)

* Beheben von Barrierefreiheits Problemen: [#2745](https://github.com/NuGet/Home/issues/2745)

* Portable Frameworks mit mittels Bindestrich-Profilen werden abgelehnt. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Der nuget-Paket-Manager sollte deutlich machen, dass die Optionsliste in Paket Details nicht für `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* Nuget 3.3.0 Update schlägt mit einer zusätzlichen Einschränkung fehl... der in packages.config definierte Vorgang wird verhindert. - [#1816](https://github.com/NuGet/Home/issues/1816)

* Das Installieren eines Pakets aus einer lokalen Quelle, die nicht vorhanden ist, löst eine falsche Nachricht aus [#1674](https://github.com/NuGet/Home/issues/1674)

* Filter "Upgrade vailable" zeigt Upgrades an, die gegen die Versions Einschränkung verstoßen- [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Leistungsverbesserungen

* Leistung: verbessern der Inhalts Modell-Ziel Framework- [#3162](https://github.com/NuGet/Home/issues/3162)

* Leistung: vermeiden `runtime.json` Sie das Lesen von Dateien für Wiederherstellungen, die keine RIDs [#3150](https://github.com/NuGet/Home/issues/3150)haben. Auf CI-Computern wird die Wiederherstellung einer Beispiel-ASP.NET-Webanwendung von mehr als 15 Sekunden auf 3 Sekunden reduziert.

* Leistung: init.ps1 Ladezeit [#2956](https://github.com/NuGet/Home/issues/2956)der Paket-Manager-Konsole. Die Zeit zum Öffnen von packagemanagerconsole wurde in einigen Fällen von 132 bis 10S verbessert.

* Lösen Sie reschärfere Leistungsprobleme beim nuget-Update- [#3044](https://github.com/NuGet/Home/issues/3044): in einem Beispiel Projekt wird die Zeit zum Installieren von Paketen von 140s auf 68s verkürzt.

## <a name="dcrs"></a>DCRs

* Nuget muss den Benutzern mitteilen, dass ein Upgrade/Installation in einer dotnet TFM-basierten PCL Probleme verursachen könnte [#3138](https://github.com/NuGet/Home/issues/3138)

* Warnung bei fehlerhafter Installation/Upgrade für Projekt w/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* Netcoreapp11-und netstandard17-Unterstützung hinzufügen- [#2998](https://github.com/NuGet/Home/issues/2998)

* Drucken NuGet-Warning Header Inhalt in der Konsole in nuget.exe- [#2934](https://github.com/NuGet/Home/issues/2934)

* Verwenden des ASSEMBLYMETADATA-Attributs für `.nuspec` tokenersetzungen- [#2851](https://github.com/NuGet/Home/issues/2851)

* Entfernen Sie die gesperrte Eigenschaft aus der Sperrdatei [#2379](https://github.com/NuGet/Home/issues/2379)

* Symbol Pakete sollten nicht jemals in Installations-oder Update #2807 verwendet werden.

## <a name="features"></a>Features

* Unterstützung für Fall Back Paket Ordner- [#2899](https://github.com/NuGet/Home/issues/2899)

* Entwerfen und implementieren Sie ein Konzept des Pakettyps, um Tool Pakete zu unterstützen- [#2476](https://github.com/NuGet/Home/issues/2476)

* API, um den Pfad zum Ordner für globale Pakete zu erhalten [#2403](https://github.com/NuGet/Home/issues/2403)

* Unterstützung für Native Pakete aktualisieren- [#1291](https://github.com/NuGet/Home/issues/1291)
