---
title: Begrenzung der Datenübertragungsrate, NuGet-API
description: Die NuGet-APIs werden Begrenzung der Datenübertragungsrate Missbrauch zu verhindern, dass erzwungen haben.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548676"
---
# <a name="rate-limits"></a><span data-ttu-id="ec571-103">Begrenzung der Bandbreite</span><span class="sxs-lookup"><span data-stu-id="ec571-103">Rate Limits</span></span>

<span data-ttu-id="ec571-104">Der NuGet.org-API erzwingt, um Missbrauch zu verhindern, dass die Begrenzung der Übertragungsrate.</span><span class="sxs-lookup"><span data-stu-id="ec571-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="ec571-105">Anforderungen, die die ratenbegrenzung überschreiten zurückgegeben der folgende Fehler:</span><span class="sxs-lookup"><span data-stu-id="ec571-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="ec571-106">Erzwingen Sie zusätzlich zu den für die anforderungsbegrenzung mit Begrenzung der Datenübertragungsrate, einige APIs ebenfalls Kontingent aus.</span><span class="sxs-lookup"><span data-stu-id="ec571-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="ec571-107">Anforderungen, die das Kontingent überschreiten. zurück folgende Fehlermeldung:</span><span class="sxs-lookup"><span data-stu-id="ec571-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="ec571-108">Die folgenden Tabellen enthalten die Begrenzung der Datenübertragungsrate für die API "NuGet.org".</span><span class="sxs-lookup"><span data-stu-id="ec571-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="ec571-109">Paket suchen</span><span class="sxs-lookup"><span data-stu-id="ec571-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="ec571-110">Es wird empfohlen, NuGet.org [V3-APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) derzeit für die Suche, die leistungsstarke und verfügen über keine beschränken.</span><span class="sxs-lookup"><span data-stu-id="ec571-110">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="ec571-111">APIs für V1 und V2-Suche, die Followins Grenzwerte gelten:</span><span class="sxs-lookup"><span data-stu-id="ec571-111">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="ec571-112">API</span><span class="sxs-lookup"><span data-stu-id="ec571-112">API</span></span> | <span data-ttu-id="ec571-113">-Typ</span><span class="sxs-lookup"><span data-stu-id="ec571-113">Limit Type</span></span> | <span data-ttu-id="ec571-114">Grenzwert</span><span class="sxs-lookup"><span data-stu-id="ec571-114">Limit Value</span></span> | <span data-ttu-id="ec571-115">API-Anwendungsfall</span><span class="sxs-lookup"><span data-stu-id="ec571-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="ec571-116">**ERHALTEN** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="ec571-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="ec571-117">IP</span><span class="sxs-lookup"><span data-stu-id="ec571-117">IP</span></span> | <span data-ttu-id="ec571-118">1000 / Minute</span><span class="sxs-lookup"><span data-stu-id="ec571-118">1000 / minute</span></span> | <span data-ttu-id="ec571-119">Abfragen von NuGet-Paketmetadaten über v1 OData `Packages` Auflistung</span><span class="sxs-lookup"><span data-stu-id="ec571-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="ec571-120">**ERHALTEN** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="ec571-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="ec571-121">IP</span><span class="sxs-lookup"><span data-stu-id="ec571-121">IP</span></span> | <span data-ttu-id="ec571-122">3000 / Minute</span><span class="sxs-lookup"><span data-stu-id="ec571-122">3000 / minute</span></span> | <span data-ttu-id="ec571-123">Suchen Sie nach NuGet-Pakete über die v1-Suche-Endpunkt</span><span class="sxs-lookup"><span data-stu-id="ec571-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="ec571-124">**ERHALTEN** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="ec571-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="ec571-125">IP</span><span class="sxs-lookup"><span data-stu-id="ec571-125">IP</span></span> | <span data-ttu-id="ec571-126">20000 / Minute</span><span class="sxs-lookup"><span data-stu-id="ec571-126">20000 / minute</span></span> | <span data-ttu-id="ec571-127">Abfragen von NuGet-Paketmetadaten über v2 OData `Packages` Auflistung</span><span class="sxs-lookup"><span data-stu-id="ec571-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="ec571-128">**ERHALTEN** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="ec571-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="ec571-129">IP</span><span class="sxs-lookup"><span data-stu-id="ec571-129">IP</span></span> | <span data-ttu-id="ec571-130">100 / Minute</span><span class="sxs-lookup"><span data-stu-id="ec571-130">100 / minute</span></span> | <span data-ttu-id="ec571-131">Anzahl der NuGet-Pakete über v2 OData Abfragen `Packages` Auflistung</span><span class="sxs-lookup"><span data-stu-id="ec571-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="ec571-132">Paket mithilfe von Push übertragen und aus der Liste entfernen</span><span class="sxs-lookup"><span data-stu-id="ec571-132">Package Push and Unlist</span></span>

| <span data-ttu-id="ec571-133">API</span><span class="sxs-lookup"><span data-stu-id="ec571-133">API</span></span> | <span data-ttu-id="ec571-134">-Typ</span><span class="sxs-lookup"><span data-stu-id="ec571-134">Limit Type</span></span> | <span data-ttu-id="ec571-135">Grenzwert</span><span class="sxs-lookup"><span data-stu-id="ec571-135">Limit Value</span></span> | <span data-ttu-id="ec571-136">API-Anwendungsfall</span><span class="sxs-lookup"><span data-stu-id="ec571-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="ec571-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="ec571-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="ec571-138">API-Schlüssel</span><span class="sxs-lookup"><span data-stu-id="ec571-138">API Key</span></span> | <span data-ttu-id="ec571-139">250 / Stunde</span><span class="sxs-lookup"><span data-stu-id="ec571-139">250 / hour</span></span> | <span data-ttu-id="ec571-140">Hochladen eines neuen NuGet-Pakets (Version) per Push-v2-Endpunkt</span><span class="sxs-lookup"><span data-stu-id="ec571-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="ec571-141">**LÖSCHEN** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="ec571-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="ec571-142">API-Schlüssel</span><span class="sxs-lookup"><span data-stu-id="ec571-142">API Key</span></span> | <span data-ttu-id="ec571-143">250 / Stunde</span><span class="sxs-lookup"><span data-stu-id="ec571-143">250 / hour</span></span> | <span data-ttu-id="ec571-144">Entfernen Sie ein NuGet-Paket (Version) über die v2-Endpunkt aus der Liste</span><span class="sxs-lookup"><span data-stu-id="ec571-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
