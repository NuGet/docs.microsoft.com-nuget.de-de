---
title: Suche, nuget-API
description: Der Search-Dienst ermöglicht Clients das Abfragen von Paketen nach Schlüsselwort und das Filtern von Ergebnissen nach bestimmten Paket Feldern.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b898b389ee6c962831ce789a7c304c75e6bd8774
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488216"
---
# <a name="search"></a>Suchen

Es ist möglich, mithilfe der V3-API nach Paketen zu suchen, die in einer Paketquelle verfügbar sind. Die Ressource, die für die Suche `SearchQueryService` verwendet wird, ist die im [Dienst Index](service-index.md)gefundene Ressource.

## <a name="versioning"></a>Versionskontrolle

Die folgenden `@type` Werte werden verwendet:

@type -Wert                   | Hinweise
----------------------------- | -----
SearchQueryService            | Die erste Version
SearchQueryService/3.0.0-beta | Alias von`SearchQueryService`
SearchQueryService/3.0.0-rc   | Alias von`SearchQueryService`

## <a name="base-url"></a>Basis-URL

Die Basis-URL für die folgende API ist der Wert der `@id` Eigenschaft, die mit einem der oben erwähnten `@type` Ressourcen Werte verknüpft ist. Im folgenden Dokument wird die Platzhalter-Basis- `{@id}` URL verwendet.

## <a name="http-methods"></a>HTTP-Methoden

Alle URLs, die in der Registrierungs Ressource gefunden werden, `GET` unter `HEAD`stützen die HTTP-Methoden und.

## <a name="search-for-packages"></a>Nach Paketen suchen

Die Such-API ermöglicht einem Client, eine Seite von Paketen abzufragen, die mit einer bestimmten Suchabfrage übereinstimmen. Die Interpretation der Suchabfrage (z. b. die Tokenisierung der Suchbegriffe) wird von der Server Implementierung bestimmt, aber die allgemeine Erwartung ist, dass die Suchabfrage zum Abgleichen von Paket-IDs, Titeln, Beschreibungen und Tags verwendet wird. Andere paketmetadatenfelder können ebenfalls berücksichtigt werden.

Ein nicht aufgelistetes Paket sollte nie in den Suchergebnissen angezeigt werden.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Anforderungs Parameter

name        | In     | Typ    | Erforderlich | Hinweise
----------- | ------ | ------- | -------- | -----
q           | URL    | Zeichenfolge  | Nein       | Die Suchbegriffe, die zum Filtern von Paketen verwendet werden.
überspringen        | URL    | Ganze Zahl | Nein       | Die Anzahl der zu über springenden Ergebnisse für die Paginierung.
Rechnung        | URL    | Ganze Zahl | Nein       | Die Anzahl der zurück zugebende Ergebnisse für die Paginierung.
vorab  | URL    | boolean | Nein       | `true`oder `false` feststellen, ob [vorab Pakete](../create-packages/prerelease-packages.md) eingeschlossen werden sollen
semVerLevel | URL    | Zeichenfolge  | Nein       | Eine Versions Zeichenfolge für semver 1.0.0 

Die Suchabfrage `q` wird auf eine Weise analysiert, die durch die Server Implementierung definiert wird. nuget.org unterstützt die grundlegende Filterung für [verschiedene Felder](../consume-packages/finding-and-choosing-packages.md#search-syntax). Wenn kein `q` angegeben wird, sollten alle Pakete innerhalb der durch Skip und Take vorgegebenen Grenzen zurückgegeben werden. Dadurch wird die Registerkarte "Durchsuchen" in der nuget Visual Studio-Funktion aktiviert.

Der `skip` -Parameter hat den Standardwert 0.

Der `take` -Parameter muss eine ganze Zahl größer als 0 (null) sein. Die Server Implementierung kann einen maximalen Wert erzwingen.

Wenn `prerelease` nicht angegeben wird, werden vorab Versionen von Paketen ausgeschlossen.

Der `semVerLevel` -Abfrage Parameter wird verwendet, um [semver 2.0.0-Pakete](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)zu abonnieren.
Wenn dieser Abfrage Parameter ausgeschlossen wird, werden nur Pakete mit mit semver 1.0.0 kompatiblen Versionen zurückgegeben (mit der [standardmäßigen nuget-Versions](../concepts/package-versioning.md) Kontrolle, z. b. Versions Zeichenfolgen mit vier ganzzahligen teilen).
Wenn `semVerLevel=2.0.0` angegeben wird, werden sowohl das semver 1.0.0-als auch das semver 2.0.0-kompatible Paket zurückgegeben. Weitere Informationen finden Sie [unter der semver 2.0.0-Unterstützung für nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Antwort

Die Antwort ist das JSON-Dokument, `take` das die Suchergebnisse enthält. Die Suchergebnisse werden nach der Paket-ID gruppiert.

Das JSON-Stamm Objekt verfügt über die folgenden Eigenschaften:

Name      | Typ             | Erforderlich | Hinweise
--------- | ---------------- | -------- | -----
totalhits | Ganze Zahl          | ja      | Die Gesamtanzahl der Übereinstimmungen, `skip` wobei und ignoriert werden.`take`
Daten      | Array von Objekten | ja      | Die Suchergebnisse, die mit der Anforderung übereinstimmen.

### <a name="search-result"></a>Suchergebnis

Jedes Element im `data` Array ist ein JSON-Objekt, das aus einer Gruppe von Paketversionen besteht, die dieselbe Paket-ID nutzen.
Das-Objekt verfügt über die folgenden Eigenschaften:

Name           | Typ                       | Erforderlich | Hinweise
-------------- | -------------------------- | -------- | -----
id             | string                     | ja      | Die ID des übereinstimmenden Pakets.
version        | string                     | ja      | Die vollständige semver 2.0.0-Versions Zeichenfolge des Pakets (kann buildmetadaten enthalten)
description    | string                     | Nein       | 
Versionen       | Array von Objekten           | ja      | Alle Versionen des Pakets, die dem `prerelease` Parameter entsprechen
authors        | Zeichenfolge oder Array von Zeichen folgen | Nein       | 
iconUrl        | string                     | Nein       | 
licenseUrl     | string                     | Nein       | 
owners         | Zeichenfolge oder Array von Zeichen folgen | Nein       | 
projectUrl     | string                     | Nein       | 
Registrierung   | string                     | Nein       | Die absolute URL zum zugeordneten [Registrierungs Index](registration-base-url-resource.md#registration-index) .
summary        | string                     | Nein       | 
tags           | Zeichenfolge oder Array von Zeichen folgen | Nein       | 
title          | string                     | Nein       | 
totalDownloads | Ganze Zahl                    | Nein       | Dieser Wert kann durch die Summe der Downloads im `versions` Array abgeleitet werden.
Zier       | boolean                    | Nein       | Ein JSON-boolescher Wert, der angibt, ob das Paket [überprüft](../nuget-org/id-prefix-reservation.md) wird.

In nuget.org ist ein verifiziertes Paket ein überprüftes Paket, das über eine Paket-ID verfügt, die mit einem reservierten ID-Präfix übereinstimmt und im Besitz eines der reservierten Präfix Weitere Informationen finden Sie in der [Dokumentation zur ID-Präfix Reservierung](../reference/id-prefix-reservation.md).

Die Metadaten, die im Suchergebnis Objekt enthalten sind, stammen aus der aktuellen Paketversion. Jedes Element im `versions` Array ist ein JSON-Objekt mit den folgenden Eigenschaften:

Name      | Typ    | Erforderlich | Hinweise
--------- | ------- | -------- | -----
@id       | string  | ja      | Die absolute URL zum zugeordneten [Registrierungs Blatt](registration-base-url-resource.md#registration-leaf) .
version   | string  | ja      | Die vollständige semver 2.0.0-Versions Zeichenfolge des Pakets (kann buildmetadaten enthalten)
lädt | Ganze Zahl | ja      | Die Anzahl der Downloads für diese bestimmte Paketversion.

### <a name="sample-request"></a>Beispiel Anforderung

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>Beispiel Antwort

[!code-JSON [search-result.json](./_data/search-result.json)]
