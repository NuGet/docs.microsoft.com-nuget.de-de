---
title: 'NuGet 5.8: Anmerkungen zu dieser Version'
description: Versionshinweise für NuGet 5.8, einschließlich neuer Features, Fehlerbehebungen und DCRs.
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: fca9d2d068aadec207bfbf12f3ea82af872825a5
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209929"
---
# <a name="nuget-58-release-notes"></a>NuGet 5.8: Anmerkungen zu dieser Version

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version | Verfügbar in .NET SDK(s) |
|:---|:---|:---|
| [**5.8**](https://nuget.org/downloads) | [Visual Studio 2019, Version 16.8](https://visualstudio.microsoft.com/downloads/) | [5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.8.1**](https://nuget.org/downloads) | [Visual Studio 2019 Version 16.8.4](https://visualstudio.microsoft.com/downloads/) | |

<sup>1</sup> Installiert mit Visual Studio 2019 mit .NET Core-Workload
  
> [!NOTE]
> Visual Studio 16.8, MSBuild 16.8 und .NET 5.0 erfordern NuGet.exe 5.8 oder höher.


## <a name="summary-whats-new-in-58"></a>Zusammenfassung: Neues in Version 5.8
🎉 Dies ist das erste Release, das vollständige Erstellungs- und Wiederherstellungsunterstützung für NuGet-Pakete für **.NET 5.0-Pakete** 🎉

* Beschleunigen der Nupkg-Extraktion mithilfe von mmap/CreateFileMapping – [#9807](https://github.com/NuGet/Home/issues/9807)

* Anzeigen von Paketrisikodetails im Detailbereich Paket-Manager Benutzeroberflächenpakets [– #9850](https://github.com/NuGet/Home/issues/9850)

* Überprüfen Sie signierte NuGet-Pakete mit dem neuen [`dotnet nuget verify`](/dotnet/core/tools/dotnet-nuget-verify) Befehl – [#8051](https://github.com/NuGet/Home/issues/8051)

* [`dotnet add package`](/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) unterstützt `--prerelease` die Option zum Hinzufügen der neuesten Version eines Pakets, einschließlich Vorabversionen – [#4699](https://github.com/NuGet/Home/issues/4699)

* Suchen Nach Paketen in der CLI mit [`nuget.exe search`](../reference/cli-reference/cli-ref-search.md) dem Befehl [- #9704](https://github.com/NuGet/Home/issues/9704)

* [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) Befehl unterstützt `--verbosity` Option – [#9600](https://github.com/NuGet/Home/issues/9600)

* Aktivieren sie No-Op Wiederherstellungsoptimierung für PackageReference-basierte Projekte im CSPROJ-Stil in Visual Studio [- #9565](https://github.com/NuGet/Home/issues/9565)

* Benutzeroberflächenvorgänge Paket-Manager Lösungsebene, z. B. Paket- und Updatevorgänge, sind bis zu zehn mal schneller – [#6010](https://github.com/NuGet/Home/issues/6010)

* Einige andere NuGet Leistungsverbesserungen in Visual Studio : [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984), [#10052](https://github.com/NuGet/Home/issues/10052), [#9903](https://github.com/NuGet/Home/issues/9903)


### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

**DCRs:**

* .NET 5.0 TFM: Framework-Rangfolgeregeln [– #9436](https://github.com/NuGet/Home/issues/9436)

* NuGet sollte beim Analyse von TargetFramework keine Punktplattformversion [](https://github.com/NuGet/Home/issues/9842) #9842

* Verwenden Sie TargetFrameworkMoniker & TargetPlatformMoniker, um die Frameworks zu abgeleitet, anstatt einzelne TFI-, TFV-, TPI-, TPV-Eigenschaften [zu #9895](https://github.com/NuGet/Home/issues/9895)

* Update `GetReferenceNearestTargetFrameworkTask()` zur Unterstützung von Zielframeworks mit Plattformen (z.B. net5.0-windows) – [#9894](https://github.com/NuGet/Home/issues/9894)

* .NET 5.0-Visual Studio-APIs [– #9650](https://github.com/NuGet/Home/issues/9650)

* Paket-Manager Benutzeroberfläche: Konsolidieren oder Aktualisieren von Paketvorgängen sollte aufgrund von Fehlern (Paket downgrade usw.) nicht blockiert werden – [#9224](https://github.com/NuGet/Home/issues/9224)

* NuGet Funktionen sollten für Projekte mit der -Funktion aufglühen. "PackageReferences": [#9957](https://github.com/NuGet/Home/issues/9957)

* Unterdrücken No-Op Wiederherstellungsmeldungen in Visual Studio [- #6384](https://github.com/NuGet/Home/issues/6384)

**Fehler:**

* Der OutputWindowTextWriter-Konstruktor sollte im Hintergrundthread nicht aufgerufen werden [– #9764](https://github.com/NuGet/Home/issues/9764)

* Wiederherstellen signierter Pakete auf Big-Endian-CPUs [– #9547](https://github.com/NuGet/Home/issues/9547)

* OutputConsoleLogger sollte keine affinitierten Methoden in MEF-Konstruktoren aufrufen [– #9591](https://github.com/NuGet/Home/issues/9591)

* Fehler in NuGet. CommandLine.Console-Methode `PrintJustified()` [– #9737](https://github.com/NuGet/Home/issues/9737)

* Paket-Manager Speicherverlust auf der Benutzeroberfläche, wenn Paketmetadaten aufgrund einer fehlerhaften Bindung automatisch gesammelt werden – [#9757](https://github.com/NuGet/Home/issues/9757)

* [Signierung] Es wird keine Warnung in der Fehlerliste angezeigt, wenn ein signiertes Paket mit packages.config-Format auf der Paket-Manager installiert wird – [#9798](https://github.com/NuGet/Home/issues/9798)

* NuGet. CommandLine.XPlat darf keine öffentlichen APIs haben – [#9821](https://github.com/NuGet/Home/issues/9821)

* Reduzieren Sie Ressourcengefässungen zur Ladezeit der Projektmappe, die durch das Blockieren eines Threadpoolthreads mit `BlockingCollection.Take()` #9822  -  [](https://github.com/NuGet/Home/issues/9822)

* Bei der Befehlszeilenwiederherstellung mit Projekten mit mehreren Zielen sollte NuGet zielframeworkbezogene Informationen aus dem inneren Build lesen [– #9869](https://github.com/NuGet/Home/issues/9869)

* Lesen des Laufzeitbezeichnerdiagramms über das TargetFrameworkInformation-Element [– #9874](https://github.com/NuGet/Home/issues/9874)

* Die statische Graphwiederherstellung ist in Bezug auf die CrossTargeting-Eigenschaft in im Vergleich zu Visual Studio und regulären Wiederherstellungen MSBuild Auswertung [inkonsistent – #9881](https://github.com/NuGet/Home/issues/9881)

* Bei der statischen Graphwiederherstellung mit projekten mit mehreren Zielen sollten NuGet zielframeworkbezogene Informationen aus dem inneren Build lesen. - [#9870](https://github.com/NuGet/Home/issues/9870)

* Laden und Wiederherstellen von Projekten in Visual Studio `net5.0-platform` - [#9863](https://github.com/NuGet/Home/issues/9863)

* Anzeigen der aufgelösten Version auf Paket-Manager Benutzeroberfläche [– #9826](https://github.com/NuGet/Home/issues/9826)

* Paket-Manager Benutzeroberfläche: Projektmappen-Explorer zeigt nicht alle Abhängigkeiten NuGet Pakets an – [#9898](https://github.com/NuGet/Home/issues/9898)

* Aktualisieren sie die LIZENZLISTE – [#9946](https://github.com/NuGet/Home/issues/9946)

* VS 2019 stürzt nach dem Öffnen von Manage NuGet Packages ab: Das Symbol verursacht eine nicht behandelte Ausnahme in image conversio - [#9696](https://github.com/NuGet/Home/issues/9696)

* NuGet. Packaging.Extraction benötigt ilmerge, um Newtonsoft.Jsauszuschließen – [#9966](https://github.com/NuGet/Home/issues/9966)

* Beim Packen mit ContinuePackingAfterGeneratingNuspec=false sollte kein Fehler auftreten, wenn keine Fehler auftreten [– #9786](https://github.com/NuGet/Home/issues/9786)

* Paket-Manager Benutzeroberfläche: Symbole invertieren Farben nicht ordnungsgemäß – [#10017](https://github.com/NuGet/Home/issues/10017)

* Falsche Projektanzahlen für aktuelle und No-Op unter Restore - [#10026](https://github.com/NuGet/Home/issues/10026)

* Die `/p:RestoreUseStaticGraphEvaluation=true` Verwendung von Results in Value kann nicht NULL sein – [#9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` verwendet fälschlicherweise alias für WPF-Bibliotheksprojekte – [#10020](https://github.com/NuGet/Home/issues/10020)

* Paket-Manager Ui: NullReferenceException when signature validation fails - [#10042](https://github.com/NuGet/Home/issues/10042)

* Codespaces: Verwenden Sie keinen Typ `object` für Projektmetadatenwerte – [#10055](https://github.com/NuGet/Home/issues/10055)

* Codespaces: Beim Speichern von Paketquellen in Tools werden Anmeldeinformationen überschrieben [– #9711](https://github.com/NuGet/Home/issues/9711)


**[Liste aller in diesem Release behobenen Probleme: 5.8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[Liste der Probleme in diesem Release : 5.8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>Beiträge aus der Community

Vielen Dank an alle Mitwirkenden, die dazu beigetragen haben, dass NuGet veröffentlicht haben!

|Wer|Prs|Probleme|
|----|----|----|
[omajid](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | Tippfehler in fehlermeldung. "Administrator" anstelle von "Administrator": [#9662](https://github.com/NuGet/Home/issues/9662)
[lets](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | NuGet Packen mit ungültigen AssemblyInformationalVersion-Berichten "Description is required" (Beschreibung ist [erforderlich) – #5548](https://github.com/NuGet/Home/issues/5548)
[besau](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` berücksichtigt keine Branch- und Commit-Eigenschaften [– #9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | Wenn Sie im Fenster Visual Studio Fehlerliste auf NU-Code klicken, sollten Sie zu [https://docs.microsoft.com/nuget/reference/errors-and-warnings/](/nuget/reference/errors-and-warnings/)  -  [#9934](https://github.com/NuGet/Home/issues/9934)
[ChrisMaddock](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | Verwenden Sie "https://" beim Hinzufügen einer neuen Paketquelle über Visual Studio Optionen – [#9974](https://github.com/NuGet/Home/issues/9974)
[Therzok](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio` Leistungsproblem bei Mono – [#9989](https://github.com/NuGet/Home/issues/9989)
[thomaslevlevlev](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | Fügen Sie einen TypeConverter für die SemanticVersion-Klasse hinzu [– #9125](https://github.com/NuGet/Home/issues/9125)

## <a name="summary-whats-new-in-581"></a>Zusammenfassung: Neues in Version 5.8.1

* packages.config package.lock.json verwendet ein falsches Zielframework in 5.8 [– #10257](https://github.com/NuGet/Home/issues/10257)

* 5.8 + 16.8 Transitive Projektabhängigkeiten beim Mischen von PackageReference und packages.config [-](https://github.com/NuGet/Home/issues/10326) #10326

**[Liste aller in diesem Release behobenen Probleme: 5.8.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ff7aeae16150e3b19910391)**

**[Liste der Commits in diesem Release : 5.8.1](https://github.com/NuGet/NuGet.Client/compare/5.8.0.6930...5.8.1.7021)**

## <a name="feedback-welcome"></a>Feedback willkommen

Ihr Feedback ist uns sehr wichtig.  Wenn Probleme mit diesem Release auftreten, überprüfen Sie unsere GitHub [Issues](https://github.com/NuGet/Home/issues) und Visual Studio [Developer Community](https://developercommunity.visualstudio.com/) auf vorhandene Probleme.  Bei neuen Problemen in NuGet melden Sie ein GitHub [Problem.](https://github.com/NuGet/Home/issues/new)
Bei allgemeinen NuGet können Sie uns dies [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) über die Option Problem melden in Ihrer bevorzugten IDE unter Hilfe > **Problem melden.**