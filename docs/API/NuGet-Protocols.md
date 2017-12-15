---
title: NuGet.org-Protokolle | Microsoft Docs
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba1d9742-9f1c-42ff-8c30-8e953e23c501
description: Die Interaktion mit NuGet-Clients sich entwickelnden nuget.org-Protokolle.
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 097b7a86d056b692c52d6de76bc2fb99d1b58c6f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="6ddc1-103">NuGet.org-Protokolle</span><span class="sxs-lookup"><span data-stu-id="6ddc1-103">nuget.org Protocols</span></span>

<span data-ttu-id="6ddc1-104">Um mit nuget.org interagieren, müssen Clients bestimmte Protokolle zu befolgen.</span><span class="sxs-lookup"><span data-stu-id="6ddc1-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="6ddc1-105">Da diese Protokolle weiterentwickelt beizubehalten, müssen Clients die Protokollversion identifizieren nutzen, wenn bestimmte nuget.org-APIs aufrufen.</span><span class="sxs-lookup"><span data-stu-id="6ddc1-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="6ddc1-106">Dadurch können nuget.org einführen von Änderungen auf eine nicht unterbrechende Weise für die alten Clients.</span><span class="sxs-lookup"><span data-stu-id="6ddc1-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="6ddc1-107">Auf dieser Seite dokumentierten APIs für nuget.org spezifisch sind, und es ist nicht davon ausgehen, bei anderen Implementierungen des NuGet-Server diese APIs einzuführen.</span><span class="sxs-lookup"><span data-stu-id="6ddc1-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="6ddc1-108">Weitere Informationen über die NuGet-API, die allgemein für den NuGet-Ökosystem implementiert, finden Sie unter der [Übersicht über die API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="6ddc1-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="6ddc1-109">Dieses Thema enthält verschiedene Protokolle wie und wann sie auf Vorhandensein eintreffen.</span><span class="sxs-lookup"><span data-stu-id="6ddc1-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="6ddc1-110">NuGet-Protokollversion 4.1.0</span><span class="sxs-lookup"><span data-stu-id="6ddc1-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="6ddc1-111">Die 4.1.0 Protokoll gibt die Verwendung der überprüfen Bereich Schlüssel für die Interaktion mit Dienste als nuget.org, um ein Paket mit einem nuget.org-Konto zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="6ddc1-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="6ddc1-112">Beachten Sie, dass die `4.1.0` Version ist eine nicht transparente Zeichenfolge jedoch geschieht mit den in der Regel mit der ersten Version des offiziellen NuGet-Clients, die dieses Protokoll unterstützt.</span><span class="sxs-lookup"><span data-stu-id="6ddc1-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="6ddc1-113">Überprüfung wird sichergestellt, dass die benutzerdefinierte API-Schlüssel werden nur mit nuget.org verwendet, und dieser anderen Überprüfung oder Validierung von einem Drittanbieter-Dienst über einen einmaligen Verwendung überprüfen Bereich Schlüssel behandelt wird.</span><span class="sxs-lookup"><span data-stu-id="6ddc1-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="6ddc1-114">Diese Schlüssel überprüfen Bereich können verwendet werden, um sicherzustellen, dass das Paket nach einem bestimmten Benutzer (Konto) auf nuget.org gehört.</span><span class="sxs-lookup"><span data-stu-id="6ddc1-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="6ddc1-115">Client-Anforderung</span><span class="sxs-lookup"><span data-stu-id="6ddc1-115">Client requirement</span></span>

<span data-ttu-id="6ddc1-116">Clients müssen die folgenden Header übergeben werden soll, wenn sie API-Aufrufe an Stellen **Push** zu nuget.org Pakete:</span><span class="sxs-lookup"><span data-stu-id="6ddc1-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="6ddc1-117">Beachten Sie, dass die bereits vorhandenen `X-NuGet-Client-Version` Header hat den gleichen Zweck aber ist inzwischen veraltet und sollte nicht mehr verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="6ddc1-117">Note that the pre-existing `X-NuGet-Client-Version` header has the same purpose but is now deprecated and should no longer be used.</span></span>

<span data-ttu-id="6ddc1-118">Die **Push** Protokoll selbst wird beschrieben, in der Dokumentation für die [ `PackagePublish` Ressource](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="6ddc1-118">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="6ddc1-119">Wenn ein Client mit externen Diensten und Anforderungen interagiert zu prüfen, ob ein Paket zu einem bestimmten Benutzer (Konto) gehört, sollte Schlüssel überprüfen-Bereich und nicht der API-Schlüssel nuget.org verwenden das folgende Protokoll und verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="6ddc1-119">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="6ddc1-120">API zum Anfordern eines Schlüssels überprüfen-Bereich</span><span class="sxs-lookup"><span data-stu-id="6ddc1-120">API to request a verify-scope key</span></span>

<span data-ttu-id="6ddc1-121">Diese API wird verwendet, um einen Schlüssel überprüfen-Bereich für einen nuget.org-Autor zum Überprüfen von Paketen im Besitz von ihn abzurufen.</span><span class="sxs-lookup"><span data-stu-id="6ddc1-121">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="6ddc1-122">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="6ddc1-122">Request parameters</span></span>

<span data-ttu-id="6ddc1-123">Name</span><span class="sxs-lookup"><span data-stu-id="6ddc1-123">Name</span></span>           | <span data-ttu-id="6ddc1-124">In</span><span class="sxs-lookup"><span data-stu-id="6ddc1-124">In</span></span>     | <span data-ttu-id="6ddc1-125">Typ</span><span class="sxs-lookup"><span data-stu-id="6ddc1-125">Type</span></span>   | <span data-ttu-id="6ddc1-126">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="6ddc1-126">Required</span></span> | <span data-ttu-id="6ddc1-127">Hinweise</span><span class="sxs-lookup"><span data-stu-id="6ddc1-127">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="6ddc1-128">ID</span><span class="sxs-lookup"><span data-stu-id="6ddc1-128">ID</span></span>             | <span data-ttu-id="6ddc1-129">URL</span><span class="sxs-lookup"><span data-stu-id="6ddc1-129">URL</span></span>    | <span data-ttu-id="6ddc1-130">string</span><span class="sxs-lookup"><span data-stu-id="6ddc1-130">string</span></span> | <span data-ttu-id="6ddc1-131">ja</span><span class="sxs-lookup"><span data-stu-id="6ddc1-131">yes</span></span>      | <span data-ttu-id="6ddc1-132">Die Paket-Identidier für die der überprüfen Bereich Schlüssel angefordert wird</span><span class="sxs-lookup"><span data-stu-id="6ddc1-132">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="6ddc1-133">VERSION</span><span class="sxs-lookup"><span data-stu-id="6ddc1-133">VERSION</span></span>        | <span data-ttu-id="6ddc1-134">URL</span><span class="sxs-lookup"><span data-stu-id="6ddc1-134">URL</span></span>    | <span data-ttu-id="6ddc1-135">string</span><span class="sxs-lookup"><span data-stu-id="6ddc1-135">string</span></span> | <span data-ttu-id="6ddc1-136">Nein</span><span class="sxs-lookup"><span data-stu-id="6ddc1-136">no</span></span>       | <span data-ttu-id="6ddc1-137">Die Paketversion</span><span class="sxs-lookup"><span data-stu-id="6ddc1-137">The package version</span></span>
<span data-ttu-id="6ddc1-138">X-NuGet-"apikey"</span><span class="sxs-lookup"><span data-stu-id="6ddc1-138">X-NuGet-ApiKey</span></span> | <span data-ttu-id="6ddc1-139">Header</span><span class="sxs-lookup"><span data-stu-id="6ddc1-139">Header</span></span> | <span data-ttu-id="6ddc1-140">string</span><span class="sxs-lookup"><span data-stu-id="6ddc1-140">string</span></span> | <span data-ttu-id="6ddc1-141">ja</span><span class="sxs-lookup"><span data-stu-id="6ddc1-141">yes</span></span>      | <span data-ttu-id="6ddc1-142">Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="6ddc1-142">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="6ddc1-143">Antwort</span><span class="sxs-lookup"><span data-stu-id="6ddc1-143">Response</span></span>

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="6ddc1-144">-API, um den Bereich-Schlüssel überprüfen Überprüfen</span><span class="sxs-lookup"><span data-stu-id="6ddc1-144">API to verify the verify scope key</span></span>

<span data-ttu-id="6ddc1-145">Diese API dient zum Überprüfen Bereich Schlüssel für den Autor nuget.org gehörige Paket zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="6ddc1-145">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="6ddc1-146">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="6ddc1-146">Request parameters</span></span>

<span data-ttu-id="6ddc1-147">Name</span><span class="sxs-lookup"><span data-stu-id="6ddc1-147">Name</span></span>           | <span data-ttu-id="6ddc1-148">In</span><span class="sxs-lookup"><span data-stu-id="6ddc1-148">In</span></span>     | <span data-ttu-id="6ddc1-149">Typ</span><span class="sxs-lookup"><span data-stu-id="6ddc1-149">Type</span></span>   | <span data-ttu-id="6ddc1-150">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="6ddc1-150">Required</span></span> | <span data-ttu-id="6ddc1-151">Hinweise</span><span class="sxs-lookup"><span data-stu-id="6ddc1-151">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="6ddc1-152">ID</span><span class="sxs-lookup"><span data-stu-id="6ddc1-152">ID</span></span>             | <span data-ttu-id="6ddc1-153">URL</span><span class="sxs-lookup"><span data-stu-id="6ddc1-153">URL</span></span>    | <span data-ttu-id="6ddc1-154">string</span><span class="sxs-lookup"><span data-stu-id="6ddc1-154">string</span></span> | <span data-ttu-id="6ddc1-155">ja</span><span class="sxs-lookup"><span data-stu-id="6ddc1-155">yes</span></span>      | <span data-ttu-id="6ddc1-156">Die Paket-ID für die der überprüfen Bereich Schlüssel angefordert wird</span><span class="sxs-lookup"><span data-stu-id="6ddc1-156">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="6ddc1-157">VERSION</span><span class="sxs-lookup"><span data-stu-id="6ddc1-157">VERSION</span></span>        | <span data-ttu-id="6ddc1-158">URL</span><span class="sxs-lookup"><span data-stu-id="6ddc1-158">URL</span></span>    | <span data-ttu-id="6ddc1-159">string</span><span class="sxs-lookup"><span data-stu-id="6ddc1-159">string</span></span> | <span data-ttu-id="6ddc1-160">Nein</span><span class="sxs-lookup"><span data-stu-id="6ddc1-160">no</span></span>       | <span data-ttu-id="6ddc1-161">Die Paketversion</span><span class="sxs-lookup"><span data-stu-id="6ddc1-161">The package version</span></span>
<span data-ttu-id="6ddc1-162">X-NuGet-"apikey"</span><span class="sxs-lookup"><span data-stu-id="6ddc1-162">X-NuGet-ApiKey</span></span> | <span data-ttu-id="6ddc1-163">Header</span><span class="sxs-lookup"><span data-stu-id="6ddc1-163">Header</span></span> | <span data-ttu-id="6ddc1-164">string</span><span class="sxs-lookup"><span data-stu-id="6ddc1-164">string</span></span> | <span data-ttu-id="6ddc1-165">ja</span><span class="sxs-lookup"><span data-stu-id="6ddc1-165">yes</span></span>      | <span data-ttu-id="6ddc1-166">Beispiel: `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="6ddc1-166">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="6ddc1-167">Diese überprüfen Bereich API-Schlüssel läuft ab, in einem Tag oder bei der ersten Verwendung, welcher Fall zuerst eintritt.</span><span class="sxs-lookup"><span data-stu-id="6ddc1-167">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="6ddc1-168">Antwort</span><span class="sxs-lookup"><span data-stu-id="6ddc1-168">Response</span></span>

<span data-ttu-id="6ddc1-169">Statuscode</span><span class="sxs-lookup"><span data-stu-id="6ddc1-169">Status Code</span></span> | <span data-ttu-id="6ddc1-170">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="6ddc1-170">Meaning</span></span>
----------- | -------
<span data-ttu-id="6ddc1-171">300</span><span class="sxs-lookup"><span data-stu-id="6ddc1-171">200</span></span>         | <span data-ttu-id="6ddc1-172">Die API-Schlüssel ist ungültig</span><span class="sxs-lookup"><span data-stu-id="6ddc1-172">The API key is valid</span></span>
<span data-ttu-id="6ddc1-173">403</span><span class="sxs-lookup"><span data-stu-id="6ddc1-173">403</span></span>         | <span data-ttu-id="6ddc1-174">API-Schlüssel ist ungültig oder nicht autorisierte für das Paket mithilfe von Push übertragen</span><span class="sxs-lookup"><span data-stu-id="6ddc1-174">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="6ddc1-175">404</span><span class="sxs-lookup"><span data-stu-id="6ddc1-175">404</span></span>         | <span data-ttu-id="6ddc1-176">Das Paket verweist auf `ID` und `VERSION` (optional) ist nicht vorhanden</span><span class="sxs-lookup"><span data-stu-id="6ddc1-176">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
