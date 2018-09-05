---
title: Signierte Pakete
description: Anforderungen zum Signieren von NuGet-Paket.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c36db9486ad787f19430c75fc38a2e9dd8ba6e37
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550420"
---
# <a name="signed-packages"></a><span data-ttu-id="a3317-103">Signierte Pakete</span><span class="sxs-lookup"><span data-stu-id="a3317-103">Signed packages</span></span>

<span data-ttu-id="a3317-104">*NuGet 4.6.0+ und Visual Studio 2017 Version 15.6 und höher*</span><span class="sxs-lookup"><span data-stu-id="a3317-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="a3317-105">NuGet-Paketen können es sich um eine digitale Signatur enthalten, die Schutz vor manipulierte Inhalte bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="a3317-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="a3317-106">Diese Signatur wird aus einem x. 509-Zertifikat erstellt, die die eigentliche Quelle des Pakets auch Authentizität Nachweise hinzufügt.</span><span class="sxs-lookup"><span data-stu-id="a3317-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="a3317-107">Signierte Pakete bereitstellen die stärkste End-to-End-Überprüfung.</span><span class="sxs-lookup"><span data-stu-id="a3317-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="a3317-108">Es gibt zwei verschiedene Arten von NuGet-Signaturen:</span><span class="sxs-lookup"><span data-stu-id="a3317-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="a3317-109">**Erstellen der Signatur**.</span><span class="sxs-lookup"><span data-stu-id="a3317-109">**Author Signature**.</span></span> <span data-ttu-id="a3317-110">Eine Autor-Signatur wird sichergestellt, dass das Paket nicht geändert wurde, seit der Autor signiert das Paket, unabhängig davon aus dem Repository, oder welche Methode transport wird das Paket bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="a3317-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="a3317-111">Darüber hinaus bieten Autor signierte Pakete einen zusätzlichen Authentifizierungsmechanismus für die Veröffentlichung nuget.org-Pipeline aus, da das Signaturzertifikat vorab registriert werden muss.</span><span class="sxs-lookup"><span data-stu-id="a3317-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="a3317-112">Weitere Informationen finden Sie unter [Registrieren von Zertifikaten](#register-certificate-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="a3317-112">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>
- <span data-ttu-id="a3317-113">**Repository-Signatur**.</span><span class="sxs-lookup"><span data-stu-id="a3317-113">**Repository Signature**.</span></span> <span data-ttu-id="a3317-114">Repository-Signaturen bieten eine Garantie der Integrität für **alle** Pakete in einem Repository, ob diese Autor signiert oder unsigniert, sind, auch wenn diese Pakete aus einem anderen Ort als das ursprüngliche Repository abgerufen werden, in denen sie waren, signiert.</span><span class="sxs-lookup"><span data-stu-id="a3317-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="a3317-115">Ausführliche Informationen zum Erstellen eines signierten Autor-Pakets, finden Sie unter [Pakete signieren](../create-packages/Sign-a-package.md) und [Nuget-anmelden-Befehl](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="a3317-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="a3317-116">Paketsignierung wird derzeit nur bei Verwendung von nuget.exe auf Windows unterstützt.</span><span class="sxs-lookup"><span data-stu-id="a3317-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="a3317-117">Überprüfung von signierten Paketen werden derzeit nur bei Verwendung von nuget.exe- oder Visual Studio für Windows.</span><span class="sxs-lookup"><span data-stu-id="a3317-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="a3317-118">Zertifikatanforderungen</span><span class="sxs-lookup"><span data-stu-id="a3317-118">Certificate requirements</span></span>

<span data-ttu-id="a3317-119">Paketsignierung erfordert ein Codesignaturzertifikat, der eine besondere Art von Zertifikat ist, für ungültig ist, die `id-kp-codeSigning` Zweck [[RFC 5280 Abschnitt 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="a3317-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="a3317-120">Darüber hinaus muss das Zertifikat eine RSA Länge des öffentliche Schlüssels von 2048 Bits oder höher aufweisen.</span><span class="sxs-lookup"><span data-stu-id="a3317-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="a3317-121">Erhalten Sie ein Codesignaturzertifikat</span><span class="sxs-lookup"><span data-stu-id="a3317-121">Get a code signing certificate</span></span>

<span data-ttu-id="a3317-122">Gültige Zertifikate können von einer öffentlichen Zertifizierungsstelle wie abgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="a3317-122">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="a3317-123">Symantec</span><span class="sxs-lookup"><span data-stu-id="a3317-123">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="a3317-124">DigiCert</span><span class="sxs-lookup"><span data-stu-id="a3317-124">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="a3317-125">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="a3317-125">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="a3317-126">Globale anmelden</span><span class="sxs-lookup"><span data-stu-id="a3317-126">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="a3317-127">Comodo</span><span class="sxs-lookup"><span data-stu-id="a3317-127">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="a3317-128">Certum</span><span class="sxs-lookup"><span data-stu-id="a3317-128">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="a3317-129">Die vollständige Liste der Zertifizierungsstellen, die von Windows als vertrauenswürdig eingestuft erhalten Sie vom [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="a3317-129">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="a3317-130">Ein Testzertifikat erstellen</span><span class="sxs-lookup"><span data-stu-id="a3317-130">Create a test certificate</span></span>

<span data-ttu-id="a3317-131">Sie können selbst ausgestellte Zertifikate verwenden, zu Testzwecken.</span><span class="sxs-lookup"><span data-stu-id="a3317-131">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="a3317-132">Verwenden Sie zum Erstellen eines selbst ausgegebenen Zertifikats die [New-SelfSignedCertificate-PowerShell-Befehl](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="a3317-132">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="a3317-133">Dieser Befehl erstellt ein Test-Zertifikat verfügbar im persönlichen Zertifikatspeicher des aktuellen Benutzers.</span><span class="sxs-lookup"><span data-stu-id="a3317-133">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="a3317-134">Öffnen Sie den Zertifikatspeicher, indem Sie mit `certmgr.msc` um das neu erstellte Zertifikat anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="a3317-134">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="a3317-135">"NuGet.org" akzeptiert keine Pakete mit selbst ausgestellte Zertifikate signiert.</span><span class="sxs-lookup"><span data-stu-id="a3317-135">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="a3317-136">Zeitstempel-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="a3317-136">Timestamp requirements</span></span>

<span data-ttu-id="a3317-137">Signierte Pakete sollten einen Zeitstempel RFC 3161 Sicherstellen der Gültigkeit der Signatur über das Paket Signieren der Gültigkeitszeitraum des Zertifikats enthalten.</span><span class="sxs-lookup"><span data-stu-id="a3317-137">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="a3317-138">Das Zertifikat zum Signieren des Zeitstempels muss für die `id-kp-timeStamping` Zweck [[RFC 5280 Abschnitt 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="a3317-138">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="a3317-139">Darüber hinaus muss das Zertifikat eine RSA Länge des öffentliche Schlüssels von 2048 Bits oder höher aufweisen.</span><span class="sxs-lookup"><span data-stu-id="a3317-139">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="a3317-140">Zusätzliche technische Details finden Sie in der [Paket Signatur technische Spezifikationen](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="a3317-140">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="a3317-141">Signatur-Anforderungen auf nuget.org</span><span class="sxs-lookup"><span data-stu-id="a3317-141">Signature requirements on nuget.org</span></span>

<span data-ttu-id="a3317-142">"NuGet.org" verfügt über zusätzliche Anforderungen für das Akzeptieren eines signierten Pakets:</span><span class="sxs-lookup"><span data-stu-id="a3317-142">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="a3317-143">Die primäre Signatur muss eine Signatur erstellen.</span><span class="sxs-lookup"><span data-stu-id="a3317-143">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="a3317-144">Die primäre Signatur muss einen einzigen gültigen Zeitstempel haben.</span><span class="sxs-lookup"><span data-stu-id="a3317-144">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="a3317-145">Die x. 509-Zertifikate für die Signatur der Autor und der Timestamp-Signatur:</span><span class="sxs-lookup"><span data-stu-id="a3317-145">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="a3317-146">Benötigen Sie einen öffentlichen RSA-Schlüssel 2048 Bits betragen.</span><span class="sxs-lookup"><span data-stu-id="a3317-146">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="a3317-147">Muss innerhalb seiner Gültigkeitsdauer pro aktuelle UTC-Zeit zum Zeitpunkt der paketüberprüfung auf nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a3317-147">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="a3317-148">Muss mit einer vertrauenswürdigen Stammzertifizierungsstelle verkettet, die standardmäßig unter Windows als vertrauenswürdig eingestuft wird.</span><span class="sxs-lookup"><span data-stu-id="a3317-148">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="a3317-149">Pakete, die mit selbst ausgestellte Zertifikate signiert werden abgelehnt.</span><span class="sxs-lookup"><span data-stu-id="a3317-149">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="a3317-150">Gültig muss für den Zweck:</span><span class="sxs-lookup"><span data-stu-id="a3317-150">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="a3317-151">Der Autor Signaturzertifikat muss zum Signieren von Code gültig sein.</span><span class="sxs-lookup"><span data-stu-id="a3317-151">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="a3317-152">Der Timestamp-Zertifikat muss für Zeitstempel gültig sein.</span><span class="sxs-lookup"><span data-stu-id="a3317-152">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="a3317-153">Muss auf den Zeitpunkt der Signatur nicht widerrufen werden.</span><span class="sxs-lookup"><span data-stu-id="a3317-153">Must not be revoked at signing time.</span></span> <span data-ttu-id="a3317-154">(Diese zum Zeitpunkt der Einreichung bei möglicherweise nicht so, dass nuget.org in regelmäßigen Abständen den Status der Zertifikatsperre dann nachkontrolliert).</span><span class="sxs-lookup"><span data-stu-id="a3317-154">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="a3317-155">Registrieren des Zertifikats auf nuget.org</span><span class="sxs-lookup"><span data-stu-id="a3317-155">Register certificate on nuget.org</span></span>

<span data-ttu-id="a3317-156">Zum Absenden eines signierten Pakets müssen Sie zuerst das Zertifikat mit "NuGet.org" registrieren. Sie benötigen das Zertifikat als eine `.cer` Datei in einem binären Format mit DER.</span><span class="sxs-lookup"><span data-stu-id="a3317-156">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="a3317-157">Sie können ein vorhandenes Zertifikat auf ein binäres Format für die DER mit den Zertifikatexport-Assistenten exportieren.</span><span class="sxs-lookup"><span data-stu-id="a3317-157">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![Zertifikatexport-Assistent](media/CertificateExportWizard.png)

<span data-ttu-id="a3317-159">Fortgeschrittene Benutzer können exportieren das Zertifikat mit dem [Export-Certificate-PowerShell-Befehl](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="a3317-159">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="a3317-160">Um das Zertifikat für "NuGet.org" zu registrieren, wechseln Sie zu `Certificates` Abschnitt `Account settings` Seite (oder der Organisation Seite "Einstellungen"), und wählen Sie `Register new certificate`.</span><span class="sxs-lookup"><span data-stu-id="a3317-160">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![Registrierten Zertifikate](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="a3317-162">Ein Benutzer kann zu übermitteln, dass mehrere Zertifikate und das gleiche Zertifikat von mehreren Benutzern registriert werden können.</span><span class="sxs-lookup"><span data-stu-id="a3317-162">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="a3317-163">Sobald ein Benutzer hat ein Zertifikat registriert, alle zukünftigen Paket Übermittlungen **müssen** mit einem der Zertifikate signiert werden.</span><span class="sxs-lookup"><span data-stu-id="a3317-163">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="a3317-164">Benutzer können auch ein registriertes Zertifikat aus dem Konto entfernen.</span><span class="sxs-lookup"><span data-stu-id="a3317-164">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="a3317-165">Sobald ein Zertifikat entfernt wurde, können Sie Pakete, die mit diesem Zertifikat signiert zur Übermittlung fehlschlagen.</span><span class="sxs-lookup"><span data-stu-id="a3317-165">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="a3317-166">Vorhandene Pakete sind nicht betroffen.</span><span class="sxs-lookup"><span data-stu-id="a3317-166">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="a3317-167">Konfigurieren Sie Paket Signieren von Anforderungen</span><span class="sxs-lookup"><span data-stu-id="a3317-167">Configure package signing requirements</span></span>

<span data-ttu-id="a3317-168">Wenn Sie der alleinige Eigentümer eines Pakets sind, können Sie den erforderlichen Signaturgeber.</span><span class="sxs-lookup"><span data-stu-id="a3317-168">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="a3317-169">D. h., können Sie eines der registrierten Zertifikate zum Signieren von Paketen und auf nuget.org zu übermitteln.</span><span class="sxs-lookup"><span data-stu-id="a3317-169">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="a3317-170">Wenn ein Paket mehrere Besitzer fest, in der Standardeinstellung verfügt, können "Any" des Besitzers Zertifikate zum Signieren des Pakets verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="a3317-170">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="a3317-171">Als Mitbesitzer des Pakets können Sie "Any" für sich selbst oder andere Mitbesitzer den Signaturgeber erforderlich sein überschreiben.</span><span class="sxs-lookup"><span data-stu-id="a3317-171">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="a3317-172">Wenn Sie als Besitzer, der nicht über eine beliebige registrierte Zertifikat verfügt festlegen, werden nicht signierte Paketen zugelassen.</span><span class="sxs-lookup"><span data-stu-id="a3317-172">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="a3317-173">Auf ähnliche Weise die Standardeinstellung "Alle" ausgewählt ist für ein Paket, die einen Besitzer, in denen ein registriertes Zertifikat hat und einen anderen Besitzer keine registrierte Zertifikat verfügt, klicken Sie dann "NuGet.org" akzeptiert entweder ein signiertes Pakets mit einer Signatur, die von einer ihrer Besitzer registriert oder eine nicht signierte Paket (da der Besitzer keine registrierte Zertifikat besitzt).</span><span class="sxs-lookup"><span data-stu-id="a3317-173">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![Konfigurieren Sie die Paket-Signaturgeber](media/configure-package-signers.png)
