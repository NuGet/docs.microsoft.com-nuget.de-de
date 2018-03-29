---
title: NuGet-CLI-Anmelde-Befehl | Microsoft Docs
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenz für den nuget.exe Anmelde-Befehl
keywords: NuGet-Anmelde-Verweis, Anmelde-Befehl
ms.reviewer:
- karann
- rmpablos
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9c83e5abae0e70cdc62917861c1febfce4f792c7
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="sign-command-nuget-cli"></a>Anmelde-Befehl (NuGet CLI)

**Gilt für:** Erstellen von Paketen &bullet; **unterstützte Versionen:** 4.6 +

Signiert alle Pakete, die mit dem ersten Argument mit einem Zertifikat übereinstimmt. Das Zertifikat mit dem privaten Schlüssel kann aus einer Datei oder aus einem Zertifikat in keinem Zertifikatspeicher installiert werden, indem einen Antragstellernamen oder Fingerabdruck eines abgerufen werden.

Paketsignierung ist noch nicht unter Mono oder auf nicht-Windows-Plattformen unterstützt.

## <a name="usage"></a>Verwendung

```cli
nuget sign <package(s)> [options]
```

wobei `<package(s)>` enthält eine oder mehrere `.nupkg` Dateien.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| CertificateFingerprint | Gibt den SHA-1-Fingerabdruck des Zertifikats verwendet, um einen lokalen Zertifikatspeicher für das Zertifikat zu suchen. |
| CertificatePassword | Gibt das Kennwort des Zertifikats an, bei Bedarf. Wenn ein Zertifikat kennwortgeschützt ist, jedoch kein Kennwort bereitgestellt wird, der Befehl wird nach einem Kennwort Fragen zur Laufzeit, es sei denn, die - Option nicht interaktiven übergeben wird. |
| CertificatePath | Gibt den Dateipfad für das Zertifikat zum Signieren des Pakets verwendet werden. |
| CertificateStoreLocation | Gibt den Namen der dem x. 509-Zertifikat Store verwenden, für das Zertifikat gesucht werden soll. Der Standardwert ist "CurrentUser", die vom aktuellen Benutzer verwendete x. 509-Zertifikatspeicher. Diese Option sollte verwendet werden, wenn Sie das Zertifikat über - %certificatesubjectname oder CertificateFingerprint - Optionen angeben. |
| CertificateStoreName | Gibt den Namen des x. 509-Zertifikatspeichers zu verwenden, um für das Zertifikat zu suchen. Der Standardwert ist "My", dem x. 509-Zertifikatspeicher für persönliche Zertifikate. Diese Option sollte verwendet werden, wenn Sie das Zertifikat über - %certificatesubjectname oder CertificateFingerprint - Optionen angeben. |
| CertificateSubjectName | Gibt den Antragstellernamen des Zertifikats verwendet, um einen lokalen Zertifikatspeicher für das Zertifikat zu suchen.  Die Suche wird ein Zeichenfolgenvergleich mit dem bereitgestellten Wert, der alle Zertifikate mit dem Antragstellernamen, enthält die Zeichenfolge, unabhängig von der anderen Werte für den Antragsteller findet.  Der Zertifikatspeicher kann durch - Zertifikatspeichername und CertificateStoreLocation - Optionen angegeben werden. |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| ForceEnglishOutput | Erzwingt, dass nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| HashAlgorithm | Der Hashalgorithmus zum Signieren des Pakets verwendet werden. Der Standardwert ist SHA256. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| OutputDirectory | Gibt das Verzeichnis, in dem das signierte Paket gespeichert werden soll. Standardmäßig wird das ursprüngliche Paket durch das signierte Paket überschrieben. |
| Overwrite | Schalter, um anzugeben, ob die aktuelle Signatur überschrieben werden soll. Standardmäßig wird der Befehl fehl, wenn das Paket bereits über eine Signatur verfügt. |
| Timestamper | Die URL zu einer RFC 3161-Zeitstempelserver. |
| TimestampHashAlgorithm | Der Hashalgorithmus, der vom RFC 3161-Zeitstempelserver verwendet werden. Der Standardwert ist SHA256. |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*. |

## <a name="examples"></a>Beispiele

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```