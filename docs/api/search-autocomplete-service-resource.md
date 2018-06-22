---
title: AutoVervollständigen NuGet-API
description: Die AutoVervollständigen-Suchdienst unterstützt interaktive Ermittlung von Paket-IDs und Versionen.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d5e1936c6c5406a1a376c16b2bad5351320dfb4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822135"
---
# <a name="autocomplete"></a><span data-ttu-id="ba15f-103">AutoVervollständigen</span><span class="sxs-lookup"><span data-stu-id="ba15f-103">Autocomplete</span></span>

<span data-ttu-id="ba15f-104">Es ist möglich, eine Paket-ID und Version AutoVervollständigen Erfahrung mit der V3-API zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="ba15f-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="ba15f-105">Die Ressource, die zum treffen von AutoVervollständigen Abfragen verwendet wird die `SearchAutocompleteService` Ressource gefunden, der [Dienst Index](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="ba15f-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="ba15f-106">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="ba15f-106">Versioning</span></span>

<span data-ttu-id="ba15f-107">Die folgenden `@type` Werte werden verwendet:</span><span class="sxs-lookup"><span data-stu-id="ba15f-107">The following `@type` values are used:</span></span>

<span data-ttu-id="ba15f-108">@type-Wert</span><span class="sxs-lookup"><span data-stu-id="ba15f-108">@type value</span></span>                          | <span data-ttu-id="ba15f-109">Hinweise</span><span class="sxs-lookup"><span data-stu-id="ba15f-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="ba15f-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="ba15f-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="ba15f-111">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="ba15f-111">The initial release</span></span>
<span data-ttu-id="ba15f-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="ba15f-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="ba15f-113">Alias der `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="ba15f-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="ba15f-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="ba15f-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="ba15f-115">Alias der `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="ba15f-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="ba15f-116">Basis-URL</span><span class="sxs-lookup"><span data-stu-id="ba15f-116">Base URL</span></span>

<span data-ttu-id="ba15f-117">Die base-URL für die folgenden APIs ist der Wert der `@id` mit einem der oben genannten Ressource verknüpfte Eigenschaft `@type` Werte.</span><span class="sxs-lookup"><span data-stu-id="ba15f-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="ba15f-118">Im folgenden Dokument Platzhalter für die Basis-URL `{@id}` verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="ba15f-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="ba15f-119">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="ba15f-119">HTTP Methods</span></span>

<span data-ttu-id="ba15f-120">Alle URLs, die bei der Unterstützung der Registrierung-Ressource gefunden, die HTTP-Methoden `GET` und `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="ba15f-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="ba15f-121">Suchen Sie nach der Paket-IDs</span><span class="sxs-lookup"><span data-stu-id="ba15f-121">Search for package IDs</span></span>

<span data-ttu-id="ba15f-122">Das erste AutoVervollständigen-API unterstützt die Teil einer Paket-ID-Zeichenfolge gesucht.</span><span class="sxs-lookup"><span data-stu-id="ba15f-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="ba15f-123">Dies ist nützlich, wenn Sie eine Paket Typeahead-Funktion in einer Benutzeroberfläche mit einem NuGet-Paket integriert bereitstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="ba15f-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="ba15f-124">Ein Paket mit nur nicht aufgeführte Versionen werden nicht in den Ergebnissen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="ba15f-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="ba15f-125">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="ba15f-125">Request parameters</span></span>

<span data-ttu-id="ba15f-126">name</span><span class="sxs-lookup"><span data-stu-id="ba15f-126">Name</span></span>        | <span data-ttu-id="ba15f-127">In</span><span class="sxs-lookup"><span data-stu-id="ba15f-127">In</span></span>     | <span data-ttu-id="ba15f-128">Typ</span><span class="sxs-lookup"><span data-stu-id="ba15f-128">Type</span></span>    | <span data-ttu-id="ba15f-129">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="ba15f-129">Required</span></span> | <span data-ttu-id="ba15f-130">Hinweise</span><span class="sxs-lookup"><span data-stu-id="ba15f-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="ba15f-131">q</span><span class="sxs-lookup"><span data-stu-id="ba15f-131">q</span></span>           | <span data-ttu-id="ba15f-132">URL</span><span class="sxs-lookup"><span data-stu-id="ba15f-132">URL</span></span>    | <span data-ttu-id="ba15f-133">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="ba15f-133">string</span></span>  | <span data-ttu-id="ba15f-134">Nein</span><span class="sxs-lookup"><span data-stu-id="ba15f-134">no</span></span>       | <span data-ttu-id="ba15f-135">Die Zeichenfolge zum Vergleich von Paket-IDs</span><span class="sxs-lookup"><span data-stu-id="ba15f-135">The string to compare against package IDs</span></span>
<span data-ttu-id="ba15f-136">überspringen</span><span class="sxs-lookup"><span data-stu-id="ba15f-136">skip</span></span>        | <span data-ttu-id="ba15f-137">URL</span><span class="sxs-lookup"><span data-stu-id="ba15f-137">URL</span></span>    | <span data-ttu-id="ba15f-138">Ganze Zahl</span><span class="sxs-lookup"><span data-stu-id="ba15f-138">integer</span></span> | <span data-ttu-id="ba15f-139">Nein</span><span class="sxs-lookup"><span data-stu-id="ba15f-139">no</span></span>       | <span data-ttu-id="ba15f-140">Die Anzahl der Ergebnisse für die Paginierung überspringen</span><span class="sxs-lookup"><span data-stu-id="ba15f-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="ba15f-141">Take</span><span class="sxs-lookup"><span data-stu-id="ba15f-141">take</span></span>        | <span data-ttu-id="ba15f-142">URL</span><span class="sxs-lookup"><span data-stu-id="ba15f-142">URL</span></span>    | <span data-ttu-id="ba15f-143">Ganze Zahl</span><span class="sxs-lookup"><span data-stu-id="ba15f-143">integer</span></span> | <span data-ttu-id="ba15f-144">Nein</span><span class="sxs-lookup"><span data-stu-id="ba15f-144">no</span></span>       | <span data-ttu-id="ba15f-145">Die Anzahl der zurückzugebenden Ergebnisseite, für die Paginierung</span><span class="sxs-lookup"><span data-stu-id="ba15f-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="ba15f-146">Vorabversion</span><span class="sxs-lookup"><span data-stu-id="ba15f-146">prerelease</span></span>  | <span data-ttu-id="ba15f-147">URL</span><span class="sxs-lookup"><span data-stu-id="ba15f-147">URL</span></span>    | <span data-ttu-id="ba15f-148">boolean</span><span class="sxs-lookup"><span data-stu-id="ba15f-148">boolean</span></span> | <span data-ttu-id="ba15f-149">Nein</span><span class="sxs-lookup"><span data-stu-id="ba15f-149">no</span></span>       | <span data-ttu-id="ba15f-150">`true` oder `false` bestimmen, ob enthalten [Vorabversion Pakete](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="ba15f-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="ba15f-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="ba15f-151">semVerLevel</span></span> | <span data-ttu-id="ba15f-152">URL</span><span class="sxs-lookup"><span data-stu-id="ba15f-152">URL</span></span>    | <span data-ttu-id="ba15f-153">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="ba15f-153">string</span></span>  | <span data-ttu-id="ba15f-154">Nein</span><span class="sxs-lookup"><span data-stu-id="ba15f-154">no</span></span>       | <span data-ttu-id="ba15f-155">Eine Versionszeichenfolge SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="ba15f-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="ba15f-156">Die AutoVervollständigen-Abfrage `q` wird analysiert, die in einer Weise, die durch die Implementierung definiert ist.</span><span class="sxs-lookup"><span data-stu-id="ba15f-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="ba15f-157">NuGet.org unterstützt das Abfragen für das Präfix des Paket-ID-Token, die Teile der von Spliting erzeugte ID werden der ursprünglichen Kamel Groß-/Kleinschreibung und das Symbol für Zeichen.</span><span class="sxs-lookup"><span data-stu-id="ba15f-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="ba15f-158">Die `skip` Parameter beträgt standardmäßig 0.</span><span class="sxs-lookup"><span data-stu-id="ba15f-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="ba15f-159">Die `take` Parameter muss eine ganze Zahl größer als 0 (null) sein.</span><span class="sxs-lookup"><span data-stu-id="ba15f-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="ba15f-160">Die Implementierung der Server kann einen maximalen Wert verursachen.</span><span class="sxs-lookup"><span data-stu-id="ba15f-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="ba15f-161">Wenn `prerelease` nicht angegeben wird, Vorabversion Paketen ausgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="ba15f-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="ba15f-162">Die `semVerLevel` Query-Parameter wird verwendet, um abonnieren [SemVer 2.0.0 Pakete](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="ba15f-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="ba15f-163">Wenn dieser Parameter ausgeschlossen ist, werden nur Paket-IDs mit SemVer 1.0.0 kompatible Versionen zurückgegeben (mit der [standard NuGet Versioning](../reference/package-versioning.md) Vorsichtsmaßnahmen, z. B. Versionszeichenfolgen mit 4 Einheiten für ganze Zahl).</span><span class="sxs-lookup"><span data-stu-id="ba15f-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="ba15f-164">Wenn `semVerLevel=2.0.0` angegeben wird, SemVer 1.0.0 und SemVer 2.0.0 kompatibel Pakete zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="ba15f-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="ba15f-165">Finden Sie unter der [SemVer 2.0.0-Unterstützung für nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) für Weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="ba15f-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="ba15f-166">Antwort</span><span class="sxs-lookup"><span data-stu-id="ba15f-166">Response</span></span>

<span data-ttu-id="ba15f-167">Die Antwort ist, enthält bis zu JSON-Dokument `take` AutoVervollständigen Ergebnisse.</span><span class="sxs-lookup"><span data-stu-id="ba15f-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="ba15f-168">Der Stamm-JSON-Objekt hat die folgenden Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="ba15f-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="ba15f-169">name</span><span class="sxs-lookup"><span data-stu-id="ba15f-169">Name</span></span>      | <span data-ttu-id="ba15f-170">Typ</span><span class="sxs-lookup"><span data-stu-id="ba15f-170">Type</span></span>             | <span data-ttu-id="ba15f-171">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="ba15f-171">Required</span></span> | <span data-ttu-id="ba15f-172">Hinweise</span><span class="sxs-lookup"><span data-stu-id="ba15f-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="ba15f-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="ba15f-173">totalHits</span></span> | <span data-ttu-id="ba15f-174">Ganze Zahl</span><span class="sxs-lookup"><span data-stu-id="ba15f-174">integer</span></span>          | <span data-ttu-id="ba15f-175">ja</span><span class="sxs-lookup"><span data-stu-id="ba15f-175">yes</span></span>      | <span data-ttu-id="ba15f-176">Die Gesamtzahl der Übereinstimmungen, Basiseigenschaft `skip` und `take`</span><span class="sxs-lookup"><span data-stu-id="ba15f-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="ba15f-177">Daten</span><span class="sxs-lookup"><span data-stu-id="ba15f-177">data</span></span>      | <span data-ttu-id="ba15f-178">Array von Zeichenfolgen</span><span class="sxs-lookup"><span data-stu-id="ba15f-178">array of strings</span></span> | <span data-ttu-id="ba15f-179">ja</span><span class="sxs-lookup"><span data-stu-id="ba15f-179">yes</span></span>      | <span data-ttu-id="ba15f-180">Die Paket-IDs übereinstimmen, die von der Anforderung</span><span class="sxs-lookup"><span data-stu-id="ba15f-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="ba15f-181">Beispielanforderung</span><span class="sxs-lookup"><span data-stu-id="ba15f-181">Sample request</span></span>

<span data-ttu-id="ba15f-182">ERHALTEN https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="ba15f-182">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="ba15f-183">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="ba15f-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="ba15f-184">Auflisten von Paketversionen</span><span class="sxs-lookup"><span data-stu-id="ba15f-184">Enumerate package versions</span></span>

<span data-ttu-id="ba15f-185">Eine Paket-ID mithilfe der vorherigen-API ermittelt wurde, können ein Client die AutoVervollständigen-API Sie Paketversionen für eine angegebene Paket-ID aufgelistet werden.</span><span class="sxs-lookup"><span data-stu-id="ba15f-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="ba15f-186">Eine Paketversion, die nicht aufgeführte ist, werden nicht in den Ergebnissen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="ba15f-186">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="ba15f-187">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="ba15f-187">Request parameters</span></span>

<span data-ttu-id="ba15f-188">name</span><span class="sxs-lookup"><span data-stu-id="ba15f-188">Name</span></span>        | <span data-ttu-id="ba15f-189">In</span><span class="sxs-lookup"><span data-stu-id="ba15f-189">In</span></span>     | <span data-ttu-id="ba15f-190">Typ</span><span class="sxs-lookup"><span data-stu-id="ba15f-190">Type</span></span>    | <span data-ttu-id="ba15f-191">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="ba15f-191">Required</span></span> | <span data-ttu-id="ba15f-192">Hinweise</span><span class="sxs-lookup"><span data-stu-id="ba15f-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="ba15f-193">ID</span><span class="sxs-lookup"><span data-stu-id="ba15f-193">id</span></span>          | <span data-ttu-id="ba15f-194">URL</span><span class="sxs-lookup"><span data-stu-id="ba15f-194">URL</span></span>    | <span data-ttu-id="ba15f-195">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="ba15f-195">string</span></span>  | <span data-ttu-id="ba15f-196">ja</span><span class="sxs-lookup"><span data-stu-id="ba15f-196">yes</span></span>      | <span data-ttu-id="ba15f-197">Die Paket-ID für Versionen abgerufen</span><span class="sxs-lookup"><span data-stu-id="ba15f-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="ba15f-198">Vorabversion</span><span class="sxs-lookup"><span data-stu-id="ba15f-198">prerelease</span></span>  | <span data-ttu-id="ba15f-199">URL</span><span class="sxs-lookup"><span data-stu-id="ba15f-199">URL</span></span>    | <span data-ttu-id="ba15f-200">boolean</span><span class="sxs-lookup"><span data-stu-id="ba15f-200">boolean</span></span> | <span data-ttu-id="ba15f-201">Nein</span><span class="sxs-lookup"><span data-stu-id="ba15f-201">no</span></span>       | <span data-ttu-id="ba15f-202">`true` oder `false` bestimmen, ob enthalten [Vorabversion Pakete](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="ba15f-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="ba15f-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="ba15f-203">semVerLevel</span></span> | <span data-ttu-id="ba15f-204">URL</span><span class="sxs-lookup"><span data-stu-id="ba15f-204">URL</span></span>    | <span data-ttu-id="ba15f-205">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="ba15f-205">string</span></span>  | <span data-ttu-id="ba15f-206">Nein</span><span class="sxs-lookup"><span data-stu-id="ba15f-206">no</span></span>       | <span data-ttu-id="ba15f-207">Eine Versionszeichenfolge SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="ba15f-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="ba15f-208">Wenn `prerelease` nicht angegeben wird, Vorabversion Paketen ausgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="ba15f-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="ba15f-209">Die `semVerLevel` Query-Parameter wird verwendet, um Pakete von SemVer 2.0.0 teilnehmen.</span><span class="sxs-lookup"><span data-stu-id="ba15f-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="ba15f-210">Wenn dieser Parameter ausgeschlossen ist, werden nur SemVer 1.0.0 Versionen zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="ba15f-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="ba15f-211">Wenn `semVerLevel=2.0.0` angegeben wird, SemVer 1.0.0 und SemVer 2.0.0-Versionen zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="ba15f-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="ba15f-212">Finden Sie unter der [SemVer 2.0.0-Unterstützung für nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) für Weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="ba15f-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="ba15f-213">Antwort</span><span class="sxs-lookup"><span data-stu-id="ba15f-213">Response</span></span>

<span data-ttu-id="ba15f-214">Die Antwort ist JSON-Dokument, das alle Paketversionen der bereitgestellte Paket-ID, die das Filtern nach der angegebenen Abfrageparameter enthält.</span><span class="sxs-lookup"><span data-stu-id="ba15f-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="ba15f-215">Der Stamm-JSON-Objekt hat die folgende Eigenschaft:</span><span class="sxs-lookup"><span data-stu-id="ba15f-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="ba15f-216">name</span><span class="sxs-lookup"><span data-stu-id="ba15f-216">Name</span></span>      | <span data-ttu-id="ba15f-217">Typ</span><span class="sxs-lookup"><span data-stu-id="ba15f-217">Type</span></span>             | <span data-ttu-id="ba15f-218">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="ba15f-218">Required</span></span> | <span data-ttu-id="ba15f-219">Hinweise</span><span class="sxs-lookup"><span data-stu-id="ba15f-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="ba15f-220">Daten</span><span class="sxs-lookup"><span data-stu-id="ba15f-220">data</span></span>      | <span data-ttu-id="ba15f-221">Array von Zeichenfolgen</span><span class="sxs-lookup"><span data-stu-id="ba15f-221">array of strings</span></span> | <span data-ttu-id="ba15f-222">ja</span><span class="sxs-lookup"><span data-stu-id="ba15f-222">yes</span></span>      | <span data-ttu-id="ba15f-223">Die Zeichenfolge, die für der Anforderungs Paketversionen</span><span class="sxs-lookup"><span data-stu-id="ba15f-223">The package versions matched by the request</span></span>

<span data-ttu-id="ba15f-224">Die Paketversionen in der `data` Array konnte SemVer 2.0.0 Build Metadaten enthalten (z. B. `1.0.0+metadata`) Wenn die `semVerLevel=2.0.0` wurde in der Abfragezeichenfolge angegeben.</span><span class="sxs-lookup"><span data-stu-id="ba15f-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="ba15f-225">Beispielanforderung</span><span class="sxs-lookup"><span data-stu-id="ba15f-225">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="ba15f-226">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="ba15f-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
