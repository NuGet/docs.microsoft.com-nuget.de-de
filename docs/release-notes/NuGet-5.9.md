---
title: Anmerkungen zu dieser Version von nuget 5,9
description: Anmerkungen zu dieser Version von nuget 5,9, einschließlich neuer Features, Fehlerbehebungen und dcrs.
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 24933ebb51851da2583b03e7fd3e55fade5e8a18
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859530"
---
# <a name="nuget-59-release-notes"></a>Anmerkungen zu dieser Version von nuget 5,9

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version | Verfügbar in .NET SDK(s) |
|:---|:---|:---|
| [**5.9**](https://nuget.org/downloads) | [Visual Studio 2019, Version 16,9](https://visualstudio.microsoft.com/downloads/) | [5,0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> installiert mit Visual Studio 2019 mit .net Core-Arbeitsauslastung
  
> [!NOTE]
> Für Visual Studio 16,9, MSBuild 16,9 und .net 5.0.3 + ist NuGet.exe 5,9 oder höher erforderlich.

## <a name="summary-whats-new-in-59"></a>Zusammenfassung: Neues in 5,9

* Fügen Sie das Kontextmenü Element "Aktualisieren" für Paketabhängigkeiten hinzu, die die Benutzeroberfläche des Paket-Managers mit vorab ausgewählten Paketen zum Aktualisieren starten- [#10378](https://github.com/NuGet/Home/issues/10378)

    ![Klicken Sie mit der rechten Maustaste auf Paket "Aktualisieren".](media/releasenotes-59-update.png)

* Zeigt die angeforderte Version (einschließlich der unverankerten Version oder Versions Bereichs Anforderung) in der Spalte "Version" der Projektliste in der Benutzeroberfläche des Paket-Managers auf Projektmappenebene an [#9827](https://github.com/NuGet/Home/issues/9827)

    ![Angeforderte Version in der Paket-Manager-Benutzeroberfläche](media/releasenotes-59-requested-version.png)

* Intellicode-Paket Vorschläge auf der Registerkarte "Benutzeroberfläche Durchsuchen" des Paket-Managers als A/B-Test- [#10053](https://github.com/NuGet/Home/issues/10053)

* Erweitern `.nupkg.metadata` Sie die Datei, sodass Sie die Installationsquelle enthält [#10354](https://github.com/NuGet/Home/issues/10354)

* Führen Sie eine neue MSBuild-Eigenschaft ein, um die Buildausgabe für bestimmte tfms während Pack-Task- [#10396](https://github.com/NuGet/Home/issues/10396) auszuschließen.

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

**Dcrs (Entwurfs Änderungs Anforderung):**

* Das Symbol "nach unten" ist nicht intuitiv, wenn die neueste Paketversion installiert ist. Der alte grüne Tick war perfekt [#9789](https://github.com/NuGet/Home/issues/9789)

* "Nuget-debugausführlichkeit" sollte sagen, wo ein Paket stammt [#3055](https://github.com/NuGet/Home/issues/3055)

* Das nuget-Paket sollte das falsche Weglassen des Punkts in Versionsnummern erfassen- [#9215](https://github.com/NuGet/Home/issues/9215)

* [Cpvm] Deaktivieren Sie das Fixieren der zentralen transitiven Abhängigkeiten [#10132](https://github.com/NuGet/Home/issues/10132)

* net5 TFM: Fehler beim fehlendem TPV- [#9441](https://github.com/NuGet/Home/issues/9441)

* Protokoll Paket Konflikt während der Wiederherstellung der Protokollierung (während der Extraktion)- [#10384](https://github.com/NuGet/Home/issues/10384)

* Implementieren Sie einen Mechanismus vor der Registrierung für ältere PR-Projekte, die Restore in Solution Open- [#9986](https://github.com/NuGet/Home/issues/9986)

* Der nuget-Paket-Empfehlungs Dienst sollte funktionieren, wenn im Paket-Manager mehr als eine Quelle ausgewählt ist [#10433](https://github.com/NuGet/Home/issues/10433)

* Beim Wiederherstellen bei normaler Ausführlichkeit protokollieren Sie die Quelle, von der ein Paket wieder hergestellt wird [#10461](https://github.com/NuGet/Home/issues/10461)

**K**

* Inugetpackagefileservice: Abrufen von Images und eingebetteten Lizenzen für mit codespaces verbundene und eigenständige [#10151](https://github.com/NuGet/Home/issues/10151)

* VS OE: IProjectMetadataContextInfo fehlendes Formatierer- [#10079](https://github.com/NuGet/Home/issues/10079)

* [Cpvm-perf] Reduzieren Sie die Informationen, die in centraltransitivedependencygroups geschrieben werden [#10002](https://github.com/NuGet/Home/issues/10002)

* Wiederherstellungs Vorgänge, die aufgrund eines nicht geladenen Projekts ausgelöst werden, werden als `NoOp` in der Telemetrie gemeldet [#9985](https://github.com/NuGet/Home/issues/9985)

* Symbole mit bestimmten Farbpaletten verursachen einen Absturz der PM-Benutzeroberfläche im Vergleich zu [#10037](https://github.com/NuGet/Home/issues/10037)

* [Cpvm-perf] Reduzieren Sie den "packagespec"-Klon beim Hinzufügen der cpvm-Informationen [#10003](https://github.com/NuGet/Home/issues/10003)

* PM UI-asyncify Icon Load- [#10009](https://github.com/NuGet/Home/issues/10009)

* UI-Verzögerung beim Laden von Symbol-URLs in der PM-Benutzeroberfläche [#8505](https://github.com/NuGet/Home/issues/8505)

* Thread Affinität in BitmapSource-und WPF-UI-Threads- [#9161](https://github.com/NuGet/Home/issues/9161)

* Warnung für Warnung NU5128 wenn packastool mit TargetFramework-Alias- [#10097](https://github.com/NuGet/Home/issues/10097)

* Die OutputPath-Logik in Paket Zielen in einem angepassten Build funktioniert nicht ordnungsgemäß [#9234](https://github.com/NuGet/Home/issues/9234)

* VS OE: IService Broker-Instanz auf Client- [#10141](https://github.com/NuGet/Home/issues/10141) Zwischenspeichern

* Erstellen von nugetprojectactions für die Deinstallation von der PM-Benutzeroberfläche a parallel Operation- [#9956](https://github.com/NuGet/Home/issues/9956)

* Leistung: verringern Sie uiverzögerungen in getpackagespecsasync für Legacy Projekte und nicht-PR-Projekte- [#9953](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg`` überträgt nicht mehr als eine Datei [#4393](https://github.com/NuGet/Home/issues/4393)

* Die Ausgabe wird bei umgeleitetem [#10198](https://github.com/NuGet/Home/issues/10198) um 80 Zeichen in macOS umschließt.

* Restore schlägt mit-Source- <Relative Path>  -  [#9406](https://github.com/NuGet/Home/issues/9406) fehl

* netcoreapp 5.0-Windows führt kein Roundtrip aus und analysiert Platt Form Informationen nicht [#10177](https://github.com/NuGet/Home/issues/10177)

* Für benutzerdefinierte CPS-Projekte ist AssemblyReferences-Projekt Funktion erforderlich, um wieder hergestellt zu werden. - [#8071](https://github.com/NuGet/Home/issues/8071)

* Die Überprüfung der vorhanden sein von Lizenz-und Symbol Dateien sollte immer einen Vergleich mit Unterscheidung nach Groß- [#9817](https://github.com/NuGet/Home/issues/9817)

* Durch die Wiederherstellung von dotnetclitoolreference ist es schwierig, die Anzahl von No-op-Projekten/uptodateprojectioncount- [#10038](https://github.com/NuGet/Home/issues/10038)

* Es ist schwierig, das Feld "Strich Zeile" des Paket Formats zu sehen, wenn Sie mit der Registerkarte im Dialogfeld "nuget-Paket-Manager [#9729](https://github.com/NuGet/Home/issues/9729) -Format auswählen" im Design "dunkel"

* Transitiv frameworkverweise aus `CollectFrameworkReferences`  -  [#10314](https://github.com/NuGet/Home/issues/10314) ausschließen

* Statische Comparer-Eigenschaften müssen idempotent sein [#10339](https://github.com/NuGet/Home/issues/10339)

* Auflösen des assemblyladens interner Verträge (Beheben von RPS-oder Get-Ausnahmen)- [#9919](https://github.com/NuGet/Home/issues/9919)

* Ersetzen Sie "GetService" durch "getserviceasync" in "nuget. Clients", Teil 1- [#10362](https://github.com/NuGet/Home/issues/10362)

* CLI-Installationen dürfen nicht aufgelistete Pakete nicht installieren- [#7466](https://github.com/NuGet/Home/issues/7466)

* Statische MSBuild-Diagramm Wiederherstellung: nicht erforderliche Protokollierung über msbuildstartupdirectory- [#10335](https://github.com/NuGet/Home/issues/10335)

* Projekt Abhängigkeiten von ProjectReferences, die als privateassets gekennzeichnet sind, dürfen nicht in die Aktualisierungs Datei der Sperrdatei eingefügt werden [#8565](https://github.com/NuGet/Home/issues/8565)

* SDK-Projekte mit ungültigen Daten, die keine Wiederherstellungs Fehler in vs- [#10406](https://github.com/NuGet/Home/issues/10406) zeigen

* NU1004 beim Wiederherstellen einer Projekt Mappe, die über gemischte Legacy-und netstandard2-Projekte aus der cmd-Zeile mit lockedmode- [#9623](https://github.com/NuGet/Home/issues/9623)

* Pack enthält Inhalte, die über Abhängigkeits Pakete in das Paket des aktuellen Projekts eingefügt werden (nur SDK-basierte Projekte)- [#8867](https://github.com/NuGet/Home/issues/8867)

* Hinzufügen von Telemetriedaten für nuget-vs-Erweiterbarkeits-API-Fehler- [#10062](https://github.com/NuGet/Home/issues/10062)

* Fügen Sie generaterestoregraphfile in static Graph Restore hinzu, um die debugability zu verbessern.  - [#10365](https://github.com/NuGet/Home/issues/10365)

* Der nuget-Paket-Manager kann nicht geöffnet werden [#10336](https://github.com/NuGet/Home/issues/10336)

* NVDA/Sprachausgabe liest nicht die Bezeichnung "License" für "Apache-2,0" Link- [#10425](https://github.com/NuGet/Home/issues/10425)

* Die Status leisten Meldung "aktuell" ist in vs- [#9402](https://github.com/NuGet/Home/issues/9402) nicht hervorragend.

* packages.config package.lock.json verwendet ein falsches Ziel Framework- [#10257](https://github.com/NuGet/Home/issues/10257)

* Codespaces: Beheben von Telemetriedaten aus https://github.com/NuGet/NuGet.Client/pull/3786  -  [#10439](https://github.com/NuGet/Home/issues/10439)

* Fehler NU1004 bei der Erstellung der Projekt Mappe nach dem Aktivieren von "restorelockedmode" nicht mehr: [#8973](https://github.com/NuGet/Home/issues/8973)

* Durch die Tab-Taste durch PMUI in umgekehrter Richtung sollte die Vorwärtsrichtung gespiegelt werden [#10234](https://github.com/NuGet/Home/issues/10234)

* Beim Debuggen von PMUI in der experimentellen Instanz wird manchmal InvalidCastException von solutionview zu projectview- [#10416](https://github.com/NuGet/Home/issues/10416)

* Die Standardversion ist NULL, nachdem Sie auf ein veraltes Paket auf der Registerkarte Durchsuchen geklickt haben [#10380](https://github.com/NuGet/Home/issues/10380)

* Der nuget-Manager in Visual Studio wird erneut geladen, wenn der Fokus wieder hergestellt wird [#4176](https://github.com/NuGet/Home/issues/4176)

* IPackageSourceProvider2 und verwandte Typen entfernen- [#10098](https://github.com/NuGet/Home/issues/10098)

* Das Paket "nameof Package" ist mit "All"-Frameworks in Project- [#5127](https://github.com/NuGet/Home/issues/5127) nicht kompatibel.

* "Kreateversionsasync" führt unnötige nugetversion-Vergleiche aus- [#10436](https://github.com/NuGet/Home/issues/10436)

* "Nuget. Client" sollte die Verwendung von "managedimagemoniker" durch "knownmonikers- [#9977](https://github.com/NuGet/Home/issues/9977) ersetzen.

* Das veraltete Symbol überlappt mit der Version des veralteten Pakets auf der Registerkarte "Durchsuchen" [#10452](https://github.com/NuGet/Home/issues/10452)

* Packagereferenzierung NU1604 die Fehlerbehandlung ist in vs und in der Befehlszeile (Restore &-Paket-Manager-Benutzeroberfläche) unterschiedlich [#9289](https://github.com/NuGet/Home/issues/9289)

* Codespaces: erforderliche Formatierer nicht registriert- [#10467](https://github.com/NuGet/Home/issues/10467)

* Entfernen Sie net45 AS als Ziel Framework aus "nuget. Frameworks- [#10470](https://github.com/NuGet/Home/issues/10470) ".

* Implementierung: Fügen Sie neue telemetrien hinzu, um Ereignisse im Zusammenhang mit PMC und PowerShell-Nutzung zu verfolgen. - [#10142](https://github.com/NuGet/Home/issues/10142)

* Im Fenster "Vorschau der Änderungen" wird nur ein Paket angezeigt, wenn mehrere Pakete zur Aktualisierung in der Benutzeroberfläche des Paket-Managers verfügbar sind. [#10483](https://github.com/NuGet/Home/issues/10483)

* Beim Packen von multizielgerichteten Projekten sollten leere frameworkreferences-Gruppen generiert werden [#10218](https://github.com/NuGet/Home/issues/10218)

* Es ist schwierig, das Kontrollkästchen des Pakets auf der Registerkarte "Updates" zu sehen, wenn Sie mit der Tab-Taste in blau/blau (zusätzlicher Kontrast)/Light Themes- [#8963](https://github.com/NuGet/Home/issues/8963)

* Die Kontrollkästchen für die Registerkarte "Updates" funktionieren nicht gut mit Bildschirmlesern- [#10449](https://github.com/NuGet/Home/issues/10449)

* Das Aktualisieren in PMUI bewirkt, dass der Objekt Verweis nicht auf eine Instanz eines Objekts festgelegt ist [#9882](https://github.com/NuGet/Home/issues/9882)

* Implementierung: Fügen Sie neue telemetrien hinzu, um Ereignisse im Zusammenhang mit PMC und PowerShell-Verwendungs Nachverfolgung zu verfolgen. - [#10478](https://github.com/NuGet/Home/issues/10478)

* Kopier-/Einfüge Fehler in V2FeedPackageInfo- [#10480](https://github.com/NuGet/Home/issues/10480)

* Nugetpackagefileservice-Korrektur: Verwendung von für verwerfbaren MemoryStream- [#10503](https://github.com/NuGet/Home/issues/10503)


**[Liste aller in dieser Version behobene Probleme 5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[Liste der Commits in dieser Version-5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>Beiträge aus der Community

Vielen Dank für alle Mitwirkenden, die dazu beigetragen haben, dass diese nuget-Version großartig ist!

|Wer|PRS|Probleme|
|----|----|----|
[omajid](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | Kopier-/Einfüge Fehler in V2FeedPackageInfo- [#10480](https://github.com/NuGet/Home/issues/10480)
[Marcin-krystianc](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | Fehlende Tests für den Fall, dass auf Pakete mit privateassets = "All"-Attribut verwiesen wird [#10397](https://github.com/NuGet/Home/issues/10397)
[Marcin-krystianc](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | Hinzufügen von Unterstützung für das übertragen mehrerer Pakete [#4393](https://github.com/NuGet/Home/issues/4393)
[Marcin-krystianc](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | Das Erstellen von nuget-Bibliotheken ist beschädigt, wenn die Assemblysignierung deaktiviert ist [#10173](https://github.com/NuGet/Home/issues/10173)
[kant2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | Bereinigen Sie die zugehörigen Dokumente [#10399](https://github.com/NuGet/Home/issues/10399)
[Pathogendavid](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | Die Überprüfung der vorhanden sein von Lizenz-und Symbol Dateien sollte immer einen Vergleich mit Unterscheidung nach Groß- [#9817](https://github.com/NuGet/Home/issues/9817)
[Groß-und-her](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | Verwenden Sie bitmapkreateoptions. ignorecolorprofile, um das WPF-Problem zu umgehen, wenn Sie DecodePixelWidth- [#10037](https://github.com/NuGet/Home/issues/10037)
[bjorkstromm](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | Der Link "Windows SDK 10" ist in nuget beschädigt. Leitfaden für den Client Beitrag- [#10099](https://github.com/NuGet/Home/issues/10099)
[bjorkstromm](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | Relative Verknüpfungen werden in nuget getrennt. clientdebughandbuch- [#10100](https://github.com/NuGet/Home/issues/10100)
[Nirmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | Verbessern von Test Vorrichtungen und zugehöriger Code- [#9996](https://github.com/NuGet/Home/issues/9996)
[Rolf Bjarne](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | Die Ausgabe wird bei umgeleitetem [#10198](https://github.com/NuGet/Home/issues/10198) um 80 Zeichen in macOS umschließt.
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | Stellen Sie "nuget. packagemanagement" als .NET Standard Paket bereit [#6150](https://github.com/NuGet/Home/issues/6150)
[Anipik](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | Führen Sie eine neue MSBuild-Eigenschaft ein, um die Buildausgabe für bestimmte tfms während Pack-Task- [#10396](https://github.com/NuGet/Home/issues/10396) auszuschließen.

## <a name="feedback-welcome"></a>Feedback Willkommen

Ihr Feedback ist uns sehr wichtig.  Wenn bei diesem Release Probleme auftreten, überprüfen Sie unsere [GitHub-Probleme](https://github.com/NuGet/Home/issues) und die [Visual Studio-Entwickler Community](https://developercommunity.visualstudio.com/) auf vorhandene Probleme.  Melden Sie sich bei neuen Problemen in nuget an einem [GitHub-Problem](https://github.com/NuGet/Home/issues/new).
Wenn Sie allgemeine Probleme mit der nuget-Umgebung haben, informieren Sie uns über die Option " [Problem melden](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) " in Ihrer bevorzugten IDE unter **Hilfe > melden Sie ein Problem**.
