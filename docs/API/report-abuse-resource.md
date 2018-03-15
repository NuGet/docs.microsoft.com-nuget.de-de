---
title: Bericht Missbrauch URL-Vorlage, NuGet-API | Microsoft Docs
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
description: "Der Bericht Missbrauch URL-Vorlage kann Clients einen Missbrauch Berichtslink in ihre Benutzeroberfläche anzeigen."
keywords: NuGet-API Melden des Missbrauchs, NuGet-API-Datei kompatibel, nuget.org-Berichts-URL-Vorlage
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: efbe5704e6e6028f9382fea3fe5ec453f573a2e9
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="8a810-104">Berichtsvorlage Missbrauch-URL</span><span class="sxs-lookup"><span data-stu-id="8a810-104">Report abuse URL template</span></span>

<span data-ttu-id="8a810-105">Es ist möglich, dass ein Client eine URL zu erstellen, die vom Benutzer zum Melden des Missbrauchs zu einem bestimmten Paket verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="8a810-105">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="8a810-106">Dies ist hilfreich, wenn eine Paketquelle möchte, um alle Clients Erfahrungen (auch 3rd Party) Missbrauch Berichte für die Paketquelle delegieren zu erzielen.</span><span class="sxs-lookup"><span data-stu-id="8a810-106">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="8a810-107">Die Ressource für das Abrufen von Paketinhalt verwendet die `ReportAbuseUriTemplate` Ressource gefunden, der [Dienst Index](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="8a810-107">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="8a810-108">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="8a810-108">Versioning</span></span>

<span data-ttu-id="8a810-109">Die folgenden `@type` Werte werden verwendet:</span><span class="sxs-lookup"><span data-stu-id="8a810-109">The following `@type` values are used:</span></span>

<span data-ttu-id="8a810-110">@type-Wert</span><span class="sxs-lookup"><span data-stu-id="8a810-110">@type value</span></span>                       | <span data-ttu-id="8a810-111">Notizen</span><span class="sxs-lookup"><span data-stu-id="8a810-111">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="8a810-112">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="8a810-112">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="8a810-113">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="8a810-113">The initial release</span></span>
<span data-ttu-id="8a810-114">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="8a810-114">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="8a810-115">Alias der `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="8a810-115">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="8a810-116">URL-Vorlage</span><span class="sxs-lookup"><span data-stu-id="8a810-116">URL template</span></span>

<span data-ttu-id="8a810-117">Die URL für die folgende API wird der Wert von der `@id` mit einem der oben genannten Ressource verknüpfte Eigenschaft `@type` Werte.</span><span class="sxs-lookup"><span data-stu-id="8a810-117">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="8a810-118">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="8a810-118">HTTP methods</span></span>

<span data-ttu-id="8a810-119">Obwohl der Client nicht vorgesehen ist, damit Anforderungen an die URL des Berichts Missbrauch im Namen des Benutzers zu senden, sollte die Webseite unterstützen die `GET` Methode, um eine URL geklickt wurde, problemlos in einem Webbrowser geöffnet werden zuzulassen.</span><span class="sxs-lookup"><span data-stu-id="8a810-119">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="8a810-120">Die URL zu erstellen</span><span class="sxs-lookup"><span data-stu-id="8a810-120">Construct the URL</span></span>

<span data-ttu-id="8a810-121">Erteilt ein bekannter Paket-ID und eine Version, kann die Clientimplementierung eine URL verwendet, um eine Weboberfläche zugreifen zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="8a810-121">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="8a810-122">Die Clientimplementierung sollte diese erstellte URL (oder einen klickbaren Link) für den Benutzer, die sie zulassen, dass auf einen Webbrowser an die URL öffnen, und stellen alle erforderlichen Missbrauch Bericht anzeigen.</span><span class="sxs-lookup"><span data-stu-id="8a810-122">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="8a810-123">Die Implementierung des Formulars Bericht Missbrauch richtet sich nach der Server-Implementierung.</span><span class="sxs-lookup"><span data-stu-id="8a810-123">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="8a810-124">Der Wert, der die `@id` ist eine URL-Zeichenfolge, die keines der folgenden Platzhalter-Token enthält:</span><span class="sxs-lookup"><span data-stu-id="8a810-124">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="8a810-125">URL-Platzhalter</span><span class="sxs-lookup"><span data-stu-id="8a810-125">URL placeholders</span></span>

<span data-ttu-id="8a810-126">Name</span><span class="sxs-lookup"><span data-stu-id="8a810-126">Name</span></span>        | <span data-ttu-id="8a810-127">Typ</span><span class="sxs-lookup"><span data-stu-id="8a810-127">Type</span></span>    | <span data-ttu-id="8a810-128">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="8a810-128">Required</span></span> | <span data-ttu-id="8a810-129">Notizen</span><span class="sxs-lookup"><span data-stu-id="8a810-129">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="8a810-130">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="8a810-130">string</span></span>  | <span data-ttu-id="8a810-131">nein</span><span class="sxs-lookup"><span data-stu-id="8a810-131">no</span></span>       | <span data-ttu-id="8a810-132">Die Paket-ID zum Melden des Missbrauchs für</span><span class="sxs-lookup"><span data-stu-id="8a810-132">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="8a810-133">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="8a810-133">string</span></span>  | <span data-ttu-id="8a810-134">nein</span><span class="sxs-lookup"><span data-stu-id="8a810-134">no</span></span>       | <span data-ttu-id="8a810-135">Die Paketversion zum Melden des Missbrauchs für</span><span class="sxs-lookup"><span data-stu-id="8a810-135">The package version to report abuse for</span></span>

<span data-ttu-id="8a810-136">Die `{id}` und `{version}` Werte interpretiert werden, durch die Implementierung der Server muss Groß-/Kleinschreibung beachtet und nicht vertraulich, gibt an, ob die Version normalisiert wird.</span><span class="sxs-lookup"><span data-stu-id="8a810-136">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="8a810-137">Beispielsweise sieht sich der Nuget.org Missbrauch Berichtsvorlage wie folgt:</span><span class="sxs-lookup"><span data-stu-id="8a810-137">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="8a810-138">Wenn die Clientimplementierung einen Link zum Bericht Missbrauch Formular für NuGet.Versioning 4.3.0 anzuzeigen muss, würde es erzeugt die folgende URL und für den Benutzer bereitstellen:</span><span class="sxs-lookup"><span data-stu-id="8a810-138">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
