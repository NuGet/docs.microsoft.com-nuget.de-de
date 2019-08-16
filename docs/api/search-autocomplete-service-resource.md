---
title: AutoComplete, nuget-API
description: Der Dienst "Auto Vervollständigen suchen" unterstützt die interaktive Ermittlung von Paket-IDs und-Versionen.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488305"
---
# <a name="autocomplete"></a>AutoVervollständigen

Mithilfe der V3-API können Sie eine Paket-ID und eine automatische vollständige Version erstellen. Die Ressource, die für die automatische Vervollständigung von `SearchAutocompleteService` Abfragen verwendet wird, ist die im [Dienst Index](service-index.md)gefundene Ressource.

## <a name="versioning"></a>Versionskontrolle

Die folgenden `@type` Werte werden verwendet:

@type -Wert                          | Hinweise
------------------------------------ | -----
SearchAutocompleteService            | Die erste Version
Searchautocompleteservice/3.0.0-Beta | Alias von`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Alias von`SearchAutocompleteService`

## <a name="base-url"></a>Basis-URL

Die Basis-URL für die folgenden APIs ist der Wert der `@id` Eigenschaft, die mit einem der oben erwähnten `@type` Ressourcen Werte verknüpft ist. Im folgenden Dokument wird die Platzhalter-Basis- `{@id}` URL verwendet.

## <a name="http-methods"></a>HTTP-Methoden

Alle URLs, die in der Registrierungs Ressource gefunden werden, `GET` unter `HEAD`stützen die HTTP-Methoden und.

## <a name="search-for-package-ids"></a>Nach Paket-IDs suchen

Die erste Auto Vervollständigen-API unterstützt die Suche nach einem Teil einer Paket-ID-Zeichenfolge. Dies eignet sich hervorragend, wenn Sie ein Paket typeahead-Feature in einer Benutzeroberfläche bereitstellen möchten, die in eine nuget-Paketquelle integriert ist.

Ein Paket, das nur nicht aufgelistete Versionen enthält, wird in den Ergebnissen nicht angezeigt.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Anforderungs Parameter

name        | In     | Typ    | Erforderlich | Hinweise
----------- | ------ | ------- | -------- | -----
q           | URL    | Zeichenfolge  | Nein       | Die Zeichenfolge, die mit Paket-IDs verglichen werden soll
überspringen        | URL    | Ganze Zahl | Nein       | Die Anzahl der zu über springenden Ergebnisse für die Paginierung.
Rechnung        | URL    | Ganze Zahl | Nein       | Die Anzahl der zurück zugebende Ergebnisse für die Paginierung.
vorab  | URL    | boolean | Nein       | `true`oder `false` feststellen, ob [vorab Pakete](../create-packages/prerelease-packages.md) eingeschlossen werden sollen
semVerLevel | URL    | Zeichenfolge  | Nein       | Eine Versions Zeichenfolge für semver 1.0.0 

Die Auto Vervollständigen- `q` Abfrage wird auf eine Weise analysiert, die durch die Server Implementierung definiert wird. nuget.org unterstützt das Abfragen für das Präfix von Paket-ID-Token, bei denen es sich um Teile der ID handelt, die durch das Aufteilen der ursprünglichen nach Kamel-und Symbol Zeichen erzeugt werden.

Der `skip` -Parameter hat den Standardwert 0.

Der `take` -Parameter muss eine ganze Zahl größer als 0 (null) sein. Die Server Implementierung kann einen maximalen Wert erzwingen.

Wenn `prerelease` nicht angegeben wird, werden vorab Versionen von Paketen ausgeschlossen.

Der `semVerLevel` -Abfrage Parameter wird verwendet, um [semver 2.0.0-Pakete](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)zu abonnieren.
Wenn dieser Abfrage Parameter ausgeschlossen wird, werden nur Paket-IDs mit mit semver 1.0.0 kompatiblen Versionen zurückgegeben (mit der [standardmäßigen nuget-Versions](../concepts/package-versioning.md) Kontrolle, z. b. Versions Zeichenfolgen mit vier ganzzahligen teilen).
Wenn `semVerLevel=2.0.0` angegeben wird, werden sowohl das semver 1.0.0-als auch das semver 2.0.0-kompatible Paket zurückgegeben. Weitere Informationen finden Sie [unter der semver 2.0.0-Unterstützung für nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Antwort

Die Antwort ist das JSON-Dokument, `take` das die Ergebnisse für die automatische Vervollständigung enthält.

Das JSON-Stamm Objekt verfügt über die folgenden Eigenschaften:

Name      | Typ             | Erforderlich | Hinweise
--------- | ---------------- | -------- | -----
totalhits | Ganze Zahl          | ja      | Die Gesamtanzahl der Übereinstimmungen, `skip` wobei und ignoriert werden.`take`
Daten      | Array von Zeichen folgen | ja      | Die Paket-IDs, die mit der Anforderung übereinstimmen.

### <a name="sample-request"></a>Beispiel Anforderung

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Beispiel Antwort

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Auflisten von Paketversionen

Sobald eine Paket-ID mit der vorherigen API ermittelt wurde, kann ein Client die Auto Vervollständigen-API verwenden, um Paketversionen für eine angegebene Paket-ID aufzulisten.

Eine nicht aufgelistete Paketversion wird in den Ergebnissen nicht angezeigt.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Anforderungs Parameter

name        | In     | Typ    | Erforderlich | Hinweise
----------- | ------ | ------- | -------- | -----
id          | URL    | Zeichenfolge  | ja      | Die Paket-ID, für die Versionen abgerufen werden sollen.
vorab  | URL    | boolean | Nein       | `true`oder `false` feststellen, ob [vorab Pakete](../create-packages/prerelease-packages.md) eingeschlossen werden sollen
semVerLevel | URL    | Zeichenfolge  | Nein       | Semver 2.0.0-Versions Zeichenfolge 

Wenn `prerelease` nicht angegeben wird, werden vorab Versionen von Paketen ausgeschlossen.

Der `semVerLevel` -Abfrage Parameter wird verwendet, um semver 2.0.0-Pakete zu abonnieren. Wenn dieser Abfrage Parameter ausgeschlossen wird, werden nur die semver 1.0.0-Versionen zurückgegeben. Wenn `semVerLevel=2.0.0` angegeben wird, werden die Versionen semver 1.0.0 und semver 2.0.0 zurückgegeben. Weitere Informationen finden Sie [unter der semver 2.0.0-Unterstützung für nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Antwort

Die Antwort ist das JSON-Dokument, das alle Paketversionen der angegebenen Paket-ID enthält, die nach den angegebenen Abfrage Parametern gefiltert werden.

Das JSON-Stamm Objekt hat die folgende Eigenschaft:

Name      | Typ             | Erforderlich | Hinweise
--------- | ---------------- | -------- | -----
Daten      | Array von Zeichen folgen | ja      | Die Paketversionen, die mit der Anforderung übereinstimmen.

Die Paketversionen im `data` Array enthalten möglicherweise semver 2.0.0-buildmetadaten (z. b. `1.0.0+metadata`), wenn der `semVerLevel=2.0.0` in der Abfrage Zeichenfolge bereitgestellt wird.

### <a name="sample-request"></a>Beispiel Anforderung

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Beispiel Antwort

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
