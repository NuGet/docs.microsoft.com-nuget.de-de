---
title: Anmerkungen zu dieser Version von nuget 2,7
description: Anmerkungen zu dieser Version von nuget 2,7 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 70600e3c563e357663b4a2f24139d2fc25f75fdf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780401"
---
# <a name="nuget-27-release-notes"></a>Anmerkungen zu dieser Version von nuget 2,7

[Anmerkungen zu dieser Version von nuget 2.6.1 für webmatrix](../release-notes/nuget-2.6.1-for-webmatrix.md)  |  [Anmerkungen zu dieser Version von nuget 2.7.1](../release-notes/nuget-2.7.1.md)

Nuget 2,7 wurde am 22. August 2013 veröffentlicht.

## <a name="acknowledgements"></a>Danksagung

Wir danken den folgenden externen Mitwirkenden bei ihren bedeutenden Beiträgen zu nuget 2,7:

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ( [@mxrss](https://twitter.com/mxrss) )
    - Anzeigen der Lizenz-URL beim Auflisten von Paketen und Ausführlichkeit.
2. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )
    - [#1956](http://nuget.codeplex.com/workitem/1956) : das developmentabhängigkeits-Attribut hinzufügen `packages.config` und es im Pack-Befehl verwenden, um nur Lauf Zeit Pakete einzubeziehen.
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ( [@tkrafael](https://twitter.com/tkrafael) )
    - Vermeiden Sie einen doppelten Eigenschafts Schlüssel im nuget.exe Pack-Befehl.
4. [Ben phegan](http://www.codeplex.com/site/users/view/benphegan) ( [@BenPhegan](https://twitter.com/benphegan) )
    - [#2610](http://nuget.codeplex.com/workitem/2610) : erhöhen Sie die Größe des Computer Caches auf 200.
5. [Slava-Trend](http://www.codeplex.com/site/users/view/derigel) ( [@derigel](https://twitter.com/derigel) )
    - [#3217](http://nuget.codeplex.com/workitem/3217) : das nuget-Dialogfeld, das Updates auf der falschen Registerkarte anzeigt
    - Projekt korrigieren. TargetFramework kann in projectmanager NULL sein.
    - [#3248](http://nuget.codeplex.com/workitem/3248) -Korrektur von sharedpackagerepository findpackage/findpackagesbyid schlägt bei nicht vorhandenem PackageID fehl
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ( [@kevfromireland](https://twitter.com/kevfromireland) )
    - [#3234](http://nuget.codeplex.com/workitem/3234) -Unterstützung für das Nomaden Projekt aktivieren
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ( [@corinblaikie](https://twitter.com/corinblaikie) )
    - der [#3252](http://nuget.codeplex.com/workitem/3252) -Fix-Push-Befehl schlägt mit Exitcode 0 fehl, wenn die Datei nicht existiert.
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) beheben Sie den Fehler mit Add-BindingRedirect Befehl, wenn ein Projekt auf ein Datenbankprojekt verweist.
9. [Miroslav-bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ( [@bajtos](https://twitter.com/bajtos) )
    - Fehler bei der [#2891](http://nuget.codeplex.com/workitem/2891) Behebung von "nuget. Pack", wobei der Platzhalter im Attribut "Exclude" falsch verarbeitet wird.
10. [Justin](http://www.codeplex.com/site/users/view/zippy1981) -aufsetzen ( [@zippy1981](https://twitter.com/zippy1981) )
     - [#3307](http://nuget.codeplex.com/workitem/3307) Korrektur Fehler `NuGet.targets` übergibt $ (Platform) nicht an nuget.exe, wenn Pakete wieder hergestellt werden.
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) Korrektur des Fehlers in nuget.exe Package-Befehl, der das Hinzufügen von Dateien mit demselben Namen, aber unterschiedlicher Groß-/Kleinschreibung ermöglicht.
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ( [@kzu](https://twitter.com/kzu) )
     - [#2990](http://nuget.codeplex.com/workitem/2990) -Version der netportableprofile-Klasse hinzufügen.
13. [David simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -Fix-Bug NullReferenceException if Requirements APIKey = true, aber der Header "X-nuget-APIKey" ist nicht vorhanden.
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ( [@friism](https://twitter.com/friism) )
     - [#3278](https://nuget.codeplex.com/workitem/3278) -Fixes "nuget. Build Targets"-Datei auf, damit Sie auf monodevelop ordnungsgemäß funktioniert.
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ( [@pranav_km](https://twitter.com/pranav_km) )
     - Verbessern der Leistung des Wiederherstellungs Befehls durch Erhöhen der Parallelisierung

## <a name="notable-features-in-the-release"></a>Wichtige Features in der Version

### <a name="package-restore-by-default-with-implicit-consent"></a>Paket Wiederherstellung standardmäßig (mit impliziter Zustimmung)

Mit nuget 2,7 wird ein neuer Ansatz für die Paket Wiederherstellung eingeführt, und es kommt auch zu einer wichtigen Hürde: die Zustimmung zur Paket Wiederherstellung ist jetzt standardmäßig aktiviert. Die Kombination des neuen Ansatzes und der impliziten Zustimmung führt zu einer drastischen Vereinfachung der Paket Wiederherstellungs Szenarien.

#### <a name="implicit-consent"></a>Implizite Zustimmung

Mit den nuget-Versionen 2,0, 2,1, 2,2, 2,5 und 2,6 mussten Benutzer das Herunterladen fehlender Pakete während des Builds explizit zulassen. Wenn diese Zustimmung nicht explizit angegeben wurde, können Lösungen, für die die Paket Wiederherstellung aktiviert war, erst erstellt werden, wenn der Benutzer seine Zustimmung erteilt hat.

Ab nuget 2,7 ist die Paket Wiederherstellungs Zustimmung standardmäßig aktiviert, während Benutzer die Paket Wiederherstellung ggf. explizit *ablehnen* können, indem Sie das Kontrollkästchen in den nuget-Einstellungen in Visual Studio verwenden. Diese Änderung der impliziten Zustimmung betrifft nuget in den folgenden Umgebungen:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* nuget.exe Command-Line-Hilfsprogramm

#### <a name="automatic-package-restore-in-visual-studio"></a>Automatische Paket Wiederherstellung in Visual Studio

Ab nuget 2,7 lädt nuget automatisch fehlende Pakete während des Builds in Visual Studio herunter, auch wenn die Paket Wiederherstellung nicht explizit für die Lösung aktiviert wurde. Diese automatische Paket Wiederherstellung erfolgt in Visual Studio, wenn Sie ein Projekt oder eine Projekt Mappe erstellen, aber bevor MSBuild aufgerufen wird. Dies bringt einige bedeutende Vorteile mit sich:

1. Es ist nicht mehr erforderlich, die Geste "nuget-Paket Wiederherstellung aktivieren" für Ihre Lösung zu verwenden.
1. Projekte müssen nicht geändert werden, und nuget nimmt keine Änderungen an Ihrem Projekt vor, um sicherzustellen, dass die Paket Wiederherstellung aktiviert ist.
1. Alle nuget-Pakete, einschließlich derjenigen, die MSBuild-Importe für Eigenschaften/Zieldateien enthalten, werden wieder hergestellt, *bevor* MSBuild aufgerufen wird. Dadurch wird sichergestellt, dass diese Eigenschaften/Ziele während des Builds ordnungsgemäß erkannt werden.

Um die automatische Paket Wiederherstellung in Visual Studio verwenden zu können, müssen Sie nur eine Aktion (in) ausführen:

1. Ordner nicht einchecken `packages`

Es gibt mehrere Möglichkeiten, den `packages` Ordner aus der Quell Code Verwaltung auszulassen. Weitere Informationen finden Sie im Thema [Pakete und Quell](../consume-packages/packages-and-source-control.md) Code Verwaltung.

Obwohl alle Benutzer implizit die automatische Zustimmung zur Paket Wiederherstellung gewählt haben, können Sie die Paket-Manager-Einstellungen in Visual Studio problemlos ablehnen.

![Paket-Manager-Einstellungen](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Vereinfachte Paket Wiederherstellung aus der Command-Line

Mit nuget 2,7 wird eine neue Funktion für nuget.exe eingeführt: `nuget.exe restore`

Mit diesem neuen Restore-Befehl können Sie problemlos alle Pakete für eine Lösung mit einem einzelnen Befehl Wiederherstellen, indem Sie eine Projektmappendatei oder einen Ordner als Argument akzeptieren. Außerdem wird dieses Argument impliziert, wenn nur eine einzige Lösung im aktuellen Ordner vorhanden ist. Dies bedeutet, dass die folgenden Elemente aus einem Ordner, der eine einzelne Projektmappendatei (MySolution. sln) enthält, funktionieren:

1. nuget.exe Restore MySolution. sln
1. nuget.exe Restore.
1. nuget.exe Wiederherstellung

Der Restore-Befehl öffnet die Projektmappendatei und findet alle Projekte in der Projekt Mappe. Von dort werden die `packages.config` Dateien für jedes der Projekte gefunden und alle gefundenen Pakete wieder hergestellt. Außerdem werden Pakete auf Projektmappenebene wieder hergestellt, die in der Datei gefunden wurden `.nuget\packages.config` . Weitere Informationen zum neuen Restore-Befehl finden Sie in der [Befehlszeilen Referenz](../reference/cli-reference/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Der neue Workflow für die Paket Wiederherstellung

Wir freuen uns über diese Änderungen an der Paket Wiederherstellung, da es einen neuen Workflow einführt. Wenn Sie die Pakete aus der Quell Code Verwaltung weglassen möchten, können Sie den Ordner einfach nicht übertragen `packages` . Visual Studio-Benutzer, die die Projekt Mappe öffnen und erstellen, sehen, dass die Pakete automatisch wieder hergestellt werden. Bei Befehlszeilenbuilds rufen Sie einfach auf, bevor Sie aufrufen `nuget.exe restore` `msbuild` . Sie müssen nicht mehr daran denken, die Geste "nuget-Paket Wiederherstellung aktivieren" für Ihre Lösung zu verwenden, und wir müssen Ihre Projekte nicht mehr ändern, um den Build zu ändern. Dies führt auch zu einer deutlich verbesserten Funktionalität für Pakete, die MSBuild-Importe einschließen. Dies gilt insbesondere für Importe, die über das neueste Feature von nuget zum [automatischen Importieren von Eigenschaften/Zieldateien](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) aus dem Ordner "\build" hinzugefügt wurden.

Zusätzlich zu den Aufgaben, die wir selbst durchgeführt haben, arbeiten wir auch mit einigen wichtigen Partnern zusammen, um diesen neuen Ansatz zu umgehen. Wir haben noch keine konkreten Zeitachsen, aber jeder Partner ist so aufgeregt, wie wir den neuen Ansatz kennen.

* Team Foundation Service-Sie arbeiten an der Integration des Aufrufes `nuget.exe restore` in die standardbuildszenarien.
* Windows Azure-Websites: Sie funktionieren, um Ihr Projekt per Push in Azure zu übersetzen und `nuget.exe restore` vor der Erstellung Ihrer Website aufzurufen.
* TeamCity: Sie aktualisieren das nuget-Installer-Plug-in für TeamCity 8. x.
* Appharbor: Sie können Ihr Repository per Push an appharbor übersetzen und `nuget.exe restore` vor dem Erstellen der Projekt Mappe aufgerufen haben.

Mit jedem der oben genannten Partner würden Sie eine eigene Kopie von nuget.exe verwenden, und Sie müssten keine nuget.exe in Ihrer Lösung durchführen.

#### <a name="known-issues"></a>Bekannte Probleme

Es gab zwei bekannte Probleme bei der nuget.exe Restore-Version mit der ersten Version von 2,7. Sie wurden jedoch auf 9/6/2013 mit einem Update des [Pakets "nuget. commandline](http://www.nuget.org/packages/NuGet.CommandLine/)" korrigiert.  Dieses Update steht auch auf der [nuget 2,7-Downloadseite](https://nuget.codeplex.com/releases/view/107605) auf CodePlex zur Verfügung.  `nuget.exe update -self`Das Ausführen von wird auf die neueste Version aktualisiert.

Die festgelegte lautete:

1. [Die neue Paket Wiederherstellung funktioniert bei Verwendung der SLN-Datei nicht in Mono.](https://nuget.codeplex.com/workitem/3596)
1. [Die neue Paket Wiederherstellung funktioniert nicht mit WiX-Projekten.](https://nuget.codeplex.com/workitem/3598)

Es gibt auch ein bekanntes Problem mit dem neuen Paket Wiederherstellungs Workflow, bei dem die [Automatische Paket Wiederherstellung nicht für Projekte in einem Projektmappenordner funktioniert](https://nuget.codeplex.com/workitem/3625). Dieses Problem wurde in nuget 2.7.1 behoben.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Projektneuzuweisungs-und upgradebuildfehler/-Warnungen

Viele Male nach der Neuerstellung oder dem Upgrade Ihres Projekts werden Sie feststellen, dass einige nuget-Pakete nicht ordnungsgemäß funktionieren. Leider gibt es keinen Hinweis darauf, und dann gibt es keine Anleitung, wie Sie es beheben können. Mit nuget 2,7 werden nun einige Visual Studio-Ereignisse verwendet, um zu erkennen, wann Sie Ihr Projekt neu zugewiesen oder auf eine Weise aktualisiert haben, die sich auf die installierten nuget-Pakete auswirkt.

Wenn Sie feststellen, dass Ihre Pakete von der Neuerstellung oder dem Upgrade betroffen sind, führen wir unmittelbare Buildfehler aus, um Sie zu informieren. Zusätzlich zum unmittelbaren Buildfehler behalten wir auch ein `requireReinstallation="true"` Flag in Ihrer `packages.config` Datei für alle Pakete bei, die von der Neuerstellung betroffen sind, und jeder nachfolgende Build in Visual Studio gibt Buildwarnungen für diese Pakete aus.

Obwohl nuget keine automatische Aktion zur erneuten Installation betroffener Pakete ausführen kann, hoffen wir, dass diese Angabe und Warnung Ihnen helfen, herauszufinden, wann Sie Pakete neu installieren müssen. Wir arbeiten auch an der [Dokumentation zur Paket Neuinstallation](../consume-packages/reinstalling-and-updating-packages.md) , die Ihnen diese Fehlermeldungen zuleitet.

### <a name="nuget-configuration-defaults"></a>Nuget-Konfigurations Standardwerte

In vielen Unternehmen wird nuget intern verwendet, aber es war schwierig, Ihre Entwickler daran zu beteiligen, interne Paketquellen anstelle von nuget.org zu verwenden. Mit nuget 2,7 wird eine Funktion für Konfigurations Standards eingeführt, mit der Computer weite Standardwerte für Folgendes angegeben werden können:

1. Aktivierte Paketquellen
1. Registrierte, aber deaktivierte Paketquellen
1. Die Standard nuget.exe Push-Quelle

Diese können jetzt in einer Datei unter konfiguriert werden `%ProgramData%\NuGet\NuGetDefaults.Config` . Wenn diese Konfigurationsdatei Paketquellen angibt, wird die standardmäßige nuget.org-Paketquelle nicht automatisch registriert, und die in werden `NuGetDefaults.Config` stattdessen registriert.

Die Verwendung dieser Funktion ist zwar nicht erforderlich, es wird jedoch erwartet, dass Unternehmen `NuGetDefaults.Config` Dateien mithilfe von Gruppenrichtlinie bereitstellen.

*Beachten Sie, dass diese Funktion niemals bewirkt, dass eine Paketquelle aus den nuget-Einstellungen eines Entwicklers entfernt wird. Dies bedeutet, dass der Entwickler, wenn er nuget bereits verwendet hat und daher die nuget.org-Paketquelle registriert hat, nach dem Erstellen einer Datei nicht entfernt wird `NuGetDefaults.Config` .*

Weitere Informationen zu diesem Feature finden [Sie unter nuget-Konfigurations Standardwerte](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) .

### <a name="renaming-the-default-package-source"></a>Umbenennen der Standardpaket Quelle

Nuget hat immer eine Standardpaket Quelle mit dem Namen "nuget Official Package Source" registriert, die auf nuget.org verweist. Dieser Name war ausführlich, und es wurde auch nicht angegeben, wo er tatsächlich zeigte. Um diese beiden Probleme zu beheben, haben wir diese Paketquelle in "nuget.org" in der Benutzeroberfläche umbenannt. Die URL für die Paketquelle wurde ebenfalls so geändert, dass Sie "www" enthält. . Nachdem Sie nuget 2,7 verwendet haben, wird die vorhandene "nuget Official Package Source" automatisch auf "nuget.org" als Name und " <https://www.nuget.org/api/v2/> " als URL aktualisiert.

### <a name="performance-improvements"></a>Leistungsverbesserungen

Wir haben in 2,7 eine Verbesserung der Leistung erzielt, was zu geringerem Speicherbedarf, weniger Datenträger Nutzung und schnellerer Paketinstallation führt. Außerdem haben wir intelligentere Abfragen für odata-basierte Feeds vorgenommen, wodurch die Gesamt Nutzlast verringert wird.

### <a name="new-extensibility-apis"></a>Neue Erweiterbarkeits-APIs

Wir haben unseren Erweiterbarkeits Diensten einige neue APIs hinzugefügt, um die Lücke fehlender Funktionen in früheren Versionen zu füllen.

#### <a name="ivspackageinstallerservices"></a>Ivspackageinstallerservices

```cs
// Checks if a NuGet package with the specified Id and version is installed in the specified project.
bool IsPackageInstalledEx(Project project, string id, string versionString);

// Get the list of NuGet packages installed in the specified project.
IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
```

#### <a name="ivspackageinstaller"></a>Ivspackagin Staller

```cs
// Installs one or more packages that exist on disk in a folder defined in the registry.
void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

// Installs one or more packages that are embedded in a Visual Studio Extension Package.
void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);
```

### <a name="development-only-dependencies"></a>Abhängigkeiten Development-Only

Diese Funktion wurde von [Adam Ralph](https://twitter.com/adamralph) bereitgestellt und ermöglicht es Paket Autoren, Abhängigkeiten zu deklarieren, die nur zur Entwicklungszeit verwendet wurden und keine Paketabhängigkeiten erfordern. Durch das Hinzufügen eines- `developmentDependency="true"` Attributs zu einem Paket in `packages.config` `nuget.exe pack` wird dieses Paket von nicht mehr als Abhängigkeit einbezogen.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Unterstützung für Visual Studio 2010 Express für Windows Phone wurde entfernt.

Das neue Paket Wiederherstellungs Modell in 2,7 wird von einem neuen VSPackage implementiert, das sich von dem nuget-Haupt-VSPackage unterscheidet. Aufgrund eines technischen Problems funktioniert dieses neue VSPackage in *Visual Studio 2010 Express für Windows Phone* SKU nicht ordnungsgemäß, da wir die gleiche Codebasis mit anderen unterstützten Visual Studio-SKUs gemeinsam verwenden. Ab nuget 2,7 wird die Unterstützung für *Visual Studio 2010 Express für Windows Phone* aus der veröffentlichten Erweiterung entfernt. Die Unterstützung für *Visual Studio 2010 Express für Web* ist weiterhin in der primären Erweiterung enthalten, die im Visual Studio-Erweiterungs Katalog veröffentlicht wurde.

Da wir nicht sicher sind, wie viele Entwickler in dieser Version/Edition von Visual Studio weiterhin nuget verwenden, veröffentlichen wir eine separate Visual Studio-Erweiterung speziell für diese Benutzer und veröffentlichen Sie auf CodePlex (anstelle des Visual Studio-Erweiterungs Katalogs). Wir planen nicht, die Erweiterung fortzusetzen, aber wenn Sie dies betrifft, informieren Sie uns, indem Sie ein Problem auf CodePlex einreichen.

Zum Herunterladen des nuget-Paket-Managers (für Visual Studio 2010 Express für Windows Phone) besuchen Sie die [nuget](https://nuget.codeplex.com/releases/view/107605) -Downloadseite von 2,7.

### <a name="bug-fixes"></a>Fehlerkorrekturen

Zusätzlich zu diesen Features umfasst diese Version von nuget auch viele andere Fehlerbehebungen. In der Version wurden 97 Gesamtprobleme behoben. Eine vollständige Liste der Arbeitselemente, die in nuget 2,7 behoben wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
