---
title: Paket Inhalt, nuget-API
description: Die Paketbasis Adresse ist eine einfache Schnittstelle zum Abrufen des Pakets selbst.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 8ea03ece635aa06e22032c4fb43ce932dbdf717c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773929"
---
# <a name="package-content"></a><span data-ttu-id="925f4-103">Paketinhalt</span><span class="sxs-lookup"><span data-stu-id="925f4-103">Package Content</span></span>

<span data-ttu-id="925f4-104">Es ist möglich, eine URL zum Abrufen des Inhalts eines beliebigen Pakets (die nupkg-Datei) mit der V3-API zu generieren.</span><span class="sxs-lookup"><span data-stu-id="925f4-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="925f4-105">Die Ressource, die zum Abrufen von Paket Inhalten verwendet wird, ist die Ressource, die `PackageBaseAddress` im [Dienst Index](service-index.md)gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="925f4-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="925f4-106">Diese Ressource ermöglicht außerdem die Ermittlung aller Versionen eines Pakets, die aufgelistet oder nicht aufgelistet sind.</span><span class="sxs-lookup"><span data-stu-id="925f4-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="925f4-107">Diese Ressource wird im Allgemeinen als "Paketbasis Adresse" oder als "flatcontainer" bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="925f4-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="925f4-108">Versionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="925f4-108">Versioning</span></span>

<span data-ttu-id="925f4-109">Der folgende `@type` Wert wird verwendet:</span><span class="sxs-lookup"><span data-stu-id="925f4-109">The following `@type` value is used:</span></span>

<span data-ttu-id="925f4-110">Wert vom Typ @type</span><span class="sxs-lookup"><span data-stu-id="925f4-110">@type value</span></span>              | <span data-ttu-id="925f4-111">Hinweise</span><span class="sxs-lookup"><span data-stu-id="925f4-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="925f4-112">Packagebaseaddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="925f4-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="925f4-113">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="925f4-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="925f4-114">Basis-URL</span><span class="sxs-lookup"><span data-stu-id="925f4-114">Base URL</span></span>

<span data-ttu-id="925f4-115">Die Basis-URL für die folgenden APIs ist der Wert der `@id` Eigenschaft, die dem oben erwähnten Ressourcen Wert zugeordnet ist `@type` .</span><span class="sxs-lookup"><span data-stu-id="925f4-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="925f4-116">Im folgenden Dokument wird die Platzhalter-Basis-URL `{@id}` verwendet.</span><span class="sxs-lookup"><span data-stu-id="925f4-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="925f4-117">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="925f4-117">HTTP methods</span></span>

<span data-ttu-id="925f4-118">Alle URLs, die in der Registrierungs Ressource gefunden werden, unterstützen die HTTP `GET` -Methoden und `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="925f4-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="925f4-119">Auflisten von Paketversionen</span><span class="sxs-lookup"><span data-stu-id="925f4-119">Enumerate package versions</span></span>

<span data-ttu-id="925f4-120">Wenn der Client eine Paket-ID kennt und ermitteln möchte, welche Paketversionen von der Paketquelle verfügbar sind, kann der Client eine vorhersagbare URL zum Auflisten aller Paketversionen erstellen.</span><span class="sxs-lookup"><span data-stu-id="925f4-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="925f4-121">Diese Liste ist als "Verzeichnis Auflistung" für die weiter unten erwähnte Paket Inhalts-API gedacht.</span><span class="sxs-lookup"><span data-stu-id="925f4-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="925f4-122">Diese Liste enthält sowohl die aufgelisteten als auch die nicht aufgelisteten Paketversionen.</span><span class="sxs-lookup"><span data-stu-id="925f4-122">This list contains both listed and unlisted package versions.</span></span>

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a><span data-ttu-id="925f4-123">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="925f4-123">Request parameters</span></span>

<span data-ttu-id="925f4-124">Name</span><span class="sxs-lookup"><span data-stu-id="925f4-124">Name</span></span>     | <span data-ttu-id="925f4-125">In</span><span class="sxs-lookup"><span data-stu-id="925f4-125">In</span></span>     | <span data-ttu-id="925f4-126">Typ</span><span class="sxs-lookup"><span data-stu-id="925f4-126">Type</span></span>    | <span data-ttu-id="925f4-127">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="925f4-127">Required</span></span> | <span data-ttu-id="925f4-128">Notizen</span><span class="sxs-lookup"><span data-stu-id="925f4-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="925f4-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="925f4-129">LOWER_ID</span></span> | <span data-ttu-id="925f4-130">URL</span><span class="sxs-lookup"><span data-stu-id="925f4-130">URL</span></span>    | <span data-ttu-id="925f4-131">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="925f4-131">string</span></span>  | <span data-ttu-id="925f4-132">ja</span><span class="sxs-lookup"><span data-stu-id="925f4-132">yes</span></span>      | <span data-ttu-id="925f4-133">Die Paket-ID, Kleinbuchstaben</span><span class="sxs-lookup"><span data-stu-id="925f4-133">The package ID, lowercased</span></span>

<span data-ttu-id="925f4-134">Der `LOWER_ID` Wert ist die gewünschte Paket-ID in Kleinbuchstaben unter Verwendung der Regeln, die von implementiert werden. NET- [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) Methode.</span><span class="sxs-lookup"><span data-stu-id="925f4-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) method.</span></span>

### <a name="response"></a><span data-ttu-id="925f4-135">Antwort</span><span class="sxs-lookup"><span data-stu-id="925f4-135">Response</span></span>

<span data-ttu-id="925f4-136">Wenn die Paketquelle keine Versionen der angegebenen Paket-ID enthält, wird ein 404-Statuscode zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="925f4-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="925f4-137">Wenn die Paketquelle mindestens eine Version aufweist, wird ein 200-Statuscode zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="925f4-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="925f4-138">Der Antworttext ist ein JSON-Objekt mit der folgenden Eigenschaft:</span><span class="sxs-lookup"><span data-stu-id="925f4-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="925f4-139">Name</span><span class="sxs-lookup"><span data-stu-id="925f4-139">Name</span></span>     | <span data-ttu-id="925f4-140">Typ</span><span class="sxs-lookup"><span data-stu-id="925f4-140">Type</span></span>             | <span data-ttu-id="925f4-141">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="925f4-141">Required</span></span> | <span data-ttu-id="925f4-142">Notizen</span><span class="sxs-lookup"><span data-stu-id="925f4-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="925f4-143">versions</span><span class="sxs-lookup"><span data-stu-id="925f4-143">versions</span></span> | <span data-ttu-id="925f4-144">array of strings</span><span class="sxs-lookup"><span data-stu-id="925f4-144">array of strings</span></span> | <span data-ttu-id="925f4-145">ja</span><span class="sxs-lookup"><span data-stu-id="925f4-145">yes</span></span>      | <span data-ttu-id="925f4-146">Verfügbare Versionen</span><span class="sxs-lookup"><span data-stu-id="925f4-146">The versions available</span></span>

<span data-ttu-id="925f4-147">Die Zeichen folgen im `versions` Array sind alle in Kleinbuchstaben, [normalisierten nuget-Versions](../concepts/package-versioning.md#normalized-version-numbers)Zeichenfolgen.</span><span class="sxs-lookup"><span data-stu-id="925f4-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="925f4-148">Die Versions Zeichenfolgen enthalten keine semver 2.0.0 Build-Metadaten.</span><span class="sxs-lookup"><span data-stu-id="925f4-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="925f4-149">Der Zweck ist, dass die in diesem Array gefundenen Versions Zeichenfolgen wörtlich für die Token verwendet werden können, die `LOWER_VERSION` in den folgenden Endpunkten gefunden werden.</span><span class="sxs-lookup"><span data-stu-id="925f4-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="925f4-150">Beispiel für eine Anforderung</span><span class="sxs-lookup"><span data-stu-id="925f4-150">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a><span data-ttu-id="925f4-151">Beispiel für eine Antwort</span><span class="sxs-lookup"><span data-stu-id="925f4-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="925f4-152">Paket Inhalt herunterladen (nupkg-Datei)</span><span class="sxs-lookup"><span data-stu-id="925f4-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="925f4-153">Wenn der Client eine Paket-ID und-Version kennt und den Paket Inhalt herunterladen möchte, muss er lediglich die folgende URL erstellen:</span><span class="sxs-lookup"><span data-stu-id="925f4-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a><span data-ttu-id="925f4-154">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="925f4-154">Request parameters</span></span>

<span data-ttu-id="925f4-155">Name</span><span class="sxs-lookup"><span data-stu-id="925f4-155">Name</span></span>          | <span data-ttu-id="925f4-156">In</span><span class="sxs-lookup"><span data-stu-id="925f4-156">In</span></span>     | <span data-ttu-id="925f4-157">Typ</span><span class="sxs-lookup"><span data-stu-id="925f4-157">Type</span></span>   | <span data-ttu-id="925f4-158">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="925f4-158">Required</span></span> | <span data-ttu-id="925f4-159">Notizen</span><span class="sxs-lookup"><span data-stu-id="925f4-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="925f4-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="925f4-160">LOWER_ID</span></span>      | <span data-ttu-id="925f4-161">URL</span><span class="sxs-lookup"><span data-stu-id="925f4-161">URL</span></span>    | <span data-ttu-id="925f4-162">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="925f4-162">string</span></span> | <span data-ttu-id="925f4-163">ja</span><span class="sxs-lookup"><span data-stu-id="925f4-163">yes</span></span>      | <span data-ttu-id="925f4-164">Die Paket-ID, Kleinbuchstaben</span><span class="sxs-lookup"><span data-stu-id="925f4-164">The package ID, lowercase</span></span>
<span data-ttu-id="925f4-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="925f4-165">LOWER_VERSION</span></span> | <span data-ttu-id="925f4-166">URL</span><span class="sxs-lookup"><span data-stu-id="925f4-166">URL</span></span>    | <span data-ttu-id="925f4-167">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="925f4-167">string</span></span> | <span data-ttu-id="925f4-168">ja</span><span class="sxs-lookup"><span data-stu-id="925f4-168">yes</span></span>      | <span data-ttu-id="925f4-169">Die Paketversion, normalisierte und Kleinbuchstaben</span><span class="sxs-lookup"><span data-stu-id="925f4-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="925f4-170">Sowohl `LOWER_ID` als auch `LOWER_VERSION` werden mithilfe der von implementierten Regeln in Kleinbuchstaben geschrieben. NET es [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="925f4-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true)</span></span>
<span data-ttu-id="925f4-171">-Methode.</span><span class="sxs-lookup"><span data-stu-id="925f4-171">method.</span></span>

<span data-ttu-id="925f4-172">Die `LOWER_VERSION` ist die gewünschte Paketversion, die mithilfe von nuget-Versions [normalisierungs Regeln](../concepts/package-versioning.md#normalized-version-numbers)normalisiert wird.</span><span class="sxs-lookup"><span data-stu-id="925f4-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="925f4-173">Dies bedeutet, dass buildmetadaten, die von der semver 2.0.0-Spezifikation zugelassen werden, in diesem Fall ausgeschlossen werden müssen.</span><span class="sxs-lookup"><span data-stu-id="925f4-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="925f4-174">Antworttext</span><span class="sxs-lookup"><span data-stu-id="925f4-174">Response body</span></span>

<span data-ttu-id="925f4-175">Wenn das Paket in der Paketquelle vorhanden ist, wird ein 200-Statuscode zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="925f4-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="925f4-176">Der Antworttext ist der Paket Inhalt selbst.</span><span class="sxs-lookup"><span data-stu-id="925f4-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="925f4-177">Wenn das Paket nicht in der Paketquelle vorhanden ist, wird der Statuscode 404 zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="925f4-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="925f4-178">Beispiel für eine Anforderung</span><span class="sxs-lookup"><span data-stu-id="925f4-178">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a><span data-ttu-id="925f4-179">Beispiel für eine Antwort</span><span class="sxs-lookup"><span data-stu-id="925f4-179">Sample response</span></span>

<span data-ttu-id="925f4-180">Der binäre Stream, bei dem es sich um die. nupkg-Newtonsoft.Jsauf 9.0.1 handelt.</span><span class="sxs-lookup"><span data-stu-id="925f4-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="925f4-181">Paket Manifest herunterladen (. nuspec)</span><span class="sxs-lookup"><span data-stu-id="925f4-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="925f4-182">Wenn der Client eine Paket-ID und-Version kennt und das Paket Manifest herunterladen möchte, muss nur die folgende URL erstellt werden:</span><span class="sxs-lookup"><span data-stu-id="925f4-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a><span data-ttu-id="925f4-183">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="925f4-183">Request parameters</span></span>

<span data-ttu-id="925f4-184">Name</span><span class="sxs-lookup"><span data-stu-id="925f4-184">Name</span></span>          | <span data-ttu-id="925f4-185">In</span><span class="sxs-lookup"><span data-stu-id="925f4-185">In</span></span>     | <span data-ttu-id="925f4-186">Typ</span><span class="sxs-lookup"><span data-stu-id="925f4-186">Type</span></span>   | <span data-ttu-id="925f4-187">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="925f4-187">Required</span></span> | <span data-ttu-id="925f4-188">Notizen</span><span class="sxs-lookup"><span data-stu-id="925f4-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="925f4-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="925f4-189">LOWER_ID</span></span>      | <span data-ttu-id="925f4-190">URL</span><span class="sxs-lookup"><span data-stu-id="925f4-190">URL</span></span>    | <span data-ttu-id="925f4-191">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="925f4-191">string</span></span> | <span data-ttu-id="925f4-192">ja</span><span class="sxs-lookup"><span data-stu-id="925f4-192">yes</span></span>      | <span data-ttu-id="925f4-193">Die Paket-ID, Kleinbuchstaben</span><span class="sxs-lookup"><span data-stu-id="925f4-193">The package ID, lowercase</span></span>
<span data-ttu-id="925f4-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="925f4-194">LOWER_VERSION</span></span> | <span data-ttu-id="925f4-195">URL</span><span class="sxs-lookup"><span data-stu-id="925f4-195">URL</span></span>    | <span data-ttu-id="925f4-196">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="925f4-196">string</span></span> | <span data-ttu-id="925f4-197">ja</span><span class="sxs-lookup"><span data-stu-id="925f4-197">yes</span></span>      | <span data-ttu-id="925f4-198">Die Paketversion, normalisierte und Kleinbuchstaben</span><span class="sxs-lookup"><span data-stu-id="925f4-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="925f4-199">Sowohl `LOWER_ID` als auch `LOWER_VERSION` werden mithilfe der von implementierten Regeln in Kleinbuchstaben geschrieben. NET- [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) Methode.</span><span class="sxs-lookup"><span data-stu-id="925f4-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) method.</span></span>

<span data-ttu-id="925f4-200">Die `LOWER_VERSION` ist die gewünschte Paketversion, die mithilfe von nuget-Versions [normalisierungs Regeln](../concepts/package-versioning.md#normalized-version-numbers)normalisiert wird.</span><span class="sxs-lookup"><span data-stu-id="925f4-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="925f4-201">Dies bedeutet, dass buildmetadaten, die von der semver 2.0.0-Spezifikation zugelassen werden, in diesem Fall ausgeschlossen werden müssen.</span><span class="sxs-lookup"><span data-stu-id="925f4-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="925f4-202">Antworttext</span><span class="sxs-lookup"><span data-stu-id="925f4-202">Response body</span></span>

<span data-ttu-id="925f4-203">Wenn das Paket in der Paketquelle vorhanden ist, wird ein 200-Statuscode zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="925f4-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="925f4-204">Der Antworttext ist das Paket Manifest, bei dem es sich um die nuspec-Datei im entsprechenden nupkg-Element handelt.</span><span class="sxs-lookup"><span data-stu-id="925f4-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="925f4-205">Die nuspec-Datei ist ein XML-Dokument.</span><span class="sxs-lookup"><span data-stu-id="925f4-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="925f4-206">Wenn das Paket nicht in der Paketquelle vorhanden ist, wird der Statuscode 404 zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="925f4-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="925f4-207">Beispiel für eine Anforderung</span><span class="sxs-lookup"><span data-stu-id="925f4-207">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a><span data-ttu-id="925f4-208">Beispiel für eine Antwort</span><span class="sxs-lookup"><span data-stu-id="925f4-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
