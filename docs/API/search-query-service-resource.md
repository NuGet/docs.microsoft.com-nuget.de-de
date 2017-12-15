---
title: Suchen, die NuGet-API | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 11ca2092-67dc-41a9-a7af-afe610d8febb
description: "Der Search-Dienst ermöglicht Clients zum Abfragen von Paketen von Schlüsselwort und Filterergebnisse auf bestimmte paketfelder."
keywords: "NuGet-Suchdienst-API, NuGet-Pakete, für Abfrage NuGet-Pakete, API-API zum Durchsuchen von NuGet-Pakete zu ermitteln"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 8b37c1bfb66290de49641a8b6197cb83cd35318a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="search"></a>Suchen

Es ist möglich, mithilfe der API V3 Paketquelle verfügbaren Pakete suchen. Ist die Ressource für die Suche verwendet die `SearchQueryService` Ressource gefunden, der [Dienst Index](service-index.md).

## <a name="versioning"></a>Versionskontrolle

Die folgenden `@type` Werte werden verwendet:

@type-Wert                   | Hinweise
----------------------------- | -----
SearchQueryService            | Die erste Version
SearchQueryService/3.0.0-beta | Alias der`SearchQueryService`
SearchQueryService/3.0.0-rc   | Alias der`SearchQueryService`

## <a name="base-url"></a>Basis-URL

Die base-URL für die folgende API wird der Wert von der `@id` mit einem der oben genannten Ressource verknüpfte Eigenschaft `@type` Werte. Im folgenden Dokument Platzhalter für die Basis-URL `{@id}` verwendet werden.

## <a name="http-methods"></a>HTTP-Methoden

Alle URLs, die bei der Unterstützung der Registrierung-Ressource gefunden, die HTTP-Methoden `GET` und `HEAD`.

## <a name="search-for-packages"></a>Suchen Sie nach Pakete

Die Such-API ermöglicht einem Client Abfrage für eine Seite der Pakete, die eine Abfrage für die angegebenen Suchkriterien entsprechen. Die Interpretation der Suchabfrage (z. B. die Tokenisierung der Suchbegriffe) richtet sich nach der Implementierung, aber der allgemeinen Annahme ist, dass die Suchabfrage verwendet wird, für den Abgleich von Paket-IDs, Titel, Beschreibungen und Tags. Andere Metadatenfelder Paket möglicherweise ebenfalls berücksichtigt werden.

Eine nicht aufgeführte Paket sollte nie in den Suchergebnissen angezeigt werden.

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a>Anforderungsparameter

Name        | In     | Typ    | Erforderlich | Hinweise
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | Nein       | Suchbegriffe zur Filter-Pakete
überspringen        | URL    | Ganze Zahl | Nein       | Die Anzahl der Ergebnisse für die Paginierung überspringen
Take        | URL    | Ganze Zahl | Nein       | Die Anzahl der zurückzugebenden Ergebnisseite, für die Paginierung
Vorabversion  | URL    | boolean | Nein       | `true`oder `false` bestimmen, ob enthalten [Vorabversion Pakete](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | Nein       | Eine Versionszeichenfolge SemVer 1.0.0 

Die Suchabfrage `q` wird analysiert, die in einer Weise, die durch die Implementierung definiert ist. NuGet.org unterstützt Standardfilter auf eine [Vielzahl von Feldern](../consume-packages/finding-and-choosing-packages.md#search-syntax). Wenn kein `q` angegeben wird, alle Pakete, innerhalb der Grenzen, die durch überspringen, und ergreifen Sie auferlegt, zurückgegeben werden sollen. Dadurch wird die Registerkarte "Durchsuchen" in der NuGet-Visual Studio-Umgebung.

Die `skip` Parameter beträgt standardmäßig 0.

Die `take` Parameter muss eine ganze Zahl größer als 0 (null) sein. Die Implementierung der Server kann einen maximalen Wert verursachen.

Wenn `prerelease` nicht angegeben wird, Vorabversion Paketen ausgeschlossen werden.

Die `semVerLevel` Query-Parameter wird verwendet, um abonnieren [SemVer 2.0.0 Pakete](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Wenn dieser Parameter ausgeschlossen ist, werden nur Pakete mit SemVer 1.0.0 kompatible Versionen zurückgegeben (mit der [standard NuGet Versioning](../reference/package-versioning.md) Vorsichtsmaßnahmen, z. B. Versionszeichenfolgen mit 4 Einheiten für ganze Zahl).
Wenn `semVerLevel=2.0.0` angegeben wird, SemVer 1.0.0 und SemVer 2.0.0 kompatibel Pakete zurückgegeben werden. Finden Sie unter der [SemVer 2.0.0-Unterstützung für nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) für Weitere Informationen.

### <a name="response"></a>Antwort

Die Antwort ist, enthält bis zu JSON-Dokument `take` Suchergebnissen. Suchergebnisse werden nach Paket-ID gruppiert.

Der Stamm-JSON-Objekt hat die folgenden Eigenschaften:

Name      | Typ             | Erforderlich | Hinweise
--------- | ---------------- | -------- | -----
totalHits | Ganze Zahl          | ja      | Die Gesamtzahl der Übereinstimmungen, Basiseigenschaft `skip` und`take`
Daten      | Array von Objekten | ja      | Die Suchergebnisse abgeglichen, die von der Anforderung

### <a name="search-result"></a>Suchergebnis

Jedes Element in der `data` Array ist ein JSON-Objekt, bestehend aus einer Gruppe von Paketversionen, die gemeinsame Nutzung der gleichen Paket-ID.
Das Objekt hat die folgenden Eigenschaften:

Name           | Typ                       | Erforderlich | Hinweise
-------------- | -------------------------- | -------- | -----
ID             | string                     | ja      | Die ID des übereinstimmenden Pakets
version        | string                     | ja      | Die vollständige SemVer 2.0.0 Versionszeichenfolge des Pakets (konnte die Build-Metadaten enthalten)
Beschreibung    | string                     | Nein       | 
Versionen       | Array von Objekten           | ja      | Alle Versionen der übereinstimmenden Paket die `prerelease` Parameter
authors        | Zeichenfolge oder ein Array von Zeichenfolgen | Nein       | 
iconUrl        | string                     | Nein       | 
licenseUrl     | string                     | Nein       | 
owners         | Zeichenfolge oder ein Array von Zeichenfolgen | Nein       | 
projectUrl     | string                     | Nein       | 
Registrierung   | string                     | Nein       | Die absolute URL an die zugeordnete [Registrierung Index](registration-base-url-resource.md#registration-index)
Zusammenfassung        | string                     | Nein       | 
Tags           | Zeichenfolge oder ein Array von Zeichenfolgen | Nein       | 
Titel          | string                     | Nein       | 
totalDownloads | Ganze Zahl                    | Nein       | Dieser Wert abgeleitet werden kann, durch die Summe der Downloads in den `versions` Array
Überprüft       | boolean                    | Nein       | Gibt an, ob das Paket ist JSON-Typ Boolean [überprüft](../reference/id-prefix-reservation.md)

Auf nuget.org ist ein überprüfter Paket eines, das eine Paket-ID entsprechen ein reserviertes ID-Präfix wurde und im Besitz einer reservierten Namespace-Besitzer an. Weitere Informationen finden Sie unter der [Dokumentation zur ID-Präfix Reservierung](../reference/id-prefix-reservation.md).

Die Metadaten in die Suche-Ergebnisobjekt enthaltenen stammt aus der aktuellen Paketversion. Jedes Element in der `versions` Array ist ein JSON-Objekt mit den folgenden Eigenschaften:

Name      | Typ    | Erforderlich | Hinweise
--------- | ------- | -------- | -----
@id       | string  | ja      | Die absolute URL an die zugeordnete [Registrierung Blattebene](registration-base-url-resource.md#registration-leaf)
version   | string  | ja      | Die vollständige SemVer 2.0.0 Versionszeichenfolge des Pakets (konnte die Build-Metadaten enthalten)
Downloads | Ganze Zahl | ja      | Die Anzahl der Downloads für diese bestimmte Paketversion

### <a name="sample-request"></a>Beispielanforderung

```
GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false
```

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [search-result.json](./_data/search-result.json)]
