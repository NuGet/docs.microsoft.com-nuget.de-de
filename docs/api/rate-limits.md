---
title: Begrenzung der Datenübertragungs Rate, nuget-API
description: Die NuGet-APIs haben Ratenbegrenzungen, um Missbrauch zu verhindern.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 9e60c0236bd4e6f1374b50a236447faf80dddb38
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813194"
---
# <a name="rate-limits"></a><span data-ttu-id="3573e-103">Begrenzung der Bandbreite</span><span class="sxs-lookup"><span data-stu-id="3573e-103">Rate Limits</span></span>

<span data-ttu-id="3573e-104">Die nuget.org-API erzwingt die Begrenzung der Datenübertragungsrate, um Missbrauch zu verhindern.</span><span class="sxs-lookup"><span data-stu-id="3573e-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="3573e-105">Anforderungen, die die Begrenzung überschreiten, geben folgenden Fehler zurück:</span><span class="sxs-lookup"><span data-stu-id="3573e-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="3573e-106">Zusätzlich zu dem Fakt, dass Anforderungsbegrenzungen die Begrenzungen der Datenübertragungsrate verwenden, erzwingen manche APIs auch ein Kontingent.</span><span class="sxs-lookup"><span data-stu-id="3573e-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="3573e-107">Anforderungen, die das Kontingent überschreiten, geben folgenden Fehler zurück:</span><span class="sxs-lookup"><span data-stu-id="3573e-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="3573e-108">Die folgenden Tabellen enthalten die Begrenzungen für die nuget.org-API.</span><span class="sxs-lookup"><span data-stu-id="3573e-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="3573e-109">Paketsuche</span><span class="sxs-lookup"><span data-stu-id="3573e-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="3573e-110">Es wird empfohlen, die [V3-Suche-APIs](search-query-service-resource.md) von nuget. org zu verwenden, da es derzeit keine Raten Beschränkung gibt.</span><span class="sxs-lookup"><span data-stu-id="3573e-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="3573e-111">Für v1-und v2-Such-APIs gelten die folgenden Grenzwerte:</span><span class="sxs-lookup"><span data-stu-id="3573e-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="3573e-112">API</span><span class="sxs-lookup"><span data-stu-id="3573e-112">API</span></span> | <span data-ttu-id="3573e-113">Limit-Typ</span><span class="sxs-lookup"><span data-stu-id="3573e-113">Limit Type</span></span> | <span data-ttu-id="3573e-114">Limit-Wert</span><span class="sxs-lookup"><span data-stu-id="3573e-114">Limit Value</span></span> | <span data-ttu-id="3573e-115">API-UseCase</span><span class="sxs-lookup"><span data-stu-id="3573e-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="3573e-116">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="3573e-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="3573e-117">IP</span><span class="sxs-lookup"><span data-stu-id="3573e-117">IP</span></span> | <span data-ttu-id="3573e-118">1000/Minute</span><span class="sxs-lookup"><span data-stu-id="3573e-118">1000 / minute</span></span> | <span data-ttu-id="3573e-119">Abfragen von NuGet-Paketmetadaten über die v1-OData-Auflistung `Packages`</span><span class="sxs-lookup"><span data-stu-id="3573e-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="3573e-120">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="3573e-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="3573e-121">IP</span><span class="sxs-lookup"><span data-stu-id="3573e-121">IP</span></span> | <span data-ttu-id="3573e-122">3000/Minute</span><span class="sxs-lookup"><span data-stu-id="3573e-122">3000 / minute</span></span> | <span data-ttu-id="3573e-123">Suche nach NuGet-Paketen über den v1-Suche-Endpunkt</span><span class="sxs-lookup"><span data-stu-id="3573e-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="3573e-124">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="3573e-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="3573e-125">IP</span><span class="sxs-lookup"><span data-stu-id="3573e-125">IP</span></span> | <span data-ttu-id="3573e-126">20000/Minute</span><span class="sxs-lookup"><span data-stu-id="3573e-126">20000 / minute</span></span> | <span data-ttu-id="3573e-127">Abfragen von NuGet-Paketmetadaten über die v2-OData-Auflistung `Packages`</span><span class="sxs-lookup"><span data-stu-id="3573e-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="3573e-128">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="3573e-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="3573e-129">IP</span><span class="sxs-lookup"><span data-stu-id="3573e-129">IP</span></span> | <span data-ttu-id="3573e-130">100/Minute</span><span class="sxs-lookup"><span data-stu-id="3573e-130">100 / minute</span></span> | <span data-ttu-id="3573e-131">Anzahl der NuGet-Pakete über die v2-OData-Auflistung `Packages`</span><span class="sxs-lookup"><span data-stu-id="3573e-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="3573e-132">Package Push und Unlist</span><span class="sxs-lookup"><span data-stu-id="3573e-132">Package Push and Unlist</span></span>

| <span data-ttu-id="3573e-133">API</span><span class="sxs-lookup"><span data-stu-id="3573e-133">API</span></span> | <span data-ttu-id="3573e-134">Limit-Typ</span><span class="sxs-lookup"><span data-stu-id="3573e-134">Limit Type</span></span> | <span data-ttu-id="3573e-135">Limit-Wert</span><span class="sxs-lookup"><span data-stu-id="3573e-135">Limit Value</span></span> | <span data-ttu-id="3573e-136">API-UseCase</span><span class="sxs-lookup"><span data-stu-id="3573e-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="3573e-137">**Put** -`/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="3573e-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="3573e-138">API-Schlüssel</span><span class="sxs-lookup"><span data-stu-id="3573e-138">API Key</span></span> | <span data-ttu-id="3573e-139">350/Stunde</span><span class="sxs-lookup"><span data-stu-id="3573e-139">350 / hour</span></span> | <span data-ttu-id="3573e-140">Hochladen eines neuen NuGet-Pakets (Version) per v2-Push-Endpunkt</span><span class="sxs-lookup"><span data-stu-id="3573e-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="3573e-141">**DELETE** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="3573e-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="3573e-142">API-Schlüssel</span><span class="sxs-lookup"><span data-stu-id="3573e-142">API Key</span></span> | <span data-ttu-id="3573e-143">250/Stunde</span><span class="sxs-lookup"><span data-stu-id="3573e-143">250 / hour</span></span> | <span data-ttu-id="3573e-144">Entfernen eines NuGet-Pakets oder einer Paketversion über den v2-Endpunkt</span><span class="sxs-lookup"><span data-stu-id="3573e-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
