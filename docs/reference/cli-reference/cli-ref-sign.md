---
title: Befehl "nuget CLI-Befehl"
description: Referenz für den Befehl "nuget.exe Sign"
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622771"
---
# <a name="sign-command-nuget-cli"></a>Sign-Befehl (nuget-CLI)

**Gilt für: von** der Paket Erstellung &bullet; **unterstützte Versionen:** 4.6 und höher

Signiert alle Pakete, die mit dem ersten Argument übereinstimmen, mit einem Zertifikat. Das Zertifikat mit dem privaten Schlüssel kann aus einer Datei oder einem Zertifikat abgerufen werden, das in einem Zertifikat Speicher installiert ist, indem ein Antragsteller Name oder ein Fingerabdruck bereitgestellt wird.

> [!Note]
> Die Paket Signierung wird in .net Core, unter Mono oder auf nicht-Windows-Plattformen noch nicht unterstützt.

## <a name="usage"></a>Verwendung

```cli
nuget sign <package(s)> [options]
```

dabei `<package(s)>` ist eine oder mehrere `.nupkg` Dateien.

## <a name="options"></a>Optionen

- **`-CertificateFingerprint`**

  Gibt den SHA-1-Fingerabdruck des Zertifikats an, das zum Durchsuchen eines lokalen Zertifikat Speicher für das Zertifikat verwendet wird.

- **`-CertificatePassword`**

  Gibt ggf. das Zertifikat Kennwort an. Wenn ein Zertifikat Kenn Wort geschützt ist, aber kein Kennwort angegeben wird, fordert der Befehl zur Laufzeit zur Eingabe eines Kennworts auf, es sei denn, die `-NonInteractive` Option wird übermittelt.

- **`-CertificatePath`**

  Gibt den Dateipfad zum Zertifikat an, das zum Signieren des Pakets verwendet werden soll.

- **`-CertificateStoreLocation`**

  Gibt den Namen des X. 509-Zertifikat Speicher an, der für die Suche nach dem Zertifikat verwendet wird. Der Standardwert ist "CurrentUser", der vom aktuellen Benutzer verwendete X. 509-Zertifikat Speicher. Diese Option sollte verwendet werden, wenn das Zertifikat über die `-CertificateSubjectName` Optionen oder angegeben wird `-CertificateFingerprint` .

- **`-CertificateStoreName`**

  Gibt den Namen des X. 509-Zertifikat Speicher an, der für die Suche nach dem Zertifikat verwendet werden soll. Der Standardwert lautet "My", der X. 509-Zertifikat Speicher für persönliche Zertifikate. Diese Option sollte verwendet werden, wenn das Zertifikat über die `-CertificateSubjectName` Optionen oder angegeben wird `-CertificateFingerprint` .

- **`-CertificateSubjectName`**

  Gibt den Antragsteller Namen des Zertifikats an, das zum Durchsuchen eines lokalen Zertifikat Speicher für das Zertifikat verwendet wird.  Bei der Suche handelt es sich um einen Zeichen folgen Vergleich ohne Berücksichtigung der Groß-/Kleinschreibung unter Verwendung des angegebenen Werts, der alle Zertifikate mit dem Antragsteller Namen enthält, die diese Zeichenfolge enthalten, unabhängig von anderen  Der Zertifikat Speicher kann durch die `-CertificateStoreName` -Option und die-Option angegeben werden `-CertificateStoreLocation` .

- **`-ConfigFile`**

  Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.

- **`-ForceEnglishOutput`**

  Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.

- **`-HashAlgorithm`**

  Hash Algorithmus, der zum Signieren des Pakets verwendet werden soll. Der Standardwert ist SHA256. Mögliche Werte sind SHA256, SHA384 und SHA512.

- **`-?|-help`**

  Zeigt Hilfe Informationen für den Befehl an.

- **`-NonInteractive`**

  Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.

- **`-OutputDirectory`**

  Gibt das Verzeichnis an, in dem das signierte Paket gespeichert werden soll. Standardmäßig wird das ursprüngliche Paket durch das signierte Paket überschrieben.

- **`-Overwrite`**

  Wechseln Sie zu, um anzugeben, ob die aktuelle Signatur überschrieben werden soll. Standardmäßig schlägt der Befehl fehl, wenn das Paket bereits über eine Signatur verfügt.

- **`-Timestamper`**

  URL zu einem RFC 3161-Zeitstempel Server.

- **`-TimestampHashAlgorithm`**

  Hash Algorithmus, der vom RFC 3161-Zeitstempel Server verwendet werden soll. Der Standardwert ist SHA256.

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .

## <a name="examples"></a>Beispiele

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
