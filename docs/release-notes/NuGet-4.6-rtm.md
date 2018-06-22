---
title: Anmerkungen zu Version 4.6 RTM von NuGet
description: Anmerkungen zu NuGet 4.6.0, einschließlich bekannter Fehler, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: 11e604ad9a28ac2b22880a13ef9d8b41d8c09507
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/22/2018
ms.locfileid: "34449616"
---
# <a name="nuget-46-rtm-release-notes"></a>Anmerkungen zu Version 4.6 RTM von NuGet

[NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe) ist im Lieferumfang von [Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) enthalten.

## <a name="summary-whats-new-in-this-release"></a>Zusammenfassung: Neues in diesem Release

* Unterstützung für das [Signieren von Paketen](../create-packages/sign-a-package.md) wurde hinzugefügt.
* Visual Studio 2017 und „nuget.exe“ überprüfen nun vor der Installation die Paketintegrität, sodass Pakete für [signierte Pakete](../reference/signed-packages-reference.md) wiederhergestellt werden.
* Die Leistung von aufeinander folgenden Wiederherstellungen wurde verbessert.

## <a name="known-issues"></a>Bekannte Probleme

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Probleme mit .NET Standard 2.0 mit .NET Framework und NuGet 

.NET Standard und die dazugehörigen Tools wurden so konzipiert, dass Projekte, die für .NET Framework 4.6.1 erstellt wurden, NuGet-Pakete und -Projekte verarbeiten können, die für .NET Standard 2.0 oder früher erstellt wurden. In [diesem Dokument](https://github.com/dotnet/standard/issues/481) werden die Probleme, die in diesem Szenario auftreten können, der Plan für die Behebung dieser Probleme und Problemumgehungen zusammengefasst, die Sie nach aktuellem Stand für die Tools bereitstellen können.

## <a name="top-issues-fixed-in-this-release"></a>In diesem Release behobene Hauptprobleme

**Behobene Leistungsprobleme**

* Medienobjektdateien nicht schreiben, wenn keine Änderungen vorgenommen wurden – [#6491](https://github.com/NuGet/Home/issues/6491)
* Wiederherstellung verursacht zusätzliche MSBuild-Auswertungen, wenn der TFM von untergeordneten Projekten nicht mit dem des übergeordneten Projekts übereinstimmt – [#6311](https://github.com/NuGet/Home/issues/6311)
* Verbesserung der NoOp-Wiederherstellungsleistung durch Optimieren der Erstellung der Spezifikationen für das Abhängigkeitsdiagramm – [#6252](https://github.com/NuGet/Home/issues/6252)

**Fehler**

* Bei Push an einen lokalen Ordner wird NUPKG gesperrt – [#6325](https://github.com/NuGet/Home/issues/6325)
* Implementierung des NuGet-Plug-Ins: mehrere Probleme – [#6149](https://github.com/NuGet/Home/issues/6149)
* UIHang: Entfernen des Aufrufs des Abfragediensts aus der MEF-Initialisierung in VSSolutionManager – [#6110](https://github.com/NuGet/Home/issues/6110)
* Ausnahme für die Fehlerberichterstattung für abgebrochene Paketdownloadtasks – [#6096](https://github.com/NuGet/Home/issues/6096)
* „NuGet.exe“ ersetzt „+“ durch „%2B“ im Assemblynamen – [#5956](https://github.com/NuGet/Home/issues/5956)
* Fn+F1 führt bei der PM-Benutzeroberfläche und -Konsole nicht zu der richtigen Hilfeseite – [#5912](https://github.com/NuGet/Home/issues/5912)
* NuGet schreibt unter bestimmten Umständen absolute Pfade in Projektdateien – [#5888](https://github.com/NuGet/Home/issues/5888)
* Beheben der 4.3-Regression: Platzhalter „$product$“ und „$AssemblyGuid$“ werden in der Inhaltsdatei nicht durch Transformation ersetzt – [#5880](https://github.com/NuGet/Home/issues/5880)
* „dotnet restore“ stürzt bei mehreren Quellen ab – [#5817](https://github.com/NuGet/Home/issues/5817)
* „Pack“ sollte die Projektversionen erneut auswerten, um die Git-Versionsverwaltung zu ermöglichen – [#4790](https://github.com/NuGet/Home/issues/4790)
* Verbessern schwer verständlicher Fehlermeldungen beim Installieren eines inkompatiblen Pakets – [#4555](https://github.com/NuGet/Home/issues/4555)
* TemplateWizard benötigt eine Option zum Installieren von Paketen als PackageReferences – [#4549](https://github.com/NuGet/Home/issues/4549)
* Durch ein Paket übermittelte Eigenschaftendateien werden ignoriert, wenn „MSBuild.exe“ außerhalb einer Developer-Eingabeaufforderung ausgeführt wird – [#4530](https://github.com/NuGet/Home/issues/4530)
* Beheben schlechter Fehlermeldungen, wenn auf die .NET Standard-Bibliothek verwiesen wird, die nicht auf das Projekt anwendbar ist – [#4423](https://github.com/NuGet/Home/issues/4423)
* Der Paketbefehl „dotnet add“ schlägt bei Paketen fehl, die ein portables Profil mit wenig Anleitung als Ziel verwenden – [#4349](https://github.com/NuGet/Home/issues/4349)
* dotnet pack: Versionssuffix fehlt in ProjectReference – [#4337](https://github.com/NuGet/Home/issues/4337)
* Buildfehler und Abstürzen von Visual Studio bei .NET Core-Vorlagen – [#3973](https://github.com/NuGet/Home/issues/3973)
* Dienstindex für HTTPS der Quelle kann nicht geladen werden – [#3681](https://github.com/NuGet/Home/issues/3681)
* nuget.exe-Liste: „Allversions“ funktioniert nicht – [#3441](https://github.com/NuGet/Home/issues/3441)
* Irreführende Fehlermeldung für die Abhängigkeitsauflösung – [#2984](https://github.com/NuGet/Home/issues/2984)
* Das Wiederherstellen von „nuget.exe“ erstellt keine PROPS- und TARGETS-Dateien für MSBUILDPROJ (Regression im Upgrade von Version 3.3.0 auf 3.4.4) – [#2921](https://github.com/NuGet/Home/issues/2921)
* Verzögerung der Benutzeroberfläche beim Aktualisieren eines NuGet-Pakets, wenn die XAML-Datei geöffnet ist – [#2878](https://github.com/NuGet/Home/issues/2878)
* Websiteprojekt von IIS löst einen Fehler mit ungültigen Zeichen im Pfad aus – [#2798](https://github.com/NuGet/Home/issues/2798)
* Der Befehl „nuget add“ stürzt unter CentOS ab – [#2708](https://github.com/NuGet/Home/issues/2708)
* Wiederherstellung mit „packagesavemode -nupkg“ für „json.net“ schlägt fehl – [#2706](https://github.com/NuGet/Home/issues/2706)
* Paket-Manager-Filter ist im Ausgabefenster für den Befehl „restore“ von Visual Studio nicht verfügbar – [#2704](https://github.com/NuGet/Home/issues/2704)

[Liste aller in diesem Release behobener Fehler](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
