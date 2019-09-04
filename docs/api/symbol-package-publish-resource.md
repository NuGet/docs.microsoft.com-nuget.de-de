---
title: Push-Symbol Pakete, nuget-API | Microsoft-Dokumentation
author: cristinamanum
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Der Veröffentlichungs Dienst ermöglicht Clients das Veröffentlichen neuer Symbol Pakete.
keywords: Nuget-API-Push-Symbol Paket
ms.reviewer: karann
ms.openlocfilehash: 27e557bf15ce31152243a409eddc4112eeb6c38b
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235106"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="8ded6-104">Push-Symbol Pakete</span><span class="sxs-lookup"><span data-stu-id="8ded6-104">Push Symbol Packages</span></span>

<span data-ttu-id="8ded6-105">Es ist möglich, Symbol Pakete ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) mithilfe der nuget-V3-API per Push zu übermitteln.</span><span class="sxs-lookup"><span data-stu-id="8ded6-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="8ded6-106">Diese Vorgänge basieren `SymbolPackagePublish` auf der Ressource, die im [Dienst Index](service-index.md)gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="8ded6-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="8ded6-107">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="8ded6-107">Versioning</span></span>

<span data-ttu-id="8ded6-108">Der folgende `@type` Wert wird verwendet:</span><span class="sxs-lookup"><span data-stu-id="8ded6-108">The following `@type` value is used:</span></span>

<span data-ttu-id="8ded6-109">@type -Wert</span><span class="sxs-lookup"><span data-stu-id="8ded6-109">@type value</span></span>                 | <span data-ttu-id="8ded6-110">Hinweise</span><span class="sxs-lookup"><span data-stu-id="8ded6-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="8ded6-111">Symbolpackagepublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="8ded6-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="8ded6-112">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="8ded6-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="8ded6-113">Basis-URL</span><span class="sxs-lookup"><span data-stu-id="8ded6-113">Base URL</span></span>

<span data-ttu-id="8ded6-114">Die Basis-URL für die folgenden APIs ist der Wert der `@id` -Eigenschaft `SymbolPackagePublish/4.9.0` der Ressource im [Dienst Index](service-index.md)der Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="8ded6-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="8ded6-115">In der nachfolgenden Dokumentation wird die URL von "nuget. org" verwendet.</span><span class="sxs-lookup"><span data-stu-id="8ded6-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="8ded6-116">Beachten `https://www.nuget.org/api/v2/symbolpackage` Sie als Platzhalter für den `@id` Wert, der im Dienst Index gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="8ded6-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="8ded6-117">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="8ded6-117">HTTP methods</span></span>

<span data-ttu-id="8ded6-118">Die `PUT` HTTP-Methode wird von dieser Ressource unterstützt.</span><span class="sxs-lookup"><span data-stu-id="8ded6-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="8ded6-119">Symbol Paket per Push übersetzen</span><span class="sxs-lookup"><span data-stu-id="8ded6-119">Push a symbol package</span></span>

<span data-ttu-id="8ded6-120">nuget.org unterstützt das Pushen des neuen Symbol Paket Formats ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) mithilfe der folgenden API.</span><span class="sxs-lookup"><span data-stu-id="8ded6-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="8ded6-121">Symbol Pakete mit derselben ID und Version können mehrmals übermittelt werden.</span><span class="sxs-lookup"><span data-stu-id="8ded6-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="8ded6-122">Ein Symbol Paket wird in den folgenden Fällen zurückgewiesen.</span><span class="sxs-lookup"><span data-stu-id="8ded6-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="8ded6-123">Ein Paket mit derselben ID und Version ist nicht vorhanden.</span><span class="sxs-lookup"><span data-stu-id="8ded6-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="8ded6-124">Ein Symbol Paket mit derselben ID und Version wurde per pushübertragung übermittelt, aber noch nicht veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="8ded6-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="8ded6-125">Das Symbol Paket ("[snupkg](../create-packages/Symbol-Packages-snupkg.md)") ist ungültig (siehe [Symbol Paket Einschränkungen](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="8ded6-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="8ded6-126">Anforderungs Parameter</span><span class="sxs-lookup"><span data-stu-id="8ded6-126">Request parameters</span></span>

<span data-ttu-id="8ded6-127">name</span><span class="sxs-lookup"><span data-stu-id="8ded6-127">Name</span></span>           | <span data-ttu-id="8ded6-128">In</span><span class="sxs-lookup"><span data-stu-id="8ded6-128">In</span></span>     | <span data-ttu-id="8ded6-129">Typ</span><span class="sxs-lookup"><span data-stu-id="8ded6-129">Type</span></span>   | <span data-ttu-id="8ded6-130">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="8ded6-130">Required</span></span> | <span data-ttu-id="8ded6-131">Hinweise</span><span class="sxs-lookup"><span data-stu-id="8ded6-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="8ded6-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="8ded6-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="8ded6-133">Header</span><span class="sxs-lookup"><span data-stu-id="8ded6-133">Header</span></span> | <span data-ttu-id="8ded6-134">String</span><span class="sxs-lookup"><span data-stu-id="8ded6-134">string</span></span> | <span data-ttu-id="8ded6-135">ja</span><span class="sxs-lookup"><span data-stu-id="8ded6-135">yes</span></span>      | <span data-ttu-id="8ded6-136">Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="8ded6-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="8ded6-137">Der API-Schlüssel ist eine nicht transparente Zeichenfolge, die vom Benutzer aus der Paketquelle abgerufen und für den Client konfiguriert wurde.</span><span class="sxs-lookup"><span data-stu-id="8ded6-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="8ded6-138">Es ist kein bestimmtes Zeichen folgen Format vorgeschrieben, aber die Länge des API-Schlüssels sollte keine angemessene Größe für HTTP-Header Werte überschreiten.</span><span class="sxs-lookup"><span data-stu-id="8ded6-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="8ded6-139">Anforderungstext</span><span class="sxs-lookup"><span data-stu-id="8ded6-139">Request body</span></span>

<span data-ttu-id="8ded6-140">Der Anforderungs Text für das Symbol Push entspricht dem Anforderungs Text einer paketpushanforderung (siehe [Package Push und DELETE](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="8ded6-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="8ded6-141">Antwort</span><span class="sxs-lookup"><span data-stu-id="8ded6-141">Response</span></span>

<span data-ttu-id="8ded6-142">Statuscode</span><span class="sxs-lookup"><span data-stu-id="8ded6-142">Status Code</span></span> | <span data-ttu-id="8ded6-143">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="8ded6-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="8ded6-144">201</span><span class="sxs-lookup"><span data-stu-id="8ded6-144">201</span></span>         | <span data-ttu-id="8ded6-145">Das Symbol Paket wurde erfolgreich per pushübertragung übermittelt.</span><span class="sxs-lookup"><span data-stu-id="8ded6-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="8ded6-146">400</span><span class="sxs-lookup"><span data-stu-id="8ded6-146">400</span></span>         | <span data-ttu-id="8ded6-147">Das angegebene Symbol Paket ist ungültig.</span><span class="sxs-lookup"><span data-stu-id="8ded6-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="8ded6-148">401</span><span class="sxs-lookup"><span data-stu-id="8ded6-148">401</span></span>         | <span data-ttu-id="8ded6-149">Der Benutzer ist nicht autorisiert, diese Aktion auszuführen.</span><span class="sxs-lookup"><span data-stu-id="8ded6-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="8ded6-150">404</span><span class="sxs-lookup"><span data-stu-id="8ded6-150">404</span></span>         | <span data-ttu-id="8ded6-151">Ein entsprechendes Paket mit der angegebenen ID und der angegebenen Version ist nicht vorhanden.</span><span class="sxs-lookup"><span data-stu-id="8ded6-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="8ded6-152">409</span><span class="sxs-lookup"><span data-stu-id="8ded6-152">409</span></span>         | <span data-ttu-id="8ded6-153">Ein Symbol Paket mit der angegebenen ID und Version wurde per Pushvorgang übermittelt, ist aber noch nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="8ded6-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="8ded6-154">413</span><span class="sxs-lookup"><span data-stu-id="8ded6-154">413</span></span>         | <span data-ttu-id="8ded6-155">Das Paket ist zu groß.</span><span class="sxs-lookup"><span data-stu-id="8ded6-155">The package is too large.</span></span>

