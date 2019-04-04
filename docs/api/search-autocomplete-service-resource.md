---
title: AutoVervollständigen-Funktion, NuGet-API
description: Der Search-Dienst für automatische Vervollständigung unterstützt interaktive Suche in der Paket-IDs und Versionen.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fdc3ad8aa239a42d8a4c169a757715e856bdcb41
ms.sourcegitcommit: 9f94e00428d83aef4a7a87db679129eff7720c59
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/03/2019
ms.locfileid: "58911048"
---
# <a name="autocomplete"></a>AutoVervollständigen

Es ist möglich, eine Paket-ID und Version AutoVervollständigen Erfahrung mit der V3-API zu erstellen. Die Ressource, die zum Durchführen von AutoVervollständigen-Abfragen ist die `SearchAutocompleteService` Ressource finden Sie in der [dienstindex](service-index.md).

## <a name="versioning"></a>Versionskontrolle

Die folgenden `@type` Werte werden verwendet:

@type-Wert                          | Hinweise
------------------------------------ | -----
SearchAutocompleteService            | Die erste Version
SearchAutocompleteService/3.0.0-beta | Alias der `SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Alias der `SearchAutocompleteService`

## <a name="base-url"></a>Basis-URL

Die base-URL für die folgenden APIs ist der Wert des der `@id` Eigenschaft, die einer der oben genannten Ressource zugeordneten `@type` Werte. Basis-URL im folgenden Dokument der Platzhalter `{@id}` verwendet werden.

## <a name="http-methods"></a>HTTP-Methoden

Alle URLs finden Sie in die Registrierung Unterstützung der HTTP-Methoden `GET` und `HEAD`.

## <a name="search-for-package-ids"></a>Suchen Sie nach der Paket-IDs

Die erste API für AutoVervollständigen unterstützt das Suchen nach Teil einer Paket-ID-Zeichenfolge. Dies ist nützlich, wenn Sie ein Paket Typeahead-Feature in einer Benutzeroberfläche, die in einem NuGet-Paketquelle integriert bereitstellen möchten.

Ein Paket mit nur nicht aufgeführte Versionen wird nicht in den Ergebnissen angezeigt.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Anforderungsparameter

name        | In     | Typ    | Erforderlich | Hinweise
----------- | ------ | ------- | -------- | -----
q           | URL    | Zeichenfolge  | Nein       | Die Zeichenfolge, die mit der Paket-IDs verglichen werden soll
überspringen        | URL    | Ganze Zahl | Nein       | Die Anzahl von Ergebnissen für die Paginierung überspringen
Take        | URL    | Ganze Zahl | Nein       | Die Anzahl der zurückzugebenden Ergebnisse, für die Paginierung
Vorabversion  | URL    | boolean | Nein       | `true` oder `false` bestimmen, ob enthalten [Vorabversionen von Paketen](../create-packages/prerelease-packages.md)
semVerLevel | URL    | Zeichenfolge  | Nein       | Eine Versionszeichenfolge SemVer 1.0.0 

Die AutoVervollständigen-Abfrage `q` wird analysiert, in einer Weise, die von der serverimplementierung definiert ist. NuGet.org unterstützt das Abfragen für das Präfix der Paket-ID-Token, die Teile der Teilung von erzeugten-ID des ursprünglichen Camel Case "und" Symbol Zeichen.

Die `skip` Parameter hat den Standardwert 0.

Die `take` Parameter muss eine ganze Zahl größer als 0 (null) sein. Die Server-Implementierung kann es sich um einen maximalen Wert verursachen.

Wenn `prerelease` ist nicht angegeben wird, Vorabversionen von Paketen ausgeschlossen werden.

Die `semVerLevel` Query-Parameter wird verwendet, um abonnieren [SemVer 2.0.0 Pakete](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Wenn dieser Parameter ausgeschlossen wird, wird nur Paket-IDs mit SemVer 1.0.0 kompatible Versionen zurückgegeben werden (mit der [standard NuGet-Versionsschema](../reference/package-versioning.md) Einschränkungen, z. B. Versionszeichenfolgen mit 4 Einheiten für ganze Zahl).
Wenn `semVerLevel=2.0.0` bereitgestellt wird, werden sowohl SemVer 1.0.0 und kompatiblen Paketen SemVer 2.0.0 zurückgegeben werden. Finden Sie unter den [SemVer 2.0.0-Unterstützung für "NuGet.org"](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) für Weitere Informationen.

### <a name="response"></a>Antwort

Die Antwort ist die JSON-Dokument mit bis zu `take` Autocomplete-Ergebnisse.

Die JSON-Stammobjekt hat die folgenden Eigenschaften:

Name      | Typ             | Erforderlich | Hinweise
--------- | ---------------- | -------- | -----
totalHits | Ganze Zahl          | ja      | Die Gesamtzahl der Übereinstimmungen ohne Berücksichtigung der `skip` und `take`
Daten      | Array von Zeichenfolgen | ja      | Die Paket-IDs, die von der Anforderung übereinstimmen

### <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Auflisten von Paketversionen

Eine Paket-ID mit der vorherigen-API ermittelt wurde, können ein Client die AutoVervollständigen-API Sie Auflisten von Paketversionen für ein bereitgestelltes Paket-ID

Eine Version des Pakets, die nicht aufgeführt ist, wird nicht in den Ergebnissen angezeigt.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Anforderungsparameter

name        | In     | Typ    | Erforderlich | Hinweise
----------- | ------ | ------- | -------- | -----
id          | URL    | Zeichenfolge  | ja      | Die Paket-ID zum Abrufen von Versionen
Vorabversion  | URL    | boolean | Nein       | `true` oder `false` bestimmen, ob enthalten [Vorabversionen von Paketen](../create-packages/prerelease-packages.md)
semVerLevel | URL    | Zeichenfolge  | Nein       | Eine Zeichenfolge der SemVer 2.0.0-version 

Wenn `prerelease` ist nicht angegeben wird, Vorabversionen von Paketen ausgeschlossen werden.

Die `semVerLevel` Query-Parameter wird verwendet, um SemVer 2.0.0-Paketen teilnehmen. Wenn dieser Parameter ausgeschlossen wird, werden nur SemVer 1.0.0-Versionen zurückgegeben. Wenn `semVerLevel=2.0.0` bereitgestellt wird, werden sowohl die SemVer 1.0.0 als auch die SemVer 2.0.0-Version zurückgegeben werden. Finden Sie unter den [SemVer 2.0.0-Unterstützung für "NuGet.org"](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) für Weitere Informationen.

### <a name="response"></a>Antwort

Die Antwort ist die JSON-Dokument mit der alle Paketversionen von den angegebenen Paket-ID filtern nach den angegebenen Abfrageparametern.

Die JSON-Stammobjekt hat die folgende Eigenschaft:

Name      | Typ             | Erforderlich | Hinweise
--------- | ---------------- | -------- | -----
Daten      | Array von Zeichenfolgen | ja      | Die Paketversionen, die von der Anforderung übereinstimmen

Die Versionen des Pakets in der `data` Array SemVer 2.0.0-Build-Metadaten enthalten (z. B. `1.0.0+metadata`) Wenn die `semVerLevel=2.0.0` wird in der Abfragezeichenfolge bereitgestellt.

### <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
