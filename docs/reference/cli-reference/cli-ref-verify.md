---
title: Befehl "nuget CLI verify"
description: Referenz für den Befehl "nuget. exe verify"
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327497"
---
# <a name="verify-command-nuget-cli"></a>Der Befehl „verify“ (NuGet-CLI)

**Gilt für:** &bullet; **unterstützte Versionen** : 4.6 und höher

Überprüft ein Paket.

Die Überprüfung von signierten Paketen wird in .net Core, unter Mono oder auf nicht-Windows-Plattformen noch nicht unterstützt.

## <a name="usage"></a>Verwendung

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

Dabei ist eine oder mehrere `.nupkg`Dateien. `<package(s)>`

## <a name="nuget-verify--all"></a>nuget-Überprüfung-alle

Gibt an, dass alle Überprüfungen, die für die Pakete ausgeführt werden können, ausgeführt werden sollen.

## <a name="nuget-verify--signatures"></a>nuget-Überprüfung-Signaturen

Gibt an, dass die Überprüfung der Paket Signatur ausgeführt werden soll.

## <a name="options-for-verify--signatures"></a>Optionen für "Verify-Signaturen"

| Option | Beschreibung |
| --- | --- |
| CertificateFingerprint | Gibt einen oder mehrere SHA-256-Zertifikat Fingerabdrücke von Zertifikaten an, mit denen signierte Pakete signiert werden müssen. Ein Zertifikat SHA-256-Fingerabdruck ist ein SHA-256-Hash des Zertifikats. Mehrere Eingaben sollten durch Semikolon getrennt sein. |

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.|
| ForceEnglishOutput | Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird. |
| Help | Zeigt Hilfe Informationen für den Befehl an. |
| Verbosity | Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*. |

## <a name="examples"></a>Beispiele

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```