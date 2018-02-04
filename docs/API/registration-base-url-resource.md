---
title: Metadaten-API-NuGet-Paket | Microsoft Docs
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
description: "Die Basis-URL des Pakets Registrierung ermöglicht das Abrufen von Metadaten zu Paketen."
keywords: NuGet-API-Metadaten von Paketen, die NuGet-API-Registrierung NuGet-API nicht aufgelistete Pakete
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c098d70d58011bad7f9829f0c95c87c1339dd362
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="package-metadata"></a>Metadaten von Paketen

Es ist möglich, um Metadaten über die verfügbaren Pakete auf eine Paketquelle mithilfe der NuGet-V3-API abzurufen. Diese Metadaten kann abgerufen werden, mithilfe der `RegistrationsBaseUrl` Ressource gefunden, der [Dienst Index](service-index.md).

Die Auflistung der Dokumente finden Sie unter `RegistrationsBaseUrl` werden häufig als "Registrierungen" oder "Registrierung Blobs" bezeichnet. Der Satz von Dokumenten innerhalb eines einzelnen `RegistrationsBaseUrl` wird als "Registrierung Hive" bezeichnet. Eine Registrierungsstruktur enthält alle Metadaten zu jedem Paket auf eine Paketquelle.

## <a name="versioning"></a>Versionskontrolle

Die folgenden `@type` Werte werden verwendet:

@type-Wert                     | Hinweise
------------------------------- | -----
RegistrationsBaseUrl            | Die erste Version
RegistrationsBaseUrl/3.0.0-beta | Alias der`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Alias der`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | GZIP-Antworten
RegistrationsBaseUrl/3.6.0      | Umfasst SemVer 2.0.0 Pakete

Dies stellt drei verschiedene Registrierungsstrukturen, die für die verschiedenen Clientversionen verfügbar.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Diese Registrierungen werden nicht komprimiert (d. h., sie verwenden ein implizites `Content-Encoding: identity`). SemVer 2.0.0 Pakete sind **ausgeschlossen** aus dieser ab.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Diese Registrierungen mit komprimiert sind `Content-Encoding: gzip`. SemVer 2.0.0 Pakete sind **ausgeschlossen** aus dieser ab.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Diese Registrierungen mit komprimiert sind `Content-Encoding: gzip`. SemVer 2.0.0 Pakete sind **enthalten** in dieser Struktur.
Weitere Informationen zu SemVer 2.0.0, finden Sie unter [SemVer 2.0.0-Unterstützung für nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>Basis-URL

Die base-URL für die folgenden APIs ist der Wert der `@id` Eigenschaft, die zuvor erwähnten zur Ressource zugeordnete `@type` Werte. Im folgenden Dokument Platzhalter für die Basis-URL `{@id}` verwendet werden.

## <a name="http-methods"></a>HTTP-Methoden

Alle URLs, die bei der Unterstützung der Registrierung-Ressource gefunden, die HTTP-Methoden `GET` und `HEAD`.

## <a name="registration-index"></a>Registrierung index

Die Registrierung Ressourcengruppen Paket Metadaten von Paket-ID Es ist nicht möglich, zum Abrufen von Daten über mehr als eine Paket-ID zu einem Zeitpunkt. Diese Ressource bietet keine Möglichkeit zum Ermitteln der Paket-IDs. Stattdessen wird der Client davon ausgegangen, dass die gewünschte Paket-ID bereits kennen Metadaten zu jeder Paketversion variiert je nach Server-Implementierung. Die Paket-Registrierung Blobs haben die folgenden hierarchische Struktur:

- **Index**: der Einstiegspunkt für die Metadaten von Paketen, gemeinsam von allen Paketen in der Quelle mit der gleichen Paket-ID.
- **Seite "**: eine Gruppierung von Paketversionen. Die Anzahl der Paketversionen auf einer Seite wird durch die Implementierung definiert.
- **Endknoten**: ein Dokument, die spezifisch für ein einzelnes Paket-Version.

Die URL des Indexes Registrierung ist vorhersagbar und kann bestimmt werden, vom Client erhält eine Paket-ID und der Registrierung Ressource `@id` Wert aus dem Dienst-Index. Die URLs für die Registrierungsseiten und Blätter werden durch Überprüfen des Indexes der Registrierung ermittelt.

### <a name="registration-pages-and-leaves"></a>Registrierungsseiten und bewirkt, dass

Obwohl es nicht unbedingt für eine Server-Implementierung zum Speichern von, dass die Registrierung in separaten Registrierung mehrseitige Dokumente leafs erforderlich ist, ist es eine empfohlene Methode, um die clientseitige Speicherplatz zu sparen. Anstelle von inlining alle Registrierung bewirkt, dass der Index oder sofort bewirkt, dass in mehrseitige Dokumente zu speichern, es wird empfohlen, dass die Server-Implementierung einem heuristischen Wert zwischen den beiden Ansätzen basierend auf der Anzahl von Paketversionen auswählen definieren oder die kumulierte Größe des Pakets verlässt.

Speichern alle Paketversionen Blätter () in der Registrierung Index speichert auf der Anzahl der HTTP-Anforderungen erforderlich, Fetch Paketmetadaten jedoch bedeutet, die dass ein größeres Dokument heruntergeladen werden muss und mehr Clientarbeitsspeicher zugeordnet werden muss. Andererseits, wenn die Server-Implementierung Registrierung bewirkt, dass sofort in separaten mehrseitige Dokumente gespeichert werden, muss der Client ausführen Weitere HTTP-Anforderungen zum Abrufen der Informationen, die es benötigt.

Die Heuristik, die nuget.org verwendet wird wie folgt: treten 128 oder mehrere Versionen eines Pakets, das bewirkt, dass in Seiten mit einer Größe von 64 geteilt. Wenn weniger als 128 Versionen verfügbar sind, bewirkt, dass alle Inline in den Index für die Registrierung.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Anforderungsparameter

name     | In     | Typ    | Erforderlich | Hinweise
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | Zeichenfolge  | ja      | Die Paket-ID, klein

Die `LOWER_ID` Wert ist die gewünschte Paket-ID, die klein gemäß den Vergleichsregeln von implementiert. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Methode.

### <a name="response"></a>Antwort

Die Antwort ist ein JSON-Dokument ein Stammobjekt mit den folgenden Eigenschaften besitzt:

name  | Typ             | Erforderlich | Hinweise
----- | ---------------- | -------- | -----
count | Ganze Zahl          | ja      | Die Anzahl der Registrierungsseiten, die im index
items | Array von Objekten | ja      | Das Array der Registrierungsseiten, die

Jedes Element in des Indexobjekt `items` Array ist ein JSON-Objekt, das eine Registrierungsseite darstellt.

#### <a name="registration-page-object"></a>Registrierung Page-Objekt

Die Registrierung Page-Objekt in der Registrierung Index gefunden hat die folgenden Eigenschaften:

name   | Typ             | Erforderlich | Hinweise
------ | ---------------- | -------- | -----
@id    | Zeichenfolge           | ja      | Die URL zu der Seite "Registrierung"
count  | Ganze Zahl          | ja      | Die Anzahl der Registrierung Blätter in der Seite "
items  | Array von Objekten | Nein       | Das Array von Registrierung bewirkt, dass und die zugeordneten Metadaten
Niedrigere  | Zeichenfolge           | ja      | Die niedrigste SemVer 2.0.0-Version auf der Seite (inklusiv)
parent | Zeichenfolge           | Nein       | Die URL, die dem Index für die Registrierung
obere  | Zeichenfolge           | ja      | Die höchste SemVer 2.0.0-Version auf der Seite (inklusiv)

Die `lower` und `upper` Grenzen der Page-Objekt sind nützlich, wenn die Metadaten für eine bestimmte Seitenversion erforderlich ist.
Diese Grenzen können verwendet werden, benötigt nur Registrierungsseite abgerufen. Die Versionszeichenfolgen entsprechen [NuGet Versionsregeln](../reference/package-versioning.md). Die Versionszeichenfolgen werden normalisiert und beinhalten keine Build Metadaten. Mit allen Versionen der NuGet-Ökosystem Vergleich von Versionszeichenfolgen implementierte mit [SemVer 2.0.0's Version Rangfolgeregeln](http://semver.org/spec/v2.0.0.html#spec-item-11).

Die `parent` Eigenschaft wird nur angezeigt, wenn die Registrierung Page-Objekt hat die `items` Eigenschaft.

Wenn die `items` Eigenschaft kann nicht in der Registrierung Page-Objekt vorhanden ist, in die URL angegeben die `@id` muss verwendet werden, um Metadaten über einzelne Paketversionen abzurufen. Die `items` Array manchmal ausgeschlossen zur Optimierung der Page-Objekt. Wenn die Anzahl der Versionen einer einzigen Paket-ID sehr groß ist, wird die Registrierung Indexdokument massive und den Prozess für einen Client, der eine bestimmte Version oder kleinen Bereich von Versionen nur bemüht gehen zu Lasten sein.

Beachten Sie, dass bei der `items` Eigenschaft vorhanden ist, ist die `@id` Eigenschaft muss nicht verwendet werden, da alle die Seitendaten sind bereits inline in der `items` Eigenschaft.

Jedes Element in der Page-Objekt `items` Array ist ein JSON-Objekt, das eine Registrierung Blatt darstellt, und dieser Metadaten zugewiesen ist.

#### <a name="registration-leaf-object-in-a-page"></a>Registrierung Endknotenobjekt auf einer Seite

Die Registrierung Endknotenobjekt in eine Registrierungsseite gefunden hat die folgenden Eigenschaften:

name           | Typ   | Erforderlich | Hinweise
-------------- | ------ | -------- | -----
@id            | Zeichenfolge | ja      | Die URL zu der Registrierung Blattknoten
catalogEntry   | object | ja      | Der Katalogeintrag, enthält die Metadaten von Paketen
packageContent | Zeichenfolge | ja      | Die URL für den Inhalt des Pakets (.nupkg)

Jeder Endknoten Registrierungsobjekt stellt ein einzelnes Paketversion zugeordnete Daten dar.

#### <a name="catalog-entry"></a>Katalogeintrag

Die `catalogEntry` Eigenschaft in der Registrierung Endknotenobjekt hat die folgenden Eigenschaften:

name                     | Typ                       | Erforderlich | Hinweise
------------------------ | -------------------------- | -------- | -----
@id                      | Zeichenfolge                     | ja      | Die URL zum Dokument verwendet, um dieses Objekt zu erzeugen.
authors                  | Zeichenfolge oder ein Array von Zeichenfolgen | Nein       | 
dependencyGroups         | Array von Objekten           | Nein       | Die URL für den Inhalt des Pakets (.nupkg)
Beschreibung              | Zeichenfolge                     | Nein       | 
iconUrl                  | Zeichenfolge                     | Nein       | 
ID                       | Zeichenfolge                     | ja      | Die ID des Pakets
licenseUrl               | Zeichenfolge                     | Nein       | 
Liste                   | boolean                    | Nein       | Sollte angesehen als aufgelisteten Falls nicht vorhanden
minClientVersion         | Zeichenfolge                     | Nein       | 
projectUrl               | Zeichenfolge                     | Nein       | 
Veröffentlicht                | Zeichenfolge                     | Nein       | Eine Zeichenfolge mit dem ISO 8601 Zeitstempel wann das Paket veröffentlicht wurde.
requireLicenseAcceptance | boolean                    | Nein       | 
Zusammenfassung                  | Zeichenfolge                     | Nein       | 
Tags                     | String oder Array von Zeichenfolgen  | Nein       | 
Titel                    | Zeichenfolge                     | Nein       | 
Version                  | Zeichenfolge                     | ja      | Die Version des Pakets

Die `dependencyGroups` Eigenschaft ist ein Array von Objekten, die die Abhängigkeiten des Pakets, gruppiert nach Zielframework darstellen. Wenn das Paket keine Abhängigkeiten enthält die `dependencyGroups` Eigenschaft nicht vorhanden, wird ein leeres Array oder die `dependencies` Eigenschaft aller Gruppen ist leer oder nicht vorhanden.

#### <a name="package-dependency-group"></a>Paket Abhängigkeitsgruppe

Jede Gruppe Abhängigkeitsobjekt hat die folgenden Eigenschaften:

name            | Typ             | Erforderlich | Hinweise
--------------- | ---------------- | -------- | -----
targetFramework | Zeichenfolge           | Nein       | Das Zielframework, dem diese Abhängigkeiten betreffen
Abhängigkeiten    | Array von Objekten | Nein       |

Die `targetFramework` Zeichenfolge verwendet das Format von NuGet .NET Bibliothek implementiert [NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/). Wenn kein `targetFramework` angegeben ist, wird der Abhängigkeitsgruppe betrifft alle Zielframeworks.

Die `dependencies` Eigenschaft ist ein Array von Objekten, die jeweils eine paketabhängigkeit des aktuellen Pakets darstellen.

#### <a name="package-dependency"></a>Paketabhängigkeit

Jede paketabhängigkeit hat die folgenden Eigenschaften:

name         | Typ   | Erforderlich | Hinweise
------------ | ------ | -------- | -----
ID           | Zeichenfolge | ja      | Die paketabhängigkeit-ID
range        | object | Nein       | Die zulässigen [Versionsbereich](../reference/package-versioning.md#version-ranges-and-wildcards) gegen das Abhängigkeitsverhältnis
Registrierung | Zeichenfolge | Nein       | Die URL, die dem Index der Registrierung für diese Abhängigkeit

Wenn die `range` -Eigenschaft ausgeschlossen oder eine leere Zeichenfolge des Clients sollte der Versionsbereich standardmäßig `(, )`. D. h. ist jede Version der Abhängigkeit zulässig.

### <a name="sample-request"></a>Beispielanforderung

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

In diesem speziellen Fall hat der Registrierung Index Inline Registrierungsseite aus, damit keine zusätzlichen Anforderungen zum Abrufen von Metadaten über einzelne Paketversionen erforderlich sind.

## <a name="registration-page"></a>Seite "Registrierung"

Die Registrierungsseite enthält Registrierung bleibt. Die URL eine Registrierungsseite abzurufenden richtet sich nach der `@id` Eigenschaft in der [Seite Registrierungsobjekt](#registration-page-object) oben genannten.

Wenn die `items` Array nicht in der Registrierung Index angegeben ist, eine HTTP GET-Anforderung von der `@id` Rückgabewert ein JSON-Dokument ein Objekt als Stamm besitzt. Das Objekt hat die folgenden Eigenschaften:

name   | Typ             | Erforderlich | Hinweise
------ | ---------------- | -------- | -----
@id    | Zeichenfolge           | ja      | Die URL zu der Seite "Registrierung"
count  | Ganze Zahl          | ja      | Die Anzahl der Registrierung Blätter in der Seite "
items  | Array von Objekten | ja      | Das Array von Registrierung bewirkt, dass und die zugeordneten Metadaten
Niedrigere  | Zeichenfolge           | ja      | Die niedrigste SemVer 2.0.0-Version auf der Seite (inklusiv)
parent | Zeichenfolge           | ja      | Die URL, die dem Index für die Registrierung
obere  | Zeichenfolge           | ja      | Die höchste SemVer 2.0.0-Version auf der Seite (inklusiv)

Die Form des Registrierungs-Endknotenobjekten ist dasselbe wie bei der Registrierung Index [oben](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Beispielanforderung

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Beispielantwort

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Registrierung Blattebene

Das Blatt für die Registrierung enthält Informationen zu einem bestimmten Paket-ID und die Version. Die Metadaten über die spezifische Version möglicherweise nicht verfügbar in diesem Dokument. Paketmetadaten abgerufen werden sollen, aus der [Registrierung Index](#registration-index) oder [Registrierungsseite](#registration-page) (die wird mithilfe des Indexes Registrierung gefunden).

Die URL zur Registrierung Endknoten fetch abgerufen wird, aus der `@id` Eigenschaft eines Objekts Registrierung Blattebene in einer Registrierung Index oder die Seite "Registrierung".

Das Blatt für die Registrierung ist ein JSON-Dokument mit einem Stammobjekt mit den folgenden Eigenschaften:

name           | Typ    | Erforderlich | Hinweise
-------------- | ------- | -------- | -----
@id            | Zeichenfolge  | ja      | Die URL zu der Registrierung Blattknoten
catalogEntry   | Zeichenfolge  | Nein       | Die URL für den Katalogeintrag, der diese Endknoten erzeugt
Liste         | boolean | Nein       | Sollte angesehen als aufgelisteten Falls nicht vorhanden
packageContent | Zeichenfolge  | Nein       | Die URL für den Inhalt des Pakets (.nupkg)
Veröffentlicht      | Zeichenfolge  | Nein       | Eine Zeichenfolge mit dem ISO 8601 Zeitstempel wann das Paket veröffentlicht wurde.
Registrierung   | Zeichenfolge  | Nein       | Die URL, die dem Index für die Registrierung

> [!Note]
> Auf nuget.org die `published` auf Jahr 1900, wenn das Paket nicht aufgeführte wird, Wert festgelegt ist.

### <a name="sample-request"></a>Beispielanforderung

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
