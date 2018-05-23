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
# <a name="signed-packages"></a><span data-ttu-id="53a4f-103">Signierte Pakete</span><span class="sxs-lookup"><span data-stu-id="53a4f-103">Signed packages</span></span>

<span data-ttu-id="53a4f-104">*NuGet-4.6.0+ und Visual Studio 2017 15.6 und höher*</span><span class="sxs-lookup"><span data-stu-id="53a4f-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="53a4f-105">NuGet-Pakete können es sich um eine digitale Signatur einzuschließen, die Schutz vor manipulierte Inhalte enthält.</span><span class="sxs-lookup"><span data-stu-id="53a4f-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="53a4f-106">Diese Signatur wird aus einem x. 509-Zertifikat erzeugt, die der tatsächliche Ursprung der das Paket auch Authentizität Proofs hinzufügt.</span><span class="sxs-lookup"><span data-stu-id="53a4f-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="53a4f-107">Signierte Pakete bereitstellen die stärkste End-to-End-Überprüfung.</span><span class="sxs-lookup"><span data-stu-id="53a4f-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="53a4f-108">Eine Autor-Signatur wird sichergestellt, dass das Paket nicht geändert wurde, seit der Autor das Paket, unabhängig davon aus signiert die Repositorys oder welche Methode transport das Paket wird übermittelt.</span><span class="sxs-lookup"><span data-stu-id="53a4f-108">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="53a4f-109">Darüber hinaus bieten Autor signierte Pakete einen zusätzlichen Authentifizierungsmechanismus die publishing nuget.org-Pipeline, da das Signaturzertifikat voraus registriert werden muss.</span><span class="sxs-lookup"><span data-stu-id="53a4f-109">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="53a4f-110">Weitere Informationen finden Sie unter [Registrieren von Zertifikaten](#register-certificate-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="53a4f-110">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>

<span data-ttu-id="53a4f-111">Weitere Informationen zum Erstellen eines signierten Pakets, finden Sie unter [Signieren von Paketen](../create-packages/Sign-a-package.md) und [NuGet-Anmelde-Befehls](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="53a4f-111">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="53a4f-112">Paketsignierung wird derzeit nur bei Verwendung von nuget.exe unter Windows unterstützt.</span><span class="sxs-lookup"><span data-stu-id="53a4f-112">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="53a4f-113">Überprüfung von signierten Paketen ist derzeit nur unterstützt, wenn nuget.exe oder Visual Studio unter Windows verwenden.</span><span class="sxs-lookup"><span data-stu-id="53a4f-113">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="53a4f-114">Zertifikatanforderungen</span><span class="sxs-lookup"><span data-stu-id="53a4f-114">Certificate requirements</span></span>

<span data-ttu-id="53a4f-115">Codesignaturzertifikat anfordern, die eine besondere Art von Zertifikat ist, die für gültig ist paketsignierung erfordert die `id-kp-codeSigning` Zweck [[RFC 5280 Abschnitt 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="53a4f-115">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="53a4f-116">Darüber hinaus muss das Zertifikat eine RSA Länge des öffentliche Schlüssels von 2048 Bits oder höher aufweisen.</span><span class="sxs-lookup"><span data-stu-id="53a4f-116">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="53a4f-117">Erhalten Sie ein Codesignaturzertifikat</span><span class="sxs-lookup"><span data-stu-id="53a4f-117">Get a code signing certificate</span></span>

<span data-ttu-id="53a4f-118">Gültige Zertifikate können von einer öffentlichen Zertifizierungsstelle wie abgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="53a4f-118">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="53a4f-119">Symantec</span><span class="sxs-lookup"><span data-stu-id="53a4f-119">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="53a4f-120">DigiCert</span><span class="sxs-lookup"><span data-stu-id="53a4f-120">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="53a4f-121">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="53a4f-121">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="53a4f-122">Globale anmelden</span><span class="sxs-lookup"><span data-stu-id="53a4f-122">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="53a4f-123">Comodo</span><span class="sxs-lookup"><span data-stu-id="53a4f-123">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="53a4f-124">Certum</span><span class="sxs-lookup"><span data-stu-id="53a4f-124">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="53a4f-125">Die vollständige Liste der Zertifizierungsstellen von Windows als vertrauenswürdig eingestuft erhalten von [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="53a4f-125">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="53a4f-126">Ein Testzertifikat erstellen</span><span class="sxs-lookup"><span data-stu-id="53a4f-126">Create a test certificate</span></span>

<span data-ttu-id="53a4f-127">Sie können selbst ausgestellte Zertifikate für Testzwecke verwenden.</span><span class="sxs-lookup"><span data-stu-id="53a4f-127">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="53a4f-128">Verwenden Sie zum Erstellen eines selbst ausgegebenen Zertifikats die [New-SelfSignedCertificate-PowerShell-Befehl](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="53a4f-128">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="53a4f-129">Dieser Befehl erstellt ein Testzertifikats verfügbar im persönlichen Zertifikatspeicher des aktuellen Benutzers.</span><span class="sxs-lookup"><span data-stu-id="53a4f-129">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="53a4f-130">Sie können den Zertifikatspeicher öffnen, indem ausgeführt `certmgr.msc` des neu erstellten Zertifikats angezeigt.</span><span class="sxs-lookup"><span data-stu-id="53a4f-130">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="53a4f-131">NuGet.org akzeptiert keine Pakete mit selbst ausgestellte Zertifikate signiert.</span><span class="sxs-lookup"><span data-stu-id="53a4f-131">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="53a4f-132">Timestamp-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="53a4f-132">Timestamp requirements</span></span>

<span data-ttu-id="53a4f-133">Signierte Pakete sollten einen RFC 3161-Zeitstempel Sicherstellen der Gültigkeit der Signatur außerhalb der Gültigkeitsdauer des Zertifikats signieren Paket enthalten.</span><span class="sxs-lookup"><span data-stu-id="53a4f-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="53a4f-134">Das Zertifikat zum Signieren des Zeitstempels muss gültig sein kann die `id-kp-timeStamping` Zweck [[RFC 5280 Abschnitt 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="53a4f-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="53a4f-135">Darüber hinaus muss das Zertifikat eine RSA Länge des öffentliche Schlüssels von 2048 Bits oder höher aufweisen.</span><span class="sxs-lookup"><span data-stu-id="53a4f-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="53a4f-136">Zusätzliche technische Details finden Sie der [Paket Signatur technische Spezifikationen](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="53a4f-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="53a4f-137">Signatur-Anforderungen für nuget.org</span><span class="sxs-lookup"><span data-stu-id="53a4f-137">Signature requirements on nuget.org</span></span>

<span data-ttu-id="53a4f-138">NuGet.org hat zusätzliche Anforderungen für das Akzeptieren eines signierten Pakets:</span><span class="sxs-lookup"><span data-stu-id="53a4f-138">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="53a4f-139">Die primäre Signatur muss ein Autor-Signatur.</span><span class="sxs-lookup"><span data-stu-id="53a4f-139">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="53a4f-140">Die primäre Signatur muss einen gültigen Zeitstempel an einzelnen verfügen.</span><span class="sxs-lookup"><span data-stu-id="53a4f-140">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="53a4f-141">Die x. 509-Zertifikate für die Signatur der Autor und der Timestamp-Signatur:</span><span class="sxs-lookup"><span data-stu-id="53a4f-141">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="53a4f-142">Benötigen Sie einen öffentlichen RSA-Schlüssel 2048 Bits betragen.</span><span class="sxs-lookup"><span data-stu-id="53a4f-142">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="53a4f-143">Muss innerhalb seiner Gültigkeitsdauer pro aktuelle UTC-Zeit zum Zeitpunkt der paketüberprüfung auf nuget.org sein.</span><span class="sxs-lookup"><span data-stu-id="53a4f-143">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="53a4f-144">Muss mit einer vertrauenswürdigen Stammzertifizierungsstelle verkettet, die standardmäßig unter Windows als vertrauenswürdig eingestuft wird.</span><span class="sxs-lookup"><span data-stu-id="53a4f-144">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="53a4f-145">Pakete mit selbst ausgestellte Zertifikate signiert werden zurückgewiesen.</span><span class="sxs-lookup"><span data-stu-id="53a4f-145">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="53a4f-146">Muss für den Zweck gültig:</span><span class="sxs-lookup"><span data-stu-id="53a4f-146">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="53a4f-147">Der Autor Signaturzertifikat muss zum Signieren von Code gültig sein.</span><span class="sxs-lookup"><span data-stu-id="53a4f-147">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="53a4f-148">Der Timestamp-Zertifikat muss für Zeitstempel gültig sein.</span><span class="sxs-lookup"><span data-stu-id="53a4f-148">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="53a4f-149">Muss auf den Zeitpunkt der Signatur nicht aufgehoben werden.</span><span class="sxs-lookup"><span data-stu-id="53a4f-149">Must not be revoked at signing time.</span></span> <span data-ttu-id="53a4f-150">(Dies kann nicht zum Zeitpunkt der Übermittlung bei sein, daher nuget.org in regelmäßigen Abständen den Status der Zertifikatsperre durch erneutes).</span><span class="sxs-lookup"><span data-stu-id="53a4f-150">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="53a4f-151">Nuget.org-Zertifikat registrieren</span><span class="sxs-lookup"><span data-stu-id="53a4f-151">Register certificate on nuget.org</span></span>

<span data-ttu-id="53a4f-152">Einreichen ein signiertes Pakets müssen Sie zuerst das Zertifikat mit nuget.org registrieren. Sie benötigen das Zertifikat als eine `.cer` in einem binären Format mit DER Datei.</span><span class="sxs-lookup"><span data-stu-id="53a4f-152">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="53a4f-153">Sie können ein vorhandenes Zertifikat in ein Binärformat der-KODIERTE exportieren, mithilfe des Assistenten zum Exportieren von Zertifikaten.</span><span class="sxs-lookup"><span data-stu-id="53a4f-153">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![Zertifikatexport-Assistent](media/CertificateExportWizard.png)

<span data-ttu-id="53a4f-155">Erfahrene Benutzer können die Verwendung des Zertifikats Exportieren der [Export-Certificate-PowerShell-Befehl](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="53a4f-155">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="53a4f-156">Um das Zertifikat mit nuget.org zu registrieren, wechseln Sie zu `Certificates` Abschnitt `Account settings` Seite (oder die Seite "Einstellungen" der Organisation), und wählen Sie `Register new certificate`.</span><span class="sxs-lookup"><span data-stu-id="53a4f-156">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![Registrierten Zertifikate](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="53a4f-158">Ein Benutzer kann senden, dass mehrere Zertifikate und das gleiche Zertifikat von mehreren Benutzern registriert werden können.</span><span class="sxs-lookup"><span data-stu-id="53a4f-158">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="53a4f-159">Sobald ein Benutzer hat ein Zertifikat registriert, alle zukünftigen Paket Übermittlungen **müssen** mit einem der Zertifikate signiert werden.</span><span class="sxs-lookup"><span data-stu-id="53a4f-159">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="53a4f-160">Benutzer können auch ein registriertes Zertifikat aus dem Konto entfernen.</span><span class="sxs-lookup"><span data-stu-id="53a4f-160">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="53a4f-161">Sobald ein Zertifikat entfernt wurde, werden mit diesem Zertifikat signierte Pakete zur Übermittlung fehlschlagen.</span><span class="sxs-lookup"><span data-stu-id="53a4f-161">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="53a4f-162">Vorhandene Pakete sind nicht betroffen.</span><span class="sxs-lookup"><span data-stu-id="53a4f-162">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="53a4f-163">Konfigurieren Sie Paket signierungsanforderungen an</span><span class="sxs-lookup"><span data-stu-id="53a4f-163">Configure package signing requirements</span></span>

<span data-ttu-id="53a4f-164">Wenn Sie der alleinige Besitzer eines Pakets sind, können Sie den Signaturgeber erforderlich.</span><span class="sxs-lookup"><span data-stu-id="53a4f-164">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="53a4f-165">D. h., können Sie eines der registrierten Zertifikate zum Signieren von Paketen und an nuget.org zu senden.</span><span class="sxs-lookup"><span data-stu-id="53a4f-165">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="53a4f-166">Wenn ein Paket mehrere Besitzer in der Standardeinstellung verfügt, können "Beliebig" Besitzer Zertifikate zum Signieren des Pakets verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="53a4f-166">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="53a4f-167">Als eine Mitbesitzer des Pakets können Sie "Alle" mit sich selbst oder andere Mitbesitzer erforderlichen Signaturgebers werden überschreiben.</span><span class="sxs-lookup"><span data-stu-id="53a4f-167">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="53a4f-168">Wenn Sie einen Besitzer, der nicht über eine beliebige registrierte Zertifikat verfügt vornehmen, werden nicht signierte Paketen zulässig.</span><span class="sxs-lookup"><span data-stu-id="53a4f-168">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="53a4f-169">Auf ähnliche Weise, wenn der Standardwert "Alle" ausgewählt ist für ein Paket, das einen Besitzer, in dem ein registriertes Zertifikat verfügt und einen anderen Besitzer keine registrierte Zertifikat verfügt, klicken Sie dann nuget.org akzeptiert entweder ein signiertes Pakets mit einer Signatur registriert, indem Sie eine ihrer Besitzer angegeben oder einen nicht signierten-Paket (da der Besitzer keine registrierte Zertifikat besitzt).</span><span class="sxs-lookup"><span data-stu-id="53a4f-169">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![Paket Signaturgeber konfigurieren](media/configure-package-signers.png)
