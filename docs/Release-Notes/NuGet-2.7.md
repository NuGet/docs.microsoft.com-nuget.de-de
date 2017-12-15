---
title: Anmerkungen zur Version des NuGet-2.7 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba2edaad-4795-47a0-a572-d0e1716bd540
description: "Versionshinweise für NuGet 2.7 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-2.7 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 502cb5e68f905e9ad8f4003bb0690d3e676f6bb7
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-27-release-notes"></a>NuGet-Version 2.7 Hinweise

[NuGet 2.6.1 Anmerkungen zu dieser Version von WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1-Versionshinweise](../release-notes/nuget-2.7.1.md)

NuGet-2.7 wurde 22 August 2013 freigegeben.

## <a name="acknowledgements"></a>Bestätigungen

Wir möchten, vielen Dank, dass die folgenden externen Contributors für ihre bedeutende Beiträge zum NuGet 2.7:

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Zeigen Sie Lizenz-Url beim Auflisten von Paketen und Ausführlichkeit detailliert erläutert wird.
1. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -attributhinzufügen DevelopmentDependency auf `packages.config` und zum im Befehl Pack nur Runtime Pakete enthalten
1. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Vermeiden Sie die doppelten Schlüssel von Eigenschaften in nuget.exe-Pack-Befehl.
1. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -Cachegröße auf 200 Computer erweitern.
1. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -beheben NuGet-Dialogfeld auf der Registerkarte "falsch" anzeigen
    - Korrektur Project.TargetFramework kann in Projektmanager null sein.
    - [#3248](http://nuget.codeplex.com/workitem/3248) -beheben SharedPackageRepository FindPackage/FindPackagesById auf nicht existierende PackageId fehl
1. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -Unterstützung für Nomad Projekt aktivieren
1. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -Fix Push-Befehl schlägt fehl mit Exitcode 0 code, wenn die Datei nicht vorhanden ist.
1. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -Update ein Problem mit Add BindingRedirect-Befehl, wenn ein Projekt auf ein Datenbankprojekt verweist.
1. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -Fix-Fehler des nuget.pack analysieren Sie Platzhalter im Attribut "Exclude" nicht ordnungsgemäß.
1. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
    - [#3307](http://nuget.codeplex.com/workitem/3307) -Fix-Bug `NuGet.targets` übergibt keine $(Platform) an nuget.exe beim Wiederherstellen von Paketen.
1. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
    - [#3294](http://nuget.codeplex.com/workitem/3294) -Fix Fehler im nuget.exe Paket Befehl das Hinzufügen von Dateien mit demselben Namen, aber unterschiedliche Groß-/Kleinschreibung, schließlich "Element ist bereits vorhanden" Ausnahme verursacht zulassen würde.
1. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
    - [#2990](http://nuget.codeplex.com/workitem/2990) -Version hinzufügen Eigenschaft NetPortableProfile-Klasse.
1. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
    - [#3460](https://nuget.codeplex.com/workitem/3460) -NullReferenceException-Fehler zu beheben, wenn RequireApiKey = "true", aber der Header "X-NUGET-apikey" nicht vorhanden ist.
1. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
    - [#3278](https://nuget.codeplex.com/workitem/3278) -behebt NuGet.Build Ziele Datei an, damit er auf MonoDevelop richtig funktioniert
1. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
    - Verbessern Sie Restore-Befehl-Leistung, indem die Parallelisierung zu erhöhen

## <a name="notable-features-in-the-release"></a>Wichtige Funktionen in der Version

### <a name="package-restore-by-default-with-implicit-consent"></a>Die Paketwiederherstellung wird standardmäßig (mit impliziten Zustimmung)

NuGet 2.7 verfolgt einen neuen Ansatz zum Packen von Restore und überwunden werden auch eine Hürde: Paket Wiederherstellung Zustimmung ist jetzt standardmäßig aktiviert. Die Kombination der neuen Ansatz und die impliziten Zustimmung wird Paket Wiederherstellungsszenarien erheblich vereinfachen.

#### <a name="implicit-consent"></a>Impliziten Zustimmung

Erstellen mit NuGet-Versionen 2.0, 2.1, 2.2, 2.5 und 2.6 ist erforderlich, um explizit zulassen, NuGet das Herunterladen fehlender Pakete während der Benutzer ein. Wäre diese Zustimmung nicht wurde explizit angegeben, dann würde Lösungen, die paketwiederherstellung aktiviert haben nicht erstellt werden, bis der Benutzer die Zustimmung erteilt wurde.

Beginnend mit NuGet 2.7, Paket Wiederherstellung Zustimmung ist standardmäßig während Benutzer explizit *Abmelden* der paketwiederherstellung bei Bedarf das Kontrollkästchen in der NuGet Einstellungen in Visual Studio verwenden können. Diese Änderung für impliziten Zustimmung betrifft NuGet in den folgenden Umgebungen:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* NuGet.exe Befehlszeilen-Hilfsprogramm

#### <a name="automatic-package-restore-in-visual-studio"></a>Automatische Paketwiederherstellung in Visual Studio

Beginnend mit NuGet 2.7, wird NuGet automatisch herunterladen fehlender Pakete während des Builds in Visual Studio, selbst wenn die paketwiederherstellung für die Projektmappe explizit aktiviert wurde noch nicht. Diese automatische Paketwiederherstellung erfolgt in Visual Studio, wenn Sie ein Projekt oder die Projektmappe erstellen, aber bevor MSBuild aufgerufen wird. Dies löst einige bedeutende Vorteile:

1. Keine weiteren müssen Sie die Aktion "Aktivieren der NuGet-Paketwiederherstellung" in der Projektmappe verwenden
1. Projekte, die nicht geändert werden müssen wird nicht, und NuGet zu Ihrem Projekt, um sicherzustellen, dass die paketwiederherstellung aktiviert ist
1. Alle NuGet-Pakete, einschließlich derer, die MSBuild-Importe für Props/Targets-Dateien enthalten werden wiederhergestellt *vor* MSBuild aufgerufen, sicherstellen Props/Ziele werden während des Erstellungsvorgangs ordnungsgemäß erkannt

Um die automatische Paketwiederherstellung in Visual Studio verwenden, müssen Sie nur einen (in) Aktion ausführen:

1. Aktivieren Sie nicht Ihrem `packages` Ordner

Es gibt mehrere Möglichkeiten, lassen Sie Ihre `packages` Ordner aus der quellcodeverwaltung. Weitere Informationen finden Sie unter der [Paketen und Datenquellen-Steuerelements](../consume-packages/packages-and-source-control.md) Thema.

Alle Benutzer implizit sind teilgenommen Zustimmung automatische Paketwiederherstellung haben, können problemlos ausgeschlossen über die Paket-Manager-Einstellungen in Visual Studio.

![Paket-Manager-Einstellungen](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Vereinfachte Paketwiederherstellung über die Befehlszeile

NuGet-2.7 führt ein neues Feature für nuget.exe:`nuget.exe restore`

Diese neue Restore-Befehl können Sie alle Pakete für eine Projektmappe mit einem einzigen Befehl problemlos wiederherstellen, indem eine Projektmappendatei oder einen Ordner als Argument akzeptiert. Darüber hinaus wird dieses Argument impliziert, wenn im aktuellen Ordner nur eine einzige Lösung besteht. Das bedeutet, dass alle folgenden aus einem Ordner geeignet sein, die eine einzelne Projektmappendatei (MySolution.sln) enthält:

1. NuGet.exe Wiederherstellung MySolution.sln
1. NuGet.exe wiederherstellen.
1. NuGet.exe wiederherstellen

Der Restore-Befehl wird die Projektmappendatei öffnen, und suchen alle Projekte innerhalb der Projektmappe. Dort finden sie die `packages.config` für die einzelnen Projekte und Wiederherstellen aller Pakete gefunden. Auch wird wiederhergestellt, Lösung auf Dokumentebene-Paketen, die aus der `.nuget\packages.config` Datei. Weitere Informationen zu den neuen Restore-Befehl finden Sie der [Command-Line Reference](../tools/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Neue Paket Restore-Workflow

Wir freuen zu diesen Änderungen Paket wiederhergestellt, da es sich um einen neuen Workflow führt. Wenn Sie die Pakete aus quellcodeverwaltung ausschließen möchten Sie einfach nicht ein commit für die `packages` Ordner. Visual Studio-Benutzer, die zu öffnen und erstellen Sie die Projektmappe sehen die Pakete, die automatisch wiederhergestellt. Rufen Sie einfach für Befehlszeilenbuilds `nuget.exe restore` vor dem Aufrufen `msbuild`. Sie müssen nicht mehr zu merken sind, verwenden Sie die Aktion "Aktivieren der NuGet-Paketwiederherstellung" in der Projektmappe, und benötigen wir nicht mehr so ändern Sie Ihre Projekte aus, um den Build zu ändern. Und dies auch viel benutzerfreundlicheres MSBuild Importe, insbesondere für Importe, die über die aktuelle NuGet-Funktion für hinzugefügt enthaltenen Pakete ergibt [automatisch zu importieren Props/Ziele Dateien](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) aus dem Ordner \build.

Zusätzlich zu den Arbeitsaufgabentypen, den wir uns das Tool installiert haben, arbeiten wir auch mit einigen wichtigen Partnern für dieses neue Konzept gerundet. Wir haben Sie konkrete Zeitachsen für diese noch kein, aber jeder Partner wird als begeistert, da wir über die neuen Ansatz sind.

* Team Foundation Service - deren ordnungsgemäße zum Integrieren des Aufrufs von `nuget.exe restore` an den standardmäßigen Szenarien zu erstellen.
* Windows Azure Websites - deren ordnungsgemäße Weise können Sie das push von Ihrem Projekts in Azure und `nuget.exe restore` aufgerufen wird, bevor die Website erstellt wird.
* TeamCity - sie ihre NuGet-Installer-Plug-In für TeamCity aktualisieren 8.x
* AppHarbor - deren ordnungsgemäße Weise können Sie das push von Ihrem Repository an AppHarbor und `nuget.exe restore` aufgerufen, damit die Projektmappe erstellen.

Mit jeder der oben aufgeführten Partner würden sie jeweils eine eigenen Kopie nuget.exe verwenden und müssen Sie nicht in der Projektmappe nuget.exe ausführen.

#### <a name="known-issues"></a>Bekannte Probleme

Gab es zwei bekannte Probleme mit nuget.exe Restore mit der ersten Version 2.7, aber sie wurden behoben auf 9/6/2013 mit Update für die [NuGet.CommandLine Paket](http://www.nuget.org/packages/NuGet.CommandLine/).  Dieses Update kann auch auf die [NuGet 2.7 Downloadseite](https://nuget.codeplex.com/releases/view/107605) auf CodePlex.  Ausführen `nuget.exe update -self` auf die neueste Version aktualisiert.

Die festen wurden:

1. [Neue paketwiederherstellung funktioniert auf Mono nicht bei Verwendung der SLN-Datei](https://nuget.codeplex.com/workitem/3596)
1. [Neue paketwiederherstellung funktioniert nicht mit Wix-Projekte](https://nuget.codeplex.com/workitem/3598)

Es gibt auch ein bekanntes Problem mit dem neuen Paket Wiederherstellung Workflow bei dem [automatische Paketwiederherstellung funktioniert nicht für Projekte unter einem Projektmappenordner](https://nuget.codeplex.com/workitem/3625). Dieses Problem wurde in NuGet 2.7.1 behoben.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Erstellen von Projekt einer neuen Zielversion und Upgrade Fehler-, Warn-

Häufig Suchen nach einer neuen Zielversion oder aktualisieren das Projekt, Sie, dass einige NuGet-Pakete werden nicht einwandfrei. Leider gibt es keinen Hinweis Dieses und dann es gibt keine allgemeinen Vorgaben zum behoben werden. Mit NuGet 2.7 verwenden wir jetzt einige Visual Studio-Ereignisse um zu erkennen, wenn Sie als Zielversion neu zugewiesen oder aktualisiert das Projekt in einer Weise, die Ihre installierten NuGet-Pakete wirkt sich auf haben.

Wenn festgestellt wird, dass keines der Pakete von einer neuen Zielversion oder Aktualisierung des betroffen sind, müssen wir sofortige Buildfehler, um Sie zu informieren erzeugen. Zusätzlich zu den unmittelbaren Buildfehler wir auch beibehalten einer `requireReinstallation="true"` -flag in Ihrer `packages.config` Datei für alle Pakete, die von der neuzuweisungen betroffen, und jeder nachfolgende Waren in Visual Studio erstellen löst Buildwarnungen für diese Pakete.

Obwohl NuGet keine automatische Maßnahmen kann betroffene Pakete neu zu installieren, wir hoffen, diese Angabe dass und Warnung Hilfe führt können Sie ermitteln, wenn Sie Pakete installieren müssen. Wir sind auch die Arbeit [Paket Neuinstallation Prozessleitfaden-Dokumentation](../consume-packages/reinstalling-and-updating-packages.md) , dass diese Fehlermeldungen, die Sie verweisen.

### <a name="nuget-configuration-defaults"></a>Standardwerte für die Konfiguration von NuGet

Viele Unternehmen haben eine feste Zeit abgleichsarbeit Entwickler Verwendung interner Paketquellen statt nuget.org hatten jedoch mithilfe von NuGet intern sind. NuGet-2.7 führt eine Konfiguration standardmäßig-Funktion, die computerweite Standardwerte für angegeben werden kann:

1. Aktivierten Paketquellen überein
1. Registriert, jedoch deaktiviert Paketquellen
1. Die Standardeinstellung nuget.exe Push-Quelle

Jede dieser Optionen kann jetzt in einer Datei am konfiguriert `%ProgramData%\NuGet\NuGetDefaults.Config`. Wenn diese Konfigurationsdatei Paketquellen überein gibt, und klicken Sie dann die Paketquelle an Standardeinstellung nuget.org nicht automatisch registriert werden wird und den Werten in `NuGetDefaults.Config` stattdessen registriert wird.

Zwar nicht erforderlich, um dieses Feature zu verwenden, erwarten wir Unternehmen bereitzustellende `NuGetDefaults.Config` Dateien mithilfe von Gruppenrichtlinien.

*Beachten Sie, dass diese Funktion nie eine Paketquelle aus eines Entwicklers NuGet-Einstellungen zu entfernenden verursacht. Bedeutet, dass der Entwickler NuGet wird bereits verwendet und daher hat die Paketquelle nuget.org registriert, es wird nicht entfernt werden nach der Erstellung einer `NuGetDefaults.Config` Datei.*

Finden Sie unter [NuGet-Standardeinstellungen für die Konfiguration](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) für Weitere Informationen zu dieser Funktion.

### <a name="renaming-the-default-package-source"></a>Die Paketquelle an Standardeinstellung umbenennen

NuGet ist immer eine Standard-Paketquelle namens "NuGet-offizielle Paketquelle", die auf nuget.org verweist registriert. Dieses Namens wurde ausführliche und auch nicht angeben, der tatsächlich verweist. Um diese beiden Probleme zu beheben, haben wir diese Paketquelle, um einfach "nuget.org" in der Benutzeroberfläche umbenannt. Die URL für die Paketquelle wurde ebenfalls geändert, um den "Www" enthalten Gruppenpräfix („group.“) zusammensetzt. Nachdem Sie mit NuGet 2.7, wird Ihre vorhandenen "NuGet-offizielle Paketquelle" automatisch "nuget.org" als Namen und "https://www.nuget.org/api/v2/" der URL aktualisiert werden.

### <a name="performance-improvements"></a>Leistungsverbesserungen

Wir haben einige leistungsverbesserungen vorgenommen, in 2.7, die weniger Speicher beansprucht, weniger Datenträgerverwendung und schnellere Paketinstallation zurückgibt. Wir haben auch intelligentere Abfragen OData-Feeds an die gesamte Nutzlast zu reduzieren, vorgenommen.

### <a name="new-extensibility-apis"></a>Neue Erweiterbarkeit-APIs

Wir haben unsere Dienste Erweiterbarkeit, um die Lücke der fehlenden Funktionen in früheren Versionen einige neue APIs hinzugefügt.

#### <a name="ivspackageinstallerservices"></a>IVsPackageInstallerServices

    ```cs
    // Checks if a NuGet package with the specified Id and version is installed in the specified project.
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    // Get the list of NuGet packages installed in the specified project.
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
    ```

#### <a name="ivspackageinstaller"></a>IVsPackageInstaller

    ```cs
    // Installs one or more packages that exist on disk in a folder defined in the registry.
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    // Installs one or more packages that are embedded in a Visual Studio Extension Package.
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);
    ```

### <a name="development-only-dependencies"></a>Reine Abhängigkeiten

Diese Funktion wurde durch beigetragen [Adam Ralph](https://twitter.com/adamralph) Hilfeartikeln Paketersteller zu deklarieren, Abhängigkeiten, die nur bei der Entwicklung verwendet wurden, Uhrzeit und paketabhängigkeiten erfordern. Durch Hinzufügen einer `developmentDependency="true"` -Attribut auf ein Paket in `packages.config`, `nuget.exe pack` wird das Paket als Abhängigkeit nicht mehr enthalten.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Entfernt die Unterstützung für Visual Studio 2010 Express für Windows Phone

Das neue Paket-Restore-Modell in 2.7 ist durch ein neues VSPackage implementiert, die aus dem Haupt-NuGet-VSPackage unterscheidet. Aufgrund eines technischen Problems dieses neue VSPackage funktioniert nicht ordnungsgemäß in der *Visual Studio 2010 Express für Windows Phone* SKU wie wir die gleiche Codebasis mit anderen Teilen SKUs von Visual Studio unterstützt. Aus diesem Grund ab NuGet 2.7, wir werden löschen Unterstützung für *Visual Studio 2010 Express für Windows Phone* veröffentlichte Erweiterung. Unterstützung für *zuerst Visual Studio 2010 Express für Web* ist immer noch in der primären Erweiterung in der Visual Studio-Erweiterung Gallery veröffentlicht enthalten.

Da wir nicht sicher sind, wie viele Entwickler weiterhin NuGet in dieser Version/Edition von Visual Studio verwenden, wir veröffentlichen eine separate Visual Studio-Erweiterung speziell für diese Benutzer und veröffentlichen es auf CodePlex (anstelle der Visual Studio-Erweiterung Gallery) . Wir planen nicht, um den Vorgang fortzusetzen, verwalten Sie diese Erweiterung, aber wenn dies Sie betrifft informieren Sie uns durch ein Problem auf CodePlex ablegen.

Um den NuGet-Paket-Manager (für Visual Studio 2010 Express für Windows Phone) herunterzuladen, besuchen Sie die [NuGet 2.7 Downloads](https://nuget.codeplex.com/releases/view/107605) Seite.

### <a name="bug-fixes"></a>Fehlerkorrekturen

Zusätzlich zu diesen Features enthält diese Version von NuGet auch zahlreiche Programmfehlerbehebungen. Es gab 97 insgesamt Probleme, die in der Version behoben. Eine vollständige Liste der Arbeit Elemente eine feste NuGet 2.7 Bitte Ansicht der [NuGet Issue Tracker für diese Version](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
