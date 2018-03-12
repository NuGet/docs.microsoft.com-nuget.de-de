---
title: Dienst-Index, die NuGet-API | Microsoft Docs
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
description: Der Dienst-Index ist der Einstiegspunkt der NuGet-HTTP-API und listet die Funktionen des Servers.
keywords: NuGet-API-Einstiegspunkt, NuGetA PI-Endpunkt-Ermittlung
ms.reviewer:
- karann
- unnir
ms.openlocfilehash: 8de0bc15edc358d091d84da54b8b67c085f29645
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="service-index"></a><span data-ttu-id="0e318-104">Dienst-index</span><span class="sxs-lookup"><span data-stu-id="0e318-104">Service index</span></span>

<span data-ttu-id="0e318-105">Der Dienst-Index ist ein JSON-Dokument, ist der Einstiegspunkt für die Quelle ein NuGet-Paket und eine Clientimplementierung der Paketquelle Funktionen ermitteln kann.</span><span class="sxs-lookup"><span data-stu-id="0e318-105">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="0e318-106">Der Dienst-Index ist ein JSON-Objekt, mit zwei erforderliche Eigenschaften: `version` (die Schemaversion des Indexes Service) und `resources` (die Endpunkte oder die Funktionen des die Paketquelle).</span><span class="sxs-lookup"><span data-stu-id="0e318-106">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="0e318-107">sich der NuGet.org-Dienst Index befindet sich unter `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="0e318-107">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="0e318-108">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="0e318-108">Versioning</span></span>

<span data-ttu-id="0e318-109">Die `version` Wert ist eine Zeichenfolge der SemVer 2.0.0-Schemakontexts Version gibt die Schemaversion des Dienst-Indexes an.</span><span class="sxs-lookup"><span data-stu-id="0e318-109">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="0e318-110">Die API ordnet an, dass die Versionszeichenfolge eine höhere Versionsnummer hat `3`.</span><span class="sxs-lookup"><span data-stu-id="0e318-110">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="0e318-111">Das IndexSchema Service nicht maßgebliche Änderungen vorgenommen werden, wird die Versionszeichenfolge Nebenversion erhöht werden.</span><span class="sxs-lookup"><span data-stu-id="0e318-111">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="0e318-112">Jede Ressource in die Dienst-Index ist unabhängig von der Dienst Index Schemaversion versionsspezifisch.</span><span class="sxs-lookup"><span data-stu-id="0e318-112">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="0e318-113">Die aktuelle Schemaversion ist `3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="0e318-113">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="0e318-114">Die `3.0.0` Version ist funktionell gleichwertig mit der älteren `3.0.0-beta.1` Version jedoch sollte bevorzugt werden, wie es deutlich stabile, definierte Schema kommuniziert.</span><span class="sxs-lookup"><span data-stu-id="0e318-114">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="0e318-115">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="0e318-115">HTTP methods</span></span>

<span data-ttu-id="0e318-116">Der Dienst-Index ist über HTTP-Methoden möglich `GET` und `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="0e318-116">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="0e318-117">Ressourcen</span><span class="sxs-lookup"><span data-stu-id="0e318-117">Resources</span></span>

<span data-ttu-id="0e318-118">Die `resources` -Eigenschaft enthält ein Array von Ressourcen, die von diesem Paketquelle unterstützt.</span><span class="sxs-lookup"><span data-stu-id="0e318-118">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="0e318-119">Ressource</span><span class="sxs-lookup"><span data-stu-id="0e318-119">Resource</span></span>

<span data-ttu-id="0e318-120">Eine Ressource ist ein Objekt in der `resources` Array.</span><span class="sxs-lookup"><span data-stu-id="0e318-120">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="0e318-121">Es stellt eine Möglichkeit, eine Paketquelle mit Versionsangabe.</span><span class="sxs-lookup"><span data-stu-id="0e318-121">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="0e318-122">Eine Ressource hat die folgenden Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="0e318-122">A resource has the following properties:</span></span>

<span data-ttu-id="0e318-123">name</span><span class="sxs-lookup"><span data-stu-id="0e318-123">Name</span></span>          | <span data-ttu-id="0e318-124">Typ</span><span class="sxs-lookup"><span data-stu-id="0e318-124">Type</span></span>   | <span data-ttu-id="0e318-125">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="0e318-125">Required</span></span> | <span data-ttu-id="0e318-126">Hinweise</span><span class="sxs-lookup"><span data-stu-id="0e318-126">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="0e318-127">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="0e318-127">string</span></span> | <span data-ttu-id="0e318-128">ja</span><span class="sxs-lookup"><span data-stu-id="0e318-128">yes</span></span>      | <span data-ttu-id="0e318-129">Die URL der Ressource</span><span class="sxs-lookup"><span data-stu-id="0e318-129">The URL to the resource</span></span>
@type         | <span data-ttu-id="0e318-130">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="0e318-130">string</span></span> | <span data-ttu-id="0e318-131">ja</span><span class="sxs-lookup"><span data-stu-id="0e318-131">yes</span></span>      | <span data-ttu-id="0e318-132">Eine Zeichenfolgenkonstante, die den Ressourcentyp darstellt.</span><span class="sxs-lookup"><span data-stu-id="0e318-132">A string constant representing the resource type</span></span>
<span data-ttu-id="0e318-133">Kommentar</span><span class="sxs-lookup"><span data-stu-id="0e318-133">comment</span></span>       | <span data-ttu-id="0e318-134">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="0e318-134">string</span></span> | <span data-ttu-id="0e318-135">Nein</span><span class="sxs-lookup"><span data-stu-id="0e318-135">no</span></span>       | <span data-ttu-id="0e318-136">Eine lesbare Beschreibung der Ressource</span><span class="sxs-lookup"><span data-stu-id="0e318-136">A human readable description of the resource</span></span>

<span data-ttu-id="0e318-137">Die `@id` ist eine URL, die muss absolut sein und muss entweder das HTTP- oder HTTPS-Schema vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="0e318-137">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="0e318-138">Die `@type` wird verwendet, um das bestimmte Protokoll verwenden, bei der Interaktion mit Ressourcen zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="0e318-138">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="0e318-139">Der Typ der Ressource ist eine nicht transparente Zeichenfolge, aber im Allgemeinen weist das Format:</span><span class="sxs-lookup"><span data-stu-id="0e318-139">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="0e318-140">Clients voraussichtlich hartcodieren der `@type` Werte, die sie kennen und effizient in eine Paketquelle Dienst Index gesucht werden.</span><span class="sxs-lookup"><span data-stu-id="0e318-140">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="0e318-141">Die genaue `@type` Werte heute werden aufgelistet, auf die einzelne Ressource Referenzdokumente aufgeführt, die der [Übersicht über die API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="0e318-141">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="0e318-142">In dieser Dokumentation wird die Dokumentation zu anderen Ressourcen im Wesentlichen durch gruppiert werden die `{RESOURCE_NAME}` gefunden, in die Dienst-Index, der Gruppierung nach Szenario entspricht.</span><span class="sxs-lookup"><span data-stu-id="0e318-142">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="0e318-143">Es ist nicht erforderlich, dass jede Ressource eine eindeutige weist `@id` oder `@type`.</span><span class="sxs-lookup"><span data-stu-id="0e318-143">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="0e318-144">Es ist Aufgabe der Clientimplementierung, um zu bestimmen, welche Ressourcen zu vor anderen bevorzugen.</span><span class="sxs-lookup"><span data-stu-id="0e318-144">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="0e318-145">Eine mögliche Implementierung ist, die die Ressourcen der denselben oder einen kompatiblen `@type` kann in einem Roundrobin bei einem Verbindungsfehler oder verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="0e318-145">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="0e318-146">Beispielanforderung</span><span class="sxs-lookup"><span data-stu-id="0e318-146">Sample request</span></span>

<span data-ttu-id="0e318-147">GET https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="0e318-147">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="0e318-148">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="0e318-148">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
