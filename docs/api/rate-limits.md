---
title: Bandbreitenbegrenzungen, NuGet-API
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
# <a name="rate-limits"></a>Begrenzung der Bandbreite

Die nuget.org-API erzwingt Ratenbegrenzungen, um Missbrauch zu verhindern. Anfragen, die die Begrenzung überschreiten, geben folgenden Fehler zurück:

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Zusätzlich zu den Ratenbegrenzungen erzwingen manche APIs auch ein Kontingent. Anfragen, die das Kontingent überschreiten, geben folgenden Fehler zurück:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

Die folgenden Tabellen enthalten die Begrenzungen für die nuget.org-API.

## <a name="package-search"></a>Paketsuche

> [!Note]
> Es wird empfohlen, die nuget.org [V3-APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) für die Suche zu nutzen. Diese sind performant und haben momentan kein Limit. Für die V1- und V2-Such-APIs gelten die folgenden Limits:


| API | Limit-Typ | Grenzwert | API-Anwendungsfall |
|:---|:---|:---|:---|
**GET** `/api/v1/Packages` | IP | 1000 / Minute | Abfragen von NuGet-Paketmetadaten über die v1-OData-Auflistung `Packages`|
**GET** `/api/v1/Search()` | IP | 3000 / Minute | Suche nach NuGet-Paketen über den v1-Suche-Endpunkt |
**GET** `/api/v2/Packages` | IP | 20000 / Minute | Abfragen von NuGet-Paketmetadaten über die v2-OData-Auflistung `Packages` |
**GET** `/api/v2/Packages/$count` | IP | 100 / Minute | Anzahl der NuGet-Pakete über die v2-OData-Auflistung `Packages` |

## <a name="package-push-and-unlist"></a>Paket mit Push übertragen und aus der Liste entfernen

| API | Limit-Typ | Grenzwert | API-Anwendungsfall |
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | API-Schlüssel | 250 / Stunde | Hochladen eines neuen NuGet-Pakets (Version) per v2-Push-Endpunkt
**DELETE** `/api/v2/package/{id}/{version}` | API-Schlüssel | 250 / Stunde | Entfernen eines NuGet-Pakets oder einer Paketversion über den v2-Endpunkt
