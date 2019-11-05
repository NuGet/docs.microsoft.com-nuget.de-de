---
title: Paket Details-URL-Vorlage, nuget-API
description: Mit der Vorlage "Paket Details-URL" können Clients in der Benutzeroberfläche einen Weblink zu weiteren Paket Details anzeigen.
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 3102cb9a20f354e92a0da8bba6457dc2ad0f0f2d
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610955"
---
# <a name="package-details-url-template"></a><span data-ttu-id="f36c4-103">Paket Details-URL-Vorlage</span><span class="sxs-lookup"><span data-stu-id="f36c4-103">Package details URL template</span></span>

<span data-ttu-id="f36c4-104">Es ist möglich, dass ein Client eine URL erstellt, die vom Benutzer verwendet werden kann, um weitere Paket Details in seinem Webbrowser anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="f36c4-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="f36c4-105">Dies ist hilfreich, wenn eine Paketquelle zusätzliche Informationen zu einem Paket anzeigen möchte, die möglicherweise nicht in den Bereich der nuget-Client Anwendung passen.</span><span class="sxs-lookup"><span data-stu-id="f36c4-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="f36c4-106">Die Ressource, die zum aufbauen dieser URL verwendet wird, ist die `PackageDetailsUriTemplate` Ressource, die im [Dienst Index](service-index.md)gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="f36c4-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="f36c4-107">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="f36c4-107">Versioning</span></span>

<span data-ttu-id="f36c4-108">Die folgenden `@type` Werte werden verwendet:</span><span class="sxs-lookup"><span data-stu-id="f36c4-108">The following `@type` values are used:</span></span>

<span data-ttu-id="f36c4-109">@type -Wert</span><span class="sxs-lookup"><span data-stu-id="f36c4-109">@type value</span></span>                     | <span data-ttu-id="f36c4-110">Notizen</span><span class="sxs-lookup"><span data-stu-id="f36c4-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="f36c4-111">Packagedetailsuritemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="f36c4-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="f36c4-112">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="f36c4-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="f36c4-113">URL-Vorlage</span><span class="sxs-lookup"><span data-stu-id="f36c4-113">URL template</span></span>

<span data-ttu-id="f36c4-114">Die URL für die folgende API ist der Wert der `@id`-Eigenschaft, die einem der oben erwähnten Ressourcen `@type` Werte zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="f36c4-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="f36c4-115">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="f36c4-115">HTTP methods</span></span>

<span data-ttu-id="f36c4-116">Obwohl der Client nicht dafür vorgesehen ist, Anforderungen an die Paket Details-URL für den Benutzer zu senden, sollte die Webseite die `GET`-Methode unterstützen, damit eine angeklickte URL problemlos in einem Webbrowser geöffnet werden kann.</span><span class="sxs-lookup"><span data-stu-id="f36c4-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="f36c4-117">Erstellen der URL</span><span class="sxs-lookup"><span data-stu-id="f36c4-117">Construct the URL</span></span>

<span data-ttu-id="f36c4-118">Wenn eine bekannte Paket-ID und-Version angegeben ist, kann die Client Implementierung eine URL für den Zugriff auf eine Weboberfläche erstellen.</span><span class="sxs-lookup"><span data-stu-id="f36c4-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="f36c4-119">Die Client Implementierung sollte diese erstellte URL (oder einen klickbaren Link) dem Benutzer anzeigen, sodass Sie einen Webbrowser für die URL öffnen und weitere Informationen zum Paket erhalten können.</span><span class="sxs-lookup"><span data-stu-id="f36c4-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="f36c4-120">Der Inhalt der Seite Paket Details wird von der Server Implementierung bestimmt.</span><span class="sxs-lookup"><span data-stu-id="f36c4-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="f36c4-121">Die URL muss eine absolute URL sein, und das Schema (Protokoll) muss https sein.</span><span class="sxs-lookup"><span data-stu-id="f36c4-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="f36c4-122">Der Wert der `@id` im Dienst Index ist eine URL-Zeichenfolge, die eines der folgenden Platzhalter Token enthält:</span><span class="sxs-lookup"><span data-stu-id="f36c4-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="f36c4-123">URL-Platzhalter</span><span class="sxs-lookup"><span data-stu-id="f36c4-123">URL placeholders</span></span>

<span data-ttu-id="f36c4-124">-Name</span><span class="sxs-lookup"><span data-stu-id="f36c4-124">Name</span></span>        | <span data-ttu-id="f36c4-125">Geben Sie Folgendes ein:</span><span class="sxs-lookup"><span data-stu-id="f36c4-125">Type</span></span>    | <span data-ttu-id="f36c4-126">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="f36c4-126">Required</span></span> | <span data-ttu-id="f36c4-127">Notizen</span><span class="sxs-lookup"><span data-stu-id="f36c4-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="f36c4-128">string</span><span class="sxs-lookup"><span data-stu-id="f36c4-128">string</span></span>  | <span data-ttu-id="f36c4-129">Nein</span><span class="sxs-lookup"><span data-stu-id="f36c4-129">no</span></span>       | <span data-ttu-id="f36c4-130">Die Paket-ID, für die Details zu erhalten sind.</span><span class="sxs-lookup"><span data-stu-id="f36c4-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="f36c4-131">string</span><span class="sxs-lookup"><span data-stu-id="f36c4-131">string</span></span>  | <span data-ttu-id="f36c4-132">Nein</span><span class="sxs-lookup"><span data-stu-id="f36c4-132">no</span></span>       | <span data-ttu-id="f36c4-133">Die Paketversion, für die Details zu erhalten sind</span><span class="sxs-lookup"><span data-stu-id="f36c4-133">The package version to get details for</span></span>

<span data-ttu-id="f36c4-134">Der Server sollte `{id}` und `{version}` Werte in beliebiger Groß-/Kleinschreibung akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="f36c4-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="f36c4-135">Außerdem sollte der Server nicht darauf achten, ob die Version [normalisiert](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers)ist.</span><span class="sxs-lookup"><span data-stu-id="f36c4-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="f36c4-136">Das heißt, der Server sollte auch akzeptieren, dass nicht normalisierte Versionen akzeptiert werden.</span><span class="sxs-lookup"><span data-stu-id="f36c4-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="f36c4-137">Beispielsweise sieht die Paket Detail Vorlage von nuget. org wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="f36c4-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="f36c4-138">Wenn die Client Implementierung einen Link zu den Paket Details für "nuget. Versionierung 4.3.0" anzeigen muss, würde Sie die folgende URL erstellen und für den Benutzer bereitstellen:</span><span class="sxs-lookup"><span data-stu-id="f36c4-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
