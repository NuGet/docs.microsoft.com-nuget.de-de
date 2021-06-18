---
title: Befehl "Trusted Signers" der NuGet-CLI
description: Referenz für den befehl nuget.exe trusted-signers
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: a5f3564af8b96dfa673d2252aea2e77a79c184a4
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323589"
---
# <a name="trusted-signers-command-nuget-cli"></a>Befehl "trusted-signers" (NuGet-CLI)

**Gilt für: Paketverbrauch** &bullet; **Unterstützte Versionen:** 4.9.1+

Ruft vertrauenswürdige Signierer für die NuGet-Konfiguration ab oder legt diese fest. Weitere Informationen zur Verwendung finden Sie unter [Allgemeine NuGet-Konfigurationen.](../../consume-packages/configuring-nuget-behavior.md) Weitere Informationen dazu, wie nuget.config Schema aussieht, finden Sie in der [Referenz zur NuGet-Konfigurationsdatei.](../nuget-config-file.md)

## <a name="usage"></a>Verwendung

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Wenn keiner von `list|add|remove|sync` angegeben wird, wird der Befehl standardmäßig auf `list` festgelegt.

## <a name="nuget-trusted-signers-list"></a>Liste der vertrauenswürdigen NuGet-Signierer

Listet alle vertrauenswürdigen Signierer in der Konfiguration auf. Diese Option enthält alle Zertifikate (mit Fingerabdruck- und Fingerabdruckalgorithmus), über die jeder Signator verfügt. Wenn ein Zertifikat über eine vorangehende `[U]` verfügt, bedeutet dies, dass der Zertifikateintrag `allowUntrustedRoot` auf festgelegt `true` wurde.

Im Folgenden finden Sie eine Beispielausgabe dieses Befehls:

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D
        SHA256 - 5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>nuget trusted-signers add [Optionen]

Fügt der Konfiguration einen vertrauenswürdigen Signator mit dem angegebenen Namen hinzu. Diese Option verfügt über unterschiedliche Gesten zum Hinzufügen eines vertrauenswürdigen Autors oder Repositorys.

## <a name="options-for-add-based-on-a-package"></a>Optionen für das Hinzufügen basierend auf einem Paket

```cli
nuget trusted-signers add <package> -Name <name> [options]
```

dabei `<package>` ist eine signierte `.nupkg` Datei.

- **`-Author`**

  Gibt an, dass die Signatur des signierten Pakets als vertrauenswürdig eingestuft werden soll.

- **`-AllowUntrustedRoot`**

  Gibt an, ob das Zertifikat für den vertrauenswürdigen Signator mit einem nicht vertrauenswürdigen Stamm verkettet werden soll.

- **`-Owners`**

  Durch Semikolons getrennte Liste vertrauenswürdiger Besitzer, um die Vertrauensstellung eines Repositorys weiter einzuschränken. Nur gültig, wenn die Option verwendet `-Repository` wird.

- **`-Repository`**

  Gibt an, dass die Repositorysignatur oder Gegensignatur des signierten Pakets als vertrauenswürdig eingestuft werden soll.

Die gleichzeitige Bereitstellung von und `-Author` `-Repository` wird nicht unterstützt.

## <a name="options-for-add-based-on-a-service-index"></a>Optionen für das Hinzufügen basierend auf einem Dienstindex

```cli
nuget trusted-signers add -Name <name> [options]
```

_Hinweis:_ Mit dieser Option werden nur vertrauenswürdige Repositorys hinzugefügt. 

- **`-AllowUntrustedRoot`**

  Gibt an, ob das Zertifikat für den vertrauenswürdigen Signator mit einem nicht vertrauenswürdigen Stamm verkettet werden soll.

- **`-Owners`**

  Durch Semikolons getrennte Liste vertrauenswürdiger Besitzer, um die Vertrauensstellung eines Repositorys weiter einzuschränken.

- **`-ServiceIndex`**

  Gibt den V3-Dienstindex des Repositorys an, das als vertrauenswürdig eingestuft werden soll. Dieses Repository muss die Repositorysignaturressource unterstützen. Falls nicht angegeben, sucht der Befehl nach einer Paketquelle mit demselben und dem `-Name` Dienstindex.

## <a name="options-for-add-based-on-the-certificate-information"></a>Optionen zum Hinzufügen basierend auf den Zertifikatinformationen

```cli
nuget trusted-signers add -Name <name> [options]
```

_Hinweis:_ Wenn bereits ein vertrauenswürdiger Signator mit dem angegebenen Namen vorhanden ist, wird das Zertifikatelement diesem Signator hinzugefügt. Andernfalls wird ein vertrauenswürdiger Autor mit einem Zertifikatelement aus den angegebenen Zertifikatinformationen erstellt.


- **`-AllowUntrustedRoot`**

  Gibt an, ob das Zertifikat für den vertrauenswürdigen Signator mit einem nicht vertrauenswürdigen Stamm verkettet werden soll.

- **`-CertificateFingerprint`**

  Gibt einen Zertifikatfingerabdruck eines Zertifikats an, mit dem signierte Pakete signiert werden müssen. Ein Zertifikatfingerabdruck ist ein Hash des Zertifikats. Der hash-Algorithmus, der zum Berechnen dieses Hashs verwendet wird, sollte in der Option angegeben `FingerprintAlgorithm` werden.

- **`-FingerprintAlgorithm`**

  Gibt den Hashalgorithmus an, der zum Berechnen des Zertifikatfingerabdrucks verwendet wird. Wird standardmäßig auf `SHA256` festgelegt. Unterstützte Werte sind `SHA256` , `SHA384` und `SHA512` .

## <a name="nuget-trusted-signers-remove--name-name"></a>nuget trusted-signers remove -Name \<name\>

Entfernt alle vertrauenswürdigen Signierer, die mit dem angegebenen Namen übereinstimmen.

## <a name="nuget-trusted-signers-sync--name-name"></a>nuget trusted-signers sync -Name \<name\>

Fordert die aktuelle Liste der Zertifikate an, die in einem derzeit vertrauenswürdigen Repository verwendet werden, um die vorhandene Zertifikatliste im vertrauenswürdigen Signator zu aktualisieren.

_Hinweis:_ Mit dieser Geste wird die aktuelle Liste der Zertifikate gelöscht und durch eine aktuelle Liste aus dem Repository ersetzt.

## <a name="options"></a>Optionen

- **`-ConfigFile`**

  Die nuGet-Konfigurationsdatei, die angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` werden (Windows) `~/.nuget/NuGet/NuGet.Config` oder oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.

- **`-ForceEnglishOutput`**

  Erzwingt nuget.exe ausführung mit einer invarianten, englischsprachigen Kultur.

- **`-?|-help`**

  Zeigt Hilfeinformationen für den Befehl an.

- **`-Name`**

  Name des vertrauenswürdigen Signers.

- **`-NonInteractive`**

  Unterdrückt Eingabeaufforderungen oder Bestätigungen von Benutzereingaben.

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt die Detailmenge an, die in der Ausgabe angezeigt wird: `normal` (Standard), `quiet` oder `detailed` .


## <a name="examples"></a>Beispiele

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget trusted-signers Remove -Name TrustedRepo

nuget trusted-signers Sync -Name TrustedRepo
```
