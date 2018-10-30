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
# <a name="rate-limits"></a>Begrenzung der Bandbreite

Der NuGet.org-API erzwingt, um Missbrauch zu verhindern, dass die Begrenzung der Übertragungsrate. Anforderungen, die die ratenbegrenzung überschreiten zurückgegeben der folgende Fehler: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Erzwingen Sie zusätzlich zu den für die anforderungsbegrenzung mit Begrenzung der Datenübertragungsrate, einige APIs ebenfalls Kontingent aus. Anforderungen, die das Kontingent überschreiten. zurück folgende Fehlermeldung:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

Die folgenden Tabellen enthalten die Begrenzung der Datenübertragungsrate für die API "NuGet.org".

## <a name="package-search"></a>Paket suchen

> [!Note]
> Es wird empfohlen, NuGet.org [V3-APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) derzeit für die Suche, die leistungsstarke und verfügen über keine beschränken. APIs für V1 und V2-Suche, die Followins Grenzwerte gelten:


| API | Limit-Typ | Grenzwert | API-Anwendungsfall |
|:---|:---|:---|:---|
**ERHALTEN** `/api/v1/Packages` | IP | 1000 / Minute | Abfragen von NuGet-Paketmetadaten über v1 OData `Packages` Auflistung |
**ERHALTEN** `/api/v1/Search()` | IP | 3000 / Minute | Suchen Sie nach NuGet-Pakete über die v1-Suche-Endpunkt | 
**ERHALTEN** `/api/v2/Packages` | IP | 20000 / Minute | Abfragen von NuGet-Paketmetadaten über v2 OData `Packages` Auflistung | 
**ERHALTEN** `/api/v2/Packages/$count` | IP | 100 / Minute | Anzahl der NuGet-Pakete über v2 OData Abfragen `Packages` Auflistung | 

## <a name="package-push-and-unlist"></a>Paket mithilfe von Push übertragen und aus der Liste entfernen

| API | Limit-Typ | Grenzwert | API-Anwendungsfall | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | API-Schlüssel | 250 / Stunde | Hochladen eines neuen NuGet-Pakets (Version) per Push-v2-Endpunkt 
**LÖSCHEN** `/api/v2/package/{id}/{version}` | API-Schlüssel | 250 / Stunde | Entfernen Sie ein NuGet-Paket (Version) über die v2-Endpunkt aus der Liste 
