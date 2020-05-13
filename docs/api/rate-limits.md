---
title: Begrenzung der Datenübertragungs Rate, nuget-API
description: Die nuget-APIs verfügen über erzwungene Raten Limits, um Missbrauch zu verhindern.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367933"
---
# <a name="rate-limits"></a><span data-ttu-id="ef472-103">Begrenzung der Bandbreite</span><span class="sxs-lookup"><span data-stu-id="ef472-103">Rate Limits</span></span>

<span data-ttu-id="ef472-104">Die NuGet.org-API erzwingt die Raten Begrenzung, um Missbrauch zu verhindern.</span><span class="sxs-lookup"><span data-stu-id="ef472-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="ef472-105">Bei Anforderungen, die die Raten Begrenzung überschreiten, wird folgender Fehler zurückgegeben:</span><span class="sxs-lookup"><span data-stu-id="ef472-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="ef472-106">Zusätzlich zur Einschränkung der Einschränkung durch die Begrenzung der Datenübertragungsrate erzwingen einige APIs auch das Kontingent.</span><span class="sxs-lookup"><span data-stu-id="ef472-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="ef472-107">Bei Anforderungen, die das Kontingent überschreiten, wird folgender Fehler zurückgegeben:</span><span class="sxs-lookup"><span data-stu-id="ef472-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="ef472-108">In den folgenden Tabellen sind die Begrenzung der Datenübertragungsrate für die NuGet.org-API aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="ef472-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="ef472-109">Paket Suche</span><span class="sxs-lookup"><span data-stu-id="ef472-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="ef472-110">Es wird empfohlen, die [V3-Suche-APIs](search-query-service-resource.md) von nuget. org zu verwenden, da es derzeit keine Raten Beschränkung gibt.</span><span class="sxs-lookup"><span data-stu-id="ef472-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="ef472-111">Für v1-und v2-Such-APIs gelten die folgenden Grenzwerte:</span><span class="sxs-lookup"><span data-stu-id="ef472-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="ef472-112">API</span><span class="sxs-lookup"><span data-stu-id="ef472-112">API</span></span> | <span data-ttu-id="ef472-113">Beschränkungstyp</span><span class="sxs-lookup"><span data-stu-id="ef472-113">Limit Type</span></span> | <span data-ttu-id="ef472-114">Limit-Wert</span><span class="sxs-lookup"><span data-stu-id="ef472-114">Limit Value</span></span> | <span data-ttu-id="ef472-115">API-Anwendungsfall</span><span class="sxs-lookup"><span data-stu-id="ef472-115">API Use Case</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="ef472-116">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="ef472-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="ef472-117">IP</span><span class="sxs-lookup"><span data-stu-id="ef472-117">IP</span></span> | <span data-ttu-id="ef472-118">1000/Minute</span><span class="sxs-lookup"><span data-stu-id="ef472-118">1000 / minute</span></span> | <span data-ttu-id="ef472-119">Abfragen von nuget-Paket Metadaten über die v1-odata- `Packages` Sammlung</span><span class="sxs-lookup"><span data-stu-id="ef472-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="ef472-120">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="ef472-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="ef472-121">IP</span><span class="sxs-lookup"><span data-stu-id="ef472-121">IP</span></span> | <span data-ttu-id="ef472-122">3000/Minute</span><span class="sxs-lookup"><span data-stu-id="ef472-122">3000 / minute</span></span> | <span data-ttu-id="ef472-123">Suchen nach nuget-Paketen über den v1-Such Endpunkt</span><span class="sxs-lookup"><span data-stu-id="ef472-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="ef472-124">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="ef472-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="ef472-125">IP</span><span class="sxs-lookup"><span data-stu-id="ef472-125">IP</span></span> | <span data-ttu-id="ef472-126">20000/Minute</span><span class="sxs-lookup"><span data-stu-id="ef472-126">20000 / minute</span></span> | <span data-ttu-id="ef472-127">Abfragen von nuget-Paket Metadaten über die V2-odata- `Packages` Sammlung</span><span class="sxs-lookup"><span data-stu-id="ef472-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="ef472-128">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="ef472-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="ef472-129">IP</span><span class="sxs-lookup"><span data-stu-id="ef472-129">IP</span></span> | <span data-ttu-id="ef472-130">100/Minute</span><span class="sxs-lookup"><span data-stu-id="ef472-130">100 / minute</span></span> | <span data-ttu-id="ef472-131">Abfragen der nuget-Paket Anzahl über die V2-odata- `Packages` Sammlung</span><span class="sxs-lookup"><span data-stu-id="ef472-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="ef472-132">Package Push und Unlist</span><span class="sxs-lookup"><span data-stu-id="ef472-132">Package Push and Unlist</span></span>

| <span data-ttu-id="ef472-133">API</span><span class="sxs-lookup"><span data-stu-id="ef472-133">API</span></span> | <span data-ttu-id="ef472-134">Beschränkungstyp</span><span class="sxs-lookup"><span data-stu-id="ef472-134">Limit Type</span></span> | <span data-ttu-id="ef472-135">Limit-Wert</span><span class="sxs-lookup"><span data-stu-id="ef472-135">Limit Value</span></span> | <span data-ttu-id="ef472-136">API-Anwendungsfall</span><span class="sxs-lookup"><span data-stu-id="ef472-136">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="ef472-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="ef472-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="ef472-138">API-Schlüssel</span><span class="sxs-lookup"><span data-stu-id="ef472-138">API Key</span></span> | <span data-ttu-id="ef472-139">350/Stunde</span><span class="sxs-lookup"><span data-stu-id="ef472-139">350 / hour</span></span> | <span data-ttu-id="ef472-140">Neues nuget-Paket (Version) über v2-Push-Endpunkt hochladen</span><span class="sxs-lookup"><span data-stu-id="ef472-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="ef472-141">**Löschen**`/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="ef472-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="ef472-142">API-Schlüssel</span><span class="sxs-lookup"><span data-stu-id="ef472-142">API Key</span></span> | <span data-ttu-id="ef472-143">250/Stunde</span><span class="sxs-lookup"><span data-stu-id="ef472-143">250 / hour</span></span> | <span data-ttu-id="ef472-144">Auflisten eines nuget-Pakets (Version) über den V2-Endpunkt</span><span class="sxs-lookup"><span data-stu-id="ef472-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 

## <a name="nugetorg-website-page-views"></a><span data-ttu-id="ef472-145">nuget.org Website Ansichten von Websites</span><span class="sxs-lookup"><span data-stu-id="ef472-145">nuget.org website page views</span></span>

<span data-ttu-id="ef472-146">Wenn Sie Programm gesteuert auf die nuget.org-Webseiten zugreifen, sollten Sie eine Untersuchung unserer dokumentierten [V3-APIs](overview.md)in Erwägung zieht.</span><span class="sxs-lookup"><span data-stu-id="ef472-146">If you are accessing the nuget.org web pages programmatically, consider investigating our documented [V3 APIs](overview.md).</span></span> <span data-ttu-id="ef472-147">Diese Endpunkte ermöglichen einen einfacheren Zugriff auf Paket Metadaten und-Inhalte.</span><span class="sxs-lookup"><span data-stu-id="ef472-147">These endpoints allow for simpler access to package metadata and content.</span></span> <span data-ttu-id="ef472-148">Die V3-API bietet eine bessere Verfügbarkeit und bietet eine höhere Leistung als der Zugriff auf die nuget-Katalog Webseiten, die für Webbrowser Interaktion entwickelt wurden.</span><span class="sxs-lookup"><span data-stu-id="ef472-148">The V3 API has better availability and has higher performance than accessing the NuGet Gallery web pages, which are designed for web browser interaction.</span></span>

| <span data-ttu-id="ef472-149">API</span><span class="sxs-lookup"><span data-stu-id="ef472-149">API</span></span> | <span data-ttu-id="ef472-150">Beschränkungstyp</span><span class="sxs-lookup"><span data-stu-id="ef472-150">Limit Type</span></span> | <span data-ttu-id="ef472-151">Limit-Wert</span><span class="sxs-lookup"><span data-stu-id="ef472-151">Limit Value</span></span> | <span data-ttu-id="ef472-152">API-Anwendungsfall</span><span class="sxs-lookup"><span data-stu-id="ef472-152">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="ef472-153">**GET** `/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="ef472-153">**GET** `/package/{id}/{version}`</span></span> | <span data-ttu-id="ef472-154">IP</span><span class="sxs-lookup"><span data-stu-id="ef472-154">IP</span></span> | <span data-ttu-id="ef472-155">50/Minute</span><span class="sxs-lookup"><span data-stu-id="ef472-155">50 / minute</span></span> | <span data-ttu-id="ef472-156">Seite "Details zum Paket (Version)" anzeigen.</span><span class="sxs-lookup"><span data-stu-id="ef472-156">Display package (version) details page.</span></span> 
