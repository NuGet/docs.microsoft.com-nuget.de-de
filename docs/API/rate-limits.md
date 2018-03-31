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
# <a name="rate-limits"></a>Begrenzung der Bandbreite

Der NuGet.org-API erzwingt die Begrenzung der Übertragungsrate um Missbrauch zu verhindern. Anforderungen, die die Begrenzung überschreiten zurückgegeben der folgende Fehler: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Die folgenden Tabellen enthalten die Begrenzung der Datenübertragungsrate für die NuGet.org-API.

## <a name="package-search"></a>Paket-Suche

> [!Note]
> Es wird empfohlen, sich der NuGet.org [V3-APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) derzeit für die Suche, die leistungsstarke und verfügen über keine beschränken. Suchen Sie nach V1 und V2 APIs, die Grenzwerte Followins gelten:


| API | Limittyp | Grenzwert | API-Anwendungsfall |
|:---|:---|:---|:---|
**GET** `/api/v1/Packages` | IP | 1000 / Minute | Abfragen von Metadaten von NuGet-Paketen über OData v1 `Packages` Auflistung |
**GET** `/api/v1/Search()` | IP | 3000 / Minute | Suchen Sie nach NuGet-Pakete über einen Endpunkt für v1-Suche | 
**GET** `/api/v2/Packages` | IP | 20000 / Minute | Abfragen von Metadaten von NuGet-Paketen über OData v2 `Packages` Auflistung | 
**GET** `/api/v2/Packages/$count` | IP | 100 / Minute | Anzahl von NuGet-Paket über v2 OData-Abfrage `Packages` Auflistung | 

## <a name="package-push-and-unlist"></a>Paket Push-als auch Benutzerauswahl

| API | Limittyp | Grenzwert | Hilfskraftturbine Anwendungsfall | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | API-Schlüssel | 100 / Minute | Hochladen Sie über v2-Push-Endpunkt ein neues NuGet-Paket (Version) 
**DELETE** `/api/v2/package/{id}/{version}` | API-Schlüssel | 100 / Minute | NuGet-Paket (Version) über einen Endpunkt v2 Benutzerauswahl 
