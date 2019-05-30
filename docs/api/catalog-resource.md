---
title: Katalogressource, Version 3 von NuGet-API
description: Der Katalog ist ein Index für alle Pakete erstellt und auf nuget.org gelöscht.
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 4884de71151ee1ae3c0a78b803c9222f9c1d86ec
ms.sourcegitcommit: ef08f376688f0191a8d3d873b6a4386afd799373
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2019
ms.locfileid: "66266358"
---
# <a name="catalog"></a>Catalog

Die **Katalog** ist eine Ressource, die auf eine Paketquelle an, wie, wann alle Paketvorgängen erfasst. Die Katalogressource hat die `Catalog` Geben Sie in der [dienstindex](service-index.md). Sie können diese Ressource zu verwenden, [Abfragen für alle Pakete veröffentlicht](../guides/api/query-for-all-published-packages.md).

> [!Note]
> Da der Katalog nicht von der offiziellen NuGet-Client verwendet wird, implementieren Sie nicht alle Paketquellen des Katalogs.

> [!Note]
> Derzeit ist der Katalog von nuget.org nicht in China verfügbar. Weitere Informationen finden Sie unter [NuGet/NuGetGallery #4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Versionskontrolle

Die folgenden `@type` Wert wird verwendet:

@type -Wert   | Hinweise
------------- | -----
Catalog/3.0.0 | Die erste Version

## <a name="base-url"></a>Basis-URL

Der Eintrag-Zugriffspunkt-URL für die folgenden APIs ist der Wert des der `@id` -Eigenschaft zusammen mit den oben genannten Ressourcen `@type` Werte. In diesem Thema verwendet die Platzhalter-URL `{@id}`.

## <a name="http-methods"></a>HTTP-Methoden

Alle URLs finden Sie in der Unterstützung des Katalogs Ressource nur für die HTTP-Methoden `GET` und `HEAD`.

## <a name="catalog-index"></a>Katalogindex

Der Katalogindex ist ein Dokument in einem bekannten Speicherort, der eine Liste von Katalogelementen, Migrationen chronologisch angeordnet hat. Es ist der Einstiegspunkt der Katalogressource.

Der Index besteht Katalogseiten. Jede Katalogseite enthält Katalogelemente. Jede Katalogelement stellt ein Ereignis zu einem einzelnen Paket zu einem bestimmten Zeitpunkt dar. Ein Katalogelement kann es sich um ein Paket darstellen, die nicht aufgeführte, neu erstellt, oder gelöschten aus der Paketquelle wurde. Durch die Verarbeitung von Katalogelementen in chronologischer Reihenfolge, kann der Client eine aktuelle Ansicht der jedes Paket, das vorhanden ist, auf die Paketquelle V3 erstellen.

Kurz gesagt, haben die Katalog-Blobs die folgende hierarchische Struktur:

- **Index**: der Einstiegspunkt für den Katalog.
- **Seite**: eine Gruppierung von Katalogelementen.
- **Blattelemente**: ein Dokument, das ein Katalogelement, wird eine Momentaufnahme des Status eines einzelnen Pakets darstellt.

Jede Katalogobjekt verfügt über eine Eigenschaft mit dem Namen der `commitTimeStamp` darstellen, wenn das Element im Katalog hinzugefügt wurde. Ein Katalogseite in Batches, die als Commits bezeichnet werden Katalogelemente hinzugefügt. Alle Katalogelemente im selben Commit haben den gleichen commitzeitstempel (`commitTimeStamp`) und commit-ID (`commitId`). Katalogelemente, die im selben Commit platziert darstellen, Ereignisse, die gleiche Punktmenge rechtzeitig auf die Paketquelle aufgetreten sind. Es gibt keine Reihenfolge in einem Katalog Commit.

Da jede Paket-ID und Version eindeutig ist, werden es nie mehr als ein Element des Katalogs in einem Commit. Dadurch wird sichergestellt, dass die Katalogelemente, die für ein einzelnes Paket immer eindeutig in Bezug auf Commit-Timestamps sortiert werden können.

Es ist nie mehr als ein Commit für den Katalog pro `commitTimeStamp`. Das heißt, die `commitId` ist redundant, mit der `commitTimeStamp`.

Im Gegensatz zu den [paketmetadatenressource](registration-base-url-resource.md), die von Paket-ID indiziert ist, wird der Katalog wird indiziert (und abgefragt werden) nur nach Zeit.

Katalogelemente werden immer im Katalog in einer monoton ansteigende, chronologischer Reihenfolge hinzugefügt. Dies bedeutet, dass kein Commit Katalog je hinzugefügt werden, wenn ein Katalog-Commit, zum Zeitpunkt X hinzugefügt wird wird mit einer Zeit, die kleiner als oder gleich X.

Die folgende Anforderung Ruft den Katalogindex ab.

    GET {@id}

Der Katalogindex ist ein JSON-Dokument, das ein Objekt mit den folgenden Eigenschaften enthält:

Name            | Typ             | Erforderlich | Hinweise
--------------- | ---------------- | -------- | -----
commitId        | Zeichenfolge           | ja      | Eine eindeutige ID zugewiesen, mit dem aktuellsten commit
commitTimeStamp | Zeichenfolge           | ja      | Ein Zeitstempel des letzten Commits
count           | Ganze Zahl          | ja      | Die Anzahl der Seiten im index
items           | Array von Objekten | ja      | Ein Array von Objekten, jedes Objekt, das eine Seite darstellt.

Jedes Element in der `items` Array ist ein Objekt mit einigen minimale Details zu den einzelnen Seiten. Diese Seitenobjekte enthalten nicht die Katalogblättern (Elemente). Die Reihenfolge der Elemente im Array ist nicht definiert. Seiten können sortiert werden, vom Client in den Arbeitsspeicher mit ihren `commitTimeStamp` Eigenschaft.

Wenn neue Seiten eingeführt werden, die `count` erhöht und neue Objekte werden angezeigt, der `items` Array.

Hinzufügen von Elementen im Katalog, der Index des `commitId` ändert und die `commitTimeStamp` erhöht. Diese beiden Eigenschaften sind im Wesentlichen eine Zusammenfassung über die Seite "alle" `commitId` und `commitTimeStamp` Werte in der `items` Array.

### <a name="catalog-page-object-in-the-index"></a>Katalog-Page-Objekt im index

Die Seite Katalogobjekten finden Sie in des Katalogindex `items` Eigenschaft haben die folgenden Eigenschaften:

Name            | Typ    | Erforderlich | Hinweise
--------------- | ------- | -------- | -----
@id             | Zeichenfolge  | ja      | Die URL, Fetch-Seite "Sicherungskatalog"
commitId        | Zeichenfolge  | ja      | Eine eindeutige ID, die mit dem aktuellsten Commit auf dieser Seite verknüpft ist
commitTimeStamp | Zeichenfolge  | ja      | Ein Zeitstempel des letzten Commits auf dieser Seite
count           | Ganze Zahl | ja      | Die Anzahl der Elemente in der Seite "Katalog"

Im Gegensatz zu den [paketmetadatenressource](registration-base-url-resource.md) in einigen Situationen wird in den Index verlässt, Katalogseiten werden nie inline in den Index und müssen immer abgerufen werden, mithilfe der Seite `@id` URL.

### <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Seite "Sicherungskatalog"

Die Seite "Katalog" ist eine Sammlung von Katalogelementen. Es ist ein Dokument mithilfe eines der `@id` finden Sie in den Katalogindex. Die URL zu einer Katalogseite sollte nicht vorhersehbar sein und sollte nur den Katalogindex mithilfe ermittelt werden.

Neuen Katalogelemente werden auf der Seite in den Katalogindex nur mit der höchsten Commit-Timestamps oder auf eine neue Seite hinzugefügt. Sobald eine Seite mit einem höheren commitzeitstempel im Katalog hinzugefügt wurde, werden ältere Seiten nicht hinzugefügt oder geändert.

Das Katalog-Seite-Dokument ist ein JSON-Objekt mit den folgenden Eigenschaften:

Name            | Typ             | Erforderlich | Hinweise
--------------- | ---------------- | -------- | -----
commitId        | Zeichenfolge           | ja      | Eine eindeutige ID, die mit dem aktuellsten Commit auf dieser Seite verknüpft ist
commitTimeStamp | Zeichenfolge           | ja      | Ein Zeitstempel des letzten Commits auf dieser Seite
count           | Ganze Zahl          | ja      | Die Anzahl der Elemente auf der Seite
items           | Array von Objekten | ja      | Die Katalogelemente auf dieser Seite
parent          | Zeichenfolge           | ja      | Eine URL zu den Katalogindex

Jedes Element in der `items` Array ist ein Objekt mit einigen minimale Details über das Katalogelement. Diese Objekte enthalten nicht alle Daten für das Katalogelement. Die Reihenfolge der Elemente in der Seite `items` Array ist nicht definiert. Elemente können sortiert werden, vom Client in den Arbeitsspeicher mit ihren `commitTimeStamp` Eigenschaft.

Die Anzahl von Katalogelementen in einer Seite wird durch die Implementierung definiert. Für "nuget.org" sind es höchstens 550 Elemente auf jeder Seite, obwohl die tatsächliche Anzahl rechtzeitig für einige Seiten abhängig von der Größe des nächsten Commits Batches an dem Punkt kleiner sein kann.

Wenn neue Elemente eingeführt werden, die `count` wird erhöht und der neue Katalogobjekte angezeigt werden, der `items` Array.

Hinzufügen von Elementen auf der Seite die `commitId` Änderungen und die `commitTimeStamp` erhöht. Diese beiden Eigenschaften sind im Wesentlichen eine Übersicht über alle `commitId` und `commitTimeStamp` Werte in der `items` Array.

### <a name="catalog-item-object-in-a-page"></a>Katalogobjekt Element auf einer Seite

Die Elementobjekte Katalog finden Sie in der Katalogseite `items` Eigenschaft haben die folgenden Eigenschaften:

Name            | Typ    | Erforderlich | Hinweise
--------------- | ------- | -------- | -----
@id             | Zeichenfolge  | ja      | Die URL zum Abrufen des Katalogelements
@type           | Zeichenfolge  | ja      | Der Typ des Katalogelements
commitId        | Zeichenfolge  | ja      | Die Commit-ID, die diesem Katalogelement zugeordnet
commitTimeStamp | Zeichenfolge  | ja      | Der commitzeitstempel, der dieses Katalogelement
nuget:id        | Zeichenfolge  | ja      | Die Paket-ID, die auf diesem Blatt beziehen
nuget:version   | Zeichenfolge  | ja      | Die Paketversion, der auf diesem Blatt beziehen

Die `@type` Wert wird einer der beiden folgenden Werte sein:

1. `nuget:PackageDetails`: Dies entspricht `PackageDetails` Geben Sie die katalogblattdokument.
1. `nuget:PackageDelete`: Dies entspricht der `PackageDelete` Geben Sie die katalogblattdokument.

Weitere Informationen finden Sie unter jeder Art bedeutet die [entsprechende Elemente Typ](#item-types) unten.

### <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Katalog-Blatt

Das Katalog-Blatt enthält Metadaten zu einem bestimmten Paket-ID und Version an einem bestimmten Punkt in-Time an. Es ist ein Dokument mithilfe der `@id` Wert in eine Seite "Katalog" gefunden. Die URL zu einem Blattknoten Katalog sollte nicht vorhersehbar sein und sollte mit nur einer Katalogseite ermittelt werden.

Die katalogblattdokument ist ein JSON-Objekt mit den folgenden Eigenschaften:

Name                    | Typ                       | Erforderlich | Hinweise
----------------------- | -------------------------- | -------- | -----
@type                   | Zeichenfolge oder Array von Zeichenfolgen | ja      | Die Typen des Katalogelements
catalog:commitId        | Zeichenfolge                     | ja      | Eine Commit-ID, die diesem Katalogelement zugeordnet
catalog:commitTimeStamp | Zeichenfolge                     | ja      | Der commitzeitstempel, der dieses Katalogelement
id                      | Zeichenfolge                     | ja      | Die Paket-ID des Katalogelements
Veröffentlicht               | Zeichenfolge                     | ja      | Das Datum der Veröffentlichung des Pakets Katalogelement
version                 | Zeichenfolge                     | ja      | Die Paketversion des Katalogelements

### <a name="item-types"></a>Elementtypen

Die `@type` -Eigenschaft ist eine Zeichenfolge oder ein Array von Zeichenfolgen. Der Einfachheit halber Wenn die `@type` Wert ist eine Zeichenfolge, die es als ein Array der Größe eines behandelt werden soll. Nicht alle möglichen Werte für `@type` dokumentiert sind. Jede Katalogelement weist jedoch genau einem der beiden folgenden geben Zeichenfolgenwerte:

1. `PackageDetails`: stellt eine Momentaufnahme der Metadaten von Paketen
1. `PackageDelete`: Stellt ein Paket, das gelöscht wurde

### <a name="package-details-catalog-items"></a>Paketdetails Katalogobjekte

Katalogobjekte mit dem Typ `PackageDetails` enthalten eine Momentaufnahme der Metadaten von Paketen für ein bestimmtes Paket (Kombination aus ID und Version). Ein Paket-Details-Katalogelement wird immer dann ausgelöst, wenn eine Paketquelle, eines der folgenden Szenarien auftritt:

1. Ein Paket ist **mithilfe von Push übertragen**.
1. Ein Paket ist **aufgeführten**.
1. Ein Paket ist **nicht aufgeführte**.
1. Ein Paket ist **solche**.

Ein Paket geräteauflösung ist eine administrative Aktion, die im Wesentlichen einen gefälschten Push von einem vorhandenen Paket ohne Änderungen auf das Paket selbst generiert. Auf nuget.org wird eine geänderte flussrichtung verwendet, nach dem Beheben eines Fehlers in einem der Hintergrundaufträge, die Verarbeiten des Katalogs.

Nutzen die Katalogelemente Clients sollten nicht versuchen, um zu bestimmen, welche dieser Szenarien das Katalogelement erstellt. Stattdessen sollte der Client einfach jede Verwaltete Sicht oder den Index mit den im Katalogelement enthaltenen Metadaten aktualisieren. Darüber hinaus doppelte oder redundante Katalogelemente sollte nicht erfolgreich behandelt werden (Wiederholungsversuche).

Paket-Details-Katalogelemente haben die folgenden Eigenschaften zusätzlich zu den [enthalten alle Katalogseiten](#catalog-leaf).

Name                    | Typ                       | Erforderlich | Hinweise
----------------------- | -------------------------- | -------- | -----
authors                 | Zeichenfolge                     | Nein       |
created                 | Zeichenfolge                     | Nein       | Ein Zeitstempel, wann das Paket zuerst erstellt wurde. Fallback-Eigenschaft: `published`.
dependencyGroups        | Array von Objekten           | Nein       | Gleiche format wie die [paketmetadatenressource](registration-base-url-resource.md#package-dependency-group)
description             | Zeichenfolge                     | Nein       |
iconUrl                 | Zeichenfolge                     | Nein       |
isPrerelease            | boolean                    | Nein       | Unabhängig davon, ob die Paketversion Vorabversion ist. Erkannt werden können, von `version`.
language                | Zeichenfolge                     | Nein       |
licenseUrl              | Zeichenfolge                     | Nein       |
Liste                  | boolean                    | Nein       | Unabhängig davon, ob das Paket aufgeführt ist
minClientVersion        | Zeichenfolge                     | Nein       |
packageHash             | Zeichenfolge                     | ja      | Der Hash des Pakets, Codierung mit [base-64-standard](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | Zeichenfolge                     | ja      |
packageSize             | Ganze Zahl                    | ja      | Die Größe der Paket-NUPKG-Datei in Byte
projectUrl              | Zeichenfolge                     | Nein       |
releaseNotes            | Zeichenfolge                     | Nein       |
requireLicenseAgreement | boolean                    | Nein       | Angenommen `false` ausgeschlossen
summary                 | Zeichenfolge                     | Nein       |
tags                    | Array von Zeichenfolgen           | Nein       |
title                   | Zeichenfolge                     | Nein       |
verbatimVersion         | Zeichenfolge                     | Nein       | Die Versionszeichenfolge, wie sie wurde ursprünglich in der NuSpec gefunden.

Das Paket `version` Eigenschaft ist die vollständige Versionszeichenfolge nach der Normalisierung. Dies bedeutet, dass SemVer 2.0.0-Builddaten hier aufgenommen werden können.

Die `created` Zeitstempel ist, wenn das Paket zuerst von der Paketquelle empfangen wurde, in der Regel eine kurze Zeit vor dem Commit-Timestamps für das Katalogelement.

Die `packageHashAlgorithm` ist eine Zeichenfolge, die durch die serverimplementierung, die die hashing-Algorithmus verwendet, um erzeugen darstellt definiert die `packageHash`. NuGet.org verwendet immer die `packageHashAlgorithm` Wert `SHA512`.

Die `published` Zeitstempel ist die Zeit, wenn das Paket zuletzt aufgeführt.

> [!Note]
> Auf nuget.org die `published` Wert wird festgelegt, um das Jahr 1900, wenn das Paket nicht aufgelistet ist.

#### <a name="sample-request"></a>Beispiel für eine Anforderung

ERHALTEN https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>Beispielantwort

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Paket löschen Katalogelemente

Katalogobjekte mit dem Typ `PackageDelete` enthalten einen minimalen Satz von Informationen, die für Katalog-Clients, dass ein Paket aus der Paketquelle gelöscht wurde und nicht mehr verfügbar ist, für jeden Paket-Vorgang (z. B. Wiederherstellung ist).

> [!Note]
> Es ist möglich, dass ein Paket gelöscht werden und später erneut veröffentlichten mithilfe der gleichen Paket-ID und Version. Auf nuget.org entspricht dies einer seltenen Fall des Clients, auf der offiziellen Annahme unterbrochen wird, die ein Paket-ID und eine Version einer bestimmten Paketinhalt implizieren. Weitere Informationen zum Löschen des Pakets auf nuget.org finden Sie unter [unsere Richtlinie](../policies/deleting-packages.md).

Paket löschen Katalogelemente verfügen nicht über zusätzlichen Eigenschaften zusätzlich zu den [enthalten alle Katalogseiten](#catalog-leaf).

Die `version` Eigenschaft ist die ursprüngliche Versionszeichenfolge finden Sie in der im Paket-Abschnitt.

Die `published` Eigenschaft ist der Zeitpunkt, wenn Paket gelöscht wurde, in der Regel als kurz vor dem Commit-Timestamps für das Katalogelement.

#### <a name="sample-request"></a>Beispiel für eine Anforderung

ERHALTEN https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>Beispielantwort

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Cursor

### <a name="overview"></a>Übersicht

In diesem Abschnitt wird beschrieben, ein Client-Konzept, die zwar nicht notwendigerweise vom Netzwerkprotokoll beauftragt wird von der Implementierung einer praktischen Katalog-Client angehören soll.

Der Client sollte speichern, da der Katalog eine nur-anfügen-Datenstruktur Zeitindex wird, eine **Cursor** lokal darstellt, auf was den Client einem bestimmten Zeitpunkt verarbeitet hat Katalogelemente. Beachten Sie, dass dieser Cursorwert nie dem Client-Computer-Format generiert werden soll. In diesem Fall stammt der Wert sollte ein Katalogobjekt `commitTimestamp` Wert.

Jedes Mal, wenn neue Ereignisse in der Paketquelle zu verarbeiten, ist der Client möchte, sie benötigen nur die Abfrage den Katalog für alle Katalogelemente mit einem commitzeitstempel größer als der gespeicherte Cursor. Nachdem der Client alle neuen Katalogelemente erfolgreich verarbeitet wurde, zeichnet sie neueste commitzeitstempel von Katalogelementen nur als seine neuen Cursorwert verarbeitet.

Mit diesem Ansatz kann der Client werden Sie sicher, dass verpassen Sie nie paketereignisse wieder, die auf die Paketquelle aufgetreten sind.
Darüber hinaus muss der Client nicht erneut verarbeiten, alte Ereignisse vor der aufgezeichneten commitzeitstempel des Cursors.

Dieses leistungsfähige Konzept der Cursor wird verwendet, für viele der nuget.org-Hintergrundaufträge und wird verwendet, um die V3-API selbst auf dem neuesten Stand zu halten. 

### <a name="initial-value"></a>Anfangswert

Wenn der Katalog-Client zum ersten Mal gestartet wird (und daher keine Cursorwert hat), sollten sie den Cursor Standardwert verwenden. NET `System.DateTimeOffset.MinValue` oder eine solche Analog ansatzweise mindestzeitstempel dargestellt werden kann.

### <a name="iterating-over-catalog-items"></a>Durchlaufen von Katalogelementen

Um den nächsten Satz von Katalogelementen verarbeiten abzufragen, sollten der Client:

1. Rufen Sie die aufgezeichneten Cursorwert aus einem lokalen Speicher.
1. Laden und Deserialisieren des Katalogindexes.
1. Suchen, die alle Seiten mit einem commitzeitstempel Katalog *größer als* des Cursors.
1. Deklarieren Sie eine leere Liste von Katalogelementen verarbeiten.
1. Jede Katalogseite abgeglichen, die in Schritt 3:
   1. Herunterladen und deserialisiert die Seite "Katalog".
   1. Suchen, die alle Katalogobjekte mit einem commitzeitstempel *größer als* des Cursors.
   1. Fügen Sie alle übereinstimmenden Katalogelemente der Liste, die deklariert, die in Schritt 4 hinzu.
1. Sortieren Sie die Liste der Katalog-Element, nach dem commitzeitstempel.
1. Verarbeiten Sie jede Katalogelement nacheinander aus:
   1. Laden Sie und Deserialisieren Sie das Katalogelement.
   1. Angemessen zu reagieren auf das Katalogelement-Typ.
   1. Das Katalogdokument-Element in einer Client-spezifische Weise zu verarbeiten.
1. Notieren Sie das letzte Katalogelement commitzeitstempel als den neuen Cursorwert.

Die Clientimplementierung kann mit diesem einfachen Algorithmus einen vollständigen Überblick über alle verfügbaren Pakete auf die Paketquelle erstellen. Der Client muss diesen Algorithmus in regelmäßigen Abständen, um immer die neuesten Änderungen an der Paketquelle achten nur ausgeführt werden.

> [!Note]
> Dies ist der Algorithmus, nuget.org verwendet wird, zu der [Paketmetadaten](registration-base-url-resource.md), [Paketinhalt](package-base-address-resource.md), [Suche](search-query-service-resource.md) und [AutoVervollständigen](search-autocomplete-service-resource.md) Ressourcen, die auf dem neuesten Stand sind.

### <a name="dependent-cursors"></a>Abhängige Cursor

Angenommen Sie, es gibt zwei Katalog-Clients, die eine inhärente Abhängigkeit verfügen, hängt, in denen ein Client-Ausgabe in einem anderen Client-Ausgabe. 

#### <a name="example"></a>Beispiel

Beispielsweise sollte auf nuget.org ein neu veröffentlichtes Paket nicht in der Ressource suchen angezeigt werden, bevor er in den Metadatenressource "Package" angezeigt wird. Dies ist, da Sie der Vorgang "Restore" von der offiziellen NuGet-Client die Ressource "Package" Metadaten verwendet. Wenn ein Kunde ein Paket mit der Search-Dienst erkennt, sollten sie sich, dieses Paket mit der Ressource "Package" Metadaten erfolgreich wiederherstellen können. Die Ressource "Package" Metadaten also abhängig Suche Ressource. Jede Ressource weist einen Katalog Client Hintergrundauftrag aktualisieren diese Ressource. Jeder Client verfügt über eine eigene Cursor.

Da beide Ressourcen aus dem Katalog, der den Cursor über den Katalog-Client erstellt werden, die die Suche ressourcenupdates *muss nicht hinausgehen* den Cursor über dem Paket Metadaten Katalog-Client.

#### <a name="algorithm"></a>Algorithmus

Um diese Einschränkung zu implementieren, ändern Sie einfach den Algorithmus aus, um die werden:

1. Rufen Sie die aufgezeichneten Cursorwert aus einem lokalen Speicher.
1. Laden und Deserialisieren des Katalogindexes.
1. Suchen, die alle Seiten mit einem commitzeitstempel Katalog *größer als* des Cursors **kleiner oder gleich der Abhängigkeit Cursor.**
1. Deklarieren Sie eine leere Liste von Katalogelementen verarbeiten.
1. Jede Katalogseite abgeglichen, die in Schritt 3:
   1. Herunterladen und deserialisiert die Seite "Katalog".
   1. Suchen, die alle Katalogobjekte mit einem commitzeitstempel *größer als* des Cursors **kleiner oder gleich der Abhängigkeit Cursor.**
   1. Fügen Sie alle übereinstimmenden Katalogelemente der Liste, die deklariert, die in Schritt 4 hinzu.
1. Sortieren Sie die Liste der Katalog-Element, nach dem commitzeitstempel.
1. Verarbeiten Sie jede Katalogelement nacheinander aus:
   1. Laden Sie und Deserialisieren Sie das Katalogelement.
   1. Angemessen zu reagieren auf das Katalogelement-Typ.
   1. Das Katalogdokument-Element in einer Client-spezifische Weise zu verarbeiten.
1. Notieren Sie das letzte Katalogelement commitzeitstempel als den neuen Cursorwert.

Mit diesem geänderten Algorithmus können Sie ein System von abhängigen Katalog Clients erstellen, eigene bestimmte Indizes, Artefakte usw. alle erzeugt.
