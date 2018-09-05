---
title: Anmerkungen zu NuGet 2.7
description: Anmerkungen zu NuGet 2.7, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 97d3e5f0238fd6947a54e5eb3229b89b6746f18c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550964"
---
# <a name="nuget-27-release-notes"></a>Anmerkungen zu NuGet 2.7

[NuGet 2.6.1 für WebMatrix – Anmerkungen zu dieser](../release-notes/nuget-2.6.1-for-webmatrix.md) | [Anmerkungen zu NuGet 2.7.1](../release-notes/nuget-2.7.1.md)

NuGet 2.7 wurde 22 August 2013 veröffentlicht.

## <a name="acknowledgements"></a>Bestätigungen

Wir würden gerne, vielen Dank, dass die folgenden externen Mitwirkenden für ihre wichtige Beiträge zu NuGet 2.7:

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Zeigen Sie Lizenz-Url beim Auflisten von Paketen und Ausführlichkeit ausführlich beschrieben wird.
2. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -Attribut DevelopmentDependency hinzufügen `packages.config` und verwenden in den Befehl "Pack" nur die Runtime-Pakete einschließen
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Vermeiden Sie die doppelten Schlüssel von Eigenschaften in nuget.exe-Befehl "Pack".
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -Cache-Größe auf 200 Computer zu erhöhen.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -Beheben von NuGet-Dialogfeld anzeigen in der Registerkarte "falsch"
    - Korrektur Project.TargetFramework kann in der Projektmanager null sein.
    - [#3248](http://nuget.codeplex.com/workitem/3248) -beheben SharedPackageRepository FindPackage/FindPackagesById schlägt eine nicht existierende PackageId
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -Unterstützung für Nomad Projekt aktivieren
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -Fix Push-Befehl schlägt fehl mit Exitcode 0 code, wenn die Datei nicht vorhanden ist.
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -Fix-Bug mit BindingRedirect-Add-Befehl, wenn ein Projekt ein Datenbankprojekt.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -Fix-Bug von nuget.pack Platzhalter im Attribut "Exclude" nicht ordnungsgemäß analysiert.
10. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) -Fix Bug `NuGet.targets` leitet nicht $(Platform) an nuget.exe beim Wiederherstellen von Paketen.
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -Fix-Bug in nuget.exe-Paket-Befehl ermöglicht das Hinzufügen von Dateien mit demselben Namen, aber unterschiedlicher Groß-/Kleinschreibung, schließlich "Element ist bereits vorhanden" Ausnahme verursacht.
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) -Versionseigenschaft NetPortableProfile-Klasse hinzufügen.
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -Bug "NullReferenceException" behoben, wenn RequireApiKey = "true", aber der Header "X-NUGET-apikey" nicht vorhanden ist.
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) -behebt NuGet.Build Ziele, damit sie ordnungsgemäß funktioniert haben, an MonoDevelop Datei
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - Verbessern Sie Restore-Befehl-Leistung, indem Sie die Parallelisierung zu erhöhen

## <a name="notable-features-in-the-release"></a>Wichtige Features in der Version

### <a name="package-restore-by-default-with-implicit-consent"></a>Wiederherstellen von Paketen, die standardmäßig (mit impliziten Zustimmung)

NuGet 2.7 führt einen neuen Ansatz zum Packen der Wiederherstellung ein, und löst auch eine Wichtige Hürde: Package Restore Zustimmung ist jetzt standardmäßig aktiviert. Die Kombination der neue Ansatz und die impliziten Zustimmung wird Wiederherstellungsszenarien Paket erheblich vereinfacht werden.

#### <a name="implicit-consent"></a>Impliziten Zustimmung

Erstellen mit NuGet-Versionen 2.0, 2.1, 2.2, 2.5 und 2.6 Benutzer erforderlich, um NuGet das Herunterladen fehlender Pakete während der explizit gewähren. Hätte diese Zustimmung nicht wurde explizit angegeben, und klicken Sie dann Lösungen, die paketwiederherstellung aktiviert haben würde nicht erstellt werden, bis der Benutzer seine Zustimmung erteilt haben.

Ab NuGet 2.7, Package Restore Zustimmung ist standardmäßig während Benutzer explizit *kündigen* der paketwiederherstellung ggf. das Kontrollkästchen in NuGets-Einstellungen in Visual Studio verwenden. Diese Änderung zur impliziten Zustimmung betrifft NuGet in den folgenden Umgebungen:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* NuGet.exe-Befehlszeilen-Hilfsprogramm

#### <a name="automatic-package-restore-in-visual-studio"></a>Automatische Paketwiederherstellung in Visual Studio

Ab NuGet 2.7, lädt NuGet automatisch fehlende Pakete während des Buildvorgangs in Visual Studio herunter, auch wenn die paketwiederherstellung für die Projektmappe explizit aktiviert wurde noch nicht. Diese automatische Paketwiederherstellung tritt in Visual Studio beim Erstellen eines Projekts oder die Projektmappe, jedoch bevor MSBuild aufgerufen wird. Dies führt einige wichtige Vorteile:

1. Keine weiteren müssen Sie die Geste "NuGet-Paketwiederherstellung aktivieren" in Ihrer Lösung verwenden
1. Projekte nicht geändert werden müssen, und NuGet wird nicht nehmen Sie Änderungen an Ihrem Projekt aus, um sicherzustellen, dass die paketwiederherstellung aktiviert ist
1. Alle NuGet-Pakete, einschließlich derjenigen, die MSBuild-Importe für Eigenschaften/Ziele Dateien enthalten werden wiederhergestellt, *vor* MSBuild aufgerufen, um sicherzustellen, die Eigenschaften/Ziele ordnungsgemäß während des Buildvorgangs erkannt

Um die automatische Paketwiederherstellung in Visual Studio verwenden, müssen Sie nur eine (Aktion in) ausführen:

1. Überprüfen Sie die nicht Ihrem `packages` Ordner

Es gibt mehrere Möglichkeiten, lassen Sie Ihre `packages` Ordner aus der quellcodeverwaltung. Weitere Informationen finden Sie unter den [Pakete und Quellcodeverwaltung](../consume-packages/packages-and-source-control.md) Thema.

Alle Benutzer zwar implizit automatische Paketwiederherstellung Zustimmung festgelegt, Sie können problemlos die Deaktivierung über die Paket-Manager-Einstellungen in Visual Studio.

![Paket-Manager-Einstellungen](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Vereinfachte Paketwiederherstellung über die Befehlszeile

NuGet 2.7 wird ein neues Feature für nuget.exe eingeführt: `nuget.exe restore`

Dieser neue Restore-Befehl können Sie alle Pakete für eine Lösung mit einem einzigen Befehl problemlos wiederherstellen, indem akzeptiert eine Projektmappendatei oder einen Ordner als Argument. Darüber hinaus wird dieses Argument impliziert, wenn nur eine einzige Lösung in den aktuellen Ordner vorhanden ist. Das bedeutet, dass alle folgenden aus einem Ordner arbeiten, die eine einzelne Projektmappe (MySolution.sln) enthalten:

1. NuGet.exe-Wiederherstellung MySolution.sln
1. NuGet.exe-Wiederherstellung.
1. NuGet.exe-Wiederherstellung

Restore-Befehl öffnet die Projektmappendatei und alle Projekte in der Projektmappe suchen. Dort finden sie die `packages.config` für die einzelnen Projekte und Wiederherstellen aller Pakete gefunden. Auch auf Projektmappenebene Paketen im wiederhergestellt, die `.nuget\packages.config` Datei. Weitere Informationen zu den neuen Befehl für die Wiederherstellung befinden sich die [Command-Line Reference](../tools/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Neue Paket-Workflow-Wiederherstellung

Wir freuen zu diesen Änderungen, die Paketwiederherstellung, wie sie einen neuen Workflow führt. Wenn Sie die Pakete aus der quellcodeverwaltung ausschließen möchten Sie einfach nicht bestätigen die `packages` Ordner. Visual Studio-Benutzer, die zu öffnen und erstellen Sie die Projektmappe sehen die Pakete automatisch wiederhergestellt. Rufen Sie einfach für Befehlszeilenbuilds `nuget.exe restore` vor dem Aufrufen `msbuild`. Sie nicht mehr benötigen, denken Sie daran, die Geste "NuGet-Paketwiederherstellung aktivieren" in Ihrer Lösung zu verwenden, und wir müssen nicht mehr so ändern Sie Ihre Projekte, um den Build zu ändern. Und dies führt auch eine bessere Erfahrung für Pakete, die MSBuild-Importe, insbesondere für Importe, die über NuGets-neues Feature für hinzugefügt enthalten [Eigenschaften/Ziele automatisch importieren von Dateien](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) aus dem Ordner \build.

Zusätzlich zu den Arbeitselementtypen, die, den wir selbst ausgeführt haben, arbeiten wir auch mit einigen wichtigen Partnern zu diesem neuen Ansatz. Noch keine Starttermine konkrete für diese noch, aber jeder Partner wird ebenso begeistert wie wir über das neue Konzept sind.

* Team Foundation Service - deren ordnungsgemäße zum Integrieren des Aufrufs von `nuget.exe restore` erstellen Sie in der Standardeinstellung Szenarien.
* Windows Azure-Websites – sie arbeiten können Sie Ihr Projekt in Azure übertragen und `nuget.exe restore` wird aufgerufen, bevor die Website erstellt wird.
* TeamCity – werden sie ihre NuGet-Installer-Plug-in aktualisieren, für TeamCity 8.x
* AppHarbor – sie arbeiten können Sie mithilfe von Push übertragen Ihres Repositorys zum AppHarbor und `nuget.exe restore` wird aufgerufen, bevor die Projektmappe erstellen.

Mit jedem der oben aufgeführten Partner würden sie ihre eigene Kopie nuget.exe verwenden, und Sie müssen nicht zum Ausführen von nuget.exe in Ihrer Lösung.

#### <a name="known-issues"></a>Bekannte Probleme

Gab es zwei bekannte Probleme bei der nuget.exe-Wiederherstellung von der Version 2.7 Erstveröffentlichung, aber sie wurden auf 9/6/2013, mit einem Update korrigiert das [NuGet.CommandLine Paket](http://www.nuget.org/packages/NuGet.CommandLine/).  Dieses Update steht auch auf die [Downloadseite für NuGet 2.7](https://nuget.codeplex.com/releases/view/107605) auf CodePlex.  Ausführung `nuget.exe update -self` wird auf die neueste Version aktualisiert.

Die behoben wurden:

1. [Neue paketwiederherstellung funktioniert unter Mono nicht bei Verwendung der SLN-Datei](https://nuget.codeplex.com/workitem/3596)
1. [Neue paketwiederherstellung funktioniert nicht mit Wix-Projekte](https://nuget.codeplex.com/workitem/3598)

Es gibt auch ein bekanntes Problem mit dem neuen Paket wiederherstellungsworkflow durch [automatische Paketwiederherstellung funktioniert nicht für Projekte unter einem Projektmappenordner](https://nuget.codeplex.com/workitem/3625). Dieses Problem wurde in NuGet 2.7.1 behoben.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Erstellen von erneute Zielzuweisung des Projekt und Upgrades /-Warnungen

Häufig finden Sie nach der neuzuweisung von oder Aktualisierung des Projekts, Sie, dass einige NuGet-Pakete werden nicht ordnungsgemäß. Leider es gibt keinen Hinweis dieser und besteht keine Anleitungen dazu, wie Sie diese beheben. Mit NuGet 2.7 verwenden wir nun einige Visual Studio-Ereignisse um zu erkennen, wenn Sie als Zielversion neu zugewiesen oder das Projekt in einer Weise, die die installierten NuGet-Pakete, wirkt sich auf aktualisiert haben.

Wenn festgestellt wird, dass Ihre Pakete von der neuzuweisung oder Upgrade betroffen sind, werden wir sofort Buildfehler, um Sie zu informieren erzeugen. Zusätzlich zu den unmittelbaren Buildfehler, behalten wir auch eine `requireReinstallation="true"` -flag in Ihrer `packages.config` Datei für alle Pakete, die von der neuzuweisung von beeinflusst, und jeder nachfolgende wurden in Visual Studio erstellen löst Buildwarnungen für diese Pakete.

Obwohl NuGet kann nicht automatisch Maßnahmen ergreifen, die betroffenen Pakete erneut zu installieren, wir hoffen, diese Angabe dass und Warnung Hilfe führt können Sie ermitteln, wenn Sie Pakete installieren müssen. Wir arbeiten auch an [Paket Neuinstallation Anleitungen Dokumentation](../consume-packages/reinstalling-and-updating-packages.md) , dass diese Fehlermeldungen, die Sie weiterleiten.

### <a name="nuget-configuration-defaults"></a>Die Standardeinstellungen der NuGet-Konfiguration

Viele Unternehmen mithilfe von NuGet intern sind, aber hatten schwierigkeiten Leitfaden für ihre Entwickler zum internen Paketquellen statt nuget.org verwenden. NuGet 2.7 führt eine Standardeinstellungen der Konfiguration-Funktion, die computerweiten Standardwerte für angegeben werden können:

1. Aktivierte Paketquellen
1. Registriert, jedoch deaktivierte Paketquellen
1. Die standardmäßige nuget.exe-Push-Quelle

Jede dieser Optionen kann jetzt in eine Datei unter konfiguriert `%ProgramData%\NuGet\NuGetDefaults.Config`. Wenn diese Konfigurationsdatei gibt Paketquellen, Paketquelle von nuget.org standardmäßig nicht automatisch registriert und in `NuGetDefaults.Config` stattdessen registriert wird.

Zwar nicht erforderlich, um dieses Feature zu verwenden, erwarten wir Unternehmen bereitstellen `NuGetDefaults.Config` Dateien mithilfe von Gruppenrichtlinien.

*Beachten Sie, dass diese Funktion niemals führen eine Paketquelle aus eines Entwicklers NuGet-Einstellungen entfernt werden soll. Das bedeutet, wenn der Entwickler bereits NuGet verwendet und dementsprechend Paketquelle von nuget.org registriert, es wird nicht entfernt, nach der Erstellung des eine `NuGetDefaults.Config` Datei.*

Finden Sie unter [NuGet Serverkonfiguration: Standardeinstellungen](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) für Weitere Informationen zu diesem Feature.

### <a name="renaming-the-default-package-source"></a>Die Standardpaketquelle umbenennen

NuGet hat immer registriert die Paketquelle standardmäßig dem Namen "NuGet offizielle Paketquelle", der auf nuget.org zeigt. Dieser Name wurde ausführlich, und es auch nicht angeben, wo sie tatsächlich gezeigt wurde. Um diese beiden Probleme zu beheben, haben wir diese Paketquelle auf einfach "nuget.org" in der Benutzeroberfläche umbenannt. Die URL für die Paketquelle wurde ebenfalls geändert, um den "Www." enthalten. Gruppenpräfix („group.“) zusammensetzt. Nachdem Sie mit NuGet 2.7, Ihre vorhandenen "NuGet offizielle Paketquelle" wird automatisch aktualisiert auf "nuget.org" als Namen und "<https://www.nuget.org/api/v2/>" als die URL.

### <a name="performance-improvements"></a>Leistungsverbesserungen

Wir haben einige leistungsverbesserungen in 2.7, die geringeren Speicherbedarf, weniger Datenträgerverwendung und die schnellere Paketinstallation zurückgibt. Wir haben außerdem intelligentere Abfragen OData-Feeds zu reduzieren, die gesamte Nutzlast vorgenommen.

### <a name="new-extensibility-apis"></a>Neue Erweiterbarkeits-APIs

Wir haben unsere Dienste Erweiterbarkeit, um die Lücke fehlende Funktionen in früheren Versionen zu füllen einige neue APIs hinzugefügt.

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

Dieses Feature wurde von beigetragenen [Adam Ralph](https://twitter.com/adamralph) und Paketersteller zum Deklarieren von Abhängigkeiten, die nur auf die Entwicklung verwendet wurden, Zeit und müssen nicht paketabhängigkeiten ermöglicht. Durch das Hinzufügen einer `developmentDependency="true"` -Attribut auf ein Paket in `packages.config`, `nuget.exe pack` wird das Paket als Abhängigkeit nicht mehr enthalten.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Unterstützung für Visual Studio 2010 Express für Windows Phone

Das neue Paket-Modell für die Wiederherstellung in 2.7 ist durch ein neues VSPackage implementiert, die aus dem Haupt-NuGet-VSPackage unterscheidet. Aufgrund eines technischen Problems, dieses neue VSPackage funktioniert nicht ordnungsgemäß in der *Visual Studio 2010 Express für Windows Phone* SKU wie wir dieselbe Codebasis für andere Benutzer freigeben Visual Studio-SKUs unterstützt. Aus diesem Grund ab NuGet 2.7, wir werden löschen Unterstützung für *Visual Studio 2010 Express für Windows Phone* aus den veröffentlichten Extension. Unterstützung für *zuerst Visual Studio 2010 Express für Web* befindet sich noch in die primäre Durchwahl, die auf dem Visual Studio Extension Gallery veröffentlicht werden.

Da wir nicht sicher sind, wie viele Entwickler weiterhin NuGet in dieser Version/Edition von Visual Studio verwenden, werden wir Veröffentlichen einer separate Visual Studio-Erweiterung speziell für diese Benutzer und veröffentlichen es auf CodePlex (anstelle der Visual Studio Extension Gallery) . Wir planen nicht, um den Vorgang fortzusetzen, verwalten Sie diese Erweiterung, aber wenn dies Sie betrifft informieren Sie uns durch Ausfüllen eines Problems auf CodePlex.

Um den NuGet-Paket-Manager (für Visual Studio 2010 Express für Windows Phone) herunterzuladen, besuchen Sie die [NuGet 2.7 Downloads](https://nuget.codeplex.com/releases/view/107605) Seite.

### <a name="bug-fixes"></a>Fehlerkorrekturen

Neben diesen Features umfasst dieses Release von NuGet auch viele andere Fehlerkorrekturen. Gab es 97 insgesamt in den Release behobenen Problemen. Eine vollständige Liste der Arbeit Elemente eine feste in NuGet 2.7, bitte Ansicht der [NuGet Issue Tracker für diese Version](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
