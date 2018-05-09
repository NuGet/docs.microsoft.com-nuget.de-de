---
title: Push-als auch löschen, die NuGet-API
description: Der Dienst veröffentlichen kann Clients Veröffentlichen neuer Pakete und Benutzerauswahl oder löschen vorhandene Pakete.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 911c8238624f806b1fbb5c7938d02b6bdfbd8614
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="327de-103">Push-als auch löschen</span><span class="sxs-lookup"><span data-stu-id="327de-103">Push and Delete</span></span>

<span data-ttu-id="327de-104">Es ist möglich, mithilfe von Push übertragen, löschen (oder Benutzerauswahl, je nach serverimplementierung), und stellen Sie Pakete mithilfe der NuGet-V3-API.</span><span class="sxs-lookup"><span data-stu-id="327de-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="327de-105">Basieren diese Vorgänge deaktivieren, der die `PackagePublish` Ressource gefunden, der [Dienst Index](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="327de-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="327de-106">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="327de-106">Versioning</span></span>

<span data-ttu-id="327de-107">Die folgenden `@type` Wert wird verwendet:</span><span class="sxs-lookup"><span data-stu-id="327de-107">The following `@type` value is used:</span></span>

<span data-ttu-id="327de-108">@type-Wert</span><span class="sxs-lookup"><span data-stu-id="327de-108">@type value</span></span>          | <span data-ttu-id="327de-109">Hinweise</span><span class="sxs-lookup"><span data-stu-id="327de-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="327de-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="327de-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="327de-111">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="327de-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="327de-112">Basis-URL</span><span class="sxs-lookup"><span data-stu-id="327de-112">Base URL</span></span>

<span data-ttu-id="327de-113">Die base-URL für die folgenden APIs ist der Wert des der `@id` Eigenschaft von der `PackagePublish/2.0.0` Ressource in der Paketquelle [Dienst Index](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="327de-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="327de-114">Die Dokumentation wird sich der Nuget.org-URL verwendet.</span><span class="sxs-lookup"><span data-stu-id="327de-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="327de-115">Betrachten Sie `https://www.nuget.org/api/v2/package` als Platzhalter für die `@id` Wert in der Service-Index gefunden.</span><span class="sxs-lookup"><span data-stu-id="327de-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="327de-116">Beachten Sie, dass diese URL verweist auf am gleichen Speicherort wie die ältere V2-Push-Endpunkt auf, da das Protokoll identisch ist.</span><span class="sxs-lookup"><span data-stu-id="327de-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="327de-117">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="327de-117">HTTP methods</span></span>

<span data-ttu-id="327de-118">Die `PUT`, `POST` und `DELETE` HTTP-Methoden werden durch diese Ressource unterstützt.</span><span class="sxs-lookup"><span data-stu-id="327de-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="327de-119">Welche Methoden für jeden Endpunkt unterstützt werden finden Sie weiter unten.</span><span class="sxs-lookup"><span data-stu-id="327de-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="327de-120">Ein Paket mithilfe von Push übertragen</span><span class="sxs-lookup"><span data-stu-id="327de-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="327de-121">NuGet.org hat [zusätzliche Anforderungen](NuGet-Protocols.md) für die Interaktion mit der Push-Endpunkt.</span><span class="sxs-lookup"><span data-stu-id="327de-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="327de-122">NuGet.org unterstützt, wie neue Pakete, die mithilfe der folgenden-API.</span><span class="sxs-lookup"><span data-stu-id="327de-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="327de-123">Wenn das Paket mit der angegebenen ID und die Version bereits vorhanden ist, lehnt nuget.org der Push-Vorgang.</span><span class="sxs-lookup"><span data-stu-id="327de-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="327de-124">Andere Paketquellen unterstützen möglicherweise das Ersetzen eines vorhandenen Pakets.</span><span class="sxs-lookup"><span data-stu-id="327de-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="327de-125">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="327de-125">Request parameters</span></span>

<span data-ttu-id="327de-126">name</span><span class="sxs-lookup"><span data-stu-id="327de-126">Name</span></span>           | <span data-ttu-id="327de-127">In</span><span class="sxs-lookup"><span data-stu-id="327de-127">In</span></span>     | <span data-ttu-id="327de-128">Typ</span><span class="sxs-lookup"><span data-stu-id="327de-128">Type</span></span>   | <span data-ttu-id="327de-129">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="327de-129">Required</span></span> | <span data-ttu-id="327de-130">Hinweise</span><span class="sxs-lookup"><span data-stu-id="327de-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="327de-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="327de-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="327de-132">Header</span><span class="sxs-lookup"><span data-stu-id="327de-132">Header</span></span> | <span data-ttu-id="327de-133">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="327de-133">string</span></span> | <span data-ttu-id="327de-134">ja</span><span class="sxs-lookup"><span data-stu-id="327de-134">yes</span></span>      | <span data-ttu-id="327de-135">Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="327de-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="327de-136">API-Schlüssel ist eine nicht transparente Zeichenfolge, aus der Paketquelle vom Benutzer erhalten und in den Client konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="327de-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="327de-137">Wird kein bestimmtes Zeichenfolgenformat beauftragt, aber der API-Schlüssel sollte nicht länger als eine angemessene Größe für HTTP-Header-Werte.</span><span class="sxs-lookup"><span data-stu-id="327de-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="327de-138">Anforderungstext</span><span class="sxs-lookup"><span data-stu-id="327de-138">Request body</span></span>

<span data-ttu-id="327de-139">Der Anforderungstext muss in der folgenden Form stammen:</span><span class="sxs-lookup"><span data-stu-id="327de-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="327de-140">Mehrteiligen Formulardaten.</span><span class="sxs-lookup"><span data-stu-id="327de-140">Multipart form data</span></span>

<span data-ttu-id="327de-141">Der Anforderungsheader `Content-Type` ist `multipart/form-data` und das erste Element im Hauptteil Anforderung ist, das die Rohdatenbytes, die von der NUPKG per Push übermittelt.</span><span class="sxs-lookup"><span data-stu-id="327de-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="327de-142">Nachfolgende Elemente in den mehrteiligen Text werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="327de-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="327de-143">Der Dateiname oder eventuelle weitere Header der mehrteiligen Elemente werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="327de-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="327de-144">Antwort</span><span class="sxs-lookup"><span data-stu-id="327de-144">Response</span></span>

<span data-ttu-id="327de-145">Statuscode</span><span class="sxs-lookup"><span data-stu-id="327de-145">Status Code</span></span> | <span data-ttu-id="327de-146">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="327de-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="327de-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="327de-147">201, 202</span></span>    | <span data-ttu-id="327de-148">Das Paket wurde erfolgreich übertragen.</span><span class="sxs-lookup"><span data-stu-id="327de-148">The package was successfully pushed</span></span>
<span data-ttu-id="327de-149">400</span><span class="sxs-lookup"><span data-stu-id="327de-149">400</span></span>         | <span data-ttu-id="327de-150">Das bereitgestellte Paket ist ungültig</span><span class="sxs-lookup"><span data-stu-id="327de-150">The provided package is invalid</span></span>
<span data-ttu-id="327de-151">409</span><span class="sxs-lookup"><span data-stu-id="327de-151">409</span></span>         | <span data-ttu-id="327de-152">Ein Paket mit der angegebenen ID und die Version ist bereits vorhanden.</span><span class="sxs-lookup"><span data-stu-id="327de-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="327de-153">Serverimplementierungen unterscheiden sich auf dem Erfolgsstatuscode zurückgegeben, wenn ein Paket erfolgreich übertragen wird.</span><span class="sxs-lookup"><span data-stu-id="327de-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="327de-154">Löschen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="327de-154">Delete a package</span></span>

<span data-ttu-id="327de-155">NuGet.org interpretiert die Paket-Delete-Anforderung als ein "Benutzerauswahl".</span><span class="sxs-lookup"><span data-stu-id="327de-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="327de-156">Dies bedeutet, dass das Paket für vorhandene Consumer des Pakets weiterhin verfügbar ist, aber das Paket nicht mehr angezeigt, in den Suchergebnissen oder in der Webschnittstelle wird.</span><span class="sxs-lookup"><span data-stu-id="327de-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="327de-157">Weitere Informationen zu dieser Vorgehensweise finden Sie unter der [Pakete gelöscht](../policies/deleting-packages.md) Richtlinie.</span><span class="sxs-lookup"><span data-stu-id="327de-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="327de-158">Andere serverimplementierungen sind frei, um dieses Signal als feste Löschvorgang interpretieren, vorläufigen löschen oder Benutzerauswahl.</span><span class="sxs-lookup"><span data-stu-id="327de-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="327de-159">Beispielsweise [NuGet.Server in](https://www.nuget.org/packages/NuGet.Server) (eine Server-Implementierung unterstützt nur die ältere V2-API) unterstützt diese Anforderung als ein Unlist oder ein hartes löschen, die basierend auf einer Konfigurationsoption behandeln.</span><span class="sxs-lookup"><span data-stu-id="327de-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="327de-160">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="327de-160">Request parameters</span></span>

<span data-ttu-id="327de-161">name</span><span class="sxs-lookup"><span data-stu-id="327de-161">Name</span></span>           | <span data-ttu-id="327de-162">In</span><span class="sxs-lookup"><span data-stu-id="327de-162">In</span></span>     | <span data-ttu-id="327de-163">Typ</span><span class="sxs-lookup"><span data-stu-id="327de-163">Type</span></span>   | <span data-ttu-id="327de-164">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="327de-164">Required</span></span> | <span data-ttu-id="327de-165">Hinweise</span><span class="sxs-lookup"><span data-stu-id="327de-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="327de-166">Id</span><span class="sxs-lookup"><span data-stu-id="327de-166">ID</span></span>             | <span data-ttu-id="327de-167">URL</span><span class="sxs-lookup"><span data-stu-id="327de-167">URL</span></span>    | <span data-ttu-id="327de-168">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="327de-168">string</span></span> | <span data-ttu-id="327de-169">ja</span><span class="sxs-lookup"><span data-stu-id="327de-169">yes</span></span>      | <span data-ttu-id="327de-170">Die ID des Pakets zu löschenden</span><span class="sxs-lookup"><span data-stu-id="327de-170">The ID of the package to delete</span></span>
<span data-ttu-id="327de-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="327de-171">VERSION</span></span>        | <span data-ttu-id="327de-172">URL</span><span class="sxs-lookup"><span data-stu-id="327de-172">URL</span></span>    | <span data-ttu-id="327de-173">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="327de-173">string</span></span> | <span data-ttu-id="327de-174">ja</span><span class="sxs-lookup"><span data-stu-id="327de-174">yes</span></span>      | <span data-ttu-id="327de-175">Die Version des Pakets gelöscht</span><span class="sxs-lookup"><span data-stu-id="327de-175">The version of the package to delete</span></span>
<span data-ttu-id="327de-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="327de-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="327de-177">Header</span><span class="sxs-lookup"><span data-stu-id="327de-177">Header</span></span> | <span data-ttu-id="327de-178">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="327de-178">string</span></span> | <span data-ttu-id="327de-179">ja</span><span class="sxs-lookup"><span data-stu-id="327de-179">yes</span></span>      | <span data-ttu-id="327de-180">Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="327de-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="327de-181">Antwort</span><span class="sxs-lookup"><span data-stu-id="327de-181">Response</span></span>

<span data-ttu-id="327de-182">Statuscode</span><span class="sxs-lookup"><span data-stu-id="327de-182">Status Code</span></span> | <span data-ttu-id="327de-183">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="327de-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="327de-184">204</span><span class="sxs-lookup"><span data-stu-id="327de-184">204</span></span>         | <span data-ttu-id="327de-185">Das Paket wurde gelöscht.</span><span class="sxs-lookup"><span data-stu-id="327de-185">The package was deleted</span></span>
<span data-ttu-id="327de-186">404</span><span class="sxs-lookup"><span data-stu-id="327de-186">404</span></span>         | <span data-ttu-id="327de-187">Kein Paket mit dem angegebenen `ID` und `VERSION` vorhanden ist</span><span class="sxs-lookup"><span data-stu-id="327de-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="327de-188">Ein Paket wiedereinstellen</span><span class="sxs-lookup"><span data-stu-id="327de-188">Relist a package</span></span>

<span data-ttu-id="327de-189">Wenn ein Paket nicht aufgeführte ist, ist es möglich, das Paket erneut in den Suchergebnissen unter Verwendung des Endpunkts "Artikel" sichtbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="327de-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="327de-190">Dieser Endpunkt hat dieselbe Form wie die [löschen (Benutzerauswahl) Endpunkt](#delete-a-package) verwendet jedoch die `POST` HTTP-Methode der `DELETE` Methode.</span><span class="sxs-lookup"><span data-stu-id="327de-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="327de-191">Wenn das Paket bereits aufgeführt ist, wird die Anforderung trotzdem ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="327de-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="327de-192">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="327de-192">Request parameters</span></span>

<span data-ttu-id="327de-193">name</span><span class="sxs-lookup"><span data-stu-id="327de-193">Name</span></span>           | <span data-ttu-id="327de-194">In</span><span class="sxs-lookup"><span data-stu-id="327de-194">In</span></span>     | <span data-ttu-id="327de-195">Typ</span><span class="sxs-lookup"><span data-stu-id="327de-195">Type</span></span>   | <span data-ttu-id="327de-196">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="327de-196">Required</span></span> | <span data-ttu-id="327de-197">Hinweise</span><span class="sxs-lookup"><span data-stu-id="327de-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="327de-198">Id</span><span class="sxs-lookup"><span data-stu-id="327de-198">ID</span></span>             | <span data-ttu-id="327de-199">URL</span><span class="sxs-lookup"><span data-stu-id="327de-199">URL</span></span>    | <span data-ttu-id="327de-200">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="327de-200">string</span></span> | <span data-ttu-id="327de-201">ja</span><span class="sxs-lookup"><span data-stu-id="327de-201">yes</span></span>      | <span data-ttu-id="327de-202">Die ID des Pakets wiedereinstellen</span><span class="sxs-lookup"><span data-stu-id="327de-202">The ID of the package to relist</span></span>
<span data-ttu-id="327de-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="327de-203">VERSION</span></span>        | <span data-ttu-id="327de-204">URL</span><span class="sxs-lookup"><span data-stu-id="327de-204">URL</span></span>    | <span data-ttu-id="327de-205">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="327de-205">string</span></span> | <span data-ttu-id="327de-206">ja</span><span class="sxs-lookup"><span data-stu-id="327de-206">yes</span></span>      | <span data-ttu-id="327de-207">Die Version des Pakets wiedereinstellen</span><span class="sxs-lookup"><span data-stu-id="327de-207">The version of the package to relist</span></span>
<span data-ttu-id="327de-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="327de-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="327de-209">Header</span><span class="sxs-lookup"><span data-stu-id="327de-209">Header</span></span> | <span data-ttu-id="327de-210">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="327de-210">string</span></span> | <span data-ttu-id="327de-211">ja</span><span class="sxs-lookup"><span data-stu-id="327de-211">yes</span></span>      | <span data-ttu-id="327de-212">Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="327de-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="327de-213">Antwort</span><span class="sxs-lookup"><span data-stu-id="327de-213">Response</span></span>

<span data-ttu-id="327de-214">Statuscode</span><span class="sxs-lookup"><span data-stu-id="327de-214">Status Code</span></span> | <span data-ttu-id="327de-215">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="327de-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="327de-216">300</span><span class="sxs-lookup"><span data-stu-id="327de-216">200</span></span>         | <span data-ttu-id="327de-217">Das Paket wird jetzt aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="327de-217">The package is now listed</span></span>
<span data-ttu-id="327de-218">404</span><span class="sxs-lookup"><span data-stu-id="327de-218">404</span></span>         | <span data-ttu-id="327de-219">Kein Paket mit dem angegebenen `ID` und `VERSION` vorhanden ist</span><span class="sxs-lookup"><span data-stu-id="327de-219">No package with the provided `ID` and `VERSION` exists</span></span>
