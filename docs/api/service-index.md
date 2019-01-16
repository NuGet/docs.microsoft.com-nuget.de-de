---
title: -Dienst Index, NuGet-API
description: Der dienstindex ist der Einstiegspunkt, der die NuGet-HTTP-API und listet die Funktionen des Servers.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1dcfb87690b728280b494d4434f9c1d7ee7a7e74
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324720"
---
# <a name="service-index"></a><span data-ttu-id="28084-103">Dienstindex</span><span class="sxs-lookup"><span data-stu-id="28084-103">Service index</span></span>

<span data-ttu-id="28084-104">Dienstindex ist ein JSON-Dokument, ist der Einstiegspunkt für eine NuGet-Paketquelle und eine Client-Implementierung der Paketquelle Funktionen ermitteln kann.</span><span class="sxs-lookup"><span data-stu-id="28084-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="28084-105">Der dienstindex ist ein JSON-Objekt mit zwei erforderliche Eigenschaften: `version` (die Schemaversion des dienstindex) und `resources` (Endpunkte oder Funktionen der Paketquelle).</span><span class="sxs-lookup"><span data-stu-id="28084-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="28084-106">NuGet.org dienstindex befindet sich unter `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="28084-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="28084-107">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="28084-107">Versioning</span></span>

<span data-ttu-id="28084-108">Die `version` Wert ist eine analysierbare SemVer 2.0.0-Versionszeichenfolge, womit die Schemaversion der dienstindex.</span><span class="sxs-lookup"><span data-stu-id="28084-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="28084-109">Die API erfordert, dass die version-Zeichenfolge die Hautpversionsnummer `3` hat.</span><span class="sxs-lookup"><span data-stu-id="28084-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="28084-110">Wenn API-kompatible Änderungen am Schema des Dienstindex durchgeführt werden, wird die Nebenversion der version-Zeichenfolge erhöht.</span><span class="sxs-lookup"><span data-stu-id="28084-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="28084-111">Jede Ressource im dienstindex ist unabhängig von der Schemaversion des Dienst-Index mit Versionsangabe.</span><span class="sxs-lookup"><span data-stu-id="28084-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="28084-112">Die aktuelle Version des Datenbankschemas ist `3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="28084-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="28084-113">Die `3.0.0` Version ist funktionell gleichwertig mit dem älteren `3.0.0-beta.1` Version aber sollten bevorzugt werden, wie das stabile, definierte Schema deutlicher kommuniziert.</span><span class="sxs-lookup"><span data-stu-id="28084-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="28084-114">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="28084-114">HTTP methods</span></span>

<span data-ttu-id="28084-115">Dienstindex kann zugegriffen werden, mithilfe von HTTP-Methoden `GET` und `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="28084-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="28084-116">Ressourcen</span><span class="sxs-lookup"><span data-stu-id="28084-116">Resources</span></span>

<span data-ttu-id="28084-117">Die `resources` Eigenschaft enthält eine Reihe von Ressourcen, die von diesem Paketquelle unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="28084-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="28084-118">Ressource</span><span class="sxs-lookup"><span data-stu-id="28084-118">Resource</span></span>

<span data-ttu-id="28084-119">Eine Ressource ist ein Objekt in der `resources` Array.</span><span class="sxs-lookup"><span data-stu-id="28084-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="28084-120">Es stellt eine Funktion mit versionsverwaltung durch das der Paketquelle dar.</span><span class="sxs-lookup"><span data-stu-id="28084-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="28084-121">Eine Ressource hat die folgenden Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="28084-121">A resource has the following properties:</span></span>

<span data-ttu-id="28084-122">name</span><span class="sxs-lookup"><span data-stu-id="28084-122">Name</span></span>          | <span data-ttu-id="28084-123">Typ</span><span class="sxs-lookup"><span data-stu-id="28084-123">Type</span></span>   | <span data-ttu-id="28084-124">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="28084-124">Required</span></span> | <span data-ttu-id="28084-125">Hinweise</span><span class="sxs-lookup"><span data-stu-id="28084-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="28084-126">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="28084-126">string</span></span> | <span data-ttu-id="28084-127">ja</span><span class="sxs-lookup"><span data-stu-id="28084-127">yes</span></span>      | <span data-ttu-id="28084-128">Die URL der Ressource</span><span class="sxs-lookup"><span data-stu-id="28084-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="28084-129">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="28084-129">string</span></span> | <span data-ttu-id="28084-130">ja</span><span class="sxs-lookup"><span data-stu-id="28084-130">yes</span></span>      | <span data-ttu-id="28084-131">Eine Zeichenfolgenkonstante, die den Ressourcentyp darstellt.</span><span class="sxs-lookup"><span data-stu-id="28084-131">A string constant representing the resource type</span></span>
<span data-ttu-id="28084-132">Kommentar</span><span class="sxs-lookup"><span data-stu-id="28084-132">comment</span></span>       | <span data-ttu-id="28084-133">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="28084-133">string</span></span> | <span data-ttu-id="28084-134">Nein</span><span class="sxs-lookup"><span data-stu-id="28084-134">no</span></span>       | <span data-ttu-id="28084-135">Eine lesbare Beschreibung der Ressource</span><span class="sxs-lookup"><span data-stu-id="28084-135">A human readable description of the resource</span></span>

<span data-ttu-id="28084-136">Die `@id` ist eine URL, die muss absolut sein und muss entweder das HTTP- oder HTTPS-Schema aufweisen.</span><span class="sxs-lookup"><span data-stu-id="28084-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="28084-137">Die `@type` wird verwendet, um das bestimmte Protokoll verwenden, bei der Interaktion mit Ressourcen zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="28084-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="28084-138">Der Typ der Ressource ist eine nicht transparente Zeichenfolge, aber im Allgemeinen weist das Format auf:</span><span class="sxs-lookup"><span data-stu-id="28084-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="28084-139">Clients wird vorausgesetzt, durch hartcodierung der `@type` Werte, die diese Partner kennen, und suchen sie in eine Paketquelle dienstindex.</span><span class="sxs-lookup"><span data-stu-id="28084-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="28084-140">Die genaue `@type` Werte heute werden aufgezählt, auf die einzelne Ressource Referenzdokumente aufgeführt, die der [-API – Übersicht](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="28084-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="28084-141">Aus Gründen der dieser Dokumentation wird die Dokumentation zu anderen Ressourcen im Wesentlichen nach gruppiert werden die `{RESOURCE_NAME}` in dienstindex handelt es sich analog zur Gruppierung nach Szenario gefunden.</span><span class="sxs-lookup"><span data-stu-id="28084-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="28084-142">Es ist nicht erforderlich, dass jede Ressource eine eindeutige hat `@id` oder `@type`.</span><span class="sxs-lookup"><span data-stu-id="28084-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="28084-143">Es ist Aufgabe der Clientimplementierung, um zu bestimmen, welche Ressourcen vor anderen bevorzugen.</span><span class="sxs-lookup"><span data-stu-id="28084-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="28084-144">Eine mögliche Implementierung ist, die Ressourcen, die von der gleichen oder einen kompatiblen `@type` in eine Roundrobin-bei einem Verbindungsfehler oder verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="28084-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="28084-145">Beispiel für eine Anforderung</span><span class="sxs-lookup"><span data-stu-id="28084-145">Sample request</span></span>

    GET https://api.nuget.org/v3/index.json

### <a name="sample-response"></a><span data-ttu-id="28084-146">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="28084-146">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
