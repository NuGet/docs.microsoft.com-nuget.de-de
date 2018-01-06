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
ms.openlocfilehash: 0bc71795d120256b9eb14ca64141f0b69f01e620
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/05/2018
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="28a50-103">NuGet.org-Protokolle</span><span class="sxs-lookup"><span data-stu-id="28a50-103">nuget.org Protocols</span></span>

<span data-ttu-id="28a50-104">Um mit nuget.org interagieren, müssen Clients bestimmte Protokolle zu befolgen.</span><span class="sxs-lookup"><span data-stu-id="28a50-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="28a50-105">Da diese Protokolle weiterentwickelt beizubehalten, müssen Clients die Protokollversion identifizieren nutzen, wenn bestimmte nuget.org-APIs aufrufen.</span><span class="sxs-lookup"><span data-stu-id="28a50-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="28a50-106">Dadurch können nuget.org einführen von Änderungen auf eine nicht unterbrechende Weise für die alten Clients.</span><span class="sxs-lookup"><span data-stu-id="28a50-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="28a50-107">Auf dieser Seite dokumentierten APIs für nuget.org spezifisch sind, und es ist nicht davon ausgehen, bei anderen Implementierungen des NuGet-Server diese APIs einzuführen.</span><span class="sxs-lookup"><span data-stu-id="28a50-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="28a50-108">Weitere Informationen über die NuGet-API, die allgemein für den NuGet-Ökosystem implementiert, finden Sie unter der [Übersicht über die API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="28a50-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="28a50-109">Dieses Thema enthält verschiedene Protokolle wie und wann sie auf Vorhandensein eintreffen.</span><span class="sxs-lookup"><span data-stu-id="28a50-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="28a50-110">NuGet-Protokollversion 4.1.0</span><span class="sxs-lookup"><span data-stu-id="28a50-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="28a50-111">Die 4.1.0 Protokoll gibt die Verwendung der überprüfen Bereich Schlüssel für die Interaktion mit Dienste als nuget.org, um ein Paket mit einem nuget.org-Konto zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="28a50-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="28a50-112">Beachten Sie, dass die `4.1.0` Version ist eine nicht transparente Zeichenfolge jedoch geschieht mit den in der Regel mit der ersten Version des offiziellen NuGet-Clients, die dieses Protokoll unterstützt.</span><span class="sxs-lookup"><span data-stu-id="28a50-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="28a50-113">Überprüfung wird sichergestellt, dass die benutzerdefinierte API-Schlüssel werden nur mit nuget.org verwendet, und dieser anderen Überprüfung oder Validierung von einem Drittanbieter-Dienst über einen einmaligen Verwendung überprüfen Bereich Schlüssel behandelt wird.</span><span class="sxs-lookup"><span data-stu-id="28a50-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="28a50-114">Diese Schlüssel überprüfen Bereich können verwendet werden, um sicherzustellen, dass das Paket nach einem bestimmten Benutzer (Konto) auf nuget.org gehört.</span><span class="sxs-lookup"><span data-stu-id="28a50-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="28a50-115">Client-Anforderung</span><span class="sxs-lookup"><span data-stu-id="28a50-115">Client requirement</span></span>

<span data-ttu-id="28a50-116">Clients müssen die folgenden Header übergeben werden soll, wenn sie API-Aufrufe an Stellen **Push** zu nuget.org Pakete:</span><span class="sxs-lookup"><span data-stu-id="28a50-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="28a50-117">Beachten Sie, dass die `X-NuGet-Client-Version` Header weist eine ähnliche Semantik jedoch reserviert nur durch den offiziellen NuGet-Client verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="28a50-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="28a50-118">Clients von Drittanbietern verwenden sollten die `X-NuGet-Protocol-Version` Header und Wert.</span><span class="sxs-lookup"><span data-stu-id="28a50-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="28a50-119">Die **Push** Protokoll selbst wird beschrieben, in der Dokumentation für die [ `PackagePublish` Ressource](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="28a50-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="28a50-120">Wenn ein Client mit externen Diensten und Anforderungen interagiert zu prüfen, ob ein Paket zu einem bestimmten Benutzer (Konto) gehört, sollte Schlüssel überprüfen-Bereich und nicht der API-Schlüssel nuget.org verwenden das folgende Protokoll und verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="28a50-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="28a50-121">API zum Anfordern eines Schlüssels überprüfen-Bereich</span><span class="sxs-lookup"><span data-stu-id="28a50-121">API to request a verify-scope key</span></span>

<span data-ttu-id="28a50-122">Diese API wird verwendet, um einen Schlüssel überprüfen-Bereich für einen nuget.org-Autor zum Überprüfen von Paketen im Besitz von ihn abzurufen.</span><span class="sxs-lookup"><span data-stu-id="28a50-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="28a50-123">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="28a50-123">Request parameters</span></span>

<span data-ttu-id="28a50-124">name</span><span class="sxs-lookup"><span data-stu-id="28a50-124">Name</span></span>           | <span data-ttu-id="28a50-125">In</span><span class="sxs-lookup"><span data-stu-id="28a50-125">In</span></span>     | <span data-ttu-id="28a50-126">Typ</span><span class="sxs-lookup"><span data-stu-id="28a50-126">Type</span></span>   | <span data-ttu-id="28a50-127">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="28a50-127">Required</span></span> | <span data-ttu-id="28a50-128">Hinweise</span><span class="sxs-lookup"><span data-stu-id="28a50-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="28a50-129">Id</span><span class="sxs-lookup"><span data-stu-id="28a50-129">ID</span></span>             | <span data-ttu-id="28a50-130">URL</span><span class="sxs-lookup"><span data-stu-id="28a50-130">URL</span></span>    | <span data-ttu-id="28a50-131">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="28a50-131">string</span></span> | <span data-ttu-id="28a50-132">ja</span><span class="sxs-lookup"><span data-stu-id="28a50-132">yes</span></span>      | <span data-ttu-id="28a50-133">Die Paket-Identidier für die der überprüfen Bereich Schlüssel angefordert wird</span><span class="sxs-lookup"><span data-stu-id="28a50-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="28a50-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="28a50-134">VERSION</span></span>        | <span data-ttu-id="28a50-135">URL</span><span class="sxs-lookup"><span data-stu-id="28a50-135">URL</span></span>    | <span data-ttu-id="28a50-136">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="28a50-136">string</span></span> | <span data-ttu-id="28a50-137">Nein</span><span class="sxs-lookup"><span data-stu-id="28a50-137">no</span></span>       | <span data-ttu-id="28a50-138">Die Paketversion</span><span class="sxs-lookup"><span data-stu-id="28a50-138">The package version</span></span>
<span data-ttu-id="28a50-139">X-NuGet-"apikey"</span><span class="sxs-lookup"><span data-stu-id="28a50-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="28a50-140">Header</span><span class="sxs-lookup"><span data-stu-id="28a50-140">Header</span></span> | <span data-ttu-id="28a50-141">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="28a50-141">string</span></span> | <span data-ttu-id="28a50-142">ja</span><span class="sxs-lookup"><span data-stu-id="28a50-142">yes</span></span>      | <span data-ttu-id="28a50-143">Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="28a50-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="28a50-144">Antwort</span><span class="sxs-lookup"><span data-stu-id="28a50-144">Response</span></span>

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="28a50-145">-API, um den Bereich-Schlüssel überprüfen Überprüfen</span><span class="sxs-lookup"><span data-stu-id="28a50-145">API to verify the verify scope key</span></span>

<span data-ttu-id="28a50-146">Diese API dient zum Überprüfen Bereich Schlüssel für den Autor nuget.org gehörige Paket zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="28a50-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="28a50-147">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="28a50-147">Request parameters</span></span>

<span data-ttu-id="28a50-148">name</span><span class="sxs-lookup"><span data-stu-id="28a50-148">Name</span></span>           | <span data-ttu-id="28a50-149">In</span><span class="sxs-lookup"><span data-stu-id="28a50-149">In</span></span>     | <span data-ttu-id="28a50-150">Typ</span><span class="sxs-lookup"><span data-stu-id="28a50-150">Type</span></span>   | <span data-ttu-id="28a50-151">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="28a50-151">Required</span></span> | <span data-ttu-id="28a50-152">Hinweise</span><span class="sxs-lookup"><span data-stu-id="28a50-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="28a50-153">Id</span><span class="sxs-lookup"><span data-stu-id="28a50-153">ID</span></span>             | <span data-ttu-id="28a50-154">URL</span><span class="sxs-lookup"><span data-stu-id="28a50-154">URL</span></span>    | <span data-ttu-id="28a50-155">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="28a50-155">string</span></span> | <span data-ttu-id="28a50-156">ja</span><span class="sxs-lookup"><span data-stu-id="28a50-156">yes</span></span>      | <span data-ttu-id="28a50-157">Die Paket-ID für die der überprüfen Bereich Schlüssel angefordert wird</span><span class="sxs-lookup"><span data-stu-id="28a50-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="28a50-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="28a50-158">VERSION</span></span>        | <span data-ttu-id="28a50-159">URL</span><span class="sxs-lookup"><span data-stu-id="28a50-159">URL</span></span>    | <span data-ttu-id="28a50-160">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="28a50-160">string</span></span> | <span data-ttu-id="28a50-161">Nein</span><span class="sxs-lookup"><span data-stu-id="28a50-161">no</span></span>       | <span data-ttu-id="28a50-162">Die Paketversion</span><span class="sxs-lookup"><span data-stu-id="28a50-162">The package version</span></span>
<span data-ttu-id="28a50-163">X-NuGet-"apikey"</span><span class="sxs-lookup"><span data-stu-id="28a50-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="28a50-164">Header</span><span class="sxs-lookup"><span data-stu-id="28a50-164">Header</span></span> | <span data-ttu-id="28a50-165">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="28a50-165">string</span></span> | <span data-ttu-id="28a50-166">ja</span><span class="sxs-lookup"><span data-stu-id="28a50-166">yes</span></span>      | <span data-ttu-id="28a50-167">Beispiel: `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="28a50-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="28a50-168">Diese überprüfen Bereich API-Schlüssel läuft ab, in einem Tag oder bei der ersten Verwendung, welcher Fall zuerst eintritt.</span><span class="sxs-lookup"><span data-stu-id="28a50-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="28a50-169">Antwort</span><span class="sxs-lookup"><span data-stu-id="28a50-169">Response</span></span>

<span data-ttu-id="28a50-170">Statuscode</span><span class="sxs-lookup"><span data-stu-id="28a50-170">Status Code</span></span> | <span data-ttu-id="28a50-171">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="28a50-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="28a50-172">300</span><span class="sxs-lookup"><span data-stu-id="28a50-172">200</span></span>         | <span data-ttu-id="28a50-173">Die API-Schlüssel ist ungültig</span><span class="sxs-lookup"><span data-stu-id="28a50-173">The API key is valid</span></span>
<span data-ttu-id="28a50-174">403</span><span class="sxs-lookup"><span data-stu-id="28a50-174">403</span></span>         | <span data-ttu-id="28a50-175">API-Schlüssel ist ungültig oder nicht autorisierte für das Paket mithilfe von Push übertragen</span><span class="sxs-lookup"><span data-stu-id="28a50-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="28a50-176">404</span><span class="sxs-lookup"><span data-stu-id="28a50-176">404</span></span>         | <span data-ttu-id="28a50-177">Das Paket verweist auf `ID` und `VERSION` (optional) ist nicht vorhanden</span><span class="sxs-lookup"><span data-stu-id="28a50-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
