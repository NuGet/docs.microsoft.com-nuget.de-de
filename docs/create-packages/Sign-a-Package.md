---
title: Signieren von NuGet-Paketen
description: Informationen zur Verwendung von signierten Paketen zur Aktivierung der Integritätsüberprüfung des Inhalts.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 9900db1970a89de129d9074e5900e0aa048101de
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/22/2018
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="457eb-103">Signieren von NuGet-Paketen</span><span class="sxs-lookup"><span data-stu-id="457eb-103">Signing NuGet Packages</span></span>

<span data-ttu-id="457eb-104">Durch die Signierung eines Pakets wird sichergestellt, dass dieses nicht mehr verändert wurde, nachdem es erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="457eb-104">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="457eb-105">Erforderliche Komponenten</span><span class="sxs-lookup"><span data-stu-id="457eb-105">Prerequisites</span></span>

1. <span data-ttu-id="457eb-106">Das zu signierende Paket (eine `.nupkg`-Datei).</span><span class="sxs-lookup"><span data-stu-id="457eb-106">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="457eb-107">Weitere Informationen finden Sie unter [Erstellen von NuGet-Paketen](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="457eb-107">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="457eb-108">nuget.exe 4.6.0 oder höher.</span><span class="sxs-lookup"><span data-stu-id="457eb-108">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="457eb-109">Weitere Informationen finden Sie unter [Installieren von NuGet-Clienttools](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="457eb-109">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="457eb-110">[Signierte Pakete](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="457eb-110">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="457eb-111">Signieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="457eb-111">Sign a package</span></span>

<span data-ttu-id="457eb-112">Verwenden Sie den NuGet-Befehl [sign](../tools/cli-ref-sign.md), um ein Paket zu signieren:</span><span class="sxs-lookup"><span data-stu-id="457eb-112">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="457eb-113">Sie können, wie in der Referenz zu dem Befehl beschrieben, ein Zertifikat, das im Zertifikatspeicher verfügbar ist, oder ein Zertifikat aus einer Datei verwenden.</span><span class="sxs-lookup"><span data-stu-id="457eb-113">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="457eb-114">Häufig auftretende Probleme beim Signieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="457eb-114">Common problems when signing a package</span></span>

- <span data-ttu-id="457eb-115">Das Zertifikat ist nicht gültig für das Codesignieren.</span><span class="sxs-lookup"><span data-stu-id="457eb-115">The certificate is not valid for code signing.</span></span> <span data-ttu-id="457eb-116">Sie müssen sicherstellen, dass das angegebene Zertifikat über die entsprechende erweiterte Schlüsselverwendung verfügt (EKU 1.3.6.1.5.5.7.3.3).</span><span class="sxs-lookup"><span data-stu-id="457eb-116">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="457eb-117">Das Zertifikat entspricht nicht den grundlegenden Anforderungen wie dem RSA SHA-256-Signaturalgorithmus oder einem öffentlicher Schlüssel mit einer Größe von mindestens 2048 Bit.</span><span class="sxs-lookup"><span data-stu-id="457eb-117">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="457eb-118">Das Zertifikat ist abgelaufen oder wurde widerrufen.</span><span class="sxs-lookup"><span data-stu-id="457eb-118">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="457eb-119">Der Zeitstempelserver entspricht nicht den Zertifikatanforderungen.</span><span class="sxs-lookup"><span data-stu-id="457eb-119">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="457eb-120">Signierte Pakete sollten einen Zeitstempel enthalten, um sicherzustellen, dass die Signatur gültig bleibt, wenn das Signaturzertifikat abläuft.</span><span class="sxs-lookup"><span data-stu-id="457eb-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="457eb-121">Beim Signiervorgang wird die [Warnung NU3002](../reference/Errors-and-Warnings.md#nu3002) ausgelöst, wenn kein Zeitstempel verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="457eb-121">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="457eb-122">Überprüfen eines signierten Pakets</span><span class="sxs-lookup"><span data-stu-id="457eb-122">Verify a signed package</span></span>

<span data-ttu-id="457eb-123">Verwenden Sie den NuGet-Befehl [verify](../tools/cli-ref-verify.md), um die Details der Signatur eines bestimmten Pakets anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="457eb-123">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="457eb-124">Installieren eines signierten Pakets</span><span class="sxs-lookup"><span data-stu-id="457eb-124">Install a signed package</span></span>

<span data-ttu-id="457eb-125">Es erfordert keine bestimmten Aktionen, um signierte Pakete zu installieren. Wenn jedoch nach der Signierung Veränderungen am Inhalt vorgenommen wurden, wird die Installation blockiert und der [Fehler NU3008](../reference/Errors-and-Warnings.md#nu3008) ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="457eb-125">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="457eb-126">Pakete, die mit nicht vertrauenswürdigen Zertifikaten signiert wurden, werden als „nicht signiert“ angesehen und lösen wie alle anderen nicht signierten Pakete bei der Installation weder Warnungen noch Fehler aus.</span><span class="sxs-lookup"><span data-stu-id="457eb-126">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="457eb-127">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="457eb-127">See also</span></span>

[<span data-ttu-id="457eb-128">Referenz für signierte Pakete</span><span class="sxs-lookup"><span data-stu-id="457eb-128">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
