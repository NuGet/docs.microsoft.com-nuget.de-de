---
title: Befehl "nuget CLI-Befehl"
description: Referenz für den Befehl "nuget. exe Sign"
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327587"
---
# <a name="sign-command-nuget-cli"></a>Der Befehl „sign“ (NuGet CLI)

**Gilt für: von** der &bullet; Paket Erstellung **unterstützte Versionen:** 4.6 und höher

Signiert alle Pakete, die mit dem ersten Argument übereinstimmen, mit einem Zertifikat. Das Zertifikat mit dem privaten Schlüssel kann aus einer Datei oder einem Zertifikat abgerufen werden, das in einem Zertifikat Speicher installiert ist, indem ein Antragsteller Name oder ein Fingerabdruck bereitgestellt wird.

Die Paket Signierung wird in .net Core, unter Mono oder auf nicht-Windows-Plattformen noch nicht unterstützt.

## <a name="usage"></a>Verwendung

```cli
nuget sign <package(s)> [options]
```

Dabei ist eine oder mehrere `.nupkg`Dateien. `<package(s)>`

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| CertificateFingerprint | Gibt den SHA-1-Fingerabdruck des Zertifikats an, das zum Durchsuchen eines lokalen Zertifikat Speicher für das Zertifikat verwendet wird. |
| CertificatePassword | Gibt ggf. das Zertifikat Kennwort an. Wenn ein Zertifikat Kenn Wort geschützt ist, aber kein Kennwort angegeben wird, fordert der Befehl zur Laufzeit zur Eingabe eines Kennworts auf, es sei denn, die Option "-noninteractive" wird übermittelt. |
| CertificatePath | Gibt den Dateipfad zum Zertifikat an, das zum Signieren des Pakets verwendet werden soll. |
| CertificateStoreLocation | Gibt den Namen des X. 509-Zertifikat Speicher an, der für die Suche nach dem Zertifikat verwendet wird. Der Standardwert ist "CurrentUser", der vom aktuellen Benutzer verwendete X. 509-Zertifikat Speicher. Diese Option sollte verwendet werden, wenn Sie das Zertifikat über die Optionen "-certificatesubjectname" oder "-certificatefingerabdruck" angeben. |
| CertificateStoreName | Gibt den Namen des X. 509-Zertifikat Speicher an, der für die Suche nach dem Zertifikat verwendet werden soll. Der Standardwert lautet "My", der X. 509-Zertifikat Speicher für persönliche Zertifikate. Diese Option sollte verwendet werden, wenn Sie das Zertifikat über die Optionen "-certificatesubjectname" oder "-certificatefingerabdruck" angeben. |
| CertificateSubjectName | Gibt den Antragsteller Namen des Zertifikats an, das zum Durchsuchen eines lokalen Zertifikat Speicher für das Zertifikat verwendet wird.  Bei der Suche handelt es sich um einen Zeichen folgen Vergleich ohne Berücksichtigung der Groß-/Kleinschreibung unter Verwendung des angegebenen Werts, der alle Zertifikate mit dem Antragsteller Namen enthält, die diese Zeichenfolge enthalten, unabhängig von anderen  Der Zertifikat Speicher kann durch die Optionen-certifikatestorename und-certifikatestoreloation angegeben werden. |
| ConfigFile | Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.|
| ForceEnglishOutput | Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird. |
| HashAlgorithm | Hash Algorithmus, der zum Signieren des Pakets verwendet werden soll. Der Standardwert ist SHA256. |
| Help | Zeigt Hilfe Informationen für den Befehl an. |
| NonInteractive | Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen. |
| OutputDirectory | Gibt das Verzeichnis an, in dem das signierte Paket gespeichert werden soll. Standardmäßig wird das ursprüngliche Paket durch das signierte Paket überschrieben. |
| Overwrite | Wechseln Sie zu, um anzugeben, ob die aktuelle Signatur überschrieben werden soll. Standardmäßig schlägt der Befehl fehl, wenn das Paket bereits über eine Signatur verfügt. |
| Timestamper | URL zu einem RFC 3161-Zeitstempel Server. |
| Timestamphashalgorithm | Hash Algorithmus, der vom RFC 3161-Zeitstempel Server verwendet werden soll. Der Standardwert ist SHA256. |
| Verbosity | Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*. |

## <a name="examples"></a>Beispiele

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```