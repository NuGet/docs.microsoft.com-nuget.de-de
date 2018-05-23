---
title: Signierte Pakete
description: Anforderungen für die Signierung von NuGet-Paket.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 72fb1a87c13160c53f632d2ef87a12a4e9bc02a3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/22/2018
---
# <a name="signed-packages"></a>Signierte Pakete

*NuGet-4.6.0+ und Visual Studio 2017 15.6 und höher*

NuGet-Pakete können es sich um eine digitale Signatur einzuschließen, die Schutz vor manipulierte Inhalte enthält. Diese Signatur wird aus einem x. 509-Zertifikat erzeugt, die der tatsächliche Ursprung der das Paket auch Authentizität Proofs hinzufügt.

Signierte Pakete bereitstellen die stärkste End-to-End-Überprüfung. Eine Autor-Signatur wird sichergestellt, dass das Paket nicht geändert wurde, seit der Autor das Paket, unabhängig davon aus signiert die Repositorys oder welche Methode transport das Paket wird übermittelt.

Darüber hinaus bieten Autor signierte Pakete einen zusätzlichen Authentifizierungsmechanismus die publishing nuget.org-Pipeline, da das Signaturzertifikat voraus registriert werden muss. Weitere Informationen finden Sie unter [Registrieren von Zertifikaten](#register-certificate-on-nugetorg).

Weitere Informationen zum Erstellen eines signierten Pakets, finden Sie unter [Signieren von Paketen](../create-packages/Sign-a-package.md) und [NuGet-Anmelde-Befehls](../tools/cli-ref-sign.md).

> [!Important]
> Paketsignierung wird derzeit nur bei Verwendung von nuget.exe unter Windows unterstützt. Überprüfung von signierten Paketen ist derzeit nur unterstützt, wenn nuget.exe oder Visual Studio unter Windows verwenden.

## <a name="certificate-requirements"></a>Zertifikatanforderungen

Codesignaturzertifikat anfordern, die eine besondere Art von Zertifikat ist, die für gültig ist paketsignierung erfordert die `id-kp-codeSigning` Zweck [[RFC 5280 Abschnitt 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Darüber hinaus muss das Zertifikat eine RSA Länge des öffentliche Schlüssels von 2048 Bits oder höher aufweisen.

## <a name="get-a-code-signing-certificate"></a>Erhalten Sie ein Codesignaturzertifikat

Gültige Zertifikate können von einer öffentlichen Zertifizierungsstelle wie abgerufen werden:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Globale anmelden](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

Die vollständige Liste der Zertifizierungsstellen von Windows als vertrauenswürdig eingestuft erhalten von [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Ein Testzertifikat erstellen

Sie können selbst ausgestellte Zertifikate für Testzwecke verwenden. Verwenden Sie zum Erstellen eines selbst ausgegebenen Zertifikats die [New-SelfSignedCertificate-PowerShell-Befehl](/powershell/module/pkiclient/new-selfsignedcertificate.md).

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

Dieser Befehl erstellt ein Testzertifikats verfügbar im persönlichen Zertifikatspeicher des aktuellen Benutzers. Sie können den Zertifikatspeicher öffnen, indem ausgeführt `certmgr.msc` des neu erstellten Zertifikats angezeigt.

> [!Warning]
> NuGet.org akzeptiert keine Pakete mit selbst ausgestellte Zertifikate signiert.

## <a name="timestamp-requirements"></a>Timestamp-Anforderungen

Signierte Pakete sollten einen RFC 3161-Zeitstempel Sicherstellen der Gültigkeit der Signatur außerhalb der Gültigkeitsdauer des Zertifikats signieren Paket enthalten. Das Zertifikat zum Signieren des Zeitstempels muss gültig sein kann die `id-kp-timeStamping` Zweck [[RFC 5280 Abschnitt 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Darüber hinaus muss das Zertifikat eine RSA Länge des öffentliche Schlüssels von 2048 Bits oder höher aufweisen.

Zusätzliche technische Details finden Sie der [Paket Signatur technische Spezifikationen](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Signatur-Anforderungen für nuget.org

NuGet.org hat zusätzliche Anforderungen für das Akzeptieren eines signierten Pakets:

- Die primäre Signatur muss ein Autor-Signatur.
- Die primäre Signatur muss einen gültigen Zeitstempel an einzelnen verfügen.
- Die x. 509-Zertifikate für die Signatur der Autor und der Timestamp-Signatur:
  - Benötigen Sie einen öffentlichen RSA-Schlüssel 2048 Bits betragen.
  - Muss innerhalb seiner Gültigkeitsdauer pro aktuelle UTC-Zeit zum Zeitpunkt der paketüberprüfung auf nuget.org sein.
  - Muss mit einer vertrauenswürdigen Stammzertifizierungsstelle verkettet, die standardmäßig unter Windows als vertrauenswürdig eingestuft wird. Pakete mit selbst ausgestellte Zertifikate signiert werden zurückgewiesen.
  - Muss für den Zweck gültig: 
    - Der Autor Signaturzertifikat muss zum Signieren von Code gültig sein.
    - Der Timestamp-Zertifikat muss für Zeitstempel gültig sein.
  - Muss auf den Zeitpunkt der Signatur nicht aufgehoben werden. (Dies kann nicht zum Zeitpunkt der Übermittlung bei sein, daher nuget.org in regelmäßigen Abständen den Status der Zertifikatsperre durch erneutes).

## <a name="register-certificate-on-nugetorg"></a>Nuget.org-Zertifikat registrieren

Einreichen ein signiertes Pakets müssen Sie zuerst das Zertifikat mit nuget.org registrieren. Sie benötigen das Zertifikat als eine `.cer` in einem binären Format mit DER Datei. Sie können ein vorhandenes Zertifikat in ein Binärformat der-KODIERTE exportieren, mithilfe des Assistenten zum Exportieren von Zertifikaten.

![Zertifikatexport-Assistent](media/CertificateExportWizard.png)

Erfahrene Benutzer können die Verwendung des Zertifikats Exportieren der [Export-Certificate-PowerShell-Befehl](/powershell/module/pkiclient/export-certificate.md).

Um das Zertifikat mit nuget.org zu registrieren, wechseln Sie zu `Certificates` Abschnitt `Account settings` Seite (oder die Seite "Einstellungen" der Organisation), und wählen Sie `Register new certificate`.

![Registrierten Zertifikate](media/registered-certs.png)

> [!Tip]
> Ein Benutzer kann senden, dass mehrere Zertifikate und das gleiche Zertifikat von mehreren Benutzern registriert werden können.

Sobald ein Benutzer hat ein Zertifikat registriert, alle zukünftigen Paket Übermittlungen **müssen** mit einem der Zertifikate signiert werden.

Benutzer können auch ein registriertes Zertifikat aus dem Konto entfernen. Sobald ein Zertifikat entfernt wurde, werden mit diesem Zertifikat signierte Pakete zur Übermittlung fehlschlagen. Vorhandene Pakete sind nicht betroffen.

## <a name="configure-package-signing-requirements"></a>Konfigurieren Sie Paket signierungsanforderungen an

Wenn Sie der alleinige Besitzer eines Pakets sind, können Sie den Signaturgeber erforderlich. D. h., können Sie eines der registrierten Zertifikate zum Signieren von Paketen und an nuget.org zu senden.

Wenn ein Paket mehrere Besitzer in der Standardeinstellung verfügt, können "Beliebig" Besitzer Zertifikate zum Signieren des Pakets verwendet werden. Als eine Mitbesitzer des Pakets können Sie "Alle" mit sich selbst oder andere Mitbesitzer erforderlichen Signaturgebers werden überschreiben. Wenn Sie einen Besitzer, der nicht über eine beliebige registrierte Zertifikat verfügt vornehmen, werden nicht signierte Paketen zulässig. 

Auf ähnliche Weise, wenn der Standardwert "Alle" ausgewählt ist für ein Paket, das einen Besitzer, in dem ein registriertes Zertifikat verfügt und einen anderen Besitzer keine registrierte Zertifikat verfügt, klicken Sie dann nuget.org akzeptiert entweder ein signiertes Pakets mit einer Signatur registriert, indem Sie eine ihrer Besitzer angegeben oder einen nicht signierten-Paket (da der Besitzer keine registrierte Zertifikat besitzt).

![Paket Signaturgeber konfigurieren](media/configure-package-signers.png)
