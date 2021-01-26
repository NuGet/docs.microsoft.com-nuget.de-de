---
title: Anmerkungen zu Version 3.5 RTM von NuGet
description: Anmerkungen zu dieser Version von nuget 3,5 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776348"
---
# <a name="nuget-35-release-notes"></a>Anmerkungen zu dieser Version von nuget 3,5

Anmerkungen zu dieser [Version von nuget 3,5-RC](../release-notes/nuget-3.5-RC.md)  |  [Anmerkungen zu dieser Version von nuget 4,0 RC](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Fehlerkorrekturen

* Das Paket verwendet MSBuild 14,1 nicht auf Mono- [#3550](https://github.com/NuGet/Home/issues/3550)

* Registerkarte "Aktualisieren" wählt nicht die aktuellste verfügbare Version zum Aktualisieren aus. Wählen Sie stattdessen die aktuell installierte [#3498](https://github.com/NuGet/Home/issues/3498) Version

* Beheben Sie den Absturz nach dem Authentifizieren eines privaten v2-myget-Feeds, und klicken Sie auf "x weitere Ergebnisse anzeigen"- [#3469](https://github.com/NuGet/Home/issues/3469)

* Protokollmeldungen sind anscheinend in umgekehrter Reihenfolge für die Benutzeroberfläche [#3446](https://github.com/NuGet/Home/issues/3446)

* v 3.4.4-nuget-Wiederherstellung löst das Format "das angegebene Pfad Format wird nicht unterstützt"- [#3442](https://github.com/NuGet/Home/issues/3442)

* Nuget-cmdline 3,6 Beta hat keine Unterstützung für "-prop Configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)

* Nuget-Unternehmen: langsame Installation auf einem großen Projekt [#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe Update-Self behält die Aktualisierung selbst bei [#3395](https://github.com/NuGet/Home/issues/3395)

* 3,5 die Installation/Wiederherstellung über die UNC-Freigabe hat eine Leistungs Regression von 3.4.4- [#3355](https://github.com/NuGet/Home/issues/3355)

* Fehler beim Installieren von "muq" über die Benutzeroberfläche der Paketverwaltung für ein net451-Projekt [#3349](https://github.com/NuGet/Home/issues/3349)

* Registerkarte "installieren" auf Projektmappenebene zeigt die Version des Pakets nicht an [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj- `project.json` Update von installierter Registerkarte verliert Status- [#3303](https://github.com/NuGet/Home/issues/3303)

* Das nuget-Paket unter `.csproj` ignoriert ein leeres Files-Element in `.nuspec` file- [#3257](https://github.com/NuGet/Home/issues/3257)

* In IIS gehostete Website Projekte sollten nicht zu einem Fehler bei der Wiederherstellung führen [#3235](https://github.com/NuGet/Home/issues/3235)

* Anmelde Informationen, die nicht von Nuget.Config abgerufen werden, wenn der V3-Endpunkt zu v2- [#3179](https://github.com/NuGet/Home/issues/3179) umgeleitet

* Das nuget-Paket kann die Assembly beim Abrufen von portablen Assemblymetadaten nicht auflösen- [#3128](https://github.com/NuGet/Home/issues/3128)

* Nuget kann `msbuild.exe` auf Mono- [#3085](https://github.com/NuGet/Home/issues/3085) nicht finden

* nuget.exe Pack lässt kein vorab Veröffentlichungstag zu, das mit Zahlen beginnt [#1743](https://github.com/NuGet/Home/issues/1743)

* Fehler beim Installieren des nuget-Pakets auf VS2015E- [#1298](https://github.com/NuGet/Home/issues/1298)

* der "Zuweisung-Filter" funktioniert auf Projektmappenebene nicht [#333](https://github.com/NuGet/Home/issues/333)

* Die Wiederherstellung nach dem Zufallsprinzip schlägt fehl, wenn ein Element mit demselben Schlüssel bereits hinzugefügt wurde. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Nuget kann nicht installiert werden. common in `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* Wenn Sie die Benutzeroberfläche zum Durchsuchen einer v2-Quelle verwenden, wird findpackagesbyid für jede ID zweimal aufgerufen [#2517](https://github.com/NuGet/Home/issues/2517)

* Pakete können nicht von Projekten abhängen [#2490](https://github.com/NuGet/Home/issues/2490)

* nuget.exe Pack-Exclude ist dokumentiert, wird jedoch nicht unterstützt [#2284](https://github.com/NuGet/Home/issues/2284)

* Probleme mit Fehlermeldungen, wenn der Abschnitt "contentfiles" von `.nuspec` ungültig ist- [#1686](https://github.com/NuGet/Home/issues/1686)

* Push sendet das gesamte Paket immer zweimal mit den authentifizierten Paketquellen [#1501](https://github.com/NuGet/Home/issues/1501)

* Beim Aufrufen von nuget.exe Update *. csproj wurden keine Informationen angegeben, während das Projekt keine `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` bei der Wiederherstellung wird der 5XX-Statuscode aus V2-Quellen nicht wiederholt [#1217](https://github.com/NuGet/Home/issues/1217)

* Der doppelte Punkt in der Datei src in `.nuspec` funktioniert nicht [#2947](https://github.com/NuGet/Home/issues/2947)

* Die CoreCLR-Wiederherstellung muss Feeds mit Verschlüsselung ignorieren [#2942](https://github.com/NuGet/Home/issues/2942)

* nuget.exe Push 403-Behandlung-falsche Eingabe von Anmelde Informationen [#2910](https://github.com/NuGet/Home/issues/2910)

* Das nuget-Update über den Paket-Manager entfernt Eigenschaften aus dem `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* Nuget. packagemanagement. VisualStudio versucht, "nuget. TeamFoundationServer14" zu laden, aber der DLL-Name wurde in "nuget. TeamFoundationServer" geändert- [#2857](https://github.com/NuGet/Home/issues/2857)

* Die Benutzeroberfläche des Paket-Managers zeigt keine neu aktualisierte Version [#2828](https://github.com/NuGet/Home/issues/2828)

* Update-Paket versucht, PackageID, Version anstelle von Package. Version- [#2771](https://github.com/NuGet/Home/issues/2771) zu verwenden

* beim nuget-Wiederherstellungs-csproj sollte ein Fehler auftreten, wenn das Projekt keine nuget `packages.config` -(oder `project.json` )- [#2766](https://github.com/NuGet/Home/issues/2766)

* Der TFS-Fehler "[Datei] wurde in Ihrem Arbeitsbereich nicht gefunden, oder Sie haben keine Zugriffsberechtigung" während des Upgrades oder der Deinstallation, wenn Projekt Mappe/Projekt an TFS-Quell Code Verwaltung gebunden ist [#2739](https://github.com/NuGet/Home/issues/2739)

* Das Update Paket erhält keine Abhängigkeiten von nicht Ziel Paketen- [#2724](https://github.com/NuGet/Home/issues/2724)

* Es gibt keine Möglichkeit, den ausführlichkeits Grad der Protokolle für UI-Aktionen des nuget-Paket-Managers festzulegen- [#2705](https://github.com/NuGet/Home/issues/2705)

* die nuget-Konfiguration ist ungültig: vs 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)

* Defaultpushsource in `NuGetDefaults.Config` ( `ProgramData\NuGet` ) funktioniert nicht [#2653](https://github.com/NuGet/Home/issues/2653)

* nuget 3.4.3 Release: der Wert für "Get" darf bei der Paketbuild- [#2648](https://github.com/NuGet/Home/issues/2648) nicht NULL sein

* RESTORE verwendet keine gespeicherten Anmelde Informationen aus Nuget.Config für VSTS-Feeds [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet Restore]: "configfile" ist relativ zu "Project dir" statt "cmd dir- [#2639](https://github.com/NuGet/Home/issues/2639)

* Übermäßige Zuordnungen in Versions Vergleichs Code- [#2632](https://github.com/NuGet/Home/issues/2632)

* Mehrere Instanzen von nuget.exe versuchen, das gleiche Paket parallel zu installieren, verursachen einen doppelten Schreib [#2628](https://github.com/NuGet/Home/issues/2628)

* Abhängigkeitsinformationen werden nicht für Vorgänge mit mehreren Projekten zwischengespeichert- [#2619](https://github.com/NuGet/Home/issues/2619)

* Installieren und Aktualisieren von Download Paketen, ohne den Ordner "Packages" [#2618](https://github.com/NuGet/Home/issues/2618) zuerst zu überprüfen

* Wenn die Paketquellen Liste leer ist, kann die Paketquelle nicht über die Benutzeroberfläche hinzugefügt werden (nuget 3.4. x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Irreführender Fehler beim Versuch, ein Paket zu installieren, das von Entwurfszeit Fassaden abhängt [#2594](https://github.com/NuGet/Home/issues/2594)

* Wenn Sie ein Paket über die packagemanager-Konsole mit der Einstellung "All" installieren, wird nur die erste Quelle [#2557](https://github.com/NuGet/Home/issues/2557) versucht.

* Die neueste Beta Version entzippt modernhttpclient- [#2518](https://github.com/NuGet/Home/issues/2518)

* VS2015 stürzt beim Start mit selbst erstellten nuget 3.4.1- [#2419](https://github.com/NuGet/Home/issues/2419)

* Der Aktualisierungs Befehl kann etwas ausführlicher sein, wenn ich ihn Anfrage...- [#2418](https://github.com/NuGet/Home/issues/2418)

* Die lokal erstellten VSIX-Dateien sollten dieselben DLLs und Dateien wie der CI-Build aufweisen. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Beheben von nuget-Downgrade-Warnungen im Build- [#2396](https://github.com/NuGet/Home/issues/2396)

* Fehler beim Authentifizieren der Paketquelle (dreimal) ist dauerhaft blockiert- [#2362](https://github.com/NuGet/Home/issues/2362)

* Der Paket Inhalt wird bei der Installation eines Pakets aus einem nuget v 3.3 +-Feed mit dem Argument NoCache, wenn das Paketdateien enthält, nicht ordnungsgemäß wieder hergestellt `.nupkg` [#2354](https://github.com/NuGet/Home/issues/2354)

* Nuget-Installation mit allen Paketquellen, aber ein Paket fehlt in 1 Quelle, schlägt fehl [#2322](https://github.com/NuGet/Home/issues/2322)

* [Perfwatson] Uidelay: nuget.packagemanagement.visualstudio.dll! Nuget. packagemanagement. VisualStudio. vsmsbuildnugetprojectsystem + * lt; &gt; c__DisplayClass_0 + &lt; &lt; adressenz &gt; b__ &gt; d. [#2285](https://github.com/NuGet/Home/issues/2285)

* Installations Blöcke, wenn eine einzelne Quelle die Autorisierung nicht besteht- [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec`Versions Bereich sollte-includereferencedprojects Version- [#1983](https://github.com/NuGet/Home/issues/1983) überschreiben

* Update-Package super langsam: "Es wird versucht, Abhängigkeitsinformationen zu erfassen"- [#1909](https://github.com/NuGet/Home/issues/1909)

* Nuget-Paket für das herunter Skalierungen von Batches beim Aktualisieren der Abhängigkeiten von Batch- [#1903](https://github.com/NuGet/Home/issues/1903)

* nuget.exe Update löscht den starken Namen der Assembly und das private-Attribut. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Relativer Dateipfad für "defaultpushsource"- [#1746](https://github.com/NuGet/Home/issues/1746)

* Verbessern von Auflösungs Fehlermeldungen- [#1373](https://github.com/NuGet/Home/issues/1373)

* Update-Package in V3 schlägt fehl, wenn Pakete nicht in der angegebenen Quelle [#1013](https://github.com/NuGet/Home/issues/1013)

* Die Verwendung relativer Pfade für Paketquellen ist problematisch für die Verwendung- [#865](https://github.com/NuGet/Home/issues/865)

* Fehlende Abhängigkeit in der vom Projekt generierten nupkg-Datei, wenn die indirekte Abhängigkeit bereits mit einer niedrigeren Versions Anforderung vorhanden ist [#759](https://github.com/NuGet/Home/issues/759)

* Wenn Sie ein Projekt löschen, wird das zugehörige Benutzeroberflächen Fenster geschlossen, aber beim Umbenennen eines Projekts wird das Benutzeroberflächen Fenster nicht umbenannt Beachten Sie, dass die PMC auf Projekt Umbenennungen und Projekt Entfernungs Ereignisse lauscht [#670](https://github.com/NuGet/Home/issues/670)

* [Willow Web-Arbeitsauslastung] Erstellen von Razor V3-WSP-hängen- [#3241](https://github.com/NuGet/Home/issues/3241)

* Die Installation/Wiederherstellung eines bestimmten Pakets schlägt fehl, wenn "Paket enthält mehrere nuspec-Dateien". - [#3231](https://github.com/NuGet/Home/issues/3231)

* & Szenarios für Kleinbuchstaben `packages.config` - [#3209](https://github.com/NuGet/Home/issues/3209)

* [3,5-Beta2] Bei der Paket Wiederherstellung können "Legacy Pakete" nicht wieder hergestellt werden [#3208](https://github.com/NuGet/Home/issues/3208)

* Das nuget-Paket fügt die TT-Dateien in einem Inhalts Ordner hinzu, unabhängig davon, was [#3203](https://github.com/NuGet/Home/issues/3203)

* Update-Package of ASP.net Web App generiert eine Warnung im Zusammenhang mit der Datei: Quelle- [#3194](https://github.com/NuGet/Home/issues/3194)

* Das nuget-Paket "csproj" (mit `project.json` ) stürzt ab, wenn keine packoptions und Besitzer in der JSON-Datei vorhanden sind [#3180](https://github.com/NuGet/Home/issues/3180)

* Das nuget-Paket für `project.json` ignoriert packoptions-Tags wie Zusammenfassung, Autoren, Besitzer usw.- [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException über nuget. Packaging. physicalpackagefile. GetStream- [#3160](https://github.com/NuGet/Home/issues/3160)

* Das nuget-Paket ignoriert Abhängigkeiten in der Ausgabe `.nuspec` für `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Wenn Sie mehrere Pakete mit Rollback aktualisieren, bleibt das Projekt in einem unterbrochenen Zustand [#3139](https://github.com/NuGet/Home/issues/3139)

* "Contentfiles" unter "Any" wird nicht für netstandard-Projekte hinzugefügt- [#3118](https://github.com/NuGet/Home/issues/3118)

* Die Bibliothek für .NET Standard kann nicht ordnungsgemäß [#3108](https://github.com/NuGet/Home/issues/3108) werden.

* Datei > neues Projekt > Klassenbibliothek (portabel) schlägt in VS2015 und Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* der nuget-Fehler-1.0.0-* ist keine gültige Versions Zeichenfolge [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package kann nicht angezeigt werden, aber Install-Package Works- [#3068](https://github.com/NuGet/Home/issues/3068)

* Fehler bei "Install-package jQuery. Validation" auf dev15- [#3061](https://github.com/NuGet/Home/issues/3061)

* Das nuget-Paket von xproj ist standardmäßig auf einen ungültigen Zielpfad [#3060](https://github.com/NuGet/Home/issues/3060)

* Bei der Installation von vs 2015 Update 3 auf einem vs, der die nuget-Version verwendet 3.5.0 Fehler tritt auf [#3053](https://github.com/NuGet/Home/issues/3053)

* "Blockiert durch packages.config" in `project.json` (UWP, a. k. a Build Integrated) Project- [#3046](https://github.com/NuGet/Home/issues/3046)

* Aktualisieren Sie die dotnet-CLI, die vom Buildskript installiert wurde, auf Preview2-003121, also den offiziellen Preview2-Build. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Benutzeroberfläche des Paket-Managers: zeigt keine neue Version nach dem Aktualisieren eines Pakets an [#3041](https://github.com/NuGet/Home/issues/3041)

* -APIKey in der Befehlszeile "Delete" wird in 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037) nicht gelesen/gesendet

* Falsche Zeichenfolge: ein stabiles Release eines Pakets sollte nicht für eine vorab Abhängigkeit vorhanden sein. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Der optimizedzippackage-Cache verlässt leere Ordner- [#3029](https://github.com/NuGet/Home/issues/3029)

* Beim Erstellen des Projekts PCL ("net46 und Windows 10) wird die Ausnahme NullRef-Ausnahme zurückerhalten. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Das nuget-Update sollte eine informative Nachricht bereitstellen, wenn eine höhere Version durch die Einschränkung der Einschränkung-Version eingeschränkt ist [#3013](https://github.com/NuGet/Home/issues/3013)

* Probleme beim Wiederherstellen von nuget V3- [#2891](https://github.com/NuGet/Home/issues/2891)

* Das Anmelde Informations-Plug-in wurde mit Fehler-1/Fehler beim Herunterladen des Pakets beendet, wenn Anmelde Informationsanbieter mit mehreren Quellen verwendet werden [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json`die nuget [#2817](https://github.com/NuGet/Home/issues/2817) -Wiederherstellung verursacht eine Neukompilierung, wenn nichts geändert wurde

* Symbol Pakete sollten nicht jemals in install-oder Update- [#2807](https://github.com/NuGet/Home/issues/2807) verwendet werden.

* VS unterstützt keine Umgebungsvariablen in repositoryPath (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)

* Bezeichnen Sie die unbezeichneten UIElements in der Benutzeroberfläche des Paket-Managers für Barrierefreiheit- [#2745](https://github.com/NuGet/Home/issues/2745)

* Portable Frameworks mit mittels Bindestrich-Profilen werden abgelehnt. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Der nuget-Paket-Manager sollte deutlich machen, dass die Optionsliste in Paket Details nicht für `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe Push/DELETE verwendet keinen API-Schlüssel [#2627](https://github.com/NuGet/Home/issues/2627)

* Entfernen Sie die gesperrte Eigenschaft aus der Sperrdatei [#2379](https://github.com/NuGet/Home/issues/2379)

* Nuget 3.3.0 Update schlägt mit einer zusätzlichen Einschränkung fehl... der in packages.config definierte Vorgang wird verhindert. - [#1816](https://github.com/NuGet/Home/issues/1816)

* Das Installieren eines Pakets aus einer lokalen Quelle, die nicht vorhanden ist, löst eine falsche Nachricht aus [#1674](https://github.com/NuGet/Home/issues/1674)

* Filter "Upgrade available" zeigt Upgrades an, die gegen die Versions Einschränkung verstoßen- [#1094](https://github.com/NuGet/Home/issues/1094)

* Systemeigene Pakete können nicht aktualisiert werden- [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Features

* Unterstützung beim Festlegen von CopyLocal auf false bei von nuget- [#329](https://github.com/NuGet/Home/issues/329) hinzugefügten verweisen

* nuget.exe-Unterstützung für MSBuild 15- [#1937](https://github.com/NuGet/Home/issues/1937)

* Paket Unterstützung für.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Benutzeraktion deaktivieren, wenn Benutzeraktionen ausgeführt werden [#1440](https://github.com/NuGet/Home/issues/1440)

* Nuget sollte Unterstützung für `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782) hinzufügen

* Hinzufügen von frameworkkompatibilitäten, die in nuget 2. x fehlen (die bereits in 3. x vorhanden sind): [#2720](https://github.com/NuGet/Home/issues/2720)

* Unterstützung für Fall Back Paket Ordner- [#2899](https://github.com/NuGet/Home/issues/2899)

* Entwerfen und implementieren Sie ein Konzept des Pakettyps, um Tool Pakete zu unterstützen- [#2476](https://github.com/NuGet/Home/issues/2476)

* Fügen Sie eine API hinzu, um den Pfad zum Ordner für globale Pakete zu erhalten [#2403](https://github.com/NuGet/Home/issues/2403)

* Semver 2.0.0 in Pack- [#3356](https://github.com/NuGet/Home/issues/3356) aktivieren

## <a name="dcrs"></a>DCRs

* nuget.exe Push-Timeout-Parameter funktioniert nicht [#2785](https://github.com/NuGet/Home/issues/2785)

* Der Paket Beschreibungstext sollte auswählbar sein- [#1769](https://github.com/NuGet/Home/issues/1769)

* Aktivieren Sie nuget.exe, um `.props` -und- `.targets` Dateien für Projekte zu entwickeln `.nuproj` [#2711](https://github.com/NuGet/Home/issues/2711)

* Hinzufügen der Erweiterbarkeits-API zum Vergleichen von Frameworks mit Importen- [#2633](https://github.com/NuGet/Home/issues/2633)

* Abhängigkeits Optionen beim Verwenden von `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486) ausblenden

* Ausgabe nuget.exe Versions Headers in detaillierter Ausgabe [#1887](https://github.com/NuGet/Home/issues/1887)

* Nuget muss den Benutzern mitteilen, dass ein Upgrade/Installation in einer dotnet TFM-basierten PCL Probleme verursachen könnte [#3138](https://github.com/NuGet/Home/issues/3138)

* Warnung bei fehlerhafter Installation/Upgrade für Projekt w/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* Beheben von Leistungsproblemen mit reshaper und nuget für Update- [#3044](https://github.com/NuGet/Home/issues/3044)

* Netcoreapp11-und netstandard17-Unterstützung hinzufügen- [#2998](https://github.com/NuGet/Home/issues/2998)

* Verwenden des ASSEMBLYMETADATA-Attributs für `.nuspec` tokenersetzungen- [#2851](https://github.com/NuGet/Home/issues/2851)
