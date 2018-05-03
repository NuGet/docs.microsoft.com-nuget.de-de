---
title: Begrenzung der Datenübertragungsrate NuGet-API
description: Die NuGet-APIs werden erzwungen, um Missbrauch zu verhindern, dass die Begrenzung der Datenübertragungsrate haben.
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 3aaebef8fff670759c6484a5a8f90a2f4dd58c66
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
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
**ERHALTEN** `/api/v1/Packages` | IP | 1000 / Minute | Abfragen von Metadaten von NuGet-Paketen über OData v1 `Packages` Auflistung |
**ERHALTEN** `/api/v1/Search()` | IP | 3000 / Minute | Suchen Sie nach NuGet-Pakete über einen Endpunkt für v1-Suche | 
**ERHALTEN** `/api/v2/Packages` | IP | 20000 / Minute | Abfragen von Metadaten von NuGet-Paketen über OData v2 `Packages` Auflistung | 
**ERHALTEN** `/api/v2/Packages/$count` | IP | 100 / Minute | Anzahl von NuGet-Paket über v2 OData-Abfrage `Packages` Auflistung | 

## <a name="package-push-and-unlist"></a>Paket Push-als auch Benutzerauswahl

| API | Limittyp | Grenzwert | Hilfskraftturbine Anwendungsfall | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | API-Schlüssel | 100 / Minute | Hochladen Sie über v2-Push-Endpunkt ein neues NuGet-Paket (Version) 
**LÖSCHEN** `/api/v2/package/{id}/{version}` | API-Schlüssel | 100 / Minute | NuGet-Paket (Version) über einen Endpunkt v2 Benutzerauswahl 
