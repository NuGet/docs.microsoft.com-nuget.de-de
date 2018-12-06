---
title: Anmerkungen zu NuGet 4.9 RTM
description: Anmerkungen zu NuGet 4.9 einschließlich bekannter Fehler, Fehlerkorrekturen, neuer Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 3da1056f64b76f27afa662d879ef9f85868e2a07
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453772"
---
# <a name="nuget-49-release-notes"></a>Anmerkungen zu NuGet 4.9

Die NuGet 4.9.0-Funktionalität ist im Lieferumfang von [Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) enthalten.


Befehlszeilenversionen der gleichen Funktionalität sind ebenfalls verfügbar:
* NuGet.exe 4.9.x – [nuget.org/downloads](https://nuget.org/downloads)
* dotnet.exe – [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-490"></a>Zusammenfassung: Neues in 4.9.0

* Signieren: Aktivieren von ClientPolicies, um die Nutzung eines Satzes vertrauenswürdiger Autoren und Repositorys vorauszusetzen, die in „NuGet.config“ – [#6961](https://github.com/NuGet/Home/issues/6961) aufgelistet sind

* Erstellen von SNUPKG-Dateien, sodass Symbole im Paket enthalten sind – Erweitern von Push zum Verstehen des NuGet-Protokolls zum Akzeptieren der SNUPKG-Dateien für den Symbolserver – [#6878](https://github.com/NuGet/Home/issues/6878)

* NuGet-Anmeldeinformationen-Plug-In V2 – [#6642](https://github.com/NuGet/Home/issues/6642)

* Eigenständige NuGet-Pakete – Lizenz – [#4628](https://github.com/NuGet/Home/issues/4628)

* Aktivieren Sie die „GeneratePathProperty“-Metadaten einer PackageReference zum Abonnieren zum Generieren einer MSBuild-Eigenschaft pro Paket im Verzeichnis „Foo.Bar\1.0\"“ – [#6949](https://github.com/NuGet/Home/issues/6949)

* Verbessern Sie den Kundenerfolg mit NuGet-Vorgängen – [#7108](https://github.com/NuGet/Home/issues/7108)

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

* DCR – Signieren: NuGet-Protokoll unterstützen: RepositorySignatures/4.9.0-Ressource – [#7421](https://github.com/NuGet/Home/issues/7421)

* DCR – .nupkg.metadata-Datei wird jetzt während der Paketextrahierung erstellt – enthält „content-hash“ – [#7283](https://github.com/NuGet/Home/issues/7283)

* DCR – Authenticode-Überprüfung für Plug-Ins bei der Ausführung auf Mono überspringen – [#7222](https://github.com/NuGet/Home/issues/7222)

[Liste aller in diesem Release 4.9.0 behobener Fehler](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>Zusammenfassung: Neues in 4.9.1

* Unterstützung für das Lesen des Schreibens in die Datei „nuget.config“ über einen neuen Befehl „trusted-signers“ hinzufügen – [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

* Lizenzlinkerstellung korrigieren – [#7515](https://github.com/NuGet/Home/issues/7515)

* Fehlercoderegression zum Überprüfen von Signaturen – [#7492](https://github.com/NuGet/Home/issues/7492)

* NuGet.Build.Tasks.Pack-Paket enthält keine Lizenzinformationen – [#7379](https://github.com/NuGet/Home/issues/7379)

[Liste aller in diesem Release 4.9.1 behobenen Fehler](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="known-issues"></a>Bekannte Probleme

### <a name="dotnetexenugetexe-doesnt-use-credentials-when-source-name-contains-a-whitespace---7517httpsgithubcomnugethomeissues7517"></a>„dotnet.exe/nuGet.exe“ verwendet keine Anmeldeinformationen, wenn der Quellenname ein Leerzeichen enthält – [#7517](https://github.com/NuGet/Home/issues/7517)

#### <a name="issue"></a>Problem
Wenn ein Leerzeichen im Quellennamen vorhanden ist, löst „nuget.exe“ eine Fehlermeldung wie `The ' ' character, hexadecimal value 0x20, cannot be included in a name.` aus.

#### <a name="workaround"></a>Problemumgehung
Ändern Sie den Namen der Quelle so, dass er kein Leerzeichen enthält.

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>„dotnet nuget push --interactive“ löst auf dem Mac eine Fehlermeldung aus. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>Problem
Das `--interactive`-Argument wird von der DotNet-CLI nicht weitergeleitet und löst die Fehlermeldung `error: Missing value for option 'interactive'` aus.

#### <a name="workaround"></a>Problemumgehung
Führen Sie jeden anderen DotNet-Befehl mit einer interaktiven Option wie `dotnet restore --interactive` aus, und authentifizieren Sie sich. Die Authentifizierung könnte dann möglicherweise vom Anmeldeinformationsanbieter zwischengespeichert werden. Führen Sie anschließend `dotnet nuget push` aus.

### <a name="licenseacceptancewindow-and-licensefilewindow-accessibility-issues---7452httpsgithubcomnugethomeissues7452"></a>LicenseAcceptanceWindow und LicenseFileWindow: Eingabehilfenfehler – [#7452](https://github.com/NuGet/Home/issues/7452)

#### <a name="issue"></a>Problem
Bei Lizenzakzeptanzfenster und Lizenzdateifenster treten Fehler bei der Eingabehilfe mit Tastaturnavigation und Anleitung per Sprachausgabe und JAWS auf.

#### <a name="workaround"></a>Problemumgehung
Keine Problemumgehung.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Von .NET Core SDK in FallbackFolders installierte Pakete werden benutzerdefiniert installiert und bestehen die Signaturüberprüfung nicht. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>Problem
Bei Verwendung von dotnet.exe 2.x zum Wiederherstellen eines Projekts mit mehreren Zielen netcoreapp 1.x und netcoreapp 2.x wird der Fallbackordner als Dateifeed behandelt. Dies bedeutet, dass NuGet bei der Wiederherstellung das Paket aus dem Fallbackordner auswählt und versucht, es im globalen Paketordner zu installieren, und die übliche Signaturüberprüfung durchführt, bei der ein Fehler auftritt.

#### <a name="workaround"></a>Problemumgehung
Deaktivieren Sie die Verwendung des Fallbackordners, indem Sie für `RestoreAdditionalProjectSources` nichts festlegen. `<RestoreAdditionalProjectSources/>` Verwenden Sie dies mit Vorsicht, da es bewirkt, dass viele Pakete von NuGet.org heruntergeladen werden, die andernfalls aus dem Fallbackordner wiederhergestellt würden.
