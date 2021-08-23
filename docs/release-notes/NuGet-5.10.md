---
title: Versionshinweise zu NuGet 5.10
description: Versionshinweise für NuGet 5.10, einschließlich neuer Features, Fehlerbehebungen und DCRs.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 80a372074604f5c0073f78927b84de00e78acc74
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726950"
---
# <a name="nuget-510-release-notes"></a>Versionshinweise zu NuGet 5.10

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version | Verfügbar in .NET SDK(s) |
|:---|:---|:---|
| [**5.10.0**](https://nuget.org/downloads) | [Visual Studio 2019 Version 16.10](https://visualstudio.microsoft.com/downloads/) | [5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> Installiert mit Visual Studio 2019 mit .NET Core-Workload
  
> [!NOTE]
> Visual Studio 16.10, MSBuild 16.10 und .NET 5.0.300 oder höher erfordert NuGet.exe 5.10 oder höher.

## <a name="summary-whats-new-in-510"></a>Zusammenfassung: Neuerungen in 5.10

* Signierung: Implementieren des Befehls dotnet trusted-signers – [#8053](https://github.com/NuGet/Home/issues/8053)

* Deaktivieren der Standardvalidierung unter Linux, aber standardmäßig aktiviert auf Windows [– #10713](https://github.com/NuGet/Home/issues/10713)

* Hinzufügen einer ENV-Variablen für die Überprüfung der Paketsignierung unter .NET 5 und mehr Linux/MAC [– #10742](https://github.com/NuGet/Home/issues/10742)

* Verbessern der Leistung bei der Installation neuer Pakete für große Lösungen [– #10166](https://github.com/NuGet/Home/issues/10166)

* Fügen Sie den Projekttyp `nfproj` der Liste der unterstütztenProjectExtensions für die NuGet-CLI hinzu. - [#10562](https://github.com/NuGet/Home/issues/10562)

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

* Unterdrücken des `<requireLicenseAcceptance>` Elements beim Packen eines Projekts [– #5133](https://github.com/NuGet/Home/issues/5133)

* [CPVM] Vorschauwarnung sollte auf dotnet cli angezeigt werden – [#10226](https://github.com/NuGet/Home/issues/10226)

* Aktualisieren Sie die Hintergrund- und Vordergrundfarbtoken der PMUI auf CommonDocumentColors [– #10608](https://github.com/NuGet/Home/issues/10608)

* [Fehler Bash] Fehler "Vorgang vom Benutzer abgebrochen" wird im Fenster Fehlerliste angezeigt, wenn auf der PM-Benutzeroberfläche schnell zwischen Registerkarten gewechselt wird [– #10671](https://github.com/NuGet/Home/issues/10671)

* PM-Benutzeroberfläche: Verbessern der Paketinstallationsleistung auf Lösungsebene [– #10210](https://github.com/NuGet/Home/issues/10210)

* Ersetzen Sie GetService überall in NuGet durch GetServiceAsync. Clients [– #3784](https://github.com/NuGet/Home/issues/3784)

* NuGet.exe Paketleistungsproblem mit `..` relativem Pfad – [#5016](https://github.com/NuGet/Home/issues/5016)

* Die Leistung von "nuget pack" sinkt mit zunehmenden Ebenen in den Quellpfaden [– #5706](https://github.com/NuGet/Home/issues/5706)

* NuGet tritt beim Packen von nuspec mit doppelten Dateien kein Fehler auf. - [#6941](https://github.com/NuGet/Home/issues/6941)

* NuGet Paket "The DateTimeOffset specified cannot be converted into a ZIP file timestamp" (Das angegebene DateTimeOffset kann nicht in einen Zip-Dateizeitstempel konvertiert werden) [– #7001](https://github.com/NuGet/Home/issues/7001)

* Zeitstempel der Datei des gepackten Pakets werden durch die Zeitzone verschoben [– #7395](https://github.com/NuGet/Home/issues/7395)

* NU1004 sollte umsetzbarere Informationen enthalten – [#7696](https://github.com/NuGet/Home/issues/7696)

* [Fehler Bash] [Testfehler] Die leere/falsch formatierte Sperrdatei sollte nicht aktualisiert werden, wenn "dotnet restore --use-lock-file --locked-mode" ausgeführt wird [#8640](https://github.com/NuGet/Home/issues/8640)

* NuGetVersionRange ermöglicht die Analyse logisch falscher Bereiche – [#9145](https://github.com/NuGet/Home/issues/9145)

* Die PM-Benutzeroberfläche kann keine unterscheidbare Hintergrundfarbe zwischen ausgewählten und mit dem Mauszeiger zeigenden Paketquellen anzeigen – [#9538](https://github.com/NuGet/Home/issues/9538)

* Kontrollkästchen zum Auswählen von Projekten, auf die installiert werden soll, wird nicht von der Sprachausgabe gelesen [– #9578](https://github.com/NuGet/Home/issues/9578)

* Die Standardauswahl der Dropdownliste "Versionen des Detailbereichs" sollte auf den Registerkarten "Installiert/Updates" installiert/LatestStable sein [– #9887](https://github.com/NuGet/Home/issues/9887)

* Entfernen Sie das Problemumgehungskonto für einige .NET 5 SDKs-Berichte TargetPlatformMoniker von ` ,Version= `  -  [#9913](https://github.com/NuGet/Home/issues/9913)

* dotnet nuget verify is too quiet – [#10316](https://github.com/NuGet/Home/issues/10316)

* VersionRange kann keine einstelligen Bereiche analysieren [– #10342](https://github.com/NuGet/Home/issues/10342)

* Vs Solution Manager löst während des Debuggens eine NULL-Ausnahme für aus [– #10352](https://github.com/NuGet/Home/issues/10352)

* Verschieben von CLI-Ausnahmemeldungen in [Zeichenfolgenressourcendateien – #10392](https://github.com/NuGet/Home/issues/10392)

* Entfernen von intakten Code (TabItemButtonAutomationPeer) [– #10435](https://github.com/NuGet/Home/issues/10435)

* Kontextmenü aktualisieren sollte zum ersten ausgewählten Element scrollen [– #10498](https://github.com/NuGet/Home/issues/10498)

* Projektmappen-PMUI-Details mit überlappender horizontaler Leiste [– #10533](https://github.com/NuGet/Home/issues/10533)

* Signierung: Primäre Signaturdetails werden nicht angezeigt, wenn das Zertifikat abgelaufen ist und der Zeitstempel nicht vertrauenswürdig ist [– #10535](https://github.com/NuGet/Home/issues/10535)

* Wenn keine Quellen aktiviert sind, wird verhindert, dass die PM-Benutzeroberfläche angezeigt wird [– #10541](https://github.com/NuGet/Home/issues/10541)

* Paketmetadaten (Details, Veraltet) werden manchmal nicht aus nuget.org in CodeSpaces abgerufen – [#10549](https://github.com/NuGet/Home/issues/10549)

* PmUI-Initialisierung schlägt mit Ausnahme während der Debugsitzung fehl – [#10559](https://github.com/NuGet/Home/issues/10559)

* NuGet-Wiederherstellung führt zu einem Fehler bei der Paketintegritätsprüfung auf dem Big-Endian-System [– #10567](https://github.com/NuGet/Home/issues/10567)

* FormatException wird anstelle von PackagingException ausgelöst – [#10595](https://github.com/NuGet/Home/issues/10595)

* CPVM : Parallelitätsprobleme im Graph-Walking-Algorithmus [– #10598](https://github.com/NuGet/Home/issues/10598)

* Hinzufügen von Telemetriedaten zur PMC-PowerShell-Version [– #10609](https://github.com/NuGet/Home/issues/10609)

* Verbessern der NuGetVersion-Sortierleistung [– #10611](https://github.com/NuGet/Home/issues/10611)

* Trusted Signers Add verfügt über inkonsistente Argumente [– #10647](https://github.com/NuGet/Home/issues/10647)

* Vs2019 v16.9.0: Durch das Wechseln von Registerkarten in NuGet Paket-Manager von "Updates" zu "Installiert" wird der Frame nicht aktualisiert. - [#10654](https://github.com/NuGet/Home/issues/10654)

* Entfernen Sie "v" aus der Versionsnummer in PMUI [– #10677](https://github.com/NuGet/Home/issues/10677)

* INuGetProjectService.GetInstalledPackagesAsync löst aus, bevor der CPS-Projektsystemvorschlag empfangen wird – [#10681](https://github.com/NuGet/Home/issues/10681)

* Eingebettete Symbole führen dazu, dass der Zugriff von der Quelle "Microsoft Visual Studio Offlinepakete" auf der Registerkarte Durchsuchen verweigert wird [– #10687](https://github.com/NuGet/Home/issues/10687)

* INuGetProjectService.GetInstalledPackagesAsync löst aus, wenn MSBuildProjectExtensionsPath nicht festgelegt ist – [#10739](https://github.com/NuGet/Home/issues/10739)

* "dotnet nuget remove source nuget.org" funktioniert nicht zum ersten Mal – [#10745](https://github.com/NuGet/Home/issues/10745)

* NuGet blockiert einen Threadpoolthread in einer asynchronen Methode, die einen synchronen Aufruf des UI-Threads vornimmt – [#10775](https://github.com/NuGet/Home/issues/10775)

* `PackageLoadContext.GetInstalledAndTransitivePackagesAsync` ist nicht toter Code und beeinträchtigt die Leistung [– #10790](https://github.com/NuGet/Home/issues/10790)

* Eingebettetes Symbol in NuGet SDK-Paketen verwenden – [#10795](https://github.com/NuGet/Home/issues/10795)

* Aktualisieren der LIZENZIERUNGX-Lizenzliste [– #10806](https://github.com/NuGet/Home/issues/10806)

**[Liste aller in diesem Release behobenen Probleme: 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**
  
**[Liste der Commits in dieser Version : 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**
  
### <a name="community-contributions"></a>Beiträge aus der Community

Vielen Dank an alle Mitwirkenden, die dieses NuGet Release super gemacht haben!

|Wer|Prs|Probleme|
|----|----|----|
[im NS-Z-201](https://github.com/louis-z) | [3991](https://github.com/NuGet/NuGet.Client/pull/3991) | VersionRange kann keine einstelligen Bereiche analysieren [– #10342](https://github.com/NuGet/Home/issues/10342)
[omajid](https://github.com/omajid) | [3860](https://github.com/NuGet/NuGet.Client/pull/3860) | NuGet. Client-build.sh ist fehlerhaft [– #10139](https://github.com/NuGet/Home/issues/10139)
[Nirmal4G](https://github.com/Nirmal4G) | [3623](https://github.com/NuGet/NuGet.Client/pull/3623) | NuGet. Client-build.sh ist fehlerhaft [– #10139](https://github.com/NuGet/Home/issues/10139)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | Die Leistung von "nuget pack" sinkt mit zunehmenden Ebenen in den Quellpfaden [– #5706](https://github.com/NuGet/Home/issues/5706)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | NuGet.exe Paketleistungsproblem mit . relativer Pfad [– #5016](https://github.com/NuGet/Home/issues/5016)
[djin-krysakuc](https://github.com/marcin-krystianc) | [3940](https://github.com/NuGet/NuGet.Client/pull/3940) | CPVM : Parallelitätsprobleme im Graph-Walking-Algorithmus [– #10598](https://github.com/NuGet/Home/issues/10598)
[jossimoes](https://github.com/josesimoes) | [3943](https://github.com/NuGet/NuGet.Client/pull/3943) | Fügen Sie den Projekttyp nfproj der Liste der unterstütztenProjectExtensions für die NuGet CLI hinzu. - [#10562](https://github.com/NuGet/Home/issues/10562)

## <a name="feedback-welcome"></a>Feedback willkommen

Ihr Feedback ist uns sehr wichtig.  Wenn probleme mit dieser Version auftreten, überprüfen Sie unsere [GitHub Probleme](https://github.com/NuGet/Home/issues) und [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) auf vorhandene Probleme.  Melden Sie bei neuen Problemen innerhalb NuGet eine [GitHub Problem.](https://github.com/NuGet/Home/issues/new)
Informieren Sie uns bei allgemeinen NuGet Problemen über die Option [Problem melden](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) in Ihrer bevorzugten IDE unter Hilfe > Melden **eines Problems.**
