---
title: Anmerkungen zu NuGet 3.5 Beta
description: Anmerkungen zu NuGet 3.5, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d8df2cb51ddcc03fb3922d9e9def17b39fccc661
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550683"
---
# <a name="nuget-35-release-notes"></a>Anmerkungen zu NuGet 3.5

[Anmerkungen zu NuGet 3.5-RC](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC-Versionsanmerkungen](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Fehlerkorrekturen

* Pack verwendet nicht MSBuild 14.1 unter Mono - [#3550](https://github.com/NuGet/Home/issues/3550)

* Registerkarte "Updates" nicht wählen Sie die neueste verfügbare Version zu aktualisieren, wählen Sie derzeit installierte Version - stattdessen [#3498](https://github.com/NuGet/Home/issues/3498)

* Beheben der Absturz nach einer privaten v2 MyGet-feed zu authentifizieren, und klicken auf "X mehr Ergebnisse anzeigen"- [#3469](https://github.com/NuGet/Home/issues/3469)

* Protokollmeldungen für UI - in umgekehrter Reihenfolge zu sein scheinen [#3446](https://github.com/NuGet/Home/issues/3446)

* V3.4.4 - Nuget-Wiederherstellung löst "Format für den angegebenen Pfad wird nicht unterstützt" - [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet-Befehlszeile 3.6 Beta berücksichtigt keine - Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)

* NuGet IKVM langsam zu installieren, auf großen Projekt - [#3428](https://github.com/NuGet/Home/issues/3428)

* NuGet.exe - Self-Service wird auf sich selbst zu aktualisieren – Update [#3395](https://github.com/NuGet/Home/issues/3395)

* 3.5 installieren/Wiederherstellen von UNC-Freigabe ist Regression aus 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)

* Fehler bei der Installation von Moq aus der Paket-Verwaltungsoberfläche für ein Projekt "net451" - [#3349](https://github.com/NuGet/Home/issues/3349)

* Install-Registerkarte auf Projektmappenebene keine Version des Pakets - anzeigen [#3339](https://github.com/NuGet/Home/issues/3339)

* Xproj `project.json` Update aus der Registerkarte "installiert" verliert die Status - [#3303](https://github.com/NuGet/Home/issues/3303)

* NuGet Pack auf `.csproj` ignoriert leere Dateien-Element im `.nuspec` -Datei – [#3257](https://github.com/NuGet/Home/issues/3257)

* Websiteprojekten in IIS gehostete sollte nicht dazu, dass der Wiederherstellung ein Fehler auftritt – [#3235](https://github.com/NuGet/Home/issues/3235)

* Anmeldeinformationen, die nicht aus der Datei "NuGet.config" abgerufen werden, wenn v3-Endpunkts auf v2 - umleitet [#3179](https://github.com/NuGet/Home/issues/3179)

* NuGet Pack nicht Assembly aufgelöst wird, beim Abrufen von Metadaten für übertragbare Assembly - [#3128](https://github.com/NuGet/Home/issues/3128)

* NuGet wurde nicht gefunden. `msbuild.exe` unter Mono - [#3085](https://github.com/NuGet/Home/issues/3085)

* NuGet.exe-Pack kann kein vorab veröffentlichtes-Tag der beginnt mit einer Anzahl - [#1743](https://github.com/NuGet/Home/issues/1743)

* Installation des NuGet-Pakets ein Fehler auftritt, auf VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)

* AllowedVersions Filtern nicht funktioniert auf Projektmappenebene - [#333](https://github.com/NuGet/Home/issues/333)

* Wiederherstellung nach dem Zufallsprinzip schlägt fehl, mit einem Element mit demselben Schlüssel wurde bereits hinzugefügt. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Kann nicht installiert werden Nuget.Common in `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* Wenn die Benutzeroberfläche verwendet, um eine V2-Quelle zu suchen, heißt FindPackagesById zweimal für jeden ID - [#2517](https://github.com/NuGet/Home/issues/2517)

* Pakete können nicht-Projekte – hängen [#2490](https://github.com/NuGet/Home/issues/2490)

* NuGet.exe-Pack - Exclude ist dokumentiert, ist jedoch nicht unterstützt – [#2284](https://github.com/NuGet/Home/issues/2284)

* Probleme mit Fehler Instanznachrichten an, wenn im Abschnitt "ContentFiles" `.nuspec` ist ungültig: [#1686](https://github.com/NuGet/Home/issues/1686)

* Pushbenachrichtigungen sendet immer die gesamtes Paket zweimal mit authentifizierte Paketquellen - [#1501](https://github.com/NuGet/Home/issues/1501)

* Es sind keine Informationen wurde angegeben, beim Aufrufen von nuget.exe-Update *.csproj, während das Projekt keine `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` Wiederherstellung wird nicht erneut versucht, auf den Statuscode 5xx in V2-Quellen – [#1217](https://github.com/NuGet/Home/issues/1217)

* Doppelter Punkt im Datei-Src in `.nuspec` funktioniert nicht – [#2947](https://github.com/NuGet/Home/issues/2947)

* CoreCLR-wiederhergestellt werden soll, um Feeds mit der Verschlüsselung – ignorieren [#2942](https://github.com/NuGet/Home/issues/2942)

* NuGet.exe-push 403 - falsch Aufforderung zur Eingabe von Anmeldeinformationen - Behandlung [#2910](https://github.com/NuGet/Home/issues/2910)

* NuGet-Update über die Paket-Manager entfernt, Eigenschaften aus der `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* NuGet.PackageManagement.VisualStudio versuchen Sie es beim Laden von "NuGet.TeamFoundationServer14" geändert, denn DLL-Namen auf "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)

* Paket-Manager-Benutzeroberfläche neu zeigen keine aktualisierte Version - [#2828](https://github.com/NuGet/Home/issues/2828)

* Update-Package möchten, verwenden Sie die Paket-ID, Version statt package.version - [#2771](https://github.com/NuGet/Home/issues/2771)

* NuGet-Wiederherstellung Csproj sollten Fehler, wenn das Projekt Nuget verwenden, ist nicht (`packages.config` oder `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)

* TFS-Fehler "[Datei] nicht in Ihrem Arbeitsbereich gefunden, oder Sie sind nicht berechtigt, darauf zuzugreifen" beim Aktualisieren oder deinstallieren, wenn die Projektmappe oder eines Projekts an TFS-quellcodeverwaltung - gebunden ist [#2739](https://github.com/NuGet/Home/issues/2739)

* Update-Paket keine Abhängigkeiten für Pakete, nicht-Ziel abrufen [#2724](https://github.com/NuGet/Home/issues/2724)

* Es gibt keine Möglichkeit festzulegende Protokolle Ausführlichkeitsgrad für Nuget-Paket-Manager-UI-Aktionen – [#2705](https://github.com/NuGet/Home/issues/2705)

* NuGet-Konfiguration ist ungültig: Visual Studio 2015 VSIX (3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) funktioniert nicht – [#2653](https://github.com/NuGet/Home/issues/2653)

* Version von NuGet 3.4.3 - Wert abrufen darf nicht null sein beim Erstellen des Paket - [#2648](https://github.com/NuGet/Home/issues/2648)

* Wiederherstellung verwendet gespeicherte Anmeldeinformationen aus der Datei "NuGet.config" nicht für VSTS-Feeds - [#2647](https://github.com/NuGet/Home/issues/2647)

* [Dotnet-Restore]--Configfile ist relativ zum Projekt Dir anstelle der Cmd-Dir - [#2639](https://github.com/NuGet/Home/issues/2639)

* Übermäßig viele Zuordnungen im Code von Version-Vergleichs - [#2632](https://github.com/NuGet/Home/issues/2632)

* Mehrere Instanzen von nuget.exe gleich installieren möchten-Paket in parallelen bewirkt, dass einen double-Schreibvorgang - [#2628](https://github.com/NuGet/Home/issues/2628)

* Informationen zu den Abhängigkeiten ist nicht für mehrere Projekte – Vorgänge – zwischengespeichert [#2619](https://github.com/NuGet/Home/issues/2619)

* Installieren und aktualisieren Sie die Downloadpakete ohne Überprüfung der Ordner "Pakete" zuerst - [#2618](https://github.com/NuGet/Home/issues/2618)

* Wenn die Liste der Pakete-Quelle leer ist, kann nicht Paketquelle Benutzeroberfläche hinzugefügt (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Irreführender Fehler, wenn Sie versuchen, das Paket zu installieren, von denen abhängt, während der Entwurfszeit Fassaden - [#2594](https://github.com/NuGet/Home/issues/2594)

* Installieren eines Pakets von PackageManager-Konsole mit der Einstellung "Alle" aus versucht nur erste Quelle - [#2557](https://github.com/NuGet/Home/issues/2557)

* Neueste Betaversion nicht Entzippen ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)

* Absturz von Visual Studio 2015 beim Start mit selbst erstellten NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)

* Befehl "Update" ist möglicherweise ein wenig ausführlicher, wenn i Datenbankanmeldeinformationen... – werden Fragen [#2418](https://github.com/NuGet/Home/issues/2418)

* Lokal erstellten VSIX müssen dieselben DLLs und Dateien wie der CI-Build. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Beheben Sie Warnungen für NuGet-Herabstufung im Build - [#2396](https://github.com/NuGet/Home/issues/2396)

* Paketquelle (3 Mal) authentifizieren nicht unbegrenzt - blockiert [#2362](https://github.com/NuGet/Home/issues/2362)

* Paketinhalt wird nicht ordnungsgemäß wiederhergestellt, beim Installieren eines Pakets aus einem Nuget-Version 3.3 +-mit dem Argument Feeds - NoCache, wenn das Paket enthält `.nupkg` Dateien – [#2354](https://github.com/NuGet/Home/issues/2354)

* Installieren von NuGet mit alle Paketquellen, aber das Paket umfasst keine aus Quelle 1 ein Fehler auftritt – [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt; &gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;B__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)

* Installieren Sie Blöcke, fällt eine einzelne Quelle Authorization - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` Bereich sollten außer Kraft setzen - IncludeReferencedProjects Version – Version [#1983](https://github.com/NuGet/Home/issues/1983)

* Update-Package extrem langsam: "Es wurde versucht zum Sammeln von Informationen von Abhängigkeiten" - [#1909](https://github.com/NuGet/Home/issues/1909)

* Geschützter Downgrades von NuGet-Paket beim Batch - Abhängigkeiten aktualisieren [#1903](https://github.com/NuGet/Home/issues/1903)

* NuGet.exe-Update löscht die Assembly starke Namen und das Private-Attribut. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Relativen Pfad für "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)

* Verbesserung der Fehlermeldungen Resolver - [#1373](https://github.com/NuGet/Home/issues/1373)

* V3-Update-Paket ein Fehler auftritt, mit Paketen, die nicht in der angegebenen Quelle - [#1013](https://github.com/NuGet/Home/issues/1013)

* Das verwenden relativer Pfade für die Paketquellen ist problematisch, Verwendung von - [#865](https://github.com/NuGet/Home/issues/865)

* Fehlende Abhängigkeit in NUPKG-Datei aus Projekt generiert wird, wenn indirekte Abhängigkeit mit einer niedrigeren versionsanforderung bereits - [#759](https://github.com/NuGet/Home/issues/759)

* Löschen ein Projekt wird die entsprechende Benutzeroberfläche-Fenster geschlossen, aber Umbenennen eines Projekts UI-Fenster nicht umbenannt. Beachten Sie, dass die PMC umbenennen und Projekt entfernen-Ereignisse – überwacht [#670](https://github.com/NuGet/Home/issues/670)

* [Willow-Web-Workload] Hängt, erstellen Razor v3 WSP - [#3241](https://github.com/NuGet/Home/issues/3241)

* Installation/Wiederherstellung eines bestimmten Pakets schlägt fehl mit "enthält Paket mehrere Nuspec-Dateien." - [#3231](https://github.com/NuGet/Home/issues/3231)

* Kleinbuchstaben IDs & `packages.config` Szenarien – [#3209](https://github.com/NuGet/Home/issues/3209)

* [3.5-beta2] Wiederherstellen von Paketen nicht wiederherstellen "legacy" Pakete - [#3208](https://github.com/NuGet/Home/issues/3208)

* NuGet Pack fügt das TT-Dateien zum Ordner "Content" unabhängig davon, was - [#3203](https://github.com/NuGet/Home/issues/3203)

* Update-Package, ASP.NET Web-App generiert die Warnung im Zusammenhang mit der Datei: Source - [#3194](https://github.com/NuGet/Home/issues/3194)

* NuGet Pack Csproj (mit `project.json`) stürzt ab, wenn es keine PackOptions und Besitzer in der JSON-Datei sind - [#3180](https://github.com/NuGet/Home/issues/3180)

* NuGet Pack für `project.json` ignoriert PackOptions Tags wie Zusammenfassung, Autoren und Besitzer usw. – [#3161](https://github.com/NuGet/Home/issues/3161)

* "NullReferenceException" über NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)

* NuGet Pack werden die Abhängigkeiten in der Ausgabe ignoriert `.nuspec` für `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Aktualisieren mehrere Pakete mit Rollback lässt das Projekt in einem unterbrochenen Zustand - [#3139](https://github.com/NuGet/Home/issues/3139)

* "Contentfiles", unter einer werden nicht hinzugefügt werden, für die Netstandard-Projekte – [#3118](https://github.com/NuGet/Home/issues/3118)

* Kann nicht gepackt werden Library für .net Standard ordnungsgemäß - [#3108](https://github.com/NuGet/Home/issues/3108)

* Datei -> Neues Projekt -> Klassenbibliothek (portabel) ein Fehler auftritt-Projekt in Visual Studio 2015 und Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* NuGet-Fehler: 1.0.0-* ist keine gültige Versionszeichenfolge - [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package ein Fehler auftritt, anzeigen, aber funktioniert für Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Fehler bei "Install-Package jquery.validation" auf dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* Ungültiger Zielpfad - NuGet-Paket von Xproj Standardwert ist [#3060](https://github.com/NuGet/Home/issues/3060)

* Bei der installierten Visual Studio 2015 update 3 für einen im Vergleich, der verwendet NuGet 3.5.0-Versionsfehler tritt auf, - [#3053](https://github.com/NuGet/Home/issues/3053)

* "Von" Packages.config "blockiert" in `project.json` (UWP, bzw.-Build integriert)-Projekt – [#3046](https://github.com/NuGet/Home/issues/3046)

* Aktualisieren Sie die Dotnet-Cli, die vom Buildskript, um Preview 2-003121, die in der offiziellen Preview 2-Build ist installiert. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Paket-Manager-Benutzeroberfläche: neue Version nicht angezeigt werden, nach dem Aktualisieren eines Pakets- [#3041](https://github.com/NuGet/Home/issues/3041)

* -"Apikey" Befehlszeile für Delete-Befehl nicht Lese-/gesendet 3.5.0-Beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Falsches Zeichenfolgenformat: eine stabile Version eines Pakets müssen sich nicht auf einer Vorabversion Abhängigkeit. - [#3030](https://github.com/NuGet/Home/issues/3030)

* OptimizedZipPackage Cache bewirkt, dass leere Ordner - [#3029](https://github.com/NuGet/Home/issues/3029)

* Erstellen die PCL (net46 und Windows 10)-Projekt Get NullRef-Ausnahme. - [#3014](https://github.com/NuGet/Home/issues/3014)

* NuGet-Updates sollten informationsmeldung bereitstellen, wenn eine höhere Version durch Einschränkung der AllowedVersions - eingeschränkt ist [#3013](https://github.com/NuGet/Home/issues/3013)

* Probleme mit NuGet v3 der datenbankwiederherstellung - [#2891](https://github.com/NuGet/Home/issues/2891)

* Anmeldeinformationen-Plug-in wurde mit Fehler-1 beendet / Fehler beim Herunterladen bei Verwendung der Anmeldeinformationsanbieter mit mehreren Quellen – package [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` NuGet-Wiederherstellung führt dazu, dass eine Neukompilierung, wenn nichts geändert – [#2817](https://github.com/NuGet/Home/issues/2817)

* Symbolpakete sollte nicht immer in installieren oder Aktualisieren von - verwendet [#2807](https://github.com/NuGet/Home/issues/2807)

* Visual Studio unterstützt keine Umgebungsvariablen im RepositoryPath (nuget.exe bewirkt) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Bezeichnung der noch nicht gekennzeichneten UIElements im Paket-Manager-UI für die Barrierefreiheit - [#2745](https://github.com/NuGet/Home/issues/2745)

* Portable-Frameworks mit Bindestrichen Profile werden abgelehnt. - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet-Paket-Manager sollten diese Optionsliste in Paketen zu verdeutlichen, Detail nicht für gilt, `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet.exe-Push/Delete-API-Schlüssel – nicht verwendet, [#2627](https://github.com/NuGet/Home/issues/2627)

* Entfernen Sie die gesperrte Eigenschaft aus der Sperrdatei - [#2379](https://github.com/NuGet/Home/issues/2379)

* NuGet 3.3.0-Aktualisierung ein Fehler auftritt, mit "... eine zusätzliche Einschränkung definiert" Packages.config "wird verhindert, dass dieser Vorgang." - [#1816](https://github.com/NuGet/Home/issues/1816)

* Installieren des Pakets aus einer lokalen Quelle, die nicht vorhanden ist löst einer gefälschten Nachricht - [#1674](https://github.com/NuGet/Home/issues/1674)

* "Upgrade verfügbar"-Filter werden Upgrades, bei denen die versionseinschränkung - verletzen [#1094](https://github.com/NuGet/Home/issues/1094)

* Kann nicht aktualisiert werden native Pakete - [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Features

* Einstellung CopyLocal auf "false" für hinzugefügt, die von NuGet - Verweise unterstützen [#329](https://github.com/NuGet/Home/issues/329)

* NuGet.exe-Unterstützung für MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)

* Unterstützung für.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Benutzeraktion zu deaktivieren, wenn Benutzer Aktionen ausgeführt wird – [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet sollten Hinzufügen von Unterstützung für `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* Hinzufügen des Framework Probleme mit der fehlt in NuGet 2.x (die bereits in 3.x sind) - [#2720](https://github.com/NuGet/Home/issues/2720)

* Unterstützung für den fallback-Paket-Ordner - [#2899](https://github.com/NuGet/Home/issues/2899)

* Entwerfen und implementieren Sie eine Vorstellung von Pakettyp Tool Pakete, unterstützen [#2476](https://github.com/NuGet/Home/issues/2476)

* Hinzufügen einer API zum Abrufen des Pfads zu dem Ordner mit globalen Paketen - [#2403](https://github.com/NuGet/Home/issues/2403)

* Aktivieren von SemVer 2.0.0 im Paket - [von #3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>DCRs

* NuGet.exe-Push - Timeout-Parameter funktioniert nicht – [#2785](https://github.com/NuGet/Home/issues/2785)

* Beschreibungstext des Pakets muss auswählbare - [#1769](https://github.com/NuGet/Home/issues/1769)

* Aktivieren von nuget.exe erzeugt `.props` und `.targets` -Dateien für `.nuproj` Projekte [#2711](https://github.com/NuGet/Home/issues/2711)

* Hinzufügen-Erweiterbarkeits-API-Frameworks mit Imports - vergleichen [#2633](https://github.com/NuGet/Home/issues/2633)

* Abhängigkeitsoptionen ausblenden, wenn mit `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Drucken Sie nuget.exe-Version-Header in der ausführlichen Ausgabe - [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet muss, damit Benutzer wissen, dass in einem Dotnet Tfm-basierte aktualisieren bzw. installieren PCL-Fehlern – verursachen [#3138](https://github.com/NuGet/Home/issues/3138)

* Ungültige installieren/aktualisieren für Projekt mit Tfm warnen = "Dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)

* Beheben von Leistungsproblemen mit ReShaper und NuGet für Update - [#3044](https://github.com/NuGet/Home/issues/3044)

* Hinzufügen von Unterstützung für netcoreapp11 und netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* AssemblyMetadata-Attribut für nutzen `.nuspec` Ersetzungen - token [#2851](https://github.com/NuGet/Home/issues/2851)
