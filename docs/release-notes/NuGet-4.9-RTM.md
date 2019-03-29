---
title: Anmerkungen zu NuGet 4.9 RTM
description: Anmerkungen zu NuGet 4.9 einschließlich bekannter Fehler, Fehlerkorrekturen, neuer Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: e0dea74fe179c0dce4996f3e498185bb3a491856
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432490"
---
# <a name="nuget-49-release-notes"></a>Anmerkungen zu NuGet 4.9

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version| Verfügbar in .NET SDK(s)|
|:---|:---|:---|
| [**4.9.0**](https://nuget.org/downloads) | [Visual Studio 2017, Version 15.9.0](https://visualstudio.microsoft.com/downloads/) | [2.1.500, 2.2.100](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.1**](https://nuget.org/downloads) | n/v | n/v |
| [**4.9.2**](https://nuget.org/downloads) |[Visual Studio 2017 Version 15.9.4](https://visualstudio.microsoft.com/downloads/) | [2.1.502, 2.2.101](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.3**](https://nuget.org/downloads) |[Visual Studio 2017, Version 15.9.6](https://visualstudio.microsoft.com/downloads/) | [2.1.504, 2.2.104](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a>Zusammenfassung: Neuerungen in Version 4.9.0

* Signierung: Aktivieren von ClientPolicies, um die Nutzung eines Satzes vertrauenswürdiger Autoren und Repositorys als erforderlich festzulegen, die in „NuGet.Config“ aufgelistet sind – [#6961](https://github.com/NuGet/Home/issues/6961), [Blogbeitrag](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)

* Erstellen von SNUPKG-Dateien, sodass Symbole im Paket enthalten sind – Erweitern von Push zum Verstehen des NuGet-Protokolls zum Akzeptieren der SNUPKG-Dateien für den Symbolserver – [#6878](https://github.com/NuGet/Home/issues/6878), [Blogbeitrag](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)

* NuGet-Anmeldeinformationen-Plug-In V2 – [#6642](https://github.com/NuGet/Home/issues/6642)

* Eigenständige NuGet-Pakete – Lizenz – [#4628](https://github.com/NuGet/Home/issues/4628), [Ankündigung](https://github.com/NuGet/Announcements/issues/32)

* Aktivieren Sie die „GeneratePathProperty“-Metadaten einer PackageReference zum Abonnieren zum Generieren einer MSBuild-Eigenschaft pro Paket im Verzeichnis „Foo.Bar\1.0\"“ – [#6949](https://github.com/NuGet/Home/issues/6949)

* Verbessern Sie den Kundenerfolg mit NuGet-Vorgängen – [#7108](https://github.com/NuGet/Home/issues/7108)

* Aktivieren wiederholbarer Paketwiederherstellungen mithilfe einer Sperrdatei – [#5602](https://github.com/NuGet/Home/issues/5602), [Ankündigung](https://github.com/NuGet/Announcements/issues/28), [Blogbeitrag](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

* Von PackageExtraction ausgelöste, (über WarnAsErrors) zu Fehlern heraufgestufte Warnungen sollten nie ein extrahiertes Paket hinterlassen – [#7445](https://github.com/NuGet/Home/issues/7445)

* Fehlerhaft signierte Pakete sollten nicht im globalen Paketordner abgelegt werden – [#7423](https://github.com/NuGet/Home/issues/7423)

* Bindungsumleitungsgenerierung sollte vordergründige Assemblys nicht überspringen – [#7393](https://github.com/NuGet/Home/issues/7393)

* „VersionRange Equals“ vergleicht keine Gleitkommabereiche – [#7324](https://github.com/NuGet/Home/issues/7324)

* Wiederherstellen: Leistungsregression unter Verwendung des neuen .NET Core 2.1 HTTP-Stapels – [#7314](https://github.com/NuGet/Home/issues/7314)

* Aktualisieren eines Pakets sollte PrivateAssets einer PackageReference nicht ändern – [#7285](https://github.com/NuGet/Home/issues/7285)

* Signieren: Beim Signieren sollte ein Fehler auftreten, wenn ein Paket zu viele Paketeinträge aufweist (>65534) – [#7248](https://github.com/NuGet/Home/issues/7248)

* „dotnet nuget push“-Codepfad sollte den neuen Anmeldeinformationsanbieter unterstützen – [#7233](https://github.com/NuGet/Home/issues/7233)

* Ausführung von Plug-Ins mit invarianter Kultur unterstützen (wie in Docker) – [#7223](https://github.com/NuGet/Home/issues/7223)

* Hinzufügen von NuGet-Quellen sollte keine Anmeldeinformationen aus „NuGet.config“ löschen – [#7200](https://github.com/NuGet/Home/issues/7200)

* Installieren einer devDependency-PackageReference sollte standardmäßig „excludeassets=compile“ ergeben – [#7084](https://github.com/NuGet/Home/issues/7084)

* Migratoroption korrigieren, sodass sie für alle Projekte angezeigt wird, und Fehlermeldung anzeigen, wenn das Projekt inkompatibel ist – [#6958](https://github.com/NuGet/Home/issues/6958)

* „dotnet add package“ sollte die durchgeführte Wiederherstellung an die Ressourcendatei senden – [#6928](https://github.com/NuGet/Home/issues/6928)

* Signieren: auf Signierung bezogene Fehlermeldungen verbessern – [#6906](https://github.com/NuGet/Home/issues/6906)

* [Testfehler][zh-TW]Zeichenfolge „Package Manager Console“ bewirkt auf Paket-Manager-Konsole keine Lokalisierung [#6381](https://github.com/NuGet/Home/issues/6381)

* Fehlermeldung „Projektinformationen nicht gefunden“ sollte in Visual Studio etwas spezifischer sein – [#5350](https://github.com/NuGet/Home/issues/5350)

* Nicht hilfreiche Fehlermeldung bei falscher Verwendung des NUSPEC-Versionstags des NuGet-Pakets – [#2714](https://github.com/NuGet/Home/issues/2714)

* DCR – Signierung: Unterstützung für NuGet-Protokoll: RepositorySignatures/4.9.0-Ressource – [#7421](https://github.com/NuGet/Home/issues/7421)

* DCR – .nupkg.metadata-Datei wird jetzt während der Paketextrahierung erstellt – enthält „content-hash“ – [#7283](https://github.com/NuGet/Home/issues/7283)

* DCR – Authenticode-Überprüfung für Plug-Ins bei der Ausführung auf Mono überspringen – [#7222](https://github.com/NuGet/Home/issues/7222)

[Liste aller in diesem Release 4.9.0 behobener Fehler](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>Zusammenfassung: Neuerungen in Version 4.9.1

* Unterstützung für das Lesen des Schreibens in die Datei „nuget.config“ über einen neuen Befehl „trusted-signers“ hinzufügen – [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

* Lizenzlinkerstellung korrigieren – [#7515](https://github.com/NuGet/Home/issues/7515)

* Fehlercoderegression zum Überprüfen von Signaturen – [#7492](https://github.com/NuGet/Home/issues/7492)

* NuGet.Build.Tasks.Pack-Paket enthält keine Lizenzinformationen – [#7379](https://github.com/NuGet/Home/issues/7379)

[Liste aller in diesem Release 4.9.1 behobenen Fehler](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a>Zusammenfassung: Neuerungen in 4.9.2

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

* VS/dotnet.exe/nuget.exe/msbuild.exe-Wiederherstellung verwendet keine Anmeldeinformationen, wenn der Quellenname ein Leerzeichen enthält – [#7517](https://github.com/NuGet/Home/issues/7517)

* LicenseAcceptanceWindow und LicenseFileWindow: Eingabehilfenfehler – [#7452](https://github.com/NuGet/Home/issues/7452)

* Korrektur von FormatException in DateTime.Parse aus DateTimeConverter – [#7539](https://github.com/NuGet/Home/issues/7539)

[Liste aller in diesem Release 4.9.2 behobenen Fehler](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a>Zusammenfassung: Neuerungen in Version 4.9.3

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a>Probleme mit „Wiederholbare Paketwiederherstellungen mithilfe einer Sperrdatei“

* Der gesperrte Modus funktioniert nicht, weil das Hash für zuvor zwischengespeicherte Pakete nicht richtig berechnet wird – [#7682](https://github.com/NuGet/Home/issues/7682)

* Die Wiederherstellung wird in eine andere Version aufgelöst als in der Datei `packages.lock.json` beschrieben – [#7667](https://github.com/NuGet/Home/issues/7667)

* „--locked-mode / RestoreLockedMode“ verursacht unechte Wiederherstellungsfehler bei Beteiligung von ProjectReferences – [#7646](https://github.com/NuGet/Home/issues/7646)

* Der MSBuild-SDK-Resolver versucht, SHA für ein SDK-Paket zu überprüfen, bei dem die Wiederherstellung bei Verwendung von „packages.lock.json“ nicht durchgeführt werden kann – [#7599](https://github.com/NuGet/Home/issues/7599)

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a>Probleme beim „Sperren Ihrer Abhängigkeiten über konfigurierbare Vertrauensrichtlinien“
* „dotnet.exe“ darf vertrauenswürdige Signaturgeber nicht auswerten, wenn signierte Pakete nicht unterstützt werden – [#7574](https://github.com/NuGet/Home/issues/7574)

* Die Reihenfolge von trustedSigners in der Konfigurationsdatei wirkt sich auf die Auswertung der Vertrauensstellung aus – [#7572](https://github.com/NuGet/Home/issues/7572)

* ISettings kann nicht implementiert werden [durch das Refactoring von Einstellungs-APIs zur Unterstützung des Vertrauensrichtlinienfeatures] – [#7614](https://github.com/NuGet/Home/issues/7614)

#### <a name="improved-debugging-experience-issues"></a>Probleme bei „Verbesserte Debugfunktionen“

* Das Symbolpaket kann für das globale .NET Core-Tool nicht veröffentlicht werden – [#7632](https://github.com/NuGet/Home/issues/7632)

#### <a name="self-contained-nuget-packages---license-issues"></a>Probleme mit „Eigenständige NuGet-Pakete – Lizenz“

* Fehler beim Erstellen eines SNUPKG-Symbolpakets bei Verwendung einer eingebetteten Lizenzdatei – [#7591](https://github.com/NuGet/Home/issues/7591)

[Liste aller in diesem Release 4.9.3 behobenen Fehler](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a>Zusammenfassung: Neuerungen in Version 4.9.4

* Sicherheitsfix: Die Berechtigungen für Dateien, die in ~/.nuget erstellt werden, sind nicht restriktiv genug ([#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)).


## <a name="known-issues"></a>Bekannte Probleme

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>„dotnet nuget push --interactive“ löst auf dem Mac eine Fehlermeldung aus. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>Problem
Das `--interactive`-Argument wird von der DotNet-CLI nicht weitergeleitet und löst die Fehlermeldung `error: Missing value for option 'interactive'` aus.

#### <a name="workaround"></a>Problemumgehung
Führen Sie jeden anderen DotNet-Befehl mit einer interaktiven Option wie `dotnet restore --interactive` aus, und authentifizieren Sie sich. Die Authentifizierung könnte dann möglicherweise vom Anmeldeinformationsanbieter zwischengespeichert werden. Führen Sie anschließend `dotnet nuget push` aus.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Von .NET Core SDK in FallbackFolders installierte Pakete werden benutzerdefiniert installiert und bestehen die Signaturüberprüfung nicht. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>Problem
Bei Verwendung von dotnet.exe 2.x zum Wiederherstellen eines Projekts mit mehreren Zielen netcoreapp 1.x und netcoreapp 2.x wird der Fallbackordner als Dateifeed behandelt. Dies bedeutet, dass NuGet bei der Wiederherstellung das Paket aus dem Fallbackordner auswählt und versucht, es im globalen Paketordner zu installieren, und die übliche Signaturüberprüfung durchführt, bei der ein Fehler auftritt.

#### <a name="workaround"></a>Problemumgehung
Deaktivieren Sie die Verwendung des Fallbackordners, indem Sie für `RestoreAdditionalProjectSources` nichts festlegen. `<RestoreAdditionalProjectSources/>` Verwenden Sie dies mit Vorsicht, da es bewirkt, dass viele Pakete von NuGet.org heruntergeladen werden, die andernfalls aus dem Fallbackordner wiederhergestellt würden.
