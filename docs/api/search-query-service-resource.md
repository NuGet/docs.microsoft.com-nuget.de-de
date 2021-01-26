---
title: Suche, nuget-API
description: Der Search-Dienst ermöglicht Clients das Abfragen von Paketen nach Schlüsselwort und das Filtern von Ergebnissen nach bestimmten Paket Feldern.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 7047dfd48b7f93756bbb1491de1b7e65da2c12b4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775404"
---
# <a name="search"></a>Suchen,

Es ist möglich, mithilfe der V3-API nach Paketen zu suchen, die in einer Paketquelle verfügbar sind. Die Ressource, die für die Suche verwendet wird, ist die `SearchQueryService` im [Dienst Index](service-index.md)gefundene Ressource.

## <a name="versioning"></a>Versionsverwaltung

Die folgenden `@type` Werte werden verwendet:

Wert vom Typ @type                   | Hinweise
----------------------------- | -----
Searchqueryservice            | Die erste Version
Searchqueryservice/3.0.0-Beta | Alias von `SearchQueryService`
Searchqueryservice/3.0.0-RC   | Alias von `SearchQueryService`
Searchqueryservice/3.5.0      | Enthält Unterstützung für `packageType` Abfrage Parameter.

### <a name="searchqueryservice350"></a>Searchqueryservice/3.5.0
Diese Version führt die Unterstützung für den `packageType` Abfrage Parameter und die Response-Eigenschaft ein und `packageTypes` ermöglicht das Filtern nach Autor definierten Pakettypen. Es ist vollständig abwärts kompatibel mit Abfragen an `SearchQueryService` .

## <a name="base-url"></a>Basis-URL

Die Basis-URL für die folgende API ist der Wert der `@id` Eigenschaft, die mit einem der oben erwähnten Ressourcen Werte verknüpft ist `@type` . Im folgenden Dokument wird die Platzhalter-Basis-URL `{@id}` verwendet.

## <a name="http-methods"></a>HTTP-Methoden

Alle URLs, die in der Registrierungs Ressource gefunden werden, unterstützen die HTTP `GET` -Methoden und `HEAD` .

## <a name="search-for-packages"></a>Nach Paketen suchen

Die Such-API ermöglicht einem Client, eine Seite von Paketen abzufragen, die mit einer bestimmten Suchabfrage übereinstimmen. Die Interpretation der Suchabfrage (z. b. die Tokenisierung der Suchbegriffe) wird von der Server Implementierung bestimmt, aber die allgemeine Erwartung ist, dass die Suchabfrage zum Abgleichen von Paket-IDs, Titeln, Beschreibungen und Tags verwendet wird. Andere paketmetadatenfelder können ebenfalls berücksichtigt werden.

Ein nicht aufgelistetes Paket sollte nie in den Suchergebnissen angezeigt werden.

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}
```

### <a name="request-parameters"></a>Anforderungsparameter

Name        | In     | Typ    | Erforderlich | Notizen
----------- | ------ | ------- | -------- | -----
q           | URL    | Zeichenfolge  | nein       | Die Suchbegriffe, die zum Filtern von Paketen verwendet werden.
skip        | URL    | integer | Nein       | Die Anzahl der zu über springenden Ergebnisse für die Paginierung.
take        | URL    | integer | Nein       | Die Anzahl der zurück zugebende Ergebnisse für die Paginierung.
prerelease  | URL    | boolean | Nein       | `true`oder `false` feststellen, ob [vorab Pakete](../create-packages/prerelease-packages.md) eingeschlossen werden sollen
semverlevel | URL    | Zeichenfolge  | nein       | Eine Versions Zeichenfolge für semver 1.0.0 
packageType | URL    | Zeichenfolge  | nein       | Der Pakettyp, der zum Filtern von Paketen verwendet wird (in hinzugefügt `SearchQueryService/3.5.0` ).

Die Suchabfrage `q` wird auf eine Weise analysiert, die durch die Server Implementierung definiert wird. nuget.org unterstützt die grundlegende Filterung für [verschiedene Felder](../consume-packages/finding-and-choosing-packages.md#search-syntax). Wenn kein `q` angegeben wird, sollten alle Pakete innerhalb der durch Skip und Take vorgegebenen Grenzen zurückgegeben werden. Dadurch wird die Registerkarte "Durchsuchen" in der nuget Visual Studio-Funktion aktiviert.

Der-Parameter hat den `skip` Standardwert 0.

Der- `take` Parameter muss eine ganze Zahl größer als 0 (null) sein. Die Server Implementierung kann einen maximalen Wert erzwingen.

Wenn `prerelease` nicht angegeben wird, werden vorab Versionen von Paketen ausgeschlossen.

Der `semVerLevel` -Abfrage Parameter wird verwendet, um [semver 2.0.0-Pakete](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)zu abonnieren.
Wenn dieser Abfrage Parameter ausgeschlossen wird, werden nur Pakete mit mit semver 1.0.0 kompatiblen Versionen zurückgegeben (mit der [standardmäßigen nuget-Versions](../concepts/package-versioning.md) Kontrolle, z. b. Versions Zeichenfolgen mit vier ganzzahligen teilen).
Wenn `semVerLevel=2.0.0` angegeben wird, werden sowohl das semver 1.0.0-als auch das semver 2.0.0-kompatible Paket zurückgegeben. Weitere Informationen finden Sie [unter der semver 2.0.0-Unterstützung für nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

Der- `packageType` Parameter wird verwendet, um die Suchergebnisse auf Pakete zu filtern, die mindestens einen Pakettyp aufweisen, der mit dem Pakettyp Namen übereinstimmt.
Wenn es sich bei dem bereitgestellten Pakettyp nicht um einen gültigen Pakettyp handelt, wie vom [Pakettyp Dokument](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D)definiert, wird ein leeres Ergebnis zurückgegeben.
Wenn der bereitgestellte Pakettyp leer ist, wird kein Filter angewendet. Anders ausgedrückt: das Übergeben von No Value an den PackageType-Parameter verhält sich so, als ob der Parameter nicht übergeben würde.

### <a name="response"></a>Antwort

Die Antwort ist das JSON-Dokument, das die `take` Suchergebnisse enthält. Die Suchergebnisse werden nach der Paket-ID gruppiert.

Das JSON-Stamm Objekt verfügt über die folgenden Eigenschaften:

Name      | Typ             | Erforderlich | Notizen
--------- | ---------------- | -------- | -----
totalhits | integer          | ja      | Die Gesamtanzahl der Übereinstimmungen, wobei und ignoriert werden. `skip``take`
data      | Array von Objekten | ja      | Die Suchergebnisse, die mit der Anforderung übereinstimmen.

### <a name="search-result"></a>Suchergebnis

Jedes Element im `data` Array ist ein JSON-Objekt, das aus einer Gruppe von Paketversionen besteht, die dieselbe Paket-ID nutzen.
Das Objekt hat die folgenden Eigenschaften:

Name           | Typ                       | Erforderlich | Notizen
-------------- | -------------------------- | -------- | -----
id             | Zeichenfolge                     | ja      | Die ID des übereinstimmenden Pakets.
version        | Zeichenfolge                     | ja      | Die vollständige semver 2.0.0-Versions Zeichenfolge des Pakets (kann buildmetadaten enthalten)
description    | Zeichenfolge                     | nein       | 
versions       | Array von Objekten           | ja      | Alle Versionen des Pakets, die dem Parameter entsprechen `prerelease`
authors        | Zeichenfolge oder Array von Zeichenfolgen | Nein       | 
iconUrl        | Zeichenfolge                     | nein       | 
licenseUrl     | Zeichenfolge                     | nein       | 
owners         | Zeichenfolge oder Array von Zeichenfolgen | Nein       | 
projectUrl     | Zeichenfolge                     | nein       | 
Registrierung   | Zeichenfolge                     | nein       | Die absolute URL zum zugeordneten [Registrierungs Index](registration-base-url-resource.md#registration-index) .
Zusammenfassung        | Zeichenfolge                     | nein       | 
tags           | Zeichenfolge oder Array von Zeichenfolgen | Nein       | 
title          | Zeichenfolge                     | nein       | 
totaldownloads | integer                    | Nein       | Dieser Wert kann durch die Summe der Downloads im Array abgeleitet werden. `versions`
Zier       | boolean                    | Nein       | Ein JSON-boolescher Wert, der angibt, ob das Paket [überprüft](../nuget-org/id-prefix-reservation.md) wird.
packageTypes   | Array von Objekten           | ja      | Die vom Paket Ersteller definierten Pakettypen (in hinzugefügt `SearchQueryService/3.5.0` ).

In nuget.org ist ein verifiziertes Paket ein überprüftes Paket, das über eine Paket-ID verfügt, die mit einem reservierten ID-Präfix übereinstimmt und im Besitz eines der reservierten Präfix Weitere Informationen finden Sie in der [Dokumentation zur ID-Präfix Reservierung](../nuget-org/id-prefix-reservation.md).

Die Metadaten, die im Suchergebnis Objekt enthalten sind, stammen aus der aktuellen Paketversion. Jedes Element im `versions` Array ist ein JSON-Objekt mit den folgenden Eigenschaften:

Name      | Typ    | Erforderlich | Notizen
--------- | ------- | -------- | -----
@id       | Zeichenfolge  | ja      | Die absolute URL zum zugeordneten [Registrierungs Blatt](registration-base-url-resource.md#registration-leaf) .
version   | Zeichenfolge  | ja      | Die vollständige semver 2.0.0-Versions Zeichenfolge des Pakets (kann buildmetadaten enthalten)
Downloads | integer | ja      | Die Anzahl der Downloads für diese bestimmte Paketversion.

Das `packageTypes` Array besteht immer aus mindestens einem (1) Element. Der Pakettyp für eine bestimmte Paket-ID wird als die von der aktuellen Version des Pakets definierten Pakettypen in Bezug auf die anderen Suchparameter betrachtet. Jedes Element im `packageTypes` Array ist ein JSON-Objekt mit den folgenden Eigenschaften:

Name      | Typ    | Erforderlich | Notizen
--------- | ------- | -------- | -----
name      | Zeichenfolge  | ja      | Der Name des Pakettyps.

### <a name="sample-request"></a>Beispiel für eine Anforderung

```
GET https://azuresearch-usnc.nuget.org/query?q=NuGet.Versioning&prerelease=false&semVerLevel=2.0.0
```

### <a name="sample-response"></a>Beispiel für eine Antwort

[!code-JSON [search-result.json](./_data/search-result.json)]