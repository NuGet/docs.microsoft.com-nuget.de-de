---
title: Missbrauch URL Berichtsvorlage, NuGet-API
description: Der Bericht Missbrauch URL-Vorlage kann Clients einen Missbrauch Berichtslink in ihre Benutzeroberfläche anzeigen.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 15cf0953391489d9dd9b5d609c3f4c8f66748f19
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
ms.locfileid: "31818466"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="18892-103">Berichtsvorlage Missbrauch-URL</span><span class="sxs-lookup"><span data-stu-id="18892-103">Report abuse URL template</span></span>

<span data-ttu-id="18892-104">Es ist möglich, dass ein Client eine URL zu erstellen, die vom Benutzer zum Melden des Missbrauchs zu einem bestimmten Paket verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="18892-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="18892-105">Dies ist hilfreich, wenn eine Paketquelle möchte, um alle Clients Erfahrungen (auch 3rd Party) Missbrauch Berichte für die Paketquelle delegieren zu erzielen.</span><span class="sxs-lookup"><span data-stu-id="18892-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="18892-106">Die Ressource für das Abrufen von Paketinhalt verwendet die `ReportAbuseUriTemplate` Ressource gefunden, der [Dienst Index](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="18892-106">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="18892-107">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="18892-107">Versioning</span></span>

<span data-ttu-id="18892-108">Die folgenden `@type` Werte werden verwendet:</span><span class="sxs-lookup"><span data-stu-id="18892-108">The following `@type` values are used:</span></span>

<span data-ttu-id="18892-109">@type-Wert</span><span class="sxs-lookup"><span data-stu-id="18892-109">@type value</span></span>                       | <span data-ttu-id="18892-110">Hinweise</span><span class="sxs-lookup"><span data-stu-id="18892-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="18892-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="18892-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="18892-112">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="18892-112">The initial release</span></span>
<span data-ttu-id="18892-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="18892-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="18892-114">Alias der `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="18892-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="18892-115">URL-Vorlage</span><span class="sxs-lookup"><span data-stu-id="18892-115">URL template</span></span>

<span data-ttu-id="18892-116">Die URL für die folgende API wird der Wert von der `@id` mit einem der oben genannten Ressource verknüpfte Eigenschaft `@type` Werte.</span><span class="sxs-lookup"><span data-stu-id="18892-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="18892-117">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="18892-117">HTTP methods</span></span>

<span data-ttu-id="18892-118">Obwohl der Client nicht vorgesehen ist, damit Anforderungen an die URL des Berichts Missbrauch im Namen des Benutzers zu senden, sollte die Webseite unterstützen die `GET` Methode, um eine URL geklickt wurde, problemlos in einem Webbrowser geöffnet werden zuzulassen.</span><span class="sxs-lookup"><span data-stu-id="18892-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="18892-119">Die URL zu erstellen</span><span class="sxs-lookup"><span data-stu-id="18892-119">Construct the URL</span></span>

<span data-ttu-id="18892-120">Erteilt ein bekannter Paket-ID und eine Version, kann die Clientimplementierung eine URL verwendet, um eine Weboberfläche zugreifen zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="18892-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="18892-121">Die Clientimplementierung sollte diese erstellte URL (oder einen klickbaren Link) für den Benutzer, die sie zulassen, dass auf einen Webbrowser an die URL öffnen, und stellen alle erforderlichen Missbrauch Bericht anzeigen.</span><span class="sxs-lookup"><span data-stu-id="18892-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="18892-122">Die Implementierung des Formulars Bericht Missbrauch richtet sich nach der Server-Implementierung.</span><span class="sxs-lookup"><span data-stu-id="18892-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="18892-123">Der Wert, der die `@id` ist eine URL-Zeichenfolge, die keines der folgenden Platzhalter-Token enthält:</span><span class="sxs-lookup"><span data-stu-id="18892-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="18892-124">URL-Platzhalter</span><span class="sxs-lookup"><span data-stu-id="18892-124">URL placeholders</span></span>

<span data-ttu-id="18892-125">name</span><span class="sxs-lookup"><span data-stu-id="18892-125">Name</span></span>        | <span data-ttu-id="18892-126">Typ</span><span class="sxs-lookup"><span data-stu-id="18892-126">Type</span></span>    | <span data-ttu-id="18892-127">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="18892-127">Required</span></span> | <span data-ttu-id="18892-128">Hinweise</span><span class="sxs-lookup"><span data-stu-id="18892-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="18892-129">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="18892-129">string</span></span>  | <span data-ttu-id="18892-130">Nein</span><span class="sxs-lookup"><span data-stu-id="18892-130">no</span></span>       | <span data-ttu-id="18892-131">Die Paket-ID zum Melden des Missbrauchs für</span><span class="sxs-lookup"><span data-stu-id="18892-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="18892-132">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="18892-132">string</span></span>  | <span data-ttu-id="18892-133">Nein</span><span class="sxs-lookup"><span data-stu-id="18892-133">no</span></span>       | <span data-ttu-id="18892-134">Die Paketversion zum Melden des Missbrauchs für</span><span class="sxs-lookup"><span data-stu-id="18892-134">The package version to report abuse for</span></span>

<span data-ttu-id="18892-135">Die `{id}` und `{version}` Werte interpretiert werden, durch die Implementierung der Server muss Groß-/Kleinschreibung beachtet und nicht vertraulich, gibt an, ob die Version normalisiert wird.</span><span class="sxs-lookup"><span data-stu-id="18892-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="18892-136">Beispielsweise sieht sich der Nuget.org Missbrauch Berichtsvorlage wie folgt:</span><span class="sxs-lookup"><span data-stu-id="18892-136">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="18892-137">Wenn die Clientimplementierung einen Link zum Bericht Missbrauch Formular für NuGet.Versioning 4.3.0 anzuzeigen muss, würde es erzeugt die folgende URL und für den Benutzer bereitstellen:</span><span class="sxs-lookup"><span data-stu-id="18892-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
