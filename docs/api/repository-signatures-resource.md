---
title: Repository-Signaturen, NuGet-API | Microsoft-Dokumentation
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: Die Repository-Signaturen-Ressource ermöglicht es Clients Paketquellen, ihrem Repository Signieren Funktionen ankündigen zu können.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 50f309b99d4bf59e14f3e29b6b0421d8c3e8aa5a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547980"
---
# <a name="repository-signatures"></a><span data-ttu-id="04889-103">Repository-Signaturen</span><span class="sxs-lookup"><span data-stu-id="04889-103">Repository signatures</span></span>

<span data-ttu-id="04889-104">Wenn eine Paketquelle hinzufügen Repository Signaturen veröffentlichte Pakete unterstützt, ist es möglich, ein Client die Signaturzertifikate zu ermitteln, die von der Paketquelle verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="04889-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="04889-105">Diese Ressource ermöglicht Clients erkennen, ob ein Repository signiert. Paket wurde manipuliert oder ein unerwartetes Signaturzertifikat an.</span><span class="sxs-lookup"><span data-stu-id="04889-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="04889-106">Die Ressource, die zum Abrufen von diesem Repository Signaturinformationen ist die `RepositorySignatures` Ressource finden Sie in der [dienstindex](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="04889-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="04889-107">"NuGet.org" startet die Ankündigung der `RepositorySignatures` Ressource in der nahen Zukunft.</span><span class="sxs-lookup"><span data-stu-id="04889-107">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="04889-108">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="04889-108">Versioning</span></span>

<span data-ttu-id="04889-109">Die folgenden `@type` Wert wird verwendet:</span><span class="sxs-lookup"><span data-stu-id="04889-109">The following `@type` value is used:</span></span>

<span data-ttu-id="04889-110">@type-Wert</span><span class="sxs-lookup"><span data-stu-id="04889-110">@type value</span></span>                | <span data-ttu-id="04889-111">Hinweise</span><span class="sxs-lookup"><span data-stu-id="04889-111">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="04889-112">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="04889-112">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="04889-113">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="04889-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="04889-114">Basis-URL</span><span class="sxs-lookup"><span data-stu-id="04889-114">Base URL</span></span>

<span data-ttu-id="04889-115">Der Eintrag-Zugriffspunkt-URL für die folgenden APIs ist der Wert des der `@id` -Eigenschaft zusammen mit den oben genannten Ressourcen `@type` Wert.</span><span class="sxs-lookup"><span data-stu-id="04889-115">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="04889-116">In diesem Thema verwendet die Platzhalter-URL `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="04889-116">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="04889-117">Beachten Sie, dass im Gegensatz zu anderen Ressourcen, die `{@id}` URL ist erforderlich, um über HTTPS bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="04889-117">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="04889-118">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="04889-118">HTTP methods</span></span>

<span data-ttu-id="04889-119">Alle URLs, die in den Repositorys Signaturen Ressource unterstützt nur den HTTP-Methoden gefunden `GET` und `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="04889-119">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="04889-120">Index der Repository-Signaturen</span><span class="sxs-lookup"><span data-stu-id="04889-120">Repository signatures index</span></span>

<span data-ttu-id="04889-121">Der Index der Repository-Signaturen enthält zwei Angaben:</span><span class="sxs-lookup"><span data-stu-id="04889-121">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="04889-122">Sind an, ob alle Pakete an der Quelle gefunden Repository, die von dieser Quelle signiert.</span><span class="sxs-lookup"><span data-stu-id="04889-122">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="04889-123">Die Liste der Zertifikate, die von der Paketquelle verwendet wird, um Pakete zu signieren.</span><span class="sxs-lookup"><span data-stu-id="04889-123">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="04889-124">In den meisten Fällen wird die Liste der Zertifikate nur angefügt werden.</span><span class="sxs-lookup"><span data-stu-id="04889-124">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="04889-125">Neue Zertifikate würde zur Liste hinzugefügt werden, wenn das vorherige Signaturzertifikat abgelaufen ist und die Paketquelle beim Einstieg in ein neues Signaturzertifikat muss.</span><span class="sxs-lookup"><span data-stu-id="04889-125">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="04889-126">Wenn ein Zertifikat aus der Liste entfernt wird, bedeutet, dass an, dass Signaturen für alle Pakete erstellt, mit dem entfernten Signaturzertifikat nicht mehr gültigen vom Client berücksichtigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="04889-126">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="04889-127">In diesem Fall ist der Paketsignatur (aber nicht unbedingt das Paket) ungültig.</span><span class="sxs-lookup"><span data-stu-id="04889-127">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="04889-128">Eine Clientrichtlinie können die Installation des Pakets als ohne Vorzeichen.</span><span class="sxs-lookup"><span data-stu-id="04889-128">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="04889-129">Im Fall von zertifikatsperrung (z. B. schlüsselgefährdung) wird die Paketquelle erwartet, zum erneuten Signieren der alle Pakete, die durch das betroffene Zertifikat signiert.</span><span class="sxs-lookup"><span data-stu-id="04889-129">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="04889-130">Darüber hinaus sollten die Paketquelle das betroffene Zertifikat aus der Liste der Signierung entfernen.</span><span class="sxs-lookup"><span data-stu-id="04889-130">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="04889-131">Die folgende Anforderung Ruft den Index der Repository-Signaturen ab.</span><span class="sxs-lookup"><span data-stu-id="04889-131">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="04889-132">Der Index der Repository-Signatur ist ein JSON-Dokument, das ein Objekt mit den folgenden Eigenschaften enthält:</span><span class="sxs-lookup"><span data-stu-id="04889-132">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="04889-133">name</span><span class="sxs-lookup"><span data-stu-id="04889-133">Name</span></span>                | <span data-ttu-id="04889-134">Typ</span><span class="sxs-lookup"><span data-stu-id="04889-134">Type</span></span>             | <span data-ttu-id="04889-135">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="04889-135">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="04889-136">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="04889-136">allRepositorySigned</span></span> | <span data-ttu-id="04889-137">boolean</span><span class="sxs-lookup"><span data-stu-id="04889-137">boolean</span></span>          | <span data-ttu-id="04889-138">ja</span><span class="sxs-lookup"><span data-stu-id="04889-138">yes</span></span>
<span data-ttu-id="04889-139">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="04889-139">signingCertificates</span></span> | <span data-ttu-id="04889-140">Array von Objekten</span><span class="sxs-lookup"><span data-stu-id="04889-140">array of objects</span></span> | <span data-ttu-id="04889-141">ja</span><span class="sxs-lookup"><span data-stu-id="04889-141">yes</span></span>

<span data-ttu-id="04889-142">Die `allRepositorySigned` boolescher Wert auf "false" festgelegt ist, wenn die Paketquelle einige Pakete gespeichert sind, die keine Repository-Signatur verfügen.</span><span class="sxs-lookup"><span data-stu-id="04889-142">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="04889-143">Bei Verwendung der boolesche Wert auf true festgelegt ist, alle Pakete verfügbar muss die Quelle eine Repository-Signatur, die durch eines der Signaturzertifikate in erwähnten erzeugt `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="04889-143">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="04889-144">Es muss eine oder mehrere Signaturzertifikate in der `signingCertificates` array, wenn die `allRepositorySigned` booleschen Wert festgelegt ist auf "true".</span><span class="sxs-lookup"><span data-stu-id="04889-144">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="04889-145">Wenn das Array leer ist und `allRepositorySigned` nastaven NA hodnotu True gibt an, alle Pakete aus der Quelle angesehen werden ungültig ist, obwohl eine Clientrichtlinie möglicherweise weiterhin die Nutzung von Paketen zulässt.</span><span class="sxs-lookup"><span data-stu-id="04889-145">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="04889-146">Jedes Element im Array ist ein JSON-Objekt mit den folgenden Eigenschaften an.</span><span class="sxs-lookup"><span data-stu-id="04889-146">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="04889-147">name</span><span class="sxs-lookup"><span data-stu-id="04889-147">Name</span></span>         | <span data-ttu-id="04889-148">Typ</span><span class="sxs-lookup"><span data-stu-id="04889-148">Type</span></span>   | <span data-ttu-id="04889-149">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="04889-149">Required</span></span> | <span data-ttu-id="04889-150">Hinweise</span><span class="sxs-lookup"><span data-stu-id="04889-150">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="04889-151">contentUrl</span><span class="sxs-lookup"><span data-stu-id="04889-151">contentUrl</span></span>   | <span data-ttu-id="04889-152">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="04889-152">string</span></span> | <span data-ttu-id="04889-153">ja</span><span class="sxs-lookup"><span data-stu-id="04889-153">yes</span></span>      | <span data-ttu-id="04889-154">Das öffentliche Zertifikat von DER-codierte absolute URL</span><span class="sxs-lookup"><span data-stu-id="04889-154">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="04889-155">Fingerabdrücke</span><span class="sxs-lookup"><span data-stu-id="04889-155">fingerprints</span></span> | <span data-ttu-id="04889-156">object</span><span class="sxs-lookup"><span data-stu-id="04889-156">object</span></span> | <span data-ttu-id="04889-157">ja</span><span class="sxs-lookup"><span data-stu-id="04889-157">yes</span></span>      |
<span data-ttu-id="04889-158">Betreff</span><span class="sxs-lookup"><span data-stu-id="04889-158">subject</span></span>      | <span data-ttu-id="04889-159">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="04889-159">string</span></span> | <span data-ttu-id="04889-160">ja</span><span class="sxs-lookup"><span data-stu-id="04889-160">yes</span></span>      | <span data-ttu-id="04889-161">Definierter Antragstellername aus dem Zertifikat</span><span class="sxs-lookup"><span data-stu-id="04889-161">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="04889-162">issuer</span><span class="sxs-lookup"><span data-stu-id="04889-162">issuer</span></span>       | <span data-ttu-id="04889-163">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="04889-163">string</span></span> | <span data-ttu-id="04889-164">ja</span><span class="sxs-lookup"><span data-stu-id="04889-164">yes</span></span>      | <span data-ttu-id="04889-165">Der distinguished Name des der Zertifikataussteller</span><span class="sxs-lookup"><span data-stu-id="04889-165">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="04889-166">notBefore</span><span class="sxs-lookup"><span data-stu-id="04889-166">notBefore</span></span>    | <span data-ttu-id="04889-167">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="04889-167">string</span></span> | <span data-ttu-id="04889-168">ja</span><span class="sxs-lookup"><span data-stu-id="04889-168">yes</span></span>      | <span data-ttu-id="04889-169">Der Gültigkeitszeitraum des Zertifikats den Timestamp des Starts</span><span class="sxs-lookup"><span data-stu-id="04889-169">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="04889-170">notAfter</span><span class="sxs-lookup"><span data-stu-id="04889-170">notAfter</span></span>     | <span data-ttu-id="04889-171">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="04889-171">string</span></span> | <span data-ttu-id="04889-172">ja</span><span class="sxs-lookup"><span data-stu-id="04889-172">yes</span></span>      | <span data-ttu-id="04889-173">Der Endpunkt Zeitstempel der Gültigkeitszeitraum des Zertifikats</span><span class="sxs-lookup"><span data-stu-id="04889-173">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="04889-174">Beachten Sie, dass die `contentUrl` ist erforderlich, um über HTTPS bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="04889-174">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="04889-175">Diese URL verfügt über keine bestimmten URL-Muster und muss dynamisch ermittelt werden mit diesem Repository Signaturen Indizieren von Dokumenten.</span><span class="sxs-lookup"><span data-stu-id="04889-175">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="04889-176">Alle Eigenschaften in diesem Objekt (abgesehen vom `contentUrl`) muss aus dem Zertifikat finden Sie unter Geschäftstrends `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="04889-176">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="04889-177">Diese Geschäftstrends Eigenschaften dienen als praktische Roundtrips zu minimieren.</span><span class="sxs-lookup"><span data-stu-id="04889-177">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="04889-178">Die `fingerprints` Objekt hat die folgenden Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="04889-178">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="04889-179">name</span><span class="sxs-lookup"><span data-stu-id="04889-179">Name</span></span>                   | <span data-ttu-id="04889-180">Typ</span><span class="sxs-lookup"><span data-stu-id="04889-180">Type</span></span>   | <span data-ttu-id="04889-181">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="04889-181">Required</span></span> | <span data-ttu-id="04889-182">Hinweise</span><span class="sxs-lookup"><span data-stu-id="04889-182">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="04889-183">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="04889-183">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="04889-184">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="04889-184">string</span></span> | <span data-ttu-id="04889-185">ja</span><span class="sxs-lookup"><span data-stu-id="04889-185">yes</span></span>      | <span data-ttu-id="04889-186">Der SHA-256-Fingerabdruck</span><span class="sxs-lookup"><span data-stu-id="04889-186">The SHA-256 fingerprint</span></span>

<span data-ttu-id="04889-187">Der Name des Schlüssels `2.16.840.1.101.3.4.2.1` ist die OID des SHA-256-Hashalgorithmus.</span><span class="sxs-lookup"><span data-stu-id="04889-187">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="04889-188">Alle Hashwerte muss hexadezimal-codierten Zeichenfolge mit Kleinbuchstaben Darstellungen des Hash-Digests.</span><span class="sxs-lookup"><span data-stu-id="04889-188">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="04889-189">Beispiel für eine Anforderung</span><span class="sxs-lookup"><span data-stu-id="04889-189">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="04889-190">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="04889-190">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
