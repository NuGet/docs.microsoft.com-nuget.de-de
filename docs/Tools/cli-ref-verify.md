---
title: Befehl "verify" NuGet CLI | Microsoft Docs
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Überprüfen von Verweis für die nuget.exe-Befehl"
keywords: NuGet sicher Verweis und Befehl
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 096c79670267d9b602dd6ad30640e832441c31c5
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="verify-command-nuget-cli"></a>Vergewissern Sie sich Befehl (NuGet CLI)

**Gilt für:** Verpacken Sie Verbrauch &bullet; **unterstützte Versionen:** 4.6 +

Überprüft ein Paket an.

## <a name="usage"></a>Verwendung

```cli
nuget verify <package(s)> [options]
```

wobei `<package(s)>` enthält eine oder mehrere `.nupkg` Dateien.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| Alle | Gibt an, dass alle möglichen Überprüfungen auf die Pakete ausgeführt werden dürfen. |
| CertificateFingerprint | Gibt einen oder mehrere SHA-256-Zertifikat Fingerabdrücke von Zertifikaten (s), mit denen signierte Pakete signiert werden müssen. Ein SHA-256 zertifikatsfingerabdruck ist ein SHA-256-Hash des Zertifikats. Mehrere Eingaben sollten durch Semikolons getrennt werden. |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| ForceEnglishOutput | Erzwingt, dass nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Signaturen | Gibt an, dass die Überprüfung der Signatur Paket ausgeführt werden soll. |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*. |

## <a name="examples"></a>Beispiele

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```