---
title: Push-Symbolpakete, NuGet-API | Microsoft-Dokumentation
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Publish-Diensts kann Clients neue Symbolpakete zu veröffentlichen.
keywords: NuGet-API-Push-Symbolpaket
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580413"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="7c629-104">Push-Symbolpaketen</span><span class="sxs-lookup"><span data-stu-id="7c629-104">Push Symbol Packages</span></span>

<span data-ttu-id="7c629-105">Es ist möglich, Push-Symbolpakete ([Snupkg](../create-packages/Symbol-Packages-snupkg.md)) mithilfe der NuGet-V3-API.</span><span class="sxs-lookup"><span data-stu-id="7c629-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="7c629-106">Diese Vorgänge sind basierend auf den `SymbolPackagePublish` Ressource finden Sie in der [dienstindex](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="7c629-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="7c629-107">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="7c629-107">Versioning</span></span>

<span data-ttu-id="7c629-108">Die folgenden `@type` Wert wird verwendet:</span><span class="sxs-lookup"><span data-stu-id="7c629-108">The following `@type` value is used:</span></span>

<span data-ttu-id="7c629-109">@type-Wert</span><span class="sxs-lookup"><span data-stu-id="7c629-109">@type value</span></span>                 | <span data-ttu-id="7c629-110">Hinweise</span><span class="sxs-lookup"><span data-stu-id="7c629-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="7c629-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="7c629-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="7c629-112">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="7c629-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="7c629-113">Basis-URL</span><span class="sxs-lookup"><span data-stu-id="7c629-113">Base URL</span></span>

<span data-ttu-id="7c629-114">Die base-URL für die folgenden APIs ist der Wert des der `@id` Eigenschaft der `SymbolPackagePublish/4.9.0` Ressource in der Paketquelle [dienstindex](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="7c629-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="7c629-115">Die folgende Dokumentation dient Nuget.org URL.</span><span class="sxs-lookup"><span data-stu-id="7c629-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="7c629-116">Betrachten Sie `https://www.nuget.org/api/v2/symbolpackage` als Platzhalter für die `@id` Wert in der dienstindex gefunden.</span><span class="sxs-lookup"><span data-stu-id="7c629-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="7c629-117">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="7c629-117">HTTP methods</span></span>

<span data-ttu-id="7c629-118">Die `PUT` HTTP-Methode wird durch diese Ressource unterstützt.</span><span class="sxs-lookup"><span data-stu-id="7c629-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="7c629-119">Ein Symbolpaket mithilfe von Push übertragen</span><span class="sxs-lookup"><span data-stu-id="7c629-119">Push a symbol package</span></span>

<span data-ttu-id="7c629-120">NuGet.org unterstützt Ablegevorgänge neues Format für die Symbol-Pakete ([Snupkg](../create-packages/Symbol-Packages-snupkg.md)) mithilfe der folgenden-API.</span><span class="sxs-lookup"><span data-stu-id="7c629-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="7c629-121">Symbolpakete, mit der gleichen ID und Version können mehrere Male gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="7c629-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="7c629-122">Ein Symbolpaket werden in den folgenden Fällen zurückgewiesen.</span><span class="sxs-lookup"><span data-stu-id="7c629-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="7c629-123">Ein Paket mit der gleichen ID und Version ist nicht vorhanden.</span><span class="sxs-lookup"><span data-stu-id="7c629-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="7c629-124">Ein Symbolpaket, mit der gleichen ID und Version mithilfe von Push übertragen wurde, aber es wurde noch nicht veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="7c629-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="7c629-125">Das Symbolpaket ([Snupkg](../create-packages/Symbol-Packages-snupkg.md)) ist ungültig (finden Sie unter [symbol Paket Einschränkungen](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="7c629-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="7c629-126">Anforderungsparameter</span><span class="sxs-lookup"><span data-stu-id="7c629-126">Request parameters</span></span>

<span data-ttu-id="7c629-127">name</span><span class="sxs-lookup"><span data-stu-id="7c629-127">Name</span></span>           | <span data-ttu-id="7c629-128">In</span><span class="sxs-lookup"><span data-stu-id="7c629-128">In</span></span>     | <span data-ttu-id="7c629-129">Typ</span><span class="sxs-lookup"><span data-stu-id="7c629-129">Type</span></span>   | <span data-ttu-id="7c629-130">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="7c629-130">Required</span></span> | <span data-ttu-id="7c629-131">Hinweise</span><span class="sxs-lookup"><span data-stu-id="7c629-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="7c629-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="7c629-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="7c629-133">Header</span><span class="sxs-lookup"><span data-stu-id="7c629-133">Header</span></span> | <span data-ttu-id="7c629-134">String</span><span class="sxs-lookup"><span data-stu-id="7c629-134">string</span></span> | <span data-ttu-id="7c629-135">ja</span><span class="sxs-lookup"><span data-stu-id="7c629-135">yes</span></span>      | <span data-ttu-id="7c629-136">Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="7c629-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="7c629-137">Die API-Schlüssel ist eine nicht transparente Zeichenfolge, aus der Paketquelle vom Benutzer abgerufen und in den Client konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="7c629-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="7c629-138">Kein besonderes Zeichenfolgenformat wird vorgeschrieben, aber der API-Schlüssel sollte nicht länger als eine angemessene Größe für HTTP-Headerwerte.</span><span class="sxs-lookup"><span data-stu-id="7c629-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="7c629-139">Anforderungstext</span><span class="sxs-lookup"><span data-stu-id="7c629-139">Request body</span></span>

<span data-ttu-id="7c629-140">Der Anforderungstext für die Symbol-Push ist identisch mit dem Anforderungstext, der eine Anforderung zum Paketimport Push (finden Sie unter [Push-Paket, und Löschen von](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="7c629-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="7c629-141">Antwort</span><span class="sxs-lookup"><span data-stu-id="7c629-141">Response</span></span>

<span data-ttu-id="7c629-142">Statuscode</span><span class="sxs-lookup"><span data-stu-id="7c629-142">Status Code</span></span> | <span data-ttu-id="7c629-143">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="7c629-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="7c629-144">201</span><span class="sxs-lookup"><span data-stu-id="7c629-144">201</span></span>         | <span data-ttu-id="7c629-145">Das Symbolpaket wurde erfolgreich per Push übertragen.</span><span class="sxs-lookup"><span data-stu-id="7c629-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="7c629-146">400</span><span class="sxs-lookup"><span data-stu-id="7c629-146">400</span></span>         | <span data-ttu-id="7c629-147">Das angegebene Symbolpaket ist ungültig.</span><span class="sxs-lookup"><span data-stu-id="7c629-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="7c629-148">401</span><span class="sxs-lookup"><span data-stu-id="7c629-148">401</span></span>         | <span data-ttu-id="7c629-149">Der Benutzer ist nicht zum Ausführen dieser Aktion autorisiert.</span><span class="sxs-lookup"><span data-stu-id="7c629-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="7c629-150">404</span><span class="sxs-lookup"><span data-stu-id="7c629-150">404</span></span>         | <span data-ttu-id="7c629-151">Eine entsprechende Paket mit der angegebenen ID und Version ist nicht vorhanden.</span><span class="sxs-lookup"><span data-stu-id="7c629-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="7c629-152">409</span><span class="sxs-lookup"><span data-stu-id="7c629-152">409</span></span>         | <span data-ttu-id="7c629-153">Ein Symbolpaket, mit der angegebenen ID und Version wurde per Push übertragen, aber es ist noch nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="7c629-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="7c629-154">413</span><span class="sxs-lookup"><span data-stu-id="7c629-154">413</span></span>         | <span data-ttu-id="7c629-155">Das Paket ist zu groß.</span><span class="sxs-lookup"><span data-stu-id="7c629-155">The package is too large.</span></span>

