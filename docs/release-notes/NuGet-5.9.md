---
title: Versionshinweise zu NuGet 5.9
description: Versionshinweise für NuGet 5.9, einschließlich neuer Features, Fehlerbehebungen und DCRs.
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 50fd277a4f1f39b4a68a89cd07af4e21f0d3d831
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508812"
---
# <a name="nuget-59-release-notes"></a>Versionshinweise zu NuGet 5.9

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version | Verfügbar in .NET SDK(s) |
|:---|:---|:---|
| [**5.9.0**](https://nuget.org/downloads) | [Visual Studio 2019 Version 16.9](https://visualstudio.microsoft.com/downloads/) | [5.0.200](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.9.1**](https://nuget.org/downloads) | [Visual Studio 2019 Version 16.9](https://visualstudio.microsoft.com/downloads/) | [5.0.202](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> Installiert mit Visual Studio 2019 mit .NET Core-Workload
  
> [!NOTE]
> Visual Studio 16.9, MSBuild 16.9 und .NET 5.0.200 und höher erfordert NuGet.exe 5.9 oder höher.

## <a name="summary-whats-new-in-59"></a>Zusammenfassung: Neuerungen in 5.9

* Hinzufügen des Kontextmenüelements "Aktualisieren" für Paketabhängigkeiten, das Paket-Manager Benutzeroberfläche mit vorab ausgewählten Zu aktualisierenden Paketen startet – [#10378](https://github.com/NuGet/Home/issues/10378)

    ![Aktualisieren des Pakets mit der rechten Maustaste](media/releasenotes-59-update.png)

* Zeigen Sie die angeforderte Version (einschließlich unverankerte Version oder Versionsbereichsanforderung) in der Spalte "Version" der Projektliste auf Projektmappenebene Paket-Manager Ui an – [#9827](https://github.com/NuGet/Home/issues/9827)

    ![Angeforderte Version auf Projektmappenebene Paket-Manager Benutzeroberfläche](media/releasenotes-59-requested-version.png)

* IntelliCode-Paketvorschläge auf der Registerkarte "Durchsuchen" der Paket-Manager Benutzeroberfläche, die als A/B-Test veröffentlicht wurde [– #10053](https://github.com/NuGet/Home/issues/10053)

* Erweitern Sie die `.nupkg.metadata` Datei so, dass sie die Installationsquelle enthält [– #10354](https://github.com/NuGet/Home/issues/10354)

* Einführung einer neuen msbuild-Eigenschaft zum Ausschließen der Buildausgabe für bestimmte TFMs während der Packaufgabe [– #10396](https://github.com/NuGet/Home/issues/10396)

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

**DCRs (Design Change Request):**

* Das Symbol "Nach unten" ist nicht intuitiv, wenn die neueste Paketversion installiert ist. Der alte grüne Teilstrich war perfekt [– #9789](https://github.com/NuGet/Home/issues/9789)

* Ausführlichkeit des NuGet-Debuggens sollte sagen, woher ein Paket stammt – [#3055](https://github.com/NuGet/Home/issues/3055)

* NuGet-Paket sollte falsches Auslassen des Punkts in Versionsnummern abfangen [– #9215](https://github.com/NuGet/Home/issues/9215)

* [CPVM] Deaktivieren des Anheftens der zentralen transitiven Abhängigkeiten [– #10132](https://github.com/NuGet/Home/issues/10132)

* net5 TFM: Fehler bei fehlendem TPV erzeugen – [#9441](https://github.com/NuGet/Home/issues/9441)

* Protokollpaketinhalthash während der Wiederherstellungsprotokollierung (während der [Extraktion)](https://github.com/NuGet/Home/issues/10384) – #10384

* Implementieren Sie einen Vorregistrierungsmechanismus für ältere PR-Projekte, die die Wiederherstellung bei geöffneter [Projektmappe aufrufen – #9986](https://github.com/NuGet/Home/issues/9986)

* Das NuGet-Paket recommender sollte funktionieren, wenn im Paket-Manager mehrere Quellen ausgewählt [sind– #10433](https://github.com/NuGet/Home/issues/10433)

* Protokollieren Sie bei der Wiederherstellung bei normaler Ausführlichkeit, von welcher Quelle ein Paket wiederhergestellt wird– [#10461](https://github.com/NuGet/Home/issues/10461)

**Fehler:**

* INuGetPackageFileService: Abrufen von Images und eingebetteten Lizenzen [](https://github.com/NuGet/Home/issues/10151) für mit Codespaces verbundene und eigenständige #10151

* VS OE: IProjectMetadataContextInfo missing formatter - [#10079](https://github.com/NuGet/Home/issues/10079)

* [CPVM-Perf] Reduzieren der in centralTransitiveDependencyGroups geschriebenen Informationen [– #10002](https://github.com/NuGet/Home/issues/10002)

* Wiederherstellungsvorgänge, die aufgrund eines nicht geladenen Projekts auslösen, werden `NoOp` als in Telemetriedaten [gemeldet – #9985](https://github.com/NuGet/Home/issues/9985)

* Symbole mit bestimmten Farbpaletten verursachen einen Absturz der PM-Benutzeroberfläche in VS [– #10037](https://github.com/NuGet/Home/issues/10037)

* [CPVM-Perf] Reduzieren des PackageSpec-Klons beim Hinzufügen der CPVM-Informationen [– #10003](https://github.com/NuGet/Home/issues/10003)

* PM UI – asyncify icon loading – [#10009](https://github.com/NuGet/Home/issues/10009)

* Verzögerung der Benutzeroberfläche beim Laden von Symbol-URLs in der PM-Benutzeroberfläche [– #8505](https://github.com/NuGet/Home/issues/8505)

* Threadaffinität in BitmapSource- und WPF-Benutzeroberflächenthreads [– #9161](https://github.com/NuGet/Home/issues/9161)

* Warnung für warnung NU5128, wenn packastool mit Targetframework-Alias [– #10097](https://github.com/NuGet/Home/issues/10097)

* OutputPath-Logik in Packzielen in einem benutzerdefinierten Build funktioniert nicht ordnungsgemäß [– #9234](https://github.com/NuGet/Home/issues/9234)

* VS OE: Zwischenspeichern der IServiceBroker-Instanz auf dem Client [– #10141](https://github.com/NuGet/Home/issues/10141)

* Erstellen von NuGetProjectActions für die Deinstallation über die PM-Benutzeroberfläche als parallelen Vorgang [– #9956](https://github.com/NuGet/Home/issues/9956)

* Leistung: Reduzieren von UIDelays in GetPackageSpecsAsync für Legacy- und Nicht-PR-Projekte [– #9953](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg`` pusht nicht mehr als eine Datei [– #4393](https://github.com/NuGet/Home/issues/4393)

* Die Ausgabe wird unter macOS mit 80 Zeichen umschlossen, wenn sie umgeleitet wird [– #10198](https://github.com/NuGet/Home/issues/10198)

* Fehler bei der Wiederherstellung mit -Source <Relative Path>  -  [#9406](https://github.com/NuGet/Home/issues/9406)

* netcoreapp5.0-windows führt keinen Roundtrip durch und analysiert keine Plattforminformationen [– #10177](https://github.com/NuGet/Home/issues/10177)

* Für benutzerdefinierte CPS-Projekte ist eine AssemblyReferences-Projektfunktion erforderlich, um die Wiederherstellung zu ermöglichen. - [#8071](https://github.com/NuGet/Home/issues/8071)

* Bei der Überprüfung des Vorhandenseins von Lizenz- und Symboldateien sollte immer die Groß-/Kleinschreibung beachtet [werden – #9817](https://github.com/NuGet/Home/issues/9817)

* DotnetCLiToolReference-Wiederherstellungen erschweren die Ursachen für die Anzahl von No-Op-Projekten/uptodateprojectscount – [#10038](https://github.com/NuGet/Home/issues/10038)

* Das Bindestrichfeld des Paketformats ist schwer zu sehen, wenn Sie über die Registerkarte im Dialogfeld "NuGet Paket-Manager Format auswählen" unter Dunkles Design navigieren : [#9729](https://github.com/NuGet/Home/issues/9729)

* Ausschließen transitiver Frameworkverweise aus `CollectFrameworkReferences`  -  [#10314](https://github.com/NuGet/Home/issues/10314)

* Statische Comparer-Eigenschaften sollten idempotent sein [– #10339](https://github.com/NuGet/Home/issues/10339)

* Auflösen des Ladens interner Verträge (Korrigieren von RPS oder Abrufen einer Ausnahme) – [#9919](https://github.com/NuGet/Home/issues/9919)

* Ersetzen Von GetService durch GetServiceAsync in NuGet.Clients, Teil 1: [#10362](https://github.com/NuGet/Home/issues/10362)

* Cli-Installationen sollten nicht aufgelistete Pakete nicht installieren [– #7466](https://github.com/NuGet/Home/issues/7466)

* Statische MsBuild-Graphwiederherstellung – unnötige Protokollierung über MSBuildStartupDirectory [– #10335](https://github.com/NuGet/Home/issues/10335)

* Project Dependencies of ProjectReferences marked as PrivateAssets should not be included in the lock file up to date check - [#8565](https://github.com/NuGet/Home/issues/8565)

* SDK-Projekte mit fehlerhaften Daten ohne Wiederherstellungsfehler in VS – [#10406](https://github.com/NuGet/Home/issues/10406)

* NU1004 beim Wiederherstellen einer Projektmappe mit gemischten Legacy- und netstandard2-Projekten aus der Befehlszeile mit LockedMode – [#9623](https://github.com/NuGet/Home/issues/9623)

* Das Paket enthält Inhalte, die über Abhängigkeitspakete in das Paket des aktuellen Projekts (nur SDK-basierte Projekte) integriert werden – [#8867](https://github.com/NuGet/Home/issues/8867)

* Hinzufügen von Telemetriedaten für Fehler in der VS-Erweiterbarkeits-API von NuGet [– #10062](https://github.com/NuGet/Home/issues/10062)

* Fügen Sie GenerateRestoreGraphFile in der statischen Graphwiederherstellung hinzu, um die Debugbarkeit zu verbessern.  - [#10365](https://github.com/NuGet/Home/issues/10365)

* Der NuGet-Paket-Manager kann nicht geöffnet [werden – #10336](https://github.com/NuGet/Home/issues/10336)

* NVDA/Sprachausgabe liest die Bezeichnung "Lizenz" für den Link "Apache-2.0" nicht – [#10425](https://github.com/NuGet/Home/issues/10425)

* Die aktuelle Statusleistenmeldung ist in [](https://github.com/NuGet/Home/issues/9402) VS - #9402

* packages.config package.lock.json verwendet ein falsches Zielframework [– #10257](https://github.com/NuGet/Home/issues/10257)

* Codespaces: Beheben von Telemetriedaten https://github.com/NuGet/NuGet.Client/pull/3786  -  [#10439](https://github.com/NuGet/Home/issues/10439)

* Fehler NU1004 wird beim Erstellen der Projektmappe nach dem Aktivieren von "RestoreLockedMode" nicht mehr angezeigt [– #8973](https://github.com/NuGet/Home/issues/8973)

* Wenn Sie die PMUI in umgekehrter Richtung mit der Tabulatoren-TASTE verwenden, sollte die Vorwärtsrichtung [gespiegelt](https://github.com/NuGet/Home/issues/10234) werden – #10234

* Das Debuggen von PMUI in einer experimentellen Instanz löst manchmal InvalidCastException aus SolutionView in ProjectView [#10416](https://github.com/NuGet/Home/issues/10416)

* Die Standardversion ist NULL, nachdem Sie auf der Registerkarte Durchsuchen auf ein veraltetes Paket geklickt [#10380](https://github.com/NuGet/Home/issues/10380)

* Der NuGet-Manager in Visual Studio erneut geladen, wenn der Fokus wiedererlangt wird [– #4176](https://github.com/NuGet/Home/issues/4176)

* Entfernen von IPackageSourceProvider2 und zugehörigen Typen [– #10098](https://github.com/NuGet/Home/issues/10098)

* Das Paket "NameOfPackage" ist mit "all"-Frameworks im Projekt nicht kompatibel – [#5127](https://github.com/NuGet/Home/issues/5127)

* CreateVersionsAsync führt unnötige NuGetVersion-Vergleiche durch [– #10436](https://github.com/NuGet/Home/issues/10436)

* NuGet.Client sollte die Verwendung von ManagedImageMonikers durch KnownMonikers ersetzen [– #9977](https://github.com/NuGet/Home/issues/9977)

* Das veraltete Symbol überschneidet sich mit der Version des veralteten Pakets auf der Registerkarte Durchsuchen – [#10452](https://github.com/NuGet/Home/issues/10452)

* Die Fehlerbehandlung für PackageReference NU1604 unterscheidet sich in VS und befehlszeilenübergreifend (& Paket-Manager Benutzeroberfläche wiederherstellen) [– #9289](https://github.com/NuGet/Home/issues/9289)

* Codespaces: erforderliche Formatierer, die nicht registriert sind [– #10467](https://github.com/NuGet/Home/issues/10467)

* Entfernen von net45 als Zielframework aus NuGet.Frameworks [– #10470](https://github.com/NuGet/Home/issues/10470)

* Implementierung: Fügen Sie neue Telemetriedaten hinzu, um Ereignisse im Zusammenhang mit der PMC- und PowerShell-Nutzung nachzuverfolgen. - [#10142](https://github.com/NuGet/Home/issues/10142)

* Im Fenster Vorschau der Änderungen wird nur ein Paket angezeigt, wenn mehrere Pakete auf der Paket-Manager-Benutzeroberfläche aktualisiert werden können – [#10483](https://github.com/NuGet/Home/issues/10483)

* Leere frameworkReferences-Gruppen sollten beim Packen von Projekten mit mehreren Zielzielen generiert werden – [#10218](https://github.com/NuGet/Home/issues/10218)

* Das Kontrollkästchen des Pakets auf der Registerkarte "Updates" ist mit einem Bindestrichfeld gekennzeichnet, wenn die Navigation durch die Registerkarte in Blau/Blau (zusätzlicher Kontrast)/Helle Designs erfolgt – [#8963](https://github.com/NuGet/Home/issues/8963)

* Registerkarte "Updates" Kontrollkästchen funktionieren für Sprachausgaben nicht gut – [#10449](https://github.com/NuGet/Home/issues/10449)

* Das Aktualisieren in PMUI bewirkt, dass der Objektverweis nicht auf eine Instanz eines Objekts festgelegt ist [– #9882](https://github.com/NuGet/Home/issues/9882)

* Implementierung: Fügen Sie neue Telemetriedaten hinzu, um Ereignisse im Zusammenhang mit der Nachverfolgung der PMC- und PowerShell-Nutzung nachzuverfolgen. - [#10478](https://github.com/NuGet/Home/issues/10478)

* Kopier-/Einfügefehler in V2FeedPackageInfo [– #10480](https://github.com/NuGet/Home/issues/10480)

* Korrektur von NuGetPackageFileService: Verwenden von für verwerfbare Speicherstreams [– #10503](https://github.com/NuGet/Home/issues/10503)

**[Liste aller in diesem Release behobenen Probleme: 5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[Liste der Commits in diesem Release: 5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>Beiträge aus der Community

Vielen Dank an alle Mitwirkenden, die dieses NuGet-Release super gemacht haben!

|Wer|Prs|Probleme|
|----|----|----|
[omajid](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | Fehler beim Kopieren und Einfügen in V2FeedPackageInfo [– #10480](https://github.com/NuGet/Home/issues/10480)
[automatisch in-krys wies zu](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | Fehlende Tests für den Fall, dass auf Pakete mit dem PrivateAssets="All"-Attribut verwiesen wird [– #10397](https://github.com/NuGet/Home/issues/10397)
[automatisch in-krys wies zu](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | Hinzufügen von Unterstützung für das Pushen mehrerer Pakete [– #4393](https://github.com/NuGet/Home/issues/4393)
[bei -krysizec](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | Die Erstellung von NuGet-Bibliotheken ist unterbrochen, wenn die Assemblysignatur deaktiviert ist [– #10173](https://github.com/NuGet/Home/issues/10173)
[seit 2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | Bereinige die beitragenden Dokumente [– #10399](https://github.com/NuGet/Home/issues/10399)
[Solldavid](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | Bei der Überprüfung des Vorhandenseins von Lizenz- [](https://github.com/NuGet/Home/issues/9817) und Symboldatei sollte immer zwischen Schreibung und #9817
[besau](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | Verwenden Sie BitmapCreateOptions.IgnoreColorProfile, um das WPF-Problem zu umgehen, wenn DecodePixelWidth - [#10037](https://github.com/NuGet/Home/issues/10037)
[bjorkstromm](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | Windows SDK 10-Link im NuGet.Client Contribution guide - [#10099](https://github.com/NuGet/Home/issues/10099)
[bjorkstromm](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | Relative Links sind im NuGet.Client-Debughandbuch fehlerhaft [– #10100](https://github.com/NuGet/Home/issues/10100)
[Nirmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | Verbessern von Testvorrichtungen und zugehörigem Code – [#9996](https://github.com/NuGet/Home/issues/9996)
[beimbjarne](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | Die Ausgabe wird unter macOS mit 80 Zeichen umschlossen, wenn sie umgeleitet wird [– #10198](https://github.com/NuGet/Home/issues/10198)
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | Verfügbarmachen von NuGet.PackageManagement als .NET Standard-Paket [– #6150](https://github.com/NuGet/Home/issues/6150)
[Anipik](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | Einführung einer neuen msbuild-Eigenschaft zum Ausschließen der Buildausgabe für bestimmte tfms während der Packaufgabe [– #10396](https://github.com/NuGet/Home/issues/10396)

## <a name="summary-whats-new-in-591"></a>Zusammenfassung: Neuerungen in 5.9.1

* "dotnet nuget remove source nuget.org" funktioniert nicht zum ersten Mal – [#10745](https://github.com/NuGet/Home/issues/10745)
* Deaktivieren der Standardvalidierung unter Linux, aber standardmäßig unter Windows aktiviert – [#10713](https://github.com/NuGet/Home/issues/10713)

**[Liste aller in diesem Release behobenen Probleme: 5.9.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f42efd068017639b4036)**

**[Liste der Commits in dieser Version – 5.9.1](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.9.1.8)**

## <a name="feedback-welcome"></a>Feedback willkommen

Ihr Feedback ist uns sehr wichtig.  Wenn probleme mit dieser Version auftreten, überprüfen Sie unsere [GitHub-Probleme,](https://github.com/NuGet/Home/issues) und [Visual Studio-Entwicklercommunity](https://developercommunity.visualstudio.com/) auf vorhandene Probleme.  Melden Sie bei neuen Problemen in NuGet ein [GitHub-Problem.](https://github.com/NuGet/Home/issues/new)
Informieren Sie uns bei allgemeinen Problemen [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) mit NuGet über die Option Problem melden in Ihrer bevorzugten IDE unter Hilfe > **Problem melden.**
