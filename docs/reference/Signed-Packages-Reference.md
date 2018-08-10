---
title: Signierte Pakete
description: Anforderungen zum Signieren von NuGet-Paket.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 992097281e21cd8cf37edf67fb1968b70c2b359b
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020513"
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

## <a name="get-a-code-signing-certificate"></a>Erhalten Sie ein Codesignaturzertifikat

Gültige Zertifikate können von einer öffentlichen Zertifizierungsstelle wie abgerufen werden:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Globale anmelden](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

Die vollständige Liste der Zertifizierungsstellen, die von Windows als vertrauenswürdig eingestuft erhalten Sie vom [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Ein Testzertifikat erstellen

Sie können selbst ausgestellte Zertifikate verwenden, zu Testzwecken. Verwenden Sie zum Erstellen eines selbst ausgegebenen Zertifikats die [New-SelfSignedCertificate-PowerShell-Befehl](/powershell/module/pkiclient/new-selfsignedcertificate.md).

```ps
New-SelfSignedCertificate -Subject "CN=NuGet Test Developer, OU=Use for testing purposes ONLY" `
                          -FriendlyName "NuGetTestDeveloper" `
                          -Type CodeSigning `
                          -KeyUsage DigitalSignature `
                          -KeyLength 2048 `
                          -KeyAlgorithm RSA `
                          -HashAlgorithm SHA256 `
                          -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
                          -CertStoreLocation "Cert:\CurrentUser\My" 
```

Dieser Befehl erstellt ein Test-Zertifikat verfügbar im persönlichen Zertifikatspeicher des aktuellen Benutzers. Öffnen Sie den Zertifikatspeicher, indem Sie mit `certmgr.msc` um das neu erstellte Zertifikat anzuzeigen.

> [!Warning]
> "NuGet.org" akzeptiert keine Pakete mit selbst ausgestellte Zertifikate signiert.

## <a name="timestamp-requirements"></a>Zeitstempel-Anforderungen

Signierte Pakete sollten einen Zeitstempel RFC 3161 Sicherstellen der Gültigkeit der Signatur über das Paket Signieren der Gültigkeitszeitraum des Zertifikats enthalten. Das Zertifikat zum Signieren des Zeitstempels muss für die `id-kp-timeStamping` Zweck [[RFC 5280 Abschnitt 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Darüber hinaus muss das Zertifikat eine RSA Länge des öffentliche Schlüssels von 2048 Bits oder höher aufweisen.

Zusätzliche technische Details finden Sie in der [Paket Signatur technische Spezifikationen](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Signatur-Anforderungen auf nuget.org

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

## <a name="register-certificate-on-nugetorg"></a>Registrieren des Zertifikats auf nuget.org

Zum Absenden eines signierten Pakets müssen Sie zuerst das Zertifikat mit "NuGet.org" registrieren. Sie benötigen das Zertifikat als eine `.cer` Datei in einem binären Format mit DER. Sie können ein vorhandenes Zertifikat auf ein binäres Format für die DER mit den Zertifikatexport-Assistenten exportieren.

![Zertifikatexport-Assistent](media/CertificateExportWizard.png)

Fortgeschrittene Benutzer können exportieren das Zertifikat mit dem [Export-Certificate-PowerShell-Befehl](/powershell/module/pkiclient/export-certificate.md).

Um das Zertifikat für "NuGet.org" zu registrieren, wechseln Sie zu `Certificates` Abschnitt `Account settings` Seite (oder der Organisation Seite "Einstellungen"), und wählen Sie `Register new certificate`.

![Registrierten Zertifikate](media/registered-certs.png)

> [!Tip]
> Ein Benutzer kann zu übermitteln, dass mehrere Zertifikate und das gleiche Zertifikat von mehreren Benutzern registriert werden können.

Sobald ein Benutzer hat ein Zertifikat registriert, alle zukünftigen Paket Übermittlungen **müssen** mit einem der Zertifikate signiert werden.

Benutzer können auch ein registriertes Zertifikat aus dem Konto entfernen. Sobald ein Zertifikat entfernt wurde, können Sie Pakete, die mit diesem Zertifikat signiert zur Übermittlung fehlschlagen. Vorhandene Pakete sind nicht betroffen.

## <a name="configure-package-signing-requirements"></a>Konfigurieren Sie Paket Signieren von Anforderungen

Wenn Sie der alleinige Eigentümer eines Pakets sind, können Sie den erforderlichen Signaturgeber. D. h., können Sie eines der registrierten Zertifikate zum Signieren von Paketen und auf nuget.org zu übermitteln.

Wenn ein Paket mehrere Besitzer fest, in der Standardeinstellung verfügt, können "Any" des Besitzers Zertifikate zum Signieren des Pakets verwendet werden. Als Mitbesitzer des Pakets können Sie "Any" für sich selbst oder andere Mitbesitzer den Signaturgeber erforderlich sein überschreiben. Wenn Sie als Besitzer, der nicht über eine beliebige registrierte Zertifikat verfügt festlegen, werden nicht signierte Paketen zugelassen. 

Auf ähnliche Weise die Standardeinstellung "Alle" ausgewählt ist für ein Paket, die einen Besitzer, in denen ein registriertes Zertifikat hat und einen anderen Besitzer keine registrierte Zertifikat verfügt, klicken Sie dann "NuGet.org" akzeptiert entweder ein signiertes Pakets mit einer Signatur, die von einer ihrer Besitzer registriert oder eine nicht signierte Paket (da der Besitzer keine registrierte Zertifikat besitzt).

![Konfigurieren Sie die Paket-Signaturgeber](media/configure-package-signers.png)
