---
title: Anmerkungen zu NuGet 4.8 RTM
description: Anmerkungen zu NuGet 4.8.1, einschließlich bekannter Fehler, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: e6f6d9f703dd4761236d166f3772618c100aca09
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813766"
---
# <a name="nuget-48-release-notes"></a>Anmerkungen zu NuGet 4.8

Die NuGet 4.8-Funktionalität ist im Lieferumfang von [Visual Studio 2017 15.8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) enthalten.


Befehlszeilenversionen der gleichen Funktionalität sind ebenfalls verfügbar:
* NuGet.exe 4.8: [NuGet.org/Downloads](https://nuget.org/downloads)
* DotNet.exe: [.NET Core SDK 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-480"></a>Zusammenfassung: Neuerungen in Version 4.8.0
* NuGet.exe unterstützt jetzt lange Dateinamen unter Windows 10: [#6937](https://github.com/NuGet/Home/issues/6937)
* Authentifizierungs-Plug-Ins funktionieren nun übergreifend in MsBuild, DotNet.exe, NuGet.exe und Visual Studio, auch plattformübergreifend. Die erste Generation des Authentifizierung-Plug-Ins wurde in MsBuild und DotNet.exe nicht unterstützt. Hinweis: In Vorschaubuilds von VS 2017 15.9 ist ein VSTS-Authentifizierungs-Plug-In enthalten. [#6486](https://github.com/NuGet/Home/issues/6486)
* Der SDK-Konfliktlöser von MsBuild wird jetzt als Teil von NuGet erstellt und mit den NuGet-Tools für VS installiert. Dadurch wird Asynchronizität von Versionen vermieden. [#6799](https://github.com/NuGet/Home/issues/6799)
* PackageReference unterstützt jetzt DevelopmentDependency-Metadaten: [#4125](https://github.com/NuGet/Home/issues/4125)

## <a name="summary-whats-new-in-482"></a>Zusammenfassung: Neuerungen in Version 4.8.2

* Sicherheitsfix: Die Berechtigungen für Dateien, die in ~/.nuget erstellt werden, sind nicht restriktiv genug ([#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)).

## <a name="known-issues"></a>Bekannte Probleme
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a>Das Installieren von signierten Paketen auf einem CI-Computer oder in einer Offlineumgebung dauert länger als gewöhnlich

#### <a name="issue"></a>Problem
Wenn der Computer eingeschränkten Internetzugriff hat (wie etwa ein Buildcomputer in einem CI/CD-Szenario), wird beim Installieren/Wiederherstellen von signierten NuGet-Paketen eine Warnung ([NU3028](../reference/errors-and-warnings/nu3028.md)) angezeigt, da die Sperrserver nicht erreichbar sind. Dabei handelt es sich um das erwartete Verhalten. In manchen Fällen kann dies jedoch unbeabsichtigte Konsequenzen haben, etwa die, dass das Installieren/Wiederherstellen von Paketen länger als gewöhnlich dauert.

#### <a name="workaround"></a>Problemumgehung
Führen Sie ein Update auf Visual Studio 15.8.4 und NuGet.exe 4.8.1 aus, in denen wir eine Umgebungsvariable zum Umschalten des Sperrprüfmodus eingeführt haben.
Durch Festlegen der `NUGET_CERT_REVOCATION_MODE`-Umgebungsvariablen auf `offline` wird NuGet gezwungen, den Sperrstatus der Zertifikate nur anhand der zwischengespeicherten Zertifikatsperrliste zu überprüfen, und NuGet versucht dann nicht, Sperrserver zu erreichen. Wenn der Sperrprüfmodus auf `offline` eingestellt ist, wird die Warnung zu einer Information heruntergestuft.

> [!Warning]
> Es empfiehlt sich nicht, den Sperrprüfmodus unter normalen Umständen auf Offline einzustellen. Das würde dazu führen, dass NuGet die Onlinesperrprüfung auslässt und nur eine Offlinesperrprüfung anhand der zwischengespeicherten Zertifikatsperrliste durchführt, die möglicherweise veraltet ist. Das bedeutet, dass Pakete, deren Signaturzertifikat gesperrt wurde, dann trotzdem installiert/wiederhergestellt werden. Im Normalfall hätten die Pakete die Sperrprüfung nicht bestanden und wären nicht installiert worden.

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>Die Option `Migrate packages.config to PackageReference...` ist nicht im Kontextmenü (Rechtsklick) verfügbar.

#### <a name="issue"></a>Problem

Wenn ein Projekt zum ersten Mal geöffnet wird, kann es sein, dass NuGet erst mit dem ersten NuGet-Vorgang gestartet wird. Deshalb wird die Option zur Migration nicht im Kontextmenü (Rechtsklick) von `packages.config` oder `References` angezeigt.

#### <a name="workaround"></a>Problemumgehung

Führen Sie eine der folgenden NuGet-Aktionen durch:
* Öffnen Sie die Benutzeroberfläche des Paket-Managers. Klicken Sie mit der rechten Maustaste auf `References`, und wählen Sie `Manage NuGet Packages...`.
* Öffnen Sie die Paket-Manager-Konsole. Klicken Sie unter `Tools > NuGet Package Manager` auf `Package Manager Console`.
* Stellen Sie NuGet-Pakete wieder her. Klicken Sie dazu im Projektmappen-Explorer mit der rechten Maustaste auf den Projektmappenknoten, und wählen Sie `Restore NuGet Packages` aus.
* Erstellen Sie ein Projekt. Dadurch wird die Wiederherstellung von NuGet auch ausgelöst.

Jetzt sollten Sie die Option zur Migration sehen. Beachten Sie, dass diese Option für ASP.NET- und C++-Projekte nicht unterstützt und auch nach dem Durchführen dieser Schritte nicht angezeigt wird.
Hinweis: Dies wurde in VS 2017 15.9, Vorschau 3, behoben.

## <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

### <a name="bugs"></a>Fehler
#### <a name="signing"></a>Signierung
* Signierung: Installieren von signierten Paketen in einer Offlineumgebung [#7008](https://github.com/NuGet/Home/issues/7008): In 4.8.1 behoben
* Signierung: Fehlerhafte URL-Überprüfung: [#7174](https://github.com/NuGet/Home/issues/7174)
* Signierung: Überprüfung der Paketintegrität in RepositorySignatureVerifier, wenn ein Paket vom Repository gegensigniert ist: [#6926](https://github.com/NuGet/Home/issues/6926)
* „Fehler bei der Paketintegritätsprüfung.“ sollte eine Paket-ID (und einen Fehlercode) in der Nachricht enthalten: [#6944](https://github.com/NuGet/Home/issues/6944)
* Eine vom Repository signierte Paketüberprüfung lässt mit einem anderen Zertifikat signierte Pakete zu: [#6884](https://github.com/NuGet/Home/issues/6884)
* NuGet – Signierung: Die Zeitstempel-URL kann nicht mit „https://“ beginnen? - [#6871](https://github.com/NuGet/Home/issues/6871)
* Keine NullRef im NuSpec-Paketszenario, außerdem verbesserte Optionen: [#6866](https://github.com/NuGet/Home/issues/6866)
* Arbeitsspeicher ist beim Aktualisieren der Signaturgeberinformationen ungültig, wenn der Gegensignatur ein Zeitstempel hinzugefügt wird: [#6840](https://github.com/NuGet/Home/issues/6840)
* Signierung: CTL-Ausnahmen entfernen: [#6794](https://github.com/NuGet/Home/issues/6794)
* Signierung: ContentUrl muss HTTPS sein: [#6777](https://github.com/NuGet/Home/issues/6777)
* Signierung:  SignedPackageVerifierSettings.VSClientDefaultPolicy wird nicht verwendet: [#6601](https://github.com/NuGet/Home/issues/6601)


#### <a name="pack"></a>Verpacken
* Wiederherstellung und Erstellen sollten bei der Verwendung von dotnet.exe zum Verpacken von nuspec nicht erforderlich sein: [#6866](https://github.com/NuGet/Home/issues/6866)
* Zulassen von leeren Ersetzungstoken in NuspecProperties: [#6722](https://github.com/NuGet/Home/issues/6722)
* PackTask löst eine NullReferenceException aus, wenn NuspecProperties angegeben ist: [#4649](https://github.com/NuGet/Home/issues/4649)

#### <a name="accessibility"></a>Zugriff
* [Barrierefreiheit] Zeichenfolge ‚Vorabrelease‘ unter der Verpacken-Schaltfläche wird von ihrer Paketbeschreibung in der PM-Benutzeroberfläche verdeckt: [#4504](https://github.com/NuGet/Home/issues/4504)
* [Barrierefreiheit] Die Paketquellen-Dropdownliste und die Schaltfläche „Einstellungen“ sind beim Auswählen von „Microsoft Visual Studio-Offlinepakete“ in der PM-Benutzeroberfläche abgeschnitten: [#4502](https://github.com/NuGet/Home/issues/4502)

#### <a name="powershell-management-console-pmc"></a>PowerShell-Verwaltungskonsole (PowerShell Management Console, PMC)
* `Update-Package` ignoriert den PackageReference-Versionsbereich: [#6775](https://github.com/NuGet/Home/issues/6775)
* `Update-Package -reinstall` Problem mit der Breite der Projektmappe: [#3127](https://github.com/NuGet/Home/issues/3127)
* `Update-Package [packagename] -reinstall` installiert alle Pakete anstatt nur des genannten Pakets neu: [#737](https://github.com/NuGet/Home/issues/737)
* Update in nicht gelistetes NuGet-Paket aus der Paket-Manager-Konsole möglich: [#4553](https://github.com/NuGet/Home/issues/4553)

#### <a name="misc"></a>Sonstiges
* Zum Beheben von `NuGet update self` sollte NuGet.Commandline nupkg nicht semver2.0 lauten: [#7116](https://github.com/NuGet/Home/issues/7116)
* Verbesserung der Benutzererfahrung bei NU1107-Installationsfehlern: [#7107](https://github.com/NuGet/Home/issues/7107)
* Die Serialisierung von GetAuthenticationCredentialRequest ist fehlerhaft: [#6983](https://github.com/NuGet/Home/issues/6983)
* Fehler beim Laden von NuGet Visual Studio AsyncPackage, wenn die Initialisierung aus dem Thread der Benutzeroberfläche erfolgte: [#6976](https://github.com/NuGet/Home/issues/6976)
* Die Wiederherstellung meldet irreführende Fehler, aus denen hervorgeht, dass project.json erforderlich ist: [#6959](https://github.com/NuGet/Home/issues/6959)
* Benutzeroberfläche des Paket-Managers: Bei Änderungen der Vorschau ist die OK-Schaltfläche nicht automatisch über die Tastatur bedienbar: [#6893](https://github.com/NuGet/Home/issues/6893)
* RestoreSources werden für ein Projekt mit p2p-Verweisen ignoriert: [#6776](https://github.com/NuGet/Home/issues/6776)
* Beim Erstellen eines Komponententestprojekts mithilfe der .NET Framework-Vorlage wird ein älteres Projektmodell mit packages.config geöffnet: [#6736](https://github.com/NuGet/Home/issues/6736)
* Projektverweise können Paketabhängigkeit überschreiben: [#6536](https://github.com/NuGet/Home/issues/6536)
* NoDefaultExcludes werden in MSBuild-Aufgabe verfügbar gemacht: [#6450](https://github.com/NuGet/Home/issues/6450)
* Die Statusmeldung für "Alle NuGet-Caches leeren" können beim Ändern der Fenstergröße ausgeblendet werden: [#5938](https://github.com/NuGet/Home/issues/5938)


[Liste aller in diesem Release behobener Fehler](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")
