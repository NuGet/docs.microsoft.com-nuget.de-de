---
title: Anmerkungen zu Version 4.3 RTM von NuGet
description: Anmerkungen zu Version 4.3 RTM von NuGet, einschließlich bekannter Fehler, Fehlerkorrekturen, hinzugefügter Funktionen und DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: cb44f47ef0b3bd086f0a681cb2fedc7c5afc42fa
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822655"
---
# <a name="nuget-43-rtm-release-notes"></a>Anmerkungen zu Version 4.3 RTM von NuGet

NuGet 4.3 RTM ist im Lieferumfang von [Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) enthalten, fügt die Unterstützung von neuen Szenarios wie .NET Standard 2.0 und .NET Core 2.0 hinzu, enthält viele wichtige Fehlerbehebungen und verbessert die Leistung. In diesem Release sind außerdem einige Verbesserungen enthalten, wie u.a. die Unterstützung von Version 2.0.0 der semantischen Versionierung und die MSBuild-Integration von NuGet-Warnungen und -Fehlern.

## <a name="known-issues"></a>Bekannte Probleme

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>Die NuGet-Wiederherstellung behandelt deaktivierte Paketquellen in einigen Fällen so, als wären sie aktiviert

#### <a name="issue"></a>Problem

Mit den folgenden Wiederherstellungsbefehlszeilen werden deaktivierte Paketquellen so behandelt, als wären sie aktiviert. [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore` (muss entweder mit dem in Visual Studio mitgelieferten Programm „dotnet.exe“ oder dem gleichnamigen Programm aus dem NetCore SDK 2.0.0 verwendet werden)

#### <a name="workaround"></a>Problemumgehung

1. Verwenden Sie Visual Studio (2017 15.3 oder höher) oder „NuGet.exe“ (v4.3.0 oder höher).
1. Löschen Sie die deaktivierte Paketquelle, und verwenden Sie weiterhin „msbuild“ oder „dotnet.exe“.
1. Für Ihre Projektmappe können Sie das Element „Clear“ in der Datei „NuGet.config“ verwenden und anschließend die notwendigen Paketquellen für diese Projektmappe definieren.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Beim Verwenden der Paket-Manager-Konsole funktioniert die EINGABETASTE ggf. nicht

#### <a name="issue"></a>Problem

Gelegentlich kann es vorkommen, dass die EINGABETASTE in der Paket-Manager-Konsole nicht funktioniert. Wenn dieses Problem auftritt, überprüfen Sie den Fortschritt für diese Korrektur und stellen Sie zusätzliche hilfreiche Informationen zu den Reproduktionsschritten bereit. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Problemumgehung

Starten Sie Visual Studio neu und öffnen Sie die Paketverwaltungskonsole, bevor Sie die Projektmappe öffnen. Alternativ können Sie versuchen, die Datei `project.lock.json` zu löschen und dann erneut wiederherzustellen.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Sie können DotNetCLITools nicht mit dem NuGet-Paket-Manager anzeigen, hinzufügen oder aktualisieren.

#### <a name="issue"></a>Problem

Der NuGet-Paket-Manager zeigt die DotNetCLITools nicht an und ermöglicht auch kein Hinzufügen/Aktualisieren dieser Tools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Problemumgehung

DotNetCLIToolReferences muss in der Projektdatei manuell bearbeitet werden.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Die Neuzuweisung der Framework-Zielversion kann zu unvollständigen IntelliSense-Funktionen führen

#### <a name="issue"></a>Problem

Die Neuzuweisung der Framework-Zielversion kann zu unvollständigen IntelliSense-Funktionen in Visual Studio führen. Dies geschieht, wenn Sie PackageReferences als Paket-Manager-Format verwenden. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Problemumgehung

Führen Sie eine manuelle Wiederherstellung aus.

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>Behobene Probleme mit dem NuGet 4.3 RTM-Zeitrahmen

In den [Anmerkungen zu der Version 4.0 RTM von NuGet](../release-notes/nuget-4.0-RTM.md) werden alle für NuGet 4.0 RTM behobenen Probleme aufgeführt.

### <a name="features"></a>Features

- Verbesserung der Wiederherstellungsleistung für NuGet: eine intelligentere NoOp-Version für Befehlszeilenwiederherstellungen und Visual Studio ([#5080](https://github.com/NuGet/Home/issues/5080))

- NET Core 2.0: Die Visual Studio- bzw. Dotnet-CLI sollte mithilfe von FallBack-Ordnern geöffnet werden, einer NuGet-Funktion ([#4939](https://github.com/NuGet/Home/issues/4939))

- NET Core 2.0: Benutzer können bestimmte Wiederherstellungswarnungen ignorieren oder auf einen Fehler erweitern ([#4898](https://github.com/NuGet/Home/issues/4898))

- NET Core 2.0: lokalisierte CLI-Assemblys ([#4896](https://github.com/NuGet/Home/issues/4896))

- NET Core 2.0: Registrierung aller Warnungen bzw. Fehler in Objektdateien, einschließlich PackageTargetFallback ([#4895](https://github.com/NuGet/Home/issues/4895))

- Aktivierung der TFM-Unterstützung: .NET Standard 2.0, Tizen ([#4892](https://github.com/NuGet/Home/issues/4892))

- Reduzierung der Anzahl von NuGet.Core- und NuGet.Client-Projekten und somit auch von DLLs ([#2446](https://github.com/NuGet/Home/issues/2446))

- Hinzufügen der Möglichkeit, NuGet-Warnungen als Fehler zu markieren ([#2395](https://github.com/NuGet/Home/issues/2395))

### <a name="bugs"></a>Fehler

- „MSBuild /t:pack“ schlägt mit dem DevelopmentDependency-Parameter fehl und wird nicht von der PackTask-Aufgabe unterstützt ([#5584](https://github.com/NuGet/Home/issues/5584))

- Verzeichnisstruktur für vereinfachte Inhaltsdateien, wenn nicht das Windows-Verzeichnistrennzeichen am Ende von „PackagePath“ hinzugefügt wird ([#4795](https://github.com/NuGet/Home/issues/4795))

- .NET Core-Projekte unterstützen die Einstellung „developmentDependency“ nicht ([#4694](https://github.com/NuGet/Home/issues/4694))

- „RestoreManagerPackage“ wird synchron geladen, wodurch der Benutzeroberflächenthread blockiert und ein Deadlock für Visual Studio eingetreten ist ([#4679](https://github.com/NuGet/Home/issues/4679))

- dotnet
  - „dotnet restore“ (und daher auch „msbuild /t:restore“) überspringt Projekte mit einer expliziten Abhängigkeit von einem Projektmappenprojekt ([Nr. 4578](https://github.com/NuGet/Home/issues/4578))

- Wenn Ihre Projektmappe Verweise auf dasselbe Projekt enthält, funktioniert die Wiederherstellung möglicherweise nicht, wenn die Groß- und Kleinschreibung geändert wird. Ebenfalls kommt es nicht zu einer Wiederherstellung, wenn verschiedene relative Pfade vorhanden sind, bei denen es allerdings keine Abweichungen im Hinblick auf Groß- und Kleinschreibung gibt ([#4574](https://github.com/NuGet/Home/issues/4574))

- Ausführbare Dateien, die aus NuGet-Paketen wiederhergestellt werden, können mit .NET Core 2.0 nicht mehr ausgeführt werden ([#4424](https://github.com/NuGet/Home/issues/4424))

- In der „NuGet.exe“-Datei gehen bei der Analyse der Projektmappendatei Details zur Ausnahme verloren ([#4411](https://github.com/NuGet/Home/issues/4411))

- Das Paket speichert Inhaltsdateien an einem falschen Speicherort, wenn „ContentTargetFolders“ einen Pfad unter Windows enthält, der mit einem Schrägstrich („/“) endet ([#4407](https://github.com/NuGet/Home/issues/4407))

- „DotNetCliToolReference“ kann für ein Toolpaket, das netcoreapp1.1 anzielt, nicht wiederhergestellt werden ([#4396](https://github.com/NuGet/Home/issues/4396))

- Die aktualisierte NuGet-CLI behält die veraltete Bedingung für die Paketversion in einer Projektdatei bei (C++) ([#2449](https://github.com/NuGet/Home/issues/2449))

### <a name="dcrs"></a>DCRs

- „DotnetCliToolTargetFramework“ wird aus der CPS-Notation gelesen ([#5397](https://github.com/NuGet/Home/issues/5397))

- Die Überprüfung von TPMinV sollte für UWP im Projektstil funktionieren ([#4763](https://github.com/NuGet/Home/issues/4763))

- Verbesserung der Benutzeroberflächenbeschreibung für AutoReferenced-Pakete ([#4471](https://github.com/NuGet/Home/issues/4471))

- Bei der NuGet-Wiederherstellung werden kompilierte Objekte aus dem Runtimebereich ausgewählt([#4207](https://github.com/NuGet/Home/issues/4207))

- Abhängigkeitsanalysen werden in der Sperrdatei gespeichert ([#1599](https://github.com/NuGet/Home/issues/1599))

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>Links zu GitHub-Problemen die in 4.3 RTM behoben wurden

[Probleme: Liste](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
