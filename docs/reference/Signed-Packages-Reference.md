---
title: Signierte Pakete
description: Anforderungen für das Signieren von nuget-Paketen
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: e02b2a241008b1b7096f20b351173fd3df7ed172
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317519"
---
# <a name="signed-packages"></a>Signierte Pakete

*Nuget 4.6.0 + und Visual Studio 2017 Version 15,6 und höher*

Nuget-Pakete können eine digitale Signatur enthalten, die Schutz vor Manipulations Inhalten bietet. Diese Signatur wird von einem X. 509-Zertifikat erzeugt, das dem eigentlichen Ursprung des Pakets auch Authentizitäts Nachweise hinzufügt.

Signierte Pakete bieten die stärkste End-to-End-Validierung. Es gibt zwei verschiedene Arten von nuget-Signaturen:
- **Signatur des Autors**. Eine Autoren Signatur garantiert, dass das Paket nicht geändert wurde, seit der Autor das Paket signiert hat, unabhängig davon, welches Repository oder welche Transportmethode das Paket übermittelt. Außerdem bieten Autor-signierte Pakete einen zusätzlichen Authentifizierungsmechanismus für die nuget.org-Veröffentlichungs Pipeline, da das Signaturzertifikat vorab registriert werden muss. Weitere Informationen finden Sie unter [Registrieren von Zertifikaten](#signature-requirements-on-nugetorg).
- **Repository-Signatur**. Repository-Signaturen stellen eine Integritäts Garantie für **alle** Pakete in einem Repository dar, unabhängig davon, ob Sie Autor signiert sind oder nicht, auch wenn diese Pakete von einem anderen Speicherort als dem ursprünglichen Repository abgerufen werden, in dem Sie signiert wurden.   

Weitere Informationen zum Erstellen eines signierten Pakets mit Vorzeichen finden Sie [unter Signieren von Paketen](../create-packages/Sign-a-package.md) und [nuget](../reference/cli-reference/cli-ref-sign.md)-Signierungs Befehl.

> [!Important]
> Die Paket Signierung wird derzeit nur unterstützt, wenn "nuget. exe" unter Windows verwendet wird. Die Überprüfung von signierten Paketen wird derzeit nur unterstützt, wenn Sie "nuget. exe" oder Visual Studio unter Windows verwenden.

## <a name="certificate-requirements"></a>Zertifikat Anforderungen

Zum Signieren von Paketen ist ein Code Signaturzertifikat erforderlich, bei dem es sich um einen speziellen Zertifikattyp handelt, der für den `id-kp-codeSigning` Zweck [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] gültig ist. Außerdem muss das Zertifikat eine öffentliche RSA-Schlüssellänge von 2048 Bits oder höher aufweisen.

## <a name="timestamp-requirements"></a>Timestamp-Anforderungen

Signierte Pakete sollten einen RFC 3161-Zeitstempel enthalten, um die Gültigkeit der Signatur außerhalb der Gültigkeitsdauer des Paket Signatur Zertifikats sicherzustellen. Das zum Signieren des Zeitstempels verwendete Zertifikat muss für den `id-kp-timeStamping` Zweck [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] gültig sein. Außerdem muss das Zertifikat eine öffentliche RSA-Schlüssellänge von 2048 Bits oder höher aufweisen.

Weitere technische Details finden Sie in der [Paket Signatur Technical Spezifikationen](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Signatur Anforderungen auf NuGet.org

nuget.org bietet zusätzliche Anforderungen für die Annahme eines signierten Pakets:

- Die primäre Signatur muss eine Autoren Signatur sein.
- Die primäre Signatur muss einen einzelnen gültigen Zeitstempel aufweisen.
- Die X. 509-Zertifikate für die Autor-Signatur und deren Zeitstempel Signatur:
  - Muss über einen öffentlichen RSA-Schlüssel von 2048 Bits oder höher verfügen.
  - Muss innerhalb der Gültigkeitsdauer der aktuellen UTC-Zeit zum Zeitpunkt der Paket Validierung auf nuget.org liegen.
  - Muss zu einer vertrauenswürdigen Stamm Zertifizierungsstelle verkettet werden, die standardmäßig unter Windows als vertrauenswürdig eingestuft wird Pakete, die mit selbst ausgestellten Zertifikaten signiert sind, werden abgelehnt.
  - Muss für den Zweck gültig sein: 
    - Das Signaturzertifikat des Autors muss für die Code Signatur gültig sein.
    - Das Zeitstempel Zertifikat muss für das Zeitstempel gültig sein.
  - Muss zum Zeitpunkt der Signierung nicht widerrufen werden. (Dies ist möglicherweise zum Zeitpunkt der Übermittlung nicht erkennbar, sodass nuget.org den Sperr Status regelmäßig erneut überprüft.)
  
  
## <a name="related-articles"></a>Verwandte Artikel

- [Signieren von NuGet-Paketen](../create-packages/Sign-a-Package.md)
- [Verwalten von Paketvertrauensgrenzen](../consume-packages/installing-signed-packages.md)
