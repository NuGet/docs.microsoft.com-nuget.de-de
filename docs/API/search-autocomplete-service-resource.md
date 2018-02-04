---
title: "AutoVervollständigen-Funktion, die NuGet-API | Microsoft Docs"
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
description: "Die AutoVervollständigen-Suchdienst unterstützt interaktive Ermittlung von Paket-IDs und Versionen."
keywords: "Suchen NuGet AutoVervollständigen-API, die NuGet-Paket-ID, Substring-Paket-ID"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7c984ca61799293d7832851b80cf3fefc4734288
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="autocomplete"></a><span data-ttu-id="5ce01-104">AutoVervollständigen</span><span class="sxs-lookup"><span data-stu-id="5ce01-104">Autocomplete</span></span>

<span data-ttu-id="5ce01-105">Es ist möglich, eine Paket-ID und Version AutoVervollständigen Erfahrung mit der V3-API zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="5ce01-105">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="5ce01-106">Die Ressource, die zum treffen von AutoVervollständigen Abfragen verwendet wird die `SearchAutocompleteService` Ressource gefunden, der [Dienst Index](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="5ce01-106">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="5ce01-107">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="5ce01-107">Versioning</span></span>

<span data-ttu-id="5ce01-108">Die folgenden `@type` Werte werden verwendet:</span><span class="sxs-lookup"><span data-stu-id="5ce01-108">The following `@type` values are used:</span></span>

<span data-ttu-id="5ce01-109">@type-Wert</span><span class="sxs-lookup"><span data-stu-id="5ce01-109">@type value</span></span>                          | <span data-ttu-id="5ce01-110">Hinweise</span><span class="sxs-lookup"><span data-stu-id="5ce01-110">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="5ce01-111">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="5ce01-111">SearchAutocompleteService</span></span>            | <span data-ttu-id="5ce01-112">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="5ce01-112">The initial release</span></span>
<span data-ttu-id="5ce01-113">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="5ce01-113">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="5ce01-114">Alias der`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="5ce01-114">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="5ce01-115">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="5ce01-115">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="5ce01-116">Alias der`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="5ce01-116">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="5ce01-117">Basis-URL</span><span class="sxs-lookup"><span data-stu-id="5ce01-117">Base URL</span></span>

<span data-ttu-id="5ce01-118">Die base-URL für die folgenden APIs ist der Wert der `@id` mit einem der oben genannten Ressource verknüpfte Eigenschaft `@type` Werte.</span><span class="sxs-lookup"><span data-stu-id="5ce01-118">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="5ce01-119">Im folgenden Dokument Platzhalter für die Basis-URL `{@id}` verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="5ce01-119">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="5ce01-120">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="5ce01-120">HTTP Methods</span></span>

<span data-ttu-id="5ce01-121">Alle URLs, die bei der Unterstützung der Registrierung-Ressource gefunden, die HTTP-Methoden `GET` und `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="5ce01-121">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="5ce01-122">Suchen Sie nach der Paket-IDs</span><span class="sxs-lookup"><span data-stu-id="5ce01-122">Search for package IDs</span></span>

<span data-ttu-id="5ce01-123">Das erste AutoVervollständigen-API unterstützt die Teil einer Paket-ID-Zeichenfolge gesucht.</span><span class="sxs-lookup"><span data-stu-id="5ce01-123">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="5ce01-124">Dies ist nützlich, wenn Sie eine Paket Typeahead-Funktion in einer Benutzeroberfläche mit einem NuGet-Paket integriert bereitstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="5ce01-124">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="5ce01-125">Ein Paket mit nur nicht aufgeführte Versionen werden nicht in den Ergebnissen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="5ce01-125">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="5ce01-126">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="5ce01-126">Request parameters</span></span>

<span data-ttu-id="5ce01-127">name</span><span class="sxs-lookup"><span data-stu-id="5ce01-127">Name</span></span>        | <span data-ttu-id="5ce01-128">In</span><span class="sxs-lookup"><span data-stu-id="5ce01-128">In</span></span>     | <span data-ttu-id="5ce01-129">Typ</span><span class="sxs-lookup"><span data-stu-id="5ce01-129">Type</span></span>    | <span data-ttu-id="5ce01-130">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="5ce01-130">Required</span></span> | <span data-ttu-id="5ce01-131">Hinweise</span><span class="sxs-lookup"><span data-stu-id="5ce01-131">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="5ce01-132">q</span><span class="sxs-lookup"><span data-stu-id="5ce01-132">q</span></span>           | <span data-ttu-id="5ce01-133">URL</span><span class="sxs-lookup"><span data-stu-id="5ce01-133">URL</span></span>    | <span data-ttu-id="5ce01-134">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="5ce01-134">string</span></span>  | <span data-ttu-id="5ce01-135">Nein</span><span class="sxs-lookup"><span data-stu-id="5ce01-135">no</span></span>       | <span data-ttu-id="5ce01-136">Die Zeichenfolge zum Vergleich von Paket-IDs</span><span class="sxs-lookup"><span data-stu-id="5ce01-136">The string to compare against package IDs</span></span>
<span data-ttu-id="5ce01-137">überspringen</span><span class="sxs-lookup"><span data-stu-id="5ce01-137">skip</span></span>        | <span data-ttu-id="5ce01-138">URL</span><span class="sxs-lookup"><span data-stu-id="5ce01-138">URL</span></span>    | <span data-ttu-id="5ce01-139">Ganze Zahl</span><span class="sxs-lookup"><span data-stu-id="5ce01-139">integer</span></span> | <span data-ttu-id="5ce01-140">Nein</span><span class="sxs-lookup"><span data-stu-id="5ce01-140">no</span></span>       | <span data-ttu-id="5ce01-141">Die Anzahl der Ergebnisse für die Paginierung überspringen</span><span class="sxs-lookup"><span data-stu-id="5ce01-141">The number of results to skip, for pagination</span></span>
<span data-ttu-id="5ce01-142">Take</span><span class="sxs-lookup"><span data-stu-id="5ce01-142">take</span></span>        | <span data-ttu-id="5ce01-143">URL</span><span class="sxs-lookup"><span data-stu-id="5ce01-143">URL</span></span>    | <span data-ttu-id="5ce01-144">Ganze Zahl</span><span class="sxs-lookup"><span data-stu-id="5ce01-144">integer</span></span> | <span data-ttu-id="5ce01-145">Nein</span><span class="sxs-lookup"><span data-stu-id="5ce01-145">no</span></span>       | <span data-ttu-id="5ce01-146">Die Anzahl der zurückzugebenden Ergebnisseite, für die Paginierung</span><span class="sxs-lookup"><span data-stu-id="5ce01-146">The number of results to return, for pagination</span></span>
<span data-ttu-id="5ce01-147">Vorabversion</span><span class="sxs-lookup"><span data-stu-id="5ce01-147">prerelease</span></span>  | <span data-ttu-id="5ce01-148">URL</span><span class="sxs-lookup"><span data-stu-id="5ce01-148">URL</span></span>    | <span data-ttu-id="5ce01-149">boolean</span><span class="sxs-lookup"><span data-stu-id="5ce01-149">boolean</span></span> | <span data-ttu-id="5ce01-150">Nein</span><span class="sxs-lookup"><span data-stu-id="5ce01-150">no</span></span>       | <span data-ttu-id="5ce01-151">`true`oder `false` bestimmen, ob enthalten [Vorabversion Pakete](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="5ce01-151">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="5ce01-152">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="5ce01-152">semVerLevel</span></span> | <span data-ttu-id="5ce01-153">URL</span><span class="sxs-lookup"><span data-stu-id="5ce01-153">URL</span></span>    | <span data-ttu-id="5ce01-154">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="5ce01-154">string</span></span>  | <span data-ttu-id="5ce01-155">Nein</span><span class="sxs-lookup"><span data-stu-id="5ce01-155">no</span></span>       | <span data-ttu-id="5ce01-156">A SemVer 1.0.0 version string</span><span class="sxs-lookup"><span data-stu-id="5ce01-156">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="5ce01-157">Die AutoVervollständigen-Abfrage `q` wird analysiert, die in einer Weise, die durch die Implementierung definiert ist.</span><span class="sxs-lookup"><span data-stu-id="5ce01-157">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="5ce01-158">NuGet.org unterstützt das Abfragen für das Präfix des Paket-ID-Token, die Teile der von Spliting erzeugte ID werden der ursprünglichen Kamel Groß-/Kleinschreibung und das Symbol für Zeichen.</span><span class="sxs-lookup"><span data-stu-id="5ce01-158">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="5ce01-159">Die `skip` Parameter beträgt standardmäßig 0.</span><span class="sxs-lookup"><span data-stu-id="5ce01-159">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="5ce01-160">Die `take` Parameter muss eine ganze Zahl größer als 0 (null) sein.</span><span class="sxs-lookup"><span data-stu-id="5ce01-160">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="5ce01-161">Die Implementierung der Server kann einen maximalen Wert verursachen.</span><span class="sxs-lookup"><span data-stu-id="5ce01-161">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="5ce01-162">Wenn `prerelease` nicht angegeben wird, Vorabversion Paketen ausgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="5ce01-162">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="5ce01-163">Die `semVerLevel` Query-Parameter wird verwendet, um abonnieren [SemVer 2.0.0 Pakete](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="5ce01-163">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="5ce01-164">Wenn dieser Parameter ausgeschlossen ist, werden nur Paket-IDs mit SemVer 1.0.0 kompatible Versionen zurückgegeben (mit der [standard NuGet Versioning](../reference/package-versioning.md) Vorsichtsmaßnahmen, z. B. Versionszeichenfolgen mit 4 Einheiten für ganze Zahl).</span><span class="sxs-lookup"><span data-stu-id="5ce01-164">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="5ce01-165">Wenn `semVerLevel=2.0.0` angegeben wird, SemVer 1.0.0 und SemVer 2.0.0 kompatibel Pakete zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="5ce01-165">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="5ce01-166">Finden Sie unter der [SemVer 2.0.0-Unterstützung für nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) für Weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="5ce01-166">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="5ce01-167">Antwort</span><span class="sxs-lookup"><span data-stu-id="5ce01-167">Response</span></span>

<span data-ttu-id="5ce01-168">Die Antwort ist, enthält bis zu JSON-Dokument `take` AutoVervollständigen Ergebnisse.</span><span class="sxs-lookup"><span data-stu-id="5ce01-168">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="5ce01-169">Der Stamm-JSON-Objekt hat die folgenden Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="5ce01-169">The root JSON object has the following properties:</span></span>

<span data-ttu-id="5ce01-170">name</span><span class="sxs-lookup"><span data-stu-id="5ce01-170">Name</span></span>      | <span data-ttu-id="5ce01-171">Typ</span><span class="sxs-lookup"><span data-stu-id="5ce01-171">Type</span></span>             | <span data-ttu-id="5ce01-172">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="5ce01-172">Required</span></span> | <span data-ttu-id="5ce01-173">Hinweise</span><span class="sxs-lookup"><span data-stu-id="5ce01-173">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="5ce01-174">totalHits</span><span class="sxs-lookup"><span data-stu-id="5ce01-174">totalHits</span></span> | <span data-ttu-id="5ce01-175">Ganze Zahl</span><span class="sxs-lookup"><span data-stu-id="5ce01-175">integer</span></span>          | <span data-ttu-id="5ce01-176">ja</span><span class="sxs-lookup"><span data-stu-id="5ce01-176">yes</span></span>      | <span data-ttu-id="5ce01-177">Die Gesamtzahl der Übereinstimmungen, Basiseigenschaft `skip` und`take`</span><span class="sxs-lookup"><span data-stu-id="5ce01-177">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="5ce01-178">Daten</span><span class="sxs-lookup"><span data-stu-id="5ce01-178">data</span></span>      | <span data-ttu-id="5ce01-179">Array von Zeichenfolgen</span><span class="sxs-lookup"><span data-stu-id="5ce01-179">array of strings</span></span> | <span data-ttu-id="5ce01-180">ja</span><span class="sxs-lookup"><span data-stu-id="5ce01-180">yes</span></span>      | <span data-ttu-id="5ce01-181">Die Paket-IDs übereinstimmen, die von der Anforderung</span><span class="sxs-lookup"><span data-stu-id="5ce01-181">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="5ce01-182">Beispielanforderung</span><span class="sxs-lookup"><span data-stu-id="5ce01-182">Sample request</span></span>

<span data-ttu-id="5ce01-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="5ce01-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="5ce01-184">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="5ce01-184">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="5ce01-185">Auflisten von Paketversionen</span><span class="sxs-lookup"><span data-stu-id="5ce01-185">Enumerate package versions</span></span>

<span data-ttu-id="5ce01-186">Eine Paket-ID mithilfe der vorherigen-API ermittelt wurde, können ein Client die AutoVervollständigen-API Sie Paketversionen für eine angegebene Paket-ID aufgelistet werden.</span><span class="sxs-lookup"><span data-stu-id="5ce01-186">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="5ce01-187">Eine Paketversion, die nicht aufgeführte ist, werden nicht in den Ergebnissen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="5ce01-187">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="5ce01-188">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="5ce01-188">Request parameters</span></span>

<span data-ttu-id="5ce01-189">name</span><span class="sxs-lookup"><span data-stu-id="5ce01-189">Name</span></span>        | <span data-ttu-id="5ce01-190">In</span><span class="sxs-lookup"><span data-stu-id="5ce01-190">In</span></span>     | <span data-ttu-id="5ce01-191">Typ</span><span class="sxs-lookup"><span data-stu-id="5ce01-191">Type</span></span>    | <span data-ttu-id="5ce01-192">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="5ce01-192">Required</span></span> | <span data-ttu-id="5ce01-193">Hinweise</span><span class="sxs-lookup"><span data-stu-id="5ce01-193">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="5ce01-194">ID</span><span class="sxs-lookup"><span data-stu-id="5ce01-194">id</span></span>          | <span data-ttu-id="5ce01-195">URL</span><span class="sxs-lookup"><span data-stu-id="5ce01-195">URL</span></span>    | <span data-ttu-id="5ce01-196">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="5ce01-196">string</span></span>  | <span data-ttu-id="5ce01-197">ja</span><span class="sxs-lookup"><span data-stu-id="5ce01-197">yes</span></span>      | <span data-ttu-id="5ce01-198">Die Paket-ID für Versionen abgerufen</span><span class="sxs-lookup"><span data-stu-id="5ce01-198">The package ID to fetch versions for</span></span>
<span data-ttu-id="5ce01-199">Vorabversion</span><span class="sxs-lookup"><span data-stu-id="5ce01-199">prerelease</span></span>  | <span data-ttu-id="5ce01-200">URL</span><span class="sxs-lookup"><span data-stu-id="5ce01-200">URL</span></span>    | <span data-ttu-id="5ce01-201">boolean</span><span class="sxs-lookup"><span data-stu-id="5ce01-201">boolean</span></span> | <span data-ttu-id="5ce01-202">Nein</span><span class="sxs-lookup"><span data-stu-id="5ce01-202">no</span></span>       | <span data-ttu-id="5ce01-203">`true`oder `false` bestimmen, ob enthalten [Vorabversion Pakete](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="5ce01-203">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="5ce01-204">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="5ce01-204">semVerLevel</span></span> | <span data-ttu-id="5ce01-205">URL</span><span class="sxs-lookup"><span data-stu-id="5ce01-205">URL</span></span>    | <span data-ttu-id="5ce01-206">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="5ce01-206">string</span></span>  | <span data-ttu-id="5ce01-207">Nein</span><span class="sxs-lookup"><span data-stu-id="5ce01-207">no</span></span>       | <span data-ttu-id="5ce01-208">Eine Versionszeichenfolge SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="5ce01-208">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="5ce01-209">Wenn `prerelease` nicht angegeben wird, Vorabversion Paketen ausgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="5ce01-209">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="5ce01-210">Die `semVerLevel` Query-Parameter wird verwendet, um Pakete von SemVer 2.0.0 teilnehmen.</span><span class="sxs-lookup"><span data-stu-id="5ce01-210">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="5ce01-211">Wenn dieser Parameter ausgeschlossen ist, werden nur SemVer 1.0.0 Versionen zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="5ce01-211">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="5ce01-212">Wenn `semVerLevel=2.0.0` angegeben wird, SemVer 1.0.0 und SemVer 2.0.0-Versionen zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="5ce01-212">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="5ce01-213">Finden Sie unter der [SemVer 2.0.0-Unterstützung für nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) für Weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="5ce01-213">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="5ce01-214">Antwort</span><span class="sxs-lookup"><span data-stu-id="5ce01-214">Response</span></span>

<span data-ttu-id="5ce01-215">Die Antwort ist JSON-Dokument, das alle Paketversionen der bereitgestellte Paket-ID, die das Filtern nach der angegebenen Abfrageparameter enthält.</span><span class="sxs-lookup"><span data-stu-id="5ce01-215">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="5ce01-216">Der Stamm-JSON-Objekt hat die folgende Eigenschaft:</span><span class="sxs-lookup"><span data-stu-id="5ce01-216">The root JSON object has the following property:</span></span>

<span data-ttu-id="5ce01-217">name</span><span class="sxs-lookup"><span data-stu-id="5ce01-217">Name</span></span>      | <span data-ttu-id="5ce01-218">Typ</span><span class="sxs-lookup"><span data-stu-id="5ce01-218">Type</span></span>             | <span data-ttu-id="5ce01-219">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="5ce01-219">Required</span></span> | <span data-ttu-id="5ce01-220">Hinweise</span><span class="sxs-lookup"><span data-stu-id="5ce01-220">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="5ce01-221">Daten</span><span class="sxs-lookup"><span data-stu-id="5ce01-221">data</span></span>      | <span data-ttu-id="5ce01-222">Array von Zeichenfolgen</span><span class="sxs-lookup"><span data-stu-id="5ce01-222">array of strings</span></span> | <span data-ttu-id="5ce01-223">ja</span><span class="sxs-lookup"><span data-stu-id="5ce01-223">yes</span></span>      | <span data-ttu-id="5ce01-224">Die Zeichenfolge, die für der Anforderungs Paketversionen</span><span class="sxs-lookup"><span data-stu-id="5ce01-224">The package versions matched by the request</span></span>

<span data-ttu-id="5ce01-225">Die Paketversionen in der `data` Array konnte SemVer 2.0.0 Build Metadaten enthalten (z. B. `1.0.0+metadata`) Wenn die `semVerLevel=2.0.0` wurde in der Abfragezeichenfolge angegeben.</span><span class="sxs-lookup"><span data-stu-id="5ce01-225">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="5ce01-226">Beispielanforderung</span><span class="sxs-lookup"><span data-stu-id="5ce01-226">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="5ce01-227">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="5ce01-227">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
