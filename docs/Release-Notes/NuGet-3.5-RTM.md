---
title: NuGet-3.5 Beta-Versionshinweise | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 082a96b9-607b-4225-864d-e1cea537f591
description: "Versionshinweise für NuGet 3.5 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-3.5 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0a0f039d2529e1d41bbc0c7f9ac3f76f51f96ce5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
#<a name="nuget-35-release-notes"></a>3.5 NuGet-Versionshinweise

[NuGet-3.5 RC-Versionsanmerkungen](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC-Versionsanmerkungen](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Fehlerkorrekturen

* Pack verwendet MSBuild 14,1 nicht auf das Mono - [#3550](https://github.com/NuGet/Home/issues/3550)

* Registerkarte "Update" nicht die neueste verfügbare Version select derzeitig installierten Version - stattdessen aktualisieren wählen [#3498](https://github.com/NuGet/Home/issues/3498)

* Beheben von Absturz (Crash) nach der Authentifizierung einen privaten v2 MyGet feed und durch Klicken auf "X Weitere Ergebnisse anzeigen"- [#3469](https://github.com/NuGet/Home/issues/3469)

* Protokollmeldungen für UI - in umgekehrter Reihenfolge zu sein scheinen [#3446](https://github.com/NuGet/Home/issues/3446)

* V3.4.4 - NuGet-Wiederherstellung löst "das Format des angegebenen Pfads wird nicht unterstützt" - [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet-CmdLine 3.6 Beta berücksichtigt keine - Prop Configuration = Release – [#3432](https://github.com/NuGet/Home/issues/3432)

* Installieren Sie NuGet IKVM langsam auf großen Projekten - [#3428](https://github.com/NuGet/Home/issues/3428)

* NuGet.exe - Self-Service behält auf sich selbst zu aktualisieren – Update [#3395](https://github.com/NuGet/Home/issues/3395)

* 3.5 installieren/Wiederherstellen von UNC-Freigabe hat 3.4.4 - Leistung Regression [#3355](https://github.com/NuGet/Home/issues/3355)

* Fehler bei der Installation von Moq aus der Paket-Benutzeroberfläche für ein Projekt net451 - [#3349](https://github.com/NuGet/Home/issues/3349)

* Registerkarte "installieren" auf Projektmappenebene nicht anzeigen des Paketversion - [#3339](https://github.com/NuGet/Home/issues/3339)

* Xproj `project.json` Aktualisierung über die Registerkarte "installiert" verliert State - [#3303](https://github.com/NuGet/Home/issues/3303)

* NuGet-Pack auf `.csproj` ignoriert leere Files-Element im `.nuspec` Datei - [#3257](https://github.com/NuGet/Home/issues/3257)

* Websiteprojekten in IIS gehostete sollte nicht dazu, dass der Wiederherstellung fehl - [#3235](https://github.com/NuGet/Home/issues/3235)

* Anmeldeinformationen, die nicht von "NuGet.config" abgerufen werden, wenn v3-Endpunkt auf v2 - leitet [#3179](https://github.com/NuGet/Home/issues/3179)

* NuGet-Pack nicht Assembly aufgelöst wird, beim Abrufen von Assemblymetadaten für portable - [#3128](https://github.com/NuGet/Home/issues/3128)

* NuGet wurde nicht gefunden. `msbuild.exe` auf Mono - [#3085](https://github.com/NuGet/Home/issues/3085)

* NuGet.exe Pack ein Pre-Release-Tag, das mit Zahlen - beginnt kann keine [#1743](https://github.com/NuGet/Home/issues/1743)

* Installieren von NuGet-Paket erzeugt einen Fehler, die auf VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)

* "allowedversions" Filtern funktioniert nicht auf Projektmappenebene - [#333](https://github.com/NuGet/Home/issues/333)

* Wiederherstellung nach dem Zufallsprinzip schlägt fehl, mit einem Element mit demselben Schlüssel wurde bereits hinzugefügt. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Kann nicht installiert werden Nuget.Common in `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* Wenn die Benutzeroberfläche verwenden, um eine V2-Quelle zu suchen, heißt FindPackagesById zweimal für jede ID - [#2517](https://github.com/NuGet/Home/issues/2517)

* Pakete können nicht für Projekte - abhängen [#2490](https://github.com/NuGet/Home/issues/2490)

* NuGet.exe-Pack - Exclude dokumentiert jedoch nicht unterstützt - [#2284](https://github.com/NuGet/Home/issues/2284)

* Probleme mit dem Fehler Instanznachrichten an, wenn im Abschnitt "Inhaltsdateien" `.nuspec` ist ungültig - [#1686](https://github.com/NuGet/Home/issues/1686)

* Push sendet immer die gesamtes Paket zweimal mit authentifiziert Paketquellen - [#1501](https://github.com/NuGet/Home/issues/1501)

* Es werden keine Informationen wurde beim Aufrufen von nuget.exe Update *.csproj, während das Projekt keinen angegeben ein `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config`Wiederherstellung wird nicht erneut versucht, auf 5xx-Statuscodes aus Quellen für V2 - [#1217](https://github.com/NuGet/Home/issues/1217)

* Doppelte Punkte in der Datei Src in `.nuspec` funktioniert nicht – [#2947](https://github.com/NuGet/Home/issues/2947)

* Ignorieren von Feeds mit Verschlüsselung - CoreCLR wiederherstellen muss [#2942](https://github.com/NuGet/Home/issues/2942)

* NuGet.exe push 403 - falsch zum Eingeben von Anmeldeinformationen aufzufordern - Behandlung [#2910](https://github.com/NuGet/Home/issues/2910)

* NuGet-Update durch den Paketmanager entfernt, Eigenschaften aus der `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* NuGet.PackageManagement.VisualStudio versuchen Sie es beim Laden von "NuGet.TeamFoundationServer14", aber, dass die DLL-Namen in "NuGet.TeamFoundationServer" - geändert [#2857](https://github.com/NuGet/Home/issues/2857)

* Paket-Manager, die die Benutzeroberfläche nicht werden neu angezeigt aktualisierte Version - [#2828](https://github.com/NuGet/Home/issues/2828)

* Updatepaket möchten, verwenden Sie die Paket-ID, Version statt package.version - [#2771](https://github.com/NuGet/Home/issues/2771)

* NuGet Restore Csproj sollten Fehler auf, wenn das Projekt mithilfe von Nuget ist nicht (`packages.config` oder `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)

* TFS-Fehler "[Datei] nicht in Ihrem Arbeitsbereich gefunden, oder Sie keine Berechtigung für den Zugriff" beim Aktualisieren oder deinstallieren, wenn TFS-quellcodeverwaltung - Projektmappe/Projekt gebunden ist [#2739](https://github.com/NuGet/Home/issues/2739)

* das Updatepaket nicht abrufen Abhängigkeiten für Pakete von nicht-Ziel - [#2724](https://github.com/NuGet/Home/issues/2724)

* Es gibt keine Möglichkeit, den Ausführlichkeitsgrad für NuGet-Paket-Manager-UI-Aktionen - Protokolle festlegen [#2705](https://github.com/NuGet/Home/issues/2705)

* die NuGet-Konfiguration ist ungültig – VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) funktioniert nicht – [#2653](https://github.com/NuGet/Home/issues/2653)

* NuGet 3.4.3 Version - Wert darf nicht null sein beim Erstellen des Paket - [#2648](https://github.com/NuGet/Home/issues/2648)

* Wiederherstellung verwendeten gespeicherten Anmeldeinformationen von "NuGet.config" nicht für VSTS-Feeds - [#2647](https://github.com/NuGet/Home/issues/2647)

* [Dotnet wiederherstellen]--Configfile ist relativ zum Projekt Dir anstelle der Cmd-Dir - [#2639](https://github.com/NuGet/Home/issues/2639)

* Eine übermäßige Zuordnungen in Code von Version Vergleiche - [#2632](https://github.com/NuGet/Home/issues/2632)

* Mehrere Instanzen von nuget.exe identisch installieren möchten-Pakets in parallelen Ursachen einen double-Schreibvorgang - [#2628](https://github.com/NuGet/Home/issues/2628)

* Abhängigkeitsinformationen für mehrere Projekte Operations - nicht zwischengespeichert [#2619](https://github.com/NuGet/Home/issues/2619)

* Installieren und Aktualisieren von Downloadpaketen ohne Überprüfung der Ordner "Pakete" zuerst - [#2618](https://github.com/NuGet/Home/issues/2618)

* Wenn Paketliste für die Quelle leer ist, kann nicht hinzugefügt werden über den Benutzeroberflächen-Quelldateien (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Irreführende Fehler beim Installieren des Pakets, die zur Entwurfszeit Fassaden - abhängt [#2594](https://github.com/NuGet/Home/issues/2594)

* Nur erste Quelle - Installation eines Pakets aus PackageManager-Konsole mit der Einstellung "Alle" versucht [#2557](https://github.com/NuGet/Home/issues/2557)

* Neueste Beta nicht dekomprimieren ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)

* VS2015 Absturz beim Start mit sich selbst erstellte NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)

* Aktualisierungsbefehl möglicherweise etwas ausführlicher Wenn i bitten Sie ihn abgeschnitten - [#2418](https://github.com/NuGet/Home/issues/2418)

* VSIX lokal erstellten müssen die DLLs und die Dateien wie der CI-Build. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Beheben von NuGet Downgrade für die Warnungen in den Build - [#2396](https://github.com/NuGet/Home/issues/2396)

* Wegen eines Fehlers beim Paketquelle (3 Mal) authentifizieren forever - blockiert [#2362](https://github.com/NuGet/Home/issues/2362)

* Paketinhalt wird nicht ordnungsgemäß wiederhergestellt, beim Installieren eines Pakets von Nuget v3. 3 +-mit dem Argument Feeds - NoCache, wenn das Paket enthält `.nupkg` Dateien - [#2354](https://github.com/NuGet/Home/issues/2354)

* NuGet-Installation mit allen Paketquellen überein, aber Paket fehlt in der 1-Quelle und ein Fehler auftritt - [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt; &gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;B__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)

* Blöcke zu installieren, schlägt eine einzelne Datenquelle Autorisierung - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec`Version Bereich sollten IncludeReferencedProjects - Version - überschreiben [#1983](https://github.com/NuGet/Home/issues/1983)

* Updatepaket super langsam - "versucht, Abhängigkeiten Informationen sammeln" - [#1909](https://github.com/NuGet/Home/issues/1909)

* Stealth Downgrades von NuGet-Paket beim Batch aktualisieren seiner Abhängigkeiten - [#1903](https://github.com/NuGet/Home/issues/1903)

* NuGet.exe Update löscht den starken Assemblynamen und privaten Attribut. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Ein relativer Dateipfad für "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)

* Verbesserung der Fehlermeldungen Resolver - [#1373](https://github.com/NuGet/Home/issues/1373)

* Updatepaket in v3 schlägt fehl mit Paketen, die nicht in der angegebenen Quelle - [#1013](https://github.com/NuGet/Home/issues/1013)

* Verwenden relative Pfade für Paketquellen ist problematisch verwenden - [#865](https://github.com/NuGet/Home/issues/865)

* Fehlende Abhängigkeit in NUPKG-Datei, die vom Projekt generiert wird, wenn indirekte Abhängigkeit mit einer niedrigeren Version Anforderung bereits - [#759](https://github.com/NuGet/Home/issues/759)

* Löschen ein Projekt entsprechende UI-Fenster geschlossen, aber Umbenennen eines Projekts im UI-Fenster nicht umbenennen. Beachten Sie, dass das Projekt umbenennen und Projekt entfernen-Ereignisse – PMC überwacht [#670](https://github.com/NuGet/Home/issues/670)

* [Willow Web Arbeitsauslastung] Hängenbleiben erstellen Razor v3 WSP - [#3241](https://github.com/NuGet/Home/issues/3241)

* Installation/Wiederherstellung eines bestimmten Pakets schlägt fehl mit "enthält Paket mehrere Nuspec-Dateien." - [#3231](https://github.com/NuGet/Home/issues/3231)

* Kleinbuchstaben IDs & `packages.config` Szenarien – [#3209](https://github.com/NuGet/Home/issues/3209)

* [3.5 beta2] Wiederherstellen von "legacy" Paketen - paketwiederherstellung nicht [#3208](https://github.com/NuGet/Home/issues/3208)

* NuGet-Pack fügt erzwungen TT-Dateien in Inhaltsordner unabhängig davon, was - [#3203](https://github.com/NuGet/Home/issues/3203)

* Updatepaket von ASP.NET Web-app generiert die Warnung im Zusammenhang mit der Datei: Quelle - [#3194](https://github.com/NuGet/Home/issues/3194)

* NuGet-Pack Csproj (mit `project.json`) stürzt ab, wenn es keine PackOptions "und" Besitzer in JSON-Datei sind - [#3180](https://github.com/NuGet/Home/issues/3180)

* NuGet-Pack für `project.json` ignoriert PackOptions Tags wie Zusammenfassung, Autoren und Besitzer usw. - [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException über NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)

* NuGet-Pack ignoriert Abhängigkeiten in der Ausgabe `.nuspec` für `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Aktualisieren mehrere Pakete mit Rollback lässt das Projekt in einem fehlerhaften Zustand versetzt - [#3139](https://github.com/NuGet/Home/issues/3139)

* Inhaltsdateien unter einer werden nicht hinzugefügt, für die netstandard-Projekte - [#3118](https://github.com/NuGet/Home/issues/3118)

* Bibliothek für .net Paket kann nicht standardmäßige ordnungsgemäß - [#3108](https://github.com/NuGet/Home/issues/3108)

* Datei -> Neues Projekt-Klassenbibliothek (portabel) Projekt fehl in VS2015 und Dev15 - > [#3094](https://github.com/NuGet/Home/issues/3094)

* NuGet-Fehler: 1.0.0-* ist keine gültige Versionszeichenfolge - [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package ein Fehler auftritt, um die Anzeige "," Install-Package Works - [#3068](https://github.com/NuGet/Home/issues/3068)

* Fehler bei "Install-Package jquery.validation" auf dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* Ungültiger Zielpfad - NuGet-Paket mit Xproj direktionales ist [#3060](https://github.com/NuGet/Home/issues/3060)

* Bei der installierten Visual Studio 2015 update 3 auf einem VS, die NuGet-Version 3.5.0 Fehlers - verwendet [#3053](https://github.com/NuGet/Home/issues/3053)

* "Von" Packages.config "blockiert" in `project.json` (UWP, bzw. Build integriert) Projekt - [#3046](https://github.com/NuGet/Home/issues/3046)

* Aktualisieren Sie Dotnet Cli vom Buildskript auf Preview 2-003121, der offiziellen Preview 2 ist installiert. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Paket-Manager-Benutzeroberfläche: keine neue Version angezeigt, nach dem Aktualisieren eines Pakets- [#3041](https://github.com/NuGet/Home/issues/3041)

* -"Apikey" für Delete-Befehlszeile nicht Lese-/gesendet 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Falsches Zeichenfolgenformat: eine stabile Version eines Pakets sollte keine für eine Vorabversion Abhängigkeit. - [#3030](https://github.com/NuGet/Home/issues/3030)

* OptimizedZipPackage Cache bleibt leere Ordner - [#3029](https://github.com/NuGet/Home/issues/3029)

* Erstellen PCL (net46 und Windows 10)-Projekt Get NullRef-Ausnahme. - [#3014](https://github.com/NuGet/Home/issues/3014)

* NuGet-Update sollten informationsmeldung bereitstellen, wenn eine höhere Version von "allowedversions"-Einschränkung - beschränkt ist [#3013](https://github.com/NuGet/Home/issues/3013)

* NuGet-v3-Restore-Fehlern – [#2891](https://github.com/NuGet/Home/issues/2891)

* Anmeldeinformationen-Plug-in wurde mit dem Fehlercode:-1 / Fehler herunterladen bei Verwendung von mehreren Quellen - Anmeldeinformationsanbieter mit package [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json`NuGet Restore bewirkt, dass neu kompiliert, wenn nichts geändert - [#2817](https://github.com/NuGet/Home/issues/2817)

* Symbole Pakete sollte jemals nicht verwendet werden, in der Installations- oder Update - [#2807](https://github.com/NuGet/Home/issues/2807)

* Visual Studio unterstützt keine Umgebungsvariablen im RepositoryPath (nuget.exe bewirkt) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Bezeichnen Sie die unbenannten UIElements im Paket-Manager-UI für Eingabehilfen - [#2745](https://github.com/NuGet/Home/issues/2745)

* Portable Frameworks mit getrennten Profilen werden zurückgewiesen. - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet-Paket-Manager sollten unmissverständlich, Optionsliste in Paketen Detail nicht für gilt `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet.exe Push/Delete nicht API-Schlüssel - verwendet [#2627](https://github.com/NuGet/Home/issues/2627)

* Entfernen Sie die gesperrte Eigenschaft aus der Sperrdatei - [#2379](https://github.com/NuGet/Home/issues/2379)

* NuGet 3.3.0 Update schlägt fehl mit "eine weitere Einschränkung... definiert" Packages.config ", verhindert diesen Vorgang." - [#1816](https://github.com/NuGet/Home/issues/1816)

* Installieren von einer lokalen Quelle, die löst nicht vorhanden ist eine gefälschte Nachricht - Paket [#1674](https://github.com/NuGet/Home/issues/1674)

* "Upgrade verfügbar" Filter zeigt Upgrades, die die versionseinschränkung - verletzen [#1094](https://github.com/NuGet/Home/issues/1094)

* Kann nicht aktualisiert werden systemeigene Pakete - [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Features

* Einstellung CopyLocal auf "false" für hinzugefügten von NuGet - Verweise unterstützen [#329](https://github.com/NuGet/Home/issues/329)

* NuGet.exe-Unterstützung für die MSBuild-15 - [#1937](https://github.com/NuGet/Home/issues/1937)

* Pack-Unterstützung für.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Deaktivieren Sie Handlung des Benutzers aus, wenn es werden Aktionen des Benutzers ausgeführt wird- [#1440](https://github.com/NuGet/Home/issues/1440)

* Sollte zum Hinzufügen von NuGet-Unterstützung für `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* Hinzufügen von Framework Kompatibilitäten fehlt in der NuGet 2.x (die bereits in 3.x sind) - [#2720](https://github.com/NuGet/Home/issues/2720)

* Unterstützung für alternative paketordnern - [#2899](https://github.com/NuGet/Home/issues/2899)

* Entwerfen und implementieren Sie eine Vorstellung von den Pakettyp Tool Pakete - Unterstützung [#2476](https://github.com/NuGet/Home/issues/2476)

* Hinzufügen einer API zum Abrufen des Pfads zum Paketordner globalen - [#2403](https://github.com/NuGet/Home/issues/2403)

* Aktivieren von SemVer 2.0.0 im Paket - [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>Archivierung von dcrs Design

* NuGet.exe Push - Timeoutparameter funktioniert nicht – [#2785](https://github.com/NuGet/Home/issues/2785)

* Beschreibungstext des Pakets muss auswählbare - [#1769](https://github.com/NuGet/Home/issues/1769)

* Aktivieren Sie nuget.exe erzeugt `.props` und `.targets` Dateien für `.nuproj` Projekte [#2711](https://github.com/NuGet/Home/issues/2711)

* Hinzufügen von Erweiterbarkeits-API zum Vergleichen von Importen - Frameworks [#2633](https://github.com/NuGet/Home/issues/2633)

* Abhängigkeitsoptionen ausblenden, wenn mit `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Drucken nuget.exe-Versionsheader in ausführliche Ausgabe - [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet muss, damit Benutzer wissen, dass ein Upgrade/Installation in ein Dotnet-Tfm basierend PCL Probleme - verursachen könnte [#3138](https://github.com/NuGet/Home/issues/3138)

* Warnhinweis anzeigen, fehlerhafte installiert oder aktualisiert für das Projekt mit Tfm "Dotnet" - = [#3137](https://github.com/NuGet/Home/issues/3137)

* Beheben von Leistungsproblemen mit ReShaper und NuGet für Update - [#3044](https://github.com/NuGet/Home/issues/3044)

* Hinzufügen von netcoreapp11 und netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Nutzen der Vorteile AssemblyMetadata-Attribut für `.nuspec` Ersetzungen - token [#2851](https://github.com/NuGet/Home/issues/2851)
