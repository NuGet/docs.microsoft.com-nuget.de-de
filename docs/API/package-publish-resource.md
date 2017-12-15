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
ms.openlocfilehash: 1fa3c0e1698a11208d9ef29fdf26a4980cb60cf5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="push-and-delete"></a><span data-ttu-id="077b9-104">Push-als auch löschen</span><span class="sxs-lookup"><span data-stu-id="077b9-104">Push and Delete</span></span>

<span data-ttu-id="077b9-105">Es ist möglich, mithilfe von Push übertragen, und löschen (oder Benutzerauswahl, je nach serverimplementierung)-Pakete mit der NuGet-V3-API.</span><span class="sxs-lookup"><span data-stu-id="077b9-105">It is possible to push and delete (or unlist, depending on the server implementation) packages using the NuGet V3 API.</span></span>
<span data-ttu-id="077b9-106">Beide Vorgänge basieren, der die `PackagePublish` Ressource gefunden, der [Dienst Index](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="077b9-106">Both operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="077b9-107">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="077b9-107">Versioning</span></span>

<span data-ttu-id="077b9-108">Die folgenden `@type` Wert wird verwendet:</span><span class="sxs-lookup"><span data-stu-id="077b9-108">The following `@type` value is used:</span></span>

<span data-ttu-id="077b9-109">@type-Wert</span><span class="sxs-lookup"><span data-stu-id="077b9-109">@type value</span></span>          | <span data-ttu-id="077b9-110">Hinweise</span><span class="sxs-lookup"><span data-stu-id="077b9-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="077b9-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="077b9-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="077b9-112">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="077b9-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="077b9-113">Basis-URL</span><span class="sxs-lookup"><span data-stu-id="077b9-113">Base URL</span></span>

<span data-ttu-id="077b9-114">Die base-URL für die folgenden APIs ist der Wert des der `@id` Eigenschaft von der `PackagePublish/2.0.0` Ressource in der Paketquelle [Dienst Index](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="077b9-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="077b9-115">Die Dokumentation wird sich der Nuget.org-URL verwendet.</span><span class="sxs-lookup"><span data-stu-id="077b9-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="077b9-116">Betrachten Sie `https://www.nuget.org/api/v2/package` als Platzhalter für die `@id` Wert in der Service-Index gefunden.</span><span class="sxs-lookup"><span data-stu-id="077b9-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="077b9-117">Beachten Sie, dass diese URL verweist auf am gleichen Speicherort wie die ältere V2-Push-Endpunkt auf, da das Protokoll identisch ist.</span><span class="sxs-lookup"><span data-stu-id="077b9-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="077b9-118">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="077b9-118">HTTP methods</span></span>

<span data-ttu-id="077b9-119">Die `PUT` und `DELETE` HTTP-Methoden werden durch diese Ressource unterstützt.</span><span class="sxs-lookup"><span data-stu-id="077b9-119">The `PUT` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="077b9-120">Welche Methoden für jeden Endpunkt unterstützt werden finden Sie weiter unten.</span><span class="sxs-lookup"><span data-stu-id="077b9-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="077b9-121">Ein Paket mithilfe von Push übertragen</span><span class="sxs-lookup"><span data-stu-id="077b9-121">Push a package</span></span>

<span data-ttu-id="077b9-122">NuGet.org unterstützt, wie neue Pakete, die mithilfe der folgenden-API.</span><span class="sxs-lookup"><span data-stu-id="077b9-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="077b9-123">Wenn das Paket mit der angegebenen ID und die Version bereits vorhanden ist, lehnt nuget.org der Push-Vorgang.</span><span class="sxs-lookup"><span data-stu-id="077b9-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="077b9-124">Andere Paketquellen unterstützen möglicherweise das Ersetzen eines vorhandenen Pakets.</span><span class="sxs-lookup"><span data-stu-id="077b9-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="077b9-125">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="077b9-125">Request parameters</span></span>

<span data-ttu-id="077b9-126">Name</span><span class="sxs-lookup"><span data-stu-id="077b9-126">Name</span></span>           | <span data-ttu-id="077b9-127">In</span><span class="sxs-lookup"><span data-stu-id="077b9-127">In</span></span>     | <span data-ttu-id="077b9-128">Typ</span><span class="sxs-lookup"><span data-stu-id="077b9-128">Type</span></span>   | <span data-ttu-id="077b9-129">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="077b9-129">Required</span></span> | <span data-ttu-id="077b9-130">Hinweise</span><span class="sxs-lookup"><span data-stu-id="077b9-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="077b9-131">X-NuGet-"apikey"</span><span class="sxs-lookup"><span data-stu-id="077b9-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="077b9-132">Header</span><span class="sxs-lookup"><span data-stu-id="077b9-132">Header</span></span> | <span data-ttu-id="077b9-133">string</span><span class="sxs-lookup"><span data-stu-id="077b9-133">string</span></span> | <span data-ttu-id="077b9-134">ja</span><span class="sxs-lookup"><span data-stu-id="077b9-134">yes</span></span>      | <span data-ttu-id="077b9-135">Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="077b9-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="077b9-136">API-Schlüssel ist eine nicht transparente Zeichenfolge, aus der Paketquelle vom Benutzer erhalten und in den Client konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="077b9-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="077b9-137">Wird kein bestimmtes Zeichenfolgenformat beauftragt, aber der API-Schlüssel sollte nicht länger als eine angemessene Größe für HTTP-Header-Werte.</span><span class="sxs-lookup"><span data-stu-id="077b9-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="077b9-138">Anforderungstext</span><span class="sxs-lookup"><span data-stu-id="077b9-138">Request body</span></span>

<span data-ttu-id="077b9-139">Der Anforderungstext muss in der folgenden Form stammen:</span><span class="sxs-lookup"><span data-stu-id="077b9-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="077b9-140">Mehrteiligen Formulardaten.</span><span class="sxs-lookup"><span data-stu-id="077b9-140">Multipart form data</span></span>

<span data-ttu-id="077b9-141">Der Anforderungsheader `Content-Type` ist `multipart/form-data` und das erste Element im Hauptteil Anforderung ist, das die Rohdatenbytes, die von der NUPKG per Push übermittelt.</span><span class="sxs-lookup"><span data-stu-id="077b9-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="077b9-142">Nachfolgende Elemente in den mehrteiligen Text werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="077b9-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="077b9-143">Der Dateiname oder eventuelle weitere Header der mehrteiligen Elemente werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="077b9-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="077b9-144">Antwort</span><span class="sxs-lookup"><span data-stu-id="077b9-144">Response</span></span>

<span data-ttu-id="077b9-145">Statuscode</span><span class="sxs-lookup"><span data-stu-id="077b9-145">Status Code</span></span> | <span data-ttu-id="077b9-146">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="077b9-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="077b9-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="077b9-147">201, 202</span></span>    | <span data-ttu-id="077b9-148">Das Paket wurde erfolgreich übertragen.</span><span class="sxs-lookup"><span data-stu-id="077b9-148">The package was successfully pushed</span></span>
<span data-ttu-id="077b9-149">400</span><span class="sxs-lookup"><span data-stu-id="077b9-149">400</span></span>         | <span data-ttu-id="077b9-150">Das bereitgestellte Paket ist ungültig</span><span class="sxs-lookup"><span data-stu-id="077b9-150">The provided package is invalid</span></span>
<span data-ttu-id="077b9-151">409</span><span class="sxs-lookup"><span data-stu-id="077b9-151">409</span></span>         | <span data-ttu-id="077b9-152">Ein Paket mit der angegebenen ID und die Version ist bereits vorhanden.</span><span class="sxs-lookup"><span data-stu-id="077b9-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="077b9-153">Serverimplementierungen unterscheiden sich auf dem Erfolgsstatuscode zurückgegeben, wenn ein Paket erfolgreich übertragen wird.</span><span class="sxs-lookup"><span data-stu-id="077b9-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="077b9-154">Löschen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="077b9-154">Delete a package</span></span>

<span data-ttu-id="077b9-155">NuGet.org interpretiert die Paket-Delete-Anforderung als ein "Benutzerauswahl".</span><span class="sxs-lookup"><span data-stu-id="077b9-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="077b9-156">Dies bedeutet, dass das Paket für vorhandene Consumer des Pakets weiterhin verfügbar ist, aber das Paket nicht mehr angezeigt, in den Suchergebnissen oder in der Webschnittstelle wird.</span><span class="sxs-lookup"><span data-stu-id="077b9-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="077b9-157">Weitere Informationen zu dieser Vorgehensweise finden Sie unter der [Pakete gelöscht](../policies/deleting-packages.md) Richtlinie.</span><span class="sxs-lookup"><span data-stu-id="077b9-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="077b9-158">Andere serverimplementierungen sind frei, um dieses Signal als feste Löschvorgang interpretieren, vorläufigen löschen oder Benutzerauswahl.</span><span class="sxs-lookup"><span data-stu-id="077b9-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="077b9-159">Beispielsweise [NuGet.Server in](https://www.nuget.org/packages/NuGet.Server) (eine Server-Implementierung unterstützt nur die ältere V2-API) unterstützt diese Anforderung als ein Unlist oder ein hartes löschen, die basierend auf einer Konfigurationsoption behandeln.</span><span class="sxs-lookup"><span data-stu-id="077b9-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="077b9-160">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="077b9-160">Request parameters</span></span>

<span data-ttu-id="077b9-161">Name</span><span class="sxs-lookup"><span data-stu-id="077b9-161">Name</span></span>           | <span data-ttu-id="077b9-162">In</span><span class="sxs-lookup"><span data-stu-id="077b9-162">In</span></span>     | <span data-ttu-id="077b9-163">Typ</span><span class="sxs-lookup"><span data-stu-id="077b9-163">Type</span></span>   | <span data-ttu-id="077b9-164">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="077b9-164">Required</span></span> | <span data-ttu-id="077b9-165">Hinweise</span><span class="sxs-lookup"><span data-stu-id="077b9-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="077b9-166">ID</span><span class="sxs-lookup"><span data-stu-id="077b9-166">ID</span></span>             | <span data-ttu-id="077b9-167">URL</span><span class="sxs-lookup"><span data-stu-id="077b9-167">URL</span></span>    | <span data-ttu-id="077b9-168">string</span><span class="sxs-lookup"><span data-stu-id="077b9-168">string</span></span> | <span data-ttu-id="077b9-169">ja</span><span class="sxs-lookup"><span data-stu-id="077b9-169">yes</span></span>      | <span data-ttu-id="077b9-170">Die ID des Pakets zu löschenden</span><span class="sxs-lookup"><span data-stu-id="077b9-170">The ID of the package to delete</span></span>
<span data-ttu-id="077b9-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="077b9-171">VERSION</span></span>        | <span data-ttu-id="077b9-172">URL</span><span class="sxs-lookup"><span data-stu-id="077b9-172">URL</span></span>    | <span data-ttu-id="077b9-173">string</span><span class="sxs-lookup"><span data-stu-id="077b9-173">string</span></span> | <span data-ttu-id="077b9-174">ja</span><span class="sxs-lookup"><span data-stu-id="077b9-174">yes</span></span>      | <span data-ttu-id="077b9-175">Die Version des Pakets gelöscht</span><span class="sxs-lookup"><span data-stu-id="077b9-175">The version of the package to delete</span></span>
<span data-ttu-id="077b9-176">X-NuGet-"apikey"</span><span class="sxs-lookup"><span data-stu-id="077b9-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="077b9-177">Header</span><span class="sxs-lookup"><span data-stu-id="077b9-177">Header</span></span> | <span data-ttu-id="077b9-178">string</span><span class="sxs-lookup"><span data-stu-id="077b9-178">string</span></span> | <span data-ttu-id="077b9-179">ja</span><span class="sxs-lookup"><span data-stu-id="077b9-179">yes</span></span>      | <span data-ttu-id="077b9-180">Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="077b9-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="077b9-181">Antwort</span><span class="sxs-lookup"><span data-stu-id="077b9-181">Response</span></span>

<span data-ttu-id="077b9-182">Statuscode</span><span class="sxs-lookup"><span data-stu-id="077b9-182">Status Code</span></span> | <span data-ttu-id="077b9-183">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="077b9-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="077b9-184">204</span><span class="sxs-lookup"><span data-stu-id="077b9-184">204</span></span>         | <span data-ttu-id="077b9-185">Das Paket wurde gelöscht.</span><span class="sxs-lookup"><span data-stu-id="077b9-185">The package was deleted</span></span>
<span data-ttu-id="077b9-186">404</span><span class="sxs-lookup"><span data-stu-id="077b9-186">404</span></span>         | <span data-ttu-id="077b9-187">Kein Paket mit dem angegebenen `ID` und `VERSION` vorhanden ist</span><span class="sxs-lookup"><span data-stu-id="077b9-187">No package with the provided `ID` and `VERSION` exists</span></span>
