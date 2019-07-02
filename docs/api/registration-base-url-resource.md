---
title: Metadaten von Paketen, NuGet-API
description: Die Basis-URL des Pakets Registrierung ermöglicht das Abrufen von Metadaten zu Paketen.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0b35e2bbdde63f7f7a5298bd035c180389cd345d
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496500"
---
# <a name="package-metadata"></a>Paketmetadaten

Es ist möglich, zum Abrufen von Metadaten zu den verfügbaren Paketen auf eine Paketquelle, die mithilfe der NuGet-V3-API. Diese Metadaten kann abgerufen werden, mithilfe der `RegistrationsBaseUrl` Ressource finden Sie in der [dienstindex](service-index.md).

Die Auflistung der Dokumente finden Sie unter `RegistrationsBaseUrl` werden oft als "Registrierungen" oder "Registrierung Blobs" bezeichnet. Der Satz von Dokumenten innerhalb eines einzelnen `RegistrationsBaseUrl` "Registrierung Hive" genannt wird. Eine Registrierungsstruktur enthält alle Metadaten zu jedem Paket, die auf eine Paketquelle verfügbar.

## <a name="versioning"></a>Versionskontrolle

Die folgenden `@type` Werte werden verwendet:

@type -Wert                     | Hinweise
------------------------------- | -----
RegistrationsBaseUrl            | Die erste Version
RegistrationsBaseUrl/3.0.0-beta | Alias der `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Alias der `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | GZIP-Antworten
RegistrationsBaseUrl/3.6.0      | SemVer 2.0.0-Pakete enthält

Dies stellt drei unterschiedliche Registrierung-Strukturen, die für verschiedene Clientversionen verfügbar.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Diese Registrierungen werden nicht komprimiert (d. h., sie verwenden ein implizites `Content-Encoding: identity`). SemVer 2.0.0-Pakete sind **ausgeschlossen** aus dieser Struktur.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Diese Registrierungen werden komprimiert, indem `Content-Encoding: gzip`. SemVer 2.0.0-Pakete sind **ausgeschlossen** aus dieser Struktur.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Diese Registrierungen werden komprimiert, indem `Content-Encoding: gzip`. SemVer 2.0.0-Pakete sind **enthalten** in dieser Struktur.
Weitere Informationen zu SemVer 2.0.0, finden Sie unter [SemVer 2.0.0-Unterstützung für "NuGet.org"](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>Basis-URL

Die base-URL für die folgenden APIs ist der Wert des der `@id` -Eigenschaft zusammen mit den oben genannten Ressourcen `@type` Werte. Basis-URL im folgenden Dokument der Platzhalter `{@id}` verwendet werden.

## <a name="http-methods"></a>HTTP-Methoden

Alle URLs finden Sie in die Registrierung Unterstützung der HTTP-Methoden `GET` und `HEAD`.

## <a name="registration-index"></a>Index der Registrierung

Die Registrierung Ressourcengruppen Paket Metadaten über die Paket-ID. Es ist nicht möglich, Daten über mehr als eine Paket-ID zu einem Zeitpunkt erhalten. Diese Ressource bietet keine Möglichkeit zum Ermitteln der Paket-IDs. Stattdessen wird der Client davon ausgegangen, dass die gewünschten Paket-ID bereits kennen Verfügbarer Metadaten zu jeder Paketversion, variiert je nach Implementierung. Die Paket-Registrierung Blobs haben die folgende hierarchische Struktur:

- **Index**: der Einstiegspunkt für die Metadaten von Paketen, freigegeben, die von allen Paketen auf einer Datenquelle mit der gleichen Paket-ID.
- **Seite**: eine Gruppierung von Paketversionen. Die Anzahl der Versionen des Pakets auf einer Seite wird durch die Implementierung definiert.
- **Blattelemente**: ein Dokument, die spezifisch für ein einzelnes Paket-Version.

Die URL des Indexes Registrierung ist vorhersagbar und bestimmt werden kann, durch den Client, der eine Paket-ID und der registrierungsressource `@id` Wert aus dem dienstindex. Die URLs für die Registrierungsseiten und Blätter werden ermittelt, durch den Index für die Registrierung zu überprüfen.

### <a name="registration-pages-and-leaves"></a>Registrierungsseiten und Blätter

Obwohl es nicht unbedingt für eine Implementierung zum Speichern von, dass die Registrierung in separate Registrierung mehrseitige Dokumente leafs erforderlich ist, ist es eine empfohlene Vorgehensweise, um die clientseitige Speicherplatz zu sparen. Anstelle von inlineverwendung aller Registrierung bewirkt, dass der Index oder / / Blätter sofort in mehrseitige Dokumente zu speichern, es wird empfohlen, dass die Server-Implementierung einige Heuristik zur Wahl zwischen den beiden Ansätzen basierend auf der Anzahl von Paketversionen definieren oder bewirkt, dass die Gesamtgröße des Pakets.

Alle Versionen des Pakets speichern Blätter () in der Registrierung Index speichert auf der Anzahl der HTTP-Anforderungen erforderlichen Metadaten von Paketen abrufen, aber bedeutet, die dass ein größeren Dokuments heruntergeladen werden muss und mehr Clientarbeitsspeicher zugeordnet werden muss. Andererseits, wenn die serverimplementierung Registrierung lässt sofort in separaten mehrseitige Dokumente gespeichert werden, muss der Client ausführen Weitere HTTP-Anforderungen zum Abrufen der Informationen, die es benötigt.

Die Heuristik, die "NuGet.org" verwendet wird wie folgt: Wenn die 128 oder mehr Versionen eines Pakets verfügbar sind, teilen Sie die Blätter in Seiten mit einer Größe von 64. Wenn weniger als 128 Versionen verfügbar sind, bleibt Inline-alle in den Index für die Registrierung.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Anforderungsparameter

name     | In     | Typ    | Erforderlich | Hinweise
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | Zeichenfolge  | ja      | Die Paket-ID Kleinbuchstaben geändert

Die `LOWER_ID` Wert ist die gewünschte Paket-ID Kleinbuchstaben geändert, mithilfe von implementierten Regeln entspricht. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Methode.

### <a name="response"></a>Antwort

Die Antwort ist ein JSON-Dokument mit einem Stammobjekt mit den folgenden Eigenschaften:

Name  | Typ             | Erforderlich | Hinweise
----- | ---------------- | -------- | -----
count | Ganze Zahl          | ja      | Die Anzahl der von Registrierungsseiten im index
items | Array von Objekten | ja      | Das Array von Registrierungsseiten

Jedes Element in des Indexobjekt `items` Array ist ein JSON-Objekt, das eine Registrierungsseite darstellt.

#### <a name="registration-page-object"></a>Registrierung-Page-Objekt

Das Registrierungsobjekt-Seite finden Sie in der Registrierung Index hat die folgenden Eigenschaften:

Name   | Typ             | Erforderlich | Hinweise
------ | ---------------- | -------- | -----
@id    | Zeichenfolge           | ja      | Die URL der Registrierungsseite
count  | Ganze Zahl          | ja      | Die Anzahl der Registrierung bleiben auf der Seite
items  | Array von Objekten | Nein       | Das Array der Registrierung bleibt und ihre Metadaten zuordnen
niedrigere  | Zeichenfolge           | ja      | Die niedrigste SemVer 2.0.0-Version auf der Seite (inklusiv)
parent | Zeichenfolge           | Nein       | Die URL, die dem Index für die Registrierung
obere  | Zeichenfolge           | ja      | Die höchste SemVer 2.0.0-Version auf der Seite (inklusiv)

Die `lower` und `upper` Grenzen des das Page-Objekt sind nützlich, wenn die Metadaten für eine bestimmte Seitenversion erforderlich ist.
Diese Grenzen können verwendet werden, zum Abrufen der einzige Registrierungsseite erforderlich sind. Einhalten der Versionszeichenfolgen [NuGets-Versionsregeln](../reference/package-versioning.md). Die Versionszeichenfolgen werden normalisiert und beinhalten keine Build-Metadaten. Wie mit allen Versionen im NuGet-Ökosystem, Vergleich von Versionszeichenfolgen implementiert ist mit [SemVer 2.0.0's Version Rangfolgeregeln](http://semver.org/spec/v2.0.0.html#spec-item-11).

Die `parent` Eigenschaft wird nur angezeigt, wenn es sich bei den Registrierung-Page-Objekt hat die `items` Eigenschaft.

Wenn die `items` Eigenschaft ist nicht vorhanden ist, in der Registrierung-Page-Objekt, in die URL angegeben die `@id` muss zum Abrufen von Metadaten zu den einzelnen Paketversionen verwendet werden. Die `items` Array manchmal aus der Page-Objekt als Optimierung ausgeschlossen ist. Wenn die Anzahl der Versionen einer einzelnen Paket-ID sehr groß ist, werden die Registrierung Indizieren von Dokumenten umfangreiche und ineffizient, wie ein Client, der nur über eine bestimmte Version oder eine kleine Anzahl von Versionen zählt.

Beachten Sie, dass bei der `items` Eigenschaft vorhanden ist, die `@id` Eigenschaft muss nicht verwendet werden, da alle Daten auf der Seite ist bereits inline in der `items` Eigenschaft.

Jedes Element in des Seitenobjekts `items` Array ist ein JSON-Objekt, das ein Registrierung-Blatt darstellt und die dazugehörigen Metadaten.

#### <a name="registration-leaf-object-in-a-page"></a>Registrierung Endknotenobjekt auf einer Seite

Das Registrierungsobjekt-Blatt finden Sie in einer Registrierungsseite hat die folgenden Eigenschaften:

Name           | Typ   | Erforderlich | Hinweise
-------------- | ------ | -------- | -----
@id            | Zeichenfolge | ja      | Die URL in der Registrierung-Blatt
catalogEntry   | object | ja      | Der Katalogeintrag, enthält die Metadaten von Paketen
packageContent | Zeichenfolge | ja      | Die URL für den Paketinhalt (NUPKG-Datei)

Jede Registrierung Endknotenobjekt stellt ein einzelnes Paketversion zugeordnete Daten dar.

#### <a name="catalog-entry"></a>Katalogeintrag

Die `catalogEntry` -Eigenschaft in der Registrierung Endknotenobjekt hat die folgenden Eigenschaften:

Name                     | Typ                       | Erforderlich | Hinweise
------------------------ | -------------------------- | -------- | -----
@id                      | Zeichenfolge                     | ja      | Die URL zum Dokument verwendet, um dieses Objekt zu erstellen.
authors                  | Zeichenfolge oder Array von Zeichenfolgen | Nein       | 
dependencyGroups         | Array von Objekten           | Nein       | Die Abhängigkeiten des Pakets nach Zielframework gruppiert
als veraltet              | object                     | Nein       | Die Einstellung, die dem Paket zugeordneten
description              | Zeichenfolge                     | Nein       | 
iconUrl                  | Zeichenfolge                     | Nein       | 
id                       | Zeichenfolge                     | ja      | Die ID des Pakets
licenseUrl               | Zeichenfolge                     | Nein       |
licenseExpression        | Zeichenfolge                     | Nein       | 
Liste                   | boolean                    | Nein       | Sollten als aufgelisteten Falls nicht vorhanden betrachtet werden
minClientVersion         | Zeichenfolge                     | Nein       | 
projectUrl               | Zeichenfolge                     | Nein       | 
Veröffentlicht                | Zeichenfolge                     | Nein       | Eine Zeichenfolge mit einem ISO 8601-Zeitstempel, der bei das Paket veröffentlicht wurde
requireLicenseAcceptance | boolean                    | Nein       | 
summary                  | Zeichenfolge                     | Nein       | 
tags                     | Zeichenfolge oder Array von Zeichenfolgen  | Nein       | 
title                    | Zeichenfolge                     | Nein       | 
version                  | Zeichenfolge                     | ja      | Die vollständige Versionszeichenfolge nach der Normalisierung

Das Paket `version` Eigenschaft ist die vollständige Versionszeichenfolge nach der Normalisierung. Dies bedeutet, dass SemVer 2.0.0-Builddaten hier aufgenommen werden können.

Die `dependencyGroups` -Eigenschaft ist ein Array von Objekten, die die Abhängigkeiten des Pakets nach Zielframework gruppiert darstellt. Wenn das Paket keine Abhängigkeiten auf, verfügt die `dependencyGroups` Eigenschaft nicht vorhanden ist, ein leeres Array, oder die `dependencies` -Eigenschaft aller Gruppen ist, leer oder nicht vorhanden.

Der Wert des der `licenseExpression` Eigenschaft einhält [Syntax zum Ausdrücken von NuGet-Lizenz](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license).

#### <a name="package-dependency-group"></a>Gruppe der Paket-Abhängigkeit

Jede Gruppe Abhängigkeitsobjekt hat die folgenden Eigenschaften:

Name            | Typ             | Erforderlich | Hinweise
--------------- | ---------------- | -------- | -----
targetFramework | Zeichenfolge           | Nein       | Das Zielframework aus, dem diese Abhängigkeiten betreffen
dependencies    | Array von Objekten | Nein       |

Die `targetFramework` Zeichenfolge weist das Format von NuGet-Bibliothek für .NET implementiert [NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/). Wenn kein `targetFramework` angegeben ist, wird der Gruppe "Abhängigkeit" gilt für alle Zielframeworks.

Die `dependencies` -Eigenschaft ist ein Array von Objekten, die jeweils eine paketabhängigkeit des aktuellen Pakets darstellen.

#### <a name="package-dependency"></a>Paket-Abhängigkeit

Jede paketabhängigkeit weist die folgenden Eigenschaften:

Name         | Typ   | Erforderlich | Hinweise
------------ | ------ | -------- | -----
id           | Zeichenfolge | ja      | Die ID der Paket-Abhängigkeit
range        | object | Nein       | Die zulässigen [Versionsbereich](../reference/package-versioning.md#version-ranges-and-wildcards) der Abhängigkeit
Registrierung | Zeichenfolge | Nein       | Die URL für den Index der Registrierung für diese Abhängigkeit

Wenn die `range` -Eigenschaft ausgeschlossen oder eine leere Zeichenfolge und der Client sollte standardmäßig auf den Versionsbereich `(, )`. Das heißt, ist jede Version der Abhängigkeit zulässig.

#### <a name="package-deprecation"></a>Paket-Veraltung

Jedes Paket als veraltet hat die folgenden Eigenschaften:

Name             | Typ             | Erforderlich | Hinweise
---------------- | ---------------- | -------- | -----
Gründe          | Array von Zeichenfolgen | ja      | Die Gründe, warum das Paket als veraltet markiert wurde
message          | Zeichenfolge           | Nein       | Zusätzliche Details zu dieser Einstellung
alternatePackage | object           | Nein       | Die paketabhängigkeit, die stattdessen verwendet werden soll

Die `reasons` muss mindestens eine Zeichenfolge enthalten und sollte nur Zeichenfolgen aus der folgenden Tabelle enthält:

Grund       | Beschreibung             
------------ | -----------
Legacy       | Das Paket wird nicht mehr verwaltet.
CriticalBugs | Das Paket enthält Fehler, die ungeeignet für die Verwendung zu vereinfachen
Andere        | Das Paket kann eine aus folgendem Grund nicht in dieser Liste als veraltet markiert

Wenn die `reasons` Eigenschaft enthält Zeichenfolgen, die nicht von einem bekannten Satz sind, wird sie ignoriert werden sollen. Die Zeichenfolgen sind Groß-/Kleinschreibung, sodass `legacy` muss die gleiche Weise behandelt wie `Legacy`. Es gibt keine Sortierung Einschränkung für das Array, damit die Zeichenfolgen können in beliebiger Reihenfolge angeordnet. Darüber hinaus enthält die Eigenschaft nur Zeichenfolgen, die nicht von einem bekannten Satz sind, sollten sie behandelt werden, als ob es sich nur um die Zeichenfolge "Other" enthalten.

### <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

In diesem Fall hat der Index für die Registrierung die Inline-Registrierungsseite, also keine zusätzlichen Anforderungen zum Abrufen von Metadaten zu den einzelnen Paketversionen erforderlich sind.

## <a name="registration-page"></a>Registrierungsseite

Die Registrierungsseite enthält Registrierung bleibt. Die URL zum Abrufen einer Registrierungsseite richtet sich nach der `@id` -Eigenschaft in der [Registrierung Seitenobjekt](#registration-page-object) oben genannten.

Wenn die `items` Array nicht in der Registrierung Index angegeben ist, eine HTTP GET-Anforderung von der `@id` Wert gibt ein JSON-Dokument, das ein Objekt als Stamm hat. Das Objekt hat die folgenden Eigenschaften:

Name   | Typ             | Erforderlich | Hinweise
------ | ---------------- | -------- | -----
@id    | Zeichenfolge           | ja      | Die URL der Registrierungsseite
count  | Ganze Zahl          | ja      | Die Anzahl der Registrierung bleiben auf der Seite
items  | Array von Objekten | ja      | Das Array der Registrierung bleibt und ihre Metadaten zuordnen
niedrigere  | Zeichenfolge           | ja      | Die niedrigste SemVer 2.0.0-Version auf der Seite (inklusiv)
parent | Zeichenfolge           | ja      | Die URL, die dem Index für die Registrierung
obere  | Zeichenfolge           | ja      | Die höchste SemVer 2.0.0-Version auf der Seite (inklusiv)

Die Form des Endobjekte die Registrierung ist der gleiche wie in der Registrierung Index [oben](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Beispielantwort

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Registrierung Blattelemente

Das Blatt für die Registrierung enthält Informationen zu einem bestimmten Paket-ID und Version. Die Metadaten über die jeweilige Version möglicherweise nicht zur Verfügung, in diesem Dokument. Metadaten von Paketen abgerufen werden sollen, aus der [Registrierung Index](#registration-index) oder [Registrierungsseite](#registration-page) (die wird mithilfe des Indexes für die Registrierung gefunden).

Die URL zum Abrufen der ein Blatt für die Registrierung wird abgerufen, von der `@id` -Eigenschaft des Objekts ein Registrierung-Blattelemente in einem Index für Registrierung oder Registrierungsseite.

Das Blatt für die Registrierung ist ein JSON-Dokument mit einem Stammobjekt mit den folgenden Eigenschaften:

Name           | Typ    | Erforderlich | Hinweise
-------------- | ------- | -------- | -----
@id            | Zeichenfolge  | ja      | Die URL in der Registrierung-Blatt
catalogEntry   | Zeichenfolge  | Nein       | Die URL, den Katalogeintrag, der diese Blattelemente erstellt
Liste         | boolean | Nein       | Sollten als aufgelisteten Falls nicht vorhanden betrachtet werden
packageContent | Zeichenfolge  | Nein       | Die URL für den Paketinhalt (NUPKG-Datei)
Veröffentlicht      | Zeichenfolge  | Nein       | Eine Zeichenfolge mit einem ISO 8601-Zeitstempel, der bei das Paket veröffentlicht wurde
Registrierung   | Zeichenfolge  | Nein       | Die URL, die dem Index für die Registrierung

> [!Note]
> Auf nuget.org die `published` festgelegt ist, Jahr 1900, wenn das Paket nicht aufgelistet ist.

### <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
