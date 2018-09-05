---
title: Befehl "verify" NuGet-CLI
description: Referenz für die nuget.exe überprüfen Sie den Befehl
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545212"
---
# <a name="verify-command-nuget-cli"></a>Der Befehl „verify“ (NuGet-CLI)

**Gilt für:** Paket Verbrauch &bullet; **unterstützte Versionen:** 4.6 +

Überprüft ob ein Paket aus.

Überprüfung von signierten Paketen ist noch nicht in .NET Core unter Mono oder auf nicht-Windows-Plattformen unterstützt.

## <a name="usage"></a>Verwendung

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

wo `<package(s)>` enthält eine oder mehrere `.nupkg` Dateien.

## <a name="nuget-verify--all"></a>NuGet - alle überprüfen

Gibt an, dass alle Überprüfungen möglich auf die Pakete ausgeführt werden soll.

## <a name="nuget-verify--signatures"></a>Überprüfen von NuGet - Signaturen

Gibt an, dass die Überprüfung ausgeführt werden soll.

## <a name="options-for-verify--signatures"></a>Optionen für "verify - Signaturen"

| Option | Beschreibung |
| --- | --- |
| CertificateFingerprint | Gibt einen oder mehrere SHA-256-Zertifikat Fingerabdrücke von Zertifikaten (s), mit denen signierte Pakete signiert sein müssen. Ein SHA-256 zertifikatsfingerabdruck ist ein SHA-256-Hash des Zertifikats. Mehrere Eingaben sollten durch Semikolon getrennt. |

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| ForceEnglishOutput | Erzwingt, dass nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden. |
| Hilfe | Zeigt die Informationen für den Befehl Hilfe. |
| Ausführlichkeit | Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*. |

## <a name="examples"></a>Beispiele

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```