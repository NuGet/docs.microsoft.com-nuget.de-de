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
# <a name="rate-limits"></a>Begrenzung der Bandbreite

Die nuget.org-API erzwingt die Begrenzung der Datenübertragungsrate, um Missbrauch zu verhindern. Anforderungen, die die Begrenzung überschreiten, geben folgenden Fehler zurück: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Zusätzlich zu dem Fakt, dass Anforderungsbegrenzungen die Begrenzungen der Datenübertragungsrate verwenden, erzwingen manche APIs auch ein Kontingent. Anforderungen, die das Kontingent überschreiten, geben folgenden Fehler zurück:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

Die folgenden Tabellen enthalten die Begrenzungen für die nuget.org-API.

## <a name="package-search"></a>Paketsuche

> [!Note]
> Es wird empfohlen, die [V3-Suche-APIs](search-query-service-resource.md) von nuget. org zu verwenden, da es derzeit keine Raten Beschränkung gibt. Für v1-und v2-Such-APIs gelten die folgenden Grenzwerte:

| API | Limit-Typ | Limit-Wert | API-UseCase |
|:---|:---|:---|:---|
**GET** `/api/v1/Packages` | IP | 1000/Minute | Abfragen von NuGet-Paketmetadaten über die v1-OData-Auflistung `Packages` |
**GET** `/api/v1/Search()` | IP | 3000/Minute | Suche nach NuGet-Paketen über den v1-Suche-Endpunkt | 
**GET** `/api/v2/Packages` | IP | 20000/Minute | Abfragen von NuGet-Paketmetadaten über die v2-OData-Auflistung `Packages` | 
**GET** `/api/v2/Packages/$count` | IP | 100/Minute | Anzahl der NuGet-Pakete über die v2-OData-Auflistung `Packages` | 

## <a name="package-push-and-unlist"></a>Package Push und Unlist

| API | Limit-Typ | Limit-Wert | API-UseCase | 
|:---|:---|:---|:--- |
**Put** -`/api/v2/package` | API-Schlüssel | 350/Stunde | Hochladen eines neuen NuGet-Pakets (Version) per v2-Push-Endpunkt 
**DELETE** `/api/v2/package/{id}/{version}` | API-Schlüssel | 250/Stunde | Entfernen eines NuGet-Pakets oder einer Paketversion über den v2-Endpunkt 
