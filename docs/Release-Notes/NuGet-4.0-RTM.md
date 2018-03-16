---
title: Anmerkungen zu Version 4.0 RC von NuGet | Microsoft-Dokumentation
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 03/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Anmerkungen zu Version 4.0 RTM von NuGet, einschließlich bekannter Fehler, Fehlerkorrekturen, hinzugefügter Features und DCRs."
keywords: "Anmerkungen zu Version 4.0 RTM von NuGet, Fehlerkorrekturen, bekannte Fehler, hinzugefügte Features, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d1ab89f0decb64a64d04dc293e5273b577e8398b
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-40-rtm-release-notes"></a>Anmerkungen zu Version 4.0 RTM von NuGet

In [Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) ist NuGet 4.0 enthalten. Dieses wurde in Qualität und Leistungsfähigkeit verbessert und erweitert die Funktionalität von Visual Studio um Unterstützung für .Net Core. Die Verbesserungen in diesem Release betreffen die Unterstützung für PackageReference, NuGet-Befehle als MSBuild-Ziele, die Paketwiederherstellung im Hintergrund und vieles mehr.

## <a name="known-issues"></a>Bekannte Probleme

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a>Möglicher Fehler bei der NuGet-Wiederherstellung, wenn mehrere Projekte vorhanden sind, die auf ein anderes Projekt in einer Projektmappe verweisen

#### <a name="issue"></a>Problem

Die NuGet-Wiederherstellung funktioniert möglicherweise nicht, wenn in einer Projektmappe Projektverweise auf das gleiche Projekt mit abweichender Groß-/Kleinschreibung oder mit anderen relativen Pfaden vorhanden sind. [NuGet#4574](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a>Problemumgehung

Ändern Sie die Schreibweisen bzw. relativen Pfade so, dass sie für alle Projektverweise übereinstimmen.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Beim Verwenden der Paket-Manager-Konsole funktioniert die EINGABETASTE ggf. nicht

#### <a name="issue"></a>Problem

Gelegentlich kann es vorkommen, dass die EINGABETASTE in der Paket-Manager-Konsole nicht funktioniert. Wenn dieses Problem auftritt, überprüfen Sie den Fortschritt für diese Korrektur und stellen Sie zusätzliche hilfreiche Informationen zu den Reproduktionsschritten bereit. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Problemumgehung

Starten Sie Visual Studio neu und öffnen Sie die Paketverwaltungskonsole, bevor Sie die Projektmappe öffnen. Alternativ können Sie versuchen, die Datei `project.lock.json` zu löschen und dann erneut wiederherzustellen.

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>In .NET Core-Projekten kann eine Wiederherstellungsendlosschleife auftreten, wenn Sie ein Paket mit einer Assembly verwenden, die eine ungültige Signatur enthält

#### <a name="issue"></a>Problem

Bei der Verwendung eines Pakets mit einer Assembly, die eine ungültige Signatur enthält, oder beim Festlegen der Paketversion mit dem DateTime-Ticker tritt gelegentlich bei der automatischen Paketwiederherstellung eine Endlosschleife auf. [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>Problemumgehung

Zurzeit gibt es keine Problemumgehung.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Sie können DotNetCLITools nicht mit dem NuGet-Paket-Manager anzeigen, hinzufügen oder aktualisieren.

#### <a name="issue"></a>Problem

Der NuGet-Paket-Manager zeigt die DotNetCLITools nicht an und ermöglicht auch kein Hinzufügen/Aktualisieren dieser Tools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Problemumgehung

DotNetCLIToolReferences muss in der Projektdatei manuell bearbeitet werden.

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a>Bei der NuGet-Wiederherstellung tritt ein Fehler auf, wenn Sie PackageId-Eigenschaft für Projekte festlegen

#### <a name="issue"></a>Problem

Bei .NET Core-Projekten respektiert die NuGet-Wiederherstellung in Visual Studio die PackageId-Eigenschaft von Projekten nicht. [NuGet#4586](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a>Problemumgehung

Führen Sie die Wiederherstellung mithilfe der Befehlszeile aus.

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a>Wenn das Projekt keinen Ordner „obj“ aufweist, tritt bei der Paketwiederherstellung ggf. ein Fehler auf

#### <a name="issue"></a>Problem

Visual Studio stellt PackageReferences nicht wieder her, wenn der Ordner „obj“ gelöscht wurde. [NuGet#4528](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a>Problemumgehung

Erstellen Sie den Ordner „obj“ manuell. Die Wiederherstellung sollte dann funktionieren.

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a>Beim manuellen Aktualisieren von Paketen mithilfe von „Update-Paket“ in der Konsole tritt ggf ein Fehler auf

#### <a name="issue"></a>Problem

Das manuelle Verwenden von „Update-Package“ in der Konsole funktioniert nur für PackageReferences-Projekte, die soeben konvertiert wurden. [NuGet#4431](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a>Problemumgehung

Zurzeit gibt es keine Problemumgehung.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Die Neuzuweisung der Framework-Zielversion kann zu unvollständigen IntelliSense-Funktionen führen

#### <a name="issue"></a>Problem

Die Neuzuweisung der Framework-Zielversion kann zu unvollständigen IntelliSense-Funktionen in Visual Studio führen. Dies geschieht, wenn Sie PackageReferences als Paket-Manager-Format verwenden. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Problemumgehung

Führen Sie eine manuelle Wiederherstellung aus.

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a>Fehler von „msbuild /t:restore“ , wenn ein Projekt, das .NET461 als Ziel verwendet, auf ein anderes Projekt verweist, das .NETStandard verwendet

#### <a name="issue"></a>Problem

Bei „msbuild /t:restore“ tritt ein Fehler auf, wenn ein auf PackageReference basierendes Projekt mit dem Ziel .NET461 auf ein anderes auf PackageReference basierendes Projekt verweist, das .NETStandard verwendet.  [NuGet#4532](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a>Problemumgehung

Zurzeit gibt es keine Problemumgehung.

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>Im Rahmen von NuGet 4.0 RTM behobene Probleme

In den [Anmerkungen zu Version 4.0 RC von NuGet](../release-notes/nuget-4.0-RC.md) werden alle für NuGet 4.0 RC behobenen Probleme aufgeführt.

### <a name="features"></a>Features

- Lokalisieren von Zeichenfolgen in „NuGet.Core.sln“ ([#2041](https://github.com/NuGet/Home/issues/2041))

- NuGet erzwingt das Laden von Webanwendungsprojekten im LSL-Modus ([#4258](https://github.com/NuGet/Home/issues/4258))

- Unterstützung für das PackageReference-Element mit der AutoReferenced-Eigenschaft, um Versionsänderungen in der Benutzeroberfläche für mit dem SDK installierte Pakete zu blockieren ([#4044](https://github.com/NuGet/Home/issues/4044))

- Ordnungsgemäßes Übermitteln von „PackageSpec.Version“ für alle Projektabhängigkeiten (PackageRef) ([#3902](https://github.com/NuGet/Home/issues/3902))

- Unterstützung für das Entfernen von Verweisen in der `.csproj`-Datei über die Befehlszeile ([#4101](https://github.com/NuGet/Home/issues/4101))

- Unterstützung für das Wiederherstellen von PackageReference-Projekten (normal und XPlat) und für den Lightweight-Ladevorgang für Projektmappen ([#4003](https://github.com/NuGet/Home/issues/4003))

- Unterstützung für das Hinzufügen von Verweisen in der `.csproj`-Datei über die Befehlszeile ([#3751](https://github.com/NuGet/Home/issues/3751))

- Unterstützung der NuGet-Wiederherstellung für den Lightweight-Ladevorgang für Projektmappen für `packages.config` oder `project.json` ([#3711](https://github.com/NuGet/Home/issues/3711))

- Unterstützung für „contentFiles“ in durch NuGet generierten Zieldateien ([#3683](https://github.com/NuGet/Home/issues/3683))

- Einrichten einer Mono-CI mithilfe von MSBuild für die Überprüfung von „nuget.exe“ unter Mac ([#3646](https://github.com/NuGet/Home/issues/3646))

- Verschieben von NuGet aus den NuGet.Core-Abhängigkeiten (V2) ([#3645](https://github.com/NuGet/Home/issues/3645))

### <a name="bugs"></a>Fehler

- Die NuGet-Wiederherstellung in Visual Studio berücksichtigt die PackageId-Eigenschaft von Projekten nicht [#4586](https://github.com/NuGet/Home/issues/4586)

- NuGet-Fehler „ProjectSystemCache“, wenn Pakete zum VSIX-Paket hinzugefügt werden ([#4545](https://github.com/NuGet/Home/issues/4545))

- Beim Packen wird eine Ausnahme ausgelöst, wenn IncludeSource in einem Projekt mit mehreren TFMs verwendet wird ([#4536](https://github.com/NuGet/Home/issues/4536))

- Visual Studio 2017 RC3 stürzt ab, wenn ein Update für die projektmappenweite Paketverwaltung verwendet wird ([#4474](https://github.com/NuGet/Home/issues/4474))

- Ein neu installiertes Paket kann nicht deinstalliert werden ([#4435](https://github.com/NuGet/Home/issues/4435))

- Wenn zu PackageRef migriert wird, weisen hybride Projektmappen ein merkwürdiges Verhalten bei der Wiederherstellung auf ([#4433](https://github.com/NuGet/Home/issues/4433))

- Wenn der Buildvorgang kurz nach dem Starten eines NuGet-Vorgangs (Installieren, Aktualisieren, Wiederherstellen) ausgeführt wird, kann dies zu einem Absturz von Visual Studio führen ([#4420](https://github.com/NuGet/Home/issues/4420))

- Benutzeroberfläche reagiert nicht: Deadlock beim Initialisieren von NuGet.SolutionRestoreManager.RestoreManagerPackage ([#4371](https://github.com/NuGet/Home/issues/4371))

- Der Befehl „add package“ sollte Versionen statt Elemente als Attribut hinzufügen ([#4325](https://github.com/NuGet/Home/issues/4325))

- „Dotnet Restore foo.sln“ schlägt fehl, wenn Konfigurationen in SLN dazu führen, dass Projekte im Wiederherstellungsdiagramm dupliziert werden (mit verschiedenen Konfigurationen) ([#4316](https://github.com/NuGet/Home/issues/4316))

- Pakete, die nur Inhalte enthalten ([#3668](https://github.com/NuGet/Home/issues/3668))

- Die Option des Selektors für das Paketformat standardmäßig deaktivieren ([#4468](https://github.com/NuGet/Home/issues/4468))

- Leistung: Das Projekt „CreateUAP_CSharp_VS.01.1.Create“ wurde zurückgesetzt, „Duration_TotalElapsedTime“ liegt bei 3.153,570 ms (149,1%) –  Baseline 26129,02 ([#4452](https://github.com/NuGet/Home/issues/4452))

- Leistung: Die Projektmappe „ManagedLangs_CS_DDRIT.0300.Rebuild“ wurde zurückgesetzt, „Duration_TotalElapsedTime“ liegt bei 1,5 Sekunden –  Baseline 26105 ([#4441](https://github.com/NuGet/Home/issues/4441))

- Die Nominierung schlägt in Projekten mit mehreren TFMs fehl ([#4419](https://github.com/NuGet/Home/issues/4419))

- Leistung: Die Projektmappe „WebForms_DDRIT.1200.Close“ wurde zurückgesetzt, „VM_ImagesInMemory_Total_devenv“ liegt bei 3,000 (0,5%) –  Baseline 26123,04 ([#4408](https://github.com/NuGet/Home/issues/4408))

- vsfeedback: Warnungen beim Packen, wenn netcoreapp1.1 angezielt wird ([#4397](https://github.com/NuGet/Home/issues/4397))

- „PathTooLongException“ wird ausgelöst, wenn versucht wird, ein neues NuGet-Paket zu einer leeren ASP.NET Core-Webanwendung hinzuzufügen ([#4391](https://github.com/NuGet/Home/issues/4391))

- „Pack“ wird zu häufig ausgeführt: „dotnet pack“ schlägt mit der Fehlermeldung „Im Zielabhängigkeitsdiagramm besteht eine Ringabhängigkeit im Zusammenhang mit Ziel ‚Pack‘.“ fehl ([#4381](https://github.com/NuGet/Home/issues/4381))

- „Pack“ wird zu häufig ausgeführt: Beim Generieren von NuGet-Paketen sind nicht alle Konfigurationen enthalten ([#4380](https://github.com/NuGet/Home/issues/4380))

- „NullReferenceException“ wird beim Hinzufügen von NuGet mit „PackageRef“ in C++-Projekten ausgelöst ([#4378](https://github.com/NuGet/Home/issues/4378))

- Barrierefreiheit: Die Sprachausgabe gibt das Kontrollkästchen nicht aus, das für das Auswählen der Projekte verwendet wird, für die die Pakete installiert werden sollen ([#4366](https://github.com/NuGet/Home/issues/4366))

- Das Herstellen einer Verbindung von NuGet für Visual Studio 2017 mit VSO- und VSTS-Feeds schlägt fehl (Visual Studio-Fehler 365798) ([#4365](https://github.com/NuGet/Home/issues/4365))

- „contentFiles“ speichert die Ausgabe am falschen Ort, wenn „PackagePath“ den Pfad als „contentFiles“ angibt ([#4348](https://github.com/NuGet/Home/issues/4348))

- Beim Packen des Ziels wird die PackageVersion-Eigenschaft mit dem Versionssuffix angefügt ([#4324](https://github.com/NuGet/Home/issues/4324))

- Das Angeben des Paketpfads funktioniert mit „dotnet pack“ nicht ([#4321](https://github.com/NuGet/Home/issues/4321))

- NuGet gibt während der Wiederherstellung einige Warnungen zu doppelten Importen aus ([#4304](https://github.com/NuGet/Home/issues/4304))

- Das Dialogfeld für das Auswählen des Formats des NuGet-Paket-Managers sieht im dunklen Design nicht gut aus ([#4300](https://github.com/NuGet/Home/issues/4300))

- Visual Studio stürzt beim Wiederherstellen des Builds ab ([#4298](https://github.com/NuGet/Home/issues/4298))

- Bei Visual Studio tritt ein Deadlock auf, wenn Sie den TFM zu Zielframeworks hinzufügen und dann speichern und einen Build durchführen (in 10% der Fälle) ([#4295](https://github.com/NuGet/Home/issues/4295))

- „nuget pack“ gibt keine Meldung beim erfolgreichen Packen eines Projekts aus ([#4294](https://github.com/NuGet/Home/issues/4294))

- „PackTask“ schlägt fehl, da System.IO.Compression 4.1 nicht gefunden werden konnte ([#4290](https://github.com/NuGet/Home/issues/4290))

- „Pack“ wird zu häufig ausgeführt: „PackTask“ schlägt regelmäßig wegen Konflikten beim Dateizugriff fehl ([#4289](https://github.com/NuGet/Home/issues/4289))

- NuGet öffnet das Ausgabefenster während der Wiederherstellung im Hintergrund ([#4274](https://github.com/NuGet/Home/issues/4274))

- Beseitigen von „ServiceProvider“ als riskantes Codierungsmuster (das zu Abstürzen führen kann) ([#4268](https://github.com/NuGet/Home/issues/4268))

- Leistung/Benutzeroberfläche reagiert nicht: Verbessern der Lesevorgänge von DownloadTimeoutStream ([#4266](https://github.com/NuGet/Home/issues/4266))

- Bei Visual Studio tritt ein Deadlock auf, wenn Sie versuchen, ein Projekt zu schließen, bevor die Wiederherstellung von NuGet abgeschlossen ist ([#4257](https://github.com/NuGet/Home/issues/4257))

- Probleme mit „PackTask“ und dem Packen von `.nuspec` ([#4250](https://github.com/NuGet/Home/issues/4250))

- [vsfeedback] NuGet-Pakete können für neue Projekte nicht aufgelöst werden (Visual Studio muss neu gestartet werden) ([#4217](https://github.com/NuGet/Home/issues/4217))

- [vsfeedback] Das Dropdownmenü „Version“, das die verfügbaren Paketversionen anzeigt, bleibt nicht synchron mit dem ausgewählten NuGet-Paket ([#4198](https://github.com/NuGet/Home/issues/4198))

- Nuget.Client sollte „JoinableTaskFactory“ bei der Interaktion mit CPS verwenden, um Deadlocks zu verhindern ([#4185](https://github.com/NuGet/Home/issues/4185))

- NuGet 3.5.0 entpackt `.targets` nicht aus dem Paket ([#4171](https://github.com/NuGet/Home/issues/4171))

- „dotnet pack“ unterstützt in `.csproj` keine Titel ([#4150](https://github.com/NuGet/Home/issues/4150))

- „Install-Package“ führt zu einer Fehlermeldung in Visual Studio 2017 RC ([#4127](https://github.com/NuGet/Home/issues/4127))

- Das Aktualisieren eines Pakets für .NET Core-Projekte scheint nicht zu funktionieren, da die Benutzeroberfläche das CPS-Update nicht erhält ([#4035](https://github.com/NuGet/Home/issues/4035))

- Verbesserung der Warnung für nicht aufgelöste Verweise ([#3955](https://github.com/NuGet/Home/issues/3955))

- „dotnet pack“: „ProjectReference“ verliert die Versionsinformationen ([#3953](https://github.com/NuGet/Home/issues/3953))

- Regression der insgesamt verstrichenen Zeit von „Erstellen einer UWP-App“, „Erstellen eines Projekts“ und „Neuerstellen“ ([#3873](https://github.com/NuGet/Home/issues/3873))

- Die Meldung für die erfolgreiche Wiederherstellung wird auch angezeigt, wenn während der Wiederherstellung ein Fehler auftritt ([#3799](https://github.com/NuGet/Home/issues/3799))

- Erneutes Veröffentlichen von Nuget.CommandLine 3.4.4 auf nuget.org ([#2931](https://github.com/NuGet/Home/issues/2931))

- Beim Migrieren ändert sich das Projekt von `project.json` in `.csproj` und die Wiederherstellung schlägt fehl ([#4297](https://github.com/NuGet/Home/issues/4297))

- Die Wiederherstellung des neu erstellten xUnit-Testprojekts schlägt fehl ([#4296](https://github.com/NuGet/Home/issues/4296))

- Core-Projekte reagieren möglicherweise nicht, die Benutzeroberfläche wird beim Öffnen gesperrt ([#4269](https://github.com/NuGet/Home/issues/4269))

- Fehlerbehebung bei der TARGETS-Datei für Buildaufgaben ([#4267](https://github.com/NuGet/Home/issues/4267))

- Die Fehlerliste enthält einen Fehler nach dem Erstellen der Projektmappe, der das Projekt entlädt, auf das verwiesen wird ([#4208](https://github.com/NuGet/Home/issues/4208))

- MSB4057: „Das Ziel ‚_GenerateRestoreGraphProjectEntry‘ ist im Projekt nicht vorhanden.“ ([#4194](https://github.com/NuGet/Home/issues/4194))

- vsfeedback: Die Benutzeroberfläche des NuGet-Managers für Projektmappen stürzt ab, wenn alle Projekte ausgewählt werden ([#4191](https://github.com/NuGet/Home/issues/4191))

- „MSBuildPath“ von „nuget.exe“ schlägt fehl, wenn ein nachgestellter Schrägstrich vorhanden ist ([#4180](https://github.com/NuGet/Home/issues/4180))

- vsfeedback: Die Wiederherstellung von NuGet gibt für das LinqToTwitter-Projekt mehrere Warnungen für Projektverweise aus ([#4156](https://github.com/NuGet/Home/issues/4156))

- Beim Packen von `.csproj` aus wird das Attribut „minClientVersion“ nicht eingeschlossen ([#4135](https://github.com/NuGet/Home/issues/4135))

- „NuGet.Build.Tasks.Pack.dll“ wird in Visual Studio 2017 als verzögert signiert (d15rel 26014.00) ([#4122](https://github.com/NuGet/Home/issues/4122))

- VSFeedback: Wiederherstellung eines Visual Studio 2015-Projekts, das mit CMake 3.7.1 generiert wurde, schlägt fehl ([#4114](https://github.com/NuGet/Home/issues/4114))

- VSFeedback: Fehler bei der Wiederherstellung können die umfangreicheren Fehlermeldungen des Builds verdecken ([#4113](https://github.com/NuGet/Home/issues/4113))

- [VSFeedback] Fehler beim Wiederherstellen von NuGet-Paketen für das Websiteprojekt: „Der Wert darf nicht NULL sein.“ ([#4092](https://github.com/NuGet/Home/issues/4092))

- Bei der Migration wird eine Ausnahme beim Objektverweis in „NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker“ ausgelöst ([#4067](https://github.com/NuGet/Home/issues/4067))

- „dotnet pack“ sollte Tools mit den Versionen packen, für die das Paket erstellt wurde ([#4063](https://github.com/NuGet/Home/issues/4063))

- Die neue Wiederherstellung im Hintergrund zeigt Millisekunden in der Statusleiste an, obwohl die Wiederherstellung mehrere Sekunden dauert ([#4036](https://github.com/NuGet/Home/issues/4036))

- Tippfehler bei „Fehler beim Auflösen aller Projektverweise...“ ([#4018](https://github.com/NuGet/Home/issues/4018))

- Aktivieren von PCM-Workflows in Szenarios mit Paketverweisen ([#4016](https://github.com/NuGet/Home/issues/4016))

- Die installierten Pakete können auf der Benutzeroberfläche des Paket-Managers nicht gefunden werden ([#4015](https://github.com/NuGet/Home/issues/4015))

- „dotnet pack“ schlägt fehl, wenn „PackagePath“ leer ist ([#3993](https://github.com/NuGet/Home/issues/3993))

- Die Wiederherstellungsaufgabe schlägt in Szenarios mit mehreren Benutzern fehl ([#3897](https://github.com/NuGet/Home/issues/3897))

- Der Inhaltstyp kann nicht geändert werden, wenn mithilfe der NuGet-Packaufgabe gepackt wird ([#3895](https://github.com/NuGet/Home/issues/3895))

- Die Standardkopien von „ContentFiles“ sind für „MsBuild /t:pack“ falsch ([#3894](https://github.com/NuGet/Home/issues/3894))

- Bei der Installation der Paketwiederherstellung wird die Meldung für das Wiederherstellen von Paketen doppelt protokolliert ([#3785](https://github.com/NuGet/Home/issues/3785))

- Entfernen der Sicherungen: Die Wiederherstellung des Abschnitts „Runtimes“ sollte nur für das aktuelle Projekt gelten ([#3768](https://github.com/NuGet/Home/issues/3768))

- Die Packaufgabe fügt Inhaltsdateien in „content/“ und „contentFiles/“ ein ([#3718](https://github.com/NuGet/Home/issues/3718))

- „dotnet pack3“ teilt Tags zusätzlich ([#3701](https://github.com/NuGet/Home/issues/3701))

- dotnet pack: Beim Packen von Projekten mit Paketverweisen wird eine Warnung wegen doppelten Imports ausgegeben ([#3665](https://github.com/NuGet/Home/issues/3665))

- Die Wiederherstellungsprotokollierung wird in Visual Studio nicht immer angezeigt ([#3633](https://github.com/NuGet/Home/issues/3633))

- Der lokale Hilfetexte in NuGet erwähnt weiterhin den Paketcache ([#3592](https://github.com/NuGet/Home/issues/3592))

- „Restore3“ koppelt „PackageReferences“ mit „TargetFrameworks“ ([#3504](https://github.com/NuGet/Home/issues/3504))

- NuGet wählt in der Eingabeaufforderung von VS „15“ Developer (Vorschauversion 4) eine unerwartete Version von MSBuild aus ([#3408](https://github.com/NuGet/Home/issues/3408))

- TARGETS- und PROPS-Dateien sollten auch bei einer fehlerhaften Wiederherstellung geschrieben werden ([#3399](https://github.com/NuGet/Home/issues/3399))

- NuGet berücksichtigt während der Wiederherstellung nicht die gleichen Kompatibilitätsshims wie MSBuild, wenn diese über die Visual Studio 2015-Eingabeaufforderung durchgeführt wird ([#3387](https://github.com/NuGet/Home/issues/3387))

- Reaktivieren von „PackFromProjectWithDevelopmentDependencySet“ für Visual Studio 2015 ([#3272](https://github.com/NuGet/Home/issues/3272))

- Probleme bei Blend mit NuGet ([#4043](https://github.com/NuGet/Home/issues/4043))

- Integrieren von 4.0.0.2067 in CLI- und SDK-Repositorys für die Bereitstellung mit RC2 ([#4029](https://github.com/NuGet/Home/issues/4029))

- Visual Studio reagiert nicht, wenn eine neue Core-Konsolen-App erstellt und eine Projektmappe geschlossen, geöffnet und dann wieder geschlossen wird ([#4008](https://github.com/NuGet/Home/issues/4008))

- Absturz beim Öffnen des Projekts mit „d15prerel.25916.01“ ([#3982](https://github.com/NuGet/Home/issues/3982))

- Fehler bei der doc/help-Meldung für lokale Variablen von dotnet bzw. „nuget.exe“ ([#3919](https://github.com/NuGet/Home/issues/3919))

- Überprüfen von „PackTask“ nach Problemen mit vorangestellten oder nachstehenden Leerräumen ([#3906](https://github.com/NuGet/Home/issues/3906))

- „dotnet pack“ packt von „obj“ statt von „bin“ ([#3880](https://github.com/NuGet/Home/issues/3880))

- „dotnet pack“ scheint die Version von „ProjectReference“ immer auf 1.0.0 festzulegen ([#3874](https://github.com/NuGet/Home/issues/3874))

- „dotnet pack“ schlägt trotz Projektverweisen und <TargetFramework> fehl ([#3865](https://github.com/NuGet/Home/issues/3865))

- „LockRecursionException“ in „ProjectSystemCache.TryGetProjectNameByShortName“ ([#3861](https://github.com/NuGet/Home/issues/3861))

- Leerräume aus MSBuild-Eigenschaften entfernen ([#3819](https://github.com/NuGet/Home/issues/3819))

- Konsolidieren der beiden Projektereignisse, die beim Laden des Projekts ausgelöst werden ([#3759](https://github.com/NuGet/Home/issues/3759))

- Die P2P-Bibliotheken in der `project.assets.json`-Datei besitzen die falsche Version ([#3748](https://github.com/NuGet/Home/issues/3748))

- Die Wiederherstellung stürzt aufgrund eines nicht reagierenden Feeds und eines nicht verfügbaren Pakets ab ([#3672](https://github.com/NuGet/Home/issues/3672))

- „nuget.exe“ reagiert bei einer großen Menge von Fehlerausgaben von MSBuild möglicherweise nicht ([#3572](https://github.com/NuGet/Home/issues/3572))

- Die Wiederherstellung während des Builds schlägt für Blend beim ersten Mal fehl, ist beim zweiten Mal jedoch erfolgreich (behobenes Visual Studio-Szenario) ([#2121](https://github.com/NuGet/Home/issues/2121))

### <a name="dcrs"></a>DCRs

- Migrieren von V2 VSIX zu V3 VSIX ([#4196](https://github.com/NuGet/Home/issues/4196))

- NuGet sollte über einen Mechanismus verfügen, um den Pfad für die Sperrdatei in MSBuild abzurufen ([#3351](https://github.com/NuGet/Home/issues/3351))

- Hinzufügen von Buildobjekten zu der Kompatibilitätsprüfung und der Objektdatei des TFM ([#3296](https://github.com/NuGet/Home/issues/3296))

- Definieren einer neuen „ProjectCapability“ namens „Pack“ in den Packzielen zum Aktivieren von Paketfunktionen ([#4146](https://github.com/NuGet/Home/issues/4146))

- Ausführen von Packzielen als Postbuildziel bedingt durch die MSBuild-Eigenschaft „GeneratePackageOnBuild“ ([#4145](https://github.com/NuGet/Home/issues/4145))

- Verwenden der NuGet-Eigenschaft „RestoreProjectStyle“ zum Erstellen eines spezifischen NuGet-Projekts ([#4134](https://github.com/NuGet/Home/issues/4134))

- Anpassen der Wiederherstellung für geänderte transitive Projektverweise ([#4076](https://github.com/NuGet/Home/issues/4076))

- Hinzufügen von NuGet-Eigenschaften zur Zieldatei für Nicht-UWP-Projekte ([#4030](https://github.com/NuGet/Home/issues/4030))

- UWP-Unterstützung für „TargetPlatformVersion“ ([#3923](https://github.com/NuGet/Home/issues/3923))

- Übermitteln der Projektverweismetadaten an das NuGet-Projektsystem ([#3922](https://github.com/NuGet/Home/issues/3922))

- Hinzufügen der Benutzeroberfläche für den Packmodus ([#3921](https://github.com/NuGet/Home/issues/3921))

- Für die veraltete `.csproj`-Datei müssen „NugetTargetMoniker“ und „RuntimeIdentifiers“ im Projekt und in den Zielen festgelegt sein ([#3854](https://github.com/NuGet/Home/issues/3854))

- Das Installieren des Pakets überschneidet sich möglicherweise mit der automatischen Wiederherstellung ([#3836](https://github.com/NuGet/Home/issues/3836))

- Das Kontextmenü „QueryStatus“ wird nicht angezeigt, wenn „VSPackage“ nicht geladen wird ([#3835](https://github.com/NuGet/Home/issues/3835))

- Beim Wiederherstellen von Projektmappen und Builds werden weiterhin Dialogfelder angezeigt ([#3789](https://github.com/NuGet/Home/issues/3789))

- Isolieren der VSSDK-Version während des Projektmappenbuilds von „NuGet.Clients“ ([#3890](https://github.com/NuGet/Home/issues/3890))

## <a name="links-to-github-issues-fixed-in-rtm"></a>Links zu GitHub-Problemen, die in RTM behoben wurden:
[Probleme: Liste 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RTM")  
[Probleme: Liste 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC4")  
[Probleme: Liste 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC3")  
[Probleme: Liste 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC2")  
[Probleme: Liste 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC")
