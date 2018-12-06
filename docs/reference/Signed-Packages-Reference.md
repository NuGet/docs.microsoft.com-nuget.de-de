---
title: Signierte Pakete
description: Anforderungen zum Signieren von NuGet-Paket.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 486bf4032e156168f9b2fef57ccdae0c372b2eff
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977510"
---
# <a name="signed-packages"></a>Signierte Pakete

*NuGet 4.6.0+ und Visual Studio 2017 Version 15.6 und höher*

NuGet-Paketen können es sich um eine digitale Signatur enthalten, die Schutz vor manipulierte Inhalte bereitstellt. Diese Signatur wird aus einem x. 509-Zertifikat erstellt, die die eigentliche Quelle des Pakets auch Authentizität Nachweise hinzufügt.

Signierte Pakete bereitstellen die stärkste End-to-End-Überprüfung. Es gibt zwei verschiedene Arten von NuGet-Signaturen:
- **Erstellen der Signatur**. Eine Autor-Signatur wird sichergestellt, dass das Paket nicht geändert wurde, seit der Autor signiert das Paket, unabhängig davon aus dem Repository, oder welche Methode transport wird das Paket bereitgestellt. Darüber hinaus bieten Autor signierte Pakete einen zusätzlichen Authentifizierungsmechanismus für die Veröffentlichung nuget.org-Pipeline aus, da das Signaturzertifikat vorab registriert werden muss. Weitere Informationen finden Sie unter [Registrieren von Zertifikaten](#register-certificate-on-nugetorg).
- **Repository-Signatur**. Repository-Signaturen bieten eine Garantie der Integrität für **alle** Pakete in einem Repository, ob diese Autor signiert oder unsigniert, sind, auch wenn diese Pakete aus einem anderen Ort als das ursprüngliche Repository abgerufen werden, in denen sie waren, signiert.   

Ausführliche Informationen zum Erstellen eines signierten Autor-Pakets, finden Sie unter [Pakete signieren](../create-packages/Sign-a-package.md) und [Nuget-anmelden-Befehl](../tools/cli-ref-sign.md).

> [!Important]
> Paketsignierung wird derzeit nur bei Verwendung von nuget.exe auf Windows unterstützt. Überprüfung von signierten Paketen werden derzeit nur bei Verwendung von nuget.exe- oder Visual Studio für Windows.

## <a name="certificate-requirements"></a>Zertifikatanforderungen

Paketsignierung erfordert ein Codesignaturzertifikat, der eine besondere Art von Zertifikat ist, für ungültig ist, die `id-kp-codeSigning` Zweck [[RFC 5280 Abschnitt 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Darüber hinaus muss das Zertifikat eine RSA Länge des öffentliche Schlüssels von 2048 Bits oder höher aufweisen.

## <a name="timestamp-requirements"></a>Zeitstempel-Anforderungen

Signierte Pakete sollten einen Zeitstempel RFC 3161 Sicherstellen der Gültigkeit der Signatur über das Paket Signieren der Gültigkeitszeitraum des Zertifikats enthalten. Das Zertifikat zum Signieren des Zeitstempels muss für die `id-kp-timeStamping` Zweck [[RFC 5280 Abschnitt 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Darüber hinaus muss das Zertifikat eine RSA Länge des öffentliche Schlüssels von 2048 Bits oder höher aufweisen.

Zusätzliche technische Details finden Sie in der [Paket Signatur technische Spezifikationen](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Signatur-Anforderungen auf NuGet.org

"NuGet.org" verfügt über zusätzliche Anforderungen für das Akzeptieren eines signierten Pakets:

- Die primäre Signatur muss eine Signatur erstellen.
- Die primäre Signatur muss einen einzigen gültigen Zeitstempel haben.
- Die x. 509-Zertifikate für die Signatur der Autor und der Timestamp-Signatur:
  - Benötigen Sie einen öffentlichen RSA-Schlüssel 2048 Bits betragen.
  - Muss innerhalb seiner Gültigkeitsdauer pro aktuelle UTC-Zeit zum Zeitpunkt der paketüberprüfung auf nuget.org.
  - Muss mit einer vertrauenswürdigen Stammzertifizierungsstelle verkettet, die standardmäßig unter Windows als vertrauenswürdig eingestuft wird. Pakete, die mit selbst ausgestellte Zertifikate signiert werden abgelehnt.
  - Gültig muss für den Zweck: 
    - Der Autor Signaturzertifikat muss zum Signieren von Code gültig sein.
    - Der Timestamp-Zertifikat muss für Zeitstempel gültig sein.
  - Muss auf den Zeitpunkt der Signatur nicht widerrufen werden. (Diese zum Zeitpunkt der Einreichung bei möglicherweise nicht so, dass nuget.org in regelmäßigen Abständen den Status der Zertifikatsperre dann nachkontrolliert).
  
  
## <a name="related-articles"></a>Verwandte Artikel

- [Signieren von NuGet-Paketen](../create-packages/Sign-a-Package.md)
- [Installieren von signierten Paketen](../consume-packages/installing-signed-packages.md)
