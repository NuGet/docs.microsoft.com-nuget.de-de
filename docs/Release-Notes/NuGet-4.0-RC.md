---
title: Anmerkungen zu Version 4.0 RC von NuGet | Microsoft-Dokumentation
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/17/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: fa64825d-5908-4abe-9792-d70766d6e2ff
description: "Anmerkungen zu NuGet 4.0 RC, einschließlich bekannter Fehler, Fehlerkorrekturen, hinzugefügter Features und DCRs."
keywords: "Anmerkungen zu NuGet 4.0 RC, Fehlerkorrekturen, bekannte Fehler, hinzugefügte Features, DCRs"
ms.reviewer: kraigb
ms.openlocfilehash: aa1c43be7ac0640bb5e118a162616acb36d44a83
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="40-rc-release-notes"></a>Anmerkungen zu Version 4.0 RC

[Anmerkungen zu Version 3.5 RTM von NuGet](../release-notes/nuget-3.5-RTM.md)

[NuGet 4.0 RC für Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) konzentriert sich auf das Hinzufügen der Unterstützung für .NET Core-Szenarios sowie auf das Behandeln von wichtigem Kundenfeedback und auf das Verbessern der Leistung für zahlreiche Szenarios. Die Verbesserungen in diesem Release betreffen die Unterstützung für PackageReference, NuGet-Befehle als MSBuild-Ziele, die Paketwiederherstellung im Hintergrund und vieles mehr.

## <a name="bug-fixes"></a>Fehlerkorrekturen

* Verhaltensänderungen in `dotnet pack --version-suffix foo` ([#3838](https://github.com/NuGet/Home/issues/3838))

* Das Wiederherstellen von „nuget.exe“ auf einem Computer mit VS „15“ schlägt fehl ([#3834](https://github.com/NuGet/Home/issues/3834))

* „Datei > Neues Projekt“ in .NET Core sollte den Build während der Wiederherstellung blockieren ([#3780](https://github.com/NuGet/Home/issues/3780))

* ASP.NET Core-Apps, die von Visual Studio 2015 zu VS „15“ migriert wurden, können nicht wiederhergestellt werden ([#3773](https://github.com/NuGet/Home/issues/3773))

* [Testfehler] Das Paket „jQuery Validation“ kann über die PM-Benutzeroberfläche nicht deinstalliert werden ([#3755](https://github.com/NuGet/Home/issues/3755))

* Wenn ein Paket für ein UWP-`project.json`-Projekt installiert wird, sollten übergeordnete Projekte ebenfalls wiederhergestellt werden ([#3731](https://github.com/NuGet/Home/issues/3731))

* Ändern der NuGet-Ziele, um die Paketquellen mit hohem statt normalem Ausführlichkeitsgrad zu protokollieren ([#3719](https://github.com/NuGet/Home/issues/3719))

* „dotnet pack3“ sollte standardmäßig eine XML-Dokumentation enthalten ([#3698](https://github.com/NuGet/Home/issues/3698))

* Das Batchupdate über die Benutzeroberfläche schlägt fehl, wenn die Quelle ohne das Paket zuerst aufgeführt und „Alle Quellen“ ausgewählt ist ([#3696](https://github.com/NuGet/Home/issues/3696))

* Der NuGet-Befehl „pack“ schließt nicht alle Dateien ein ([#3678](https://github.com/NuGet/Home/issues/3678))

* OOM-Problem ([#3661](https://github.com/NuGet/Home/issues/3661))

* Der Abschnitt „ProjectFileDependencyGroups“ der Ressourcendatei sollte Bibliotheksnamen für Projekte verwenden ([#3611](https://github.com/NuGet/Home/issues/3611))

* „dotnet restore“ und das Wiederherstellen von Verzeichnissen ([#3517](https://github.com/NuGet/Home/issues/3517))

* Restore3-Fehler werden als Warnungen statt als Fehler protokolliert ([#3503](https://github.com/NuGet/Home/issues/3503))

* TFS-Fehler: „Das Element [Datei] wurde in Ihrem Arbeitsbereich nicht gefunden, oder Sie besitzen keine entsprechende Zugriffsberechtigung.“ ([#2805](https://github.com/NuGet/Home/issues/2805))

* Durch das Eingeben von „nuget <packagename>“ in das Suchfeld des Visual Studio-Schnellstarts wird das Präfix „nuget“ beibehalten ([#2719](https://github.com/NuGet/Home/issues/2719))

* System.Xml.XmlException: Unbekanntes Stammelement im Bereich der Kerneigenschaften. Zeile 2, Position 2 ([#2718](https://github.com/NuGet/Home/issues/2718))

* Die `.nuspec`-Datei mit &lt;- oder &gt;-Escapezeichen in Textfeldern führt keine Builds mehr aus ([#2651](https://github.com/NuGet/Home/issues/2651))

* Beim Löschen von „nuget.exe“ wird nicht zum Eingeben der Anmeldeinformationen aufgefordert (im nicht interaktiven Modus) ([#2626](https://github.com/NuGet/Home/issues/2626))

* Beim Löschen von „nuget.exe“ wird grundlos eine Warnung bezüglich des API-Schlüssels für lokale Quellen ausgegeben ([#2625](https://github.com/NuGet/Home/issues/2625))

* Schlechte Fehlerbehandlung beim Installieren von Entity Framework (Vorabpaket) ([#2566](https://github.com/NuGet/Home/issues/2566))

* Visual Studio stürzt ab, nachdem die Auswahl im Paket-Manager geändert wurde ([#2551](https://github.com/NuGet/Home/issues/2551))

* Die Wiederherstellung von dotnet führt ID-Suchvorgänge in lokalen Repositorys mit flachen Listen durch, bei denen die Groß-/Kleinschreibung berücksichtigt wird, wenn übergreifende Versionen verwendet werden ([#2516](https://github.com/NuGet/Home/issues/2516))

* Die Löschfunktion von „nuget.exe“ funktioniert im V2-Feed nicht ([#2509](https://github.com/NuGet/Home/issues/2509))

* Die Pushbenachrichtigung für ein Timeout von „nuget.exe“ benötigt eine bessere Fehlermeldung ([#2503](https://github.com/NuGet/Home/issues/2503))

* Die Toolwiederherstellung schlägt ohne die richtigen Importe ohne Warnung fehl ([#2462](https://github.com/NuGet/Home/issues/2462))

* NuGet fordert dazu auf, Anmeldeinformationen einzugeben, wenn ein privater Feed vorhanden ist, auch wenn die Installation über nuget.org vorgenommen wird ([#2346](https://github.com/NuGet/Home/issues/2346))

* Das Paket „ApplicationInsights 2.0“ wird aufgeführt, ist aber noch nicht vorhanden ([#2317](https://github.com/NuGet/Home/issues/2317))

* UIDelay in VS „15“ (Branch für Vorschauversion 5) ([#3500](https://github.com/NuGet/Home/issues/3500))

* Das erste OnBuild-Ereignis für die Wiederherstellung fehlt während des Builds für UWP ([#3489](https://github.com/NuGet/Home/issues/3489))

* PowerShell 5 beschädigt die Installation von Entity Framework? ([#3312](https://github.com/NuGet/Home/issues/3312))

* Quelle zur ausführlichen Protokollierung hinzufügen (für 3.5 berücksichtigen) ([#3294](https://github.com/NuGet/Home/issues/3294))

* Der NoCache-Parameter wird in Version 3.4 und höher des NuGet-Clients nicht berücksichtigt ([#3074](https://github.com/NuGet/Home/issues/3074))

* Wenn ein Anbieter für Anmeldeinformationen in Visual Studio nicht geladen werden kann, soll NuGet nicht unterbrochen werden ([#2422](https://github.com/NuGet/Home/issues/2422))


## <a name="features"></a>Features

* CI einrichten, um x86 auszuführen ([#3868](https://github.com/NuGet/Home/issues/3868))

* Automatische Wiederherstellung 3/3: nicht blockierende Benutzeroberfläche ([#3658](https://github.com/NuGet/Home/issues/3658))

* Automatische Wiederherstellung 2/3: Hintergrundwiederherstellung auf Nominierung ([#3657](https://github.com/NuGet/Home/issues/3657))

* Projektverweise wiederherstellen, um dem Buildverhalten zu entsprechen (Rekursion) ([#3615](https://github.com/NuGet/Home/issues/3615))

* DPL-Unterstützung in VS „15“ (minbar) ([#3614](https://github.com/NuGet/Home/issues/3614))

* Einstellungsdatei in Programme verschieben ([#3613](https://github.com/NuGet/Home/issues/3613))

* Generierte Wiederherstellungseigenschaften und -ziele benötigen zielübergreifende Unterstützung bei der Beteiligung ([#3496](https://github.com/NuGet/Home/issues/3496))

* NuGet-Unterstützung für die Wiederherstellung für PackageTargetFallback (zuvor: Imports) ([#3494](https://github.com/NuGet/Home/issues/3494))

* Implementierung von ToolsRef ([#3472](https://github.com/NuGet/Home/issues/3472))

* Restore3 für eine RID ([#3465](https://github.com/NuGet/Home/issues/3465))

* Die NuGet-Benutzeroberfläche sollte das Hinzufügen/Entfernen/Aktualisieren von PackageRefs ermöglichen ([#3457](https://github.com/NuGet/Home/issues/3457))

* Automatische Wiederherstellung 1/3: Implementieren der Nominierungs-API über das Zwischenspeichern der Wiederherstellungsinformationen des Projekts ([#3456](https://github.com/NuGet/Home/issues/3456))

* [0] NuGet-Wiederherstellungsaufgaben und -ziele ([#2994](https://github.com/NuGet/Home/issues/2994))

* [1] Aktivieren der Wiederherstellung auf Projektmappenebene in MSBuild ([#2993](https://github.com/NuGet/Home/issues/2993))

* Unterstützung der öffentlichen Erweiterbarkeit des Anbieters für Anmeldeinformationen in Visual Studio ([#2909](https://github.com/NuGet/Home/issues/2909))

* Rekursive NuGet-Wiederherstellung ([#2533](https://github.com/NuGet/Home/issues/2533))

* Microsoft.TeamFoundation.Client kann auf dev15 nicht geladen werden, die Version von Microsoft.TeamFoundation.Client muss für VS „15“ (Vorschauversion) auf 15.0 aktualisiert werden ([#2392](https://github.com/NuGet/Home/issues/2392))

* Das C++-Paket für das UWP-C++-Projekt in VS „15“ (Vorschauversion) kann nicht installiert werden ([#2369](https://github.com/NuGet/Home/issues/2369))

* Die NUPKG-Datei muss den Ordner „\buildCrossTargeting\“ unterstützen und `.targets` / `.props` für den zielübergreifenden MSBuild-Bereich importieren ([#3499](https://github.com/NuGet/Home/issues/3499))

* Entwurf von ToolsReference ([#3462](https://github.com/NuGet/Home/issues/3462))

* Korrigieren der NuGet-Benutzeroberfläche, um die Wiederherstellung von w/ PackageReferences in `.csproj` zu unterstützen ([#3455](https://github.com/NuGet/Home/issues/3455))

* Hinzufügen der Schaltfläche „Cache löschen“ zu den Einstellungen des Paket-Managers von Visual Studio ([#3289](https://github.com/NuGet/Home/issues/3289))

## <a name="dcrs"></a>DCRs

* Die Wiederherstellung von Projektmappen sollte während der automatischen Wiederherstellung blockiert werden ([#3797](https://github.com/NuGet/Home/issues/3797))

* Die Installation von .NET Core über die Benutzeroberfläche des NuGet-Paket-Managers wird für jeden TFM statt nur für diejenigen durchgeführt, die vom Paket unterstützt werden ([#3721](https://github.com/NuGet/Home/issues/3721))

* Die Wiederherstellung der Nominierungs-API muss ebenfalls DotNetCliToolsReferences unterstützen ([#3702](https://github.com/NuGet/Home/issues/3702))

* VSIX (VS „15“) als Systemkomponente markieren ([#3700](https://github.com/NuGet/Home/issues/3700))

* Vom Verweis auf MS.VS.Services.Client zu MS.VS.Services.Client.Interactive migrieren ([#3670](https://github.com/NuGet/Home/issues/3670))

* $(RestoreLegacyPackagesDirectory) sollte von der Wiederherstellung als Projektebene berücksichtigt werden ([#3618](https://github.com/NuGet/Home/issues/3618))

* Die Wiederherstellung des Projekts mit einem einzelnen Zielframework sollte keine Eigenschaften erfordern ([#3588](https://github.com/NuGet/Home/issues/3588))

* Der Befehl „dotnet restore3 foo.csproj“ sollte wie bei „dotnet build“ den Abhängigkeiten der Projektverweise folgen und diese ebenfalls wiederherstellen ([#3577](https://github.com/NuGet/Home/issues/3577))

* "type": "platform": Abhängigkeiten werden als "type":"package" in der Sperrdatei dargestellt ([#2695](https://github.com/NuGet/Home/issues/2695))

* Der ausführliche Modus von „nuget.exe“ sollte die URL für den Download anzeigen ([#2629](https://github.com/NuGet/Home/issues/2629))

* Verschieben von NuGet.Xplat zu Microsoft.NetCore.App und netcoreapp1.0 ([#2483](https://github.com/NuGet/Home/issues/2483))

* Push: Es sollte möglich sein, den Symbolserver zu überschreiben, wenn etwas über mithilfe von Push über die Befehlszeile übertragen wird ([#2348](https://github.com/NuGet/Home/issues/2348))

* Konsolidieren von Code für das Suchen von globalen Paketpfaden ([#2296](https://github.com/NuGet/Home/issues/2296))

* Ein besserer Name als „suppressParent“ ist erforderlich ([#2196](https://github.com/NuGet/Home/issues/2196))

* Bestimmen des Abhängigkeitsnamens von `project.json`, der für MSBuild-Projekte verwendet werden soll ([#1914](https://github.com/NuGet/Home/issues/1914))

* Unterstützung für SemVer 2.0.0 zu NuGet.Core hinzufügen ([#3383](https://github.com/NuGet/Home/issues/3383))

* Transitive Abhängigkeiten von NUPKG-Dateien mit `.targets`-Dateien in MSBuild zulassen ([#3342](https://github.com/NuGet/Home/issues/3342))

* Der NuGet-Befehl „restore“ ist über die Befehlszeile wesentlich langsamer als in Visual Studio ([#3330](https://github.com/NuGet/Home/issues/3330))

* Beim Vergleich von Paket-ID und Version sollte die Groß-/Kleinschreibung nicht berücksichtigt werden ([#2522](https://github.com/NuGet/Home/issues/2522))

* Die Option „NoCache“ funktioniert nicht für auf `packages.config` basierende Wiederherstellungen und Installation (GlobalPackagesFolder) ([#1406](https://github.com/NuGet/Home/issues/1406))

* Die Ressourcen „FindPackageByIdResource“ benötigen einen Standardkontext und eine Protokollierung für den Cache ([#1357](https://github.com/NuGet/Home/issues/1357))
