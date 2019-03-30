---
title: Paket-Details-URL-Vorlage, NuGet-API
description: Die Paket-Details-URL-Vorlage kann Clients in ihrer Benutzeroberfläche, die eine Web-link auf Weitere Paketinformationen zu anzeigen
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638073"
---
# <a name="package-details-url-template"></a><span data-ttu-id="322e6-103">Paket-Details-URL-Vorlage</span><span class="sxs-lookup"><span data-stu-id="322e6-103">Package details URL template</span></span>

<span data-ttu-id="322e6-104">Es ist möglich, dass ein Client eine URL zu erstellen, die vom Benutzer verwendet werden können, um weitere Paketdetails in ihrem Webbrowser anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="322e6-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="322e6-105">Dies ist nützlich, wenn eine Paketquelle will, um zusätzliche Informationen zu einem Paket, die nicht passen möglicherweise innerhalb des Bereichs, was die NuGet-Client-Anwendung zeigt anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="322e6-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="322e6-106">Die Ressource, die zum Erstellen von dieser URL ist die `PackageDetailsUriTemplate` Ressource finden Sie in der [dienstindex](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="322e6-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="322e6-107">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="322e6-107">Versioning</span></span>

<span data-ttu-id="322e6-108">Die folgenden `@type` Werte werden verwendet:</span><span class="sxs-lookup"><span data-stu-id="322e6-108">The following `@type` values are used:</span></span>

<span data-ttu-id="322e6-109">@type-Wert</span><span class="sxs-lookup"><span data-stu-id="322e6-109">@type value</span></span>                     | <span data-ttu-id="322e6-110">Hinweise</span><span class="sxs-lookup"><span data-stu-id="322e6-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="322e6-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="322e6-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="322e6-112">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="322e6-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="322e6-113">URL-Vorlage</span><span class="sxs-lookup"><span data-stu-id="322e6-113">URL template</span></span>

<span data-ttu-id="322e6-114">Die URL für die folgende API wird der Wert des der `@id` Eigenschaft, die einer der oben genannten Ressource zugeordneten `@type` Werte.</span><span class="sxs-lookup"><span data-stu-id="322e6-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="322e6-115">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="322e6-115">HTTP methods</span></span>

<span data-ttu-id="322e6-116">Der Client nicht gedacht ist, um Anforderungen an die URL des Pakets Details im Auftrag des Benutzers zu senden, sollte die Webseite unterstützen die `GET` Methode, um eine geklickte URL ganz einfach in einem Webbrowser geöffnet werden können.</span><span class="sxs-lookup"><span data-stu-id="322e6-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="322e6-117">Erstellen Sie die URL</span><span class="sxs-lookup"><span data-stu-id="322e6-117">Construct the URL</span></span>

<span data-ttu-id="322e6-118">Wenn eine bekannte Paket-ID und Version, kann die Client-Implementierung eine URL für den Zugriff auf eine Weboberfläche erstellen.</span><span class="sxs-lookup"><span data-stu-id="322e6-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="322e6-119">Die Clientimplementierung sollte diese erstellte URL (oder einen klickbaren Link) um dem Benutzer um einen Webbrowser an die URL zu öffnen und Weitere Informationen zu dem Paket angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="322e6-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="322e6-120">Den Inhalt der Detailseite des Pakets wird durch die Implementierung der Server bestimmt.</span><span class="sxs-lookup"><span data-stu-id="322e6-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="322e6-121">Die URL muss eine absolute URL sein, und die (Protokoll)-Schema muss HTTPS sein.</span><span class="sxs-lookup"><span data-stu-id="322e6-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="322e6-122">Der Wert des der `@id` im Dienst-Index ist eine URL-Zeichenfolge, die mit einem der folgenden Platzhalter-Token:</span><span class="sxs-lookup"><span data-stu-id="322e6-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="322e6-123">URL-Platzhalter</span><span class="sxs-lookup"><span data-stu-id="322e6-123">URL placeholders</span></span>

<span data-ttu-id="322e6-124">Name</span><span class="sxs-lookup"><span data-stu-id="322e6-124">Name</span></span>        | <span data-ttu-id="322e6-125">Typ</span><span class="sxs-lookup"><span data-stu-id="322e6-125">Type</span></span>    | <span data-ttu-id="322e6-126">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="322e6-126">Required</span></span> | <span data-ttu-id="322e6-127">Hinweise</span><span class="sxs-lookup"><span data-stu-id="322e6-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="322e6-128">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="322e6-128">string</span></span>  | <span data-ttu-id="322e6-129">Nein</span><span class="sxs-lookup"><span data-stu-id="322e6-129">no</span></span>       | <span data-ttu-id="322e6-130">Die Paket-ID zum Abrufen von Details für</span><span class="sxs-lookup"><span data-stu-id="322e6-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="322e6-131">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="322e6-131">string</span></span>  | <span data-ttu-id="322e6-132">Nein</span><span class="sxs-lookup"><span data-stu-id="322e6-132">no</span></span>       | <span data-ttu-id="322e6-133">Die Paketversion, um Details zu erhalten</span><span class="sxs-lookup"><span data-stu-id="322e6-133">The package version to get details for</span></span>

<span data-ttu-id="322e6-134">Es sollte der Server akzeptiert `{id}` und `{version}` Werte mit jedem Groß-/Kleinschreibung.</span><span class="sxs-lookup"><span data-stu-id="322e6-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="322e6-135">Darüber hinaus der Server sollte nicht anfällig für gibt an, ob die Version ist [normalisierte](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="322e6-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="322e6-136">Das heißt, der Server annehmen sollte auch nicht normalisierte Versionen akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="322e6-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="322e6-137">Beispielsweise sieht die Nuget.org Paket-Details-Vorlage wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="322e6-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="322e6-138">Wenn die Clientimplementierung einen Link auf die Paketdetails für NuGet.Versioning 4.3.0 angezeigt werden soll muss, würde er erzeugt die folgende URL, und geben Sie sie für den Benutzer:</span><span class="sxs-lookup"><span data-stu-id="322e6-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
