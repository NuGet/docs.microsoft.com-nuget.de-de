---
title: NuGet-Pakete Verweis signiert
description: Anforderungen für die Signierung von NuGet-Paket.
author: rido-min
ms.author: rido-min
manager: unnir
ms.date: 04/24/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 751a8ff14bdc3a647985da4f908ad1a0fd0def9a
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/27/2018
---
# <a name="signed-packages"></a><span data-ttu-id="e5618-103">Signierte Pakete</span><span class="sxs-lookup"><span data-stu-id="e5618-103">Signed packages</span></span>

<span data-ttu-id="e5618-104">*NuGet-4.6.0+ und Visual Studio 2017 15.6 und höher*</span><span class="sxs-lookup"><span data-stu-id="e5618-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="e5618-105">NuGet-Pakete können es sich um eine digitale Signatur einzuschließen, die Schutz vor manipulierte Inhalte enthält.</span><span class="sxs-lookup"><span data-stu-id="e5618-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="e5618-106">Diese Signatur wird aus einem x. 509-Zertifikat erzeugt, die der tatsächliche Ursprung der das Paket auch Authentizität Proofs hinzufügt.</span><span class="sxs-lookup"><span data-stu-id="e5618-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="e5618-107">Signierte Pakete bereitstellen die stärkste End-to-End-Überprüfung.</span><span class="sxs-lookup"><span data-stu-id="e5618-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="e5618-108">Eine Autor-Signatur wird sichergestellt, dass das Paket nicht geändert wurde, seit der Autor das Paket, unabhängig davon aus signiert die Repositorys oder welche Methode transport das Paket wird übermittelt.</span><span class="sxs-lookup"><span data-stu-id="e5618-108">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="e5618-109">Kunden, die eine gesperrtes-Umgebung "demand" können mit einem bestimmten Autor Zertifikat signiert-Pakete erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="e5618-109">Consumers who demand a locked-down environment can require packages signed with a specific author certificate.</span></span>

<span data-ttu-id="e5618-110">Darüber hinaus bieten Autor signierte Pakete einen zusätzlichen Authentifizierungsmechanismus die publishing nuget.org-Pipeline, da das Signaturzertifikat voraus registriert werden muss.</span><span class="sxs-lookup"><span data-stu-id="e5618-110">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span>

<span data-ttu-id="e5618-111">Weitere Informationen zum Erstellen eines signierten Pakets, finden Sie unter [Signieren von Paketen](../create-packages/Sign-a-package.md) und [NuGet-Anmelde-Befehls](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="e5618-111">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="e5618-112">NuGet.org akzeptiert gegenwärtig nicht signierte Pakete.</span><span class="sxs-lookup"><span data-stu-id="e5618-112">nuget.org does not presently accept signed packages.</span></span> <span data-ttu-id="e5618-113">Sie können Pakete signieren, die auf benutzerdefinierten Feeds veröffentlicht werden sollen.</span><span class="sxs-lookup"><span data-stu-id="e5618-113">You can sign packages for publishing to custom feeds.</span></span>

> [!Important]
> <span data-ttu-id="e5618-114">Paketsignierung wird derzeit nur bei Verwendung von nuget.exe unter Windows unterstützt.</span><span class="sxs-lookup"><span data-stu-id="e5618-114">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="e5618-115">Überprüfung von signierten Paketen ist derzeit nur unterstützt, wenn nuget.exe oder Visual Studio unter Windows verwenden.</span><span class="sxs-lookup"><span data-stu-id="e5618-115">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="e5618-116">Zertifikatanforderungen</span><span class="sxs-lookup"><span data-stu-id="e5618-116">Certificate requirements</span></span>

<span data-ttu-id="e5618-117">Codesignaturzertifikat anfordern, die eine besondere Art von Zertifikat ist, die für gültig ist paketsignierung erfordert die `id-kp-codeSigning` Zweck [[RFC 5280 Abschnitt 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="e5618-117">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="e5618-118">Darüber hinaus muss das Zertifikat eine RSA Länge des öffentliche Schlüssels von 2048 Bits oder höher aufweisen.</span><span class="sxs-lookup"><span data-stu-id="e5618-118">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="e5618-119">Erhalten Sie ein Codesignaturzertifikat</span><span class="sxs-lookup"><span data-stu-id="e5618-119">Get a code signing certificate</span></span>

<span data-ttu-id="e5618-120">Gültige Zertifikate können von öffentlichen Zertifizierungsstellen wie abgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="e5618-120">Valid certificates may be obtained from public certificate authorities like:</span></span>

- [<span data-ttu-id="e5618-121">Symantec</span><span class="sxs-lookup"><span data-stu-id="e5618-121">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="e5618-122">DigiCert</span><span class="sxs-lookup"><span data-stu-id="e5618-122">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="e5618-123">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="e5618-123">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="e5618-124">Globale anmelden</span><span class="sxs-lookup"><span data-stu-id="e5618-124">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="e5618-125">Comodo</span><span class="sxs-lookup"><span data-stu-id="e5618-125">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="e5618-126">Certum</span><span class="sxs-lookup"><span data-stu-id="e5618-126">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="e5618-127">Die vollständige Liste der Zertifizierungsstellen von Windows als vertrauenswürdig eingestuft erhalten von [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="e5618-127">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="e5618-128">Ein Testzertifikat erstellen</span><span class="sxs-lookup"><span data-stu-id="e5618-128">Create a test certificate</span></span>

<span data-ttu-id="e5618-129">Sie können selbst ausgestellte Zertifikate für Testzwecke verwenden.</span><span class="sxs-lookup"><span data-stu-id="e5618-129">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="e5618-130">Verwenden Sie zum Erstellen eines selbst ausgegebenen Zertifikats die [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell-Befehl.</span><span class="sxs-lookup"><span data-stu-id="e5618-130">To create a self-issued certificate, use the [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell command.</span></span>

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

<span data-ttu-id="e5618-131">Dieser Befehl erstellt ein Testzertifikats verfügbar im persönlichen Zertifikatspeicher des aktuellen Benutzers.</span><span class="sxs-lookup"><span data-stu-id="e5618-131">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="e5618-132">Sie können den Zertifikatspeicher öffnen, indem ausgeführt `certmgr.msc` des neu erstellten Zertifikats angezeigt.</span><span class="sxs-lookup"><span data-stu-id="e5618-132">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="e5618-133">Timestamp-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="e5618-133">Timestamp requirements</span></span>

<span data-ttu-id="e5618-134">Signierte Pakete sollten einen RFC 3161-Zeitstempel Sicherstellen der Gültigkeit der Signatur außerhalb der Gültigkeitsdauer des Zertifikats signieren Paket enthalten.</span><span class="sxs-lookup"><span data-stu-id="e5618-134">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="e5618-135">Das Zertifikat zum Signieren des Zeitstempels muss gültig sein kann die `id-kp-timeStamping` Zweck [[RFC 5280 Abschnitt 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="e5618-135">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="e5618-136">Darüber hinaus muss das Zertifikat eine RSA Länge des öffentliche Schlüssels von 2048 Bits oder höher aufweisen.</span><span class="sxs-lookup"><span data-stu-id="e5618-136">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="e5618-137">Zusätzliche technische Details finden Sie der [Paket Signatur technische Spezifikationen](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="e5618-137">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>
