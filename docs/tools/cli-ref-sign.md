---
title: NuGet-CLI-anmelden-Befehl
description: Referenz für die nuget.exe-anmelden-Befehl
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546362"
---
# <a name="sign-command-nuget-cli"></a>Der Befehl „sign“ (NuGet CLI)

**Gilt für:** paketerstellung &bullet; **unterstützte Versionen:** 4.6 +

Signiert alle Pakete, die mit dem ersten Argument mit einem Zertifikat übereinstimmt. Das Zertifikat mit dem privaten Schlüssel kann aus einer Datei oder aus einem Zertifikat im Zertifikatspeicher installiert werden, durch die Bereitstellung einen Antragstellernamen oder Fingerabdruck abgerufen werden.

Paketsignierung ist noch in .NET Core unter Mono oder auf nicht-Windows-Plattformen nicht unterstützt.

## <a name="usage"></a>Verwendung

```cli
nuget sign <package(s)> [options]
```

wo `<package(s)>` enthält eine oder mehrere `.nupkg` Dateien.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| CertificateFingerprint | Gibt an, den SHA-1-Fingerabdruck des Zertifikats auf einen lokalen Zertifikatspeicher für das Zertifikat zu suchen. |
| CertificatePassword | Gibt das Kennwort des Zertifikats an, bei Bedarf. Wenn ein Zertifikat kennwortgeschützt ist. aber es wird kein Kennwort bereitgestellt, der Befehl wird nach einem Kennwort Fragen zur Laufzeit, es sei denn, der - nicht-interaktive Option übergeben wird. |
| CertificatePath | Gibt den Dateipfad für das Zertifikat zum Signieren des Pakets verwendet werden. |
| CertificateStoreLocation | Gibt den Namen, der die x. 509-Zertifikat-Store-Verwendung für das Zertifikat zu suchen. Der Standardwert ist "CurrentUser", die x. 509-Zertifikatspeicher des aktuellen Benutzers verwendet. Diese Option sollte verwendet werden, wenn Sie das Zertifikat über %certificatesubjectname - oder - CertificateFingerprint Optionen angeben. |
| CertificateStoreName | Gibt den Namen des x. 509-Zertifikatspeichers zu verwenden, um für das Zertifikat zu suchen. Der Standardwert ist "My", dem x. 509-Zertifikatspeicher für persönliche Zertifikate. Diese Option sollte verwendet werden, wenn Sie das Zertifikat über %certificatesubjectname - oder - CertificateFingerprint Optionen angeben. |
| %Certificatesubjectname | Gibt den Antragstellernamen des Zertifikats auf einen lokalen Zertifikatspeicher für das Zertifikat zu suchen.  Der Suche wird ein Zeichenfolgenvergleich mit dem bereitgestellten Wert, der alle Zertifikate mit dem Antragstellernamen, enthält diese Zeichenfolge enthält, ungeachtet anderer Betreffwerte für gefunden wird.  Der Zertifikatspeicher kann von - Zertifikatspeichername und CertificateStoreLocation - Optionen angegeben werden. |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| ForceEnglishOutput | Erzwingt, dass nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden. |
| Hashalgorithmus | Der Hashalgorithmus, der zum Signieren des Pakets verwendet werden. Der Standardwert SHA256. |
| Hilfe | Zeigt die Informationen für den Befehl Hilfe. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| OutputDirectory | Gibt das Verzeichnis, in dem das signierte Paket gespeichert werden soll. Standardmäßig wird das ursprüngliche Paket durch das signierte Paket überschrieben. |
| Overwrite | Wechseln Sie zu angibt, ob die aktuelle Signatur überschrieben werden soll. Standardmäßig wird der Befehl fehl, wenn das Paket bereits über eine Signatur verfügt. |
| Timestamper | URL zu einer RFC 3161-Zeitstempelserver. |
| TimestampHashAlgorithm | Der Hashalgorithmus, der vom RFC 3161-Zeitstempelserver verwendet werden. Der Standardwert SHA256. |
| Ausführlichkeit | Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*. |

## <a name="examples"></a>Beispiele

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```