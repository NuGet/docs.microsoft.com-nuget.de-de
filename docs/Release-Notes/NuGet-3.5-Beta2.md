---
title: 3.5 Beta 2-Versionshinweise | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 3.5 Beta 2, einschließlich der bekannten Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-3.5 Beta 2 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4073b669c19f9e96ebd35ba269919b5f42313e7c
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-35-beta2-release-notes"></a>NuGet-3.5 Beta 2-Anmerkungen zu dieser Version

[NuGet-Version 3.5 Beta Hinweise](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC-Versionsanmerkungen](../release-notes/nuget-3.5-RC.md)

NuGet-3.5 Beta 2 RTM wurde 27. Juni 2016 für Visual Studio 2013 und nuget.exe freigegeben.

[Vollständige Änderungsprotokoll](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Probleme: Liste](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Fehlerkorrekturen

* Aktualisierte Fehlermeldung keine Unterstützung für Kennwort Decrpytion im .NET-Kern für authentifizierten Feeds - [#2942](https://github.com/NuGet/Home/issues/2942)

* Package Manager Console Get-Package fehlschlägt, wenn .NET Core-Projekt öffnen - [#2932](https://github.com/NuGet/Home/issues/2932)

* Korrektur der falschen Verarbeitung des 403 in NuGet-Befehl "Push" [#2910](https://github.com/NuGet/Home/issues/2910)

* Beheben von Problemen bei der Deinstallation von Paketen in einer Projektmappe zur TFS-quellcodeverwaltung gebunden werden, wenn DisableSourceControlIntegration festgelegt ist auf "true" - [#2739](https://github.com/NuGet/Home/issues/2739)

* Korrigieren Sie die paketaktualisierung Konto nicht Ziel Pakete - übernehmen [#2724](https://github.com/NuGet/Home/issues/2724)

* Mithilfe der Ausführlichkeit der MSBuild fest Protokollierung Stufe für NuGet-Paket-Manager-UI-Aktionen - [#2705](https://github.com/NuGet/Home/issues/2705)

* Korrektur NuGet-Konfiguration ist ungültige Fehlermeldung in Websiteprojekten – VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* Beheben von Problemen von Pack von `.csproj` Wenn Inhaltsdateien enthaltenen - [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) funktioniert nicht – [#2653](https://github.com/NuGet/Home/issues/2653)

* Beheben des Problem in Nuget 3.4.3 Version - Wert darf nicht null bei der paketerstellung - [#2648](https://github.com/NuGet/Home/issues/2648)

* Wiederherstellung verwendet gespeicherte Anmeldeinformationen von "NuGet.config" für VSTS-Feeds - [#2647](https://github.com/NuGet/Home/issues/2647)

* Leistung - übermäßige Zuordnungen für die Korrektur in Code von Version Vergleiche - [#2632](https://github.com/NuGet/Home/issues/2632)

* Beheben von Problemen, wenn mehrere Instanzen von nuget.exe versucht, zum Installieren des gleichen Pakets parallel - [#2628](https://github.com/NuGet/Home/issues/2628)

* Leistung - Cache Abhängigkeitsinformationen für Vorgänge mit mehreren Projekten - [#2619](https://github.com/NuGet/Home/issues/2619)

* Beheben des Problems Paket Datenquellen kann nicht in "Einstellungen" hinzugefügt werden, wenn Quellliste leer ist [#2617](https://github.com/NuGet/Home/issues/2617)

* Korrigieren Sie irreführende Fehler beim Installieren des Pakets, die zur Entwurfszeit Fassaden - abhängig [#2594](https://github.com/NuGet/Home/issues/2594)

* Nur erste Quelle - Installation eines Pakets aus PackageManager-Konsole mit der Einstellung "Alle" versucht [#2557](https://github.com/NuGet/Home/issues/2557)

* Beheben von Problemen mit Paketen mit Dateien in der Zukunft Schreibzeiten (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)

* Ausnahme angezeigt, bei ein Fehler Suchen von Projekten in Updatebefehl - [#2418](https://github.com/NuGet/Home/issues/2418)

* Paketinhalt wird nicht ordnungsgemäß wiederhergestellt, beim Installieren eines Pakets von Nuget v3. 3 +-mit dem Argument Feeds - NoCache, wenn das Paket enthält `.nupkg` Dateien - [#2354](https://github.com/NuGet/Home/issues/2354)

* Korrektur Problem mit dem Paket installieren (alle Quellen) aus, wenn von 1 Source - Paket fehlt [#2322](https://github.com/NuGet/Home/issues/2322)

* Blöcke zu installieren, schlägt eine einzelne Datenquelle Autorisierung - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec`Version Bereich sollten IncludeReferencedProjects - Version - überschreiben [#1983](https://github.com/NuGet/Home/issues/1983)

* NuGet 3.3.0 Update schlägt fehl mit "eine weitere Einschränkung... definiert" Packages.config ", verhindert diesen Vorgang." - [#1816](https://github.com/NuGet/Home/issues/1816)

* NuGet.exe Update löscht den starken Assemblynamen und privaten Attribut. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Beheben von Problemen mit relativen Pfad für "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)

* Verbesserung der Fehlermeldungen für Update-Resolver - [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Features und Verhaltensänderungen

* NuGet.exe Push - Timeoutparameter funktioniert nicht – [#2785](https://github.com/NuGet/Home/issues/2785)

* NuGet.exe Wiederherstellung keine erzeugt `.props` und `.targets` Dateien für `.nuproj` Projekte (Regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)

* Erweiterbarkeits-API zum Vergleichen von Importen - Frameworks benötigen [#2633](https://github.com/NuGet/Home/issues/2633)

* Abhängigkeitsoptionen ausblenden, wenn mit `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Drucken nuget.exe-Versionsheader in ausführliche Ausgabe - [#1887](https://github.com/NuGet/Home/issues/1887)

* Sollte zum Hinzufügen von NuGet-Unterstützung für /runtimes/ {rid} /nativeassets/ {Txm} / - [#2782](https://github.com/NuGet/Home/issues/2782)