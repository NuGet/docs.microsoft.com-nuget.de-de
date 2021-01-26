---
title: Anmerkungen zu dieser Version von nuget 5,5
description: Anmerkungen zu dieser Version von nuget 5,5, einschließlich neuer Features, Fehlerbehebungen und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0fde67dd03c31e986ed89f2f8627608e279ef908
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780112"
---
# <a name="nuget-55-release-notes"></a>Anmerkungen zu dieser Version von nuget 5,5

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version| Verfügbar in .NET SDK(s)|
|:---|:---|:---|
| [**5.5.0**](https://nuget.org/downloads) | [Visual Studio 2019 Version 16.5](https://visualstudio.microsoft.com/downloads/) | [3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Installiert mit Visual Studio 2019 mit .net Core-Arbeitsauslastung

## <a name="summary-whats-new-in-55"></a>Zusammenfassung: Neues in 5,5

* Verbesserte Barrierefreiheit und Bildschirm Lesefunktion für die Benutzeroberfläche des nuget-Paket-Managers in Visual Studio
    * Barrierefreiheits Probleme bei der Bildschirm Lese Umgebung, fehlende AltText-und barrierefreie Namen für installierte TextBox,- [#9059](https://github.com/NuGet/Home/issues/9059)
    * Barrierefreiheits Probleme in der Sprachausgabe in der Paketliste- [#9077](https://github.com/NuGet/Home/issues/9077)
    * Barrierefreiheits Probleme im Zusammenhang mit "Durchsuchen", "installieren", "Aktualisieren"-Registerkarten- [#9078](https://github.com/NuGet/Home/issues/9078)
    * Die Sprachausgabe gibt keine Link Bezeichnung "blank", "No Dependencies", "nuget. org", "mit" an [#9157](https://github.com/NuGet/Home/issues/9157)

* Unterstützung für eigenständige Symbole in der Visual Studio-Paket-Manager-Benutzeroberfläche für Pakete, die auf lokalen Feeds gehostet werden [#8189](https://github.com/NuGet/Home/issues/8189)

* Erheblich verbesserte Leistung bei der nicht-op `RestoreUseStaticGraphEvaluation` -Wiederherstellung, bei der Auswertungen durch Aufrufen von MSBuild static Graph APIs- [8791](https://github.com/NuGet/Home/issues/8791) beschleunigt werden.

* Verbesserte dotnet.exe Zuverlässigkeit durch plattformübergreifende Authentifizierungs-Plug-ins
    * DotNet Restore Fehler mit "TaskCanceledException- [#7842](https://github.com/NuGet/Home/issues/7842)
    * Plug-in: "eine Aufgabe wurde abgebrochen": Problem bei der ADO-Authentifizierung. - [#8528](https://github.com/NuGet/Home/issues/8528)

* `dotnet nuget <add|remove|update|disable|enable|list> source`Befehls [#4126](https://github.com/NuGet/Home/issues/4126) hinzufügen

* Suport für die `--skip-duplicate`  Verwendung von dotnet nuget Push- [#8778](https://github.com/NuGet/Home/issues/8778)

* Unterstützung `packages.config` mit MSBuild/Restore- [#8506](https://github.com/NuGet/Home/issues/8506)

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

**Fehler**

* Self-Updater mit v3-APIs neu arbeiten- [#4197](https://github.com/NuGet/Home/issues/4197)

* Falsche Paket Abhängigkeits Version, wenn die Version der Paketabhängigkeit auf "*" festgelegt ist [#6697](https://github.com/NuGet/Home/issues/6697)

* Errorunsafepackageentry-Fehlermeldung verweist nicht auf die Ursache des Problems [#7505](https://github.com/NuGet/Home/issues/7505)

* Die Sperrdatei wird in "*"-Szenarios nicht berücksichtigt [#8073](https://github.com/NuGet/Home/issues/8073)

* NuGet.exe wird nicht in die neueste Version eines Pakets aufgelöst, wenn * in packagereferenziert wird (MSBuild/dotnet/vs Restore do)- [#8432](https://github.com/NuGet/Home/issues/8432)

* DotNet List-Paket mit Multi-Ziel-WPF-Projekt [#8463](https://github.com/NuGet/Home/issues/8463)

* Verbessern der hilfsdienstprogramme (CPU-Auslastung verringern)- [#8653](https://github.com/NuGet/Home/issues/8653)

* Die DG-Spezifikation für entladene Projekt Szenarien sollte nicht in der Vorschau Wiederherstellung geschrieben werden- [#8793](https://github.com/NuGet/Home/issues/8793)

* Die Visual Studio nuget-Pakete (restoremanagerpackage) müssen automatisch für projektmappenbuildereignisse geladen werden [#8796](https://github.com/NuGet/Home/issues/8796)

* Deadlock in VSSETTINGS init- [#8842](https://github.com/NuGet/Home/issues/8842)

* Die VisualStudio-Toolbox wird nicht aus einem nuget-Paket aufgefüllt, wenn ein Projekt in einem Projektmappenordner abgelegt wird [#8868](https://github.com/NuGet/Home/issues/8868)

* VS: Fehler bei der Wiederherstellung der Lösung aufgrund von Racebedingungen: [#8881](https://github.com/NuGet/Home/issues/8881)

* Konstante "wird geladen.." auf der Registerkarte "installiert" und "suchen <term>.. "auf der Registerkarte" Updates "- [#8890](https://github.com/NuGet/Home/issues/8890)

* Fehlende eingebettete Symbole in der vs-pm-Benutzeroberfläche nach Ablauf des Caches- [#9069](https://github.com/NuGet/Home/issues/9069)

* Start der PM-Benutzeroberfläche starten- [#9112](https://github.com/NuGet/Home/issues/9112)

* Restore: die includebug. include (...)-Implementierung ist falsch [#9167](https://github.com/NuGet/Home/issues/9167)

* Restore: packagespec. Clone () erstellt ungleiche Klon- [#9211](https://github.com/NuGet/Home/issues/9211)

* Die Fehlerliste wird angezeigt, wenn die Option "immer Fehlerliste anzeigen, wenn der Build mit Fehlern abgeschlossen ist" nicht aktiviert ist [#8190](https://github.com/NuGet/Home/issues/8190)

* Die statische Graph-Wiederherstellung sollte kein leeres SolutionPath- [#9061](https://github.com/NuGet/Home/issues/9061) bestehen.

* Restore: für jedes Projekt 4 mal berechnete Abschlüsse- [#9042](https://github.com/NuGet/Home/issues/9042)

* Restore: dependencygraphspec. Load (...) benötigt keine jobject- [#9040](https://github.com/NuGet/Home/issues/9040)

* Restore: große Zeichen folgen, die auf dem großen Objekt Heap (Loh) erstellt wurden, [#9031](https://github.com/NuGet/Home/issues/9031)

* Benutzerdefinierte nuget.exe in neuerem Mono kann aufgrund des MSBuild-SDK-Resolvers unterbrechen- [8848](https://github.com/NuGet/Home/issues/8848)

* Restore schlägt fehl, wenn nuget.dgspec.json "von einem anderen Prozess verwendet wird"- [8692](https://github.com/NuGet/Home/issues/8692)

**DCRs**

* Die Logik in _GetRestoreProjectStyle sollte in einer Aufgabe [#8804](https://github.com/NuGet/Home/issues/8804)

* Standardmäßig veraltete Informationen auf der Registerkarte "installiert" hinzufügen [#8541](https://github.com/NuGet/Home/issues/8541)

**[Liste aller Probleme, die in dieser Version behoben wurden: 5,5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**
