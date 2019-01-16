---
title: Vertrauenswürdige Signaturgeber NuGet-CLI-Befehl
description: Referenz für die der vertrauenswürdige Signaturgeber nuget.exe-Befehl
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ee4ffaa7e250cdbf313476fd794a8d87c80b69f9
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324707"
---
# <a name="trusted-signers-command-nuget-cli"></a>Vertrauenswürdige Signaturgeber-Befehl (NuGet-CLI)

**Gilt für:** Paket Verbrauch &bullet; **unterstützte Versionen:** 4.9.1+

Übernimmt oder bestimmt der vertrauenswürdige Signaturgeber der NuGet-Konfiguration. Zusätzliche Nutzung, finden Sie unter [Konfigurieren des NuGet-Verhaltens](../consume-packages/configuring-nuget-behavior.md). Weitere Einzelheiten, wie das Schema der Datei "NuGet.config" offenbar, auf die [NuGet Config-Dateiverweis](../reference/nuget-config-file.md).

## <a name="usage"></a>Verwendung

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Wenn keine der `list|add|remove|sync` angegeben ist, wird der Befehl standardmäßig `list`.

## <a name="nuget-trusted-signers-list"></a>Liste der NuGet-vertrauenswürdige Signaturgeber

Listet alle in der Konfiguration der vertrauenswürdige Signaturgeber. Diese Option werden alle Zertifikate enthalten (mit Fingerabdruck und fingerabdruckalgorithmus) jedes Signaturgeber hat. Wenn ein Zertifikat eine vorangestellte verfügt `[U]`, dies bedeutet, dass das Zertifikateintrag hat `allowUntrustedRoot` als `true`.

Es folgt eine Beispielausgabe dieses Befehls:

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

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>Vertrauenswürdige Signaturgeber mit NuGet add [Optionen]

Fügt einen vertrauenswürdigen Signaturgeber mit dem angegebenen Namen auf die Konfiguration an. Diese Option hat unterschiedliche Gesten zum Hinzufügen eines vertrauenswürdigen Autor oder Repository.

## <a name="options-for-add-based-on-a-package"></a>Optionen zum Hinzufügen, die basierend auf einem Paket

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

wo `<package(s)>` enthält eine oder mehrere `.nupkg` Dateien.

| Option | Beschreibung |
| --- | --- |
| Autor | Gibt an, dass die Signatur der Autor der Pakete vertrauenswürdig sind. |
| Repository | Gibt an, dass die Repository-Signatur oder die Gegensignatur der Pakete vertrauenswürdig sind. |
| AllowUntrustedRoot | Gibt an, wenn das Zertifikat für die der vertrauenswürdige Signaturgeber, eine Verkettung mit einem nicht vertrauenswürdigen Stamm zugelassen werden soll. |
| Besitzer | Durch Semikolons getrennte Liste der vertrauenswürdigen Besitzer, um die Vertrauensstellung eines Repositorys weiter einzuschränken. Nur gültig, wenn Sie mit der `-Repository` Option. |

Bereitstellung `-Author` und `-Repository` zur gleichen Zeit wird nicht unterstützt.

## <a name="options-for-add-based-on-a-service-index"></a>Optionen für die basierend auf einem Dienst hinzufügen

```cli
nuget trusted-signers add -Name <name> [options]
```

_Hinweis:_ Diese Option wird nur mit vertrauenswürdigen Repositorys hinzufügen. 

| Option | Beschreibung |
| --- | --- |
| ServiceIndex | Gibt den Index des V3-Dienst des Repositorys als vertrauenswürdig gelten sollen. Dieses Repository enthält, die die Ressource der Repository-Signaturen unterstützen. Wenn nicht angegeben ist, sieht der Befehl für eine Paketquelle mit dem gleichen `-Name` und dienstindex von dort abrufen. |
| AllowUntrustedRoot | Gibt an, wenn das Zertifikat für die der vertrauenswürdige Signaturgeber, eine Verkettung mit einem nicht vertrauenswürdigen Stamm zugelassen werden soll. |
| Besitzer | Durch Semikolons getrennte Liste der vertrauenswürdigen Besitzer, um die Vertrauensstellung eines Repositorys weiter einzuschränken. |

## <a name="options-for-add-based-on-the-certificate-information"></a>Optionen zum Hinzufügen, die basierend auf den Zertifikatinformationen

```cli
nuget trusted-signers add -Name <name> [options]
```

_Hinweis:_ Wenn es sich bei ein vertrauenswürdiger Signaturgeber mit dem angegebenen Namen bereits vorhanden ist, wird diese Signaturgeber das zertifikatselement hinzugefügt werden. Andernfalls wird der Autor ein vertrauenswürdigen erstellt werden, mit einem zertifikatselement aus den angegebenen Informationen zum Zertifikat.

| Option | Beschreibung |
| --- | --- |
| CertificateFingerprint | Gibt ein Zertifikat, mit dem Fingerabdrücke der eines Zertifikats, das signierte Pakete signiert werden müssen. Ein Fingerabdruck des Zertifikats ist ein Hash des Zertifikats. Der Hashalgorithmus für die Berechnung des Hash muss gibt an, der `FingerprintAlgorithm` Option. |
| FingerprintAlgorithm | Gibt den Hashalgorithmus, der zum Berechnen der Fingerabdruck des Zertifikats an. Wird standardmäßig auf `SHA256` festgelegt. Werte werden unterstützt `SHA256`, `SHA384` und `SHA512` |
| AllowUntrustedRoot | Gibt an, wenn das Zertifikat für die der vertrauenswürdige Signaturgeber, eine Verkettung mit einem nicht vertrauenswürdigen Stamm zugelassen werden soll. |

## <a name="nuget-trusted-signers-remove--name-name"></a>Entfernen Sie vertrauenswürdige Signaturgeber mit NuGet - Namen <name>

Entfernt alle vertrauenswürdigen Signaturgeber, die mit dem angegebenen Namen übereinstimmen.

## <a name="nuget-trusted-signers-sync--name-name"></a>Synchronisieren Sie vertrauenswürdige Signaturgeber mit NuGet - Name <name>

Fordert die aktuelle Liste der Zertifikate, die im derzeit vertrauenswürdiges Repository verwendet werden, zum Aktualisieren der die vorhandenen Zertifikatliste in der vertrauenswürdige Signaturgeber.

_Hinweis:_ Diese stiftbewegung wird die aktuelle Liste der Zertifikate zu löschen und Ersetzen Sie sie durch eine aktuelle Liste, aus dem Repository.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| ForceEnglishOutput | Erzwingt, dass nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden. |
| Help | Zeigt die Informationen für den Befehl Hilfe. |
| Ausführlichkeit | Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*. |

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
