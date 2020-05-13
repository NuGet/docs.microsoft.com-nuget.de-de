---
title: Begrenzung der Datenübertragungs Rate, nuget-API
description: Die nuget-APIs verfügen über erzwungene Raten Limits, um Missbrauch zu verhindern.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367933"
---
# <a name="rate-limits"></a>Begrenzung der Bandbreite

Die NuGet.org-API erzwingt die Raten Begrenzung, um Missbrauch zu verhindern. Bei Anforderungen, die die Raten Begrenzung überschreiten, wird folgender Fehler zurückgegeben: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Zusätzlich zur Einschränkung der Einschränkung durch die Begrenzung der Datenübertragungsrate erzwingen einige APIs auch das Kontingent. Bei Anforderungen, die das Kontingent überschreiten, wird folgender Fehler zurückgegeben:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

In den folgenden Tabellen sind die Begrenzung der Datenübertragungsrate für die NuGet.org-API aufgeführt.

## <a name="package-search"></a>Paket Suche

> [!Note]
> Es wird empfohlen, die [V3-Suche-APIs](search-query-service-resource.md) von nuget. org zu verwenden, da es derzeit keine Raten Beschränkung gibt. Für v1-und v2-Such-APIs gelten die folgenden Grenzwerte:

| API | Beschränkungstyp | Limit-Wert | API-Anwendungsfall |
|:---|:---|:---|:---|
**GET** `/api/v1/Packages` | IP | 1000/Minute | Abfragen von nuget-Paket Metadaten über die v1-odata- `Packages` Sammlung |
**GET** `/api/v1/Search()` | IP | 3000/Minute | Suchen nach nuget-Paketen über den v1-Such Endpunkt | 
**GET** `/api/v2/Packages` | IP | 20000/Minute | Abfragen von nuget-Paket Metadaten über die V2-odata- `Packages` Sammlung | 
**GET** `/api/v2/Packages/$count` | IP | 100/Minute | Abfragen der nuget-Paket Anzahl über die V2-odata- `Packages` Sammlung | 

## <a name="package-push-and-unlist"></a>Package Push und Unlist

| API | Beschränkungstyp | Limit-Wert | API-Anwendungsfall | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | API-Schlüssel | 350/Stunde | Neues nuget-Paket (Version) über v2-Push-Endpunkt hochladen 
**Löschen**`/api/v2/package/{id}/{version}` | API-Schlüssel | 250/Stunde | Auflisten eines nuget-Pakets (Version) über den V2-Endpunkt 

## <a name="nugetorg-website-page-views"></a>nuget.org Website Ansichten von Websites

Wenn Sie Programm gesteuert auf die nuget.org-Webseiten zugreifen, sollten Sie eine Untersuchung unserer dokumentierten [V3-APIs](overview.md)in Erwägung zieht. Diese Endpunkte ermöglichen einen einfacheren Zugriff auf Paket Metadaten und-Inhalte. Die V3-API bietet eine bessere Verfügbarkeit und bietet eine höhere Leistung als der Zugriff auf die nuget-Katalog Webseiten, die für Webbrowser Interaktion entwickelt wurden.

| API | Beschränkungstyp | Limit-Wert | API-Anwendungsfall | 
|:---|:---|:---|:--- |
**GET** `/package/{id}/{version}` | IP | 50/Minute | Seite "Details zum Paket (Version)" anzeigen. 
