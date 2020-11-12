---
title: Anmerkungen zu dieser Version von nuget 5,8
description: Anmerkungen zu dieser Version von nuget 5,8, einschließlich neuer Features, Fehlerbehebungen und dcrs.
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: 86e173b9d760578454df8f5f817533f64e193996
ms.sourcegitcommit: 0cc6ac680c3202d0b036c0bed7910f6709215682
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/12/2020
ms.locfileid: "94550741"
---
# <a name="nuget-58-release-notes"></a>Anmerkungen zu dieser Version von nuget 5,8

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version | Verfügbar in .NET SDK(s) |
|:---|:---|:---|
| [**5.8**](https://nuget.org/downloads) | [Visual Studio 2019, Version 16.8](https://visualstudio.microsoft.com/downloads/) | [5,0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> installiert mit Visual Studio 2019 mit .net Core-Arbeitsauslastung
  
> [!NOTE]
> Für Visual Studio 16,8, MSBuild 16,8 und .net 5,0 ist NuGet.exe 5,8 oder höher erforderlich.


## <a name="summary-whats-new-in-58"></a>Zusammenfassung: Neues in 5,8
🎉 **Dies ist die erste Version, die die Unterstützung für das Erstellen und Wiederherstellen von nuget-Paketen für .net 5,0 bietet** 🎉

* Details zu Paket Sicherheitsrisiken im Detailbereich des Paket-Managers Benutzeroberflächen Paket anzeigen- [#9850](https://github.com/NuGet/Home/issues/9850)

* Überprüfen Sie signierte nuget-Pakete mit dem neuen [`dotnet nuget verify`](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-verify) Befehl [#8051](https://github.com/NuGet/Home/issues/8051)

* [`dotnet add package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) unterstützt `--prerelease` die Option zum Hinzufügen der neuesten Version eines Pakets, einschließlich vorab Versionen [#4699](https://github.com/NuGet/Home/issues/4699)

* Suchen von Paketen in der CLI mit [`nuget.exe search`](https://docs.microsoft.com/nuget/reference/cli-reference/cli-ref-search) Befehls [#9704](https://github.com/NuGet/Home/issues/9704)

* [`dotnet list package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-list-package) Befehl unterstützt `--verbosity` Option- [#9600](https://github.com/NuGet/Home/issues/9600)

* Aktivieren Sie die schnelle No-Op Wiederherstellungs Optimierung für csproj-, packagereferenzierungsbasierte Projekte in Visual Studio [#9565](https://github.com/NuGet/Home/issues/9565)

* Benutzeroberflächen Vorgänge des Paket-Managers auf Projektmappenebene, z. b. Paketinstallationen und Updates, sind bis zu zehnmal schneller [#6010](https://github.com/NuGet/Home/issues/6010)

* Mehrere weitere Leistungsverbesserungen in Visual Studio [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984) [#10052](https://github.com/NuGet/Home/issues/10052), [#9903](https://github.com/NuGet/Home/issues/9903)


### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

**DCRs**

* .Net 5,0 TFM: Framework-Rang folgen Regeln- [#9436](https://github.com/NuGet/Home/issues/9436)

* Nuget sollte die Version der dpi-Plattform nicht ableiten, wenn Sie TargetFramework- [#9842](https://github.com/NuGet/Home/issues/9842) .

* Verwenden Sie TargetFrameworkMoniker & targetplatformmoniker, um die Frameworks zu ableiten, anstatt einzelne TFI-, TFV-, TPI-, TPV-Eigenschaften- [#9895](https://github.com/NuGet/Home/issues/9895)

* Update `GetReferenceNearestTargetFrameworkTask()` zur Unterstützung von Ziel-Frameworks mit Plattformen (z. b. net 5.0-Windows): [#9894](https://github.com/NuGet/Home/issues/9894)

* .Net 5,0 Visual Studio-APIs- [#9650](https://github.com/NuGet/Home/issues/9650)

* Benutzeroberfläche des Paket-Managers: Vorgänge zum konsolidieren oder Aktualisieren von Paketen sollten aufgrund von Fehlern (paketdowngrade usw.) nicht blockiert werden- [#9224](https://github.com/NuGet/Home/issues/9224)

* Nuget-Features sollten für Projekte, die über die Funktion verfügen, bereinigt werden. "Packagereferences"- [#9957](https://github.com/NuGet/Home/issues/9957)

* No-Op Wiederherstellungs Meldungen in Visual Studio unterdrücken- [#6384](https://github.com/NuGet/Home/issues/6384)

**K**

* Der outputwindowtextwriter-Konstruktor sollte nicht im Hintergrund Thread [#9764](https://github.com/NuGet/Home/issues/9764) aufgerufen werden.

* Wiederherstellen von signierten Paketen auf Big-in-CPUs- [#9547](https://github.com/NuGet/Home/issues/9547)

* Outputconsolelogger sollte keine affinitisierten Methoden in MEF-Konstruktoren abrufen- [#9591](https://github.com/NuGet/Home/issues/9591)

* Fehler in der Methode "nuget. commandline. Console" `PrintJustified()` - [#9737](https://github.com/NuGet/Home/issues/9737)

* Benutzeroberflächen-Arbeitsspeicher Fehler beim Paket-Manager, wenn Paket Metadaten aufgrund einer ungültigen Bindung bereinigt werden [#9757](https://github.com/NuGet/Home/issues/9757)

* Schrieben Bei der Installation eines signierten Pakets mit packages.config Format in der Benutzeroberfläche des Paket-Managers wird in Fehlerliste keine Warnung angezeigt [#9798](https://github.com/NuGet/Home/issues/9798)

* "Nuget. commandline. xplat" sollte keine öffentlichen APIs aufweisen [#9821](https://github.com/NuGet/Home/issues/9821)

* Reduzieren Sie Ressourcenkonflikte in der Ladezeit der Projekt Mappe, die durch Blockieren eines Thread Pool Threads mit `BlockingCollection.Take()`  -  [#9822](https://github.com/NuGet/Home/issues/9822)

* In der Befehlszeilen Wiederherstellung mit mehreren zielprojekten sollte nuget die Ziel Framework-bezogenen Informationen aus dem inneren Build lesen [#9869](https://github.com/NuGet/Home/issues/9869)

* Lesen des laufzeitbezeichnerdiagramms über das targetframeworkinformation-Element- [#9874](https://github.com/NuGet/Home/issues/9874)

* Die statische Graph-Wiederherstellung ist im Vergleich zu Visual Studio und regulärer MSBuild-Evaluierungs Wiederherstellung nicht konsistent. [#9881](https://github.com/NuGet/Home/issues/9881)

* Bei der statischen Graph-Wiederherstellung mit mehreren zielprojekten sollte nuget die Ziel Framework-bezogenen Informationen aus dem inneren Build lesen. - [#9870](https://github.com/NuGet/Home/issues/9870)

* `net5.0-platform`Laden und Wiederherstellen von Projekten in Visual Studio zulassen- [#9863](https://github.com/NuGet/Home/issues/9863)

* Anzeigen der aufgelösten Version in der Benutzeroberfläche des Paket-Managers- [#9826](https://github.com/NuGet/Home/issues/9826)

* Benutzeroberfläche des Paket-Managers: Projektmappen-Explorer zeigt nicht alle Abhängigkeiten von nuget-Paketen an [#9898](https://github.com/NuGet/Home/issues/9898)

* Aktualisieren der spdx-Lizenz Liste- [#9946](https://github.com/NuGet/Home/issues/9946)

* VS 2019 stürzt nach dem Öffnen von "nuget-Pakete verwalten" ab: das Symbol bewirkt eine nicht behandelte Ausnahme in Image conversio- [#9696](https://github.com/NuGet/Home/issues/9696)

* "Nuget. Packaging. Extraktion" erfordert "ILMerge", um Newtonsoft.Json- [#9966](https://github.com/NuGet/Home/issues/9966) auszuschließen.

* Das Verpacken mit continuepackingaftergeneratingnuspec = false sollte nicht fehlschlagen, wenn keine Fehler vorliegen [#9786](https://github.com/NuGet/Home/issues/9786)

* Benutzeroberfläche des Paket-Managers: Symbole haben keine ordnungsgemäße Umkehrung der Farben [#10017](https://github.com/NuGet/Home/issues/10017)

* Falsche Projekt Anzahl für aktuelle und No-Op Projekte bei Restore- [#10026](https://github.com/NuGet/Home/issues/10026)

* Die Verwendung von `/p:RestoreUseStaticGraphEvaluation=true` Ergebnissen in value darf nicht NULL sein [#9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` verwendet fälschlicherweise Alias für WPF-Bibliotheks Projekte- [#10020](https://github.com/NuGet/Home/issues/10020)

* Benutzeroberfläche des Paket-Managers: NullReferenceException bei einem Fehler bei der Signatur Überprüfung- [#10042](https://github.com/NuGet/Home/issues/10042)

* Codespaces: Verwenden Sie nicht den `object` Typ für die projektmetadatenwerte- [#10055](https://github.com/NuGet/Home/issues/10055)

* Codespaces: beim Speichern von Paketquellen in den Tools-Optionen werden Anmelde Informationen überschrieben- [#9711](https://github.com/NuGet/Home/issues/9711)


**[Liste aller Probleme, die in dieser Version behoben wurden: 5,8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[Liste der in dieser Version behobene Probleme/Commits-5,8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>Beiträge aus der Community

Vielen Dank für alle Mitwirkenden, die dazu beigetragen haben, dass diese nuget-Version großartig ist!

|Wer|PRS|Probleme|
|----|----|----|
[omajid](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | Typo in Fehlermeldung. "Administration" anstelle von "Administrator"- [#9662](https://github.com/NuGet/Home/issues/9662)
[odalet](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | Das nuget-Paket mit ungültigen AssemblyInformationalVersion-Berichten "Beschreibung ist erforderlich"- [#5548](https://github.com/NuGet/Home/issues/5548)
[Groß-und-her](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` berücksichtigt keine Verzweigungs-und Commit-Eigenschaften- [#9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | Wenn Sie in Visual Studio Fehlerliste Fenster auf Nu-Code klicken, wechseln Sie zu https://docs.microsoft.com/nuget/reference/errors-and-warnings/  -  [#9934](https://github.com/NuGet/Home/issues/9934)
[Chrismaddock](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | Verwenden Sie "https://", wenn Sie neue Paketquelle über Visual Studio-Optionen hinzufügen [#9974](https://github.com/NuGet/Home/issues/9974)
[Therzok](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio` Leistungsproblem bei Mono- [#9989](https://github.com/NuGet/Home/issues/9989)
[thomaslevesque](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | Fügen Sie einen TypeConverter für die semanticversion-Klasse hinzu [#9125](https://github.com/NuGet/Home/issues/9125)


## <a name="feedback-welcome"></a>Feedback Willkommen

Ihr Feedback ist uns sehr wichtig.  Wenn bei diesem Release Probleme auftreten, überprüfen Sie unsere [GitHub-Probleme](https://github.com/NuGet/Home/issues) und die [Visual Studio-Entwickler Community](https://developercommunity.visualstudio.com/) auf vorhandene Probleme.  Melden Sie sich bei neuen Problemen in nuget an einem [GitHub-Problem](hhttps://github.com/NuGet/Home/issues/new).
Wenn Sie allgemeine Probleme mit der nuget-Umgebung haben, informieren Sie uns über die Option " [Problem melden](https://docs.microsoft.com/visualstudio/ide/how-to-report-a-problem-with-visual-studio) " in Ihrer bevorzugten IDE unter **Hilfe > melden Sie ein Problem**.
