---
title: Anmerkungen zu dieser Version von nuget 5,0 RTM
description: Anmerkungen zu dieser Version von nuget 5,0 einschließlich bekannter Probleme, Fehlerbehebungen, neuer Features und dcrs.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 52c71c6fe1a1854d5aed229abf2ce7ddc2685ae9
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611342"
---
# <a name="nuget-50-release-notes"></a>Anmerkungen zu dieser Version von nuget 5,0

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version| Verfügbar in .NET SDK(s)|
|:---|:---|:---|
| [**verfügbar**](https://nuget.org/downloads) | [Visual Studio 2019, Version 16,0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019 Version 16.0.4](https://visualstudio.microsoft.com/downloads/) | [2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Installiert mit Visual Studio 2019 mit .net Core-Arbeitsauslastung 

<sup>2</sup> Verfügbar als optionale Installation mit Visual Studio 2019 mit .net Core-Arbeitsauslastung

## <a name="summary-whats-new-in-50"></a>Zusammenfassung: Neues in 5,0

* Unterstützung für die Wiederherstellung von [gefilterten Lösungen](https://docs.microsoft.com/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019- [#5820](https://github.com/NuGet/Home/issues/5820)
* mit `BuildTransitive` Ordner können Pakete transitiv Ziele/Eigenschaften zum Host Projekt beitragen [#6091](https://github.com/NuGet/Home/issues/6091)
* Bessere Unterstützung für packagereferenzierungsszenarien in nuget IVS-APIs- [#7005](https://github.com/NuGet/Home/issues/7005) [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` ist veraltet- [#7928](https://github.com/NuGet/Home/issues/7928)
* Das Plug-in für die Anmelde Informationsanbieter-Plug-in wurde von Generation [2](https://aka.ms/nuget-cross-platform-authentication-plugin) abgelöst und wird in Kürze als veraltet eingestuft- [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

**Fehler**

* Wenn Sie eine NOOP-Wiederherstellung durchgeführt haben, vermeiden Sie das Schreiben von *. dgspec. JSON in obj-Verzeichnis [#7854](https://github.com/NuGet/Home/issues/7854)

* Berechtigungen für Dateien, die in ~/.nuget erstellt werden, sind zu offen [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` funktioniert nicht mit Quellen, die Authentifizierung- [#7605](https://github.com/NuGet/Home/issues/7605) benötigen.

* "Nuget. VisualStudio. ivspackageinstaller-Call" für ein Projekt ohne Paket Verweise verwendet immer "Packages. config", auch wenn die Standardeinstellung auf "packagerereferences- [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC: bei der erneuten Installation von Update-Package tritt ein Fehler auf ("das Paket wurde nicht gefunden"). - [#7268](https://github.com/NuGet/Home/issues/7268)

* Hinzufügen eines Drittanbieter Hinweises in unserem Repository und VSIX- [#7409](https://github.com/NuGet/Home/issues/7409)

* "Nuget. VisualStudio. ivspackageinstaller. INSTALLPACKAGE" sollte die neueste Version installieren, wenn keine Version angegeben ist [#7493](https://github.com/NuGet/Home/issues/7493)

* --interaktive Unterstützung für dotnet nuget Push- [#7519](https://github.com/NuGet/Home/issues/7519)

* Bei der Wiederherstellung mit der Sperrdatei sollte NU1603 Warning nicht ausgelöst werden. - [#7529](https://github.com/NuGet/Home/issues/7529)

* Nuget sollte den Projektpfad während der Wiederherstellung nicht mit minimaler Protokollierung drucken [#7647](https://github.com/NuGet/Home/issues/7647)

* --interaktive Unterstützung für dotnet Remove Package- [#7727](https://github.com/NuGet/Home/issues/7727)

* Fügen Sie "nuget. Packaging. Core" mit typeforwardto attrs- [#7768](https://github.com/NuGet/Home/issues/7768) hinzu.

* plugins_cache erfordert einen kürzeren Pfad, um gut zu funktionieren [#7770](https://github.com/NuGet/Home/issues/7770)

* Pfad für MSBuild-Ermittlung bevorzugen, wenn der Benutzer keine bestimmte MSBuild-Version angefordert hat [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` sollte die korrekten MSBuild-Versionen auflisten [#7794](https://github.com/NuGet/Home/issues/7794)

* Nuget. targets (498, 5): Fehler: ein Teil des Pfads "/tmp/NuGetScratch-on Mono- [#7793](https://github.com/NuGet/Home/issues/7793) wurde nicht gefunden.

* Restore listet den Inhalt aller Versionen des Pakets, auf das verwiesen wird, im Computer Cache auf. [#7639](https://github.com/NuGet/Home/issues/7639)

* Die automatische MSBuild-Erkennung wählt nach der Installation von vs 2019 Preview- [#7621](https://github.com/NuGet/Home/issues/7621) immer 16,0 aus.

* Das dotnet List-Paket für eine Lösung gibt doppelte Einträge für Framework- [#7607](https://github.com/NuGet/Home/issues/7607) aus.

* Ausnahme "leerer Pfadname ist nicht zulässig" beim Aufrufen von ivspackageinstaller. INSTALLPACKAGE für alte Projekte, und der Ordner "Packages" ist nicht vorhanden. - [#5936](https://github.com/NuGet/Home/issues/5936)

* MSBuild/t: Minimale Ausführlichkeit der Wiederherstellung sollte minimal sein [#4695](https://github.com/NuGet/Home/issues/4695)

* Die nuget-Benutzeroberfläche von vs 16,0 verfügt über unlesbare Registerkarten aufgrund von Farb Problemen [#7735](https://github.com/NuGet/Home/issues/7735)

* Nuget. Core & nuget. Clients License. txt-Erläuterung- [#7629](https://github.com/NuGet/Home/issues/7629)

* Restore listet den globalen Paket Ordner auf, wenn versucht wird, Type- [#7596](https://github.com/NuGet/Home/issues/7596) zu bestimmen.

* Fehler bei der Erzwingung von Sperrdateien sollten in Fehlerliste Fenster angezeigt werden [#7429](https://github.com/NuGet/Home/issues/7429)

* Beheben von Problemen mit nuget. Configuration- [#7326](https://github.com/NuGet/Home/issues/7326)

* Anpassen an MSBuild Aktualisieren des Installations Speicher Orts [#7325](https://github.com/NuGet/Home/issues/7325)

* "Nuget. Build. Tasks. Pack" sollte eine Entwicklungs Abhängigkeit [#7249](https://github.com/NuGet/Home/issues/7249)

* Hinzufügen des Paket Erweiterungs Punkts zum Einschließen von Debugsymbolen- [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` sollten den Abhängigkeits Versions Bereich in der erstellten nupkg beibehalten (auch wenn die unverankerte Version verwendet wird)- [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` schlägt bei einer authentifizierten Quelle fehl, wenn die Konfigurationsdatei auf Benutzerebene auch über Quell [#7209](https://github.com/NuGet/Home/issues/7209) verfügt.

* Paket sollte den Satz von buildactions für Inhalts Dateien nicht einschränken- [#7155](https://github.com/NuGet/Home/issues/7155)

* Wenn Sie eine projectreferenzierung verwenden, bei der "assettargetfallback" ausgeführt werden muss, sollte gewarnt werden. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Deadlock aufgrund von Threading Problemen beim Aufrufen von CPS (commonprojectsystem)- [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` verwendet keine Anmelde Informationen aus der globalen Konfiguration für eine in der lokalen Konfiguration angegebene Quelle- [#6935](https://github.com/NuGet/Home/issues/6935)

* Threading Probleme mit MEF, die für Async-Codepfade aufgerufen werden- [#6771](https://github.com/NuGet/Home/issues/6771)

* Signierung: der Fehler wird zweimal und ohne aufrufsstapel [#6455](https://github.com/NuGet/Home/issues/6455) gemeldet.

* Beim Installieren eines signierten Pakets mit nicht vertrauenswürdigem Signaturzertifikat sollte Fehler [#6318](https://github.com/NuGet/Home/issues/6318) angezeigt werden.

* Nuget Restore nicht ordnungsgemäß, wenn zwei Projekte das obj-Verzeichnis gemeinsam nutzen [#6114](https://github.com/NuGet/Home/issues/6114)

* Pat mit `dotnet restore` unter Linux kann nicht mit Paketen aus authentifizierten Feeds verwendet werden [#5651](https://github.com/NuGet/Home/issues/5651)

* DotNet Restore Fehler aufgrund eines deaktivierten Computer weiten Feeds- [#5410](https://github.com/NuGet/Home/issues/5410)

**DCRs**

* Warnung zur zukünftigen Entfernung von "dotnet Pack Project. JSON"- [#7928](https://github.com/NuGet/Home/issues/7928)
 
* Fügen Sie eine veralnungs Warnung für das Gen1 Anmelde Informationen-Plug-in hinzu [#7819](https://github.com/NuGet/Home/issues/7819)
 
* Signieren: aktiviertes Repository, das die Client Überprüfung jedes Pakets als durch das Repository signiertes Repository erfordert, über RepositorySignatures/5.0.0 Resource- [#7759](https://github.com/NuGet/Home/issues/7759)

* Begrenzen der HTTP-Anforderungs Nummer pro Quelle über "nuget. config" [#4538](https://github.com/NuGet/Home/issues/4538)

* Nuget sollte auf Net472 abzielen (um die Bereinigung des 16,0-Builds der VSIX zu erleichtern)- [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: openpackagepage-Befehls [#7384](https://github.com/NuGet/Home/issues/7384) entfernen

* Erstellen von netcoreapp 3,0 mit netstandard 2,1- [#7762](https://github.com/NuGet/Home/issues/7762)

* Hinzufügen von netstandard 2.0-Unterstützung zu nuget. * Packages- [#6516](https://github.com/NuGet/Home/issues/6516)

* Ermöglicht es Paket Autoren, das transitiv Verhalten von buildassets zu definieren- [#6091](https://github.com/NuGet/Home/issues/6091)

* Unterstützung des vs 2019-Lösungs Filter Features. Unterstützt auch Projekte, die nicht in einer Projekt Mappe oder entladen wurden. Die komplette Lösung (über CLI oder vs) muss zuerst wieder hergestellt werden [#5820](https://github.com/NuGet/Home/issues/5820)

* Nuget 5,0-Assemblys für die Verwendung von .NET 4.7.2 (über TFM-Änderung): [#7510](https://github.com/NuGet/Home/issues/7510)

* Nugetlicencdata aus nuget. Packaging sollte ein öffentlicher Typ sein. Aktualisieren Sie die Lizenz Metadaten, die von spdx erfasst wurden. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Entfernen veralteter Einstellungs-APIs- [#7294](https://github.com/NuGet/Home/issues/7294)

* Problem Umgehung Wiederherstellungs Timeouts für Systeme mit einer CPU- [#6742](https://github.com/NuGet/Home/issues/6742)

* Nuget bevorzugt NTLM-Authentifizierung, auch wenn Anmelde Informationen in der Datei "nuget. config-Add config" vorhanden sind, um Authentifizierung-Typen nach Anmelde Informationen zu filtern- [#5286](https://github.com/NuGet/Home/issues/5286)

* Embedinteroptypes für packagereferenzierung aktivieren (übereinstimmende Pakete. config-Funktion)- [#2365](https://github.com/NuGet/Home/issues/2365)

**[Liste aller in dieser Version behobene Probleme-5,0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>Zusammenfassung: Neues in 5.0.2

* Sicherheit (wenn Sie über "dotnet. exe" oder "Mono. exe" ausgeführt werden): der Ordner "obj" sollte mit den korrekten Berechtigungen erstellt werden [#7908](https://github.com/NuGet/Home/issues/7908)

* Fehler bei der Wiederherstellung von nuget. exe in Mono/MacOS mit benutzerdefinierten nuget. config-und `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>Bekannte Probleme

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Von .NET Core SDK in FallbackFolders installierte Pakete werden benutzerdefiniert installiert und bestehen die Signaturüberprüfung nicht. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Problem
Bei Verwendung von dotnet.exe 2.x zum Wiederherstellen eines Projekts mit mehreren Zielen netcoreapp 1.x und netcoreapp 2.x wird der Fallbackordner als Dateifeed behandelt. Dies bedeutet, dass NuGet bei der Wiederherstellung das Paket aus dem Fallbackordner auswählt und versucht, es im globalen Paketordner zu installieren, und die übliche Signaturüberprüfung durchführt, bei der ein Fehler auftritt.<br>
#### <a name="workaround"></a>Problemumgehung
Deaktivieren Sie die Verwendung des Fall Back Ordners, indem Sie die `RestoreAdditionalProjectSources` auf "Nothing" festlegen:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Verwenden Sie dies mit Vorsicht, da Pakete, die aus dem Fall Back Ordner wieder hergestellt werden, jetzt von NuGet.org heruntergeladen werden.
