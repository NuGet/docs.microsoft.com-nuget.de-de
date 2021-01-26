---
title: 3,5 Beta2-Anmerkungen zu dieser Version
description: Anmerkungen zu dieser Version von nuget 3,5 Beta 2 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776395"
---
# <a name="nuget-35-beta2-release-notes"></a>Anmerkungen zu dieser Version von nuget 3,5 Beta2

Anmerkungen zu dieser [Version von nuget 3,5-Beta Version](../release-notes/nuget-3.5-Beta.md)  |  [Anmerkungen zu dieser Version von nuget 3,5-RC](../release-notes/nuget-3.5-RC.md)

Nuget 3,5 Beta 2 RTM wurde am 27. Juni 2016 für Visual Studio 2013 und nuget.exe veröffentlicht.

[Vollständiges Änderungsprotokoll](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Liste der Probleme](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Fehlerkorrekturen

* Aktualisierte Fehlermeldung: fehlende Unterstützung für Kenn Wort Entschlüsselungen in .net Core für authentifizierte Feeds- [#2942](https://github.com/NuGet/Home/issues/2942)

* Der Paket-Manager-Konsolen Get-Package schlägt fehl, wenn das .net Core-Projekt geöffnet ist [#2932](https://github.com/NuGet/Home/issues/2932)

* Korrigieren Sie die falsche Behandlung von 403 in einem nuget-Push-Befehl [#2910](https://github.com/NuGet/Home/issues/2910)

* Beheben Sie Probleme beim Deinstallieren von Paketen in einer Lösung, die an die TFS-Quell Code Verwaltung gebunden ist, wenn disablesourcecontrolintegration auf true festgelegt ist [#2739](https://github.com/NuGet/Home/issues/2739)

* Korrigieren Sie die Paketaktualisierung, um nicht Ziel Pakete zu berücksichtigen- [#2724](https://github.com/NuGet/Home/issues/2724)

* Verwenden Sie den ausführlichkeits Grad von MSBuild zum Festlegen der Protokollierungs Stufe für Benutzeroberflächen Aktionen des nuget-Paket-Managers [#2705](https://github.com/NuGet/Home/issues/2705) -

* Korrigieren der nuget-Konfiguration ist ein ungültiger Fehler in Website Projekten-vs 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)

* Beheben von Paket Problemen bei der Aufnahme von `.csproj` Inhalts Dateien [#2658](https://github.com/NuGet/Home/issues/2658)

* Defaultpushsource in `NuGetDefaults.Config` ( `ProgramData\NuGet` ) funktioniert nicht [#2653](https://github.com/NuGet/Home/issues/2653)

* Problembehebung in nuget 3.4.3 Release-value darf bei der Paket Erstellung nicht NULL sein- [#2648](https://github.com/NuGet/Home/issues/2648)

* RESTORE verwendet gespeicherte Anmelde Informationen aus Nuget.Config für VSTS-Feeds [#2647](https://github.com/NuGet/Home/issues/2647)

* Leistungs-Korrektur übermäßig viele Zuordnungen in Versions Vergleichs Code- [#2632](https://github.com/NuGet/Home/issues/2632)

* Beheben Sie Probleme, wenn mehrere Instanzen von nuget.exe versuchen, das gleiche Paket parallel zu installieren [#2628](https://github.com/NuGet/Home/issues/2628)

* Leistungs-Cache Abhängigkeitsinformationen für Vorgänge mit mehreren Projekten: [#2619](https://github.com/NuGet/Home/issues/2619)

* Behebung von Problemen, bei denen Paketquellen aus den Einstellungen nicht hinzugefügt werden, wenn die Quell Liste leer ist [#2617](https://github.com/NuGet/Home/issues/2617)

* Korrektur eines irreführenden Fehlers beim Versuch, ein Paket zu installieren, das von Entwurfszeit Fassaden abhängt [#2594](https://github.com/NuGet/Home/issues/2594)

* Wenn Sie ein Paket über die packagemanager-Konsole mit der Einstellung "All" installieren, wird nur die erste Quelle [#2557](https://github.com/NuGet/Home/issues/2557) versucht.

* Beheben von Problemen mit Paketen, die über Dateien mit Schreibzeiten in Zukunft verfügen (Mono)- [#2518](https://github.com/NuGet/Home/issues/2518)

* Ausnahme anzeigen, wenn beim Suchen nach Projekten in "Update Command- [#2418](https://github.com/NuGet/Home/issues/2418) " ein Fehler auftritt

* Der Paket Inhalt wird bei der Installation eines Pakets aus einem nuget v 3.3 +-Feed mit dem Argument NoCache, wenn das Paketdateien enthält, nicht ordnungsgemäß wieder hergestellt `.nupkg` [#2354](https://github.com/NuGet/Home/issues/2354)

* Beheben Sie das Problem mit der Paketinstallation (alle Quellen), wenn das Paket in 1 Quelle fehlt [#2322](https://github.com/NuGet/Home/issues/2322)

* Installations Blöcke, wenn eine einzelne Quelle die Autorisierung nicht besteht- [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec`Versions Bereich sollte-includereferencedprojects Version- [#1983](https://github.com/NuGet/Home/issues/1983) überschreiben

* Nuget 3.3.0 Update schlägt mit einer zusätzlichen Einschränkung fehl... der in packages.config definierte Vorgang wird verhindert. - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe Update löscht den starken Namen der Assembly und das private-Attribut. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Beheben von Problemen mit dem relativen Dateipfad für "defaultpushsource"- [#1746](https://github.com/NuGet/Home/issues/1746)

* Verbessern der Fehlermeldungen des Update Resolvers- [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Features und Behavior Changes

* nuget.exe Push-Timeout-Parameter funktioniert nicht [#2785](https://github.com/NuGet/Home/issues/2785)

* nuget.exe Restore erzeugt keine `.props` `.targets` -und-Dateien für `.nuproj` Projekte (Regression in v 3.4.3.855)- [#2711](https://github.com/NuGet/Home/issues/2711)

* Benötigen Erweiterbarkeits-API zum Vergleichen von Frameworks mit Importen- [#2633](https://github.com/NuGet/Home/issues/2633)

* Abhängigkeits Optionen beim Verwenden von `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486) ausblenden

* Ausgabe nuget.exe Versions Headers in detaillierter Ausgabe [#1887](https://github.com/NuGet/Home/issues/1887)

* Nuget sollte Unterstützung für/Runtimes/{Rid}/nativeassets/{txm}/- [#2782](https://github.com/NuGet/Home/issues/2782) hinzufügen