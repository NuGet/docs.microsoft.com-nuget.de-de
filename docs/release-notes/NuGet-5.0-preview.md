---
title: Anmerkungen zu NuGet 5.0-preview
description: Anmerkungen zu NuGet-5.0-Preview, einschließlich bekannter Probleme, Fehlerbehebungen, neuen Features und DCRs.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: ed3294f88ff99d5e26f630bdbca03aa8446b6e7f
ms.sourcegitcommit: 0cb4c9853cde3647291062eadee2298dd273311e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2019
ms.locfileid: "55084936"
---
# <a name="nuget-50-preview-release-notes"></a>Anmerkungen zu NuGet 5.0 Preview

## <a name="summary-whats-new-in-50-preview-2"></a>Zusammenfassung: Neuerungen in 5.0 Preview 2

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

#### <a name="bugs"></a>Fehler:

* Visual Studio 16.0 NuGet UI enthält unlesbare Registerkarten aufgrund von Problemen mit Farbe - [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & NuGet.Clients Dateien "License.txt" Klarstellung - [#7629](https://github.com/NuGet/Home/issues/7629)

* Wiederherstellung listet globalen Paketordner unnötigerweise beim Versuch, um zu bestimmen, Typ: [#7596](https://github.com/NuGet/Home/issues/7596)

* Fehler von der Erzwingung der Sperre-Datei sollte angezeigt werden in der Fehlerliste (Fenster) - [#7429](https://github.com/NuGet/Home/issues/7429)

* Beheben von Problemen mit NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)

* Anpassung an MSBuild aktualisieren sie den Installationsort.  - [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack muss eine entwicklungsabhängigkeit - [#7249](https://github.com/NuGet/Home/issues/7249)

* Hinzufügen von Pack Erweiterungspunkt zum Einschließen von Debugsymbole - [#7234](https://github.com/NuGet/Home/issues/7234)

* Dotnet-Pack beibehalten soll Abhängigkeit Versionsbereich in NuGet-Paket erstellt. (auch, wenn die unverankerte Version verwendet wird) - [#7232](https://github.com/NuGet/Home/issues/7232)

* Dotnet-Restore auf authentifizierte Quelle schlägt fehl, wenn es sich bei auf Benutzerebene Konfiguration auch-Quelle – hat [#7209](https://github.com/NuGet/Home/issues/7209)

* Pack sollten nicht nur BuildActions für Inhaltsdateien - [#7155](https://github.com/NuGet/Home/issues/7155)

* Verwenden eine "ProjectReference" AssetTargetFallback erfolgreich ausgeführt werden müssen, sollte eine Warnung ausgeben. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Deadlock aufgrund von Threadingprobleme beim Aufrufen von in CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)

* Dotnet add-Paket nicht die Anmeldeinformationen aus der globalen Konfiguration verwendet, für eine Datenquelle angegeben, in der lokalen Konfiguration - [#6935](https://github.com/NuGet/Home/issues/6935)

* Probleme mit MEF wird Threading für asynchrone Codepfade - aufgerufen [#6771](https://github.com/NuGet/Home/issues/6771)

* Anmeldung: Fehler zweimal und ohne Aufrufliste - [#6455](https://github.com/NuGet/Home/issues/6455)

* Installieren eines signierten Pakets mit nicht vertrauenswürdigen Signaturzertifikat sollte angezeigt werden Fehler: [#6318](https://github.com/NuGet/Home/issues/6318)

* NuGet restore noops sind nicht ordnungsgemäß, beim Verzeichnis "Obj" - 2-Projekten gemeinsam [#6114](https://github.com/NuGet/Home/issues/6114)

* PAT mit Dotnet-Restore unter Linux von Paketen aus authentifizierte Feeds - können keine [#5651](https://github.com/NuGet/Home/issues/5651)

* Dotnet-Restore versagt, wenn deaktivierte auf den gesamten Computer feed - [#5410](https://github.com/NuGet/Home/issues/5410)

#### <a name="dcrs"></a>DCRs

* NuGet-5.0-Assemblys in .NET 4.7.2 (über die Änderung der TFM) - erfordern [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData aus NuGet.Packaging sollte ein öffentlicher Typ sein. Aktualisieren Sie die Lizenzmetadaten aus Spdx erfasst. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Entfernen Sie veraltete APIs für Einstellungen – [#7294](https://github.com/NuGet/Home/issues/7294)

* Problemumgehung Wiederherstellung Timeouts auf Systemen mit 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet NTLM-Authentifizierung bevorzugt, auch wenn die Anmeldeinformationen vorhanden sind, in der Datei "NuGet.config" – Filter-Auth-Typen zur Eingabe von Anmeldeinformationen - Option "Config" hinzufügen [#5286](https://github.com/NuGet/Home/issues/5286)

* Aktivieren Sie EmbedInteropTypes für "packagereference" (übereinstimmende Datei "Packages.config"-Funktion) - [#2365](https://github.com/NuGet/Home/issues/2365)

[Liste aller Probleme, die in dieser Version 5.0.0-preview2 behoben](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")


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
