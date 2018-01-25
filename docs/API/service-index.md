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
ms.openlocfilehash: 9d0bb421c163520df4a1f0e9f3f71aab823aace3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="service-index"></a><span data-ttu-id="e4c21-104">Dienst-index</span><span class="sxs-lookup"><span data-stu-id="e4c21-104">Service index</span></span>

<span data-ttu-id="e4c21-105">Der Dienst-Index ist ein JSON-Dokument, ist der Einstiegspunkt für die Quelle ein NuGet-Paket und eine Clientimplementierung der Paketquelle Funktionen ermitteln kann.</span><span class="sxs-lookup"><span data-stu-id="e4c21-105">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="e4c21-106">Der Dienst-Index ist ein JSON-Objekt, mit zwei erforderliche Eigenschaften: `version` (die Schemaversion des Indexes Service) und `resources` (die Endpunkte oder die Funktionen des die Paketquelle).</span><span class="sxs-lookup"><span data-stu-id="e4c21-106">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="e4c21-107">sich der NuGet.org-Dienst Index befindet sich unter `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="e4c21-107">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="e4c21-108">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="e4c21-108">Versioning</span></span>

<span data-ttu-id="e4c21-109">Die `version` Wert ist eine Zeichenfolge der SemVer 2.0.0-Schemakontexts Version gibt die Schemaversion des Dienst-Indexes an.</span><span class="sxs-lookup"><span data-stu-id="e4c21-109">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span>
<span data-ttu-id="e4c21-110">Die API ordnet an, dass die Versionszeichenfolge eine höhere Versionsnummer hat `3`.</span><span class="sxs-lookup"><span data-stu-id="e4c21-110">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="e4c21-111">Das IndexSchema Service nicht maßgebliche Änderungen vorgenommen werden, wird die Versionszeichenfolge Nebenversion erhöht werden.</span><span class="sxs-lookup"><span data-stu-id="e4c21-111">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="e4c21-112">Jede Ressource in die Dienst-Index ist unabhängig von der Dienst Index Schemaversion versionsspezifisch.</span><span class="sxs-lookup"><span data-stu-id="e4c21-112">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="e4c21-113">Die aktuelle Schemaversion ist `3.0.0-beta.1`.</span><span class="sxs-lookup"><span data-stu-id="e4c21-113">The current schema version is `3.0.0-beta.1`.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e4c21-114">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="e4c21-114">HTTP methods</span></span>

<span data-ttu-id="e4c21-115">Der Dienst-Index ist über HTTP-Methoden möglich `GET` und `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="e4c21-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="e4c21-116">Ressourcen</span><span class="sxs-lookup"><span data-stu-id="e4c21-116">Resources</span></span>

<span data-ttu-id="e4c21-117">Die `resources` -Eigenschaft enthält ein Array von Ressourcen, die von diesem Paketquelle unterstützt.</span><span class="sxs-lookup"><span data-stu-id="e4c21-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="e4c21-118">Ressource</span><span class="sxs-lookup"><span data-stu-id="e4c21-118">Resource</span></span>

<span data-ttu-id="e4c21-119">Eine Ressource ist ein Objekt in der `resources` Array.</span><span class="sxs-lookup"><span data-stu-id="e4c21-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="e4c21-120">Es stellt eine Möglichkeit, eine Paketquelle mit Versionsangabe.</span><span class="sxs-lookup"><span data-stu-id="e4c21-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="e4c21-121">Eine Ressource hat die folgenden Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="e4c21-121">A resource has the following properties:</span></span>

<span data-ttu-id="e4c21-122">name</span><span class="sxs-lookup"><span data-stu-id="e4c21-122">Name</span></span>          | <span data-ttu-id="e4c21-123">Typ</span><span class="sxs-lookup"><span data-stu-id="e4c21-123">Type</span></span>   | <span data-ttu-id="e4c21-124">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="e4c21-124">Required</span></span> | <span data-ttu-id="e4c21-125">Hinweise</span><span class="sxs-lookup"><span data-stu-id="e4c21-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="e4c21-126">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="e4c21-126">string</span></span> | <span data-ttu-id="e4c21-127">ja</span><span class="sxs-lookup"><span data-stu-id="e4c21-127">yes</span></span>      | <span data-ttu-id="e4c21-128">Die URL der Ressource</span><span class="sxs-lookup"><span data-stu-id="e4c21-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="e4c21-129">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="e4c21-129">string</span></span> | <span data-ttu-id="e4c21-130">ja</span><span class="sxs-lookup"><span data-stu-id="e4c21-130">yes</span></span>      | <span data-ttu-id="e4c21-131">Eine Zeichenfolgenkonstante, die den Ressourcentyp darstellt.</span><span class="sxs-lookup"><span data-stu-id="e4c21-131">A string constant representing the resource type</span></span>
<span data-ttu-id="e4c21-132">Kommentar</span><span class="sxs-lookup"><span data-stu-id="e4c21-132">comment</span></span>       | <span data-ttu-id="e4c21-133">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="e4c21-133">string</span></span> | <span data-ttu-id="e4c21-134">Nein</span><span class="sxs-lookup"><span data-stu-id="e4c21-134">no</span></span>       | <span data-ttu-id="e4c21-135">Eine lesbare Beschreibung der Ressource</span><span class="sxs-lookup"><span data-stu-id="e4c21-135">A human readable description of the resource</span></span>

<span data-ttu-id="e4c21-136">Die `@id` ist eine URL, die muss absolut sein und muss entweder das HTTP- oder HTTPS-Schema vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="e4c21-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="e4c21-137">Die `@type` wird verwendet, um das bestimmte Protokoll verwenden, bei der Interaktion mit Ressourcen zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="e4c21-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="e4c21-138">Der Typ der Ressource ist eine nicht transparente Zeichenfolge, aber im Allgemeinen weist das Format:</span><span class="sxs-lookup"><span data-stu-id="e4c21-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="e4c21-139">Clients voraussichtlich hartcodieren der `@type` Werte, die sie kennen und effizient in eine Paketquelle Dienst Index gesucht werden.</span><span class="sxs-lookup"><span data-stu-id="e4c21-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="e4c21-140">Die genaue `@type` Werte heute werden aufgelistet, auf die einzelne Ressource Referenzdokumente aufgeführt, die der [Übersicht über die API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="e4c21-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="e4c21-141">In dieser Dokumentation wird die Dokumentation zu anderen Ressourcen im Wesentlichen durch gruppiert werden die `{RESOURCE_NAME}` gefunden, in die Dienst-Index, der Gruppierung nach Szenario entspricht.</span><span class="sxs-lookup"><span data-stu-id="e4c21-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="e4c21-142">Es ist nicht erforderlich, dass jede Ressource eine eindeutige weist `@id` oder `@type`.</span><span class="sxs-lookup"><span data-stu-id="e4c21-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="e4c21-143">Es ist Aufgabe der Clientimplementierung, um zu bestimmen, welche Ressourcen zu vor anderen bevorzugen.</span><span class="sxs-lookup"><span data-stu-id="e4c21-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="e4c21-144">Eine mögliche Implementierung ist, die die Ressourcen der denselben oder einen kompatiblen `@type` kann in einem Roundrobin bei einem Verbindungsfehler oder verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="e4c21-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e4c21-145">Beispielanforderung</span><span class="sxs-lookup"><span data-stu-id="e4c21-145">Sample request</span></span>

<span data-ttu-id="e4c21-146">GET https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="e4c21-146">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="e4c21-147">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="e4c21-147">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
