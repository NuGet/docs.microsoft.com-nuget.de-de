---
title: Melden von Missbrauch URL-Vorlage, NuGet-API
description: Die Bericht Missbrauch URL-Vorlage kann Clients einen Missbrauch Berichtslink in ihrer Benutzeroberfläche angezeigt.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b1fd65b12590a6c5eeb23d946eec6ca4a1c661bc
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020439"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="ef2af-103">Bericht-Missbrauch-URL-Vorlage</span><span class="sxs-lookup"><span data-stu-id="ef2af-103">Report abuse URL template</span></span>

<span data-ttu-id="ef2af-104">Es ist möglich, dass ein Client eine URL zu erstellen, die vom Benutzer zum Angeben des Missbrauchs zu einem bestimmten Paket verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="ef2af-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="ef2af-105">Dies ist nützlich, wenn möchte, dass eine Paketquelle alle Clientumgebungen, Missbrauch Berichte für die Paketquelle zu delegieren (sogar 3rd Party) zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="ef2af-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="ef2af-106">Die Ressource, die zum Erstellen von dieser URL ist die `ReportAbuseUriTemplate` Ressource finden Sie in der [dienstindex](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="ef2af-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="ef2af-107">Versionskontrolle</span><span class="sxs-lookup"><span data-stu-id="ef2af-107">Versioning</span></span>

<span data-ttu-id="ef2af-108">Die folgenden `@type` Werte werden verwendet:</span><span class="sxs-lookup"><span data-stu-id="ef2af-108">The following `@type` values are used:</span></span>

<span data-ttu-id="ef2af-109">@type-Wert</span><span class="sxs-lookup"><span data-stu-id="ef2af-109">@type value</span></span>                       | <span data-ttu-id="ef2af-110">Hinweise</span><span class="sxs-lookup"><span data-stu-id="ef2af-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="ef2af-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="ef2af-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="ef2af-112">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="ef2af-112">The initial release</span></span>
<span data-ttu-id="ef2af-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="ef2af-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="ef2af-114">Alias der `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="ef2af-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="ef2af-115">URL-Vorlage</span><span class="sxs-lookup"><span data-stu-id="ef2af-115">URL template</span></span>

<span data-ttu-id="ef2af-116">Die URL für die folgende API wird der Wert des der `@id` Eigenschaft, die einer der oben genannten Ressource zugeordneten `@type` Werte.</span><span class="sxs-lookup"><span data-stu-id="ef2af-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="ef2af-117">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="ef2af-117">HTTP methods</span></span>

<span data-ttu-id="ef2af-118">Der Client nicht gedacht ist, um Anforderungen an die URL des Berichts Missbrauch im Auftrag des Benutzers zu senden, sollte die Webseite unterstützen die `GET` Methode, um eine geklickte URL ganz einfach in einem Webbrowser geöffnet werden können.</span><span class="sxs-lookup"><span data-stu-id="ef2af-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="ef2af-119">Erstellen Sie die URL</span><span class="sxs-lookup"><span data-stu-id="ef2af-119">Construct the URL</span></span>

<span data-ttu-id="ef2af-120">Wenn eine bekannte Paket-ID und Version, kann die Client-Implementierung eine URL für den Zugriff auf eine Weboberfläche erstellen.</span><span class="sxs-lookup"><span data-stu-id="ef2af-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="ef2af-121">Die Clientimplementierung sollte diese erstellte URL (oder einen klickbaren Link) anzeigen, um dem Benutzer, öffnen einen Webbrowser an die URL, und nehmen alle erforderlichen Missbrauch-Bericht.</span><span class="sxs-lookup"><span data-stu-id="ef2af-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="ef2af-122">Die Implementierung den Missbrauch Berichtsformular wird durch die Implementierung der Server bestimmt.</span><span class="sxs-lookup"><span data-stu-id="ef2af-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="ef2af-123">Der Wert des der `@id` ist eine URL-Zeichenfolge, die mit der eines der folgenden Platzhalter-Token:</span><span class="sxs-lookup"><span data-stu-id="ef2af-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="ef2af-124">URL-Platzhalter</span><span class="sxs-lookup"><span data-stu-id="ef2af-124">URL placeholders</span></span>

<span data-ttu-id="ef2af-125">name</span><span class="sxs-lookup"><span data-stu-id="ef2af-125">Name</span></span>        | <span data-ttu-id="ef2af-126">Typ</span><span class="sxs-lookup"><span data-stu-id="ef2af-126">Type</span></span>    | <span data-ttu-id="ef2af-127">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="ef2af-127">Required</span></span> | <span data-ttu-id="ef2af-128">Hinweise</span><span class="sxs-lookup"><span data-stu-id="ef2af-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="ef2af-129">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="ef2af-129">string</span></span>  | <span data-ttu-id="ef2af-130">Nein</span><span class="sxs-lookup"><span data-stu-id="ef2af-130">no</span></span>       | <span data-ttu-id="ef2af-131">Die Paket-ID zum Angeben des Missbrauchs für</span><span class="sxs-lookup"><span data-stu-id="ef2af-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="ef2af-132">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="ef2af-132">string</span></span>  | <span data-ttu-id="ef2af-133">Nein</span><span class="sxs-lookup"><span data-stu-id="ef2af-133">no</span></span>       | <span data-ttu-id="ef2af-134">Die Paketversion zum Angeben des Missbrauchs für</span><span class="sxs-lookup"><span data-stu-id="ef2af-134">The package version to report abuse for</span></span>

<span data-ttu-id="ef2af-135">Die `{id}` und `{version}` Werte interpretiert werden, durch die Implementierung der Server muss Groß-/Kleinschreibung und nicht vertrauliche gibt an, ob die Version normalisiert ist.</span><span class="sxs-lookup"><span data-stu-id="ef2af-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="ef2af-136">Beispielsweise sieht die Nuget.org Missbrauch Berichtsvorlage folgendermaßen aus:</span><span class="sxs-lookup"><span data-stu-id="ef2af-136">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="ef2af-137">Wenn die Clientimplementierung eine Verknüpfung zum Missbrauch Berichts angezeigt wird, für die NuGet.Versioning 4.3.0 muss, würde er erzeugt die folgende URL, und geben Sie sie für den Benutzer:</span><span class="sxs-lookup"><span data-stu-id="ef2af-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
