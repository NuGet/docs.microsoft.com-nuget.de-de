---
title: Anmerkungen zu NuGet 4.7 RTM
description: Anmerkungen zu NuGet 4.7.0, einschließlich bekannter Fehler, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 0c3c0380fe6efb3c58124ca5ba8bc1306a433340
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611349"
---
# <a name="nuget-47-release-notes"></a>Versionshinweise zu NuGet 4.7

[NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe) ist im Lieferumfang von [Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) enthalten.

## <a name="summary-whats-new-in-470"></a>Zusammenfassung: Neuerungen in Version 4.7.0

* Die Paketsignierung wurde angepasst, sodass nun [von Repositorys signierte Pakete](https://github.com/NuGet/Home/wiki/Repository-Signatures) möglich sind.

* In Visual Studio 15.7 haben wir stattdessen eine Funktion zum [Migrieren vorhandener Projekte mit packages.config-Format zum Verwenden von PackageReference](https://docs.microsoft.com/nuget/consume-packages/migrate-packages-config-to-package-reference) eingeführt.

## <a name="summary-whats-new-in-472"></a>Zusammenfassung: Neuerungen in Version 4.7.2

* Sicherheitsfix: Die Berechtigungen für Dateien, die in ~/.nuget erstellt werden, sind nicht restriktiv genug ([#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)).

## <a name="summary-whats-new-in-473"></a>Zusammenfassung: Neuerungen in Version 4.7.3

* Sicherheitsfix: Dateien innerhalb von NUPKGs können einen relativen Pfad über dem NUPKG-Verzeichnis besitzen ([#7906](https://github.com/NuGet/Home/issues/7906)).

## <a name="known-issues"></a>Bekannte Probleme

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

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Probleme mit .NET Standard 2.0 mit .NET Framework und NuGet

.NET Standard und die dazugehörigen Tools wurden so konzipiert, dass Projekte, die für .NET Framework 4.6.1 erstellt wurden, NuGet-Pakete und -Projekte verarbeiten können, die für .NET Standard 2.0 oder früher erstellt wurden. In [diesem Dokument](https://github.com/dotnet/standard/issues/481) werden die Probleme, die in diesem Szenario auftreten können, der Plan für die Behebung dieser Probleme und Problemumgehungen zusammengefasst, die Sie nach aktuellem Stand für die Tools bereitstellen können.

## <a name="top-issues-fixed-in-this-release"></a>In diesem Release behobene Hauptprobleme

### <a name="bugs"></a>Fehler

* In .NET Core-Projektsystemen (neue Regression) kommt es für NuGet zu einem Deadlock. - [#6733](https://github.com/NuGet/Home/issues/6733)
* Packen: PackagePath wird inkorrekt erstellt, wenn TfmSpecificPackageFile mit Platzhalterpfaden verwendet wird ([#6726](https://github.com/NuGet/Home/issues/6726)).
* Packen: Ein Web-API-Projekt kann Pakete nur dann erstellen, wenn ispackagable explizit festgelegt wird. - [#6156](https://github.com/NuGet/Home/issues/6156)
* Die VS-Benutzeroberfläche und PMC zeigen neue Pakete erst nach 30 Minuten an („nuget.exe“ zeigt sie umgehend an) – [#6657](https://github.com/NuGet/Home/issues/6657).
* Signierung:  SignatureUtility.GetCertificateChain(...) überprüft nicht alle Kettenstatus ([#6565](https://github.com/NuGet/Home/issues/6565)).
* Signieren: Verbesserungsbedarf bei der Behandlung von GeneralizedTime (DER) – [#6564](https://github.com/NuGet/Home/issues/6564).
* Signierung: VS zeigt keinen NU3002-Fehler an, wenn ein manipuliertes Paket installiert wird ([#6337](https://github.com/NuGet/Home/issues/6337)).
* „lockFile.GetLibrary“ beachtet die Groß- und Kleinschreibung – [#6500](https://github.com/NuGet/Home/issues/6500).
* Das Installieren/Aktualisieren von Wiederherstellungscode und das Wiederherstellen von Codepfaden sind nicht konsistent – [#3471](https://github.com/NuGet/Home/issues/3471).
* Projektmappen-Paket-Manager (Version ComboBox) kann Trennlinie über Tastatur auswählen – [#2606](https://github.com/NuGet/Home/issues/2606).
* Der Dienstindex für die Source konnte nicht geladen werden: `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException: Der Antwortstatuscode zeigt keinen Erfolg an: (403) Unzulässig ([#2530](https://github.com/NuGet/Home/issues/2530))

### <a name="dcrs"></a>DCRs

* Ausgeben des X-NuGet-Sitzungs-ID-Headers zur Korrelierung für mehrere Anforderungen (Featurevorschlag) – [#5330](https://github.com/NuGet/Home/issues/5330).
* Bieten einer Möglichkeit zum Warten auf laufende Wiederherstellungsvorgänge, die in Visual Studio über IVs-APIs ausgeführt werden. - [#6029](https://github.com/NuGet/Home/issues/6029)
* „nuget.exe“: NoServiceEndpoint verhindert das Anfügen eines Dienst-URL-Suffixes – [#6586](https://github.com/NuGet/Home/issues/6586).
* Hinzufügen von Commithash zu Versionsinformationen – [#6492](https://github.com/NuGet/Home/issues/6492).
* Signieren: Ermöglichen, dass Repositorysignatur/Gegensignatur entfernt werden kann – [#6646](https://github.com/NuGet/Home/issues/6646).
* Signierung:  API zum Entfernen der Repositorysignatur/Gegensignatur ([#6589](https://github.com/NuGet/Home/issues/6589)).
* Protokollieren zusätzlicher Informationen in VS – [#6527](https://github.com/NuGet/Home/issues/6527).
* Filtern von /tools nur in TFM und RID, damit die Einstellungs-XML in den Ordner /tools eingefügt werden kann – [#6197](https://github.com/NuGet/Home/issues/6197).
* Warnen, wenn der Befehl „Pack“ Dateien ausschließt, die mit „.“ beginnen  - [#3308](https://github.com/NuGet/Home/issues/3308)

[Liste aller in diesem Release behobener Fehler](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
