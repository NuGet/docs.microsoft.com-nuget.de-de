---
title: Anmerkungen zu Version 4.5 RTM von NuGet
description: Anmerkungen zu NuGet 4.5 RTM, einschließlich bekannter Fehler, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 1d04c508d029a6d92bbd480fe3bd7dc14727970e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820715"
---
# <a name="nuget-45-rtm-release-notes"></a>Anmerkungen zu Version 4.5 RTM von NuGet

[NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe) ist im Lieferumfang von [Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) enthalten.

## <a name="known-issues"></a>Bekannte Probleme

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Probleme mit .NET Standard 2.0 mit .NET Framework und NuGet 

.NET Standard und die dazugehörigen Tools wurden so konzipiert, dass Projekte, die für .NET Framework 4.6.1 erstellt wurden, NuGet-Pakete und -Projekte verarbeiten können, die für .NET Standard 2.0 oder früher erstellt wurden. In [diesem Dokument](https://github.com/dotnet/standard/issues/481) werden die Probleme, die in diesem Szenario auftreten können, der Plan für die Behebung dieser Probleme und Problemumgehungen zusammengefasst, die Sie nach aktuellem Stand für die Tools bereitstellen können.

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

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Ein Paket in einem .NET Core-Projekt, das eine Assembly mit einer ungültigen Signatur enthält, kann eine unendliche Wiederherstellungsschleife auslösen

#### <a name="issue"></a>Problem

Bei der Verwendung eines Pakets mit einer Assembly, die eine ungültige Signatur enthält, oder beim Festlegen der Paketversion mit dem DateTime-Ticker tritt gelegentlich bei der automatischen Paketwiederherstellung eine Endlosschleife auf ([dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457)).

#### <a name="workaround"></a>Problemumgehung

Zurzeit gibt es keine Problemumgehung.

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a>Behobene Probleme für den NuGet 4.5 RTM-Zeitrahmen

In den [Anmerkungen zu NuGet 4.4 RTM](../release-notes/nuget-4.4-RTM.md) finden Sie die in NuGet RTM 4.4 behobenen Probleme. 

### <a name="features"></a>Features

- Deaktivieren des automatischen Übertragens von Symbolpaketen per Push ([#6113](https://github.com/NuGet/Home/issues/6113))

### <a name="bugs"></a>Fehler

- [Regression] in 15.5p1: Portable0.0 wurde übersprungen ([#6105](https://github.com/NuGet/Home/issues/6105))
- Nach der Wiederherstellung fehlen Objekte aus Paketen ([#5995](https://github.com/NuGet/Home/issues/5995))
- Anbieter von Pluginanmeldeinformationen funktionieren nicht mit URIs, die Leerräume enthalten ([#5982](https://github.com/NuGet/Home/issues/5982))
- Wenn das Wiederherstellen eines Pakets fehlgeschlagen ist, sollten Fehler in der Ausgabe auch dann ausgegeben werden, wenn der geringste Ausführlichkeitsgrad aktiviert ist ([#5658](https://github.com/NuGet/Home/issues/5658))
- dotnet
  - „dotnetcore restore“ auf Projektmappenebene folgt nicht „ProjectReference“, wenn „ReferenceOutputAssembly“ auf FALSE festgelegt ist, was zu zufälligen Buildfehlern führt ([Nr. 5490](https://github.com/NuGet/Home/issues/5490))
- Die automatische Vervollständigung funktioniert in PMC mit Objektmethoden nicht ordnungsgemäß ([#4800](https://github.com/NuGet/Home/issues/4800))
- Das Wiederherstellen von „nuget.exe“ mit Visual Studio 2015-Toolset schlägt fehl ([#4713](https://github.com/NuGet/Home/issues/4713))
- Leistung: Die Instanziierung von PMC ist in Visual Studio 2017 ressourcenintensiv ([#4205](https://github.com/NuGet/Home/issues/4205))
- Es dauert lange, Abhängigkeitsinformationen bei einer langsamen Verbindung abzurufen ([#4089](https://github.com/NuGet/Home/issues/4089))
- Der Befehl zur Deinstallation eines Pakets mit -RemoveDependencies schlägt fehl, wenn mehrere Pakete eine gemeinsame Abhängigkeit haben ([#4026](https://github.com/NuGet/Home/issues/4026))
- „NuGet.Core.nupkg“ auf die Veröffentlichung vorbereiten ([#3581](https://github.com/NuGet/Home/issues/3581))
- Das NuGet-Paket löst die ID des Verzeichnisnamens auf, wenn -IncludeProjectReferences für die CSPROJ-Datei und „project.json“ verwendet wird ([#3566](https://github.com/NuGet/Home/issues/3566))
- Der Typinitialisierer für „NuGet.ProxyCache“ hat eine Ausnahme ausgelöst ([#3144](https://github.com/NuGet/Home/issues/3144))
- Problem beim Wiederherstellen von NuGet mit Kudu ([#3087](https://github.com/NuGet/Home/issues/3087))
- UI-Client zeigt weder Fehler noch Warnungen an, wenn die Suche vor Registrierungsblobs durchgeführt wird ([#2149](https://github.com/NuGet/Home/issues/2149))
- Get-Packages-Updates generiert eine falsche Abfrage ([#2135](https://github.com/NuGet/Home/issues/2135))

## <a name="links-to-github-issues-fixed-in-45-rtm"></a>Links zu GitHub-Problemen die in 4.5 RTM behoben wurden

[Liste der Probleme](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
