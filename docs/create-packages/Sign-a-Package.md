---
title: Signieren von NuGet-Paketen
description: Informationen zur Verwendung von signierten Paketen zur Aktivierung der Integritätsüberprüfung des Inhalts.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a469cbdd218a0e9c18950bb0d36faf4dbcb42a01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="daceb-103">Signieren von NuGet-Paketen</span><span class="sxs-lookup"><span data-stu-id="daceb-103">Signing NuGet Packages</span></span>

<span data-ttu-id="daceb-104">Durch die Signierung eines Pakets wird sichergestellt, dass dieses nicht mehr verändert wurde, nachdem es erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="daceb-104">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="daceb-105">Erforderliche Komponenten</span><span class="sxs-lookup"><span data-stu-id="daceb-105">Prerequisites</span></span>

1. <span data-ttu-id="daceb-106">Das zu signierende Paket (eine `.nupkg`-Datei).</span><span class="sxs-lookup"><span data-stu-id="daceb-106">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="daceb-107">Weitere Informationen finden Sie unter [Erstellen von NuGet-Paketen](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="daceb-107">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="daceb-108">nuget.exe 4.6.0 oder höher.</span><span class="sxs-lookup"><span data-stu-id="daceb-108">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="daceb-109">Weitere Informationen finden Sie unter [Installieren von NuGet-Clienttools](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="daceb-109">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="daceb-110">[Signierte Pakete](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="daceb-110">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

> [!Warning]
> <span data-ttu-id="daceb-111">Derzeit akzeptiert nuget.org keine signierten Pakete.</span><span class="sxs-lookup"><span data-stu-id="daceb-111">nuget.org does not currently accept signed packages.</span></span> <span data-ttu-id="daceb-112">Sie können Pakete signieren, die auf benutzerdefinierten Feeds veröffentlicht werden sollen.</span><span class="sxs-lookup"><span data-stu-id="daceb-112">You can sign packages for publishing to custom feeds.</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="daceb-113">Signieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="daceb-113">Sign a package</span></span>

<span data-ttu-id="daceb-114">Verwenden Sie den NuGet-Befehl [sign](../tools/cli-ref-sign.md), um ein Paket zu signieren:</span><span class="sxs-lookup"><span data-stu-id="daceb-114">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="daceb-115">Sie können, wie in der Referenz zu dem Befehl beschrieben, ein Zertifikat, das im Zertifikatspeicher verfügbar ist, oder ein Zertifikat aus einer Datei verwenden.</span><span class="sxs-lookup"><span data-stu-id="daceb-115">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="daceb-116">Häufig auftretende Probleme beim Signieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="daceb-116">Common problems when signing a package</span></span>

- <span data-ttu-id="daceb-117">Das Zertifikat ist nicht gültig für das Codesignieren.</span><span class="sxs-lookup"><span data-stu-id="daceb-117">The certificate is not valid for code signing.</span></span> <span data-ttu-id="daceb-118">Sie müssen sicherstellen, dass das angegebene Zertifikat über die entsprechende erweiterte Schlüsselverwendung verfügt (EKU 1.3.6.1.5.5.7.3.3).</span><span class="sxs-lookup"><span data-stu-id="daceb-118">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="daceb-119">Das Zertifikat entspricht nicht den grundlegenden Anforderungen wie dem RSA SHA-256-Signaturalgorithmus oder einem öffentlicher Schlüssel mit einer Größe von mindestens 2048 Bit.</span><span class="sxs-lookup"><span data-stu-id="daceb-119">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="daceb-120">Das Zertifikat ist abgelaufen oder wurde widerrufen.</span><span class="sxs-lookup"><span data-stu-id="daceb-120">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="daceb-121">Der Zeitstempelserver entspricht nicht den Zertifikatanforderungen.</span><span class="sxs-lookup"><span data-stu-id="daceb-121">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="daceb-122">Signierte Pakete sollten einen Zeitstempel enthalten, um sicherzustellen, dass die Signatur gültig bleibt, wenn das Signaturzertifikat abläuft.</span><span class="sxs-lookup"><span data-stu-id="daceb-122">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="daceb-123">Beim Signiervorgang wird die [Warnung NU3002](../reference/Errors-and-Warnings.md#nu3002) ausgelöst, wenn kein Zeitstempel verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="daceb-123">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="daceb-124">Überprüfen eines signierten Pakets</span><span class="sxs-lookup"><span data-stu-id="daceb-124">Verify a signed package</span></span>

<span data-ttu-id="daceb-125">Verwenden Sie den NuGet-Befehl [verify](../tools/cli-ref-verify.md), um die Details der Signatur eines bestimmten Pakets anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="daceb-125">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="daceb-126">Installieren eines signierten Pakets</span><span class="sxs-lookup"><span data-stu-id="daceb-126">Install a signed package</span></span>

<span data-ttu-id="daceb-127">Es erfordert keine bestimmten Aktionen, um signierte Pakete zu installieren. Wenn jedoch nach der Signierung Veränderungen am Inhalt vorgenommen wurden, wird die Installation blockiert und der [Fehler NU3008](../reference/Errors-and-Warnings.md#nu3008) ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="daceb-127">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="daceb-128">Pakete, die mit nicht vertrauenswürdigen Zertifikaten signiert wurden, werden als „nicht signiert“ angesehen und lösen wie alle anderen nicht signierten Pakete bei der Installation weder Warnungen noch Fehler aus.</span><span class="sxs-lookup"><span data-stu-id="daceb-128">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="daceb-129">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="daceb-129">See also</span></span>

[<span data-ttu-id="daceb-130">Referenz für signierte Pakete</span><span class="sxs-lookup"><span data-stu-id="daceb-130">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
