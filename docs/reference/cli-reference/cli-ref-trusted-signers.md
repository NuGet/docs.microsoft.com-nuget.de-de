---
title: Befehl für die nuget-CLI für vertrauenswürdige Signaturen
description: Referenz für den nuget.exe Befehl "Trusted-Signers"
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9e25f439617a76d30880bea3c10a5d063e681a41
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238152"
---
# <a name="trusted-signers-command-nuget-cli"></a>Befehl "Trusted-Signers" (nuget-CLI)

**Gilt für:** &bullet; **unterstützte Versionen** von Paket Verbrauch: 4.9.1 +

Ruft vertrauenswürdige Signatur Geber für die nuget-Konfiguration ab oder legt Sie fest. Weitere Informationen finden Sie unter [Allgemeine nuget-Konfigurationen](../../consume-packages/configuring-nuget-behavior.md). Ausführliche Informationen dazu, wie das nuget.config Schema aussieht, finden Sie in der [nuget-Konfigurationsdatei Referenz](../nuget-config-file.md).

## <a name="usage"></a>Verbrauch

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Wenn keines von `list|add|remove|sync` angegeben wird, wird der-Befehl standardmäßig auf festgelegt `list` .

## <a name="nuget-trusted-signers-list"></a>nuget-Liste der vertrauenswürdigen Signaturen

Listet alle vertrauenswürdigen Signatur Geber in der Konfiguration auf. Diese Option umfasst alle Zertifikate (mit Fingerabdruck und Fingerabdruck Algorithmus), die jeder Signatur Geber hat. Wenn ein Zertifikat einen vorangehenden hat `[U]` , bedeutet dies, dass der Zertifikat Eintrag `allowUntrustedRoot` als festgelegt hat `true` .

Im folgenden finden Sie ein Beispiel für die Ausgabe dieses Befehls:

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>nuget vertrauenswürdiger-Signatur Geber Add [Optionen]

Fügt der Konfiguration einen vertrauenswürdigen Signatur Geber mit dem angegebenen Namen hinzu. Diese Option weist verschiedene Gesten auf, um einen vertrauenswürdigen Autor oder ein Repository hinzuzufügen.

## <a name="options-for-add-based-on-a-package"></a>Optionen zum Hinzufügen basierend auf einem Paket

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

dabei `<package(s)>` ist eine oder mehrere `.nupkg` Dateien.

- **`-Author`**

  Gibt an, dass der Autor der Signatur des Pakets vertraut werden soll.

- **`-AllowUntrustedRoot`**

  Gibt an, ob das Zertifikat für den vertrauenswürdigen Signatur Geber an einen nicht vertrauenswürdigen Stamm verkettet werden darf.

- **`-Owners`**

  Durch Semikolons getrennte Liste vertrauenswürdiger Besitzer, um die Vertrauenswürdigkeit eines Repository weiter einzuschränken. Nur gültig, wenn die `-Repository` Option verwendet wird.

- **`-Repository`**

  Gibt an, dass die Repository-Signatur oder die gegen Signatur der Pakete als vertrauenswürdig eingestuft werden soll.

Die Angabe von `-Author` und `-Repository` zur gleichen Zeit wird nicht unterstützt.

## <a name="options-for-add-based-on-a-service-index"></a>Optionen zum Hinzufügen basierend auf einem Dienst Index

```cli
nuget trusted-signers add -Name <name> [options]
```

_Hinweis_ : mit dieser Option werden nur vertrauenswürdige Depots hinzugefügt. 

- **`-AllowUntrustedRoot`**

  Gibt an, ob das Zertifikat für den vertrauenswürdigen Signatur Geber an einen nicht vertrauenswürdigen Stamm verkettet werden darf.

- **`-Owners`**

  Durch Semikolons getrennte Liste vertrauenswürdiger Besitzer, um die Vertrauenswürdigkeit eines Repository weiter einzuschränken.

- **`-ServiceIndex`**

  Gibt den V3-Dienst Index des Repository an, das als vertrauenswürdig eingestuft werden soll. Dieses Repository muss die Repository Signature-Ressource unterstützen. Wenn keine Angabe erfolgt, sucht der Befehl nach einer Paketquelle mit dem gleichen `-Name` und erhält den Dienst Index von dort aus.

## <a name="options-for-add-based-on-the-certificate-information"></a>Optionen zum Hinzufügen basierend auf den Zertifikat Informationen

```cli
nuget trusted-signers add -Name <name> [options]
```

_Hinweis_ : Wenn bereits ein vertrauenswürdiger Signatur Geber mit dem angegebenen Namen vorhanden ist, wird das Zertifikat Element diesem Signatur Geber hinzugefügt. Andernfalls wird ein vertrauenswürdiger Autor mit einem Zertifikat Element aus den angegebenen Zertifikat Informationen erstellt.


- **`-AllowUntrustedRoot`**

  Gibt an, ob das Zertifikat für den vertrauenswürdigen Signatur Geber an einen nicht vertrauenswürdigen Stamm verkettet werden darf.

- **`-CertificateFingerprint`**

  Gibt einen Zertifikat Fingerabdruck eines Zertifikats an, mit dem signierte Pakete signiert werden müssen. Ein Zertifikat Fingerabdruck ist ein Hash des Zertifikats. Der Hash Algorithmus, der zum Berechnen dieses Hashwerts verwendet wird, sollte in der-Option angegeben werden `FingerprintAlgorithm` .

- **`-FingerprintAlgorithm`**

  Gibt den Hash Algorithmus an, mit dem der Zertifikat Fingerabdruck berechnet wird. Wird standardmäßig auf `SHA256` festgelegt. Unterstützte Werte sind `SHA256` , `SHA384` und `SHA512` .

## <a name="nuget-trusted-signers-remove--name-name"></a>nuget vertrauenswürdiger Signatur Geber Remove-Name \<name\>

Entfernt alle vertrauenswürdigen Signatur Geber, die dem angegebenen Namen entsprechen.

## <a name="nuget-trusted-signers-sync--name-name"></a>nuget-Synchronisierungs Name für vertrauenswürdige Signaturen \<name\>

Fordert die aktuelle Liste der Zertifikate an, die in einem aktuell vertrauenswürdigen Repository verwendet werden, um die Liste vorhandener Zertifikate im vertrauenswürdigen Signatur Geber zu aktualisieren.

_Hinweis_ : durch diese Geste wird die aktuelle Liste der Zertifikate gelöscht und durch eine aktuelle Liste aus dem Repository ersetzt.

## <a name="options"></a>Optionen

- **`-ConfigFile`**

  Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.

- **`-ForceEnglishOutput`**

  Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.

- **`-?|-help`**

  Zeigt Hilfe Informationen für den Befehl an.

- **`-Name`**

  Der Name des vertrauenswürdigen Signatur Gebers.

- **`-NonInteractive`**

  Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .


## <a name="examples"></a>Beispiele

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
