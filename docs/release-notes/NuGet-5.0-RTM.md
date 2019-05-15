---
title: Anmerkungen zu NuGet 5.0 RTM
description: Anmerkungen zu NuGet-5.0, einschließlich bekannter Probleme, Fehlerbehebungen, neuen Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 7e719a3bb5069c461820c6f884487af1eb04bf86
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610661"
---
# <a name="nuget-50-release-notes"></a>Anmerkungen zu NuGet 5.0

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version| Verfügbar in .NET SDK(s)|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 Version 16.0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019 version 16.0.4](https://visualstudio.microsoft.com/downloads/) | [2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>mit Visual Studio-2019 mit .NET Core-Workload installiert 

<sup>2</sup>verfügbar als optionale Installation mit Visual Studio-2019 mit .NET Core-Workload

## <a name="summary-whats-new-in-50"></a>Zusammenfassung: Neuerungen in 5.0

* Unterstützung für die Wiederherstellung [gefiltert Lösungen](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio-2019 - [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` Ordner kann Pakete transitiv targets-und Props zum Hostprojekt mitwirken [#6091](https://github.com/NuGet/Home/issues/6091)
* Bessere Unterstützung für PackageReference-Szenarien in NuGet IVs-APIs – [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` veraltet - [#7928](https://github.com/NuGet/Home/issues/7928)
* Gen 1-Anmeldeinformationsanbieter-Plug-in wurde ersetzt durch [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) und wird in Kürze veraltet sein – [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

**Fehler**

* Wenn eine NoOp-Wiederherstellung durchführen zu können, sollten Sie vermeiden *. dgspec.json schreiben im Verzeichnis "Obj" - [#7854](https://github.com/NuGet/Home/issues/7854)

* Berechtigungen für Dateien, die in ~/.nuget erstellt werden, zu open - [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` funktioniert nicht mit Datenquellen, die Authentifizierung – [#7605](https://github.com/NuGet/Home/issues/7605)

* NuGet.VisualStudio.IVsPackageInstaller - Aufruf in einem Projekt mit kein Paket verweist immer auf "Packages.config" verwendet, auch wenn der Standardwert festgelegt ist, zu "packagereference" - [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC: Update-Paket installieren schlägt fehl ("kann nicht gefunden") für die Pakete aus der Liste entfernen. - [#7268](https://github.com/NuGet/Home/issues/7268)

* Fügen Sie in unserem Repository und die VSIX - Hinweis zu Drittanbietern [#7409](https://github.com/NuGet/Home/issues/7409)

* NuGet.VisualStudio.IVsPackageInstaller.InstallPackage sollten die neueste Version, wenn keine Version angegeben – installieren [#7493](https://github.com/NuGet/Home/issues/7493)

* – Interaktive Unterstützung für Dotnet Nuget Push - [#7519](https://github.com/NuGet/Home/issues/7519)

* Wenn Sie mit der Datei wiederherstellen, sollte nicht NU1603 Warnung ausgelöst werden. - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet sollten Projektpfad nicht drucken, während der Wiederherstellung mit minimaler Protokollierung - [#7647](https://github.com/NuGet/Home/issues/7647)

* – Interaktive Unterstützung für Dotnet-remove Paket - [#7727](https://github.com/NuGet/Home/issues/7727)

* Hinzufügen NuGet.Packaging.Core mit TypeForwardedTo Attrs - später wieder [#7768](https://github.com/NuGet/Home/issues/7768)

* Plugins_cache benötigt kürzerer Pfad für eine gute - Lösung [#7770](https://github.com/NuGet/Home/issues/7770)

* Pfad für die Ermittlung von Msbuild bevorzugen, wenn Benutzer bestimmte Msbuild-Version - anfordern nicht [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` tragen Sie richtige Msbuild-Versionen – [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): error : Einen Teil des Pfads konnte nicht gefunden "/ Tmp/NuGetScratch - unter Mono - [#7793](https://github.com/NuGet/Home/issues/7793)

* Wiederherstellung listet unnötigerweise den Inhalt von allen Versionen von Referenziertes Paket im Cache Machine - [#7639](https://github.com/NuGet/Home/issues/7639)

* Automatische Erkennung von MSBuild wählt immer 16.0, nach der Installation von Visual Studio 2019 Vorschau - [#7621](https://github.com/NuGet/Home/issues/7621)

* Dotnet-umgebungsaufgabenlisten-Paket für eine Lösung gibt doppelte Einträge für Framework - [#7607](https://github.com/NuGet/Home/issues/7607)

* Ausnahme "ein leerer Pfad ist nicht zulässig." beim aufrufenden IVsPackageInstaller.InstallPackage auf dem alten Projekte und-Pakete Ordner ist nicht vorhanden. - [#5936](https://github.com/NuGet/Home/issues/5936)

* MSBuild/t: Restore Ausführlichkeitsgrad muss funktionalitätsanforderungen - [#4695](https://github.com/NuGet/Home/issues/4695)

* Visual Studio 16.0 NuGet UI enthält unlesbare Registerkarten aufgrund von Problemen mit Farbe - [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & NuGet.Clients Dateien "License.txt" Klarstellung - [#7629](https://github.com/NuGet/Home/issues/7629)

* Wiederherstellung listet globalen Paketordner unnötigerweise beim Versuch, um zu bestimmen, Typ: [#7596](https://github.com/NuGet/Home/issues/7596)

* Fehler von der Erzwingung der Sperre-Datei sollte angezeigt werden in der Fehlerliste (Fenster) - [#7429](https://github.com/NuGet/Home/issues/7429)

* Beheben von Problemen mit NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)

* Aktualisieren die Installation von MSBuild anpassen Ort – [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack muss eine entwicklungsabhängigkeit - [#7249](https://github.com/NuGet/Home/issues/7249)

* Hinzufügen von Pack Erweiterungspunkt zum Einschließen von Debugsymbole - [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` Abhängigkeit Versionsbereich in erstellte NuGet-Paket (auch, wenn die unverankerte Version verwendet wird) - beibehalten soll [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` nicht authentifizierte Quelle bei der Benutzerebene Config-Quelle – auch verfügt über [#7209](https://github.com/NuGet/Home/issues/7209)

* Pack sollten nicht nur BuildActions für Inhaltsdateien - [#7155](https://github.com/NuGet/Home/issues/7155)

* Verwenden eine "ProjectReference" AssetTargetFallback erfolgreich ausgeführt werden müssen, sollte eine Warnung ausgeben. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Deadlock aufgrund von Threadingprobleme beim Aufrufen von in CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` Verwenden Sie nicht für eine Datenquelle angegeben, in der lokalen Konfiguration - Anmeldeinformationen aus der globalen Konfiguration [#6935](https://github.com/NuGet/Home/issues/6935)

* Threadingprobleme mit MEF, die aufgerufen wird, auf die asynchrone Codepfade - [#6771](https://github.com/NuGet/Home/issues/6771)

* Anmeldung: Fehler zweimal und ohne Aufrufliste - [#6455](https://github.com/NuGet/Home/issues/6455)

* Installieren eines signierten Pakets mit nicht vertrauenswürdigen Signaturzertifikat sollte angezeigt werden Fehler: [#6318](https://github.com/NuGet/Home/issues/6318)

* NuGet restore noops sind nicht ordnungsgemäß, beim Verzeichnis "Obj" - 2-Projekten gemeinsam [#6114](https://github.com/NuGet/Home/issues/6114)

* Können keine PAT mit `dotnet restore` unter Linux mit Paketen aus authentifizierte Feeds - [#5651](https://github.com/NuGet/Home/issues/5651)

* Dotnet-Restore versagt, wenn deaktivierte auf den gesamten Computer feed - [#5410](https://github.com/NuGet/Home/issues/5410)

**DCRs**

* Warnhinweis anzeigen, über zukünftige Entfernen von "Dotnet Pack Datei"Project.JSON"" - [#7928](https://github.com/NuGet/Home/issues/7928)
 
* Fügen Sie eine Warnung zu veralteten Gen1-Anmeldeinformationen-Plug-in - [#7819](https://github.com/NuGet/Home/issues/7819)
 
* Signierung: Aktivierte Repository zum Erzwingen einer Client-Überprüfung von jedem Paket als Repository signiert--über RepositorySignatures/5.0.0-Ressource - [#7759](https://github.com/NuGet/Home/issues/7759)

* Beschränken der Anzahl von HTTP-Anforderung pro Datenquelle über die Datei "NuGet.config" - [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet sollten Net472 (um die Bereinigung der 16,0 Build des VSIX-Hilfe) - Ziel [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: Entfernen Sie OpenPackagePage-Befehl – [#7384](https://github.com/NuGet/Home/issues/7384)

* Stellen NetCoreApp 3.0-Karte, um NetStandard 2.1 – [#7762](https://github.com/NuGet/Home/issues/7762)

* Pakete, NuGet.* netstandard2.0-Unterstützung hinzufügen [#6516](https://github.com/NuGet/Home/issues/6516)

* Paketersteller, die zum Definieren von Ressourcen transitive Buildverhalten - ermöglichen [#6091](https://github.com/NuGet/Home/issues/6091)

* Visual Studio 2019 Lösungsfilter-Funktion unterstützt. Unterstützt auch das Projekt nicht in der Projektmappe oder entladene Projekte. Vollständige Lösung (per CLI oder Visual Studio) zuerst - wiederherstellen müssen [#5820](https://github.com/NuGet/Home/issues/5820)

* NuGet-5.0-Assemblys in .NET 4.7.2 (über die Änderung der TFM) - erfordern [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData aus NuGet.Packaging sollte ein öffentlicher Typ sein. Aktualisieren Sie die Lizenzmetadaten aus Spdx erfasst. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Entfernen Sie veraltete APIs für Einstellungen – [#7294](https://github.com/NuGet/Home/issues/7294)

* Problemumgehung Wiederherstellung Timeouts auf Systemen mit 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet NTLM-Authentifizierung bevorzugt, auch wenn die Anmeldeinformationen vorhanden sind, in der Datei "NuGet.config" – Filter-Auth-Typen zur Eingabe von Anmeldeinformationen - Option "Config" hinzufügen [#5286](https://github.com/NuGet/Home/issues/5286)

* Aktivieren Sie EmbedInteropTypes für "packagereference" (übereinstimmende Datei "Packages.config"-Funktion) - [#2365](https://github.com/NuGet/Home/issues/2365)

**[Liste aller in diesem Release - 5.0 RTM behobene Probleme](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>Zusammenfassung: Neuerungen in 5.0.2

* Sicherheit (über dotnet.exe "oder" mono.exe Ausführungszeit): der Ordner "Obj" sollten erstellt werden, mit den richtigen Berechtigungen [#7908](https://github.com/NuGet/Home/issues/7908)

* NuGet.exe-Wiederherstellung unter Mono/MacOS ein Fehler auftritt, mit der benutzerdefinierten Datei "NuGet.config" und `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>Bekannte Probleme

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Von .NET Core SDK in FallbackFolders installierte Pakete werden benutzerdefiniert installiert und bestehen die Signaturüberprüfung nicht. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Problem
Bei Verwendung von dotnet.exe 2.x zum Wiederherstellen eines Projekts mit mehreren Zielen netcoreapp 1.x und netcoreapp 2.x wird der Fallbackordner als Dateifeed behandelt. Dies bedeutet, dass NuGet bei der Wiederherstellung das Paket aus dem Fallbackordner auswählt und versucht, es im globalen Paketordner zu installieren, und die übliche Signaturüberprüfung durchführt, bei der ein Fehler auftritt.<br>
#### <a name="workaround"></a>Problemumgehung
Deaktivieren Sie die Verwendung des Ordners fallback durch Festlegen der `RestoreAdditionalProjectSources` auf nichts verweist:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Verwenden Sie dies mit Vorsicht, da Pakete, die aus dem fallback Ordner wiederhergestellt werden soll nun aus "NuGet.org" heruntergeladen werden.
