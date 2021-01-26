---
title: URL-Vorlage zum Melden von Missbrauch, nuget-API
description: Mit der Vorlage "Report Abuse URL" können Clients in der Benutzeroberfläche den Link "Missbrauch melden" anzeigen.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775224"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="5bebe-103">URL-Vorlage zum Melden von Missbrauch</span><span class="sxs-lookup"><span data-stu-id="5bebe-103">Report abuse URL template</span></span>

<span data-ttu-id="5bebe-104">Es ist möglich, dass ein Client eine URL erstellt, die vom Benutzer zum Melden von Missbrauch über ein bestimmtes Paket verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="5bebe-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="5bebe-105">Dies ist hilfreich, wenn eine Paketquelle die Übertragung von Missbrauchs Berichten an die Paketquelle durch eine Paketquelle ermöglichen möchte (auch von Drittanbietern).</span><span class="sxs-lookup"><span data-stu-id="5bebe-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="5bebe-106">Die Ressource, die zum aufbauen dieser URL verwendet wird, ist die Ressource, die `ReportAbuseUriTemplate` im [Dienst Index](service-index.md)gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="5bebe-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="5bebe-107">Versionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="5bebe-107">Versioning</span></span>

<span data-ttu-id="5bebe-108">Die folgenden `@type` Werte werden verwendet:</span><span class="sxs-lookup"><span data-stu-id="5bebe-108">The following `@type` values are used:</span></span>

<span data-ttu-id="5bebe-109">Wert vom Typ @type</span><span class="sxs-lookup"><span data-stu-id="5bebe-109">@type value</span></span>                       | <span data-ttu-id="5bebe-110">Hinweise</span><span class="sxs-lookup"><span data-stu-id="5bebe-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="5bebe-111">Reportabuseuritemplate/3.0.0-Beta</span><span class="sxs-lookup"><span data-stu-id="5bebe-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="5bebe-112">Die erste Version</span><span class="sxs-lookup"><span data-stu-id="5bebe-112">The initial release</span></span>
<span data-ttu-id="5bebe-113">Reportabuseuritemplate/3.0.0-RC</span><span class="sxs-lookup"><span data-stu-id="5bebe-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="5bebe-114">Alias von `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="5bebe-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="5bebe-115">URL-Vorlage</span><span class="sxs-lookup"><span data-stu-id="5bebe-115">URL template</span></span>

<span data-ttu-id="5bebe-116">Die URL für die folgende API ist der Wert der Eigenschaft, die `@id` mit einem der oben erwähnten Ressourcen `@type` Werte verknüpft ist.</span><span class="sxs-lookup"><span data-stu-id="5bebe-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="5bebe-117">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="5bebe-117">HTTP methods</span></span>

<span data-ttu-id="5bebe-118">Obwohl der Client nicht für das Senden von Anforderungen an die URL zum Melden von Missbrauch im Namen des Benutzers vorgesehen ist, sollte die Webseite die-Methode unterstützen, `GET` damit eine angeklickte URL problemlos in einem Webbrowser geöffnet werden kann.</span><span class="sxs-lookup"><span data-stu-id="5bebe-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="5bebe-119">Erstellen der URL</span><span class="sxs-lookup"><span data-stu-id="5bebe-119">Construct the URL</span></span>

<span data-ttu-id="5bebe-120">Wenn eine bekannte Paket-ID und-Version angegeben ist, kann die Client Implementierung eine URL für den Zugriff auf eine Weboberfläche erstellen.</span><span class="sxs-lookup"><span data-stu-id="5bebe-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="5bebe-121">Die Client Implementierung sollte diese erstellte URL (oder einen klickbaren Link) dem Benutzer anzeigen, sodass Sie einen Webbrowser mit der URL öffnen und einen erforderlichen Missbrauchsbericht erstellen können.</span><span class="sxs-lookup"><span data-stu-id="5bebe-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="5bebe-122">Die Implementierung des Formular für den Missbrauch von Berichten wird von der Server Implementierung bestimmt.</span><span class="sxs-lookup"><span data-stu-id="5bebe-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="5bebe-123">Der Wert von `@id` ist eine URL-Zeichenfolge, die eines der folgenden Platzhalter Token enthält:</span><span class="sxs-lookup"><span data-stu-id="5bebe-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="5bebe-124">URL-Platzhalter</span><span class="sxs-lookup"><span data-stu-id="5bebe-124">URL placeholders</span></span>

<span data-ttu-id="5bebe-125">Name</span><span class="sxs-lookup"><span data-stu-id="5bebe-125">Name</span></span>        | <span data-ttu-id="5bebe-126">Typ</span><span class="sxs-lookup"><span data-stu-id="5bebe-126">Type</span></span>    | <span data-ttu-id="5bebe-127">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="5bebe-127">Required</span></span> | <span data-ttu-id="5bebe-128">Notizen</span><span class="sxs-lookup"><span data-stu-id="5bebe-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="5bebe-129">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="5bebe-129">string</span></span>  | <span data-ttu-id="5bebe-130">nein</span><span class="sxs-lookup"><span data-stu-id="5bebe-130">no</span></span>       | <span data-ttu-id="5bebe-131">Die Paket-ID, für die Missbrauch gemeldet werden soll.</span><span class="sxs-lookup"><span data-stu-id="5bebe-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="5bebe-132">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="5bebe-132">string</span></span>  | <span data-ttu-id="5bebe-133">nein</span><span class="sxs-lookup"><span data-stu-id="5bebe-133">no</span></span>       | <span data-ttu-id="5bebe-134">Die Paketversion, für die Missbrauch gemeldet werden soll.</span><span class="sxs-lookup"><span data-stu-id="5bebe-134">The package version to report abuse for</span></span>

<span data-ttu-id="5bebe-135">Der `{id}` -Wert und der- `{version}` Wert, der von der Server Implementierung interpretiert wird, müssen die Groß-/Kleinschreibung nicht beachtet werden.</span><span class="sxs-lookup"><span data-stu-id="5bebe-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="5bebe-136">Beispielsweise sieht die Vorlage "Bericht Missbrauch" von nuget. org wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="5bebe-136">For example, nuget.org's report abuse template looks like this:</span></span>

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

<span data-ttu-id="5bebe-137">Wenn die Client Implementierung einen Link zum berichtsmissbrauchs-Formular für nuget. Versionierung 4.3.0 anzeigen muss, würde Sie die folgende URL erstellen und für den Benutzer bereitstellen:</span><span class="sxs-lookup"><span data-stu-id="5bebe-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
