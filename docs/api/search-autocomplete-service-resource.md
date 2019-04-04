---
title: AutoVervollständigen-Funktion, NuGet-API
description: Der Search-Dienst für automatische Vervollständigung unterstützt interaktive Suche in der Paket-IDs und Versionen.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fdc3ad8aa239a42d8a4c169a757715e856bdcb41
ms.sourcegitcommit: 9f94e00428d83aef4a7a87db679129eff7720c59
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/03/2019
ms.locfileid: "58911048"
---
# <a name="autocomplete"></a><span data-ttu-id="d9b88-103">AutoVervollständigen</span><span class="sxs-lookup"><span data-stu-id="d9b88-103">Autocomplete</span></span>

<span data-ttu-id="d9b88-104">Es ist möglich, eine Paket-ID und Version AutoVervollständigen Erfahrung mit der V3-API zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="d9b88-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="d9b88-105">Die Ressource, die zum Durchführen von AutoVervollständigen-Abfragen ist die `SearchAutocompleteService` Ressource finden Sie in der [dienstindex](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="d9b88-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="d9b88-106">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="d9b88-106">Versioning</span></span>

<span data-ttu-id="d9b88-107">Die folgenden `@type` Werte werden verwendet:</span><span class="sxs-lookup"><span data-stu-id="d9b88-107">The following `@type` values are used:</span></span>

<span data-ttu-id="d9b88-108">@type-Wert</span><span class="sxs-lookup"><span data-stu-id="d9b88-108">@type value</span></span>                          | <span data-ttu-id="d9b88-109">Hinweise</span><span class="sxs-lookup"><span data-stu-id="d9b88-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="d9b88-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="d9b88-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="d9b88-111">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="d9b88-111">The initial release</span></span>
<span data-ttu-id="d9b88-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="d9b88-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="d9b88-113">Alias der</span><span class="sxs-lookup"><span data-stu-id="d9b88-113">Alias of</span></span> `SearchAutocompleteService`
<span data-ttu-id="d9b88-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="d9b88-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="d9b88-115">Alias der</span><span class="sxs-lookup"><span data-stu-id="d9b88-115">Alias of</span></span> `SearchAutocompleteService`

## <a name="base-url"></a><span data-ttu-id="d9b88-116">Basis-URL</span><span class="sxs-lookup"><span data-stu-id="d9b88-116">Base URL</span></span>

<span data-ttu-id="d9b88-117">Die base-URL für die folgenden APIs ist der Wert des der `@id` Eigenschaft, die einer der oben genannten Ressource zugeordneten `@type` Werte.</span><span class="sxs-lookup"><span data-stu-id="d9b88-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="d9b88-118">Basis-URL im folgenden Dokument der Platzhalter `{@id}` verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="d9b88-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d9b88-119">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="d9b88-119">HTTP Methods</span></span>

<span data-ttu-id="d9b88-120">Alle URLs finden Sie in die Registrierung Unterstützung der HTTP-Methoden `GET` und `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="d9b88-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="d9b88-121">Suchen Sie nach der Paket-IDs</span><span class="sxs-lookup"><span data-stu-id="d9b88-121">Search for package IDs</span></span>

<span data-ttu-id="d9b88-122">Die erste API für AutoVervollständigen unterstützt das Suchen nach Teil einer Paket-ID-Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="d9b88-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="d9b88-123">Dies ist nützlich, wenn Sie ein Paket Typeahead-Feature in einer Benutzeroberfläche, die in einem NuGet-Paketquelle integriert bereitstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="d9b88-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="d9b88-124">Ein Paket mit nur nicht aufgeführte Versionen wird nicht in den Ergebnissen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d9b88-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="d9b88-125">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="d9b88-125">Request parameters</span></span>

<span data-ttu-id="d9b88-126">name</span><span class="sxs-lookup"><span data-stu-id="d9b88-126">Name</span></span>        | <span data-ttu-id="d9b88-127">In</span><span class="sxs-lookup"><span data-stu-id="d9b88-127">In</span></span>     | <span data-ttu-id="d9b88-128">Typ</span><span class="sxs-lookup"><span data-stu-id="d9b88-128">Type</span></span>    | <span data-ttu-id="d9b88-129">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="d9b88-129">Required</span></span> | <span data-ttu-id="d9b88-130">Hinweise</span><span class="sxs-lookup"><span data-stu-id="d9b88-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="d9b88-131">q</span><span class="sxs-lookup"><span data-stu-id="d9b88-131">q</span></span>           | <span data-ttu-id="d9b88-132">URL</span><span class="sxs-lookup"><span data-stu-id="d9b88-132">URL</span></span>    | <span data-ttu-id="d9b88-133">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="d9b88-133">string</span></span>  | <span data-ttu-id="d9b88-134">Nein</span><span class="sxs-lookup"><span data-stu-id="d9b88-134">no</span></span>       | <span data-ttu-id="d9b88-135">Die Zeichenfolge, die mit der Paket-IDs verglichen werden soll</span><span class="sxs-lookup"><span data-stu-id="d9b88-135">The string to compare against package IDs</span></span>
<span data-ttu-id="d9b88-136">überspringen</span><span class="sxs-lookup"><span data-stu-id="d9b88-136">skip</span></span>        | <span data-ttu-id="d9b88-137">URL</span><span class="sxs-lookup"><span data-stu-id="d9b88-137">URL</span></span>    | <span data-ttu-id="d9b88-138">Ganze Zahl</span><span class="sxs-lookup"><span data-stu-id="d9b88-138">integer</span></span> | <span data-ttu-id="d9b88-139">Nein</span><span class="sxs-lookup"><span data-stu-id="d9b88-139">no</span></span>       | <span data-ttu-id="d9b88-140">Die Anzahl von Ergebnissen für die Paginierung überspringen</span><span class="sxs-lookup"><span data-stu-id="d9b88-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="d9b88-141">Take</span><span class="sxs-lookup"><span data-stu-id="d9b88-141">take</span></span>        | <span data-ttu-id="d9b88-142">URL</span><span class="sxs-lookup"><span data-stu-id="d9b88-142">URL</span></span>    | <span data-ttu-id="d9b88-143">Ganze Zahl</span><span class="sxs-lookup"><span data-stu-id="d9b88-143">integer</span></span> | <span data-ttu-id="d9b88-144">Nein</span><span class="sxs-lookup"><span data-stu-id="d9b88-144">no</span></span>       | <span data-ttu-id="d9b88-145">Die Anzahl der zurückzugebenden Ergebnisse, für die Paginierung</span><span class="sxs-lookup"><span data-stu-id="d9b88-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="d9b88-146">Vorabversion</span><span class="sxs-lookup"><span data-stu-id="d9b88-146">prerelease</span></span>  | <span data-ttu-id="d9b88-147">URL</span><span class="sxs-lookup"><span data-stu-id="d9b88-147">URL</span></span>    | <span data-ttu-id="d9b88-148">boolean</span><span class="sxs-lookup"><span data-stu-id="d9b88-148">boolean</span></span> | <span data-ttu-id="d9b88-149">Nein</span><span class="sxs-lookup"><span data-stu-id="d9b88-149">no</span></span>       | `true` <span data-ttu-id="d9b88-150">oder `false` bestimmen, ob enthalten [Vorabversionen von Paketen](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d9b88-150">or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="d9b88-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="d9b88-151">semVerLevel</span></span> | <span data-ttu-id="d9b88-152">URL</span><span class="sxs-lookup"><span data-stu-id="d9b88-152">URL</span></span>    | <span data-ttu-id="d9b88-153">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="d9b88-153">string</span></span>  | <span data-ttu-id="d9b88-154">Nein</span><span class="sxs-lookup"><span data-stu-id="d9b88-154">no</span></span>       | <span data-ttu-id="d9b88-155">Eine Versionszeichenfolge SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="d9b88-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="d9b88-156">Die AutoVervollständigen-Abfrage `q` wird analysiert, in einer Weise, die von der serverimplementierung definiert ist.</span><span class="sxs-lookup"><span data-stu-id="d9b88-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="d9b88-157">NuGet.org unterstützt das Abfragen für das Präfix der Paket-ID-Token, die Teile der Teilung von erzeugten-ID des ursprünglichen Camel Case "und" Symbol Zeichen.</span><span class="sxs-lookup"><span data-stu-id="d9b88-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="d9b88-158">Die `skip` Parameter hat den Standardwert 0.</span><span class="sxs-lookup"><span data-stu-id="d9b88-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="d9b88-159">Die `take` Parameter muss eine ganze Zahl größer als 0 (null) sein.</span><span class="sxs-lookup"><span data-stu-id="d9b88-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="d9b88-160">Die Server-Implementierung kann es sich um einen maximalen Wert verursachen.</span><span class="sxs-lookup"><span data-stu-id="d9b88-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="d9b88-161">Wenn `prerelease` ist nicht angegeben wird, Vorabversionen von Paketen ausgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="d9b88-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="d9b88-162">Die `semVerLevel` Query-Parameter wird verwendet, um abonnieren [SemVer 2.0.0 Pakete](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="d9b88-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="d9b88-163">Wenn dieser Parameter ausgeschlossen wird, wird nur Paket-IDs mit SemVer 1.0.0 kompatible Versionen zurückgegeben werden (mit der [standard NuGet-Versionsschema](../reference/package-versioning.md) Einschränkungen, z. B. Versionszeichenfolgen mit 4 Einheiten für ganze Zahl).</span><span class="sxs-lookup"><span data-stu-id="d9b88-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="d9b88-164">Wenn `semVerLevel=2.0.0` bereitgestellt wird, werden sowohl SemVer 1.0.0 und kompatiblen Paketen SemVer 2.0.0 zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="d9b88-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="d9b88-165">Finden Sie unter den [SemVer 2.0.0-Unterstützung für "NuGet.org"](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) für Weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="d9b88-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="d9b88-166">Antwort</span><span class="sxs-lookup"><span data-stu-id="d9b88-166">Response</span></span>

<span data-ttu-id="d9b88-167">Die Antwort ist die JSON-Dokument mit bis zu `take` Autocomplete-Ergebnisse.</span><span class="sxs-lookup"><span data-stu-id="d9b88-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="d9b88-168">Die JSON-Stammobjekt hat die folgenden Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="d9b88-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="d9b88-169">Name</span><span class="sxs-lookup"><span data-stu-id="d9b88-169">Name</span></span>      | <span data-ttu-id="d9b88-170">Typ</span><span class="sxs-lookup"><span data-stu-id="d9b88-170">Type</span></span>             | <span data-ttu-id="d9b88-171">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="d9b88-171">Required</span></span> | <span data-ttu-id="d9b88-172">Hinweise</span><span class="sxs-lookup"><span data-stu-id="d9b88-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="d9b88-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="d9b88-173">totalHits</span></span> | <span data-ttu-id="d9b88-174">Ganze Zahl</span><span class="sxs-lookup"><span data-stu-id="d9b88-174">integer</span></span>          | <span data-ttu-id="d9b88-175">ja</span><span class="sxs-lookup"><span data-stu-id="d9b88-175">yes</span></span>      | <span data-ttu-id="d9b88-176">Die Gesamtzahl der Übereinstimmungen ohne Berücksichtigung der `skip` und</span><span class="sxs-lookup"><span data-stu-id="d9b88-176">The total number of matches, disregarding `skip` and</span></span> `take`
<span data-ttu-id="d9b88-177">Daten</span><span class="sxs-lookup"><span data-stu-id="d9b88-177">data</span></span>      | <span data-ttu-id="d9b88-178">Array von Zeichenfolgen</span><span class="sxs-lookup"><span data-stu-id="d9b88-178">array of strings</span></span> | <span data-ttu-id="d9b88-179">ja</span><span class="sxs-lookup"><span data-stu-id="d9b88-179">yes</span></span>      | <span data-ttu-id="d9b88-180">Die Paket-IDs, die von der Anforderung übereinstimmen</span><span class="sxs-lookup"><span data-stu-id="d9b88-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="d9b88-181">Beispiel für eine Anforderung</span><span class="sxs-lookup"><span data-stu-id="d9b88-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="d9b88-182">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="d9b88-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="d9b88-183">Auflisten von Paketversionen</span><span class="sxs-lookup"><span data-stu-id="d9b88-183">Enumerate package versions</span></span>

<span data-ttu-id="d9b88-184">Eine Paket-ID mit der vorherigen-API ermittelt wurde, können ein Client die AutoVervollständigen-API Sie Auflisten von Paketversionen für ein bereitgestelltes Paket-ID</span><span class="sxs-lookup"><span data-stu-id="d9b88-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="d9b88-185">Eine Version des Pakets, die nicht aufgeführt ist, wird nicht in den Ergebnissen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d9b88-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="d9b88-186">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="d9b88-186">Request parameters</span></span>

<span data-ttu-id="d9b88-187">name</span><span class="sxs-lookup"><span data-stu-id="d9b88-187">Name</span></span>        | <span data-ttu-id="d9b88-188">In</span><span class="sxs-lookup"><span data-stu-id="d9b88-188">In</span></span>     | <span data-ttu-id="d9b88-189">Typ</span><span class="sxs-lookup"><span data-stu-id="d9b88-189">Type</span></span>    | <span data-ttu-id="d9b88-190">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="d9b88-190">Required</span></span> | <span data-ttu-id="d9b88-191">Hinweise</span><span class="sxs-lookup"><span data-stu-id="d9b88-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="d9b88-192">id</span><span class="sxs-lookup"><span data-stu-id="d9b88-192">id</span></span>          | <span data-ttu-id="d9b88-193">URL</span><span class="sxs-lookup"><span data-stu-id="d9b88-193">URL</span></span>    | <span data-ttu-id="d9b88-194">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="d9b88-194">string</span></span>  | <span data-ttu-id="d9b88-195">ja</span><span class="sxs-lookup"><span data-stu-id="d9b88-195">yes</span></span>      | <span data-ttu-id="d9b88-196">Die Paket-ID zum Abrufen von Versionen</span><span class="sxs-lookup"><span data-stu-id="d9b88-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="d9b88-197">Vorabversion</span><span class="sxs-lookup"><span data-stu-id="d9b88-197">prerelease</span></span>  | <span data-ttu-id="d9b88-198">URL</span><span class="sxs-lookup"><span data-stu-id="d9b88-198">URL</span></span>    | <span data-ttu-id="d9b88-199">boolean</span><span class="sxs-lookup"><span data-stu-id="d9b88-199">boolean</span></span> | <span data-ttu-id="d9b88-200">Nein</span><span class="sxs-lookup"><span data-stu-id="d9b88-200">no</span></span>       | `true` <span data-ttu-id="d9b88-201">oder `false` bestimmen, ob enthalten [Vorabversionen von Paketen](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d9b88-201">or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="d9b88-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="d9b88-202">semVerLevel</span></span> | <span data-ttu-id="d9b88-203">URL</span><span class="sxs-lookup"><span data-stu-id="d9b88-203">URL</span></span>    | <span data-ttu-id="d9b88-204">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="d9b88-204">string</span></span>  | <span data-ttu-id="d9b88-205">Nein</span><span class="sxs-lookup"><span data-stu-id="d9b88-205">no</span></span>       | <span data-ttu-id="d9b88-206">Eine Zeichenfolge der SemVer 2.0.0-version</span><span class="sxs-lookup"><span data-stu-id="d9b88-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="d9b88-207">Wenn `prerelease` ist nicht angegeben wird, Vorabversionen von Paketen ausgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="d9b88-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="d9b88-208">Die `semVerLevel` Query-Parameter wird verwendet, um SemVer 2.0.0-Paketen teilnehmen.</span><span class="sxs-lookup"><span data-stu-id="d9b88-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="d9b88-209">Wenn dieser Parameter ausgeschlossen wird, werden nur SemVer 1.0.0-Versionen zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="d9b88-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="d9b88-210">Wenn `semVerLevel=2.0.0` bereitgestellt wird, werden sowohl die SemVer 1.0.0 als auch die SemVer 2.0.0-Version zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="d9b88-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="d9b88-211">Finden Sie unter den [SemVer 2.0.0-Unterstützung für "NuGet.org"](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) für Weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="d9b88-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="d9b88-212">Antwort</span><span class="sxs-lookup"><span data-stu-id="d9b88-212">Response</span></span>

<span data-ttu-id="d9b88-213">Die Antwort ist die JSON-Dokument mit der alle Paketversionen von den angegebenen Paket-ID filtern nach den angegebenen Abfrageparametern.</span><span class="sxs-lookup"><span data-stu-id="d9b88-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="d9b88-214">Die JSON-Stammobjekt hat die folgende Eigenschaft:</span><span class="sxs-lookup"><span data-stu-id="d9b88-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="d9b88-215">Name</span><span class="sxs-lookup"><span data-stu-id="d9b88-215">Name</span></span>      | <span data-ttu-id="d9b88-216">Typ</span><span class="sxs-lookup"><span data-stu-id="d9b88-216">Type</span></span>             | <span data-ttu-id="d9b88-217">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="d9b88-217">Required</span></span> | <span data-ttu-id="d9b88-218">Hinweise</span><span class="sxs-lookup"><span data-stu-id="d9b88-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="d9b88-219">Daten</span><span class="sxs-lookup"><span data-stu-id="d9b88-219">data</span></span>      | <span data-ttu-id="d9b88-220">Array von Zeichenfolgen</span><span class="sxs-lookup"><span data-stu-id="d9b88-220">array of strings</span></span> | <span data-ttu-id="d9b88-221">ja</span><span class="sxs-lookup"><span data-stu-id="d9b88-221">yes</span></span>      | <span data-ttu-id="d9b88-222">Die Paketversionen, die von der Anforderung übereinstimmen</span><span class="sxs-lookup"><span data-stu-id="d9b88-222">The package versions matched by the request</span></span>

<span data-ttu-id="d9b88-223">Die Versionen des Pakets in der `data` Array SemVer 2.0.0-Build-Metadaten enthalten (z. B. `1.0.0+metadata`) Wenn die `semVerLevel=2.0.0` wird in der Abfragezeichenfolge bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="d9b88-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d9b88-224">Beispiel für eine Anforderung</span><span class="sxs-lookup"><span data-stu-id="d9b88-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="d9b88-225">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="d9b88-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
