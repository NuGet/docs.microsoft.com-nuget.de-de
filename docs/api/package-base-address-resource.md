---
title: Paket Inhalt, nuget-API
description: Die Paketbasis Adresse ist eine einfache Schnittstelle zum Abrufen des Pakets selbst.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 5ec6c0e17a3e8b9a3f156a48685bcaafe42c744b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488219"
---
# <a name="package-content"></a><span data-ttu-id="a83a9-103">Paket Inhalt</span><span class="sxs-lookup"><span data-stu-id="a83a9-103">Package Content</span></span>

<span data-ttu-id="a83a9-104">Es ist möglich, eine URL zum Abrufen des Inhalts eines beliebigen Pakets (die nupkg-Datei) mit der V3-API zu generieren.</span><span class="sxs-lookup"><span data-stu-id="a83a9-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="a83a9-105">Die Ressource, die zum Abrufen von Paket Inhalten verwendet `PackageBaseAddress` wird, ist die Ressource, die im [Dienst Index](service-index.md)gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="a83a9-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="a83a9-106">Diese Ressource ermöglicht außerdem die Ermittlung aller Versionen eines Pakets, die aufgelistet oder nicht aufgelistet sind.</span><span class="sxs-lookup"><span data-stu-id="a83a9-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="a83a9-107">Diese Ressource wird im Allgemeinen als "Paketbasis Adresse" oder als "flatcontainer" bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="a83a9-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="a83a9-108">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="a83a9-108">Versioning</span></span>

<span data-ttu-id="a83a9-109">Der folgende `@type` Wert wird verwendet:</span><span class="sxs-lookup"><span data-stu-id="a83a9-109">The following `@type` value is used:</span></span>

<span data-ttu-id="a83a9-110">@type -Wert</span><span class="sxs-lookup"><span data-stu-id="a83a9-110">@type value</span></span>              | <span data-ttu-id="a83a9-111">Hinweise</span><span class="sxs-lookup"><span data-stu-id="a83a9-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="a83a9-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="a83a9-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="a83a9-113">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="a83a9-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="a83a9-114">Basis-URL</span><span class="sxs-lookup"><span data-stu-id="a83a9-114">Base URL</span></span>

<span data-ttu-id="a83a9-115">Die Basis-URL für die folgenden APIs ist der Wert der `@id` Eigenschaft, die dem oben erwähnten `@type` Ressourcen Wert zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="a83a9-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="a83a9-116">Im folgenden Dokument wird die Platzhalter-Basis- `{@id}` URL verwendet.</span><span class="sxs-lookup"><span data-stu-id="a83a9-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="a83a9-117">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="a83a9-117">HTTP methods</span></span>

<span data-ttu-id="a83a9-118">Alle URLs, die in der Registrierungs Ressource gefunden werden, `GET` unter `HEAD`stützen die HTTP-Methoden und.</span><span class="sxs-lookup"><span data-stu-id="a83a9-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="a83a9-119">Auflisten von Paketversionen</span><span class="sxs-lookup"><span data-stu-id="a83a9-119">Enumerate package versions</span></span>

<span data-ttu-id="a83a9-120">Wenn der Client eine Paket-ID kennt und ermitteln möchte, welche Paketversionen von der Paketquelle verfügbar sind, kann der Client eine vorhersagbare URL zum Auflisten aller Paketversionen erstellen.</span><span class="sxs-lookup"><span data-stu-id="a83a9-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="a83a9-121">Diese Liste ist als "Verzeichnis Auflistung" für die weiter unten erwähnte Paket Inhalts-API gedacht.</span><span class="sxs-lookup"><span data-stu-id="a83a9-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="a83a9-122">Diese Liste enthält sowohl die aufgelisteten als auch die nicht aufgelisteten Paketversionen.</span><span class="sxs-lookup"><span data-stu-id="a83a9-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="a83a9-123">Anforderungs Parameter</span><span class="sxs-lookup"><span data-stu-id="a83a9-123">Request parameters</span></span>

<span data-ttu-id="a83a9-124">name</span><span class="sxs-lookup"><span data-stu-id="a83a9-124">Name</span></span>     | <span data-ttu-id="a83a9-125">In</span><span class="sxs-lookup"><span data-stu-id="a83a9-125">In</span></span>     | <span data-ttu-id="a83a9-126">Typ</span><span class="sxs-lookup"><span data-stu-id="a83a9-126">Type</span></span>    | <span data-ttu-id="a83a9-127">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="a83a9-127">Required</span></span> | <span data-ttu-id="a83a9-128">Hinweise</span><span class="sxs-lookup"><span data-stu-id="a83a9-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="a83a9-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="a83a9-129">LOWER_ID</span></span> | <span data-ttu-id="a83a9-130">URL</span><span class="sxs-lookup"><span data-stu-id="a83a9-130">URL</span></span>    | <span data-ttu-id="a83a9-131">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="a83a9-131">string</span></span>  | <span data-ttu-id="a83a9-132">ja</span><span class="sxs-lookup"><span data-stu-id="a83a9-132">yes</span></span>      | <span data-ttu-id="a83a9-133">Die Paket-ID, Kleinbuchstaben</span><span class="sxs-lookup"><span data-stu-id="a83a9-133">The package ID, lowercase</span></span>

<span data-ttu-id="a83a9-134">Der `LOWER_ID` Wert ist die gewünschte Paket-ID in Kleinbuchstaben unter Verwendung der Regeln, die von implementiert werden. NET- [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Methode.</span><span class="sxs-lookup"><span data-stu-id="a83a9-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="a83a9-135">Antwort</span><span class="sxs-lookup"><span data-stu-id="a83a9-135">Response</span></span>

<span data-ttu-id="a83a9-136">Wenn die Paketquelle keine Versionen der angegebenen Paket-ID enthält, wird ein 404-Statuscode zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="a83a9-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="a83a9-137">Wenn die Paketquelle mindestens eine Version aufweist, wird ein 200-Statuscode zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="a83a9-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="a83a9-138">Der Antworttext ist ein JSON-Objekt mit der folgenden Eigenschaft:</span><span class="sxs-lookup"><span data-stu-id="a83a9-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="a83a9-139">Name</span><span class="sxs-lookup"><span data-stu-id="a83a9-139">Name</span></span>     | <span data-ttu-id="a83a9-140">Typ</span><span class="sxs-lookup"><span data-stu-id="a83a9-140">Type</span></span>             | <span data-ttu-id="a83a9-141">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="a83a9-141">Required</span></span> | <span data-ttu-id="a83a9-142">Hinweise</span><span class="sxs-lookup"><span data-stu-id="a83a9-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="a83a9-143">Versionen</span><span class="sxs-lookup"><span data-stu-id="a83a9-143">versions</span></span> | <span data-ttu-id="a83a9-144">Array von Zeichen folgen</span><span class="sxs-lookup"><span data-stu-id="a83a9-144">array of strings</span></span> | <span data-ttu-id="a83a9-145">ja</span><span class="sxs-lookup"><span data-stu-id="a83a9-145">yes</span></span>      | <span data-ttu-id="a83a9-146">Verfügbare Paket-IDs</span><span class="sxs-lookup"><span data-stu-id="a83a9-146">The package IDs available</span></span>

<span data-ttu-id="a83a9-147">Die Zeichen folgen im `versions` Array sind alle in Kleinbuchstaben, [normalisierten nuget-Versions](../concepts/package-versioning.md#normalized-version-numbers)Zeichenfolgen.</span><span class="sxs-lookup"><span data-stu-id="a83a9-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="a83a9-148">Die Versions Zeichenfolgen enthalten keine semver 2.0.0 Build-Metadaten.</span><span class="sxs-lookup"><span data-stu-id="a83a9-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="a83a9-149">Der Zweck ist, dass die in diesem Array gefundenen Versions Zeichenfolgen wörtlich für die `LOWER_VERSION` Token verwendet werden können, die in den folgenden Endpunkten gefunden werden.</span><span class="sxs-lookup"><span data-stu-id="a83a9-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a83a9-150">Beispiel Anforderung</span><span class="sxs-lookup"><span data-stu-id="a83a9-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="a83a9-151">Beispiel Antwort</span><span class="sxs-lookup"><span data-stu-id="a83a9-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="a83a9-152">Paket Inhalt herunterladen (nupkg-Datei)</span><span class="sxs-lookup"><span data-stu-id="a83a9-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="a83a9-153">Wenn der Client eine Paket-ID und-Version kennt und den Paket Inhalt herunterladen möchte, muss er lediglich die folgende URL erstellen:</span><span class="sxs-lookup"><span data-stu-id="a83a9-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="a83a9-154">Anforderungs Parameter</span><span class="sxs-lookup"><span data-stu-id="a83a9-154">Request parameters</span></span>

<span data-ttu-id="a83a9-155">name</span><span class="sxs-lookup"><span data-stu-id="a83a9-155">Name</span></span>          | <span data-ttu-id="a83a9-156">In</span><span class="sxs-lookup"><span data-stu-id="a83a9-156">In</span></span>     | <span data-ttu-id="a83a9-157">Typ</span><span class="sxs-lookup"><span data-stu-id="a83a9-157">Type</span></span>   | <span data-ttu-id="a83a9-158">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="a83a9-158">Required</span></span> | <span data-ttu-id="a83a9-159">Hinweise</span><span class="sxs-lookup"><span data-stu-id="a83a9-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="a83a9-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="a83a9-160">LOWER_ID</span></span>      | <span data-ttu-id="a83a9-161">URL</span><span class="sxs-lookup"><span data-stu-id="a83a9-161">URL</span></span>    | <span data-ttu-id="a83a9-162">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="a83a9-162">string</span></span> | <span data-ttu-id="a83a9-163">ja</span><span class="sxs-lookup"><span data-stu-id="a83a9-163">yes</span></span>      | <span data-ttu-id="a83a9-164">Die Paket-ID, Kleinbuchstaben</span><span class="sxs-lookup"><span data-stu-id="a83a9-164">The package ID, lowercase</span></span>
<span data-ttu-id="a83a9-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="a83a9-165">LOWER_VERSION</span></span> | <span data-ttu-id="a83a9-166">URL</span><span class="sxs-lookup"><span data-stu-id="a83a9-166">URL</span></span>    | <span data-ttu-id="a83a9-167">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="a83a9-167">string</span></span> | <span data-ttu-id="a83a9-168">ja</span><span class="sxs-lookup"><span data-stu-id="a83a9-168">yes</span></span>      | <span data-ttu-id="a83a9-169">Die Paketversion, normalisierte und Kleinbuchstaben</span><span class="sxs-lookup"><span data-stu-id="a83a9-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="a83a9-170">Sowohl `LOWER_ID` als `LOWER_VERSION` auch werden mithilfe der von implementierten Regeln in Kleinbuchstaben geschrieben. NET es[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="a83a9-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="a83a9-171">-Methode.</span><span class="sxs-lookup"><span data-stu-id="a83a9-171">method.</span></span>

<span data-ttu-id="a83a9-172">Die `LOWER_VERSION` ist die gewünschte Paketversion, die mithilfe von nuget-Versions [normalisierungs Regeln](../concepts/package-versioning.md#normalized-version-numbers)normalisiert wird.</span><span class="sxs-lookup"><span data-stu-id="a83a9-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="a83a9-173">Dies bedeutet, dass buildmetadaten, die von der semver 2.0.0-Spezifikation zugelassen werden, in diesem Fall ausgeschlossen werden müssen.</span><span class="sxs-lookup"><span data-stu-id="a83a9-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="a83a9-174">Antworttext</span><span class="sxs-lookup"><span data-stu-id="a83a9-174">Response body</span></span>

<span data-ttu-id="a83a9-175">Wenn das Paket in der Paketquelle vorhanden ist, wird ein 200-Statuscode zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="a83a9-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="a83a9-176">Der Antworttext ist der Paket Inhalt selbst.</span><span class="sxs-lookup"><span data-stu-id="a83a9-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="a83a9-177">Wenn das Paket nicht in der Paketquelle vorhanden ist, wird der Statuscode 404 zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="a83a9-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a83a9-178">Beispiel Anforderung</span><span class="sxs-lookup"><span data-stu-id="a83a9-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="a83a9-179">Beispiel Antwort</span><span class="sxs-lookup"><span data-stu-id="a83a9-179">Sample response</span></span>

<span data-ttu-id="a83a9-180">Der binäre Stream, bei dem es sich um die nupkg-9.0.1 für newtonsoft. JSON handelt.</span><span class="sxs-lookup"><span data-stu-id="a83a9-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="a83a9-181">Paket Manifest herunterladen (. nuspec)</span><span class="sxs-lookup"><span data-stu-id="a83a9-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="a83a9-182">Wenn der Client eine Paket-ID und-Version kennt und das Paket Manifest herunterladen möchte, muss nur die folgende URL erstellt werden:</span><span class="sxs-lookup"><span data-stu-id="a83a9-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="a83a9-183">Anforderungs Parameter</span><span class="sxs-lookup"><span data-stu-id="a83a9-183">Request parameters</span></span>

<span data-ttu-id="a83a9-184">name</span><span class="sxs-lookup"><span data-stu-id="a83a9-184">Name</span></span>          | <span data-ttu-id="a83a9-185">In</span><span class="sxs-lookup"><span data-stu-id="a83a9-185">In</span></span>     | <span data-ttu-id="a83a9-186">Typ</span><span class="sxs-lookup"><span data-stu-id="a83a9-186">Type</span></span>   | <span data-ttu-id="a83a9-187">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="a83a9-187">Required</span></span> | <span data-ttu-id="a83a9-188">Hinweise</span><span class="sxs-lookup"><span data-stu-id="a83a9-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="a83a9-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="a83a9-189">LOWER_ID</span></span>      | <span data-ttu-id="a83a9-190">URL</span><span class="sxs-lookup"><span data-stu-id="a83a9-190">URL</span></span>    | <span data-ttu-id="a83a9-191">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="a83a9-191">string</span></span> | <span data-ttu-id="a83a9-192">ja</span><span class="sxs-lookup"><span data-stu-id="a83a9-192">yes</span></span>      | <span data-ttu-id="a83a9-193">Die Paket-ID, Kleinbuchstaben</span><span class="sxs-lookup"><span data-stu-id="a83a9-193">The package ID, lowercase</span></span>
<span data-ttu-id="a83a9-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="a83a9-194">LOWER_VERSION</span></span> | <span data-ttu-id="a83a9-195">URL</span><span class="sxs-lookup"><span data-stu-id="a83a9-195">URL</span></span>    | <span data-ttu-id="a83a9-196">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="a83a9-196">string</span></span> | <span data-ttu-id="a83a9-197">ja</span><span class="sxs-lookup"><span data-stu-id="a83a9-197">yes</span></span>      | <span data-ttu-id="a83a9-198">Die Paketversion, normalisierte und Kleinbuchstaben</span><span class="sxs-lookup"><span data-stu-id="a83a9-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="a83a9-199">Sowohl `LOWER_ID` als `LOWER_VERSION` auch werden mithilfe der von implementierten Regeln in Kleinbuchstaben geschrieben. NET- [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Methode.</span><span class="sxs-lookup"><span data-stu-id="a83a9-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="a83a9-200">Die `LOWER_VERSION` ist die gewünschte Paketversion, die mithilfe von nuget-Versions [normalisierungs Regeln](../concepts/package-versioning.md#normalized-version-numbers)normalisiert wird.</span><span class="sxs-lookup"><span data-stu-id="a83a9-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="a83a9-201">Dies bedeutet, dass buildmetadaten, die von der semver 2.0.0-Spezifikation zugelassen werden, in diesem Fall ausgeschlossen werden müssen.</span><span class="sxs-lookup"><span data-stu-id="a83a9-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="a83a9-202">Antworttext</span><span class="sxs-lookup"><span data-stu-id="a83a9-202">Response body</span></span>

<span data-ttu-id="a83a9-203">Wenn das Paket in der Paketquelle vorhanden ist, wird ein 200-Statuscode zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="a83a9-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="a83a9-204">Der Antworttext ist das Paket Manifest, bei dem es sich um die nuspec-Datei im entsprechenden nupkg-Element handelt.</span><span class="sxs-lookup"><span data-stu-id="a83a9-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="a83a9-205">Die nuspec-Datei ist ein XML-Dokument.</span><span class="sxs-lookup"><span data-stu-id="a83a9-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="a83a9-206">Wenn das Paket nicht in der Paketquelle vorhanden ist, wird der Statuscode 404 zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="a83a9-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a83a9-207">Beispiel Anforderung</span><span class="sxs-lookup"><span data-stu-id="a83a9-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="a83a9-208">Beispiel Antwort</span><span class="sxs-lookup"><span data-stu-id="a83a9-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
