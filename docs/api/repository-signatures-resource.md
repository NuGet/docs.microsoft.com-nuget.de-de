---
title: Repository-Signaturen, NuGet-API | Microsoft-Dokumentation
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 3/2/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Die Repository-Signaturen-Ressource ermöglicht es Clients Paketquellen, ihrem Repository Signieren Funktionen ankündigen zu können.
keywords: NuGet-API-Repository-Signaturen, Signieren von Zertifikaten, nuget.org nuget.org-paketsignierung
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 32dd2ee19261488a2b1b92724095a11ced69ae68
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/21/2018
ms.locfileid: "42793234"
---
# <a name="repository-signatures"></a><span data-ttu-id="29b21-104">Repository-Signaturen</span><span class="sxs-lookup"><span data-stu-id="29b21-104">Repository signatures</span></span>

<span data-ttu-id="29b21-105">Wenn eine Paketquelle hinzufügen Repository Signaturen veröffentlichte Pakete unterstützt, ist es möglich, ein Client die Signaturzertifikate zu ermitteln, die von der Paketquelle verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="29b21-105">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="29b21-106">Diese Ressource ermöglicht Clients erkennen, ob ein Repository signiert. Paket wurde manipuliert oder ein unerwartetes Signaturzertifikat an.</span><span class="sxs-lookup"><span data-stu-id="29b21-106">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="29b21-107">Die Ressource, die zum Abrufen von diesem Repository Signaturinformationen ist die `RepositorySignatures` Ressource finden Sie in der [dienstindex](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="29b21-107">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="29b21-108">"NuGet.org" startet die Ankündigung der `RepositorySignatures` Ressource in der nahen Zukunft.</span><span class="sxs-lookup"><span data-stu-id="29b21-108">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="29b21-109">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="29b21-109">Versioning</span></span>

<span data-ttu-id="29b21-110">Die folgenden `@type` Wert wird verwendet:</span><span class="sxs-lookup"><span data-stu-id="29b21-110">The following `@type` value is used:</span></span>

<span data-ttu-id="29b21-111">@type-Wert</span><span class="sxs-lookup"><span data-stu-id="29b21-111">@type value</span></span>                | <span data-ttu-id="29b21-112">Hinweise</span><span class="sxs-lookup"><span data-stu-id="29b21-112">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="29b21-113">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="29b21-113">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="29b21-114">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="29b21-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="29b21-115">Basis-URL</span><span class="sxs-lookup"><span data-stu-id="29b21-115">Base URL</span></span>

<span data-ttu-id="29b21-116">Der Eintrag-Zugriffspunkt-URL für die folgenden APIs ist der Wert des der `@id` -Eigenschaft zusammen mit den oben genannten Ressourcen `@type` Wert.</span><span class="sxs-lookup"><span data-stu-id="29b21-116">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="29b21-117">In diesem Thema verwendet die Platzhalter-URL `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="29b21-117">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="29b21-118">Beachten Sie, dass im Gegensatz zu anderen Ressourcen, die `{@id}` URL ist erforderlich, um über HTTPS bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="29b21-118">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="29b21-119">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="29b21-119">HTTP methods</span></span>

<span data-ttu-id="29b21-120">Alle URLs, die in den Repositorys Signaturen Ressource unterstützt nur den HTTP-Methoden gefunden `GET` und `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="29b21-120">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="29b21-121">Index der Repository-Signaturen</span><span class="sxs-lookup"><span data-stu-id="29b21-121">Repository signatures index</span></span>

<span data-ttu-id="29b21-122">Der Index der Repository-Signaturen enthält zwei Angaben:</span><span class="sxs-lookup"><span data-stu-id="29b21-122">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="29b21-123">Sind an, ob alle Pakete an der Quelle gefunden Repository, die von dieser Quelle signiert.</span><span class="sxs-lookup"><span data-stu-id="29b21-123">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="29b21-124">Die Liste der Zertifikate, die von der Paketquelle verwendet wird, um Pakete zu signieren.</span><span class="sxs-lookup"><span data-stu-id="29b21-124">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="29b21-125">In den meisten Fällen wird die Liste der Zertifikate nur angefügt werden.</span><span class="sxs-lookup"><span data-stu-id="29b21-125">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="29b21-126">Neue Zertifikate würde zur Liste hinzugefügt werden, wenn das vorherige Signaturzertifikat abgelaufen ist und die Paketquelle beim Einstieg in ein neues Signaturzertifikat muss.</span><span class="sxs-lookup"><span data-stu-id="29b21-126">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="29b21-127">Wenn ein Zertifikat aus der Liste entfernt wird, bedeutet, dass an, dass Signaturen für alle Pakete erstellt, mit dem entfernten Signaturzertifikat nicht mehr gültigen vom Client berücksichtigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="29b21-127">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="29b21-128">In diesem Fall ist der Paketsignatur (aber nicht unbedingt das Paket) ungültig.</span><span class="sxs-lookup"><span data-stu-id="29b21-128">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="29b21-129">Eine Clientrichtlinie können die Installation des Pakets als ohne Vorzeichen.</span><span class="sxs-lookup"><span data-stu-id="29b21-129">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="29b21-130">Im Fall von zertifikatsperrung (z. B. schlüsselgefährdung) wird die Paketquelle erwartet, zum erneuten Signieren der alle Pakete, die durch das betroffene Zertifikat signiert.</span><span class="sxs-lookup"><span data-stu-id="29b21-130">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="29b21-131">Darüber hinaus sollten die Paketquelle das betroffene Zertifikat aus der Liste der Signierung entfernen.</span><span class="sxs-lookup"><span data-stu-id="29b21-131">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="29b21-132">Die folgende Anforderung Ruft den Index der Repository-Signaturen ab.</span><span class="sxs-lookup"><span data-stu-id="29b21-132">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="29b21-133">Der Index der Repository-Signatur ist ein JSON-Dokument, das ein Objekt mit den folgenden Eigenschaften enthält:</span><span class="sxs-lookup"><span data-stu-id="29b21-133">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="29b21-134">name</span><span class="sxs-lookup"><span data-stu-id="29b21-134">Name</span></span>                | <span data-ttu-id="29b21-135">Typ</span><span class="sxs-lookup"><span data-stu-id="29b21-135">Type</span></span>             | <span data-ttu-id="29b21-136">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="29b21-136">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="29b21-137">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="29b21-137">allRepositorySigned</span></span> | <span data-ttu-id="29b21-138">boolean</span><span class="sxs-lookup"><span data-stu-id="29b21-138">boolean</span></span>          | <span data-ttu-id="29b21-139">ja</span><span class="sxs-lookup"><span data-stu-id="29b21-139">yes</span></span>
<span data-ttu-id="29b21-140">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="29b21-140">signingCertificates</span></span> | <span data-ttu-id="29b21-141">Array von Objekten</span><span class="sxs-lookup"><span data-stu-id="29b21-141">array of objects</span></span> | <span data-ttu-id="29b21-142">ja</span><span class="sxs-lookup"><span data-stu-id="29b21-142">yes</span></span>

<span data-ttu-id="29b21-143">Die `allRepositorySigned` boolescher Wert auf "false" festgelegt ist, wenn die Paketquelle einige Pakete gespeichert sind, die keine Repository-Signatur verfügen.</span><span class="sxs-lookup"><span data-stu-id="29b21-143">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="29b21-144">Bei Verwendung der boolesche Wert auf true festgelegt ist, alle Pakete verfügbar muss die Quelle eine Repository-Signatur, die durch eines der Signaturzertifikate in erwähnten erzeugt `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="29b21-144">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="29b21-145">Es muss eine oder mehrere Signaturzertifikate in der `signingCertificates` array, wenn die `allRepositorySigned` booleschen Wert festgelegt ist auf "true".</span><span class="sxs-lookup"><span data-stu-id="29b21-145">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="29b21-146">Wenn das Array leer ist und `allRepositorySigned` nastaven NA hodnotu True gibt an, alle Pakete aus der Quelle angesehen werden ungültig ist, obwohl eine Clientrichtlinie möglicherweise weiterhin die Nutzung von Paketen zulässt.</span><span class="sxs-lookup"><span data-stu-id="29b21-146">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="29b21-147">Jedes Element im Array ist ein JSON-Objekt mit den folgenden Eigenschaften an.</span><span class="sxs-lookup"><span data-stu-id="29b21-147">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="29b21-148">name</span><span class="sxs-lookup"><span data-stu-id="29b21-148">Name</span></span>         | <span data-ttu-id="29b21-149">Typ</span><span class="sxs-lookup"><span data-stu-id="29b21-149">Type</span></span>   | <span data-ttu-id="29b21-150">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="29b21-150">Required</span></span> | <span data-ttu-id="29b21-151">Hinweise</span><span class="sxs-lookup"><span data-stu-id="29b21-151">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="29b21-152">contentUrl</span><span class="sxs-lookup"><span data-stu-id="29b21-152">contentUrl</span></span>   | <span data-ttu-id="29b21-153">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="29b21-153">string</span></span> | <span data-ttu-id="29b21-154">ja</span><span class="sxs-lookup"><span data-stu-id="29b21-154">yes</span></span>      | <span data-ttu-id="29b21-155">Das öffentliche Zertifikat von DER-codierte absolute URL</span><span class="sxs-lookup"><span data-stu-id="29b21-155">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="29b21-156">Fingerabdrücke</span><span class="sxs-lookup"><span data-stu-id="29b21-156">fingerprints</span></span> | <span data-ttu-id="29b21-157">object</span><span class="sxs-lookup"><span data-stu-id="29b21-157">object</span></span> | <span data-ttu-id="29b21-158">ja</span><span class="sxs-lookup"><span data-stu-id="29b21-158">yes</span></span>      |
<span data-ttu-id="29b21-159">Betreff</span><span class="sxs-lookup"><span data-stu-id="29b21-159">subject</span></span>      | <span data-ttu-id="29b21-160">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="29b21-160">string</span></span> | <span data-ttu-id="29b21-161">ja</span><span class="sxs-lookup"><span data-stu-id="29b21-161">yes</span></span>      | <span data-ttu-id="29b21-162">Definierter Antragstellername aus dem Zertifikat</span><span class="sxs-lookup"><span data-stu-id="29b21-162">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="29b21-163">issuer</span><span class="sxs-lookup"><span data-stu-id="29b21-163">issuer</span></span>       | <span data-ttu-id="29b21-164">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="29b21-164">string</span></span> | <span data-ttu-id="29b21-165">ja</span><span class="sxs-lookup"><span data-stu-id="29b21-165">yes</span></span>      | <span data-ttu-id="29b21-166">Der distinguished Name des der Zertifikataussteller</span><span class="sxs-lookup"><span data-stu-id="29b21-166">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="29b21-167">notBefore</span><span class="sxs-lookup"><span data-stu-id="29b21-167">notBefore</span></span>    | <span data-ttu-id="29b21-168">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="29b21-168">string</span></span> | <span data-ttu-id="29b21-169">ja</span><span class="sxs-lookup"><span data-stu-id="29b21-169">yes</span></span>      | <span data-ttu-id="29b21-170">Der Gültigkeitszeitraum des Zertifikats den Timestamp des Starts</span><span class="sxs-lookup"><span data-stu-id="29b21-170">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="29b21-171">notAfter</span><span class="sxs-lookup"><span data-stu-id="29b21-171">notAfter</span></span>     | <span data-ttu-id="29b21-172">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="29b21-172">string</span></span> | <span data-ttu-id="29b21-173">ja</span><span class="sxs-lookup"><span data-stu-id="29b21-173">yes</span></span>      | <span data-ttu-id="29b21-174">Der Endpunkt Zeitstempel der Gültigkeitszeitraum des Zertifikats</span><span class="sxs-lookup"><span data-stu-id="29b21-174">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="29b21-175">Beachten Sie, dass die `contentUrl` ist erforderlich, um über HTTPS bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="29b21-175">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="29b21-176">Diese URL verfügt über keine bestimmten URL-Muster und muss dynamisch ermittelt werden mit diesem Repository Signaturen Indizieren von Dokumenten.</span><span class="sxs-lookup"><span data-stu-id="29b21-176">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="29b21-177">Alle Eigenschaften in diesem Objekt (abgesehen vom `contentUrl`) muss aus dem Zertifikat finden Sie unter Geschäftstrends `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="29b21-177">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="29b21-178">Diese Geschäftstrends Eigenschaften dienen als praktische Roundtrips zu minimieren.</span><span class="sxs-lookup"><span data-stu-id="29b21-178">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="29b21-179">Die `fingerprints` Objekt hat die folgenden Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="29b21-179">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="29b21-180">name</span><span class="sxs-lookup"><span data-stu-id="29b21-180">Name</span></span>                   | <span data-ttu-id="29b21-181">Typ</span><span class="sxs-lookup"><span data-stu-id="29b21-181">Type</span></span>   | <span data-ttu-id="29b21-182">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="29b21-182">Required</span></span> | <span data-ttu-id="29b21-183">Hinweise</span><span class="sxs-lookup"><span data-stu-id="29b21-183">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="29b21-184">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="29b21-184">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="29b21-185">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="29b21-185">string</span></span> | <span data-ttu-id="29b21-186">ja</span><span class="sxs-lookup"><span data-stu-id="29b21-186">yes</span></span>      | <span data-ttu-id="29b21-187">Der SHA-256-Fingerabdruck</span><span class="sxs-lookup"><span data-stu-id="29b21-187">The SHA-256 fingerprint</span></span>

<span data-ttu-id="29b21-188">Der Name des Schlüssels `2.16.840.1.101.3.4.2.1` ist die OID des SHA-256-Hashalgorithmus.</span><span class="sxs-lookup"><span data-stu-id="29b21-188">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="29b21-189">Alle Hashwerte muss hexadezimal-codierten Zeichenfolge mit Kleinbuchstaben Darstellungen des Hash-Digests.</span><span class="sxs-lookup"><span data-stu-id="29b21-189">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="29b21-190">Beispiel für eine Anforderung</span><span class="sxs-lookup"><span data-stu-id="29b21-190">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="29b21-191">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="29b21-191">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
