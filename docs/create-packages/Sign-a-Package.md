---
title: Signieren von NuGet-Paketen
description: Informationen zur Verwendung von signierten Paketen zur Aktivierung der Integritätsüberprüfung des Inhalts.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: c0622520a325000d5fcb8fb884cb509ee4b641f4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901901"
---
# <a name="signing-nuget-packages"></a>Signieren von NuGet-Paketen

Signierte Pakete ermöglichen die Überprüfung der Integrität von Inhalten, um Inhalte vor Manipulation zu schützen. Die Paketsignatur dient auch als zentrale, vertrauenswürdige Informationsquelle in Bezug auf die tatsächliche Herkunft eines Pakets und stärkt das Vertrauen des Verbrauchers in die Echtheit des Pakets. In diesem Leitfaden wird vorausgesetzt, dass Sie bereits [ein Paket erstellt haben](creating-a-package.md).

## <a name="get-a-code-signing-certificate"></a>Abrufen eines Codesignaturzertifikats

Gültige Zertifikate können von einer öffentlichen Zertifizierungsstelle wie [DigiCert](https://www.digicert.com/code-signing/), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) usw. abgerufen werden. Die vollständige Liste der Zertifizierungsstellen, die von Windows als vertrauenswürdig eingestuft werden, finden Sie unter [http://aka.ms/trustcertpartners](/security/trusted-root/participants-list).

Sie können selbst ausgestellte Zertifikate für Testzwecke verwenden. Pakete, die mit selbst ausgestellten Zertifikaten signiert wurden, werden jedoch von NuGet.org nicht akzeptiert. Weitere Informationen zum [Erstellen eines Testzertifikats](#create-a-test-certificate).

## <a name="export-the-certificate-file"></a>Exportieren der Zertifikatdatei

* Sie können ein vorhandenes Zertifikat mithilfe des Zertifikatexport-Assistenten in ein binäres DER-Format exportieren.

  ![Zertifikatexport-Assistent](../reference/media/CertificateExportWizard.png)

* Sie können das Zertifikat auch mithilfe des [PowerShell-Befehls „Export-Certificate“](/powershell/module/pkiclient/export-certificate) exportieren.

## <a name="sign-the-package"></a>Signieren des Pakets

> [!note]
> Erfordert nuget.exe 4.6.0 oder höher. dotnet.exe-Unterstützung ist in Kürze verfügbar – [#7939](https://github.com/NuGet/Home/issues/7939)

Signieren Sie das Paket mithilfe von [nuget sign](../reference/cli-reference/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> Der Zertifikatanbieter stellt häufig auch eine Zeitstempelserver-URL bereit, die Sie für das oben gezeigte optionale Argument `Timestamper` verwenden können. Informieren Sie sich über diese Dienst-URL anhand der Dokumentation Ihres Anbieters und/oder über dessen Support.

* Sie können ein im Zertifikatspeicher verfügbares Zertifikat oder ein Zertifikat aus einer Datei verwenden. Informationen zu [nuget sign](../reference/cli-reference/cli-ref-sign.md) finden Sie in der Referenz der Befehlszeilenschnittstelle.
* Signierte Pakete sollten einen Zeitstempel enthalten, um sicherzustellen, dass die Signatur gültig bleibt, wenn das Signaturzertifikat abläuft. Andernfalls erzeugt der Signierungsvorgang eine [Warnung](../reference/errors-and-warnings/NU3002.md).
* Sie können Details der Signatur eines bestimmten Pakets mit dem [NuGet-Befehl „verify“](../reference/cli-reference/cli-ref-verify.md) anzeigen.

## <a name="register-the-certificate-on-nugetorg"></a>Registrieren des Zertifikats bei NuGet.org

Um ein signiertes Paket zu veröffentlichen, müssen Sie das Zertifikat zunächst bei NuGet.org registrieren. Sie benötigen das Zertifikat als `.cer`-Datei im binären DER-Format.

1. [Melden Sie sich](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) bei NuGet.org an.
1. Wechseln Sie zu `Account settings` (oder `Manage Organization` **>** `Edit Organization`, wenn Sie das Zertifikat für ein Organisationskonto registrieren möchten).
1. Erweitern Sie den Abschnitt `Certificates`, und wählen Sie `Register new` aus.
1. Suchen Sie nach der zuvor exportierten Zertifikatdatei, und wählen Sie sie aus.
  ![Registrierte Zertifikate](../reference/media/registered-certs.png)

**Hinweis**
* Ein Benutzer kann mehrere Zertifikate übermitteln, und ein und dasselbe Zertifikat kann von mehreren Benutzern registriert werden.
* Sobald ein Zertifikat für einen Benutzer registriert wurde, **müssen** alle zukünftigen Pakete mit einem der Zertifikate angemeldet werden. Siehe [Verwalten der Signaturanforderungen für Ihr Paket auf NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)
* Benutzer können ein registriertes Zertifikat auch aus dem Konto entfernen. Sobald ein Zertifikat entfernt wurde, tritt bei neuen Paketen, die mit diesem Zertifikat signiert wurden, ein Fehler auf. Vorhandene Pakete sind nicht betroffen.

## <a name="publish-the-package"></a>Veröffentlichen des Pakets

Sie können das Paket jetzt auf NuGet.org veröffentlichen. Siehe [Veröffentlichen von Paketen](../nuget-org/Publish-a-package.md).

## <a name="create-a-test-certificate"></a>Erstellen eines Testzertifikats

Sie können selbst ausgestellte Zertifikate für Testzwecke verwenden. Um ein selbst ausgestelltes Zertifikat zu erstellen, verwenden Sie den [PowerShell-Befehl „New-SelfSignedCertificate“](/powershell/module/pkiclient/new-selfsignedcertificate).

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

Dieser Befehl erstellt ein Testzertifikat, das im persönlichen Zertifikatspeicher des aktuellen Benutzers gespeichert wird. Sie können den Zertifikatspeicher durch Ausführen von `certmgr.msc` öffnen, um das neu erstellte Zertifikat anzuzeigen.

> [!Warning]
> NuGet.org akzeptiert keine Pakete, die mit selbst ausgestellten Zertifikaten signiert sind.

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>Verwalten der Signaturanforderungen für Ihr Paket auf NuGet.org
1. [Melden Sie sich](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) bei NuGet.org an.

1. Wechseln Sie zu `Manage Packages`. 
   ![Paketsignierer konfigurieren](../reference/media/configure-package-signers.png)

* Wenn Sie der einzige Besitzer eines Pakets sind, sind Sie der erforderliche Signaturgeber, d.h., Sie können ein beliebiges der registrierten Zertifikate verwenden, um Ihre Pakete in NuGet.org zu signieren und zu veröffentlichen.

* Wenn ein Paket über mehrere Besitzer verfügt, können standardmäßig die Zertifikate „jedes“ Besitzers zum Signieren des Pakets verwendet werden. Als Mitbesitzer des Pakets können Sie „Jeder“ außer Kraft setzen und sich selbst oder einen beliebigen Mitbesitzer als erforderlichen Signaturgeber festlegen. Wenn Sie einen Besitzer angeben, für den kein Zertifikat registriert ist, werden nicht signierte Pakete zugelassen. 

* Ähnliches gilt, wenn die Standardoption „Jeder“ für ein Paket ausgewählt wurde, für das ein Besitzer ein Zertifikat registriert hat, ein anderer Besitzer jedoch nicht: NuGet.org akzeptiert entweder ein signiertes Paket mit einer von einem der Besitzer registrierten Signatur oder ein nicht signiertes Paket (da für einen der Besitzer kein Zertifikat registriert wurde).

## <a name="related-articles"></a>Verwandte Artikel

- [Verwalten von Paketvertrauensgrenzen](../consume-packages/installing-signed-packages.md)
- [Referenz für signierte Pakete](../reference/Signed-Packages-Reference.md)
