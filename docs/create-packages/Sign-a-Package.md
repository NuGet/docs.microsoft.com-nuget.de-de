---
title: Signieren von NuGet-Paketen
description: Informationen zur Verwendung von signierten Paketen zur Aktivierung der Integritätsüberprüfung des Inhalts.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a469cbdd218a0e9c18950bb0d36faf4dbcb42a01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="signing-nuget-packages"></a>Signieren von NuGet-Paketen

Durch die Signierung eines Pakets wird sichergestellt, dass dieses nicht mehr verändert wurde, nachdem es erstellt wurde.

## <a name="prerequisites"></a>Erforderliche Komponenten

1. Das zu signierende Paket (eine `.nupkg`-Datei). Weitere Informationen finden Sie unter [Erstellen von NuGet-Paketen](creating-a-package.md).

1. nuget.exe 4.6.0 oder höher. Weitere Informationen finden Sie unter [Installieren von NuGet-Clienttools](../install-nuget-client-tools.md#nugetexe-cli).

1. [Signierte Pakete](../reference/signed-packages-reference.md#get-a-code-signing-certificate).

> [!Warning]
> Derzeit akzeptiert nuget.org keine signierten Pakete. Sie können Pakete signieren, die auf benutzerdefinierten Feeds veröffentlicht werden sollen.

## <a name="sign-a-package"></a>Signieren eines Pakets

Verwenden Sie den NuGet-Befehl [sign](../tools/cli-ref-sign.md), um ein Paket zu signieren:

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

Sie können, wie in der Referenz zu dem Befehl beschrieben, ein Zertifikat, das im Zertifikatspeicher verfügbar ist, oder ein Zertifikat aus einer Datei verwenden.

### <a name="common-problems-when-signing-a-package"></a>Häufig auftretende Probleme beim Signieren eines Pakets

- Das Zertifikat ist nicht gültig für das Codesignieren. Sie müssen sicherstellen, dass das angegebene Zertifikat über die entsprechende erweiterte Schlüsselverwendung verfügt (EKU 1.3.6.1.5.5.7.3.3).
- Das Zertifikat entspricht nicht den grundlegenden Anforderungen wie dem RSA SHA-256-Signaturalgorithmus oder einem öffentlicher Schlüssel mit einer Größe von mindestens 2048 Bit.
- Das Zertifikat ist abgelaufen oder wurde widerrufen.
- Der Zeitstempelserver entspricht nicht den Zertifikatanforderungen.

> [!Note]
> Signierte Pakete sollten einen Zeitstempel enthalten, um sicherzustellen, dass die Signatur gültig bleibt, wenn das Signaturzertifikat abläuft. Beim Signiervorgang wird die [Warnung NU3002](../reference/Errors-and-Warnings.md#nu3002) ausgelöst, wenn kein Zeitstempel verwendet wird.

## <a name="verify-a-signed-package"></a>Überprüfen eines signierten Pakets

Verwenden Sie den NuGet-Befehl [verify](../tools/cli-ref-verify.md), um die Details der Signatur eines bestimmten Pakets anzuzeigen:

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a>Installieren eines signierten Pakets

Es erfordert keine bestimmten Aktionen, um signierte Pakete zu installieren. Wenn jedoch nach der Signierung Veränderungen am Inhalt vorgenommen wurden, wird die Installation blockiert und der [Fehler NU3008](../reference/Errors-and-Warnings.md#nu3008) ausgelöst.

> [!Warning]
> Pakete, die mit nicht vertrauenswürdigen Zertifikaten signiert wurden, werden als „nicht signiert“ angesehen und lösen wie alle anderen nicht signierten Pakete bei der Installation weder Warnungen noch Fehler aus.

## <a name="see-also"></a>Siehe auch

[Referenz für signierte Pakete](../reference/Signed-Packages-Reference.md)
