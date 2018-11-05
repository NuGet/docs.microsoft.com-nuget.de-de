---
title: Begrenzung der Datenübertragungsrate, NuGet-API
description: Die NuGet-APIs haben Ratenbegrenzungen, um Missbrauch zu verhindern.
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
# <a name="rate-limits"></a><span data-ttu-id="78f06-103">Begrenzung der Bandbreite</span><span class="sxs-lookup"><span data-stu-id="78f06-103">Rate Limits</span></span>

<span data-ttu-id="78f06-104">Die nuget.org-API erzwingt die Begrenzung der Datenübertragungsrate, um Missbrauch zu verhindern.</span><span class="sxs-lookup"><span data-stu-id="78f06-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="78f06-105">Anforderungen, die die Begrenzung überschreiten, geben folgenden Fehler zurück:</span><span class="sxs-lookup"><span data-stu-id="78f06-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="78f06-106">Zusätzlich zu dem Fakt, dass Anforderungsbegrenzungen die Begrenzungen der Datenübertragungsrate verwenden, erzwingen manche APIs auch ein Kontingent.</span><span class="sxs-lookup"><span data-stu-id="78f06-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="78f06-107">Anforderungen, die das Kontingent überschreiten, geben folgenden Fehler zurück:</span><span class="sxs-lookup"><span data-stu-id="78f06-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="78f06-108">Die folgenden Tabellen enthalten die Begrenzungen für die nuget.org-API.</span><span class="sxs-lookup"><span data-stu-id="78f06-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="78f06-109">Paketsuche</span><span class="sxs-lookup"><span data-stu-id="78f06-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="78f06-110">Es wird empfohlen, die [V3-APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) von nuget.org für die Suche zu verwenden. Diese sind leistungsfähig und haben momentan kein Limit.</span><span class="sxs-lookup"><span data-stu-id="78f06-110">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="78f06-111">Für die V1- und V2-Such-APIs gelten die folgenden Limits:</span><span class="sxs-lookup"><span data-stu-id="78f06-111">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="78f06-112">API</span><span class="sxs-lookup"><span data-stu-id="78f06-112">API</span></span> | <span data-ttu-id="78f06-113">Limittyp</span><span class="sxs-lookup"><span data-stu-id="78f06-113">Limit Type</span></span> | <span data-ttu-id="78f06-114">Grenzwert</span><span class="sxs-lookup"><span data-stu-id="78f06-114">Limit Value</span></span> | <span data-ttu-id="78f06-115">API-Anwendungsfall</span><span class="sxs-lookup"><span data-stu-id="78f06-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="78f06-116">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="78f06-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="78f06-117">IP</span><span class="sxs-lookup"><span data-stu-id="78f06-117">IP</span></span> | <span data-ttu-id="78f06-118">1000 / Minute</span><span class="sxs-lookup"><span data-stu-id="78f06-118">1000 / minute</span></span> | <span data-ttu-id="78f06-119">Abfragen von NuGet-Paketmetadaten über die v1-OData-Auflistung `Packages`</span><span class="sxs-lookup"><span data-stu-id="78f06-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="78f06-120">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="78f06-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="78f06-121">IP</span><span class="sxs-lookup"><span data-stu-id="78f06-121">IP</span></span> | <span data-ttu-id="78f06-122">3000 / Minute</span><span class="sxs-lookup"><span data-stu-id="78f06-122">3000 / minute</span></span> | <span data-ttu-id="78f06-123">Suche nach NuGet-Paketen über den v1-Suche-Endpunkt</span><span class="sxs-lookup"><span data-stu-id="78f06-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="78f06-124">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="78f06-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="78f06-125">IP</span><span class="sxs-lookup"><span data-stu-id="78f06-125">IP</span></span> | <span data-ttu-id="78f06-126">20000 / Minute</span><span class="sxs-lookup"><span data-stu-id="78f06-126">20000 / minute</span></span> | <span data-ttu-id="78f06-127">Abfragen von NuGet-Paketmetadaten über die v2-OData-Auflistung `Packages`</span><span class="sxs-lookup"><span data-stu-id="78f06-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="78f06-128">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="78f06-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="78f06-129">IP</span><span class="sxs-lookup"><span data-stu-id="78f06-129">IP</span></span> | <span data-ttu-id="78f06-130">100 / Minute</span><span class="sxs-lookup"><span data-stu-id="78f06-130">100 / minute</span></span> | <span data-ttu-id="78f06-131">Anzahl der NuGet-Pakete über die v2-OData-Auflistung `Packages`</span><span class="sxs-lookup"><span data-stu-id="78f06-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="78f06-132">Paket mithilfe von Push übertragen und aus der Liste entfernen</span><span class="sxs-lookup"><span data-stu-id="78f06-132">Package Push and Unlist</span></span>

| <span data-ttu-id="78f06-133">API</span><span class="sxs-lookup"><span data-stu-id="78f06-133">API</span></span> | <span data-ttu-id="78f06-134">Limittyp</span><span class="sxs-lookup"><span data-stu-id="78f06-134">Limit Type</span></span> | <span data-ttu-id="78f06-135">Grenzwert</span><span class="sxs-lookup"><span data-stu-id="78f06-135">Limit Value</span></span> | <span data-ttu-id="78f06-136">API-Anwendungsfall</span><span class="sxs-lookup"><span data-stu-id="78f06-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="78f06-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="78f06-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="78f06-138">API-Schlüssel</span><span class="sxs-lookup"><span data-stu-id="78f06-138">API Key</span></span> | <span data-ttu-id="78f06-139">250 / Stunde</span><span class="sxs-lookup"><span data-stu-id="78f06-139">250 / hour</span></span> | <span data-ttu-id="78f06-140">Hochladen eines neuen NuGet-Pakets (Version) per v2-Push-Endpunkt</span><span class="sxs-lookup"><span data-stu-id="78f06-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="78f06-141">**DELETE** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="78f06-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="78f06-142">API-Schlüssel</span><span class="sxs-lookup"><span data-stu-id="78f06-142">API Key</span></span> | <span data-ttu-id="78f06-143">250 / Stunde</span><span class="sxs-lookup"><span data-stu-id="78f06-143">250 / hour</span></span> | <span data-ttu-id="78f06-144">Entfernen eines NuGet-Pakets oder einer Paketversion über den v2-Endpunkt</span><span class="sxs-lookup"><span data-stu-id="78f06-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
