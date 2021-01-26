---
title: nuget.org-Protokolle
description: Die sich entwickelnden nuget.org-Protokolle für die Interaktion mit nuget-Clients.
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773977"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="91abb-103">nuget.org-Protokolle</span><span class="sxs-lookup"><span data-stu-id="91abb-103">nuget.org protocols</span></span>

<span data-ttu-id="91abb-104">Um mit nuget.org interagieren zu können, müssen Clients bestimmte Protokolle einhalten.</span><span class="sxs-lookup"><span data-stu-id="91abb-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="91abb-105">Da diese Protokolle weiterentwickelt werden, müssen Clients die Protokollversion identifizieren, die Sie beim Aufrufen spezifischer nuget.org-APIs verwenden.</span><span class="sxs-lookup"><span data-stu-id="91abb-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="91abb-106">Dies ermöglicht es nuget.org, Änderungen für die alten Clients in einer nicht unterbrechend orientierten Weise einzuführen.</span><span class="sxs-lookup"><span data-stu-id="91abb-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="91abb-107">Die auf dieser Seite dokumentierten APIs sind spezifisch für nuget.org, und es wird nicht erwartet, dass andere nuget-Server Implementierungen diese APIs einführen.</span><span class="sxs-lookup"><span data-stu-id="91abb-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="91abb-108">Weitere Informationen über die nuget-API, die im gesamten nuget-Ökosystem implementiert ist, finden Sie in der [API-Übersicht](overview.md).</span><span class="sxs-lookup"><span data-stu-id="91abb-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="91abb-109">In diesem Thema werden verschiedene Protokolle als und wann Sie vorhanden sind aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="91abb-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="91abb-110">Nuget-Protokollversion 4.1.0</span><span class="sxs-lookup"><span data-stu-id="91abb-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="91abb-111">Das 4.1.0-Protokoll gibt die Verwendung von Verify-Scope-Schlüsseln für die Interaktion mit anderen Diensten als nuget.org an, um ein Paket mit einem nuget.org-Konto zu validieren.</span><span class="sxs-lookup"><span data-stu-id="91abb-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="91abb-112">Beachten Sie, dass die `4.1.0` Versionsnummer eine nicht transparente Zeichenfolge ist, aber mit der ersten Version des offiziellen nuget-Clients übereinstimmt, der dieses Protokoll unterstützt hat.</span><span class="sxs-lookup"><span data-stu-id="91abb-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="91abb-113">Bei der Validierung wird sichergestellt, dass die vom Benutzer erstellten API-Schlüssel nur mit nuget.org verwendet werden, und dass eine andere Überprüfung oder Validierung von einem Drittanbieter Dienst über die einmalige Verwendung von Verify-Scope-Schlüsseln verarbeitet wird.</span><span class="sxs-lookup"><span data-stu-id="91abb-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="91abb-114">Diese Schlüssel zum Überprüfen des Bereichs können verwendet werden, um zu überprüfen, ob das Paket zu einem bestimmten Benutzer (Konto) auf nuget.org gehört.</span><span class="sxs-lookup"><span data-stu-id="91abb-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="91abb-115">Client Anforderung</span><span class="sxs-lookup"><span data-stu-id="91abb-115">Client requirement</span></span>

<span data-ttu-id="91abb-116">Clients müssen den folgenden Header übergeben, wenn Sie API-Aufrufe **zum Übertragen von Paketen an** nuget.org durchführen:</span><span class="sxs-lookup"><span data-stu-id="91abb-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="91abb-117">Beachten Sie, dass der `X-NuGet-Client-Version` Header eine ähnliche Semantik hat, aber nur für den offiziellen nuget-Client verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="91abb-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="91abb-118">Clients von Drittanbietern sollten den `X-NuGet-Protocol-Version` -Header und den-Wert verwenden.</span><span class="sxs-lookup"><span data-stu-id="91abb-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="91abb-119">Das **pushprotokoll** selbst wird in der Dokumentation für die [ `PackagePublish` Ressource](package-publish-resource.md)beschrieben.</span><span class="sxs-lookup"><span data-stu-id="91abb-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="91abb-120">Wenn ein Client mit externen Diensten interagiert und überprüft werden muss, ob ein Paket zu einem bestimmten Benutzer (Konto) gehört, sollte er das folgende Protokoll verwenden und die Schlüssel für den Verifizierungs Bereich und nicht die API-Schlüssel von nuget.org verwenden.</span><span class="sxs-lookup"><span data-stu-id="91abb-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="91abb-121">API zum Anfordern eines Verifizierungs Bereichs Schlüssels</span><span class="sxs-lookup"><span data-stu-id="91abb-121">API to request a verify-scope key</span></span>

<span data-ttu-id="91abb-122">Diese API wird verwendet, um einen Schlüssel zum Überprüfen des Bereichs zu erhalten, damit ein nuget.org-Autor ein Paket überprüfen kann, das sich im Besitz von ihm befindet</span><span class="sxs-lookup"><span data-stu-id="91abb-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="91abb-123">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="91abb-123">Request parameters</span></span>

<span data-ttu-id="91abb-124">Name</span><span class="sxs-lookup"><span data-stu-id="91abb-124">Name</span></span>           | <span data-ttu-id="91abb-125">In</span><span class="sxs-lookup"><span data-stu-id="91abb-125">In</span></span>     | <span data-ttu-id="91abb-126">Typ</span><span class="sxs-lookup"><span data-stu-id="91abb-126">Type</span></span>   | <span data-ttu-id="91abb-127">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="91abb-127">Required</span></span> | <span data-ttu-id="91abb-128">Notizen</span><span class="sxs-lookup"><span data-stu-id="91abb-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="91abb-129">id</span><span class="sxs-lookup"><span data-stu-id="91abb-129">ID</span></span>             | <span data-ttu-id="91abb-130">URL</span><span class="sxs-lookup"><span data-stu-id="91abb-130">URL</span></span>    | <span data-ttu-id="91abb-131">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="91abb-131">string</span></span> | <span data-ttu-id="91abb-132">ja</span><span class="sxs-lookup"><span data-stu-id="91abb-132">yes</span></span>      | <span data-ttu-id="91abb-133">Der paketidentierer, für den der Gültigkeits Bereichs Schlüssel angefordert wird.</span><span class="sxs-lookup"><span data-stu-id="91abb-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="91abb-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="91abb-134">VERSION</span></span>        | <span data-ttu-id="91abb-135">URL</span><span class="sxs-lookup"><span data-stu-id="91abb-135">URL</span></span>    | <span data-ttu-id="91abb-136">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="91abb-136">string</span></span> | <span data-ttu-id="91abb-137">nein</span><span class="sxs-lookup"><span data-stu-id="91abb-137">no</span></span>       | <span data-ttu-id="91abb-138">Die Paketversion</span><span class="sxs-lookup"><span data-stu-id="91abb-138">The package version</span></span>
<span data-ttu-id="91abb-139">X-nuget-APIKey</span><span class="sxs-lookup"><span data-stu-id="91abb-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="91abb-140">Header</span><span class="sxs-lookup"><span data-stu-id="91abb-140">Header</span></span> | <span data-ttu-id="91abb-141">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="91abb-141">string</span></span> | <span data-ttu-id="91abb-142">ja</span><span class="sxs-lookup"><span data-stu-id="91abb-142">yes</span></span>      | <span data-ttu-id="91abb-143">Zum Beispiel, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="91abb-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="91abb-144">Antwort</span><span class="sxs-lookup"><span data-stu-id="91abb-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="91abb-145">API zum Überprüfen des Gültigkeits Bereichs Schlüssels</span><span class="sxs-lookup"><span data-stu-id="91abb-145">API to verify the verify scope key</span></span>

<span data-ttu-id="91abb-146">Diese API wird verwendet, um einen Schlüssel zum Überprüfen des Bereichs für das Paket zu überprüfen, das im Besitz von nuget.org Author ist</span><span class="sxs-lookup"><span data-stu-id="91abb-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="91abb-147">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="91abb-147">Request parameters</span></span>

<span data-ttu-id="91abb-148">Name</span><span class="sxs-lookup"><span data-stu-id="91abb-148">Name</span></span>           | <span data-ttu-id="91abb-149">In</span><span class="sxs-lookup"><span data-stu-id="91abb-149">In</span></span>     | <span data-ttu-id="91abb-150">Typ</span><span class="sxs-lookup"><span data-stu-id="91abb-150">Type</span></span>   | <span data-ttu-id="91abb-151">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="91abb-151">Required</span></span> | <span data-ttu-id="91abb-152">Notizen</span><span class="sxs-lookup"><span data-stu-id="91abb-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="91abb-153">id</span><span class="sxs-lookup"><span data-stu-id="91abb-153">ID</span></span>             | <span data-ttu-id="91abb-154">URL</span><span class="sxs-lookup"><span data-stu-id="91abb-154">URL</span></span>    | <span data-ttu-id="91abb-155">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="91abb-155">string</span></span> | <span data-ttu-id="91abb-156">ja</span><span class="sxs-lookup"><span data-stu-id="91abb-156">yes</span></span>      | <span data-ttu-id="91abb-157">Der Paket Bezeichner, für den der Schlüssel zum Überprüfen des Bereichs angefordert wird</span><span class="sxs-lookup"><span data-stu-id="91abb-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="91abb-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="91abb-158">VERSION</span></span>        | <span data-ttu-id="91abb-159">URL</span><span class="sxs-lookup"><span data-stu-id="91abb-159">URL</span></span>    | <span data-ttu-id="91abb-160">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="91abb-160">string</span></span> | <span data-ttu-id="91abb-161">nein</span><span class="sxs-lookup"><span data-stu-id="91abb-161">no</span></span>       | <span data-ttu-id="91abb-162">Die Paketversion</span><span class="sxs-lookup"><span data-stu-id="91abb-162">The package version</span></span>
<span data-ttu-id="91abb-163">X-nuget-APIKey</span><span class="sxs-lookup"><span data-stu-id="91abb-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="91abb-164">Header</span><span class="sxs-lookup"><span data-stu-id="91abb-164">Header</span></span> | <span data-ttu-id="91abb-165">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="91abb-165">string</span></span> | <span data-ttu-id="91abb-166">ja</span><span class="sxs-lookup"><span data-stu-id="91abb-166">yes</span></span>      | <span data-ttu-id="91abb-167">Zum Beispiel, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="91abb-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="91abb-168">Dieser Gültigkeitsbereich-API-Schlüssel läuft in einem Tag oder bei der ersten Verwendung ab, je nachdem, welcher Fall zuerst eintritt.</span><span class="sxs-lookup"><span data-stu-id="91abb-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="91abb-169">Antwort</span><span class="sxs-lookup"><span data-stu-id="91abb-169">Response</span></span>

<span data-ttu-id="91abb-170">Statuscode</span><span class="sxs-lookup"><span data-stu-id="91abb-170">Status Code</span></span> | <span data-ttu-id="91abb-171">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="91abb-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="91abb-172">200</span><span class="sxs-lookup"><span data-stu-id="91abb-172">200</span></span>         | <span data-ttu-id="91abb-173">Der API-Schlüssel ist gültig.</span><span class="sxs-lookup"><span data-stu-id="91abb-173">The API key is valid</span></span>
<span data-ttu-id="91abb-174">403</span><span class="sxs-lookup"><span data-stu-id="91abb-174">403</span></span>         | <span data-ttu-id="91abb-175">Der API-Schlüssel ist ungültig oder nicht zum Pushen des Pakets autorisiert.</span><span class="sxs-lookup"><span data-stu-id="91abb-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="91abb-176">404</span><span class="sxs-lookup"><span data-stu-id="91abb-176">404</span></span>         | <span data-ttu-id="91abb-177">Das Paket, auf das `ID` und `VERSION` (optional) verwiesen wird, ist nicht vorhanden.</span><span class="sxs-lookup"><span data-stu-id="91abb-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
