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
keywords: NuGet-API Melden des Missbrauchs, NuGet-API-Datei kompatibel, NuGet.org-Berichts-URL-Vorlage
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c12be294c71547fbce421c72aa091e0eee15aacd
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="42b66-104">Berichtsvorlage Missbrauch-URL</span><span class="sxs-lookup"><span data-stu-id="42b66-104">Report abuse URL template</span></span>

<span data-ttu-id="42b66-105">Es ist möglich, dass ein Client eine URL zu erstellen, die vom Benutzer zum Melden des Missbrauchs zu einem bestimmten Paket verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="42b66-105">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="42b66-106">Dies ist hilfreich, wenn eine Paketquelle möchte, um alle Clients Erfahrungen (auch 3rd Party) Missbrauch Berichte für die Paketquelle delegieren zu erzielen.</span><span class="sxs-lookup"><span data-stu-id="42b66-106">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="42b66-107">Die Ressource für das Abrufen von Paketinhalt verwendet die `ReportAbuseUriTemplate` Ressource gefunden, der [Dienst Index](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="42b66-107">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="42b66-108">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="42b66-108">Versioning</span></span>

<span data-ttu-id="42b66-109">Die folgenden `@type` Werte werden verwendet:</span><span class="sxs-lookup"><span data-stu-id="42b66-109">The following `@type` values are used:</span></span>

<span data-ttu-id="42b66-110">@type-Wert</span><span class="sxs-lookup"><span data-stu-id="42b66-110">@type value</span></span>                       | <span data-ttu-id="42b66-111">Hinweise</span><span class="sxs-lookup"><span data-stu-id="42b66-111">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="42b66-112">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="42b66-112">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="42b66-113">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="42b66-113">The initial release</span></span>
<span data-ttu-id="42b66-114">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="42b66-114">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="42b66-115">Alias der`ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="42b66-115">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="42b66-116">URL-Vorlage</span><span class="sxs-lookup"><span data-stu-id="42b66-116">URL template</span></span>

<span data-ttu-id="42b66-117">Die URL für die folgende API wird der Wert von der `@id` mit einem der oben genannten Ressource verknüpfte Eigenschaft `@type` Werte.</span><span class="sxs-lookup"><span data-stu-id="42b66-117">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="42b66-118">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="42b66-118">HTTP methods</span></span>

<span data-ttu-id="42b66-119">Obwohl der Client nicht vorgesehen ist, damit Anforderungen an die URL des Berichts Missbrauch im Namen des Benutzers zu senden, sollte die Webseite unterstützen die `GET` Methode, um eine URL geklickt wurde, problemlos in einem Webbrowser geöffnet werden zuzulassen.</span><span class="sxs-lookup"><span data-stu-id="42b66-119">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="42b66-120">Die URL zu erstellen</span><span class="sxs-lookup"><span data-stu-id="42b66-120">Construct the URL</span></span>

<span data-ttu-id="42b66-121">Erteilt ein bekannter Paket-ID und eine Version, kann die Clientimplementierung eine URL verwendet, um eine Weboberfläche zugreifen zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="42b66-121">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="42b66-122">Die Clientimplementierung sollte diese erstellte URL (oder einen klickbaren Link) für den Benutzer, die sie zulassen, dass auf einen Webbrowser an die URL öffnen, und stellen alle erforderlichen Missbrauch Bericht anzeigen.</span><span class="sxs-lookup"><span data-stu-id="42b66-122">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="42b66-123">Die Implementierung des Formulars Bericht Missbrauch richtet sich nach der Server-Implementierung.</span><span class="sxs-lookup"><span data-stu-id="42b66-123">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="42b66-124">Der Wert, der die `@id` ist eine URL-Zeichenfolge, die keines der folgenden Platzhalter-Token enthält:</span><span class="sxs-lookup"><span data-stu-id="42b66-124">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="42b66-125">URL-Platzhalter</span><span class="sxs-lookup"><span data-stu-id="42b66-125">URL placeholders</span></span>

<span data-ttu-id="42b66-126">name</span><span class="sxs-lookup"><span data-stu-id="42b66-126">Name</span></span>        | <span data-ttu-id="42b66-127">Typ</span><span class="sxs-lookup"><span data-stu-id="42b66-127">Type</span></span>    | <span data-ttu-id="42b66-128">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="42b66-128">Required</span></span> | <span data-ttu-id="42b66-129">Hinweise</span><span class="sxs-lookup"><span data-stu-id="42b66-129">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="42b66-130">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="42b66-130">string</span></span>  | <span data-ttu-id="42b66-131">Nein</span><span class="sxs-lookup"><span data-stu-id="42b66-131">no</span></span>       | <span data-ttu-id="42b66-132">Die Paket-ID zum Melden des Missbrauchs für</span><span class="sxs-lookup"><span data-stu-id="42b66-132">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="42b66-133">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="42b66-133">string</span></span>  | <span data-ttu-id="42b66-134">Nein</span><span class="sxs-lookup"><span data-stu-id="42b66-134">no</span></span>       | <span data-ttu-id="42b66-135">Die Paketversion zum Melden des Missbrauchs für</span><span class="sxs-lookup"><span data-stu-id="42b66-135">The package version to report abuse for</span></span>

<span data-ttu-id="42b66-136">Die `{id}` und `{version}` Werte interpretiert werden, durch die Implementierung der Server muss die Groß-/Kleinschreibung bei, und gibt an, ob die Version normalisiert wird nicht beachtet.</span><span class="sxs-lookup"><span data-stu-id="42b66-136">The `{id}` and `{version}` values interpreted by the server implementation must be case insenstive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="42b66-137">Beispielsweise sieht sich der Nuget.org Missbrauch Berichtsvorlage wie folgt:</span><span class="sxs-lookup"><span data-stu-id="42b66-137">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="42b66-138">Wenn die Clientimplementierung einen Link zum Bericht Missbrauch Formular für NuGet.Versioning 4.3.0 anzuzeigen muss, würde es erzeugt die folgende URL und für den Benutzer bereitstellen:</span><span class="sxs-lookup"><span data-stu-id="42b66-138">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
