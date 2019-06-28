---
title: Suchen, NuGet-API
description: Der Search-Dienst ermöglicht Clients, die zum Abfragen von Paketen vom Schlüsselwort und Filterergebnisse auf bestimmte paketfelder.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d462b289c39c2dd1418304dabcad47d0d4217f82
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426730"
---
# <a name="search"></a>Suchen

Es ist möglich, die auf eine Paketquelle, die mithilfe der V3-API verfügbaren Paketen suchen. Die Ressource für die Suche verwendet die `SearchQueryService` Ressource finden Sie in der [dienstindex](service-index.md).

## <a name="versioning"></a>Versionskontrolle

Die folgenden `@type` Werte werden verwendet:

@type -Wert                   | Hinweise
----------------------------- | -----
SearchQueryService            | Die erste Version
SearchQueryService/3.0.0-beta | Alias der `SearchQueryService`
SearchQueryService/3.0.0-rc   | Alias der `SearchQueryService`

## <a name="base-url"></a>Basis-URL

Die base-URL für die folgende API wird der Wert des der `@id` Eigenschaft, die einer der oben genannten Ressource zugeordneten `@type` Werte. Basis-URL im folgenden Dokument der Platzhalter `{@id}` verwendet werden.

## <a name="http-methods"></a>HTTP-Methoden

Alle URLs finden Sie in die Registrierung Unterstützung der HTTP-Methoden `GET` und `HEAD`.

## <a name="search-for-packages"></a>Nach Paketen suchen

Die Such-API ermöglicht einem Client Abfrage für eine Seite von Paketen, die mit einer angegebenen Abfrage übereinstimmen. Die Interpretation der Suchabfrage (z. B. die Tokenisierung der Suchbegriffe) richtet sich nach der Implementierung der Server jedoch Allgemein damit zu rechnen, dass die Abfrage verwendet wird, für den Abgleich von Paket-IDs, Titel, Beschreibungen und Tags. Andere Metadatenfelder Paket können ebenfalls berücksichtigt werden.

Ein nicht aufgelistetes Paket sollte nie in den Suchergebnissen angezeigt werden.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Anforderungsparameter

name        | In     | Typ    | Erforderlich | Hinweise
----------- | ------ | ------- | -------- | -----
q           | URL    | Zeichenfolge  | Nein       | Suchbegriffe verwendet, um die Filter-Pakete
überspringen        | URL    | Ganze Zahl | Nein       | Die Anzahl von Ergebnissen für die Paginierung überspringen
Take        | URL    | Ganze Zahl | Nein       | Die Anzahl der zurückzugebenden Ergebnisse, für die Paginierung
Vorabversion  | URL    | boolean | Nein       | `true` oder `false` bestimmen, ob enthalten [Vorabversionen von Paketen](../create-packages/prerelease-packages.md)
semVerLevel | URL    | Zeichenfolge  | Nein       | Eine Versionszeichenfolge SemVer 1.0.0 

Die Suchabfrage `q` wird analysiert, in einer Weise, die von der serverimplementierung definiert ist. "NuGet.org" unterstützen das einfache Filtern anhand einer [Vielzahl von Feldern](../consume-packages/finding-and-choosing-packages.md#search-syntax). Wenn kein `q` bereitgestellt wird, werden alle Pakete, innerhalb der Grenzen von Skip und Take auferlegt, zurückgegeben werden sollen. Dadurch wird die Registerkarte "Durchsuchen" in NuGet Visual Studio zu erleichtern.

Die `skip` Parameter hat den Standardwert 0.

Die `take` Parameter muss eine ganze Zahl größer als 0 (null) sein. Die Server-Implementierung kann es sich um einen maximalen Wert verursachen.

Wenn `prerelease` ist nicht angegeben wird, Vorabversionen von Paketen ausgeschlossen werden.

Die `semVerLevel` Query-Parameter wird verwendet, um abonnieren [SemVer 2.0.0 Pakete](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Wenn dieser Parameter ausgeschlossen wird, werden nur Pakete mit SemVer 1.0.0 kompatible Versionen zurückgegeben werden (mit der [standard NuGet-Versionsschema](../reference/package-versioning.md) Einschränkungen, z. B. Versionszeichenfolgen mit 4 Einheiten für ganze Zahl).
Wenn `semVerLevel=2.0.0` bereitgestellt wird, werden sowohl SemVer 1.0.0 und kompatiblen Paketen SemVer 2.0.0 zurückgegeben werden. Finden Sie unter den [SemVer 2.0.0-Unterstützung für "NuGet.org"](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) für Weitere Informationen.

### <a name="response"></a>Antwort

Die Antwort ist die JSON-Dokument mit bis zu `take` Suchergebnisse. Suchergebnisse werden nach Paket-ID gruppiert.

Die JSON-Stammobjekt hat die folgenden Eigenschaften:

Name      | Typ             | Erforderlich | Hinweise
--------- | ---------------- | -------- | -----
totalHits | Ganze Zahl          | ja      | Die Gesamtzahl der Übereinstimmungen ohne Berücksichtigung der `skip` und `take`
Daten      | Array von Objekten | ja      | Die Ergebnisse der Suche, die von der Anforderung übereinstimmen

### <a name="search-result"></a>Suchergebnis

Jedes Element in der `data` Array ist ein JSON-Objekt, bestehend aus einer Gruppe von Paketversionen, die gemeinsame Nutzung der gleichen Paket-ID.
Das Objekt hat die folgenden Eigenschaften:

Name           | Typ                       | Erforderlich | Hinweise
-------------- | -------------------------- | -------- | -----
id             | Zeichenfolge                     | ja      | Die ID des übereinstimmenden-Pakets
version        | Zeichenfolge                     | ja      | Die vollständige Zeichenfolge der SemVer 2.0.0-Version des Pakets (kann die Build-Metadaten enthalten)
description    | Zeichenfolge                     | Nein       | 
Versionen       | Array von Objekten           | ja      | Alle Versionen der übereinstimmenden Paket die `prerelease` Parameter
authors        | Zeichenfolge oder Array von Zeichenfolgen | Nein       | 
iconUrl        | Zeichenfolge                     | Nein       | 
licenseUrl     | Zeichenfolge                     | Nein       | 
owners         | Zeichenfolge oder Array von Zeichenfolgen | Nein       | 
projectUrl     | Zeichenfolge                     | Nein       | 
Registrierung   | Zeichenfolge                     | Nein       | Die absolute URL an die zugeordnete [Registrierung Index](registration-base-url-resource.md#registration-index)
summary        | Zeichenfolge                     | Nein       | 
tags           | Zeichenfolge oder Array von Zeichenfolgen | Nein       | 
title          | Zeichenfolge                     | Nein       | 
totalDownloads | Ganze Zahl                    | Nein       | Dieser Wert abgeleitet werden kann, durch die Summe der Downloads in den `versions` Array
überprüft       | boolean                    | Nein       | Ein JSON-boolescher Wert, der angibt, ob das Paket [überprüft](../nuget-org/id-prefix-reservation.md)

Auf nuget.org ist ein verifizierter Paket eine hat die Paket-ID, die ein reservierte ID-Präfix und im Besitz einer der Besitzer von dem reservierten Präfix. Weitere Informationen finden Sie unter den [Dokumentation zu ID-präfixreservierung](../reference/id-prefix-reservation.md).

Die im Ergebnisobjekt Suche enthaltene Metadaten stammen aus der aktuellen Paketversion. Jedes Element in der `versions` Array ist ein JSON-Objekt mit den folgenden Eigenschaften:

Name      | Typ    | Erforderlich | Hinweise
--------- | ------- | -------- | -----
@id       | Zeichenfolge  | ja      | Die absolute URL an die zugeordnete [Registrierung Blattelemente](registration-base-url-resource.md#registration-leaf)
version   | Zeichenfolge  | ja      | Die vollständige Zeichenfolge der SemVer 2.0.0-Version des Pakets (kann die Build-Metadaten enthalten)
downloads | Ganze Zahl | ja      | Die Anzahl der Downloads für diese spezielle Version des Pakets

### <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [search-result.json](./_data/search-result.json)]
