---
title: Inhalte, die NuGet-API-Verpacken | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Die Basisadresse des Pakets ist eine einfache Schnittstelle zum Abrufen der des Pakets selbst.
keywords: NuGet Flatfile-Container, die NuGet-Paket-Basisadresse, die NuGet Nupkg-API, die NuGet-API-Paketversionen, NuGet-API nicht aufgelistete Pakete, die NuGet-API-Download Nuspec
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c2e631dc0bba95ac849430d77142f27ef591f741
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="package-content"></a><span data-ttu-id="57fad-104">Paketinhalt</span><span class="sxs-lookup"><span data-stu-id="57fad-104">Package Content</span></span>

<span data-ttu-id="57fad-105">Es ist möglich, generieren eine URL für ein beliebiges Paket Inhalte (der .nupkg-Datei) mithilfe der V3-API abgerufen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="57fad-105">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="57fad-106">Die Ressource für das Abrufen von Paketinhalt verwendet die `PackageBaseAddress` Ressource gefunden, der [Dienst Index](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="57fad-106">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="57fad-107">Diese Ressource ermöglicht auch die Ermittlung aller Versionen eines Pakets aufgeführt oder nicht aufgeführte.</span><span class="sxs-lookup"><span data-stu-id="57fad-107">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="57fad-108">Diese Ressource wird häufig als entweder die "Paket Basisadresse" oder "Flatfile-Container" bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="57fad-108">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="57fad-109">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="57fad-109">Versioning</span></span>

<span data-ttu-id="57fad-110">Die folgenden `@type` Wert wird verwendet:</span><span class="sxs-lookup"><span data-stu-id="57fad-110">The following `@type` value is used:</span></span>

<span data-ttu-id="57fad-111">@type-Wert</span><span class="sxs-lookup"><span data-stu-id="57fad-111">@type value</span></span>              | <span data-ttu-id="57fad-112">Hinweise</span><span class="sxs-lookup"><span data-stu-id="57fad-112">Notes</span></span>
------------------------ | -----
<span data-ttu-id="57fad-113">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="57fad-113">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="57fad-114">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="57fad-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="57fad-115">Basis-URL</span><span class="sxs-lookup"><span data-stu-id="57fad-115">Base URL</span></span>

<span data-ttu-id="57fad-116">Die base-URL für die folgenden APIs ist der Wert der `@id` Eigenschaft, die zuvor erwähnten zur Ressource zugeordnete `@type` Wert.</span><span class="sxs-lookup"><span data-stu-id="57fad-116">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="57fad-117">Im folgenden Dokument Platzhalter für die Basis-URL `{@id}` verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="57fad-117">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="57fad-118">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="57fad-118">HTTP methods</span></span>

<span data-ttu-id="57fad-119">Alle URLs, die bei der Unterstützung der Registrierung-Ressource gefunden, die HTTP-Methoden `GET` und `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="57fad-119">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="57fad-120">Auflisten von Paketversionen</span><span class="sxs-lookup"><span data-stu-id="57fad-120">Enumerate package versions</span></span>

<span data-ttu-id="57fad-121">Wenn der Client bekannt eine Paket-ID ist und möchte Ermitteln der Paket-Versionen des Pakets die Quelle verfügbar ist, der Client eine vorhersagbare URL zum Aufzählen aller Paketversionen erstellen kann.</span><span class="sxs-lookup"><span data-stu-id="57fad-121">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="57fad-122">Diese Liste ist dafür vorgesehen, "Verzeichnisliste" werden für die unten aufgeführten Content Paket-API.</span><span class="sxs-lookup"><span data-stu-id="57fad-122">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="57fad-123">Diese Liste enthält beide Paketversionen aufgeführt und nicht aufgeführte.</span><span class="sxs-lookup"><span data-stu-id="57fad-123">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="57fad-124">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="57fad-124">Request parameters</span></span>

<span data-ttu-id="57fad-125">name</span><span class="sxs-lookup"><span data-stu-id="57fad-125">Name</span></span>     | <span data-ttu-id="57fad-126">In</span><span class="sxs-lookup"><span data-stu-id="57fad-126">In</span></span>     | <span data-ttu-id="57fad-127">Typ</span><span class="sxs-lookup"><span data-stu-id="57fad-127">Type</span></span>    | <span data-ttu-id="57fad-128">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="57fad-128">Required</span></span> | <span data-ttu-id="57fad-129">Hinweise</span><span class="sxs-lookup"><span data-stu-id="57fad-129">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="57fad-130">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="57fad-130">LOWER_ID</span></span> | <span data-ttu-id="57fad-131">URL</span><span class="sxs-lookup"><span data-stu-id="57fad-131">URL</span></span>    | <span data-ttu-id="57fad-132">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="57fad-132">string</span></span>  | <span data-ttu-id="57fad-133">ja</span><span class="sxs-lookup"><span data-stu-id="57fad-133">yes</span></span>      | <span data-ttu-id="57fad-134">Die Paket-ID Kleinbuchstaben</span><span class="sxs-lookup"><span data-stu-id="57fad-134">The package ID, lowercase</span></span>

<span data-ttu-id="57fad-135">Die `LOWER_ID` Wert ist die gewünschte Paket-ID, die klein gemäß den Vergleichsregeln von implementiert. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Methode.</span><span class="sxs-lookup"><span data-stu-id="57fad-135">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="57fad-136">Antwort</span><span class="sxs-lookup"><span data-stu-id="57fad-136">Response</span></span>

<span data-ttu-id="57fad-137">Wenn die Paketquelle keine Versionen der bereitgestellte Paket-ID verfügt, wird ein Statuscode "404" zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="57fad-137">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="57fad-138">Wenn die Paketquelle an eine oder mehrere Versionen verfügbar sind, wird ein Statuscode "200" zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="57fad-138">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="57fad-139">Der Antworttext ist ein JSON-Objekt, wenn Sie die folgende Eigenschaft:</span><span class="sxs-lookup"><span data-stu-id="57fad-139">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="57fad-140">name</span><span class="sxs-lookup"><span data-stu-id="57fad-140">Name</span></span>     | <span data-ttu-id="57fad-141">Typ</span><span class="sxs-lookup"><span data-stu-id="57fad-141">Type</span></span>             | <span data-ttu-id="57fad-142">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="57fad-142">Required</span></span> | <span data-ttu-id="57fad-143">Hinweise</span><span class="sxs-lookup"><span data-stu-id="57fad-143">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="57fad-144">Versionen</span><span class="sxs-lookup"><span data-stu-id="57fad-144">versions</span></span> | <span data-ttu-id="57fad-145">Array von Zeichenfolgen</span><span class="sxs-lookup"><span data-stu-id="57fad-145">array of strings</span></span> | <span data-ttu-id="57fad-146">ja</span><span class="sxs-lookup"><span data-stu-id="57fad-146">yes</span></span>      | <span data-ttu-id="57fad-147">Die Paket-IDs verfügbar</span><span class="sxs-lookup"><span data-stu-id="57fad-147">The package IDs available</span></span>

<span data-ttu-id="57fad-148">Die Zeichenfolgen in die `versions` Array sind alle klein, [normalisiert NuGet Versionszeichenfolgen](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="57fad-148">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="57fad-149">Die Versionszeichenfolgen enthalten keine Metadaten Build SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="57fad-149">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="57fad-150">Das Ziel ist, dass Versionszeichenfolgen, die in diesem Array gefunden wörtlich können, können Sie für verwendet werden die `LOWER_VERSION` Token in die folgenden Endpunkte gefunden.</span><span class="sxs-lookup"><span data-stu-id="57fad-150">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="57fad-151">Beispielanforderung</span><span class="sxs-lookup"><span data-stu-id="57fad-151">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="57fad-152">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="57fad-152">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="57fad-153">Herunterladen von Paketinhalt (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="57fad-153">Download package content (.nupkg)</span></span>

<span data-ttu-id="57fad-154">Wenn der Client bekannt, ein Paket-ID und eine Version ist und den Paketinhalt herunterladen möchte, müssen sie nur so erstellen Sie die folgende URL:</span><span class="sxs-lookup"><span data-stu-id="57fad-154">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="57fad-155">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="57fad-155">Request parameters</span></span>

<span data-ttu-id="57fad-156">name</span><span class="sxs-lookup"><span data-stu-id="57fad-156">Name</span></span>          | <span data-ttu-id="57fad-157">In</span><span class="sxs-lookup"><span data-stu-id="57fad-157">In</span></span>     | <span data-ttu-id="57fad-158">Typ</span><span class="sxs-lookup"><span data-stu-id="57fad-158">Type</span></span>   | <span data-ttu-id="57fad-159">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="57fad-159">Required</span></span> | <span data-ttu-id="57fad-160">Hinweise</span><span class="sxs-lookup"><span data-stu-id="57fad-160">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="57fad-161">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="57fad-161">LOWER_ID</span></span>      | <span data-ttu-id="57fad-162">URL</span><span class="sxs-lookup"><span data-stu-id="57fad-162">URL</span></span>    | <span data-ttu-id="57fad-163">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="57fad-163">string</span></span> | <span data-ttu-id="57fad-164">ja</span><span class="sxs-lookup"><span data-stu-id="57fad-164">yes</span></span>      | <span data-ttu-id="57fad-165">Die Paket-ID Kleinbuchstaben</span><span class="sxs-lookup"><span data-stu-id="57fad-165">The package ID, lowercase</span></span>
<span data-ttu-id="57fad-166">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="57fad-166">LOWER_VERSION</span></span> | <span data-ttu-id="57fad-167">URL</span><span class="sxs-lookup"><span data-stu-id="57fad-167">URL</span></span>    | <span data-ttu-id="57fad-168">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="57fad-168">string</span></span> | <span data-ttu-id="57fad-169">ja</span><span class="sxs-lookup"><span data-stu-id="57fad-169">yes</span></span>      | <span data-ttu-id="57fad-170">Die Paketversion normalisiert und klein</span><span class="sxs-lookup"><span data-stu-id="57fad-170">The package version, normalized and lowercased</span></span>

<span data-ttu-id="57fad-171">Beide `LOWER_ID` und `LOWER_VERSION` sind klein gemäß den Vergleichsregeln von implementiert. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Methode.</span><span class="sxs-lookup"><span data-stu-id="57fad-171">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="57fad-172">Die `LOWER_VERSION` ist die gewünschte Paketversion normalisiert mithilfe des NuGet-Version [Normalisierungsregeln](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="57fad-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="57fad-173">Dies bedeutet, dass dieser Build-Metadaten, die die SemVer 2.0.0-Spezifikation nicht zulässig ist in diesem Fall ausgeschlossen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="57fad-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="57fad-174">Antworttext</span><span class="sxs-lookup"><span data-stu-id="57fad-174">Response body</span></span>

<span data-ttu-id="57fad-175">Wenn das Paket auf die Paketquelle vorhanden ist, wird ein Statuscode "200" zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="57fad-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="57fad-176">Der Antworttext wird der Inhalt des Pakets selbst sein.</span><span class="sxs-lookup"><span data-stu-id="57fad-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="57fad-177">Wenn das Paket auf die Paketquelle nicht vorhanden ist, wird ein Statuscode "404" zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="57fad-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="57fad-178">Beispielanforderung</span><span class="sxs-lookup"><span data-stu-id="57fad-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="57fad-179">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="57fad-179">Sample response</span></span>

<span data-ttu-id="57fad-180">Der binäre Datenstrom, der NUPKG für Newtonsoft.Json 9.0.1 darstellt.</span><span class="sxs-lookup"><span data-stu-id="57fad-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="57fad-181">Paketmanifest (.nuspec) herunterladen</span><span class="sxs-lookup"><span data-stu-id="57fad-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="57fad-182">Wenn der Client bekannt, ein Paket-ID und eine Version ist und das Paketmanifest herunterladen möchte, müssen sie nur so erstellen Sie die folgende URL:</span><span class="sxs-lookup"><span data-stu-id="57fad-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="57fad-183">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="57fad-183">Request parameters</span></span>

<span data-ttu-id="57fad-184">name</span><span class="sxs-lookup"><span data-stu-id="57fad-184">Name</span></span>          | <span data-ttu-id="57fad-185">In</span><span class="sxs-lookup"><span data-stu-id="57fad-185">In</span></span>     | <span data-ttu-id="57fad-186">Typ</span><span class="sxs-lookup"><span data-stu-id="57fad-186">Type</span></span>    | <span data-ttu-id="57fad-187">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="57fad-187">Required</span></span> | <span data-ttu-id="57fad-188">Hinweise</span><span class="sxs-lookup"><span data-stu-id="57fad-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="57fad-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="57fad-189">LOWER_ID</span></span>      | <span data-ttu-id="57fad-190">URL</span><span class="sxs-lookup"><span data-stu-id="57fad-190">URL</span></span>    | <span data-ttu-id="57fad-191">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="57fad-191">string</span></span>  | <span data-ttu-id="57fad-192">ja</span><span class="sxs-lookup"><span data-stu-id="57fad-192">yes</span></span>      | <span data-ttu-id="57fad-193">Die Paket-ID Kleinbuchstaben</span><span class="sxs-lookup"><span data-stu-id="57fad-193">The package ID, lowercase</span></span>
<span data-ttu-id="57fad-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="57fad-194">LOWER_VERSION</span></span> | <span data-ttu-id="57fad-195">URL</span><span class="sxs-lookup"><span data-stu-id="57fad-195">URL</span></span>    | <span data-ttu-id="57fad-196">Ganze Zahl</span><span class="sxs-lookup"><span data-stu-id="57fad-196">integer</span></span> | <span data-ttu-id="57fad-197">ja</span><span class="sxs-lookup"><span data-stu-id="57fad-197">yes</span></span>      | <span data-ttu-id="57fad-198">Die Paketversion normalisiert und klein</span><span class="sxs-lookup"><span data-stu-id="57fad-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="57fad-199">Beide `LOWER_ID` und `LOWER_VERSION` sind klein gemäß den Vergleichsregeln von implementiert. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Methode.</span><span class="sxs-lookup"><span data-stu-id="57fad-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="57fad-200">Die `LOWER_VERSION` ist die gewünschte Paketversion normalisiert mithilfe des NuGet-Version [Normalisierungsregeln](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="57fad-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="57fad-201">Dies bedeutet, dass dieser Build-Metadaten, die die SemVer 2.0.0-Spezifikation nicht zulässig ist in diesem Fall ausgeschlossen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="57fad-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="57fad-202">Antworttext</span><span class="sxs-lookup"><span data-stu-id="57fad-202">Response body</span></span>

<span data-ttu-id="57fad-203">Wenn das Paket auf die Paketquelle vorhanden ist, wird ein Statuscode "200" zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="57fad-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="57fad-204">Der Antworttext werden Paketmanifest, also die .nuspec in die entsprechende .nupkg enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="57fad-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="57fad-205">Die .nuspec ist ein XML-Dokument.</span><span class="sxs-lookup"><span data-stu-id="57fad-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="57fad-206">Wenn das Paket auf die Paketquelle nicht vorhanden ist, wird ein Statuscode "404" zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="57fad-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="57fad-207">Beispielanforderung</span><span class="sxs-lookup"><span data-stu-id="57fad-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="57fad-208">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="57fad-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
