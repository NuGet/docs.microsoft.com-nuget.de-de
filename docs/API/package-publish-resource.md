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
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "Der Dienst veröffentlichen kann Clients Veröffentlichen neuer Pakete und Benutzerauswahl oder löschen vorhandene Pakete."
keywords: "NuGet-API-Push-Paket-API die NuGet-Paket löschen, NuGet-API Benutzerauswahl Paket API NuGet-Paket zum Hochladen, API NuGet-Paket erstellen."
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 87970a701c63bce2b74c619069ec1d231ea77ab5
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/05/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="02a4e-104">Push-als auch löschen</span><span class="sxs-lookup"><span data-stu-id="02a4e-104">Push and Delete</span></span>

<span data-ttu-id="02a4e-105">Es ist möglich, mithilfe von Push übertragen, löschen (oder Benutzerauswahl, je nach serverimplementierung), und stellen Sie Pakete mithilfe der NuGet-V3-API.</span><span class="sxs-lookup"><span data-stu-id="02a4e-105">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="02a4e-106">Basieren diese Vorgänge deaktivieren, der die `PackagePublish` Ressource gefunden, der [Dienst Index](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="02a4e-106">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="02a4e-107">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="02a4e-107">Versioning</span></span>

<span data-ttu-id="02a4e-108">Die folgenden `@type` Wert wird verwendet:</span><span class="sxs-lookup"><span data-stu-id="02a4e-108">The following `@type` value is used:</span></span>

<span data-ttu-id="02a4e-109">@type-Wert</span><span class="sxs-lookup"><span data-stu-id="02a4e-109">@type value</span></span>          | <span data-ttu-id="02a4e-110">Hinweise</span><span class="sxs-lookup"><span data-stu-id="02a4e-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="02a4e-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="02a4e-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="02a4e-112">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="02a4e-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="02a4e-113">Basis-URL</span><span class="sxs-lookup"><span data-stu-id="02a4e-113">Base URL</span></span>

<span data-ttu-id="02a4e-114">Die base-URL für die folgenden APIs ist der Wert des der `@id` Eigenschaft von der `PackagePublish/2.0.0` Ressource in der Paketquelle [Dienst Index](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="02a4e-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="02a4e-115">Die Dokumentation wird sich der Nuget.org-URL verwendet.</span><span class="sxs-lookup"><span data-stu-id="02a4e-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="02a4e-116">Betrachten Sie `https://www.nuget.org/api/v2/package` als Platzhalter für die `@id` Wert in der Service-Index gefunden.</span><span class="sxs-lookup"><span data-stu-id="02a4e-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="02a4e-117">Beachten Sie, dass diese URL verweist auf am gleichen Speicherort wie die ältere V2-Push-Endpunkt auf, da das Protokoll identisch ist.</span><span class="sxs-lookup"><span data-stu-id="02a4e-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="02a4e-118">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="02a4e-118">HTTP methods</span></span>

<span data-ttu-id="02a4e-119">Die `PUT`, `POST` und `DELETE` HTTP-Methoden werden durch diese Ressource unterstützt.</span><span class="sxs-lookup"><span data-stu-id="02a4e-119">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="02a4e-120">Welche Methoden für jeden Endpunkt unterstützt werden finden Sie weiter unten.</span><span class="sxs-lookup"><span data-stu-id="02a4e-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="02a4e-121">Ein Paket mithilfe von Push übertragen</span><span class="sxs-lookup"><span data-stu-id="02a4e-121">Push a package</span></span>

> [!Note]
> <span data-ttu-id="02a4e-122">NuGet.org hat [zusätzliche Anforderungen](NuGet-Protocols.md) für die Interaktion mit der Push-Endpunkt.</span><span class="sxs-lookup"><span data-stu-id="02a4e-122">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="02a4e-123">NuGet.org unterstützt, wie neue Pakete, die mithilfe der folgenden-API.</span><span class="sxs-lookup"><span data-stu-id="02a4e-123">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="02a4e-124">Wenn das Paket mit der angegebenen ID und die Version bereits vorhanden ist, lehnt nuget.org der Push-Vorgang.</span><span class="sxs-lookup"><span data-stu-id="02a4e-124">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="02a4e-125">Andere Paketquellen unterstützen möglicherweise das Ersetzen eines vorhandenen Pakets.</span><span class="sxs-lookup"><span data-stu-id="02a4e-125">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="02a4e-126">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="02a4e-126">Request parameters</span></span>

<span data-ttu-id="02a4e-127">name</span><span class="sxs-lookup"><span data-stu-id="02a4e-127">Name</span></span>           | <span data-ttu-id="02a4e-128">In</span><span class="sxs-lookup"><span data-stu-id="02a4e-128">In</span></span>     | <span data-ttu-id="02a4e-129">Typ</span><span class="sxs-lookup"><span data-stu-id="02a4e-129">Type</span></span>   | <span data-ttu-id="02a4e-130">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="02a4e-130">Required</span></span> | <span data-ttu-id="02a4e-131">Hinweise</span><span class="sxs-lookup"><span data-stu-id="02a4e-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="02a4e-132">X-NuGet-"apikey"</span><span class="sxs-lookup"><span data-stu-id="02a4e-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="02a4e-133">Header</span><span class="sxs-lookup"><span data-stu-id="02a4e-133">Header</span></span> | <span data-ttu-id="02a4e-134">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="02a4e-134">string</span></span> | <span data-ttu-id="02a4e-135">ja</span><span class="sxs-lookup"><span data-stu-id="02a4e-135">yes</span></span>      | <span data-ttu-id="02a4e-136">Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="02a4e-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="02a4e-137">API-Schlüssel ist eine nicht transparente Zeichenfolge, aus der Paketquelle vom Benutzer erhalten und in den Client konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="02a4e-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="02a4e-138">Wird kein bestimmtes Zeichenfolgenformat beauftragt, aber der API-Schlüssel sollte nicht länger als eine angemessene Größe für HTTP-Header-Werte.</span><span class="sxs-lookup"><span data-stu-id="02a4e-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="02a4e-139">Anforderungstext</span><span class="sxs-lookup"><span data-stu-id="02a4e-139">Request body</span></span>

<span data-ttu-id="02a4e-140">Der Anforderungstext muss in der folgenden Form stammen:</span><span class="sxs-lookup"><span data-stu-id="02a4e-140">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="02a4e-141">Mehrteiligen Formulardaten.</span><span class="sxs-lookup"><span data-stu-id="02a4e-141">Multipart form data</span></span>

<span data-ttu-id="02a4e-142">Der Anforderungsheader `Content-Type` ist `multipart/form-data` und das erste Element im Hauptteil Anforderung ist, das die Rohdatenbytes, die von der NUPKG per Push übermittelt.</span><span class="sxs-lookup"><span data-stu-id="02a4e-142">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="02a4e-143">Nachfolgende Elemente in den mehrteiligen Text werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="02a4e-143">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="02a4e-144">Der Dateiname oder eventuelle weitere Header der mehrteiligen Elemente werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="02a4e-144">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="02a4e-145">Antwort</span><span class="sxs-lookup"><span data-stu-id="02a4e-145">Response</span></span>

<span data-ttu-id="02a4e-146">Statuscode</span><span class="sxs-lookup"><span data-stu-id="02a4e-146">Status Code</span></span> | <span data-ttu-id="02a4e-147">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="02a4e-147">Meaning</span></span>
----------- | -------
<span data-ttu-id="02a4e-148">201, 202</span><span class="sxs-lookup"><span data-stu-id="02a4e-148">201, 202</span></span>    | <span data-ttu-id="02a4e-149">Das Paket wurde erfolgreich übertragen.</span><span class="sxs-lookup"><span data-stu-id="02a4e-149">The package was successfully pushed</span></span>
<span data-ttu-id="02a4e-150">400</span><span class="sxs-lookup"><span data-stu-id="02a4e-150">400</span></span>         | <span data-ttu-id="02a4e-151">Das bereitgestellte Paket ist ungültig</span><span class="sxs-lookup"><span data-stu-id="02a4e-151">The provided package is invalid</span></span>
<span data-ttu-id="02a4e-152">409</span><span class="sxs-lookup"><span data-stu-id="02a4e-152">409</span></span>         | <span data-ttu-id="02a4e-153">Ein Paket mit der angegebenen ID und die Version ist bereits vorhanden.</span><span class="sxs-lookup"><span data-stu-id="02a4e-153">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="02a4e-154">Serverimplementierungen unterscheiden sich auf dem Erfolgsstatuscode zurückgegeben, wenn ein Paket erfolgreich übertragen wird.</span><span class="sxs-lookup"><span data-stu-id="02a4e-154">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="02a4e-155">Löschen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="02a4e-155">Delete a package</span></span>

<span data-ttu-id="02a4e-156">NuGet.org interpretiert die Paket-Delete-Anforderung als ein "Benutzerauswahl".</span><span class="sxs-lookup"><span data-stu-id="02a4e-156">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="02a4e-157">Dies bedeutet, dass das Paket für vorhandene Consumer des Pakets weiterhin verfügbar ist, aber das Paket nicht mehr angezeigt, in den Suchergebnissen oder in der Webschnittstelle wird.</span><span class="sxs-lookup"><span data-stu-id="02a4e-157">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="02a4e-158">Weitere Informationen zu dieser Vorgehensweise finden Sie unter der [Pakete gelöscht](../policies/deleting-packages.md) Richtlinie.</span><span class="sxs-lookup"><span data-stu-id="02a4e-158">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="02a4e-159">Andere serverimplementierungen sind frei, um dieses Signal als feste Löschvorgang interpretieren, vorläufigen löschen oder Benutzerauswahl.</span><span class="sxs-lookup"><span data-stu-id="02a4e-159">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="02a4e-160">Beispielsweise [NuGet.Server in](https://www.nuget.org/packages/NuGet.Server) (eine Server-Implementierung unterstützt nur die ältere V2-API) unterstützt diese Anforderung als ein Unlist oder ein hartes löschen, die basierend auf einer Konfigurationsoption behandeln.</span><span class="sxs-lookup"><span data-stu-id="02a4e-160">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="02a4e-161">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="02a4e-161">Request parameters</span></span>

<span data-ttu-id="02a4e-162">name</span><span class="sxs-lookup"><span data-stu-id="02a4e-162">Name</span></span>           | <span data-ttu-id="02a4e-163">In</span><span class="sxs-lookup"><span data-stu-id="02a4e-163">In</span></span>     | <span data-ttu-id="02a4e-164">Typ</span><span class="sxs-lookup"><span data-stu-id="02a4e-164">Type</span></span>   | <span data-ttu-id="02a4e-165">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="02a4e-165">Required</span></span> | <span data-ttu-id="02a4e-166">Hinweise</span><span class="sxs-lookup"><span data-stu-id="02a4e-166">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="02a4e-167">Id</span><span class="sxs-lookup"><span data-stu-id="02a4e-167">ID</span></span>             | <span data-ttu-id="02a4e-168">URL</span><span class="sxs-lookup"><span data-stu-id="02a4e-168">URL</span></span>    | <span data-ttu-id="02a4e-169">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="02a4e-169">string</span></span> | <span data-ttu-id="02a4e-170">ja</span><span class="sxs-lookup"><span data-stu-id="02a4e-170">yes</span></span>      | <span data-ttu-id="02a4e-171">Die ID des Pakets zu löschenden</span><span class="sxs-lookup"><span data-stu-id="02a4e-171">The ID of the package to delete</span></span>
<span data-ttu-id="02a4e-172">VERSION</span><span class="sxs-lookup"><span data-stu-id="02a4e-172">VERSION</span></span>        | <span data-ttu-id="02a4e-173">URL</span><span class="sxs-lookup"><span data-stu-id="02a4e-173">URL</span></span>    | <span data-ttu-id="02a4e-174">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="02a4e-174">string</span></span> | <span data-ttu-id="02a4e-175">ja</span><span class="sxs-lookup"><span data-stu-id="02a4e-175">yes</span></span>      | <span data-ttu-id="02a4e-176">Die Version des Pakets gelöscht</span><span class="sxs-lookup"><span data-stu-id="02a4e-176">The version of the package to delete</span></span>
<span data-ttu-id="02a4e-177">X-NuGet-"apikey"</span><span class="sxs-lookup"><span data-stu-id="02a4e-177">X-NuGet-ApiKey</span></span> | <span data-ttu-id="02a4e-178">Header</span><span class="sxs-lookup"><span data-stu-id="02a4e-178">Header</span></span> | <span data-ttu-id="02a4e-179">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="02a4e-179">string</span></span> | <span data-ttu-id="02a4e-180">ja</span><span class="sxs-lookup"><span data-stu-id="02a4e-180">yes</span></span>      | <span data-ttu-id="02a4e-181">Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="02a4e-181">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="02a4e-182">Antwort</span><span class="sxs-lookup"><span data-stu-id="02a4e-182">Response</span></span>

<span data-ttu-id="02a4e-183">Statuscode</span><span class="sxs-lookup"><span data-stu-id="02a4e-183">Status Code</span></span> | <span data-ttu-id="02a4e-184">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="02a4e-184">Meaning</span></span>
----------- | -------
<span data-ttu-id="02a4e-185">204</span><span class="sxs-lookup"><span data-stu-id="02a4e-185">204</span></span>         | <span data-ttu-id="02a4e-186">Das Paket wurde gelöscht.</span><span class="sxs-lookup"><span data-stu-id="02a4e-186">The package was deleted</span></span>
<span data-ttu-id="02a4e-187">404</span><span class="sxs-lookup"><span data-stu-id="02a4e-187">404</span></span>         | <span data-ttu-id="02a4e-188">Kein Paket mit dem angegebenen `ID` und `VERSION` vorhanden ist</span><span class="sxs-lookup"><span data-stu-id="02a4e-188">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="02a4e-189">Ein Paket wiedereinstellen</span><span class="sxs-lookup"><span data-stu-id="02a4e-189">Relist a package</span></span>

<span data-ttu-id="02a4e-190">Wenn ein Paket nicht aufgeführte ist, ist es möglich, das Paket erneut in den Suchergebnissen unter Verwendung des Endpunkts "Artikel" sichtbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="02a4e-190">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="02a4e-191">Dieser Endpunkt hat dieselbe Form wie die [löschen (Benutzerauswahl) Endpunkt](#delete-a-package) verwendet jedoch die `POST` HTTP-Methode der `DELETE` Methode.</span><span class="sxs-lookup"><span data-stu-id="02a4e-191">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="02a4e-192">Wenn das Paket bereits aufgeführt ist, wird die Anforderung trotzdem ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="02a4e-192">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="02a4e-193">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="02a4e-193">Request parameters</span></span>

<span data-ttu-id="02a4e-194">name</span><span class="sxs-lookup"><span data-stu-id="02a4e-194">Name</span></span>           | <span data-ttu-id="02a4e-195">In</span><span class="sxs-lookup"><span data-stu-id="02a4e-195">In</span></span>     | <span data-ttu-id="02a4e-196">Typ</span><span class="sxs-lookup"><span data-stu-id="02a4e-196">Type</span></span>   | <span data-ttu-id="02a4e-197">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="02a4e-197">Required</span></span> | <span data-ttu-id="02a4e-198">Hinweise</span><span class="sxs-lookup"><span data-stu-id="02a4e-198">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="02a4e-199">Id</span><span class="sxs-lookup"><span data-stu-id="02a4e-199">ID</span></span>             | <span data-ttu-id="02a4e-200">URL</span><span class="sxs-lookup"><span data-stu-id="02a4e-200">URL</span></span>    | <span data-ttu-id="02a4e-201">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="02a4e-201">string</span></span> | <span data-ttu-id="02a4e-202">ja</span><span class="sxs-lookup"><span data-stu-id="02a4e-202">yes</span></span>      | <span data-ttu-id="02a4e-203">Die ID des Pakets wiedereinstellen</span><span class="sxs-lookup"><span data-stu-id="02a4e-203">The ID of the package to relist</span></span>
<span data-ttu-id="02a4e-204">VERSION</span><span class="sxs-lookup"><span data-stu-id="02a4e-204">VERSION</span></span>        | <span data-ttu-id="02a4e-205">URL</span><span class="sxs-lookup"><span data-stu-id="02a4e-205">URL</span></span>    | <span data-ttu-id="02a4e-206">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="02a4e-206">string</span></span> | <span data-ttu-id="02a4e-207">ja</span><span class="sxs-lookup"><span data-stu-id="02a4e-207">yes</span></span>      | <span data-ttu-id="02a4e-208">Die Version des Pakets wiedereinstellen</span><span class="sxs-lookup"><span data-stu-id="02a4e-208">The version of the package to relist</span></span>
<span data-ttu-id="02a4e-209">X-NuGet-"apikey"</span><span class="sxs-lookup"><span data-stu-id="02a4e-209">X-NuGet-ApiKey</span></span> | <span data-ttu-id="02a4e-210">Header</span><span class="sxs-lookup"><span data-stu-id="02a4e-210">Header</span></span> | <span data-ttu-id="02a4e-211">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="02a4e-211">string</span></span> | <span data-ttu-id="02a4e-212">ja</span><span class="sxs-lookup"><span data-stu-id="02a4e-212">yes</span></span>      | <span data-ttu-id="02a4e-213">Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="02a4e-213">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="02a4e-214">Antwort</span><span class="sxs-lookup"><span data-stu-id="02a4e-214">Response</span></span>

<span data-ttu-id="02a4e-215">Statuscode</span><span class="sxs-lookup"><span data-stu-id="02a4e-215">Status Code</span></span> | <span data-ttu-id="02a4e-216">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="02a4e-216">Meaning</span></span>
----------- | -------
<span data-ttu-id="02a4e-217">204</span><span class="sxs-lookup"><span data-stu-id="02a4e-217">204</span></span>         | <span data-ttu-id="02a4e-218">Das Paket wird jetzt aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="02a4e-218">The package is now listed</span></span>
<span data-ttu-id="02a4e-219">404</span><span class="sxs-lookup"><span data-stu-id="02a4e-219">404</span></span>         | <span data-ttu-id="02a4e-220">Kein Paket mit dem angegebenen `ID` und `VERSION` vorhanden ist</span><span class="sxs-lookup"><span data-stu-id="02a4e-220">No package with the provided `ID` and `VERSION` exists</span></span>
