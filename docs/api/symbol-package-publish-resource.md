---
title: Push-Symbol Pakete, nuget-API | Microsoft-Dokumentation
author: cristinamanum
ms.author: cmanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Der Veröffentlichungs Dienst ermöglicht Clients das Veröffentlichen neuer Symbol Pakete.
keywords: Nuget-API-Push-Symbol Paket
ms.reviewer: karann
ms.openlocfilehash: 91bb4c9ca77fd7f1ff35831e02eb4f9d65d641c5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773890"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="faec7-104">Push-Symbol Pakete</span><span class="sxs-lookup"><span data-stu-id="faec7-104">Push Symbol Packages</span></span>

<span data-ttu-id="faec7-105">Es ist möglich, Symbol Pakete ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) mithilfe der nuget-V3-API per Push zu übermitteln.</span><span class="sxs-lookup"><span data-stu-id="faec7-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="faec7-106">Diese Vorgänge basieren auf der Ressource, die `SymbolPackagePublish` im [Dienst Index](service-index.md)gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="faec7-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="faec7-107">Versionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="faec7-107">Versioning</span></span>

<span data-ttu-id="faec7-108">Der folgende `@type` Wert wird verwendet:</span><span class="sxs-lookup"><span data-stu-id="faec7-108">The following `@type` value is used:</span></span>

<span data-ttu-id="faec7-109">Wert vom Typ @type</span><span class="sxs-lookup"><span data-stu-id="faec7-109">@type value</span></span>                 | <span data-ttu-id="faec7-110">Hinweise</span><span class="sxs-lookup"><span data-stu-id="faec7-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="faec7-111">Symbolpackagepublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="faec7-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="faec7-112">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="faec7-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="faec7-113">Basis-URL</span><span class="sxs-lookup"><span data-stu-id="faec7-113">Base URL</span></span>

<span data-ttu-id="faec7-114">Die Basis-URL für die folgenden APIs ist der Wert der `@id` -Eigenschaft der `SymbolPackagePublish/4.9.0` Ressource im [Dienst Index](service-index.md)der Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="faec7-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="faec7-115">In der nachfolgenden Dokumentation wird die URL von "nuget. org" verwendet.</span><span class="sxs-lookup"><span data-stu-id="faec7-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="faec7-116">Beachten Sie `https://www.nuget.org/api/v2/symbolpackage` als Platzhalter für den `@id` Wert, der im Dienst Index gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="faec7-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="faec7-117">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="faec7-117">HTTP methods</span></span>

<span data-ttu-id="faec7-118">Die `PUT` http-Methode wird von dieser Ressource unterstützt.</span><span class="sxs-lookup"><span data-stu-id="faec7-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="faec7-119">Symbol Paket per Push übersetzen</span><span class="sxs-lookup"><span data-stu-id="faec7-119">Push a symbol package</span></span>

<span data-ttu-id="faec7-120">nuget.org unterstützt das Pushen des neuen Symbol Paket Formats ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) mithilfe der folgenden API.</span><span class="sxs-lookup"><span data-stu-id="faec7-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

```
PUT https://www.nuget.org/api/v2/symbolpackage
```

<span data-ttu-id="faec7-121">Symbol Pakete mit derselben ID und Version können mehrmals übermittelt werden.</span><span class="sxs-lookup"><span data-stu-id="faec7-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="faec7-122">Ein Symbol Paket wird in den folgenden Fällen zurückgewiesen.</span><span class="sxs-lookup"><span data-stu-id="faec7-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="faec7-123">Ein Paket mit derselben ID und Version ist nicht vorhanden.</span><span class="sxs-lookup"><span data-stu-id="faec7-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="faec7-124">Ein Symbol Paket mit derselben ID und Version wurde per pushübertragung übermittelt, aber noch nicht veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="faec7-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="faec7-125">Das Symbol Paket ("[snupkg](../create-packages/Symbol-Packages-snupkg.md)") ist ungültig (siehe [Symbol Paket Einschränkungen](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="faec7-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="faec7-126">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="faec7-126">Request parameters</span></span>

<span data-ttu-id="faec7-127">Name</span><span class="sxs-lookup"><span data-stu-id="faec7-127">Name</span></span>           | <span data-ttu-id="faec7-128">In</span><span class="sxs-lookup"><span data-stu-id="faec7-128">In</span></span>     | <span data-ttu-id="faec7-129">Typ</span><span class="sxs-lookup"><span data-stu-id="faec7-129">Type</span></span>   | <span data-ttu-id="faec7-130">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="faec7-130">Required</span></span> | <span data-ttu-id="faec7-131">Notizen</span><span class="sxs-lookup"><span data-stu-id="faec7-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="faec7-132">X-nuget-APIKey</span><span class="sxs-lookup"><span data-stu-id="faec7-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="faec7-133">Header</span><span class="sxs-lookup"><span data-stu-id="faec7-133">Header</span></span> | <span data-ttu-id="faec7-134">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="faec7-134">string</span></span> | <span data-ttu-id="faec7-135">ja</span><span class="sxs-lookup"><span data-stu-id="faec7-135">yes</span></span>      | <span data-ttu-id="faec7-136">Zum Beispiel, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="faec7-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="faec7-137">Der API-Schlüssel ist eine nicht transparente Zeichenfolge, die vom Benutzer aus der Paketquelle abgerufen und für den Client konfiguriert wurde.</span><span class="sxs-lookup"><span data-stu-id="faec7-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="faec7-138">Es ist kein bestimmtes Zeichen folgen Format vorgeschrieben, aber die Länge des API-Schlüssels sollte keine angemessene Größe für HTTP-Header Werte überschreiten.</span><span class="sxs-lookup"><span data-stu-id="faec7-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="faec7-139">Anforderungstext</span><span class="sxs-lookup"><span data-stu-id="faec7-139">Request body</span></span>

<span data-ttu-id="faec7-140">Der Anforderungs Text für das Symbol Push entspricht dem Anforderungs Text einer paketpushanforderung (siehe [Package Push und DELETE](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="faec7-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="faec7-141">Antwort</span><span class="sxs-lookup"><span data-stu-id="faec7-141">Response</span></span>

<span data-ttu-id="faec7-142">Statuscode</span><span class="sxs-lookup"><span data-stu-id="faec7-142">Status Code</span></span> | <span data-ttu-id="faec7-143">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="faec7-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="faec7-144">201</span><span class="sxs-lookup"><span data-stu-id="faec7-144">201</span></span>         | <span data-ttu-id="faec7-145">Das Symbol Paket wurde erfolgreich per pushübertragung übermittelt.</span><span class="sxs-lookup"><span data-stu-id="faec7-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="faec7-146">400</span><span class="sxs-lookup"><span data-stu-id="faec7-146">400</span></span>         | <span data-ttu-id="faec7-147">Das angegebene Symbol Paket ist ungültig.</span><span class="sxs-lookup"><span data-stu-id="faec7-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="faec7-148">401</span><span class="sxs-lookup"><span data-stu-id="faec7-148">401</span></span>         | <span data-ttu-id="faec7-149">Der Benutzer ist nicht autorisiert, diese Aktion auszuführen.</span><span class="sxs-lookup"><span data-stu-id="faec7-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="faec7-150">404</span><span class="sxs-lookup"><span data-stu-id="faec7-150">404</span></span>         | <span data-ttu-id="faec7-151">Ein entsprechendes Paket mit der angegebenen ID und der angegebenen Version ist nicht vorhanden.</span><span class="sxs-lookup"><span data-stu-id="faec7-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="faec7-152">409</span><span class="sxs-lookup"><span data-stu-id="faec7-152">409</span></span>         | <span data-ttu-id="faec7-153">Ein Symbol Paket mit der angegebenen ID und Version wurde per Pushvorgang übermittelt, ist aber noch nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="faec7-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="faec7-154">413</span><span class="sxs-lookup"><span data-stu-id="faec7-154">413</span></span>         | <span data-ttu-id="faec7-155">Das Paket ist zu groß.</span><span class="sxs-lookup"><span data-stu-id="faec7-155">The package is too large.</span></span>

