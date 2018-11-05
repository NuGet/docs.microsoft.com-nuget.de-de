---
title: nuget.org-Protokolle
description: Die sich entwickelnden Protokolle bei nuget.org für die Interaktion mit NuGet-Clients.
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547272"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="752da-103">nuget.org-Protokolle</span><span class="sxs-lookup"><span data-stu-id="752da-103">nuget.org protocols</span></span>

<span data-ttu-id="752da-104">Zum Interagieren mit nuget.org müssen Clients bestimmte Protokolle nutzen.</span><span class="sxs-lookup"><span data-stu-id="752da-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="752da-105">Da diese Protokolle sich immer weiterentwickeln, müssen Clients die von ihnen genutzte Protokollversion angeben, wenn sie bestimmte nuget.org-APIs aufrufen.</span><span class="sxs-lookup"><span data-stu-id="752da-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="752da-106">Dadurch kann nuget.org Änderungen einführen und mit alten Clients kompatibel bleiben.</span><span class="sxs-lookup"><span data-stu-id="752da-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="752da-107">Die hier dokumentierten APIs sind spezifisch für nuget.org, und es wird von anderen NuGet-Serverimplementierungen nicht erwartet, dass sie diese APIs einführen.</span><span class="sxs-lookup"><span data-stu-id="752da-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="752da-108">Weitere Informationen zur NuGet-API, die im NuGet-Ökosystem weitgehend implementiert ist, finden Sie in der [API-Übersicht](overview.md).</span><span class="sxs-lookup"><span data-stu-id="752da-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="752da-109">Dieses Thema listet verschiedene Protokolle auf, sobald diese eingeführt werden.</span><span class="sxs-lookup"><span data-stu-id="752da-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="752da-110">NuGet-Protokoll, Version 4.1.0</span><span class="sxs-lookup"><span data-stu-id="752da-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="752da-111">Die 4.1.0 Protokoll gibt an, die Nutzung der überprüfen-Scope-Schlüssel für die Interaktion mit anderen Diensten als "NuGet.org", um ein Paket mit einem nuget.org-Konto zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="752da-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="752da-112">Beachten Sie, dass die `4.1.0` Version ist eine nicht transparente Zeichenfolge wurden jedoch zufällig mit der ersten Version des offiziellen NuGet-Clients übereinstimmen, die dieses Protokoll unterstützt.</span><span class="sxs-lookup"><span data-stu-id="752da-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="752da-113">Überprüfung wird sichergestellt, dass der Benutzer erstellte API-Schlüssel werden nur mit nuget.org verwendet, und diese anderen der Überprüfung oder der Überprüfung von einem Drittanbieter-Dienst über eine einmalige Verwendung überprüfen-Scope-Schlüssel erfolgt.</span><span class="sxs-lookup"><span data-stu-id="752da-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="752da-114">Diese überprüfen-Scope-Schlüssel können verwendet werden, um sicherzustellen, dass das Paket an einen bestimmten Benutzer (Konto), die auf nuget.org gehört.</span><span class="sxs-lookup"><span data-stu-id="752da-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="752da-115">Client-Anforderung</span><span class="sxs-lookup"><span data-stu-id="752da-115">Client requirement</span></span>

<span data-ttu-id="752da-116">Clients müssen die folgenden Header übergeben werden soll, wenn sie API-Aufrufen **Push** Pakete auf nuget.org:</span><span class="sxs-lookup"><span data-stu-id="752da-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

    X-NuGet-Protocol-Version: 4.1.0

<span data-ttu-id="752da-117">Beachten Sie, dass der Header `X-NuGet-Client-Version` eine ähnliche Semantik benutzt, aber für die ausschließliche Nutzung durch den offiziellen NuGet-Client vorgesehen ist.</span><span class="sxs-lookup"><span data-stu-id="752da-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="752da-118">Clients von Drittanbietern sollten den Header und Wert `X-NuGet-Protocol-Version` nutzen.</span><span class="sxs-lookup"><span data-stu-id="752da-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="752da-119">Das **Push**-Protokoll selbst wird in der Dokumentation für die [`PackagePublish`-Ressource](package-publish-resource.md) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="752da-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="752da-120">Wenn ein Client mit externen Diensten und Anforderungen interagiert und überprüfen muss, ob ein Paket einem bestimmten Benutzer (Konto) gehört, sollte er das folgende Protokoll und die "Verify Scope"-Schlüssel, nicht die API-Schlüssel von nuget.org, verwenden.</span><span class="sxs-lookup"><span data-stu-id="752da-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="752da-121">API, um einen "Verify Scope"-Schlüssel anzufordern</span><span class="sxs-lookup"><span data-stu-id="752da-121">API to request a verify-scope key</span></span>

<span data-ttu-id="752da-122">Diese API wird genutzt, um einen "Verify Scope"-Schlüssel anzufordern, damit ein nuget.org-Autor ein Paket validieren kann, das ihm/ihr gehört.</span><span class="sxs-lookup"><span data-stu-id="752da-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="752da-123">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="752da-123">Request parameters</span></span>

<span data-ttu-id="752da-124">Name</span><span class="sxs-lookup"><span data-stu-id="752da-124">Name</span></span>           | <span data-ttu-id="752da-125">In</span><span class="sxs-lookup"><span data-stu-id="752da-125">In</span></span>     | <span data-ttu-id="752da-126">Typ</span><span class="sxs-lookup"><span data-stu-id="752da-126">Type</span></span>   | <span data-ttu-id="752da-127">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="752da-127">Required</span></span> | <span data-ttu-id="752da-128">Hinweise</span><span class="sxs-lookup"><span data-stu-id="752da-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="752da-129">ID</span><span class="sxs-lookup"><span data-stu-id="752da-129">ID</span></span>             | <span data-ttu-id="752da-130">URL</span><span class="sxs-lookup"><span data-stu-id="752da-130">URL</span></span>    | <span data-ttu-id="752da-131">String</span><span class="sxs-lookup"><span data-stu-id="752da-131">string</span></span> | <span data-ttu-id="752da-132">ja</span><span class="sxs-lookup"><span data-stu-id="752da-132">yes</span></span>      | <span data-ttu-id="752da-133">Die Paket-ID, für die der Schlüssel angefordert wird</span><span class="sxs-lookup"><span data-stu-id="752da-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="752da-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="752da-134">VERSION</span></span>        | <span data-ttu-id="752da-135">URL</span><span class="sxs-lookup"><span data-stu-id="752da-135">URL</span></span>    | <span data-ttu-id="752da-136">String</span><span class="sxs-lookup"><span data-stu-id="752da-136">string</span></span> | <span data-ttu-id="752da-137">nein</span><span class="sxs-lookup"><span data-stu-id="752da-137">no</span></span>       | <span data-ttu-id="752da-138">Die Paketversion</span><span class="sxs-lookup"><span data-stu-id="752da-138">The package version</span></span>
<span data-ttu-id="752da-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="752da-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="752da-140">Header</span><span class="sxs-lookup"><span data-stu-id="752da-140">Header</span></span> | <span data-ttu-id="752da-141">String</span><span class="sxs-lookup"><span data-stu-id="752da-141">string</span></span> | <span data-ttu-id="752da-142">ja</span><span class="sxs-lookup"><span data-stu-id="752da-142">yes</span></span>      | <span data-ttu-id="752da-143">beispielsweise `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="752da-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="752da-144">Antwort</span><span class="sxs-lookup"><span data-stu-id="752da-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="752da-145">API, um den "Verify Scope"-Schlüssel zu überprüfen</span><span class="sxs-lookup"><span data-stu-id="752da-145">API to verify the verify scope key</span></span>

<span data-ttu-id="752da-146">Diese API wird verwendet, um einen "Verify Scope"-Schlüssel für ein Paket zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="752da-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="752da-147">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="752da-147">Request parameters</span></span>

<span data-ttu-id="752da-148">name</span><span class="sxs-lookup"><span data-stu-id="752da-148">Name</span></span>           | <span data-ttu-id="752da-149">In</span><span class="sxs-lookup"><span data-stu-id="752da-149">In</span></span>     | <span data-ttu-id="752da-150">Typ</span><span class="sxs-lookup"><span data-stu-id="752da-150">Type</span></span>   | <span data-ttu-id="752da-151">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="752da-151">Required</span></span> | <span data-ttu-id="752da-152">Hinweise</span><span class="sxs-lookup"><span data-stu-id="752da-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="752da-153">Id</span><span class="sxs-lookup"><span data-stu-id="752da-153">ID</span></span>             | <span data-ttu-id="752da-154">URL</span><span class="sxs-lookup"><span data-stu-id="752da-154">URL</span></span>    | <span data-ttu-id="752da-155">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="752da-155">string</span></span> | <span data-ttu-id="752da-156">ja</span><span class="sxs-lookup"><span data-stu-id="752da-156">yes</span></span>      | <span data-ttu-id="752da-157">Die Paket-ID für die der Schlüssel des überprüfen Bereich angefordert wird</span><span class="sxs-lookup"><span data-stu-id="752da-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="752da-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="752da-158">VERSION</span></span>        | <span data-ttu-id="752da-159">URL</span><span class="sxs-lookup"><span data-stu-id="752da-159">URL</span></span>    | <span data-ttu-id="752da-160">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="752da-160">string</span></span> | <span data-ttu-id="752da-161">Nein</span><span class="sxs-lookup"><span data-stu-id="752da-161">no</span></span>       | <span data-ttu-id="752da-162">Die Paketversion</span><span class="sxs-lookup"><span data-stu-id="752da-162">The package version</span></span>
<span data-ttu-id="752da-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="752da-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="752da-164">Header</span><span class="sxs-lookup"><span data-stu-id="752da-164">Header</span></span> | <span data-ttu-id="752da-165">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="752da-165">string</span></span> | <span data-ttu-id="752da-166">ja</span><span class="sxs-lookup"><span data-stu-id="752da-166">yes</span></span>      | <span data-ttu-id="752da-167">Beispiel: `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="752da-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="752da-168">Dieser "Verify Scope"-Schlüssel läuft nach einem Tag oder der ersten Nutzung ab.</span><span class="sxs-lookup"><span data-stu-id="752da-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="752da-169">Antwort</span><span class="sxs-lookup"><span data-stu-id="752da-169">Response</span></span>

<span data-ttu-id="752da-170">Statuscode</span><span class="sxs-lookup"><span data-stu-id="752da-170">Status Code</span></span> | <span data-ttu-id="752da-171">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="752da-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="752da-172">200</span><span class="sxs-lookup"><span data-stu-id="752da-172">200</span></span>         | <span data-ttu-id="752da-173">Der API-Schlüssel ist gültig.</span><span class="sxs-lookup"><span data-stu-id="752da-173">The API key is valid</span></span>
<span data-ttu-id="752da-174">403</span><span class="sxs-lookup"><span data-stu-id="752da-174">403</span></span>         | <span data-ttu-id="752da-175">Der API-Schlüssel ist ungültig oder für dieses Paket nicht autorisiert</span><span class="sxs-lookup"><span data-stu-id="752da-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="752da-176">404</span><span class="sxs-lookup"><span data-stu-id="752da-176">404</span></span>         | <span data-ttu-id="752da-177">Das Paket, das mit `ID` und (optional) `VERSION` angegeben wurde, existiert nicht</span><span class="sxs-lookup"><span data-stu-id="752da-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
