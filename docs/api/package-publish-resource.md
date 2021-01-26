---
title: Push und DELETE, nuget-API
description: Der Veröffentlichungs Dienst ermöglicht es Clients, neue Pakete zu veröffentlichen und vorhandene Pakete zu entfernen oder zu löschen.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773921"
---
# <a name="push-and-delete"></a><span data-ttu-id="43c27-103">Push und DELETE</span><span class="sxs-lookup"><span data-stu-id="43c27-103">Push and Delete</span></span>

<span data-ttu-id="43c27-104">Es ist möglich, abhängig von der Server Implementierung Push, DELETE (oder die Auflistung aufzuheben) und Pakete mit der nuget-V3-API zu wiederholen.</span><span class="sxs-lookup"><span data-stu-id="43c27-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="43c27-105">Diese Vorgänge basieren auf der Ressource, die `PackagePublish` im [Dienst Index](service-index.md)gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="43c27-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="43c27-106">Versionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="43c27-106">Versioning</span></span>

<span data-ttu-id="43c27-107">Der folgende `@type` Wert wird verwendet:</span><span class="sxs-lookup"><span data-stu-id="43c27-107">The following `@type` value is used:</span></span>

<span data-ttu-id="43c27-108">Wert vom Typ @type</span><span class="sxs-lookup"><span data-stu-id="43c27-108">@type value</span></span>          | <span data-ttu-id="43c27-109">Hinweise</span><span class="sxs-lookup"><span data-stu-id="43c27-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="43c27-110">Packagepublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="43c27-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="43c27-111">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="43c27-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="43c27-112">Basis-URL</span><span class="sxs-lookup"><span data-stu-id="43c27-112">Base URL</span></span>

<span data-ttu-id="43c27-113">Die Basis-URL für die folgenden APIs ist der Wert der `@id` -Eigenschaft der `PackagePublish/2.0.0` Ressource im [Dienst Index](service-index.md)der Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="43c27-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="43c27-114">In der nachfolgenden Dokumentation wird die URL von "nuget. org" verwendet.</span><span class="sxs-lookup"><span data-stu-id="43c27-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="43c27-115">Beachten Sie `https://www.nuget.org/api/v2/package` als Platzhalter für den `@id` Wert, der im Dienst Index gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="43c27-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="43c27-116">Beachten Sie, dass diese URL auf denselben Speicherort wie der Legacy-v2-Push-Endpunkt verweist, da das Protokoll identisch ist.</span><span class="sxs-lookup"><span data-stu-id="43c27-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="43c27-117">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="43c27-117">HTTP methods</span></span>

<span data-ttu-id="43c27-118">Die `PUT` `POST` http- `DELETE` Methoden, und werden von dieser Ressource unterstützt.</span><span class="sxs-lookup"><span data-stu-id="43c27-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="43c27-119">Informationen dazu, welche Methoden an jedem Endpunkt unterstützt werden, finden Sie unten.</span><span class="sxs-lookup"><span data-stu-id="43c27-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="43c27-120">Pushen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="43c27-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="43c27-121">nuget.org hat [zusätzliche Anforderungen](NuGet-Protocols.md) für die Interaktion mit dem Push-Endpunkt.</span><span class="sxs-lookup"><span data-stu-id="43c27-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="43c27-122">nuget.org unterstützt das pushen neuer Pakete mithilfe der folgenden API.</span><span class="sxs-lookup"><span data-stu-id="43c27-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="43c27-123">Wenn das Paket mit der angegebenen ID und Version bereits vorhanden ist, lehnt nuget.org den Push ab.</span><span class="sxs-lookup"><span data-stu-id="43c27-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="43c27-124">Andere Paketquellen unterstützen möglicherweise das Ersetzen vorhandener Pakete.</span><span class="sxs-lookup"><span data-stu-id="43c27-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="43c27-125">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43c27-125">Request parameters</span></span>

<span data-ttu-id="43c27-126">Name</span><span class="sxs-lookup"><span data-stu-id="43c27-126">Name</span></span>           | <span data-ttu-id="43c27-127">In</span><span class="sxs-lookup"><span data-stu-id="43c27-127">In</span></span>     | <span data-ttu-id="43c27-128">Typ</span><span class="sxs-lookup"><span data-stu-id="43c27-128">Type</span></span>   | <span data-ttu-id="43c27-129">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="43c27-129">Required</span></span> | <span data-ttu-id="43c27-130">Notizen</span><span class="sxs-lookup"><span data-stu-id="43c27-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="43c27-131">X-nuget-APIKey</span><span class="sxs-lookup"><span data-stu-id="43c27-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="43c27-132">Header</span><span class="sxs-lookup"><span data-stu-id="43c27-132">Header</span></span> | <span data-ttu-id="43c27-133">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="43c27-133">string</span></span> | <span data-ttu-id="43c27-134">ja</span><span class="sxs-lookup"><span data-stu-id="43c27-134">yes</span></span>      | <span data-ttu-id="43c27-135">Zum Beispiel, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="43c27-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="43c27-136">Der API-Schlüssel ist eine nicht transparente Zeichenfolge, die vom Benutzer aus der Paketquelle abgerufen und für den Client konfiguriert wurde.</span><span class="sxs-lookup"><span data-stu-id="43c27-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="43c27-137">Es ist kein bestimmtes Zeichen folgen Format vorgeschrieben, aber die Länge des API-Schlüssels sollte keine angemessene Größe für HTTP-Header Werte überschreiten.</span><span class="sxs-lookup"><span data-stu-id="43c27-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="43c27-138">Anforderungstext</span><span class="sxs-lookup"><span data-stu-id="43c27-138">Request body</span></span>

<span data-ttu-id="43c27-139">Der Anforderungs Text muss in der folgenden Form angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="43c27-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="43c27-140">Mehrteilige Formulardaten</span><span class="sxs-lookup"><span data-stu-id="43c27-140">Multipart form data</span></span>

<span data-ttu-id="43c27-141">Der Anforderungs Header `Content-Type` ist `multipart/form-data` , und das erste Element im Anforderungs Text ist die unformatierten Bytes der. nupkg-Datei, die per pushübertragung durchgesetzt wird.</span><span class="sxs-lookup"><span data-stu-id="43c27-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="43c27-142">Nachfolgende Elemente im mehrteiligen Textkörper werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="43c27-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="43c27-143">Der Dateiname oder andere Header der mehrteiligen Elemente werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="43c27-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="43c27-144">Antwort</span><span class="sxs-lookup"><span data-stu-id="43c27-144">Response</span></span>

<span data-ttu-id="43c27-145">Statuscode</span><span class="sxs-lookup"><span data-stu-id="43c27-145">Status Code</span></span> | <span data-ttu-id="43c27-146">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="43c27-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="43c27-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="43c27-147">201, 202</span></span>    | <span data-ttu-id="43c27-148">Das Paket wurde erfolgreich übermittelt.</span><span class="sxs-lookup"><span data-stu-id="43c27-148">The package was successfully pushed</span></span>
<span data-ttu-id="43c27-149">400</span><span class="sxs-lookup"><span data-stu-id="43c27-149">400</span></span>         | <span data-ttu-id="43c27-150">Das angegebene Paket ist ungültig.</span><span class="sxs-lookup"><span data-stu-id="43c27-150">The provided package is invalid</span></span>
<span data-ttu-id="43c27-151">409</span><span class="sxs-lookup"><span data-stu-id="43c27-151">409</span></span>         | <span data-ttu-id="43c27-152">Ein Paket mit der angegebenen ID und Version ist bereits vorhanden.</span><span class="sxs-lookup"><span data-stu-id="43c27-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="43c27-153">Server Implementierungen variieren dem Erfolgsstatus Code, der zurückgegeben wird, wenn ein Paket erfolgreich übermittelt wurde.</span><span class="sxs-lookup"><span data-stu-id="43c27-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="43c27-154">Löschen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="43c27-154">Delete a package</span></span>

<span data-ttu-id="43c27-155">nuget.org interpretiert die DELETE-Anforderung des Pakets als "Unlist".</span><span class="sxs-lookup"><span data-stu-id="43c27-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="43c27-156">Dies bedeutet, dass das Paket weiterhin für vorhandene Consumer des Pakets verfügbar ist, das Paket jedoch nicht mehr in den Suchergebnissen oder der Weboberfläche angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="43c27-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="43c27-157">Weitere Informationen zu dieser Vorgehensweise finden Sie in der Richtlinie für [gelöschte Pakete](../nuget-org/policies/deleting-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="43c27-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="43c27-158">Andere Server Implementierungen können dieses Signal als harte Löschung, vorläufiges löschen oder Unlist interpretieren.</span><span class="sxs-lookup"><span data-stu-id="43c27-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="43c27-159">Beispielsweise unterstützt [nuget. Server](https://www.nuget.org/packages/NuGet.Server) (eine Server Implementierung, die nur die ältere v2-API unterstützt) die Verarbeitung dieser Anforderung als Auflistung oder Hard Delete basierend auf einer Konfigurationsoption.</span><span class="sxs-lookup"><span data-stu-id="43c27-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="43c27-160">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43c27-160">Request parameters</span></span>

<span data-ttu-id="43c27-161">Name</span><span class="sxs-lookup"><span data-stu-id="43c27-161">Name</span></span>           | <span data-ttu-id="43c27-162">In</span><span class="sxs-lookup"><span data-stu-id="43c27-162">In</span></span>     | <span data-ttu-id="43c27-163">Typ</span><span class="sxs-lookup"><span data-stu-id="43c27-163">Type</span></span>   | <span data-ttu-id="43c27-164">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="43c27-164">Required</span></span> | <span data-ttu-id="43c27-165">Notizen</span><span class="sxs-lookup"><span data-stu-id="43c27-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="43c27-166">id</span><span class="sxs-lookup"><span data-stu-id="43c27-166">ID</span></span>             | <span data-ttu-id="43c27-167">URL</span><span class="sxs-lookup"><span data-stu-id="43c27-167">URL</span></span>    | <span data-ttu-id="43c27-168">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="43c27-168">string</span></span> | <span data-ttu-id="43c27-169">ja</span><span class="sxs-lookup"><span data-stu-id="43c27-169">yes</span></span>      | <span data-ttu-id="43c27-170">Die ID des zu löschenden Pakets.</span><span class="sxs-lookup"><span data-stu-id="43c27-170">The ID of the package to delete</span></span>
<span data-ttu-id="43c27-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="43c27-171">VERSION</span></span>        | <span data-ttu-id="43c27-172">URL</span><span class="sxs-lookup"><span data-stu-id="43c27-172">URL</span></span>    | <span data-ttu-id="43c27-173">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="43c27-173">string</span></span> | <span data-ttu-id="43c27-174">ja</span><span class="sxs-lookup"><span data-stu-id="43c27-174">yes</span></span>      | <span data-ttu-id="43c27-175">Die Version des zu löschenden Pakets.</span><span class="sxs-lookup"><span data-stu-id="43c27-175">The version of the package to delete</span></span>
<span data-ttu-id="43c27-176">X-nuget-APIKey</span><span class="sxs-lookup"><span data-stu-id="43c27-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="43c27-177">Header</span><span class="sxs-lookup"><span data-stu-id="43c27-177">Header</span></span> | <span data-ttu-id="43c27-178">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="43c27-178">string</span></span> | <span data-ttu-id="43c27-179">ja</span><span class="sxs-lookup"><span data-stu-id="43c27-179">yes</span></span>      | <span data-ttu-id="43c27-180">Zum Beispiel, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="43c27-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="43c27-181">Antwort</span><span class="sxs-lookup"><span data-stu-id="43c27-181">Response</span></span>

<span data-ttu-id="43c27-182">Statuscode</span><span class="sxs-lookup"><span data-stu-id="43c27-182">Status Code</span></span> | <span data-ttu-id="43c27-183">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="43c27-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="43c27-184">204</span><span class="sxs-lookup"><span data-stu-id="43c27-184">204</span></span>         | <span data-ttu-id="43c27-185">Das Paket wurde gelöscht.</span><span class="sxs-lookup"><span data-stu-id="43c27-185">The package was deleted</span></span>
<span data-ttu-id="43c27-186">404</span><span class="sxs-lookup"><span data-stu-id="43c27-186">404</span></span>         | <span data-ttu-id="43c27-187">Es ist kein Paket mit dem angegebenen vorhanden `ID` und `VERSION` vorhanden.</span><span class="sxs-lookup"><span data-stu-id="43c27-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="43c27-188">Ein Paket erneut auflisten</span><span class="sxs-lookup"><span data-stu-id="43c27-188">Relist a package</span></span>

<span data-ttu-id="43c27-189">Wenn ein Paket nicht aufgelistet wird, ist es möglich, dieses Paket erneut in den Suchergebnissen mit dem Endpunkt "relist" sichtbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="43c27-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="43c27-190">Dieser Endpunkt hat dieselbe Form wie der [Delete (Unlist)-Endpunkt](#delete-a-package) , verwendet jedoch die `POST` http-Methode anstelle der- `DELETE` Methode.</span><span class="sxs-lookup"><span data-stu-id="43c27-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="43c27-191">Wenn das Paket bereits aufgelistet ist, ist die Anforderung weiterhin erfolgreich.</span><span class="sxs-lookup"><span data-stu-id="43c27-191">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="43c27-192">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="43c27-192">Request parameters</span></span>

<span data-ttu-id="43c27-193">Name</span><span class="sxs-lookup"><span data-stu-id="43c27-193">Name</span></span>           | <span data-ttu-id="43c27-194">In</span><span class="sxs-lookup"><span data-stu-id="43c27-194">In</span></span>     | <span data-ttu-id="43c27-195">Typ</span><span class="sxs-lookup"><span data-stu-id="43c27-195">Type</span></span>   | <span data-ttu-id="43c27-196">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="43c27-196">Required</span></span> | <span data-ttu-id="43c27-197">Notizen</span><span class="sxs-lookup"><span data-stu-id="43c27-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="43c27-198">id</span><span class="sxs-lookup"><span data-stu-id="43c27-198">ID</span></span>             | <span data-ttu-id="43c27-199">URL</span><span class="sxs-lookup"><span data-stu-id="43c27-199">URL</span></span>    | <span data-ttu-id="43c27-200">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="43c27-200">string</span></span> | <span data-ttu-id="43c27-201">ja</span><span class="sxs-lookup"><span data-stu-id="43c27-201">yes</span></span>      | <span data-ttu-id="43c27-202">Die ID des wieder zu erlefenden Pakets.</span><span class="sxs-lookup"><span data-stu-id="43c27-202">The ID of the package to relist</span></span>
<span data-ttu-id="43c27-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="43c27-203">VERSION</span></span>        | <span data-ttu-id="43c27-204">URL</span><span class="sxs-lookup"><span data-stu-id="43c27-204">URL</span></span>    | <span data-ttu-id="43c27-205">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="43c27-205">string</span></span> | <span data-ttu-id="43c27-206">ja</span><span class="sxs-lookup"><span data-stu-id="43c27-206">yes</span></span>      | <span data-ttu-id="43c27-207">Die Version des Pakets, das wieder hergestellt werden soll.</span><span class="sxs-lookup"><span data-stu-id="43c27-207">The version of the package to relist</span></span>
<span data-ttu-id="43c27-208">X-nuget-APIKey</span><span class="sxs-lookup"><span data-stu-id="43c27-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="43c27-209">Header</span><span class="sxs-lookup"><span data-stu-id="43c27-209">Header</span></span> | <span data-ttu-id="43c27-210">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="43c27-210">string</span></span> | <span data-ttu-id="43c27-211">ja</span><span class="sxs-lookup"><span data-stu-id="43c27-211">yes</span></span>      | <span data-ttu-id="43c27-212">Zum Beispiel, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="43c27-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="43c27-213">Antwort</span><span class="sxs-lookup"><span data-stu-id="43c27-213">Response</span></span>

<span data-ttu-id="43c27-214">Statuscode</span><span class="sxs-lookup"><span data-stu-id="43c27-214">Status Code</span></span> | <span data-ttu-id="43c27-215">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="43c27-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="43c27-216">200</span><span class="sxs-lookup"><span data-stu-id="43c27-216">200</span></span>         | <span data-ttu-id="43c27-217">Das Paket ist jetzt aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="43c27-217">The package is now listed</span></span>
<span data-ttu-id="43c27-218">404</span><span class="sxs-lookup"><span data-stu-id="43c27-218">404</span></span>         | <span data-ttu-id="43c27-219">Es ist kein Paket mit dem angegebenen vorhanden `ID` und `VERSION` vorhanden.</span><span class="sxs-lookup"><span data-stu-id="43c27-219">No package with the provided `ID` and `VERSION` exists</span></span>
