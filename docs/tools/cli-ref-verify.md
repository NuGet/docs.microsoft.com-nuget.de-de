---
title: Befehl "verify" NuGet CLI
description: Überprüfen von Verweis für die nuget.exe-Befehl
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c80334104f7d8b2ccbf16ea2c11dc37b39408eeb
ms.sourcegitcommit: c8485dc61469511485367d2067b97d6f74b49f6e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/23/2018
---
# <a name="verify-command-nuget-cli"></a>Der Befehl „verify“ (NuGet-CLI)

**Gilt für:** Verpacken Sie Verbrauch &bullet; **unterstützte Versionen:** 4.6 +

Überprüft ein Paket an.

Überprüfung von signierten Paketen ist noch nicht im .NET-Kern, unter Mono sowie auf nicht-Windows-Plattformen unterstützt.

## <a name="usage"></a>Verwendung

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

wobei `<package(s)>` enthält eine oder mehrere `.nupkg` Dateien.

## <a name="nuget-verify--all"></a>NuGet überprüfen - alle

Gibt an, dass alle möglichen Überprüfungen auf die Pakete ausgeführt werden dürfen.

## <a name="nuget-verify--signatures"></a>NuGet - Signaturen überprüfen

Gibt an, dass die Überprüfung der Signatur Paket ausgeführt werden soll.

## <a name="options-for-verify--signatures"></a>Optionen für "verify - Signaturen"

| Option | Beschreibung |
| --- | --- |
| CertificateFingerprint | Gibt einen oder mehrere SHA-256-Zertifikat Fingerabdrücke von Zertifikaten (s), mit denen signierte Pakete signiert werden müssen. Ein SHA-256 zertifikatsfingerabdruck ist ein SHA-256-Hash des Zertifikats. Mehrere Eingaben sollten durch Semikolons getrennt werden. |

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| ForceEnglishOutput | Erzwingt, dass nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*. |

## <a name="examples"></a>Beispiele

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```