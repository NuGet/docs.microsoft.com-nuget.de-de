---
title: Begrenzung der Datenübertragungsrate | Microsoft Docs
author:
- cmanu
- anangaur
ms.author:
- cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Die NuGet-APIs werden erzwungen, um Missbrauch zu verhindern, dass die Begrenzung der Datenübertragungsrate haben.
keywords: NuGet-API, bewerten beschränken
ms.reviewer:
- skofman
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f7891d5e4c008219d9f4808f223f3e5e7ae06ced
ms.sourcegitcommit: fa40be739d093a37d5f7072b62ebdb4f595f4110
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="rate-limits"></a><span data-ttu-id="5da40-104">Begrenzung der Bandbreite</span><span class="sxs-lookup"><span data-stu-id="5da40-104">Rate Limits</span></span>

<span data-ttu-id="5da40-105">Der NuGet.org-API erzwingt die Begrenzung der Übertragungsrate um Missbrauch zu verhindern.</span><span class="sxs-lookup"><span data-stu-id="5da40-105">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="5da40-106">Anforderungen, die die Begrenzung überschreiten zurückgegeben der folgende Fehler:</span><span class="sxs-lookup"><span data-stu-id="5da40-106">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="5da40-107">Die folgenden Tabellen enthalten die Begrenzung der Datenübertragungsrate für die NuGet.org-API.</span><span class="sxs-lookup"><span data-stu-id="5da40-107">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="5da40-108">Paket-Suche</span><span class="sxs-lookup"><span data-stu-id="5da40-108">Package search</span></span>

> [!Note]
> <span data-ttu-id="5da40-109">Es wird empfohlen, sich der NuGet.org [V3-APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) derzeit für die Suche, die leistungsstarke und verfügen über keine beschränken.</span><span class="sxs-lookup"><span data-stu-id="5da40-109">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="5da40-110">Suchen Sie nach V1 und V2 APIs, die Grenzwerte Followins gelten:</span><span class="sxs-lookup"><span data-stu-id="5da40-110">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="5da40-111">API</span><span class="sxs-lookup"><span data-stu-id="5da40-111">API</span></span> | <span data-ttu-id="5da40-112">Limittyp</span><span class="sxs-lookup"><span data-stu-id="5da40-112">Limit Type</span></span> | <span data-ttu-id="5da40-113">Grenzwert</span><span class="sxs-lookup"><span data-stu-id="5da40-113">Limit Value</span></span> | <span data-ttu-id="5da40-114">API-Anwendungsfall</span><span class="sxs-lookup"><span data-stu-id="5da40-114">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="5da40-115">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="5da40-115">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="5da40-116">IP</span><span class="sxs-lookup"><span data-stu-id="5da40-116">IP</span></span> | <span data-ttu-id="5da40-117">1000 / Minute</span><span class="sxs-lookup"><span data-stu-id="5da40-117">1000 / minute</span></span> | <span data-ttu-id="5da40-118">Abfragen von Metadaten von NuGet-Paketen über OData v1 `Packages` Auflistung</span><span class="sxs-lookup"><span data-stu-id="5da40-118">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="5da40-119">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="5da40-119">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="5da40-120">IP</span><span class="sxs-lookup"><span data-stu-id="5da40-120">IP</span></span> | <span data-ttu-id="5da40-121">3000 / Minute</span><span class="sxs-lookup"><span data-stu-id="5da40-121">3000 / minute</span></span> | <span data-ttu-id="5da40-122">Suchen Sie nach NuGet-Pakete über einen Endpunkt für v1-Suche</span><span class="sxs-lookup"><span data-stu-id="5da40-122">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="5da40-123">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="5da40-123">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="5da40-124">IP</span><span class="sxs-lookup"><span data-stu-id="5da40-124">IP</span></span> | <span data-ttu-id="5da40-125">20000 / Minute</span><span class="sxs-lookup"><span data-stu-id="5da40-125">20000 / minute</span></span> | <span data-ttu-id="5da40-126">Abfragen von Metadaten von NuGet-Paketen über OData v2 `Packages` Auflistung</span><span class="sxs-lookup"><span data-stu-id="5da40-126">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="5da40-127">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="5da40-127">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="5da40-128">IP</span><span class="sxs-lookup"><span data-stu-id="5da40-128">IP</span></span> | <span data-ttu-id="5da40-129">100 / Minute</span><span class="sxs-lookup"><span data-stu-id="5da40-129">100 / minute</span></span> | <span data-ttu-id="5da40-130">Anzahl von NuGet-Paket über v2 OData-Abfrage `Packages` Auflistung</span><span class="sxs-lookup"><span data-stu-id="5da40-130">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="5da40-131">Paket Push-als auch Benutzerauswahl</span><span class="sxs-lookup"><span data-stu-id="5da40-131">Package Push and Unlist</span></span>

| <span data-ttu-id="5da40-132">API</span><span class="sxs-lookup"><span data-stu-id="5da40-132">API</span></span> | <span data-ttu-id="5da40-133">Limittyp</span><span class="sxs-lookup"><span data-stu-id="5da40-133">Limit Type</span></span> | <span data-ttu-id="5da40-134">Grenzwert</span><span class="sxs-lookup"><span data-stu-id="5da40-134">Limit Value</span></span> | <span data-ttu-id="5da40-135">Hilfskraftturbine Anwendungsfall</span><span class="sxs-lookup"><span data-stu-id="5da40-135">APU usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="5da40-136">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="5da40-136">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="5da40-137">API-Schlüssel</span><span class="sxs-lookup"><span data-stu-id="5da40-137">API Key</span></span> | <span data-ttu-id="5da40-138">100 / Minute</span><span class="sxs-lookup"><span data-stu-id="5da40-138">100 / minute</span></span> | <span data-ttu-id="5da40-139">Hochladen Sie über v2-Push-Endpunkt ein neues NuGet-Paket (Version)</span><span class="sxs-lookup"><span data-stu-id="5da40-139">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="5da40-140">**DELETE** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="5da40-140">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="5da40-141">API-Schlüssel</span><span class="sxs-lookup"><span data-stu-id="5da40-141">API Key</span></span> | <span data-ttu-id="5da40-142">100 / Minute</span><span class="sxs-lookup"><span data-stu-id="5da40-142">100 / minute</span></span> | <span data-ttu-id="5da40-143">NuGet-Paket (Version) über einen Endpunkt v2 Benutzerauswahl</span><span class="sxs-lookup"><span data-stu-id="5da40-143">Unlist a NuGet package (version) via v2 endpoint</span></span> 
