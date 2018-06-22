---
title: AutoVervollständigen NuGet-API
description: Die AutoVervollständigen-Suchdienst unterstützt interaktive Ermittlung von Paket-IDs und Versionen.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d5e1936c6c5406a1a376c16b2bad5351320dfb4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822135"
---
# <a name="autocomplete"></a>AutoVervollständigen

Es ist möglich, eine Paket-ID und Version AutoVervollständigen Erfahrung mit der V3-API zu erstellen. Die Ressource, die zum treffen von AutoVervollständigen Abfragen verwendet wird die `SearchAutocompleteService` Ressource gefunden, der [Dienst Index](service-index.md).

## <a name="versioning"></a>Versionskontrolle

Die folgenden `@type` Werte werden verwendet:

@type-Wert                          | Hinweise
------------------------------------ | -----
SearchAutocompleteService            | Die erste Version
SearchAutocompleteService/3.0.0-beta | Alias der `SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Alias der `SearchAutocompleteService`

## <a name="base-url"></a>Basis-URL

Die base-URL für die folgenden APIs ist der Wert der `@id` mit einem der oben genannten Ressource verknüpfte Eigenschaft `@type` Werte. Im folgenden Dokument Platzhalter für die Basis-URL `{@id}` verwendet werden.

## <a name="http-methods"></a>HTTP-Methoden

Alle URLs, die bei der Unterstützung der Registrierung-Ressource gefunden, die HTTP-Methoden `GET` und `HEAD`.

## <a name="search-for-package-ids"></a>Suchen Sie nach der Paket-IDs

Das erste AutoVervollständigen-API unterstützt die Teil einer Paket-ID-Zeichenfolge gesucht. Dies ist nützlich, wenn Sie eine Paket Typeahead-Funktion in einer Benutzeroberfläche mit einem NuGet-Paket integriert bereitstellen möchten.

Ein Paket mit nur nicht aufgeführte Versionen werden nicht in den Ergebnissen angezeigt.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Anforderungsparameter

name        | In     | Typ    | Erforderlich | Hinweise
----------- | ------ | ------- | -------- | -----
q           | URL    | Zeichenfolge  | Nein       | Die Zeichenfolge zum Vergleich von Paket-IDs
überspringen        | URL    | Ganze Zahl | Nein       | Die Anzahl der Ergebnisse für die Paginierung überspringen
Take        | URL    | Ganze Zahl | Nein       | Die Anzahl der zurückzugebenden Ergebnisseite, für die Paginierung
Vorabversion  | URL    | boolean | Nein       | `true` oder `false` bestimmen, ob enthalten [Vorabversion Pakete](../create-packages/prerelease-packages.md)
semVerLevel | URL    | Zeichenfolge  | Nein       | Eine Versionszeichenfolge SemVer 1.0.0 

Die AutoVervollständigen-Abfrage `q` wird analysiert, die in einer Weise, die durch die Implementierung definiert ist. NuGet.org unterstützt das Abfragen für das Präfix des Paket-ID-Token, die Teile der von Spliting erzeugte ID werden der ursprünglichen Kamel Groß-/Kleinschreibung und das Symbol für Zeichen.

Die `skip` Parameter beträgt standardmäßig 0.

Die `take` Parameter muss eine ganze Zahl größer als 0 (null) sein. Die Implementierung der Server kann einen maximalen Wert verursachen.

Wenn `prerelease` nicht angegeben wird, Vorabversion Paketen ausgeschlossen werden.

Die `semVerLevel` Query-Parameter wird verwendet, um abonnieren [SemVer 2.0.0 Pakete](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Wenn dieser Parameter ausgeschlossen ist, werden nur Paket-IDs mit SemVer 1.0.0 kompatible Versionen zurückgegeben (mit der [standard NuGet Versioning](../reference/package-versioning.md) Vorsichtsmaßnahmen, z. B. Versionszeichenfolgen mit 4 Einheiten für ganze Zahl).
Wenn `semVerLevel=2.0.0` angegeben wird, SemVer 1.0.0 und SemVer 2.0.0 kompatibel Pakete zurückgegeben werden. Finden Sie unter der [SemVer 2.0.0-Unterstützung für nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) für Weitere Informationen.

### <a name="response"></a>Antwort

Die Antwort ist, enthält bis zu JSON-Dokument `take` AutoVervollständigen Ergebnisse.

Der Stamm-JSON-Objekt hat die folgenden Eigenschaften:

name      | Typ             | Erforderlich | Hinweise
--------- | ---------------- | -------- | -----
totalHits | Ganze Zahl          | ja      | Die Gesamtzahl der Übereinstimmungen, Basiseigenschaft `skip` und `take`
Daten      | Array von Zeichenfolgen | ja      | Die Paket-IDs übereinstimmen, die von der Anforderung

### <a name="sample-request"></a>Beispielanforderung

ERHALTEN https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Auflisten von Paketversionen

Eine Paket-ID mithilfe der vorherigen-API ermittelt wurde, können ein Client die AutoVervollständigen-API Sie Paketversionen für eine angegebene Paket-ID aufgelistet werden.

Eine Paketversion, die nicht aufgeführte ist, werden nicht in den Ergebnissen angezeigt.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Anforderungsparameter

name        | In     | Typ    | Erforderlich | Hinweise
----------- | ------ | ------- | -------- | -----
ID          | URL    | Zeichenfolge  | ja      | Die Paket-ID für Versionen abgerufen
Vorabversion  | URL    | boolean | Nein       | `true` oder `false` bestimmen, ob enthalten [Vorabversion Pakete](../create-packages/prerelease-packages.md)
semVerLevel | URL    | Zeichenfolge  | Nein       | Eine Versionszeichenfolge SemVer 2.0.0 

Wenn `prerelease` nicht angegeben wird, Vorabversion Paketen ausgeschlossen werden.

Die `semVerLevel` Query-Parameter wird verwendet, um Pakete von SemVer 2.0.0 teilnehmen. Wenn dieser Parameter ausgeschlossen ist, werden nur SemVer 1.0.0 Versionen zurückgegeben. Wenn `semVerLevel=2.0.0` angegeben wird, SemVer 1.0.0 und SemVer 2.0.0-Versionen zurückgegeben werden. Finden Sie unter der [SemVer 2.0.0-Unterstützung für nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) für Weitere Informationen.

### <a name="response"></a>Antwort

Die Antwort ist JSON-Dokument, das alle Paketversionen der bereitgestellte Paket-ID, die das Filtern nach der angegebenen Abfrageparameter enthält.

Der Stamm-JSON-Objekt hat die folgende Eigenschaft:

name      | Typ             | Erforderlich | Hinweise
--------- | ---------------- | -------- | -----
Daten      | Array von Zeichenfolgen | ja      | Die Zeichenfolge, die für der Anforderungs Paketversionen

Die Paketversionen in der `data` Array konnte SemVer 2.0.0 Build Metadaten enthalten (z. B. `1.0.0+metadata`) Wenn die `semVerLevel=2.0.0` wurde in der Abfragezeichenfolge angegeben.

### <a name="sample-request"></a>Beispielanforderung

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
