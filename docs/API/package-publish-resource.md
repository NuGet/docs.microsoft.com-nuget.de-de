---
title: "Push-als auch löschen, die NuGet-API | Microsoft Docs"
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
description: "Der Dienst veröffentlichen kann Clients Veröffentlichen neuer Pakete und Benutzerauswahl oder löschen vorhandene Pakete."
keywords: "NuGet-API-Push-Paket-API die NuGet-Paket löschen, NuGet-API Benutzerauswahl Paket API NuGet-Paket zum Hochladen, API NuGet-Paket erstellen."
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: f8051ca57fccae77917567d8c9f2f8a120a8d884
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="3c776-104">Push-als auch löschen</span><span class="sxs-lookup"><span data-stu-id="3c776-104">Push and Delete</span></span>

<span data-ttu-id="3c776-105">Es ist möglich, mithilfe von Push übertragen, löschen (oder Benutzerauswahl, je nach serverimplementierung), und stellen Sie Pakete mithilfe der NuGet-V3-API.</span><span class="sxs-lookup"><span data-stu-id="3c776-105">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="3c776-106">Basieren diese Vorgänge deaktivieren, der die `PackagePublish` Ressource gefunden, der [Dienst Index](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="3c776-106">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="3c776-107">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="3c776-107">Versioning</span></span>

<span data-ttu-id="3c776-108">Die folgenden `@type` Wert wird verwendet:</span><span class="sxs-lookup"><span data-stu-id="3c776-108">The following `@type` value is used:</span></span>

<span data-ttu-id="3c776-109">@type-Wert</span><span class="sxs-lookup"><span data-stu-id="3c776-109">@type value</span></span>          | <span data-ttu-id="3c776-110">Hinweise</span><span class="sxs-lookup"><span data-stu-id="3c776-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="3c776-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="3c776-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="3c776-112">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="3c776-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="3c776-113">Basis-URL</span><span class="sxs-lookup"><span data-stu-id="3c776-113">Base URL</span></span>

<span data-ttu-id="3c776-114">Die base-URL für die folgenden APIs ist der Wert des der `@id` Eigenschaft von der `PackagePublish/2.0.0` Ressource in der Paketquelle [Dienst Index](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="3c776-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="3c776-115">Die Dokumentation wird sich der Nuget.org-URL verwendet.</span><span class="sxs-lookup"><span data-stu-id="3c776-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="3c776-116">Betrachten Sie `https://www.nuget.org/api/v2/package` als Platzhalter für die `@id` Wert in der Service-Index gefunden.</span><span class="sxs-lookup"><span data-stu-id="3c776-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="3c776-117">Beachten Sie, dass diese URL verweist auf am gleichen Speicherort wie die ältere V2-Push-Endpunkt auf, da das Protokoll identisch ist.</span><span class="sxs-lookup"><span data-stu-id="3c776-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="3c776-118">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="3c776-118">HTTP methods</span></span>

<span data-ttu-id="3c776-119">Die `PUT`, `POST` und `DELETE` HTTP-Methoden werden durch diese Ressource unterstützt.</span><span class="sxs-lookup"><span data-stu-id="3c776-119">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="3c776-120">Welche Methoden für jeden Endpunkt unterstützt werden finden Sie weiter unten.</span><span class="sxs-lookup"><span data-stu-id="3c776-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="3c776-121">Ein Paket mithilfe von Push übertragen</span><span class="sxs-lookup"><span data-stu-id="3c776-121">Push a package</span></span>

> [!Note]
> <span data-ttu-id="3c776-122">NuGet.org hat [zusätzliche Anforderungen](NuGet-Protocols.md) für die Interaktion mit der Push-Endpunkt.</span><span class="sxs-lookup"><span data-stu-id="3c776-122">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="3c776-123">NuGet.org unterstützt, wie neue Pakete, die mithilfe der folgenden-API.</span><span class="sxs-lookup"><span data-stu-id="3c776-123">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="3c776-124">Wenn das Paket mit der angegebenen ID und die Version bereits vorhanden ist, lehnt nuget.org der Push-Vorgang.</span><span class="sxs-lookup"><span data-stu-id="3c776-124">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="3c776-125">Andere Paketquellen unterstützen möglicherweise das Ersetzen eines vorhandenen Pakets.</span><span class="sxs-lookup"><span data-stu-id="3c776-125">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="3c776-126">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="3c776-126">Request parameters</span></span>

<span data-ttu-id="3c776-127">name</span><span class="sxs-lookup"><span data-stu-id="3c776-127">Name</span></span>           | <span data-ttu-id="3c776-128">In</span><span class="sxs-lookup"><span data-stu-id="3c776-128">In</span></span>     | <span data-ttu-id="3c776-129">Typ</span><span class="sxs-lookup"><span data-stu-id="3c776-129">Type</span></span>   | <span data-ttu-id="3c776-130">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="3c776-130">Required</span></span> | <span data-ttu-id="3c776-131">Hinweise</span><span class="sxs-lookup"><span data-stu-id="3c776-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="3c776-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="3c776-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="3c776-133">Header</span><span class="sxs-lookup"><span data-stu-id="3c776-133">Header</span></span> | <span data-ttu-id="3c776-134">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="3c776-134">string</span></span> | <span data-ttu-id="3c776-135">ja</span><span class="sxs-lookup"><span data-stu-id="3c776-135">yes</span></span>      | <span data-ttu-id="3c776-136">Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="3c776-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="3c776-137">API-Schlüssel ist eine nicht transparente Zeichenfolge, aus der Paketquelle vom Benutzer erhalten und in den Client konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="3c776-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="3c776-138">Wird kein bestimmtes Zeichenfolgenformat beauftragt, aber der API-Schlüssel sollte nicht länger als eine angemessene Größe für HTTP-Header-Werte.</span><span class="sxs-lookup"><span data-stu-id="3c776-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="3c776-139">Anforderungstext</span><span class="sxs-lookup"><span data-stu-id="3c776-139">Request body</span></span>

<span data-ttu-id="3c776-140">Der Anforderungstext muss in der folgenden Form stammen:</span><span class="sxs-lookup"><span data-stu-id="3c776-140">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="3c776-141">Mehrteiligen Formulardaten.</span><span class="sxs-lookup"><span data-stu-id="3c776-141">Multipart form data</span></span>

<span data-ttu-id="3c776-142">Der Anforderungsheader `Content-Type` ist `multipart/form-data` und das erste Element im Hauptteil Anforderung ist, das die Rohdatenbytes, die von der NUPKG per Push übermittelt.</span><span class="sxs-lookup"><span data-stu-id="3c776-142">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="3c776-143">Nachfolgende Elemente in den mehrteiligen Text werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="3c776-143">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="3c776-144">Der Dateiname oder eventuelle weitere Header der mehrteiligen Elemente werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="3c776-144">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="3c776-145">Antwort</span><span class="sxs-lookup"><span data-stu-id="3c776-145">Response</span></span>

<span data-ttu-id="3c776-146">Statuscode</span><span class="sxs-lookup"><span data-stu-id="3c776-146">Status Code</span></span> | <span data-ttu-id="3c776-147">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="3c776-147">Meaning</span></span>
----------- | -------
<span data-ttu-id="3c776-148">201, 202</span><span class="sxs-lookup"><span data-stu-id="3c776-148">201, 202</span></span>    | <span data-ttu-id="3c776-149">Das Paket wurde erfolgreich übertragen.</span><span class="sxs-lookup"><span data-stu-id="3c776-149">The package was successfully pushed</span></span>
<span data-ttu-id="3c776-150">400</span><span class="sxs-lookup"><span data-stu-id="3c776-150">400</span></span>         | <span data-ttu-id="3c776-151">Das bereitgestellte Paket ist ungültig</span><span class="sxs-lookup"><span data-stu-id="3c776-151">The provided package is invalid</span></span>
<span data-ttu-id="3c776-152">409</span><span class="sxs-lookup"><span data-stu-id="3c776-152">409</span></span>         | <span data-ttu-id="3c776-153">Ein Paket mit der angegebenen ID und die Version ist bereits vorhanden.</span><span class="sxs-lookup"><span data-stu-id="3c776-153">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="3c776-154">Serverimplementierungen unterscheiden sich auf dem Erfolgsstatuscode zurückgegeben, wenn ein Paket erfolgreich übertragen wird.</span><span class="sxs-lookup"><span data-stu-id="3c776-154">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="3c776-155">Löschen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="3c776-155">Delete a package</span></span>

<span data-ttu-id="3c776-156">NuGet.org interpretiert die Paket-Delete-Anforderung als ein "Benutzerauswahl".</span><span class="sxs-lookup"><span data-stu-id="3c776-156">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="3c776-157">Dies bedeutet, dass das Paket für vorhandene Consumer des Pakets weiterhin verfügbar ist, aber das Paket nicht mehr angezeigt, in den Suchergebnissen oder in der Webschnittstelle wird.</span><span class="sxs-lookup"><span data-stu-id="3c776-157">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="3c776-158">Weitere Informationen zu dieser Vorgehensweise finden Sie unter der [Pakete gelöscht](../policies/deleting-packages.md) Richtlinie.</span><span class="sxs-lookup"><span data-stu-id="3c776-158">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="3c776-159">Andere serverimplementierungen sind frei, um dieses Signal als feste Löschvorgang interpretieren, vorläufigen löschen oder Benutzerauswahl.</span><span class="sxs-lookup"><span data-stu-id="3c776-159">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="3c776-160">Beispielsweise [NuGet.Server in](https://www.nuget.org/packages/NuGet.Server) (eine Server-Implementierung unterstützt nur die ältere V2-API) unterstützt diese Anforderung als ein Unlist oder ein hartes löschen, die basierend auf einer Konfigurationsoption behandeln.</span><span class="sxs-lookup"><span data-stu-id="3c776-160">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="3c776-161">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="3c776-161">Request parameters</span></span>

<span data-ttu-id="3c776-162">name</span><span class="sxs-lookup"><span data-stu-id="3c776-162">Name</span></span>           | <span data-ttu-id="3c776-163">In</span><span class="sxs-lookup"><span data-stu-id="3c776-163">In</span></span>     | <span data-ttu-id="3c776-164">Typ</span><span class="sxs-lookup"><span data-stu-id="3c776-164">Type</span></span>   | <span data-ttu-id="3c776-165">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="3c776-165">Required</span></span> | <span data-ttu-id="3c776-166">Hinweise</span><span class="sxs-lookup"><span data-stu-id="3c776-166">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="3c776-167">Id</span><span class="sxs-lookup"><span data-stu-id="3c776-167">ID</span></span>             | <span data-ttu-id="3c776-168">URL</span><span class="sxs-lookup"><span data-stu-id="3c776-168">URL</span></span>    | <span data-ttu-id="3c776-169">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="3c776-169">string</span></span> | <span data-ttu-id="3c776-170">ja</span><span class="sxs-lookup"><span data-stu-id="3c776-170">yes</span></span>      | <span data-ttu-id="3c776-171">Die ID des Pakets zu löschenden</span><span class="sxs-lookup"><span data-stu-id="3c776-171">The ID of the package to delete</span></span>
<span data-ttu-id="3c776-172">VERSION</span><span class="sxs-lookup"><span data-stu-id="3c776-172">VERSION</span></span>        | <span data-ttu-id="3c776-173">URL</span><span class="sxs-lookup"><span data-stu-id="3c776-173">URL</span></span>    | <span data-ttu-id="3c776-174">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="3c776-174">string</span></span> | <span data-ttu-id="3c776-175">ja</span><span class="sxs-lookup"><span data-stu-id="3c776-175">yes</span></span>      | <span data-ttu-id="3c776-176">Die Version des Pakets gelöscht</span><span class="sxs-lookup"><span data-stu-id="3c776-176">The version of the package to delete</span></span>
<span data-ttu-id="3c776-177">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="3c776-177">X-NuGet-ApiKey</span></span> | <span data-ttu-id="3c776-178">Header</span><span class="sxs-lookup"><span data-stu-id="3c776-178">Header</span></span> | <span data-ttu-id="3c776-179">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="3c776-179">string</span></span> | <span data-ttu-id="3c776-180">ja</span><span class="sxs-lookup"><span data-stu-id="3c776-180">yes</span></span>      | <span data-ttu-id="3c776-181">Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="3c776-181">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="3c776-182">Antwort</span><span class="sxs-lookup"><span data-stu-id="3c776-182">Response</span></span>

<span data-ttu-id="3c776-183">Statuscode</span><span class="sxs-lookup"><span data-stu-id="3c776-183">Status Code</span></span> | <span data-ttu-id="3c776-184">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="3c776-184">Meaning</span></span>
----------- | -------
<span data-ttu-id="3c776-185">204</span><span class="sxs-lookup"><span data-stu-id="3c776-185">204</span></span>         | <span data-ttu-id="3c776-186">Das Paket wurde gelöscht.</span><span class="sxs-lookup"><span data-stu-id="3c776-186">The package was deleted</span></span>
<span data-ttu-id="3c776-187">404</span><span class="sxs-lookup"><span data-stu-id="3c776-187">404</span></span>         | <span data-ttu-id="3c776-188">Kein Paket mit dem angegebenen `ID` und `VERSION` vorhanden ist</span><span class="sxs-lookup"><span data-stu-id="3c776-188">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="3c776-189">Ein Paket wiedereinstellen</span><span class="sxs-lookup"><span data-stu-id="3c776-189">Relist a package</span></span>

<span data-ttu-id="3c776-190">Wenn ein Paket nicht aufgeführte ist, ist es möglich, das Paket erneut in den Suchergebnissen unter Verwendung des Endpunkts "Artikel" sichtbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="3c776-190">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="3c776-191">Dieser Endpunkt hat dieselbe Form wie die [löschen (Benutzerauswahl) Endpunkt](#delete-a-package) verwendet jedoch die `POST` HTTP-Methode der `DELETE` Methode.</span><span class="sxs-lookup"><span data-stu-id="3c776-191">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="3c776-192">Wenn das Paket bereits aufgeführt ist, wird die Anforderung trotzdem ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="3c776-192">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="3c776-193">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="3c776-193">Request parameters</span></span>

<span data-ttu-id="3c776-194">name</span><span class="sxs-lookup"><span data-stu-id="3c776-194">Name</span></span>           | <span data-ttu-id="3c776-195">In</span><span class="sxs-lookup"><span data-stu-id="3c776-195">In</span></span>     | <span data-ttu-id="3c776-196">Typ</span><span class="sxs-lookup"><span data-stu-id="3c776-196">Type</span></span>   | <span data-ttu-id="3c776-197">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="3c776-197">Required</span></span> | <span data-ttu-id="3c776-198">Hinweise</span><span class="sxs-lookup"><span data-stu-id="3c776-198">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="3c776-199">Id</span><span class="sxs-lookup"><span data-stu-id="3c776-199">ID</span></span>             | <span data-ttu-id="3c776-200">URL</span><span class="sxs-lookup"><span data-stu-id="3c776-200">URL</span></span>    | <span data-ttu-id="3c776-201">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="3c776-201">string</span></span> | <span data-ttu-id="3c776-202">ja</span><span class="sxs-lookup"><span data-stu-id="3c776-202">yes</span></span>      | <span data-ttu-id="3c776-203">Die ID des Pakets wiedereinstellen</span><span class="sxs-lookup"><span data-stu-id="3c776-203">The ID of the package to relist</span></span>
<span data-ttu-id="3c776-204">VERSION</span><span class="sxs-lookup"><span data-stu-id="3c776-204">VERSION</span></span>        | <span data-ttu-id="3c776-205">URL</span><span class="sxs-lookup"><span data-stu-id="3c776-205">URL</span></span>    | <span data-ttu-id="3c776-206">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="3c776-206">string</span></span> | <span data-ttu-id="3c776-207">ja</span><span class="sxs-lookup"><span data-stu-id="3c776-207">yes</span></span>      | <span data-ttu-id="3c776-208">Die Version des Pakets wiedereinstellen</span><span class="sxs-lookup"><span data-stu-id="3c776-208">The version of the package to relist</span></span>
<span data-ttu-id="3c776-209">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="3c776-209">X-NuGet-ApiKey</span></span> | <span data-ttu-id="3c776-210">Header</span><span class="sxs-lookup"><span data-stu-id="3c776-210">Header</span></span> | <span data-ttu-id="3c776-211">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="3c776-211">string</span></span> | <span data-ttu-id="3c776-212">ja</span><span class="sxs-lookup"><span data-stu-id="3c776-212">yes</span></span>      | <span data-ttu-id="3c776-213">Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="3c776-213">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="3c776-214">Antwort</span><span class="sxs-lookup"><span data-stu-id="3c776-214">Response</span></span>

<span data-ttu-id="3c776-215">Statuscode</span><span class="sxs-lookup"><span data-stu-id="3c776-215">Status Code</span></span> | <span data-ttu-id="3c776-216">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="3c776-216">Meaning</span></span>
----------- | -------
<span data-ttu-id="3c776-217">300</span><span class="sxs-lookup"><span data-stu-id="3c776-217">200</span></span>         | <span data-ttu-id="3c776-218">Das Paket wird jetzt aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="3c776-218">The package is now listed</span></span>
<span data-ttu-id="3c776-219">404</span><span class="sxs-lookup"><span data-stu-id="3c776-219">404</span></span>         | <span data-ttu-id="3c776-220">Kein Paket mit dem angegebenen `ID` und `VERSION` vorhanden ist</span><span class="sxs-lookup"><span data-stu-id="3c776-220">No package with the provided `ID` and `VERSION` exists</span></span>
