---
title: Dienst Index, nuget-API
description: Der Dienst Index ist der Einstiegspunkt der nuget-HTTP-API und listet die Funktionen des Servers auf.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775360"
---
# <a name="service-index"></a><span data-ttu-id="82ba4-103">Dienstindex</span><span class="sxs-lookup"><span data-stu-id="82ba4-103">Service index</span></span>

<span data-ttu-id="82ba4-104">Der Dienst Index ist ein JSON-Dokument, das den Einstiegspunkt für eine nuget-Paketquelle ist und es einer Client Implementierung ermöglicht, die Funktionen der Paketquelle zu ermitteln.</span><span class="sxs-lookup"><span data-stu-id="82ba4-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="82ba4-105">Der Dienst Index ist ein JSON-Objekt mit zwei erforderlichen Eigenschaften: `version` (die Schema Version des Dienst Indexes) und `resources`  (die Endpunkte oder Funktionen der Paketquelle).</span><span class="sxs-lookup"><span data-stu-id="82ba4-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="82ba4-106">der Dienst Index von nuget. org befindet sich unter `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="82ba4-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="82ba4-107">Versionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="82ba4-107">Versioning</span></span>

<span data-ttu-id="82ba4-108">Der `version` Wert ist eine zu semver 2.0.0 ausführbare Versions Zeichenfolge, die die Schema Version des Dienst Indexes angibt.</span><span class="sxs-lookup"><span data-stu-id="82ba4-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="82ba4-109">Die API gibt an, dass die Versions Zeichenfolge eine Hauptversionsnummer von aufweist `3` .</span><span class="sxs-lookup"><span data-stu-id="82ba4-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="82ba4-110">Da nicht unterbrechende Änderungen am Dienst Index Schema vorgenommen werden, wird die neben Version der Versions Zeichenfolge erweitert.</span><span class="sxs-lookup"><span data-stu-id="82ba4-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="82ba4-111">Jede Ressource im Dienst Index wird unabhängig von der Dienst Index Schema-Version versioniert.</span><span class="sxs-lookup"><span data-stu-id="82ba4-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="82ba4-112">Die aktuelle Schema Version ist `3.0.0` .</span><span class="sxs-lookup"><span data-stu-id="82ba4-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="82ba4-113">Die `3.0.0` Version ist funktional gleichwertig mit der älteren `3.0.0-beta.1` Version, sollte aber bevorzugt werden, da Sie das stabile, definierte Schema deutlicher kommuniziert.</span><span class="sxs-lookup"><span data-stu-id="82ba4-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="82ba4-114">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="82ba4-114">HTTP methods</span></span>

<span data-ttu-id="82ba4-115">Auf den Dienst Index kann mithilfe der HTTP `GET` -Methoden und zugegriffen werden `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="82ba4-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="82ba4-116">Ressourcen</span><span class="sxs-lookup"><span data-stu-id="82ba4-116">Resources</span></span>

<span data-ttu-id="82ba4-117">Die- `resources` Eigenschaft enthält ein Array von Ressourcen, die von dieser Paketquelle unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="82ba4-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="82ba4-118">Resource</span><span class="sxs-lookup"><span data-stu-id="82ba4-118">Resource</span></span>

<span data-ttu-id="82ba4-119">Eine Ressource ist ein Objekt im `resources` Array.</span><span class="sxs-lookup"><span data-stu-id="82ba4-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="82ba4-120">Sie stellt eine versionierte Funktion einer Paketquelle dar.</span><span class="sxs-lookup"><span data-stu-id="82ba4-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="82ba4-121">Eine Ressource verfügt über die folgenden Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="82ba4-121">A resource has the following properties:</span></span>

<span data-ttu-id="82ba4-122">Name</span><span class="sxs-lookup"><span data-stu-id="82ba4-122">Name</span></span>          | <span data-ttu-id="82ba4-123">Typ</span><span class="sxs-lookup"><span data-stu-id="82ba4-123">Type</span></span>   | <span data-ttu-id="82ba4-124">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="82ba4-124">Required</span></span> | <span data-ttu-id="82ba4-125">Notizen</span><span class="sxs-lookup"><span data-stu-id="82ba4-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="82ba4-126">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="82ba4-126">string</span></span> | <span data-ttu-id="82ba4-127">ja</span><span class="sxs-lookup"><span data-stu-id="82ba4-127">yes</span></span>      | <span data-ttu-id="82ba4-128">Die URL der Ressource.</span><span class="sxs-lookup"><span data-stu-id="82ba4-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="82ba4-129">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="82ba4-129">string</span></span> | <span data-ttu-id="82ba4-130">ja</span><span class="sxs-lookup"><span data-stu-id="82ba4-130">yes</span></span>      | <span data-ttu-id="82ba4-131">Eine Zeichen folgen Konstante, die den Ressourcentyp darstellt.</span><span class="sxs-lookup"><span data-stu-id="82ba4-131">A string constant representing the resource type</span></span>
<span data-ttu-id="82ba4-132">comment</span><span class="sxs-lookup"><span data-stu-id="82ba4-132">comment</span></span>       | <span data-ttu-id="82ba4-133">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="82ba4-133">string</span></span> | <span data-ttu-id="82ba4-134">nein</span><span class="sxs-lookup"><span data-stu-id="82ba4-134">no</span></span>       | <span data-ttu-id="82ba4-135">Eine lesbare Beschreibung der Ressource.</span><span class="sxs-lookup"><span data-stu-id="82ba4-135">A human readable description of the resource</span></span>

<span data-ttu-id="82ba4-136">Bei `@id` handelt es sich um eine URL, die absolut sein muss und entweder über das http-oder HTTPS-Schema verfügen muss.</span><span class="sxs-lookup"><span data-stu-id="82ba4-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="82ba4-137">`@type`Wird verwendet, um das Protokoll zu identifizieren, das bei der Interaktion mit der Ressource verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="82ba4-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="82ba4-138">Der Typ der Ressource ist eine nicht transparente Zeichenfolge, hat jedoch im Allgemeinen das folgende Format:</span><span class="sxs-lookup"><span data-stu-id="82ba4-138">The type of the resource is an opaque string but generally has the format:</span></span>

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

<span data-ttu-id="82ba4-139">Clients sollten die `@type` Werte, die Sie verstehen, hart codieren und im Dienst Index einer Paketquelle nachschlagen.</span><span class="sxs-lookup"><span data-stu-id="82ba4-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="82ba4-140">Die aktuell `@type` verwendeten Werte werden in den einzelnen Ressourcen Verweis Dokumenten aufgelistet, die in der API- [Übersicht](overview.md#resources-and-schema)aufgeführt sind.</span><span class="sxs-lookup"><span data-stu-id="82ba4-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="82ba4-141">Im Rahmen dieser Dokumentation wird die Dokumentation zu verschiedenen Ressourcen im Wesentlichen nach dem `{RESOURCE_NAME}` im Dienst Index gefundenen gruppiert, der der Gruppierung nach Szenario entspricht.</span><span class="sxs-lookup"><span data-stu-id="82ba4-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="82ba4-142">Es ist nicht erforderlich, dass jede Ressource über eine eindeutige `@id` oder verfügt `@type` .</span><span class="sxs-lookup"><span data-stu-id="82ba4-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="82ba4-143">Es liegt an der Client Implementierung, die bevorzugte Ressource zu bestimmen.</span><span class="sxs-lookup"><span data-stu-id="82ba4-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="82ba4-144">Eine mögliche Implementierung besteht darin, dass Ressourcen des gleichen oder kompatiblen bei `@type` Verbindungsfehlern oder Server Fehlern im Roundrobin-Verfahren verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="82ba4-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="82ba4-145">Beispiel für eine Anforderung</span><span class="sxs-lookup"><span data-stu-id="82ba4-145">Sample request</span></span>

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a><span data-ttu-id="82ba4-146">Beispiel für eine Antwort</span><span class="sxs-lookup"><span data-stu-id="82ba4-146">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
