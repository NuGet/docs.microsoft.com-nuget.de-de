---
title: '3.5 Beta 2: Anmerkungen zu dieser Version'
description: Anmerkungen zu NuGet 3.5 Beta 2, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b47939e2fafc11823c41a849b3c58bbf0800ada
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551990"
---
# <a name="nuget-35-beta2-release-notes"></a>Anmerkungen zu NuGet 3.5 Beta 2

[Anmerkungen zu NuGet 3.5-Beta](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC-Versionsanmerkungen](../release-notes/nuget-3.5-RC.md)

RTM von NuGet 3.5 Beta 2 wurde am 27. Juni 2016 für Visual Studio 2013 und nuget.exe veröffentlicht.

[Vollständigen Änderungsprotokoll](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Probleme: Liste](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Fehlerkorrekturen

* Aktualisierte Fehlermeldung Mangel an Unterstützung für Kennwort Decrpytion in .NET Core für authentifizierte Feeds - [#2942](https://github.com/NuGet/Home/issues/2942)

* Paket-Manager-Console-Get-Package schlägt fehl, wenn .NET Core-Projekt geöffnet ist – [#2932](https://github.com/NuGet/Home/issues/2932)

* Korrektur der falschen Verarbeitung des 403 in NuGet Push-Befehl [#2910](https://github.com/NuGet/Home/issues/2910)

* Beheben von Problemen bei der Deinstallation von Paketen in einer Projektmappe, die an TFS-quellcodeverwaltung gebunden werden, wenn DisableSourceControlIntegration festgelegt ist auf "true" - [#2739](https://github.com/NuGet/Home/issues/2739)

* Beheben Sie die paketaktualisierung Konto nicht-Zielpakete. – berücksichtigen [#2724](https://github.com/NuGet/Home/issues/2724)

* Mit MSBuild-Ausführlichkeit fest Protokollierung Stufe für Nuget-Paket-Manager UI-Aktionen – [#2705](https://github.com/NuGet/Home/issues/2705)

* Korrektur von NuGet-Konfiguration ist ungültig Fehler in Websiteprojekte – VS 2015 VSIX (3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* Beheben Sie Probleme Pack `.csproj` bei Inhaltsdateien enthaltenen - [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) funktioniert nicht – [#2653](https://github.com/NuGet/Home/issues/2653)

* Korrigieren von Problem in Nuget 3.4.3 Release - Wert darf nicht null bei der paketerstellung - [#2648](https://github.com/NuGet/Home/issues/2648)

* Wiederherstellung verwendet gespeicherte Anmeldeinformationen aus der Datei "NuGet.config" für VSTS-Feeds - [#2647](https://github.com/NuGet/Home/issues/2647)

* Leistung - übermäßige Zuordnungen für die Korrektur in Code von Version-Vergleichs - [#2632](https://github.com/NuGet/Home/issues/2632)

* Beheben von Problemen, wenn mehrere Instanzen von nuget.exe versucht wird, zum Installieren des gleichen Pakets parallel - [#2628](https://github.com/NuGet/Home/issues/2628)

* Leistung - Cache von Abhängigkeitsinformationen für Vorgänge mit mehreren Projekten - [#2619](https://github.com/NuGet/Home/issues/2619)

* Problem wurde behoben, das Paket Quellen kann nicht aus den Einstellungen hinzugefügt werden, wenn Quellliste leer ist [#2617](https://github.com/NuGet/Home/issues/2617)

* Irreführende Fehler zu beheben, beim Versuch, Paket zu installieren, von denen abhängt, während der Entwurfszeit Fassaden - [#2594](https://github.com/NuGet/Home/issues/2594)

* Installieren eines Pakets von PackageManager-Konsole mit der Einstellung "Alle" aus versucht nur erste Quelle - [#2557](https://github.com/NuGet/Home/issues/2557)

* Beheben von Problemen mit Paketen, die Dateien in der Zukunft mit Schreibzugriff (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)

* Ausnahme angezeigt wird, wenn ein Fehler Suchen von Projekten in der Updatebefehl vorliegt – [#2418](https://github.com/NuGet/Home/issues/2418)

* Paketinhalt wird nicht ordnungsgemäß wiederhergestellt, beim Installieren eines Pakets aus einem Nuget-Version 3.3 +-mit dem Argument Feeds - NoCache, wenn das Paket enthält `.nupkg` Dateien – [#2354](https://github.com/NuGet/Home/issues/2354)

* Problem mit dem Paket installieren (alle Quellen) aus, wenn von der Quelle der 1 - Paket fehlt [#2322](https://github.com/NuGet/Home/issues/2322)

* Installieren Sie Blöcke, fällt eine einzelne Quelle Authorization - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` Bereich sollten außer Kraft setzen - IncludeReferencedProjects Version – Version [#1983](https://github.com/NuGet/Home/issues/1983)

* NuGet 3.3.0-Aktualisierung ein Fehler auftritt, mit "... eine zusätzliche Einschränkung definiert" Packages.config "wird verhindert, dass dieser Vorgang." - [#1816](https://github.com/NuGet/Home/issues/1816)

* NuGet.exe-Update löscht die Assembly starke Namen und das Private-Attribut. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Beheben von Problemen mit relativen Pfad für "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)

* Verbesserung der Fehlermeldungen für Update-Resolver - [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Features und Verhaltensänderungen

* NuGet.exe-Push - Timeout-Parameter funktioniert nicht – [#2785](https://github.com/NuGet/Home/issues/2785)

* NuGet.exe erstellt keine `.props` und `.targets` -Dateien für `.nuproj` Projekte (Regression im v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)

* Erweiterbarkeits-API-Frameworks mit Imports - vergleichen benötigen [#2633](https://github.com/NuGet/Home/issues/2633)

* Abhängigkeitsoptionen ausblenden, wenn mit `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Drucken Sie nuget.exe-Version-Header in der ausführlichen Ausgabe - [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet sollten Hinzufügen von Unterstützung für {löschen} /runtimes/ /nativeassets/ {Txm} & gt; – [#2782](https://github.com/NuGet/Home/issues/2782)