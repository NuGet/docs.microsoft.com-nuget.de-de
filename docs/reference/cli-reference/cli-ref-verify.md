---
title: Befehl "nuget CLI verify"
description: Referenz für den Befehl "nuget.exe verify"
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7ce08f11195437e94bfe69883ff525e9ad3a73f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238139"
---
# <a name="verify-command-nuget-cli"></a>Befehl "überprüfen" (nuget-CLI)

**Gilt für:** &bullet; **unterstützte Versionen** von Paket Verbrauch: 4.6 und höher

Überprüft ein Paket.

Die Überprüfung von signierten Paketen wird unter Mono noch nicht unterstützt.

## <a name="usage"></a>Verbrauch

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

dabei `<package(s)>` ist eine oder mehrere `.nupkg` Dateien.

## <a name="nuget-verify--all"></a>nuget-Überprüfung-alle

Hiermit wird angegeben, dass alle Überprüfungen für die Pakete ausgeführt werden sollen, die möglich sind.

## <a name="nuget-verify--signatures"></a>nuget-Überprüfung-Signaturen

Gibt an, dass die Überprüfung der Paket Signatur ausgeführt werden soll.

## <a name="options-for-verify--signatures"></a>Optionen für "Verify-Signaturen"

- **`-CertificateFingerprint`**

  Gibt einen oder mehrere SHA-256-Zertifikat Fingerabdrücke von Zertifikaten an, mit denen signierte Pakete signiert werden müssen. Ein Zertifikat SHA-256-Fingerabdruck ist ein SHA-256-Hash des Zertifikats. Mehrere Eingaben sollten durch Semikolon getrennt sein.

## <a name="options"></a>Optionen

- **`-ConfigFile`**

  Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.

- **`-ForceEnglishOutput`**

  Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.

- **`-?|-help`**

  Zeigt Hilfe Informationen für den Befehl an.

- **`-NonInteractive`**

  Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .

## <a name="examples"></a>Beispiele

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```