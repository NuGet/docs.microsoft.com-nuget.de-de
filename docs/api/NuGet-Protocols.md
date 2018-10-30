---
title: "\"NuGet.org\"-Protokolle"
description: Der sich entwickelnden "nuget.org"-Protokolle für die Interaktion mit NuGet-Clients.
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
# <a name="nugetorg-protocols"></a><span data-ttu-id="8717b-103">"NuGet.org"-Protokolle</span><span class="sxs-lookup"><span data-stu-id="8717b-103">nuget.org protocols</span></span>

<span data-ttu-id="8717b-104">Zum interagieren mit nuget.org müssen Sie bestimmte Protokolle zu folgen.</span><span class="sxs-lookup"><span data-stu-id="8717b-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="8717b-105">Da diese Protokolle Weiterentwicklung zu halten, müssen Clients die Version des Protokolls identifizieren nutzen, wenn bestimmte nuget.org APIs aufrufen.</span><span class="sxs-lookup"><span data-stu-id="8717b-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="8717b-106">Dadurch wird ein "NuGet.org", um die Änderungen auf eine nicht unterbrechende Weise eingeführt werden, für die alten Clients.</span><span class="sxs-lookup"><span data-stu-id="8717b-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="8717b-107">Auf dieser Seite dokumentierten APIs beziehen sich auf nuget.org aus, und es gibt keine Erwartungen an andere NuGet-Server-Implementierungen diese APIs einführen.</span><span class="sxs-lookup"><span data-stu-id="8717b-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="8717b-108">Weitere Informationen über die NuGet-API, die allgemein für die NuGet-Ökosystem implementiert, finden Sie unter den [-API – Übersicht](overview.md).</span><span class="sxs-lookup"><span data-stu-id="8717b-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="8717b-109">Dieses Thema enthält verschiedene Protokolle wie und wann sie zu Vorhandensein stammen.</span><span class="sxs-lookup"><span data-stu-id="8717b-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="8717b-110">NuGet Protocol, Version 4.1.0</span><span class="sxs-lookup"><span data-stu-id="8717b-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="8717b-111">Die 4.1.0 Protokoll gibt an, die Nutzung der überprüfen-Scope-Schlüssel für die Interaktion mit anderen Diensten als "NuGet.org", um ein Paket mit einem nuget.org-Konto zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="8717b-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="8717b-112">Beachten Sie, dass die `4.1.0` Version ist eine nicht transparente Zeichenfolge wurden jedoch zufällig mit der ersten Version des offiziellen NuGet-Clients übereinstimmen, die dieses Protokoll unterstützt.</span><span class="sxs-lookup"><span data-stu-id="8717b-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="8717b-113">Überprüfung wird sichergestellt, dass der Benutzer erstellte API-Schlüssel werden nur mit nuget.org verwendet, und diese anderen der Überprüfung oder der Überprüfung von einem Drittanbieter-Dienst über eine einmalige Verwendung überprüfen-Scope-Schlüssel erfolgt.</span><span class="sxs-lookup"><span data-stu-id="8717b-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="8717b-114">Diese überprüfen-Scope-Schlüssel können verwendet werden, um sicherzustellen, dass das Paket an einen bestimmten Benutzer (Konto), die auf nuget.org gehört.</span><span class="sxs-lookup"><span data-stu-id="8717b-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="8717b-115">Client-Anforderung</span><span class="sxs-lookup"><span data-stu-id="8717b-115">Client requirement</span></span>

<span data-ttu-id="8717b-116">Clients müssen die folgenden Header übergeben werden soll, wenn sie API-Aufrufen **Push** Pakete auf nuget.org:</span><span class="sxs-lookup"><span data-stu-id="8717b-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

    X-NuGet-Protocol-Version: 4.1.0

<span data-ttu-id="8717b-117">Beachten Sie, dass die `X-NuGet-Client-Version` Header weist eine ähnliche Semantik, sondern wird reserviert, um nur von der offiziellen NuGet-Client verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="8717b-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="8717b-118">Clients von Drittanbietern verwenden, sollten die `X-NuGet-Protocol-Version` Header und Wert.</span><span class="sxs-lookup"><span data-stu-id="8717b-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="8717b-119">Die **Push** Protokoll selbst wird beschrieben, in der Dokumentation für die [ `PackagePublish` Ressource](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="8717b-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="8717b-120">Wenn ein Client mit externen Diensten und Anforderungen interagiert zu prüfen, ob ein Paket zu einem bestimmten Benutzer (Konto) gehört, muss das folgende Protokoll verwenden und überprüfen-Scope-Schlüssel und nicht die API-Schlüssel von nuget.org verwenden.</span><span class="sxs-lookup"><span data-stu-id="8717b-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="8717b-121">-API, um einen Bereich überprüfen Schlüssel anfordern</span><span class="sxs-lookup"><span data-stu-id="8717b-121">API to request a verify-scope key</span></span>

<span data-ttu-id="8717b-122">Abrufen eines Schlüssels überprüfen-Bereich für den Autor eines "NuGet.org", um ein Paket, das im Besitz von eines Gastbenutzers zu überprüfen, wird diese API verwendet.</span><span class="sxs-lookup"><span data-stu-id="8717b-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="8717b-123">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="8717b-123">Request parameters</span></span>

<span data-ttu-id="8717b-124">name</span><span class="sxs-lookup"><span data-stu-id="8717b-124">Name</span></span>           | <span data-ttu-id="8717b-125">In</span><span class="sxs-lookup"><span data-stu-id="8717b-125">In</span></span>     | <span data-ttu-id="8717b-126">Typ</span><span class="sxs-lookup"><span data-stu-id="8717b-126">Type</span></span>   | <span data-ttu-id="8717b-127">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="8717b-127">Required</span></span> | <span data-ttu-id="8717b-128">Hinweise</span><span class="sxs-lookup"><span data-stu-id="8717b-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="8717b-129">Id</span><span class="sxs-lookup"><span data-stu-id="8717b-129">ID</span></span>             | <span data-ttu-id="8717b-130">URL</span><span class="sxs-lookup"><span data-stu-id="8717b-130">URL</span></span>    | <span data-ttu-id="8717b-131">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="8717b-131">string</span></span> | <span data-ttu-id="8717b-132">ja</span><span class="sxs-lookup"><span data-stu-id="8717b-132">yes</span></span>      | <span data-ttu-id="8717b-133">Die Paket-Identidier für die der Schlüssel des überprüfen Bereich angefordert wird</span><span class="sxs-lookup"><span data-stu-id="8717b-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="8717b-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="8717b-134">VERSION</span></span>        | <span data-ttu-id="8717b-135">URL</span><span class="sxs-lookup"><span data-stu-id="8717b-135">URL</span></span>    | <span data-ttu-id="8717b-136">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="8717b-136">string</span></span> | <span data-ttu-id="8717b-137">Nein</span><span class="sxs-lookup"><span data-stu-id="8717b-137">no</span></span>       | <span data-ttu-id="8717b-138">Die Paketversion</span><span class="sxs-lookup"><span data-stu-id="8717b-138">The package version</span></span>
<span data-ttu-id="8717b-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="8717b-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="8717b-140">Header</span><span class="sxs-lookup"><span data-stu-id="8717b-140">Header</span></span> | <span data-ttu-id="8717b-141">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="8717b-141">string</span></span> | <span data-ttu-id="8717b-142">ja</span><span class="sxs-lookup"><span data-stu-id="8717b-142">yes</span></span>      | <span data-ttu-id="8717b-143">Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="8717b-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="8717b-144">Antwort</span><span class="sxs-lookup"><span data-stu-id="8717b-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="8717b-145">API, um zu überprüfen, ob den Schlüssel der überprüfen-Bereich</span><span class="sxs-lookup"><span data-stu-id="8717b-145">API to verify the verify scope key</span></span>

<span data-ttu-id="8717b-146">Diese API wird verwendet, um überprüfen-Scope-Schlüssel für der Autor von "NuGet.org" gehörige Paket zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="8717b-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="8717b-147">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="8717b-147">Request parameters</span></span>

<span data-ttu-id="8717b-148">name</span><span class="sxs-lookup"><span data-stu-id="8717b-148">Name</span></span>           | <span data-ttu-id="8717b-149">In</span><span class="sxs-lookup"><span data-stu-id="8717b-149">In</span></span>     | <span data-ttu-id="8717b-150">Typ</span><span class="sxs-lookup"><span data-stu-id="8717b-150">Type</span></span>   | <span data-ttu-id="8717b-151">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="8717b-151">Required</span></span> | <span data-ttu-id="8717b-152">Hinweise</span><span class="sxs-lookup"><span data-stu-id="8717b-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="8717b-153">Id</span><span class="sxs-lookup"><span data-stu-id="8717b-153">ID</span></span>             | <span data-ttu-id="8717b-154">URL</span><span class="sxs-lookup"><span data-stu-id="8717b-154">URL</span></span>    | <span data-ttu-id="8717b-155">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="8717b-155">string</span></span> | <span data-ttu-id="8717b-156">ja</span><span class="sxs-lookup"><span data-stu-id="8717b-156">yes</span></span>      | <span data-ttu-id="8717b-157">Die Paket-ID für die der Schlüssel des überprüfen Bereich angefordert wird</span><span class="sxs-lookup"><span data-stu-id="8717b-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="8717b-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="8717b-158">VERSION</span></span>        | <span data-ttu-id="8717b-159">URL</span><span class="sxs-lookup"><span data-stu-id="8717b-159">URL</span></span>    | <span data-ttu-id="8717b-160">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="8717b-160">string</span></span> | <span data-ttu-id="8717b-161">Nein</span><span class="sxs-lookup"><span data-stu-id="8717b-161">no</span></span>       | <span data-ttu-id="8717b-162">Die Paketversion</span><span class="sxs-lookup"><span data-stu-id="8717b-162">The package version</span></span>
<span data-ttu-id="8717b-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="8717b-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="8717b-164">Header</span><span class="sxs-lookup"><span data-stu-id="8717b-164">Header</span></span> | <span data-ttu-id="8717b-165">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="8717b-165">string</span></span> | <span data-ttu-id="8717b-166">ja</span><span class="sxs-lookup"><span data-stu-id="8717b-166">yes</span></span>      | <span data-ttu-id="8717b-167">Beispiel: `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="8717b-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="8717b-168">Dieser Bereich API-Schlüssel stellen Sie sicher, die in einen ganzen Tag läuft ab, oder bei der ersten Verwendung, welcher Fall zuerst eintritt.</span><span class="sxs-lookup"><span data-stu-id="8717b-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="8717b-169">Antwort</span><span class="sxs-lookup"><span data-stu-id="8717b-169">Response</span></span>

<span data-ttu-id="8717b-170">Statuscode</span><span class="sxs-lookup"><span data-stu-id="8717b-170">Status Code</span></span> | <span data-ttu-id="8717b-171">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="8717b-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="8717b-172">200</span><span class="sxs-lookup"><span data-stu-id="8717b-172">200</span></span>         | <span data-ttu-id="8717b-173">Der API-Schlüssel ist gültig.</span><span class="sxs-lookup"><span data-stu-id="8717b-173">The API key is valid</span></span>
<span data-ttu-id="8717b-174">403</span><span class="sxs-lookup"><span data-stu-id="8717b-174">403</span></span>         | <span data-ttu-id="8717b-175">Der API-Schlüssel ist ungültig oder für dieses Paket nicht autorisiert</span><span class="sxs-lookup"><span data-stu-id="8717b-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="8717b-176">404</span><span class="sxs-lookup"><span data-stu-id="8717b-176">404</span></span>         | <span data-ttu-id="8717b-177">Das Paket, das mit `ID` und (optional) `VERSION` angegeben wurde, existiert nicht</span><span class="sxs-lookup"><span data-stu-id="8717b-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
