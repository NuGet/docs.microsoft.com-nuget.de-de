---
title: Signieren von NuGet-Paketen | Microsoft-Dokumentation
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Informationen zur Verwendung von signierten Paketen zur Aktivierung der Integritätsüberprüfung des Inhalts.
keywords: Signieren von NuGet-Paketen, NuGet-Sicherheit, Erstellen von signierten Paketen
ms.reviewer:
- karann-msft
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 61d90066e8cf75c8f49c7cc9390d45e1cd8afd0d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="d4d2c-104">Signieren von NuGet-Paketen</span><span class="sxs-lookup"><span data-stu-id="d4d2c-104">Signing NuGet Packages</span></span>

<span data-ttu-id="d4d2c-105">Durch die Signierung eines Pakets wird sichergestellt, dass dieses nicht mehr verändert wurde, nachdem es erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="d4d2c-105">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4d2c-106">Erforderliche Komponenten</span><span class="sxs-lookup"><span data-stu-id="d4d2c-106">Prerequisites</span></span>

1. <span data-ttu-id="d4d2c-107">Das zu signierende Paket (eine `.nupkg`-Datei).</span><span class="sxs-lookup"><span data-stu-id="d4d2c-107">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="d4d2c-108">Weitere Informationen finden Sie unter [Erstellen von NuGet-Paketen](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="d4d2c-108">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="d4d2c-109">nuget.exe 4.6.0 oder höher.</span><span class="sxs-lookup"><span data-stu-id="d4d2c-109">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="d4d2c-110">Weitere Informationen finden Sie unter [Installieren von NuGet-Clienttools](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="d4d2c-110">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="d4d2c-111">[Signierte Pakete](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="d4d2c-111">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

> [!Warning]
> <span data-ttu-id="d4d2c-112">Derzeit akzeptiert nuget.org keine signierten Pakete.</span><span class="sxs-lookup"><span data-stu-id="d4d2c-112">nuget.org does not currently accept signed packages.</span></span> <span data-ttu-id="d4d2c-113">Sie können Pakete signieren, die auf benutzerdefinierten Feeds veröffentlicht werden sollen.</span><span class="sxs-lookup"><span data-stu-id="d4d2c-113">You can sign packages for publishing to custom feeds.</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="d4d2c-114">Signieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="d4d2c-114">Sign a package</span></span>

<span data-ttu-id="d4d2c-115">Verwenden Sie den NuGet-Befehl [sign](../tools/cli-ref-sign.md), um ein Paket zu signieren:</span><span class="sxs-lookup"><span data-stu-id="d4d2c-115">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="d4d2c-116">Sie können, wie in der Referenz zu dem Befehl beschrieben, ein Zertifikat, das im Zertifikatspeicher verfügbar ist, oder ein Zertifikat aus einer Datei verwenden.</span><span class="sxs-lookup"><span data-stu-id="d4d2c-116">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="d4d2c-117">Häufig auftretende Probleme beim Signieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="d4d2c-117">Common problems when signing a package</span></span>

- <span data-ttu-id="d4d2c-118">Das Zertifikat ist nicht gültig für das Codesignieren.</span><span class="sxs-lookup"><span data-stu-id="d4d2c-118">The certificate is not valid for code signing.</span></span> <span data-ttu-id="d4d2c-119">Sie müssen sicherstellen, dass das angegebene Zertifikat über die entsprechende erweiterte Schlüsselverwendung verfügt (EKU 1.3.6.1.5.5.7.3.3).</span><span class="sxs-lookup"><span data-stu-id="d4d2c-119">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="d4d2c-120">Das Zertifikat entspricht nicht den grundlegenden Anforderungen wie dem RSA SHA-256-Signaturalgorithmus oder einem öffentlicher Schlüssel mit einer Größe von mindestens 2048 Bit.</span><span class="sxs-lookup"><span data-stu-id="d4d2c-120">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="d4d2c-121">Das Zertifikat ist abgelaufen oder wurde widerrufen.</span><span class="sxs-lookup"><span data-stu-id="d4d2c-121">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="d4d2c-122">Der Zeitstempelserver entspricht nicht den Zertifikatanforderungen.</span><span class="sxs-lookup"><span data-stu-id="d4d2c-122">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="d4d2c-123">Signierte Pakete sollten einen Zeitstempel enthalten, um sicherzustellen, dass die Signatur gültig bleibt, wenn das Signaturzertifikat abläuft.</span><span class="sxs-lookup"><span data-stu-id="d4d2c-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="d4d2c-124">Beim Signiervorgang wird die [Warnung NU3002](../reference/Errors-and-Warnings.md#nu3002) ausgelöst, wenn kein Zeitstempel verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="d4d2c-124">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="d4d2c-125">Überprüfen eines signierten Pakets</span><span class="sxs-lookup"><span data-stu-id="d4d2c-125">Verify a signed package</span></span>

<span data-ttu-id="d4d2c-126">Verwenden Sie den NuGet-Befehl [verify](../tools/cli-ref-verify.md), um die Details der Signatur eines bestimmten Pakets anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="d4d2c-126">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="d4d2c-127">Installieren eines signierten Pakets</span><span class="sxs-lookup"><span data-stu-id="d4d2c-127">Install a signed package</span></span>

<span data-ttu-id="d4d2c-128">Es erfordert keine bestimmten Aktionen, um signierte Pakete zu installieren. Wenn jedoch nach der Signierung Veränderungen am Inhalt vorgenommen wurden, wird die Installation blockiert und der [Fehler NU3008](../reference/Errors-and-Warnings.md#nu3008) ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="d4d2c-128">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="d4d2c-129">Pakete, die mit nicht vertrauenswürdigen Zertifikaten signiert wurden, werden als „nicht signiert“ angesehen und lösen wie alle anderen nicht signierten Pakete bei der Installation weder Warnungen noch Fehler aus.</span><span class="sxs-lookup"><span data-stu-id="d4d2c-129">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="d4d2c-130">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="d4d2c-130">See also</span></span>

[<span data-ttu-id="d4d2c-131">Referenz für signierte Pakete</span><span class="sxs-lookup"><span data-stu-id="d4d2c-131">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
