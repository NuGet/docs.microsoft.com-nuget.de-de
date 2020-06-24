---
title: Katalog Ressource, nuget V3-API
description: Der Katalog ist ein Index für alle Pakete, die auf nuget.org erstellt und gelöscht werden.
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: ffbcb8dc18542f39c32a6d84b279c8eccaf98fc3
ms.sourcegitcommit: 7e9c0630335ef9ec1e200e2ee9065f702e52a8ec
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/24/2020
ms.locfileid: "85292311"
---
# <a name="catalog"></a>Katalog

Der- **Katalog** ist eine Ressource, die alle Paket Vorgänge in einer Paketquelle aufzeichnet, wie z. b. Erstellungen und Löschungen. Die Katalog Ressource weist den `Catalog` Typ im [Dienst Index](service-index.md)auf. Sie können diese Ressource verwenden, um [alle veröffentlichten Pakete abzufragen](../guides/api/query-for-all-published-packages.md).

> [!Note]
> Da der Katalog nicht vom offiziellen nuget-Client verwendet wird, implementieren nicht alle Paketquellen den Katalog.

> [!Note]
> Der nuget.org-Katalog ist in China zurzeit nicht verfügbar. Weitere Informationen finden Sie unter [nuget/nugetgallery # 4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Versionskontrolle

Der folgende `@type` Wert wird verwendet:

@type-Wert   | Notizen
------------- | -----
Catalog/3.0.0 | Die erste Version

## <a name="base-url"></a>Basis-URL

Die Einstiegspunkt-URL für die folgenden APIs ist der Wert der `@id` Eigenschaft, die den oben erwähnten Ressourcen Werten zugeordnet ist `@type` . In diesem Thema wird die Platzhalter-URL verwendet `{@id}` .

## <a name="http-methods"></a>HTTP-Methoden

Alle URLs, die in der Katalog Ressource gefunden werden, unterstützen nur die HTTP `GET` -Methoden und `HEAD` .

## <a name="catalog-index"></a>Katalog Index

Der Katalog Index ist ein Dokument an einem bekannten Speicherort, das eine Liste von Katalog Elementen enthält. Dies ist der Einstiegspunkt der-Katalog Ressource.

Der Index besteht aus Katalogseiten. Jede Katalogseite enthält Katalog Elemente. Jedes Katalog Element stellt ein Ereignis für ein einzelnes Paket zu einem bestimmten Zeitpunkt dar. Ein Katalog Element kann ein Paket darstellen, das erstellt, nicht aufgelistet, erneut erstellt oder aus der Paketquelle gelöscht wurde. Wenn die Katalog Elemente in chronologischer Reihenfolge verarbeitet werden, kann der Client eine aktuelle Ansicht jedes Pakets erstellen, das in der V3-Paketquelle vorhanden ist.

Kurz gesagt, haben Katalog-blobdie folgende hierarchische Struktur:

- **Index**: der Einstiegspunkt für den Katalog.
- **Page**: eine Gruppierung von Katalog Elementen.
- **Blatt**: ein Dokument, das ein Katalog Element darstellt, bei dem es sich um eine Momentaufnahme des Zustands eines einzelnen Pakets handelt.

Jedes Katalog Objekt verfügt über eine Eigenschaft mit dem Namen `commitTimeStamp` , die beim Hinzufügen des Elements zum Katalog darstellt. Katalog Elemente werden einer Katalogseite in Batches hinzugefügt, die als Commits bezeichnet werden. Alle Katalog Elemente im gleichen Commit weisen denselben Commit-Zeitstempel ( `commitTimeStamp` ) und die Commit-ID ( `commitId` ) auf. Katalog Elemente, die im gleichen Commit abgelegt werden, stellen Ereignisse dar, die um denselben Zeitpunkt in der Paketquelle aufgetreten sind. Es gibt keine Reihenfolge innerhalb eines Katalog Commit.

Da alle Paket-IDs und-Versionen eindeutig sind, gibt es nie mehr als ein Katalog Element in einem Commit. Dadurch wird sichergestellt, dass Katalog Elemente für ein einzelnes Paket in Bezug auf den Commit-Zeitstempel immer eindeutig angeordnet werden können.

Es ist nie mehr als ein Commit für den Katalog pro vorhanden `commitTimeStamp` . Das heißt, die `commitId` ist mit dem redundant `commitTimeStamp` .

Im Gegensatz zur [Paket Metadaten-Ressource](registration-base-url-resource.md), die mit der Paket-ID indiziert ist, wird der Katalog nur nach Zeit indiziert (und abgefragt).

Katalog Elemente werden dem Katalog immer in einer monoton zunehmenden, chronologischen Reihenfolge hinzugefügt. Dies bedeutet Folgendes: Wenn ein Katalog Commit zum Zeitpunkt x hinzugefügt wird, wird nie ein Katalog Commit mit einer Zeit kleiner oder gleich x hinzugefügt.

Die folgende Anforderung Ruft den Katalog Index ab.

    GET {@id}

Der Katalog Index ist ein JSON-Dokument, das ein-Objekt mit den folgenden Eigenschaften enthält:

Name            | type             | Erforderlich | Notizen
--------------- | ---------------- | -------- | -----
commitId        | Zeichenfolge           | Ja      | Eine eindeutige ID, die mit dem letzten Commit verknüpft ist.
committimestamp | Zeichenfolge           | Ja      | Ein Zeitstempel des letzten Commit
count           | integer          | Ja      | Die Anzahl der Seiten im Index.
items           | Array von Objekten | Ja      | Ein Array von-Objekten, jedes Objekt, das eine Seite darstellt.

Jedes Element im `items` Array ist ein Objekt mit einigen minimalen Details zu jeder Seite. Diese Seiten Objekte enthalten keine Katalog Blätter (Elemente). Die Reihenfolge der Elemente in diesem Array ist nicht definiert. Seiten können vom Client im Arbeitsspeicher mithilfe ihrer-Eigenschaft geordnet werden `commitTimeStamp` .

Wenn neue Seiten eingeführt werden, wird der `count` inkrementiert, und neue Objekte werden im `items` Array angezeigt.

Wenn dem Katalog Elemente hinzugefügt werden, ändert sich der Index, `commitId` und `commitTimeStamp` erhöht sich. Diese beiden Eigenschaften sind im Wesentlichen eine Zusammenfassung über alle Seiten `commitId` und `commitTimeStamp` Werte im `items` Array.

### <a name="catalog-page-object-in-the-index"></a>Katalogseiten Objekt im Index

Die Katalogseiten Objekte, die in der-Eigenschaft des Katalog Indexes gefunden werden, `items` haben die folgenden Eigenschaften:

Name            | type    | Erforderlich | Notizen
--------------- | ------- | -------- | -----
@id             | Zeichenfolge  | Ja      | Die URL zum Abrufen der Katalogseite
commitId        | Zeichenfolge  | Ja      | Eine eindeutige ID, die dem letzten Commit auf dieser Seite zugeordnet ist.
committimestamp | Zeichenfolge  | Ja      | Ein Zeitstempel des letzten Commit auf dieser Seite
count           | integer | Ja      | Die Anzahl der Elemente auf der Seite "Katalog".

Im Gegensatz zur [paketmetadatenressource](registration-base-url-resource.md) , die in einigen Fällen in den Index verschoben wird, werden Katalog Blätter nie in den Index eingebettet und müssen immer mithilfe der URL der Seite abgerufen werden `@id` .

### <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>Beispiel für eine Antwort

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Katalogseite

Die Seite Katalog ist eine Sammlung von Katalog Elementen. Es handelt sich um ein Dokument, das mit einem der `@id` im Katalog Index gefundenen Werte abgerufen wird. Die URL zu einer Katalogseite ist nicht als vorhersagbar gedacht und sollte nur mit dem Katalog Index erkannt werden.

Neue Katalog Elemente werden der Seite im Katalog Index nur mit dem höchsten Commit-Zeitstempel oder einer neuen Seite hinzugefügt. Nachdem eine Seite mit einem Zeitstempel mit höherem Commit zum Katalog hinzugefügt wurde, werden ältere Seiten niemals hinzugefügt oder geändert.

Das Katalogseiten Dokument ist ein JSON-Objekt mit den folgenden Eigenschaften:

Name            | type             | Erforderlich | Notizen
--------------- | ---------------- | -------- | -----
commitId        | Zeichenfolge           | Ja      | Eine eindeutige ID, die dem letzten Commit auf dieser Seite zugeordnet ist.
committimestamp | Zeichenfolge           | Ja      | Ein Zeitstempel des letzten Commit auf dieser Seite
count           | integer          | Ja      | Die Anzahl der Elemente auf der Seite.
items           | Array von Objekten | Ja      | Die Katalog Elemente auf dieser Seite
parent          | Zeichenfolge           | Ja      | Eine URL zum Katalog Index.

Jedes Element im `items` Array ist ein Objekt mit minimalen Details zum Katalog Element. Diese Element Objekte enthalten nicht alle Daten des Katalog Elements. Die Reihenfolge der Elemente im Seiten `items` Array ist nicht definiert. Elemente können vom Client im Arbeitsspeicher mithilfe ihrer-Eigenschaft geordnet werden `commitTimeStamp` .

Die Anzahl der Katalog Elemente in einer Seite wird durch die Server Implementierung definiert. Für nuget.org gibt es höchstens 550 Elemente auf jeder Seite, obwohl die tatsächliche Anzahl je nach Größe des nächsten Commit-Batches zu dem Zeitpunkt kleiner sein kann.

Wenn neue Elemente eingeführt werden, `count` wird der inkrementiert und neue Katalog Element Objekte im `items` Array angezeigt.

Beim Hinzufügen von Elementen zur Seite werden die `commitId` Änderungen und die `commitTimeStamp` vergrößert. Diese beiden Eigenschaften sind im Wesentlichen eine Zusammenfassung über alle `commitId` -und- `commitTimeStamp` Werte im- `items` Array.

### <a name="catalog-item-object-in-a-page"></a>Katalog Element Objekt in einer Seite

Die Katalog Element Objekte in der-Eigenschaft der-Katalogseite `items` haben die folgenden Eigenschaften:

Name            | type    | Erforderlich | Notizen
--------------- | ------- | -------- | -----
@id             | Zeichenfolge  | Ja      | Die URL zum Abrufen des Katalog Elements.
@type           | Zeichenfolge  | Ja      | Der Typ des Katalog Elements.
commitId        | Zeichenfolge  | Ja      | Die diesem Katalog Element zugeordnete Commit-ID.
committimestamp | Zeichenfolge  | Ja      | Der Commit-Zeitstempel dieses Katalog Elements.
nuget: ID        | Zeichenfolge  | Ja      | Die Paket-ID, mit der dieses Blatt verknüpft ist.
nuget: Version   | Zeichenfolge  | Ja      | Die Paketversion, mit der dieses Blatt verknüpft ist.

Der `@type` Wert ist einer der folgenden beiden Werte:

1. `nuget:PackageDetails`: Dies entspricht `PackageDetails` dem Typ im Blatt Dokument des Katalogs.
1. `nuget:PackageDelete`: Dies entspricht dem- `PackageDelete` Typ im Katalog Blatt Dokument.

Weitere Informationen zur Bedeutung der einzelnen Typen finden Sie unten unter dem [entsprechenden Elementtyp](#item-types) .

### <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>Beispiel für eine Antwort

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Katalog Blatt

Das Blatt "Katalog" enthält Metadaten über eine bestimmte Paket-ID und-Version zu einem bestimmten Zeitpunkt. Es handelt sich um ein Dokument, das mit dem `@id` in einer Katalogseite gefundenen Wert abgerufen wird. Die URL zu einem Katalog Blatt ist nicht als vorhersagbar gedacht und sollte nur mit einer Katalogseite erkannt werden.

Das Katalog Blatt Dokument ist ein JSON-Objekt mit den folgenden Eigenschaften:

Name                    | type                       | Erforderlich | Notizen
----------------------- | -------------------------- | -------- | -----
@type                   | Zeichenfolge oder Array von Zeichenfolgen | Ja      | Der Typ (n) des Katalog Elements.
Katalog: comentschärd        | Zeichenfolge                     | Ja      | Eine Commit-ID, die diesem Katalog Element zugeordnet ist.
Katalog: committimestamp | Zeichenfolge                     | Ja      | Der Commit-Zeitstempel dieses Katalog Elements.
id                      | Zeichenfolge                     | Ja      | Die Paket-ID des Katalog Elements.
published               | Zeichenfolge                     | Ja      | Das veröffentlichte Datum des Paket Katalog Elements.
version                 | Zeichenfolge                     | Ja      | Die Paketversion des Katalog Elements.

### <a name="item-types"></a>Elementtypen

Die- `@type` Eigenschaft ist eine Zeichenfolge oder ein Array von Zeichen folgen. Der Vorteil, wenn der `@type` Wert eine Zeichenfolge ist, sollte er als beliebiges Array der Größe 1 behandelt werden. Nicht alle möglichen Werte für `@type` sind dokumentiert. Jedes Katalog Element weist jedoch genau einen der beiden folgenden Zeichen Folgentyp Werte auf:

1. `PackageDetails`: stellt eine Momentaufnahme der Paket Metadaten dar.
1. `PackageDelete`: stellt ein gelöschtes Paket dar.

### <a name="package-details-catalog-items"></a>Paket Details-Katalog Elemente

Katalog Elemente mit dem-Typ `PackageDetails` enthalten eine Momentaufnahme der Paket Metadaten für ein bestimmtes Paket (ID-und Versions Kombination). Ein Paket Details-Katalog Element wird erstellt, wenn eine Paketquelle eines der folgenden Szenarien erkennt:

1. Ein Paket wird per **pushübertragung**gesendet.
1. Ein Paket wird **aufgelistet**.
1. Das **auflisten**eines Pakets wird aufgehoben.
1. Ein Paket wird **erneut**übertragen.

Bei einem paketflow handelt es sich um eine administrative Geste, bei der im Grunde ein gefälschter Push eines vorhandenen Pakets ohne Änderungen an dem Paket selbst generiert wird. Auf nuget.org wird ein Umbruch verwendet, nachdem ein Fehler in einem der Hintergrund Aufträge behoben wurde, die den Katalog nutzen.

Clients, die die Katalog Elemente nutzen, sollten nicht versuchen, zu bestimmen, welche dieser Szenarien das Katalog Element erzeugt hat. Stattdessen sollte der Client einfach alle verwalteten Sichten oder Indizes mit den Metadaten aktualisieren, die im Katalog Element enthalten sind. Außerdem sollten doppelte oder redundante Katalog Elemente ordnungsgemäß (idemisch) behandelt werden.

Paket Details-Katalog Elemente haben zusätzlich zu den in [allen Katalog blättern enthaltenen](#catalog-leaf)Eigenschaften die folgenden Eigenschaften:

Name                    | type                       | Erforderlich | Notizen
----------------------- | -------------------------- | -------- | -----
authors                 | Zeichenfolge                     | Nein       |
created                 | Zeichenfolge                     | Nein       | Ein Zeitstempel, zu dem das Paket erstmalig erstellt wurde. Fallback-Eigenschaft: `published` .
dependencygroups        | Array von Objekten           | Nein       | Die Abhängigkeiten des Pakets, gruppiert nach Ziel Framework ([Gleiches Format wie die Paket Metadaten-Ressource](registration-base-url-resource.md#package-dependency-group))
veraltungs             | Objekt (object)                     | Nein       | Die dem Paket zugeordnete Veraltung ([Gleiches Format wie die Paket Metadaten-Ressource](registration-base-url-resource.md#package-deprecation))
description             | Zeichenfolge                     | Nein       |
iconUrl                 | Zeichenfolge                     | Nein       |
IsPreRelease            | boolean                    | Nein       | Gibt an, ob die Paketversion Vorabversion ist. Kann von erkannt werden `version` .
language                | Zeichenfolge                     | Nein       |
licenseUrl              | Zeichenfolge                     | Nein       |
Liste                  | boolean                    | Nein       | Gibt an, ob das Paket aufgelistet ist.
minClientVersion        | Zeichenfolge                     | Nein       |
packagehash             | Zeichenfolge                     | Ja      | Der Hashwert des Pakets, Codierung mit [Standardbasis 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | Zeichenfolge                     | Ja      |
PackageSize             | integer                    | Ja      | Die Größe der Datei "Package. nupkg" in Bytes.
packageTypes            | Array von Objekten           | Nein       | Die vom Autor angegebenen Pakettypen.
projectUrl              | Zeichenfolge                     | Nein       |
releaseNotes            | Zeichenfolge                     | Nein       |
requirelicensagreement | boolean                    | Nein       | `false`Bei Ausschluss ausschließen
summary                 | Zeichenfolge                     | Nein       |
tags                    | array of strings           | Nein       |
title                   | Zeichenfolge                     | Nein       |
verbatimversion         | Zeichenfolge                     | Nein       | Die Versions Zeichenfolge, wie Sie ursprünglich in der. nuspec-Datei gefunden wurde.

Die Paket `version` Eigenschaft ist die vollständige Versions Zeichenfolge nach der Normalisierung. Dies bedeutet, dass die Build-Daten von semver 2.0.0 hier eingefügt werden können.

Der `created` Zeitstempel ist der Zeitpunkt, an dem das Paket zum ersten Mal von der Paketquelle empfangen wurde. Dies ist in der Regel eine kurze Zeit vor dem Commit-Zeitstempel des Katalog Elements.

`packageHashAlgorithm`Ist eine durch die Server Implementierung definierte Zeichenfolge, die den Hash Algorithmus darstellt, mit dem der erzeugt wird `packageHash` . nuget.org hat immer den `packageHashAlgorithm` Wert von verwendet `SHA512` .

Die- `packageTypes` Eigenschaft ist nur vorhanden, wenn vom Autor ein Pakettyp angegeben wurde. Wenn Sie vorhanden ist, verfügt sie immer über mindestens einen Eintrag (1). Jedes Element im `packageTypes` Array ist ein JSON-Objekt mit den folgenden Eigenschaften:

Name      | type    | Erforderlich | Notizen
--------- | ------- | -------- | -----
name      | Zeichenfolge  | Ja      | Der Name des Pakettyps.
version    | Zeichenfolge  | Nein       | Die Version des Pakettyps. Nur vorhanden, wenn der Autor explizit eine Version in der nuspec angegeben hat.

Der `published` Zeitstempel ist der Zeitpunkt, zu dem das Paket zuletzt aufgelistet wurde.

> [!Note]
> Auf nuget.org wird der `published` Wert auf das Jahr 1900 festgelegt, wenn das Paket nicht aufgelistet ist.

#### <a name="sample-request"></a>Beispiel für eine Anforderung

GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>Beispiel für eine Antwort

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Katalog Elemente zum Löschen von Paketen

Katalog Elemente mit dem `PackageDelete` -Typ enthalten einen minimalen Satz von Informationen, die den Katalog Clients zeigen, dass ein Paket aus der Paketquelle gelöscht wurde und nicht mehr für einen Paket Vorgang (z. b. die Wiederherstellung) verfügbar ist.

> [!NOTE]
> Es ist möglich, dass ein Paket gelöscht und später mit der gleichen Paket-ID und Version erneut veröffentlicht wird. Auf nuget.org handelt es sich hierbei um einen sehr seltenen Fall, da die Annahme, dass eine Paket-ID und Version einen bestimmten Paket Inhalt impliziert, die offizielle Client Annahme unterbricht. Weitere Informationen zum Löschen von Paketen auf nuget.org finden Sie in [unserer Richtlinie](../nuget-org/policies/deleting-packages.md).

Katalog Elemente zum Löschen von Paketen haben neben den in [allen Katalog blättern enthaltenen](#catalog-leaf)Eigenschaften keine zusätzlichen Eigenschaften.

Die- `version` Eigenschaft ist die ursprüngliche Versions Zeichenfolge in der Datei "Package. nuspec".

Die- `published` Eigenschaft ist die Uhrzeit, zu der das Paket gelöscht wurde. Dies ist in der Regel der kurze Zeitpunkt vor dem Commit-Zeitstempel des Katalog Elements.

#### <a name="sample-request"></a>Beispiel für eine Anforderung

GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>Beispiel für eine Antwort

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Cursor

### <a name="overview"></a>Übersicht

In diesem Abschnitt wird ein Client Konzept beschrieben, das, obwohl nicht notwendigerweise durch das-Protokoll vorgeschrieben ist, Teil einer praktischen Implementierung des-Katalog Clients sein sollte.

Da es sich bei dem Katalog um eine nur anfügende Datenstruktur handelt, die von Zeit zu Zeit indiziert ist, sollte der Client einen **Cursor** lokal speichern und so bis zu dem Zeitpunkt, zu dem der Client Katalog Elemente verarbeitet hat, darstellen. Beachten Sie, dass dieser Cursor Wert nie mit der Computeruhr des Clients generiert werden sollte. Stattdessen sollte der Wert aus dem Wert eines Katalog Objekts stammen `commitTimestamp` .

Jedes Mal, wenn der Client neue Ereignisse in der Paketquelle verarbeiten möchte, muss er nur den Katalog für alle Katalog Elemente Abfragen, deren Commit-Zeitstempel größer als der gespeicherte Cursor ist. Nachdem der Client alle neuen Katalog Elemente erfolgreich verarbeitet hat, wird der aktuelle Commit-Zeitstempel von Katalog Elementen aufgezeichnet, die gerade als neuer Cursor Wert verarbeitet wurden.

Bei dieser Vorgehensweise kann der Client sicher sein, dass keine Paket Ereignisse auf der Paketquelle übersehen werden.
Außerdem muss der Client niemals alte Ereignisse vor dem aufgezeichneten Commit-Zeitstempel des Cursors erneut verarbeiten.

Dieses leistungsfähige cursorkonzept wird für viele der nuget.org-Hintergrund Aufträge verwendet und wird verwendet, um die V3-API selbst auf dem neuesten Stand zu halten. 

### <a name="initial-value"></a>Anfangswert

Wenn der Katalog Client zum ersten Mal gestartet wird (und daher keinen Cursor Wert hat), sollte er einen Standard Cursor Wert von verwenden. NET es `System.DateTimeOffset.MinValue` oder ein ähnliches entsprechendes Konzept eines minimalen darstellbaren Zeitstempels.

### <a name="iterating-over-catalog-items"></a>Iteration über Katalog Elemente

Zum Abfragen der nächsten zu verarbeitenden Katalog Elemente sollte der Client folgende Aktionen ausführen:

1. Abrufen des aufgezeichneten Cursor Werts aus einem lokalen Speicher.
1. Laden Sie den Katalog Index herunter, und Deserialisieren Sie ihn.
1. Sucht alle Katalogseiten mit einem Commit-Zeitstempel, der *größer ist als* der Cursor.
1. Deklarieren Sie eine leere Liste der zu verarbeitenden Katalog Elemente.
1. Für jede Katalogseite, die in Schritt 3 übereinstimmt:
   1. Herunterladen und Deserialisieren der Katalogseite.
   1. Sucht alle Katalog Elemente mit einem Commit-Zeitstempel, der *größer ist als* der Cursor.
   1. Fügen Sie alle übereinstimmenden Katalog Elemente der Liste hinzu, die in Schritt 4 deklariert wurde.
1. Sortiert die Katalog Elementliste nach dem Commit-Zeitstempel.
1. Verarbeiten Sie jedes Katalog Element nacheinander:
   1. Laden Sie das Katalog Element herunter, und Deserialisieren Sie es.
   1. Reagieren Sie entsprechend auf den Typ des Katalog Elements.
   1. Verarbeiten Sie das Katalog Element Dokument auf eine Client spezifische Weise.
1. Notieren Sie den Commit-Zeitstempel des letzten Katalog Elements als neuen Cursor Wert.

Mit diesem grundlegenden Algorithmus kann die Client Implementierung eine vollständige Ansicht aller Pakete erstellen, die in der Paketquelle verfügbar sind. Der Client muss diesen Algorithmus nur in regelmäßigen Abständen ausführen, um stets die neuesten Änderungen an der Paketquelle zu beachten.

> [!Note]
> Dies ist der Algorithmus, den nuget.org verwendet, um die [Paket Metadaten](registration-base-url-resource.md), den [Paket Inhalt](package-base-address-resource.md), die [Suche](search-query-service-resource.md) und die [Auto Vervollständigen](search-autocomplete-service-resource.md) -Ressourcen auf dem neuesten Stand zu halten.

### <a name="dependent-cursors"></a>Abhängige Cursor

Angenommen, es gibt zwei Katalog Clients, die eine inhärente Abhängigkeit aufweisen, bei der die Ausgabe eines Clients von der Ausgabe eines anderen Clients abhängig ist. 

#### <a name="example"></a>Beispiel

Beispielsweise sollte ein neu veröffentlichtes Paket unter nuget.org nicht in der Ressource Search angezeigt werden, bevor es in der Paket Metadaten-Ressource angezeigt wird. Dies liegt daran, dass der "Restore"-Vorgang, der vom offiziellen nuget-Client ausgeführt wird, die Paket Metadaten-Ressource verwendet. Wenn ein Kunde ein Paket mithilfe des Such Dienstanbieter ermittelt, sollte er in der Lage sein, das Paket mithilfe der paketmetadatenressource erfolgreich wiederherzustellen. Das heißt, die Ressource Search hängt von der Paket Metadaten-Ressource ab. Jede Ressource verfügt über einen Katalog Client-Hintergrund Auftrag, der diese Ressource aktualisiert. Jeder Client verfügt über einen eigenen Cursor.

Da beide Ressourcen aus dem Katalog erstellt wurden, darf der Cursor des Katalog Clients, der die Such Ressource aktualisiert, nicht über den Cursor des paketmetadatenkatalog-Clients *hinausgehen* .

#### <a name="algorithm"></a>Algorithmus

Um diese Einschränkung zu implementieren, ändern Sie einfach den obigen Algorithmus, um Folgendes zu erhalten:

1. Abrufen des aufgezeichneten Cursor Werts aus einem lokalen Speicher.
1. Laden Sie den Katalog Index herunter, und Deserialisieren Sie ihn.
1. Sucht alle Katalogseiten, deren Commitzeit Stempel *größer als* der Cursor **ist, der kleiner oder gleich dem Cursor der Abhängigkeit ist.**
1. Deklarieren Sie eine leere Liste der zu verarbeitenden Katalog Elemente.
1. Für jede Katalogseite, die in Schritt 3 übereinstimmt:
   1. Herunterladen und Deserialisieren der Katalogseite.
   1. Sucht alle Katalog Elemente, deren Commitzeit Stempel *größer als* der Cursor **ist, der kleiner oder gleich dem Cursor der Abhängigkeit ist.**
   1. Fügen Sie alle übereinstimmenden Katalog Elemente der Liste hinzu, die in Schritt 4 deklariert wurde.
1. Sortiert die Katalog Elementliste nach dem Commit-Zeitstempel.
1. Verarbeiten Sie jedes Katalog Element nacheinander:
   1. Laden Sie das Katalog Element herunter, und Deserialisieren Sie es.
   1. Reagieren Sie entsprechend auf den Typ des Katalog Elements.
   1. Verarbeiten Sie das Katalog Element Dokument auf eine Client spezifische Weise.
1. Notieren Sie den Commit-Zeitstempel des letzten Katalog Elements als neuen Cursor Wert.

Mithilfe dieses geänderten Algorithmus können Sie ein System abhängiger Katalog Clients erstellen, die alle Ihre eigenen spezifischen Indizes, Artefakte usw. erstellen.
