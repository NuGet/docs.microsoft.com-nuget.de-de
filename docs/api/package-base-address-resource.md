---
title: Paketinhalt, NuGet-API
description: Die Basisadresse des Pakets ist eine einfache Schnittstelle für das Paket selbst abrufen.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 740defc34077793b81fb35db73a2eee393ae3bac
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547153"
---
# <a name="package-content"></a><span data-ttu-id="24166-103">Paketinhalt</span><span class="sxs-lookup"><span data-stu-id="24166-103">Package Content</span></span>

<span data-ttu-id="24166-104">Es ist möglich, eine URL zum Abrufen des Pakets ein beliebiger Inhalt (die NUPKG-Datei) mithilfe der V3-API zu generieren.</span><span class="sxs-lookup"><span data-stu-id="24166-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="24166-105">Die Ressource, die zum Abrufen von Paketinhalt ist die `PackageBaseAddress` Ressource finden Sie in der [dienstindex](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="24166-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="24166-106">Diese Ressource ermöglicht auch die Ermittlung aller Versionen des Pakets aufgelistet oder nicht aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="24166-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="24166-107">Diese Ressource wird häufig als entweder die "Paket Basisadresse" oder "Flatfile-Container" bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="24166-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="24166-108">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="24166-108">Versioning</span></span>

<span data-ttu-id="24166-109">Die folgenden `@type` Wert wird verwendet:</span><span class="sxs-lookup"><span data-stu-id="24166-109">The following `@type` value is used:</span></span>

<span data-ttu-id="24166-110">@type-Wert</span><span class="sxs-lookup"><span data-stu-id="24166-110">@type value</span></span>              | <span data-ttu-id="24166-111">Hinweise</span><span class="sxs-lookup"><span data-stu-id="24166-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="24166-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="24166-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="24166-113">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="24166-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="24166-114">Basis-URL</span><span class="sxs-lookup"><span data-stu-id="24166-114">Base URL</span></span>

<span data-ttu-id="24166-115">Die base-URL für die folgenden APIs ist der Wert des der `@id` -Eigenschaft zusammen mit den oben genannten Ressourcen `@type` Wert.</span><span class="sxs-lookup"><span data-stu-id="24166-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="24166-116">Basis-URL im folgenden Dokument der Platzhalter `{@id}` verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="24166-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="24166-117">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="24166-117">HTTP methods</span></span>

<span data-ttu-id="24166-118">Alle URLs finden Sie in die Registrierung Unterstützung der HTTP-Methoden `GET` und `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="24166-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="24166-119">Auflisten von Paketversionen</span><span class="sxs-lookup"><span data-stu-id="24166-119">Enumerate package versions</span></span>

<span data-ttu-id="24166-120">Wenn der Client eine Paket-ID kann und ermitteln möchte, die Paket-Versionen des Pakets Quelle zur Verfügung stehen, die der Client kann eine vorhersagbare URL zum Auflisten aller Versionen des Pakets zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="24166-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="24166-121">Diese Liste soll eine "Liste" werden für die unten genannten Content Package-API.</span><span class="sxs-lookup"><span data-stu-id="24166-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="24166-122">Diese Liste enthält die beiden Paketversionen aufgeführt werden und nicht aufgeführte.</span><span class="sxs-lookup"><span data-stu-id="24166-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="24166-123">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="24166-123">Request parameters</span></span>

<span data-ttu-id="24166-124">name</span><span class="sxs-lookup"><span data-stu-id="24166-124">Name</span></span>     | <span data-ttu-id="24166-125">In</span><span class="sxs-lookup"><span data-stu-id="24166-125">In</span></span>     | <span data-ttu-id="24166-126">Typ</span><span class="sxs-lookup"><span data-stu-id="24166-126">Type</span></span>    | <span data-ttu-id="24166-127">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="24166-127">Required</span></span> | <span data-ttu-id="24166-128">Hinweise</span><span class="sxs-lookup"><span data-stu-id="24166-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="24166-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="24166-129">LOWER_ID</span></span> | <span data-ttu-id="24166-130">URL</span><span class="sxs-lookup"><span data-stu-id="24166-130">URL</span></span>    | <span data-ttu-id="24166-131">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="24166-131">string</span></span>  | <span data-ttu-id="24166-132">ja</span><span class="sxs-lookup"><span data-stu-id="24166-132">yes</span></span>      | <span data-ttu-id="24166-133">Die Paket-ID Kleinbuchstaben</span><span class="sxs-lookup"><span data-stu-id="24166-133">The package ID, lowercase</span></span>

<span data-ttu-id="24166-134">Die `LOWER_ID` Wert ist die gewünschte Paket-ID Kleinbuchstaben geändert, mithilfe von implementierten Regeln entspricht. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Methode.</span><span class="sxs-lookup"><span data-stu-id="24166-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="24166-135">Antwort</span><span class="sxs-lookup"><span data-stu-id="24166-135">Response</span></span>

<span data-ttu-id="24166-136">Wenn die Paketquelle keine Versionen der angegebenen Paket-ID verfügt, wird Statuscode 404 zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="24166-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="24166-137">Wenn die Paketquelle eine oder mehrere Versionen verfügt, wird ein Statuscode "200" zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="24166-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="24166-138">Der Antworttext ist ein JSON-Objekt mit der folgenden Eigenschaft:</span><span class="sxs-lookup"><span data-stu-id="24166-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="24166-139">name</span><span class="sxs-lookup"><span data-stu-id="24166-139">Name</span></span>     | <span data-ttu-id="24166-140">Typ</span><span class="sxs-lookup"><span data-stu-id="24166-140">Type</span></span>             | <span data-ttu-id="24166-141">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="24166-141">Required</span></span> | <span data-ttu-id="24166-142">Hinweise</span><span class="sxs-lookup"><span data-stu-id="24166-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="24166-143">Versionen</span><span class="sxs-lookup"><span data-stu-id="24166-143">versions</span></span> | <span data-ttu-id="24166-144">Array von Zeichenfolgen</span><span class="sxs-lookup"><span data-stu-id="24166-144">array of strings</span></span> | <span data-ttu-id="24166-145">ja</span><span class="sxs-lookup"><span data-stu-id="24166-145">yes</span></span>      | <span data-ttu-id="24166-146">Die Paket-IDs verfügbar</span><span class="sxs-lookup"><span data-stu-id="24166-146">The package IDs available</span></span>

<span data-ttu-id="24166-147">Die Zeichenfolgen in die `versions` Array sind alle Kleinbuchstaben geändert, [normalisiert NuGet-Versionszeichenfolgen](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="24166-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="24166-148">Die Versionszeichenfolgen enthalten keine SemVer 2.0.0-Build-Metadaten.</span><span class="sxs-lookup"><span data-stu-id="24166-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="24166-149">Die Absicht ist, finden Sie in diesem Array die Versionszeichenfolgen wörtlich können, können Sie für verwendet werden die `LOWER_VERSION` Token finden Sie in den folgenden Endpunkten.</span><span class="sxs-lookup"><span data-stu-id="24166-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="24166-150">Beispiel für eine Anforderung</span><span class="sxs-lookup"><span data-stu-id="24166-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="24166-151">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="24166-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="24166-152">Paketinhalt (NUPKG-Datei) herunterladen</span><span class="sxs-lookup"><span data-stu-id="24166-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="24166-153">Wenn der Client weiß, ein Paket-ID und die Version dass und den Paketinhalt herunterladen möchte, müssen sie nur die folgende URL zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="24166-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="24166-154">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="24166-154">Request parameters</span></span>

<span data-ttu-id="24166-155">name</span><span class="sxs-lookup"><span data-stu-id="24166-155">Name</span></span>          | <span data-ttu-id="24166-156">In</span><span class="sxs-lookup"><span data-stu-id="24166-156">In</span></span>     | <span data-ttu-id="24166-157">Typ</span><span class="sxs-lookup"><span data-stu-id="24166-157">Type</span></span>   | <span data-ttu-id="24166-158">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="24166-158">Required</span></span> | <span data-ttu-id="24166-159">Hinweise</span><span class="sxs-lookup"><span data-stu-id="24166-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="24166-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="24166-160">LOWER_ID</span></span>      | <span data-ttu-id="24166-161">URL</span><span class="sxs-lookup"><span data-stu-id="24166-161">URL</span></span>    | <span data-ttu-id="24166-162">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="24166-162">string</span></span> | <span data-ttu-id="24166-163">ja</span><span class="sxs-lookup"><span data-stu-id="24166-163">yes</span></span>      | <span data-ttu-id="24166-164">Die Paket-ID Kleinbuchstaben</span><span class="sxs-lookup"><span data-stu-id="24166-164">The package ID, lowercase</span></span>
<span data-ttu-id="24166-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="24166-165">LOWER_VERSION</span></span> | <span data-ttu-id="24166-166">URL</span><span class="sxs-lookup"><span data-stu-id="24166-166">URL</span></span>    | <span data-ttu-id="24166-167">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="24166-167">string</span></span> | <span data-ttu-id="24166-168">ja</span><span class="sxs-lookup"><span data-stu-id="24166-168">yes</span></span>      | <span data-ttu-id="24166-169">Die Paketversion, normalisiert, und klein schreiben</span><span class="sxs-lookup"><span data-stu-id="24166-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="24166-170">Beide `LOWER_ID` und `LOWER_VERSION` sind klein schreiben, die mithilfe von implementierten Regeln entspricht. NET [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="24166-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="24166-171">-Methode.</span><span class="sxs-lookup"><span data-stu-id="24166-171">method.</span></span>

<span data-ttu-id="24166-172">Die `LOWER_VERSION` wird mithilfe NuGets-Version die gewünschten Paketversion normalisiert [Normalisierungsregeln](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="24166-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="24166-173">Dies bedeutet, dass dieser Build-Metadaten, die von der SemVer 2.0.0-Spezifikation darf in diesem Fall ausgeschlossen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="24166-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="24166-174">Antworttext</span><span class="sxs-lookup"><span data-stu-id="24166-174">Response body</span></span>

<span data-ttu-id="24166-175">Wenn das Paket auf die Paketquelle vorhanden ist, wird ein Statuscode "200" zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="24166-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="24166-176">Der Antworttext werden der Inhalt des Pakets selbst.</span><span class="sxs-lookup"><span data-stu-id="24166-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="24166-177">Wenn das Paket auf die Paketquelle nicht vorhanden ist, wird der Statuscode 404 zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="24166-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="24166-178">Beispiel für eine Anforderung</span><span class="sxs-lookup"><span data-stu-id="24166-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="24166-179">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="24166-179">Sample response</span></span>

<span data-ttu-id="24166-180">Der binäre Stream, der die NUPKG-Datei für "newtonsoft.JSON 9.0.1" ist.</span><span class="sxs-lookup"><span data-stu-id="24166-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="24166-181">Das Paketmanifest (.nuspec) herunterladen</span><span class="sxs-lookup"><span data-stu-id="24166-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="24166-182">Wenn der Client weiß, ein Paket-ID und die Version dass und das Paketmanifest laden möchte, müssen sie nur die folgende URL zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="24166-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="24166-183">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="24166-183">Request parameters</span></span>

<span data-ttu-id="24166-184">name</span><span class="sxs-lookup"><span data-stu-id="24166-184">Name</span></span>          | <span data-ttu-id="24166-185">In</span><span class="sxs-lookup"><span data-stu-id="24166-185">In</span></span>     | <span data-ttu-id="24166-186">Typ</span><span class="sxs-lookup"><span data-stu-id="24166-186">Type</span></span>    | <span data-ttu-id="24166-187">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="24166-187">Required</span></span> | <span data-ttu-id="24166-188">Hinweise</span><span class="sxs-lookup"><span data-stu-id="24166-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="24166-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="24166-189">LOWER_ID</span></span>      | <span data-ttu-id="24166-190">URL</span><span class="sxs-lookup"><span data-stu-id="24166-190">URL</span></span>    | <span data-ttu-id="24166-191">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="24166-191">string</span></span>  | <span data-ttu-id="24166-192">ja</span><span class="sxs-lookup"><span data-stu-id="24166-192">yes</span></span>      | <span data-ttu-id="24166-193">Die Paket-ID Kleinbuchstaben</span><span class="sxs-lookup"><span data-stu-id="24166-193">The package ID, lowercase</span></span>
<span data-ttu-id="24166-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="24166-194">LOWER_VERSION</span></span> | <span data-ttu-id="24166-195">URL</span><span class="sxs-lookup"><span data-stu-id="24166-195">URL</span></span>    | <span data-ttu-id="24166-196">Ganze Zahl</span><span class="sxs-lookup"><span data-stu-id="24166-196">integer</span></span> | <span data-ttu-id="24166-197">ja</span><span class="sxs-lookup"><span data-stu-id="24166-197">yes</span></span>      | <span data-ttu-id="24166-198">Die Paketversion, normalisiert, und klein schreiben</span><span class="sxs-lookup"><span data-stu-id="24166-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="24166-199">Beide `LOWER_ID` und `LOWER_VERSION` sind klein schreiben, die mithilfe von implementierten Regeln entspricht. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Methode.</span><span class="sxs-lookup"><span data-stu-id="24166-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="24166-200">Die `LOWER_VERSION` wird mithilfe NuGets-Version die gewünschten Paketversion normalisiert [Normalisierungsregeln](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="24166-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="24166-201">Dies bedeutet, dass dieser Build-Metadaten, die von der SemVer 2.0.0-Spezifikation darf in diesem Fall ausgeschlossen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="24166-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="24166-202">Antworttext</span><span class="sxs-lookup"><span data-stu-id="24166-202">Response body</span></span>

<span data-ttu-id="24166-203">Wenn das Paket auf die Paketquelle vorhanden ist, wird ein Statuscode "200" zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="24166-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="24166-204">Der Antworttext werden das Paketmanifest, das im Abschnitt in der entsprechenden NUPKG-Datei enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="24166-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="24166-205">Im Abschnitt ist ein XML-Dokument.</span><span class="sxs-lookup"><span data-stu-id="24166-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="24166-206">Wenn das Paket auf die Paketquelle nicht vorhanden ist, wird der Statuscode 404 zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="24166-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="24166-207">Beispiel für eine Anforderung</span><span class="sxs-lookup"><span data-stu-id="24166-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="24166-208">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="24166-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
