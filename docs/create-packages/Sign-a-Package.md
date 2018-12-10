---
title: Signieren von NuGet-Paketen
description: Informationen zur Verwendung von signierten Paketen zur Aktivierung der Integritätsüberprüfung des Inhalts.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e8955f9d46bab235c8755d5654814a4291d542d6
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977562"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="ecac4-103">Signieren von NuGet-Paketen</span><span class="sxs-lookup"><span data-stu-id="ecac4-103">Signing NuGet Packages</span></span>

<span data-ttu-id="ecac4-104">Signierte Pakete ermöglichen die Überprüfung der Integrität von Inhalten, um Inhalte vor Manipulation zu schützen.</span><span class="sxs-lookup"><span data-stu-id="ecac4-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="ecac4-105">Die Paketsignatur dient auch als zentrale, vertrauenswürdige Informationsquelle in Bezug auf die tatsächliche Herkunft eines Pakets und stärkt das Vertrauen des Verbrauchers in die Echtheit des Pakets.</span><span class="sxs-lookup"><span data-stu-id="ecac4-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="ecac4-106">In diesem Leitfaden wird vorausgesetzt, dass Sie bereits [ein Paket erstellt haben](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="ecac4-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="ecac4-107">Abrufen eines Codesignaturzertifikats</span><span class="sxs-lookup"><span data-stu-id="ecac4-107">Get a code signing certificate</span></span>

<span data-ttu-id="ecac4-108">Gültige Zertifikate können von öffentlichen Zertifizierungsstellen wie [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) usw. abgerufen werden. Die vollständige Liste aller von Windows als vertrauenswürdig eingestuften Zertifizierungsstellen finden Sie unter [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="ecac4-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="ecac4-109">Sie können selbst ausgestellte Zertifikate für Testzwecke verwenden.</span><span class="sxs-lookup"><span data-stu-id="ecac4-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="ecac4-110">Pakete, die mit selbst ausgestellten Zertifikaten signiert wurde, werden allerdings von NuGet.org nicht akzeptiert. Weitere Informationen zum [Erstellen einer variablen Gruppe](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="ecac4-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="ecac4-111">Exportieren der Zertifikatdatei</span><span class="sxs-lookup"><span data-stu-id="ecac4-111">Export the certificate file</span></span>

* <span data-ttu-id="ecac4-112">Sie können ein vorhandenes Zertifikat mithilfe des Zertifikatexport-Assistenten in ein binäres DER-Format exportieren.</span><span class="sxs-lookup"><span data-stu-id="ecac4-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Zertifikatexport-Assistent](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="ecac4-114">Sie können das Zertifikat auch mithilfe des [PowerShell-Befehls „Export-Certificate“](/powershell/module/pkiclient/export-certificate.md) exportieren.</span><span class="sxs-lookup"><span data-stu-id="ecac4-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="ecac4-115">Signieren des Pakets</span><span class="sxs-lookup"><span data-stu-id="ecac4-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="ecac4-116">Erfordert nuget.exe 4.6.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="ecac4-116">Requires nuget.exe 4.6.0 or later</span></span>

<span data-ttu-id="ecac4-117">Signieren Sie das Paket mithilfe von [nuget sign](../tools/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="ecac4-117">Sign the package using [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateFilePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

* <span data-ttu-id="ecac4-118">Sie können ein im Zertifikatspeicher verfügbares Zertifikat oder ein Zertifikat aus einer Datei verwenden.</span><span class="sxs-lookup"><span data-stu-id="ecac4-118">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="ecac4-119">Informationen zu [nuget sign](../tools/cli-ref-sign.md) finden Sie in der Referenz der Befehlszeilenschnittstelle.</span><span class="sxs-lookup"><span data-stu-id="ecac4-119">See CLI reference for [nuget sign](../tools/cli-ref-sign.md).</span></span>
* <span data-ttu-id="ecac4-120">Signierte Pakete sollten einen Zeitstempel enthalten, um sicherzustellen, dass die Signatur gültig bleibt, wenn das Signaturzertifikat abläuft.</span><span class="sxs-lookup"><span data-stu-id="ecac4-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="ecac4-121">Andernfalls erzeugt der Signierungsvorgang eine [Warnung](../reference/errors-and-warnings/NU3002.md).</span><span class="sxs-lookup"><span data-stu-id="ecac4-121">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="ecac4-122">Sie können Details der Signatur eines bestimmten Pakets mit dem [NuGet-Befehl „verify“](../tools/cli-ref-verify.md) anzeigen.</span><span class="sxs-lookup"><span data-stu-id="ecac4-122">You can see the signature details of a given package using [nuget verify](../tools/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="ecac4-123">Registrieren des Zertifikats bei NuGet.org</span><span class="sxs-lookup"><span data-stu-id="ecac4-123">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="ecac4-124">Um ein signiertes Paket zu veröffentlichen, müssen Sie das Zertifikat zuerst bei NuGet.org registrieren. Sie benötigen das Zertifikat als `.cer`-Datei in einem binären DER-Format.</span><span class="sxs-lookup"><span data-stu-id="ecac4-124">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="ecac4-125">[Melden Sie sich](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) bei NuGet.org an.</span><span class="sxs-lookup"><span data-stu-id="ecac4-125">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="ecac4-126">Wechseln Sie zu `Account settings` (oder `Manage Organization` **>** `Edit Organziation`, wenn Sie das Zertifikat für ein Organisationskonto registrieren möchten).</span><span class="sxs-lookup"><span data-stu-id="ecac4-126">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="ecac4-127">Erweitern Sie den Abschnitt `Certificates`, und wählen Sie `Register new` aus.</span><span class="sxs-lookup"><span data-stu-id="ecac4-127">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="ecac4-128">Suchen Sie nach der zuvor exportierten Zertifikatdatei, und wählen Sie sie aus.</span><span class="sxs-lookup"><span data-stu-id="ecac4-128">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="ecac4-129">![Registrierte Zertifikate](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="ecac4-129">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="ecac4-130">**Hinweis**</span><span class="sxs-lookup"><span data-stu-id="ecac4-130">**Note**</span></span>
* <span data-ttu-id="ecac4-131">Ein Benutzer kann mehrere Zertifikate übermitteln, und ein und dasselbe Zertifikat kann von mehreren Benutzern registriert werden.</span><span class="sxs-lookup"><span data-stu-id="ecac4-131">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="ecac4-132">Sobald ein Zertifikat für einen Benutzer registriert wurde, **müssen** alle zukünftigen Pakete mit einem der Zertifikate angemeldet werden.</span><span class="sxs-lookup"><span data-stu-id="ecac4-132">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="ecac4-133">Siehe [Verwalten der Signaturanforderungen für Ihr Paket auf NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="ecac4-133">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="ecac4-134">Benutzer können ein registriertes Zertifikat auch aus dem Konto entfernen.</span><span class="sxs-lookup"><span data-stu-id="ecac4-134">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="ecac4-135">Sobald ein Zertifikat entfernt wurde, tritt bei neuen Paketen, die mit diesem Zertifikat signiert wurden, ein Fehler auf.</span><span class="sxs-lookup"><span data-stu-id="ecac4-135">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="ecac4-136">Vorhandene Pakete sind nicht betroffen.</span><span class="sxs-lookup"><span data-stu-id="ecac4-136">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="ecac4-137">Veröffentlichen des Pakets</span><span class="sxs-lookup"><span data-stu-id="ecac4-137">Publish the package</span></span>

<span data-ttu-id="ecac4-138">Sie können das Paket jetzt auf NuGet.org veröffentlichen. Informationen dazu finden Sie unter [Veröffentlichen von Paketen](Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="ecac4-138">You are now ready to publish the package to NuGet.org. See [Publishing packages](Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="ecac4-139">Erstellen eines Testzertifikats</span><span class="sxs-lookup"><span data-stu-id="ecac4-139">Create a test certificate</span></span>

<span data-ttu-id="ecac4-140">Sie können selbst ausgestellte Zertifikate für Testzwecke verwenden.</span><span class="sxs-lookup"><span data-stu-id="ecac4-140">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="ecac4-141">Um ein selbst ausgestelltes Zertifikat zu erstellen, verwenden Sie den [PowerShell-Befehl „New-SelfSignedCertificate“](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="ecac4-141">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="ecac4-142">Dieser Befehl erstellt ein Testzertifikat, das im persönlichen Zertifikatspeicher des aktuellen Benutzers gespeichert wird.</span><span class="sxs-lookup"><span data-stu-id="ecac4-142">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="ecac4-143">Sie können den Zertifikatspeicher durch Ausführen von `certmgr.msc` öffnen, um das neu erstellte Zertifikat anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="ecac4-143">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="ecac4-144">NuGet.org akzeptiert keine Pakete, die mit selbst ausgestellten Zertifikaten signiert sind.</span><span class="sxs-lookup"><span data-stu-id="ecac4-144">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="ecac4-145">Verwalten der Signaturanforderungen für Ihr Paket auf NuGet.org</span><span class="sxs-lookup"><span data-stu-id="ecac4-145">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="ecac4-146">[Melden Sie sich](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) bei NuGet.org an.</span><span class="sxs-lookup"><span data-stu-id="ecac4-146">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="ecac4-147">Wechseln Sie zu `Manage Packages`. 
   ![Paketsignierer konfigurieren](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="ecac4-147">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="ecac4-148">Wenn Sie der einzige Besitzer eines Pakets sind, sind Sie der erforderliche Signaturgeber, d.h., Sie können ein beliebiges der registrierten Zertifikate verwenden, um Ihre Pakete in NuGet.org zu signieren und zu veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="ecac4-148">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="ecac4-149">Wenn ein Paket über mehrere Besitzer verfügt, können standardmäßig die Zertifikate „jedes“ Besitzers zum Signieren des Pakets verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="ecac4-149">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="ecac4-150">Als Mitbesitzer des Pakets können Sie „Jeder“ außer Kraft setzen und sich selbst oder einen beliebigen Mitbesitzer als erforderlichen Signaturgeber festlegen.</span><span class="sxs-lookup"><span data-stu-id="ecac4-150">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="ecac4-151">Wenn Sie einen Besitzer angeben, für den kein Zertifikat registriert ist, werden nicht signierte Pakete zugelassen.</span><span class="sxs-lookup"><span data-stu-id="ecac4-151">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="ecac4-152">Ähnliches gilt, wenn die Standardoption „Jeder“ für ein Paket ausgewählt wurde, für das ein Besitzer ein Zertifikat registriert hat, ein anderer Besitzer jedoch nicht: NuGet.org akzeptiert entweder ein signiertes Paket mit einer von einem der Besitzer registrierten Signatur oder ein nicht signiertes Paket (da für einen der Besitzer kein Zertifikat registriert wurde).</span><span class="sxs-lookup"><span data-stu-id="ecac4-152">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="ecac4-153">Verwandte Artikel</span><span class="sxs-lookup"><span data-stu-id="ecac4-153">Related articles</span></span>

- [<span data-ttu-id="ecac4-154">Installieren von signierten Paketen</span><span class="sxs-lookup"><span data-stu-id="ecac4-154">Installing signed packages</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="ecac4-155">Referenz für signierte Pakete</span><span class="sxs-lookup"><span data-stu-id="ecac4-155">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
