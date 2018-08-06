---
title: Begrenzung der Datenübertragungsrate, NuGet-API
description: Die NuGet-APIs werden Begrenzung der Datenübertragungsrate Missbrauch zu verhindern, dass erzwungen haben.
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: a55eb49318b766028d1579a4d33618617bbd8801
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508126"
---
# <a name="rate-limits"></a><span data-ttu-id="5ee4e-103">Begrenzung der Bandbreite</span><span class="sxs-lookup"><span data-stu-id="5ee4e-103">Rate Limits</span></span>

<span data-ttu-id="5ee4e-104">Der NuGet.org-API erzwingt, um Missbrauch zu verhindern, dass die Begrenzung der Übertragungsrate.</span><span class="sxs-lookup"><span data-stu-id="5ee4e-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="5ee4e-105">Anforderungen, die die ratenbegrenzung überschreiten zurückgegeben der folgende Fehler:</span><span class="sxs-lookup"><span data-stu-id="5ee4e-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="5ee4e-106">Erzwingen Sie zusätzlich zu den für die anforderungsbegrenzung mit Begrenzung der Datenübertragungsrate, einige APIs ebenfalls Kontingent aus.</span><span class="sxs-lookup"><span data-stu-id="5ee4e-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="5ee4e-107">Anforderungen, die das Kontingent überschreiten. zurück folgende Fehlermeldung:</span><span class="sxs-lookup"><span data-stu-id="5ee4e-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="5ee4e-108">Die folgenden Tabellen enthalten die Begrenzung der Datenübertragungsrate für die API "NuGet.org".</span><span class="sxs-lookup"><span data-stu-id="5ee4e-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="5ee4e-109">Paket suchen</span><span class="sxs-lookup"><span data-stu-id="5ee4e-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="5ee4e-110">Es wird empfohlen, NuGet.org [V3-APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) derzeit für die Suche, die leistungsstarke und verfügen über keine beschränken.</span><span class="sxs-lookup"><span data-stu-id="5ee4e-110">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="5ee4e-111">APIs für V1 und V2-Suche, die Followins Grenzwerte gelten:</span><span class="sxs-lookup"><span data-stu-id="5ee4e-111">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="5ee4e-112">API</span><span class="sxs-lookup"><span data-stu-id="5ee4e-112">API</span></span> | <span data-ttu-id="5ee4e-113">-Typ</span><span class="sxs-lookup"><span data-stu-id="5ee4e-113">Limit Type</span></span> | <span data-ttu-id="5ee4e-114">Grenzwert</span><span class="sxs-lookup"><span data-stu-id="5ee4e-114">Limit Value</span></span> | <span data-ttu-id="5ee4e-115">API-Anwendungsfall</span><span class="sxs-lookup"><span data-stu-id="5ee4e-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="5ee4e-116">**ERHALTEN** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="5ee4e-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="5ee4e-117">IP</span><span class="sxs-lookup"><span data-stu-id="5ee4e-117">IP</span></span> | <span data-ttu-id="5ee4e-118">1000 / Minute</span><span class="sxs-lookup"><span data-stu-id="5ee4e-118">1000 / minute</span></span> | <span data-ttu-id="5ee4e-119">Abfragen von NuGet-Paketmetadaten über v1 OData `Packages` Auflistung</span><span class="sxs-lookup"><span data-stu-id="5ee4e-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="5ee4e-120">**ERHALTEN** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="5ee4e-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="5ee4e-121">IP</span><span class="sxs-lookup"><span data-stu-id="5ee4e-121">IP</span></span> | <span data-ttu-id="5ee4e-122">3000 / Minute</span><span class="sxs-lookup"><span data-stu-id="5ee4e-122">3000 / minute</span></span> | <span data-ttu-id="5ee4e-123">Suchen Sie nach NuGet-Pakete über die v1-Suche-Endpunkt</span><span class="sxs-lookup"><span data-stu-id="5ee4e-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="5ee4e-124">**ERHALTEN** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="5ee4e-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="5ee4e-125">IP</span><span class="sxs-lookup"><span data-stu-id="5ee4e-125">IP</span></span> | <span data-ttu-id="5ee4e-126">20000 / Minute</span><span class="sxs-lookup"><span data-stu-id="5ee4e-126">20000 / minute</span></span> | <span data-ttu-id="5ee4e-127">Abfragen von NuGet-Paketmetadaten über v2 OData `Packages` Auflistung</span><span class="sxs-lookup"><span data-stu-id="5ee4e-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="5ee4e-128">**ERHALTEN** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="5ee4e-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="5ee4e-129">IP</span><span class="sxs-lookup"><span data-stu-id="5ee4e-129">IP</span></span> | <span data-ttu-id="5ee4e-130">100 / Minute</span><span class="sxs-lookup"><span data-stu-id="5ee4e-130">100 / minute</span></span> | <span data-ttu-id="5ee4e-131">Anzahl der NuGet-Pakete über v2 OData Abfragen `Packages` Auflistung</span><span class="sxs-lookup"><span data-stu-id="5ee4e-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="5ee4e-132">Paket mithilfe von Push übertragen und aus der Liste entfernen</span><span class="sxs-lookup"><span data-stu-id="5ee4e-132">Package Push and Unlist</span></span>

| <span data-ttu-id="5ee4e-133">API</span><span class="sxs-lookup"><span data-stu-id="5ee4e-133">API</span></span> | <span data-ttu-id="5ee4e-134">-Typ</span><span class="sxs-lookup"><span data-stu-id="5ee4e-134">Limit Type</span></span> | <span data-ttu-id="5ee4e-135">Grenzwert</span><span class="sxs-lookup"><span data-stu-id="5ee4e-135">Limit Value</span></span> | <span data-ttu-id="5ee4e-136">API-Anwendungsfall</span><span class="sxs-lookup"><span data-stu-id="5ee4e-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="5ee4e-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="5ee4e-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="5ee4e-138">API-Schlüssel</span><span class="sxs-lookup"><span data-stu-id="5ee4e-138">API Key</span></span> | <span data-ttu-id="5ee4e-139">250 / Stunde</span><span class="sxs-lookup"><span data-stu-id="5ee4e-139">250 / hour</span></span> | <span data-ttu-id="5ee4e-140">Hochladen eines neuen NuGet-Pakets (Version) per Push-v2-Endpunkt</span><span class="sxs-lookup"><span data-stu-id="5ee4e-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="5ee4e-141">**LÖSCHEN** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="5ee4e-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="5ee4e-142">API-Schlüssel</span><span class="sxs-lookup"><span data-stu-id="5ee4e-142">API Key</span></span> | <span data-ttu-id="5ee4e-143">250 / Stunde</span><span class="sxs-lookup"><span data-stu-id="5ee4e-143">250 / hour</span></span> | <span data-ttu-id="5ee4e-144">Entfernen Sie ein NuGet-Paket (Version) über die v2-Endpunkt aus der Liste</span><span class="sxs-lookup"><span data-stu-id="5ee4e-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
