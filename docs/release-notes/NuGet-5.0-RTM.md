---
title: Versionshinweise zu NuGet 5.0 RTM
description: Versionshinweise für NuGet 5.0, einschließlich bekannter Probleme, Fehlerbehebungen, neuer Features und DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 19173d2be7cd66b65651655385466b40f5e08352
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901745"
---
# <a name="nuget-50-release-notes"></a>Versionshinweise zu NuGet 5.0

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version| Verfügbar in .NET SDK(s)|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019, Version 16.0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019, Version 16.0.4](https://visualstudio.microsoft.com/downloads/) | [2.1.60x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1,</sup> [2.2.20x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Installation mit Visual Studio 2019 mit .NET Core-Workload 

<sup>2</sup> Verfügbar als optionale Installation mit Visual Studio 2019 mit .NET Core-Workload

## <a name="summary-whats-new-in-50"></a>Zusammenfassung: Neues in Version 5.0

* Unterstützung für die [Wiederherstellung gefilterter Lösungen](/visualstudio/ide/filtered-solutions) in Visual Studio 2019 – [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` -Ordner ermöglicht Paketen das transitive Beitragen von Zielen/Props zum Hostprojekt [– #6091](https://github.com/NuGet/Home/issues/6091)
* Bessere Unterstützung für PackageReference-Szenarien in NuGet-IVs-APIs [– #7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` ist veraltet – [#7928](https://github.com/NuGet/Home/issues/7928)
* Gen 1 Anmeldeinformationsanbieter-Plug-In wurde durch [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) ersetzt und wird bald veraltet sein [– #7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

**Fehler**

* Vermeiden Sie bei einer NoOp-Wiederherstellung *.dgspec.jsbeim Schreiben in das obj-Verzeichnis – [#7854](https://github.com/NuGet/Home/issues/7854)

* Berechtigungen für Dateien, die in ~/.nuget erstellt wurden, sind zu [offen – #7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` funktioniert nicht mit Quellen, die eine Authentifizierung benötigen – [#7605](https://github.com/NuGet/Home/issues/7605)

* NuGet.VisualStudio.IVsPackageInstaller: Beim Aufrufen von für ein Projekt ohne Paketverweise wird immer packages.config verwendet, auch wenn der Standardwert auf PackageReference [-](https://github.com/NuGet/Home/issues/7005) #7005

* PMC: Update-Package Neuinstallation schlägt bei delisteten Paketen fehl ("Paket konnte nicht gefunden werden"). - [#7268](https://github.com/NuGet/Home/issues/7268)

* Hinzufügen von Drittanbieterhinweisen in unserem Repository und vsix – [#7409](https://github.com/NuGet/Home/issues/7409)

* NuGet.VisualStudio.IVsPackageInstaller.InstallPackage sollte die neueste Version installieren, wenn keine Version angegeben ist – [#7493](https://github.com/NuGet/Home/issues/7493)

* --interactive-Unterstützung für dotnet nuget push – [#7519](https://github.com/NuGet/Home/issues/7519)

* Beim Wiederherstellen mit einer Sperrdatei sollte keine NU1603-Warnung ausgelöst werden. - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet sollte während der Wiederherstellung keinen Projektpfad mit minimaler Protokollierung drucken [– #7647](https://github.com/NuGet/Home/issues/7647)

* --interactive-Unterstützung für dotnet remove package – [#7727](https://github.com/NuGet/Home/issues/7727)

* Fügen Sie NuGet.Packaging.Core mit TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache benötigt einen kürzeren Pfad, um gut zu funktionieren [– #7770](https://github.com/NuGet/Home/issues/7770)

* Pfad für msbuild-Ermittlung bevorzugen, wenn der Benutzer nicht nach einer bestimmten msbuild-Version gefragt hat [– #7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` sollte die richtigen msbuild-Versionen [auflisten – #7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): Error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)

* restore listet unnötigerweise den Inhalt aller Versionen des Pakets, auf das verwiesen wird, im Computercache [auf– #7639](https://github.com/NuGet/Home/issues/7639)

* Die automatische MSBuild-Erkennung wählt nach der Installation von VS 2019 Preview immer 16.0 aus [– #7621](https://github.com/NuGet/Home/issues/7621)

* dotnet list-Paket für eine Projektmappe gibt doppelte Einträge für Framework aus [– #7607](https://github.com/NuGet/Home/issues/7607)

* Ausnahme "Leerer Pfadname ist nicht zulässig", wenn IVsPackageInstaller.InstallPackage in alten Projekten und Paketordnern aufgerufen wird, ist nicht vorhanden. - [#5936](https://github.com/NuGet/Home/issues/5936)

* msbuild /t:restore minimaler Ausführlichkeit sollte minimaler sein – [#4695](https://github.com/NuGet/Home/issues/4695)

* Die NuGet-Benutzeroberfläche von VS 16.0 verfügt aufgrund von Farbproblemen über nicht lesbare [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & NuGet.Clients License.txt – [#7629](https://github.com/NuGet/Home/issues/7629)

* Bei der Wiederherstellung wird unnötigerweise ein globaler Paketordner enumeriert, um den Typ zu bestimmen [– #7596](https://github.com/NuGet/Home/issues/7596)

* Fehler bei der Erzwingung von Sperrdatei sollten im Fenster "Fehlerliste" angezeigt werden [– #7429](https://github.com/NuGet/Home/issues/7429)

* Beheben NuGet.ConfigUrationsprobleme [– #7326](https://github.com/NuGet/Home/issues/7326)

* Anpassen an MSBuild, indem der Installationsspeicherort aktualisiert [wird – #7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack sollte eine Entwicklungsabhängigkeit sein – [#7249](https://github.com/NuGet/Home/issues/7249)

* Hinzufügen eines Paketerweiterungspunkts zum Hinzufügen von [Debugsymbolen – #7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` sollte den Abhängigkeitsversionsbereich im erstellten nupkg beibehalten (auch wenn eine unverankerte Version [verwendet wird): #7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` schlägt bei der authentifizierten Quelle fehl, wenn die Konfiguration auf Benutzerebene auch die Quelle [-#7209](https://github.com/NuGet/Home/issues/7209)

* Pack sollte den Satz von BuildActions für Inhaltsdateien nicht einschränken – [#7155](https://github.com/NuGet/Home/issues/7155)

* Die Verwendung eines ProjectReference-Werts, für den AssetTargetFallback erfolgreich sein muss, sollte warnen. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Deadlock aufgrund von Threadingproblemen beim Aufrufen von CPS (CommonProjectSystem) [– #7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` verwendet keine Anmeldeinformationen aus der globalen Konfiguration für eine quelle, die in der lokalen Konfiguration angegeben [ist – #6935](https://github.com/NuGet/Home/issues/6935)

* Threadingprobleme beim Aufrufen von MEF für asynchrone Codepfade – [#6771](https://github.com/NuGet/Home/issues/6771)

* Signierung: Fehler zweimal und ohne Aufrufliste gemeldet [– #6455](https://github.com/NuGet/Home/issues/6455)

* Beim Installieren eines signierten Pakets mit einem nicht vertrauenswürdigen Signaturzertifikat sollte ein Fehler angezeigt [werden: #6318](https://github.com/NuGet/Home/issues/6318)

* NuGet stellt NoOps nicht ordnungsgemäß wieder auf, wenn zwei Projekte obj-Verzeichnis [gemeinsam nutzen – #6114](https://github.com/NuGet/Home/issues/6114)

* PAT kann nicht mit `dotnet restore` unter Linux mit Paketen aus authentifizierten Feeds verwendet werden [– #5651](https://github.com/NuGet/Home/issues/5651)

* dotnet restore schlägt aufgrund eines deaktivierten computerweiten Feeds fehl – [#5410](https://github.com/NuGet/Home/issues/5410)

**DCRs**

* Warnung vor zukünftigem Entfernen von "dotnet pack project.json" [– #7928](https://github.com/NuGet/Home/issues/7928)
 
* Hinzufügen einer Veraltungswarnung für das Gen1-Anmeldeinformations-Plug-In [– #7819](https://github.com/NuGet/Home/issues/7819)
 
* Signierung: Aktiviertes Repository, um die Clientüberprüfung jedes Pakets als Repository zu erfordern, das signiert ist – über die Ressource RepositorySignatures/5.0.0 – [#7759](https://github.com/NuGet/Home/issues/7759)

* Beschränken der HTTP-Anforderungsnummer pro Quelle über NuGet.Config [– #4538](https://github.com/NuGet/Home/issues/4538)

* NuGet sollte auf Net472 ausgerichtet sein (um den 16.0-Build der VSIX zu bereinigen) – [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: OpenPackagePage-Befehl entfernen [– #7384](https://github.com/NuGet/Home/issues/7384)

* Zuordnen von NetCoreApp 3.0 zu NetStandard 2.1 [– #7762](https://github.com/NuGet/Home/issues/7762)

* Hinzufügen von netstandard2.0-Unterstützung zu NuGet.*-Paketen [– #6516](https://github.com/NuGet/Home/issues/6516)

* Zulassen, dass Paketautoren transitives Verhalten für Buildressourcen definieren – [#6091](https://github.com/NuGet/Home/issues/6091)

* Unterstützung des Features "VS 2019-Lösungsfilter". Unterstützt auch Projekte, die nicht in projektmappen oder entladenen Projekten verfügbar sind. Erste Wiederherstellung der vollständigen Lösung (über CLI oder VS) [– #5820](https://github.com/NuGet/Home/issues/5820)

* NuGet 5.0-Assemblys erfordern .NET 4.7.2 (über TFM-Änderung) [– #7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData von NuGet.Packaging sollte ein öffentlicher Typ sein. Aktualisieren sie die lizenzmetadaten, die von der -Datei erfasst wurden. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Veraltete Einstellungs-APIs entfernen – [#7294](https://github.com/NuGet/Home/issues/7294)

* Problemumgehung für Wiederherstellungstimeouts auf Systemen mit 1 CPU [– #6742](https://github.com/NuGet/Home/issues/6742)

* NuGet bevorzugt die NTLM-Authentifizierung, auch wenn anmeldeinformationen in NuGet.config vorhanden sind– Option "Konfiguration hinzufügen" zum Filtern von Authentifizierungstypen nach Anmeldeinformationen – [#5286](https://github.com/NuGet/Home/issues/5286)

* Aktivieren von EmbedInteropTypes für PackageReference (Packages.Config-Funktion) – [#2365](https://github.com/NuGet/Home/issues/2365)

**[Liste aller in diesem Release behobenen Probleme: 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>Zusammenfassung: Neues in Version 5.0.2

* Sicherheit (bei Ausführung über dotnet.exe oder mono.exe): Der Ordner obj sollte mit [](https://github.com/NuGet/Home/issues/7908) den richtigen Berechtigungen #7908

* nuget.exe wiederherzustellen unter mono/macOS schlägt mit benutzerdefinierten nuget.config `PackageSignatureValidity: False` [](https://github.com/NuGet/Home/issues/8011) und #8011


## <a name="known-issues"></a>Bekannte Probleme

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>Von .NET Core SDK in FallbackFolders installierte Pakete werden benutzerdefiniert installiert und bestehen die Signaturüberprüfung nicht. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Problem
Bei Verwendung von dotnet.exe 2.x zum Wiederherstellen eines Projekts mit mehreren Zielen netcoreapp 1.x und netcoreapp 2.x wird der Fallbackordner als Dateifeed behandelt. Dies bedeutet, dass NuGet bei der Wiederherstellung das Paket aus dem Fallbackordner auswählt und versucht, es im globalen Paketordner zu installieren, und die übliche Signaturüberprüfung durchführt, bei der ein Fehler auftritt.<br>
#### <a name="workaround"></a>Problemumgehung
Deaktivieren Sie die Verwendung des Fallbackordners, indem Sie auf `RestoreAdditionalProjectSources` nichts festlegen:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Verwenden Sie dies mit Vorsicht, da Pakete, die aus dem Fallbackordner wiederhergestellt werden würden, jetzt von NuGet.org.