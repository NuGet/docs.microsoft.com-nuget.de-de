---
title: Mithilfe von Push übertragen Sie und zu löschen Sie, NuGet-API
description: Publish-Diensts kann Clients Veröffentlichen neuer Pakete und aus der Liste entfernen oder löschen vorhandene Pakete an.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: ad66d8e0ffda13aaef744104c213863b0e111e0e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547520"
---
# <a name="push-and-delete"></a><span data-ttu-id="1d697-103">Mithilfe von Push übertragen und löschen</span><span class="sxs-lookup"><span data-stu-id="1d697-103">Push and Delete</span></span>

<span data-ttu-id="1d697-104">Es ist möglich, mithilfe von Push übertragen, löschen (oder aus der Liste entfernen, je nach serverimplementierung), und stellen Sie Pakete mithilfe der NuGet-API V3.</span><span class="sxs-lookup"><span data-stu-id="1d697-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="1d697-105">Diese Vorgänge sind basierend auf den `PackagePublish` Ressource finden Sie in der [dienstindex](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="1d697-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="1d697-106">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="1d697-106">Versioning</span></span>

<span data-ttu-id="1d697-107">Die folgenden `@type` Wert wird verwendet:</span><span class="sxs-lookup"><span data-stu-id="1d697-107">The following `@type` value is used:</span></span>

<span data-ttu-id="1d697-108">@type-Wert</span><span class="sxs-lookup"><span data-stu-id="1d697-108">@type value</span></span>          | <span data-ttu-id="1d697-109">Hinweise</span><span class="sxs-lookup"><span data-stu-id="1d697-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="1d697-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="1d697-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="1d697-111">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="1d697-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="1d697-112">Basis-URL</span><span class="sxs-lookup"><span data-stu-id="1d697-112">Base URL</span></span>

<span data-ttu-id="1d697-113">Die base-URL für die folgenden APIs ist der Wert des der `@id` Eigenschaft der `PackagePublish/2.0.0` Ressource in der Paketquelle [dienstindex](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="1d697-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="1d697-114">Die folgende Dokumentation dient Nuget.org URL.</span><span class="sxs-lookup"><span data-stu-id="1d697-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="1d697-115">Betrachten Sie `https://www.nuget.org/api/v2/package` als Platzhalter für die `@id` Wert in der dienstindex gefunden.</span><span class="sxs-lookup"><span data-stu-id="1d697-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="1d697-116">Beachten Sie, dass diese URL, am gleichen Speicherort wie die legacy-V2-Push-Endpunkt, verweist da das Protokoll identisch ist.</span><span class="sxs-lookup"><span data-stu-id="1d697-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="1d697-117">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="1d697-117">HTTP methods</span></span>

<span data-ttu-id="1d697-118">Die `PUT`, `POST` und `DELETE` HTTP-Methoden werden durch diese Ressource unterstützt.</span><span class="sxs-lookup"><span data-stu-id="1d697-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="1d697-119">Welche Methoden für jeden Endpunkt unterstützt werden finden Sie unten.</span><span class="sxs-lookup"><span data-stu-id="1d697-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="1d697-120">Ein Paket mithilfe von Push übertragen</span><span class="sxs-lookup"><span data-stu-id="1d697-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="1d697-121">"NuGet.org" verfügt über [zusätzliche Anforderungen](NuGet-Protocols.md) für die Interaktion mit der Push-Endpunkt.</span><span class="sxs-lookup"><span data-stu-id="1d697-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="1d697-122">NuGet.org unterstützt Ablegevorgänge neuer Pakete mithilfe der folgenden-API.</span><span class="sxs-lookup"><span data-stu-id="1d697-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="1d697-123">Wenn das Paket mit der angegebenen ID und Version bereits vorhanden ist, lehnt nuget.org den Push.</span><span class="sxs-lookup"><span data-stu-id="1d697-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="1d697-124">Anderen Paketquellen unterstützen möglicherweise das Ersetzen eines vorhandenen Pakets.</span><span class="sxs-lookup"><span data-stu-id="1d697-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="1d697-125">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="1d697-125">Request parameters</span></span>

<span data-ttu-id="1d697-126">name</span><span class="sxs-lookup"><span data-stu-id="1d697-126">Name</span></span>           | <span data-ttu-id="1d697-127">In</span><span class="sxs-lookup"><span data-stu-id="1d697-127">In</span></span>     | <span data-ttu-id="1d697-128">Typ</span><span class="sxs-lookup"><span data-stu-id="1d697-128">Type</span></span>   | <span data-ttu-id="1d697-129">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="1d697-129">Required</span></span> | <span data-ttu-id="1d697-130">Hinweise</span><span class="sxs-lookup"><span data-stu-id="1d697-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="1d697-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="1d697-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="1d697-132">Header</span><span class="sxs-lookup"><span data-stu-id="1d697-132">Header</span></span> | <span data-ttu-id="1d697-133">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="1d697-133">string</span></span> | <span data-ttu-id="1d697-134">ja</span><span class="sxs-lookup"><span data-stu-id="1d697-134">yes</span></span>      | <span data-ttu-id="1d697-135">Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="1d697-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="1d697-136">Die API-Schlüssel ist eine nicht transparente Zeichenfolge, aus der Paketquelle vom Benutzer abgerufen und in den Client konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="1d697-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="1d697-137">Kein besonderes Zeichenfolgenformat wird vorgeschrieben, aber der API-Schlüssel sollte nicht länger als eine angemessene Größe für HTTP-Headerwerte.</span><span class="sxs-lookup"><span data-stu-id="1d697-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="1d697-138">Anforderungstext</span><span class="sxs-lookup"><span data-stu-id="1d697-138">Request body</span></span>

<span data-ttu-id="1d697-139">Der Anforderungstext muss in der folgenden Form stehen:</span><span class="sxs-lookup"><span data-stu-id="1d697-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="1d697-140">Mehrteilige Formulardaten</span><span class="sxs-lookup"><span data-stu-id="1d697-140">Multipart form data</span></span>

<span data-ttu-id="1d697-141">Der Anforderungsheader `Content-Type` ist `multipart/form-data` und das erste Element im Hauptteil Anforderung ist die unformatierten Bytes des der NUPKG-Datei mithilfe von Push übertragen wird.</span><span class="sxs-lookup"><span data-stu-id="1d697-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="1d697-142">Nachfolgende Elemente in den mehrteiligen Text werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="1d697-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="1d697-143">Der Dateiname oder anderen Header der mehrteiligen Elemente werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="1d697-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="1d697-144">Antwort</span><span class="sxs-lookup"><span data-stu-id="1d697-144">Response</span></span>

<span data-ttu-id="1d697-145">Statuscode</span><span class="sxs-lookup"><span data-stu-id="1d697-145">Status Code</span></span> | <span data-ttu-id="1d697-146">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="1d697-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="1d697-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="1d697-147">201, 202</span></span>    | <span data-ttu-id="1d697-148">Das Paket wurde erfolgreich per Push übertragen</span><span class="sxs-lookup"><span data-stu-id="1d697-148">The package was successfully pushed</span></span>
<span data-ttu-id="1d697-149">400</span><span class="sxs-lookup"><span data-stu-id="1d697-149">400</span></span>         | <span data-ttu-id="1d697-150">Das angegebene Paket ist ungültig.</span><span class="sxs-lookup"><span data-stu-id="1d697-150">The provided package is invalid</span></span>
<span data-ttu-id="1d697-151">409</span><span class="sxs-lookup"><span data-stu-id="1d697-151">409</span></span>         | <span data-ttu-id="1d697-152">Ein Paket mit der angegebenen ID und Version ist bereits vorhanden.</span><span class="sxs-lookup"><span data-stu-id="1d697-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="1d697-153">Serverimplementierungen unterscheiden sich auf den Statuscode für Erfolg zurückgegeben, wenn ein Paket wurde erfolgreich per Push übertragen wird.</span><span class="sxs-lookup"><span data-stu-id="1d697-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="1d697-154">Löschen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="1d697-154">Delete a package</span></span>

<span data-ttu-id="1d697-155">"NuGet.org" interpretiert, die Paket-Delete-Anforderung als eine "Auflistung aufheben".</span><span class="sxs-lookup"><span data-stu-id="1d697-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="1d697-156">Dies bedeutet, dass das Paket noch für vorhandene Benutzer des Pakets verfügbar ist, aber das Paket nicht mehr angezeigt, in den Suchergebnissen oder in der Webschnittstelle wird.</span><span class="sxs-lookup"><span data-stu-id="1d697-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="1d697-157">Weitere Informationen zu dieser Vorgehensweise finden Sie unter den [Pakete gelöscht](../policies/deleting-packages.md) Richtlinie.</span><span class="sxs-lookup"><span data-stu-id="1d697-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="1d697-158">Andere serverimplementierungen können dieses Signal als ein hartes löschen interpretieren, vorläufiges löschen oder aus der Liste entfernen.</span><span class="sxs-lookup"><span data-stu-id="1d697-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="1d697-159">Z. B. ["NuGet.Server"](https://www.nuget.org/packages/NuGet.Server) (eine Server-Implementierung unterstützt nur die älteren V2-API) unterstützt diese Anforderung verarbeitet, als ein Aufheben der Auflistung oder ein hartes löschen, die basierend auf einer Konfigurationsoption.</span><span class="sxs-lookup"><span data-stu-id="1d697-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="1d697-160">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="1d697-160">Request parameters</span></span>

<span data-ttu-id="1d697-161">name</span><span class="sxs-lookup"><span data-stu-id="1d697-161">Name</span></span>           | <span data-ttu-id="1d697-162">In</span><span class="sxs-lookup"><span data-stu-id="1d697-162">In</span></span>     | <span data-ttu-id="1d697-163">Typ</span><span class="sxs-lookup"><span data-stu-id="1d697-163">Type</span></span>   | <span data-ttu-id="1d697-164">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="1d697-164">Required</span></span> | <span data-ttu-id="1d697-165">Hinweise</span><span class="sxs-lookup"><span data-stu-id="1d697-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="1d697-166">Id</span><span class="sxs-lookup"><span data-stu-id="1d697-166">ID</span></span>             | <span data-ttu-id="1d697-167">URL</span><span class="sxs-lookup"><span data-stu-id="1d697-167">URL</span></span>    | <span data-ttu-id="1d697-168">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="1d697-168">string</span></span> | <span data-ttu-id="1d697-169">ja</span><span class="sxs-lookup"><span data-stu-id="1d697-169">yes</span></span>      | <span data-ttu-id="1d697-170">Die ID des Pakets zu löschenden</span><span class="sxs-lookup"><span data-stu-id="1d697-170">The ID of the package to delete</span></span>
<span data-ttu-id="1d697-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="1d697-171">VERSION</span></span>        | <span data-ttu-id="1d697-172">URL</span><span class="sxs-lookup"><span data-stu-id="1d697-172">URL</span></span>    | <span data-ttu-id="1d697-173">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="1d697-173">string</span></span> | <span data-ttu-id="1d697-174">ja</span><span class="sxs-lookup"><span data-stu-id="1d697-174">yes</span></span>      | <span data-ttu-id="1d697-175">Die Version des zu löschenden Pakets</span><span class="sxs-lookup"><span data-stu-id="1d697-175">The version of the package to delete</span></span>
<span data-ttu-id="1d697-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="1d697-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="1d697-177">Header</span><span class="sxs-lookup"><span data-stu-id="1d697-177">Header</span></span> | <span data-ttu-id="1d697-178">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="1d697-178">string</span></span> | <span data-ttu-id="1d697-179">ja</span><span class="sxs-lookup"><span data-stu-id="1d697-179">yes</span></span>      | <span data-ttu-id="1d697-180">Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="1d697-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="1d697-181">Antwort</span><span class="sxs-lookup"><span data-stu-id="1d697-181">Response</span></span>

<span data-ttu-id="1d697-182">Statuscode</span><span class="sxs-lookup"><span data-stu-id="1d697-182">Status Code</span></span> | <span data-ttu-id="1d697-183">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="1d697-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="1d697-184">204</span><span class="sxs-lookup"><span data-stu-id="1d697-184">204</span></span>         | <span data-ttu-id="1d697-185">Das Paket wurde gelöscht.</span><span class="sxs-lookup"><span data-stu-id="1d697-185">The package was deleted</span></span>
<span data-ttu-id="1d697-186">404</span><span class="sxs-lookup"><span data-stu-id="1d697-186">404</span></span>         | <span data-ttu-id="1d697-187">Kein Paket mit dem angegebenen `ID` und `VERSION` vorhanden ist</span><span class="sxs-lookup"><span data-stu-id="1d697-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="1d697-188">Neu Auflisten eines Pakets</span><span class="sxs-lookup"><span data-stu-id="1d697-188">Relist a package</span></span>

<span data-ttu-id="1d697-189">Wenn ein Paket nicht aufgeführt ist, ist es möglich, das Paket wieder in den Suchergebnissen, die mit dem Endpunkt "Artikel" sichtbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="1d697-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="1d697-190">Dieser Endpunkt hat die gleiche Form wie die [löschen (aus der Liste entfernen) Endpunkt](#delete-a-package) verwendet jedoch die `POST` anstelle von HTTP-Methode der `DELETE` Methode.</span><span class="sxs-lookup"><span data-stu-id="1d697-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="1d697-191">Wenn das Paket bereits aufgeführt wird, ist die Anforderung immer noch erfolgreich.</span><span class="sxs-lookup"><span data-stu-id="1d697-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="1d697-192">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="1d697-192">Request parameters</span></span>

<span data-ttu-id="1d697-193">name</span><span class="sxs-lookup"><span data-stu-id="1d697-193">Name</span></span>           | <span data-ttu-id="1d697-194">In</span><span class="sxs-lookup"><span data-stu-id="1d697-194">In</span></span>     | <span data-ttu-id="1d697-195">Typ</span><span class="sxs-lookup"><span data-stu-id="1d697-195">Type</span></span>   | <span data-ttu-id="1d697-196">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="1d697-196">Required</span></span> | <span data-ttu-id="1d697-197">Hinweise</span><span class="sxs-lookup"><span data-stu-id="1d697-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="1d697-198">Id</span><span class="sxs-lookup"><span data-stu-id="1d697-198">ID</span></span>             | <span data-ttu-id="1d697-199">URL</span><span class="sxs-lookup"><span data-stu-id="1d697-199">URL</span></span>    | <span data-ttu-id="1d697-200">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="1d697-200">string</span></span> | <span data-ttu-id="1d697-201">ja</span><span class="sxs-lookup"><span data-stu-id="1d697-201">yes</span></span>      | <span data-ttu-id="1d697-202">Die ID des Pakets, die neu auflisten</span><span class="sxs-lookup"><span data-stu-id="1d697-202">The ID of the package to relist</span></span>
<span data-ttu-id="1d697-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="1d697-203">VERSION</span></span>        | <span data-ttu-id="1d697-204">URL</span><span class="sxs-lookup"><span data-stu-id="1d697-204">URL</span></span>    | <span data-ttu-id="1d697-205">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="1d697-205">string</span></span> | <span data-ttu-id="1d697-206">ja</span><span class="sxs-lookup"><span data-stu-id="1d697-206">yes</span></span>      | <span data-ttu-id="1d697-207">Die Version des Pakets neu auflisten</span><span class="sxs-lookup"><span data-stu-id="1d697-207">The version of the package to relist</span></span>
<span data-ttu-id="1d697-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="1d697-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="1d697-209">Header</span><span class="sxs-lookup"><span data-stu-id="1d697-209">Header</span></span> | <span data-ttu-id="1d697-210">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="1d697-210">string</span></span> | <span data-ttu-id="1d697-211">ja</span><span class="sxs-lookup"><span data-stu-id="1d697-211">yes</span></span>      | <span data-ttu-id="1d697-212">Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="1d697-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="1d697-213">Antwort</span><span class="sxs-lookup"><span data-stu-id="1d697-213">Response</span></span>

<span data-ttu-id="1d697-214">Statuscode</span><span class="sxs-lookup"><span data-stu-id="1d697-214">Status Code</span></span> | <span data-ttu-id="1d697-215">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="1d697-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="1d697-216">300</span><span class="sxs-lookup"><span data-stu-id="1d697-216">200</span></span>         | <span data-ttu-id="1d697-217">Das Paket wird jetzt aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="1d697-217">The package is now listed</span></span>
<span data-ttu-id="1d697-218">404</span><span class="sxs-lookup"><span data-stu-id="1d697-218">404</span></span>         | <span data-ttu-id="1d697-219">Kein Paket mit dem angegebenen `ID` und `VERSION` vorhanden ist</span><span class="sxs-lookup"><span data-stu-id="1d697-219">No package with the provided `ID` and `VERSION` exists</span></span>
