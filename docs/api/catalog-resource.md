---
title: Katalog der Ressourcen, NuGet-V3-API
description: Der Katalog ist einen Index aller Pakete erstellt und auf nuget.org gelöscht.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 8554f9515b671dbececd94a025ec7e56037c2bd9
ms.sourcegitcommit: 055248d790051774c892b220eca12015babbd668
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2018
ms.locfileid: "34152434"
---
# <a name="catalog"></a>Catalog

Die **Katalog** ist eine Ressource, die auf eine Paketquelle, wie, wann alle Paketvorgängen zeichnet. Das Katalogressource verfügt über die `Catalog` Geben Sie in der [Dienst Index](service-index.md).

> [!Note]
> Da der Katalog nicht durch den offiziellen NuGet-Client verwendet wird, implementieren nicht alle Paketquellen des Katalogs.

> [!Note]
> Derzeit ist der nuget.org-Katalog nicht in China verfügbare. Weitere Informationen finden Sie unter [NuGet/NuGetGallery #4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Versionskontrolle

Die folgenden `@type` Wert wird verwendet:

@type-Wert   | Hinweise
------------- | -----
Catalog/3.0.0 | Die erste Version

## <a name="base-url"></a>Basis-URL

Der Eintrag Point-URL für die folgenden APIs ist der Wert des der `@id` Eigenschaft, die zuvor erwähnten zur Ressource zugeordnete `@type` Werte. In diesem Thema verwendet die Platzhalter-URL `{@id}`.

## <a name="http-methods"></a>HTTP-Methoden

Alle URLs, die in der Unterstützung des Katalogs Ressource nur die HTTP-Methoden gefunden `GET` und `HEAD`.

## <a name="catalog-index"></a>Katalogfeldindex

Der Katalogindex ist ein Dokument in einen bekannten Speicherort mit einer Liste von Katalogelementen, chronologisch sortiert. Es ist der Einstiegspunkt der Katalogressource.

Der Index besteht aus Katalogseiten. Jede Seite "Katalog" enthält Katalogelemente. Jedes Katalogelement stellt ein Ereignis, das über ein einzelnes Paket zu einem Zeitpunkt zeitlich dar. Ein Katalogelement kann ein Paket darstellen, die, nicht aufgeführte, wiedereingestellte oder gelöschten aus der Paketquelle erstellt wurde. Durch die Verarbeitung der Katalogelemente in chronologischer Reihenfolge an, kann der Client keine auf dem neuesten Stand Ansicht der jedes Paket, das vorhanden ist, auf die Paketquelle V3 erstellen.

Kurz gesagt, haben die Katalog-Blobs die folgende hierarchische Struktur:

- **Index**: den Einstiegspunkt für den Katalog.
- **Seite "**: eine Gruppierung von Katalogobjekten.
- **Endknoten**: ein Dokument, das ein Katalogelement, also eine Momentaufnahme des Zustands eines einzelnen Pakets darstellt.

Jedes Katalogobjekt verfügt über eine Eigenschaft mit dem Namen der `commitTimeStamp` darstellen, wenn das Element im Katalog hinzugefügt wurde. Eine Seite "Katalog" batchweise Commits aufgerufen werden Katalogelemente hinzugefügt. Alle Katalogelemente in der gleichen Commit haben die gleichen commitzeitstempel (`commitTimeStamp`) und commit-ID (`commitId`). Katalogelemente, die in der gleichen Commit platziert darstellen, Ereignisse, die den gleichen Zeitpunkt rechtzeitig auf die Paketquelle aufgetreten sind. Es gibt keine Reihenfolge in einem Katalog Commit.

Da jedes Paket-ID und jede Version eindeutig ist, wird in einem Commit nie mehr als ein Katalogelement vorhanden sein. Dadurch wird sichergestellt, dass Katalogelemente für ein einzelnes Paket immer eindeutig in Bezug auf Commit-Timestamps sortiert werden können.

Es ist nie mehr als ein Commit im Katalog pro werden `commitTimeStamp`. Das heißt, die `commitId` ist redundant, mit der `commitTimeStamp`.

Im Gegensatz zu den [Metadatenressource "package"](registration-base-url-resource.md), die von Paket-ID indiziert ist, der Katalog ist indiziert (und abgefragt werden) nur nach Zeit.

Katalogelemente werden immer im Katalog in eine monoton ansteigende, chronologischer Reihenfolge hinzugefügt. Dies bedeutet, dass kein Commit Katalog jemals hinzugefügt werden, wenn ein Commit Katalog, zum Zeitpunkt X hinzugefügt wird wird mit einer Zeit, die kleiner oder gleich X.

Die folgende Anforderung Ruft den Index des ab.

    GET {@id}

Der Katalogindex ist ein JSON-Dokument, das ein Objekt mit den folgenden Eigenschaften enthält:

name            | Typ             | Erforderlich | Hinweise
--------------- | ---------------- | -------- | -----
commitId        | Zeichenfolge           | ja      | Eine eindeutige ID des letzten Commits zugeordnet
commitTimeStamp | Zeichenfolge           | ja      | Einen Zeitstempel des letzten Commits
count           | Ganze Zahl          | ja      | Die Anzahl der Seiten im index
items           | Array von Objekten | ja      | Ein Array von Objekten, jedes Objekt, das eine Seite darstellt.

Jedes Element in der `items` Array ist ein Objekt mit einigen minimale Details zu den einzelnen Seiten. Diese Seitenobjekte enthalten nicht die Katalog Blättern (Elemente). Die Reihenfolge der Elemente im Array ist nicht definiert. Seiten vom Client im Arbeitsspeicher mit geordnet werden ihre `commitTimeStamp` Eigenschaft.

Neue Seiten eingeführt werden, die `count` wird erhöht, und neue Objekte erscheint der `items` Array.

Hinzufügen von Elementen im Katalog, der Index des `commitId` ändert sich und die `commitTimeStamp` erhöht. Diese beiden Eigenschaften sind im Wesentlichen eine Zusammenfassung über die Seite "alle" `commitId` und `commitTimeStamp` Werte in der `items` Array.

### <a name="catalog-page-object-in-the-index"></a>Katalog-Page-Objekt im index

Die Seite Catalog-Objekten in des Katalog Indexes gefunden `items` Eigenschaft weist die folgenden Eigenschaften:

name            | Typ    | Erforderlich | Hinweise
--------------- | ------- | -------- | -----
@id             | Zeichenfolge  | ja      | Die URL zu der Seite "Katalog" Abrufen von Daten
commitId        | Zeichenfolge  | ja      | Eine eindeutige ID der letzten Commit auf dieser Seite zugeordnet
commitTimeStamp | Zeichenfolge  | ja      | Einen Zeitstempel des letzten Commits auf dieser Seite
count           | Ganze Zahl | ja      | Die Anzahl der Elemente in der Seite "Katalog"

Im Gegensatz zu den [Metadatenressource "package"](registration-base-url-resource.md) bewirkt, dass die in einigen Fällen mit Inlines in den Index, Katalog bewirkt, dass werden nie inline in den Index und müssen immer abgerufen werden, mithilfe der Seite `@id` URL.

### <a name="sample-request"></a>Beispielanforderung

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Seite "Katalog"

Die Seite "Katalog" ist eine Auflistung von Katalogobjekten. Es ist ein Dokument mit einer der abgerufenen der `@id` Werte im Katalogindex gefunden. Die URL zu einer Seite "Katalog" sollte nicht vorhersagbar sein und muss mit nur den Index des erkannt werden.

Neue Katalogelemente werden auf der Seite im Katalogindex nur mit der höchsten commitzeitstempel oder auf eine neue Seite hinzugefügt. Sobald eine Seite mit einem höheren commitzeitstempel zum Katalog hinzugefügt wird, werden ältere Seiten nie hinzugefügt oder geändert.

Das Katalogdokument-Seite ist ein JSON-Objekt mit den folgenden Eigenschaften:

name            | Typ             | Erforderlich | Hinweise
--------------- | ---------------- | -------- | -----
commitId        | Zeichenfolge           | ja      | Eine eindeutige ID der letzten Commit auf dieser Seite zugeordnet
commitTimeStamp | Zeichenfolge           | ja      | Einen Zeitstempel des letzten Commits auf dieser Seite
count           | Ganze Zahl          | ja      | Die Anzahl der Elemente auf der Seite
items           | Array von Objekten | ja      | Auf dieser Seite die Katalogelemente
parent          | Zeichenfolge           | ja      | Eine URL für den Index des

Jedes Element in der `items` Array ist ein Objekt mit einigen minimale Details über das Element des Katalogs. Diese Objekte enthalten nicht alle Daten für das Katalogelement. Die Reihenfolge der Elemente auf der Seite `items` Array ist nicht definiert. Elemente können sortiert werden, vom Client im Arbeitsspeicher mit ihren `commitTimeStamp` Eigenschaft.

Die Anzahl von Katalogelementen auf einer Seite wird durch die Implementierung definiert. Nuget.org sind höchstens 550 Elemente auf den einzelnen Seiten, auch wenn die tatsächliche Anzahl zeitlich kleinere für einige Seiten je nach Größe der nächste Batch von Commit an die Stelle sein kann.

Als neue Elemente eingefügt werden, die `count` wird erhöht und der neue Katalogobjekte angezeigt werden, der `items` Array.

Hinzufügen von Elementen auf der Seite der `commitId` Änderungen und die `commitTimeStamp` erhöht. Diese beiden Eigenschaften sind im Wesentlichen eine Übersicht über alle `commitId` und `commitTimeStamp` Werte in der `items` Array.

### <a name="catalog-item-object-in-a-page"></a>Katalog-Objekt auf einer Seite

Die Elementobjekte Katalog gefunden werden, in der Katalogseite `items` Eigenschaft weist die folgenden Eigenschaften:

name            | Typ    | Erforderlich | Hinweise
--------------- | ------- | -------- | -----
@id             | Zeichenfolge  | ja      | Die URL für das Katalogelement abrufen
@type           | Zeichenfolge  | ja      | Der Typ des Katalogelements
commitId        | Zeichenfolge  | ja      | Die Commit-ID, die diese Katalogelement zugeordnet
commitTimeStamp | Zeichenfolge  | ja      | Der commitzeitstempel, der diese Katalogelement
NuGet:ID        | Zeichenfolge  | ja      | Die Paket-ID, die auf diesem Blatt bezieht
NuGet:Version   | Zeichenfolge  | ja      | Die Version des Pakets, der auf diesem Blatt bezieht

Die `@type` Wert werden die folgenden zwei Werte:

1. `nuget:PackageDetails`: Dies entspricht `PackageDetails` im Katalog Endknoten Dokument.
1. `nuget:PackageDelete`: Dies entspricht der `PackageDelete` im Katalog Endknoten Dokument.

Weitere Informationen zu jeder Art bedeutet finden Sie unter der [Typ entsprechende Elemente](#item-types) unten.

### <a name="sample-request"></a>Beispielanforderung

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Katalog Blattebene

Der Katalog Blattebene enthält Metadaten über ein bestimmtes Paket-ID und eine Version irgendwann zeitlich. Es ist ein Dokument abgerufen, mit der `@id` Wert in eine Seite "Katalog" gefunden. Die URL zu einem Blattknoten Katalog sollte nicht vorhersagbar sein und muss mit nur einer Seite "Katalog" erkannt werden.

Das Blatt Katalogdokument ist ein JSON-Objekt mit den folgenden Eigenschaften:

name                    | Typ                       | Erforderlich | Hinweise
----------------------- | -------------------------- | -------- | -----
@type                   | Zeichenfolge oder ein Array von Zeichenfolgen | ja      | Der/die Typ(en) des Katalogelements
catalog:commitId        | Zeichenfolge                     | ja      | Eine Commit-ID, die diese Katalogelement zugeordnet
catalog:commitTimeStamp | Zeichenfolge                     | ja      | Der commitzeitstempel, der diese Katalogelement
ID                      | Zeichenfolge                     | ja      | Die Paket-ID des Katalogelements
Veröffentlicht               | Zeichenfolge                     | ja      | Das Datum der Veröffentlichung des Pakets Katalogelement
Version                 | Zeichenfolge                     | ja      | Die Paketversion des Katalogelements

### <a name="item-types"></a>Elementtypen

Die `@type` Eigenschaft ist eine Zeichenfolge oder ein Array von Zeichenfolgen. Zur Vereinfachung Wenn die `@type` Wert ist eine Zeichenfolge, die sie als beliebiges Array der Größe einer behandelt werden soll. Nicht alle möglichen Werte für `@type` dokumentiert sind. Allerdings hat jedes Katalogelement mit genau einem der beiden folgenden Werte vom Zeichenfolgentyp:

1. `PackageDetails`: stellt eine Momentaufnahme der Metadaten von Paketen
1. `PackageDelete`: Stellt ein Paket, das gelöscht wurde

### <a name="package-details-catalog-items"></a>Paketdetails Katalogelemente

Katalogelemente mit dem Typ `PackageDetails` enthalten eine Momentaufnahme der Metadaten von Paketen für ein bestimmtes Paket (Kombination aus ID und Version). Ein Paket Details Katalogelement wird erzeugt, wenn eine Paketquelle eine der folgenden Szenarien trifft:

1. Ein Paket ist **abgelegt**.
1. Ein Paket ist **aufgeführten**.
1. Ein Paket ist **nicht aufgeführte**.
1. Ein Paket ist **solche**.

Ein Paket Umfließen ist eine administrative Geste, die im Wesentlichen einen gefälschten Push eines vorhandenen Pakets ohne Änderungen auf das Paket selbst generiert. Auf nuget.org dient ein Umfließen nach einer Fehlerkorrektur in einem Hintergrund-Aufträge, die den Katalog verwenden.

Clients nutzen die Katalogelemente sollten nicht versuchen, um zu bestimmen, welches der folgenden Szenarien das Katalogelement erstellt. Stattdessen sollte der Client einfach eines verwalteten Ansicht oder eines Index mit den Metadaten, die im Katalogelement enthaltenen aktualisieren. Darüber hinaus Duplikat oder eine redundante Katalogelemente sollten unauffällig behandelt werden (idempotente).

Paket Details Katalogelemente haben die folgenden Eigenschaften zusätzlich zu den [auf bewirkt, dass alle Katalog enthalten](#catalog-leaf).

name                    | Typ                       | Erforderlich | Hinweise
----------------------- | -------------------------- | -------- | -----
authors                 | Zeichenfolge                     | Nein       |
created                 | Zeichenfolge                     | Nein       | Ein Zeitstempel, wann das Paket zuerst erstellt wurde. Fallback-Eigenschaft: `published`.
dependencyGroups        | Array von Objekten           | Nein       | Gleiche format wie die [Metadatenressource "package"](registration-base-url-resource.md#package-dependency-group)
Beschreibung             | Zeichenfolge                     | Nein       |
iconUrl                 | Zeichenfolge                     | Nein       |
isPrerelease            | boolean                    | Nein       | Davon, ob die Version des Pakets eine Vorabversion ist. Können von erkannt werden `version`.
language                | Zeichenfolge                     | Nein       |
licenseUrl              | Zeichenfolge                     | Nein       |
Liste                  | boolean                    | Nein       | Und zwar unabhängig davon, ob das Paket aufgeführt ist
minClientVersion        | Zeichenfolge                     | Nein       |
packageHash             | Zeichenfolge                     | ja      | Der Hashwert des Pakets, mit Codierung [base-64 standard](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | Zeichenfolge                     | ja      |
packageSize             | Ganze Zahl                    | ja      | Die Größe der dem Paket NUPKG in bytes
projectUrl              | Zeichenfolge                     | Nein       |
releaseNotes            | Zeichenfolge                     | Nein       |
requireLicenseAgreement | boolean                    | Nein       | Angenommen `false` ausgeschlossen
Zusammenfassung                 | Zeichenfolge                     | Nein       |
Tags                    | Array von Zeichenfolgen           | Nein       |
Titel                   | Zeichenfolge                     | Nein       |
verbatimVersion         | Zeichenfolge                     | Nein       | Die Versionszeichenfolge, wie er wurde ursprünglich in der .nuspec gefunden.

Das Paket `version` Eigenschaft ist für die vollständige, normalisierte Versionszeichenfolge. Dies bedeutet, dass SemVer 2.0.0 Builddaten hier aufgenommen werden können.

Die `created` Zeitstempel ist, wenn das Paket zuerst von der Paketquelle empfangen wurde, in der Regel kurz bevor das Katalogelement commitzeitstempel.

Die `packageHashAlgorithm` ist eine Zeichenfolge, die durch die serverimplementierung, die den Hashalgorithmus zum Erzeugen darstellt definiert die `packageHash`. NuGet.org verwendet immer die `packageHashAlgorithm` Wert `SHA512`.

Die `published` Zeitstempel ist die Uhrzeit, wann das Paket zuletzt aufgelistet.

> [!Note]
> Auf nuget.org die `published` auf das Jahr 1900, wenn das Paket nicht aufgeführte wird, Wert festgelegt ist.

#### <a name="sample-request"></a>Beispielanforderung

ERHALTEN https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>Beispielantwort

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Paket löschen Katalogelemente

Katalogelemente mit dem Typ `PackageDelete` enthalten einen minimalen Satz von Informationen, Katalog-Clients anzeigt, dass ein Paket aus der Paketquelle gelöscht wurde, und nicht mehr verfügbar, für jeden Vorgang Paket (z. B. Wiederherstellung ist).

> [!Note]
> Es ist möglich, dass ein Paket gelöscht werden soll und später erneut veröffentlichten mit dem gleichen Paket-ID und die Version. Auf nuget.org ist dies ein sehr seltenen Fall, da er den offiziellen Client Annahme zuwiderläuft, dass ein Paket-ID und eine Version einer bestimmten Paketinhalt implizieren. Weitere Informationen zum Löschen des Pakets auf nuget.org finden Sie unter [unsere Richtlinien](../policies/deleting-packages.md).

Paket löschen Katalogelemente verfügen nicht über zusätzlichen Eigenschaften zusätzlich zu den [auf bewirkt, dass alle Katalog enthalten](#catalog-leaf).

Die `version` Eigenschaft ist für die ursprüngliche Versionszeichenfolge, die in der Paket-.nuspec gefunden.

Die `published` Eigenschaft entspricht der Zeit, wenn Paket gelöscht wurde, i. d. r. als kurz bevor das Katalogelement commitzeitstempel.

#### <a name="sample-request"></a>Beispielanforderung

ERHALTEN https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>Beispielantwort

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Cursor

### <a name="overview"></a>Übersicht

In diesem Abschnitt wird beschrieben, ein Client-Konzept, die zwar nicht notwendigerweise durch das Protokoll beauftragt wird von der Implementierung einer praktische Katalog-Client verwendet werden sollte.

Da es sich bei der Katalog eine nur Anhängen-Datenstruktur, die durch Zeit indiziert ist, sollte der Client Speichern einer **Cursor** lokal darstellt, auf was den Client einem bestimmten Zeitpunkt verarbeitet hat Katalogelemente. Beachten Sie, dass dieser Cursor Wert nie die Client Computer-Format generiert werden soll. Stattdessen sollte der Wert aus einem Katalogobjekt stammen `commitTimestamp` Wert.

Jedes Mal, wenn der Client möchte neue Ereignisse in der Paketquelle zu verarbeiten, sie benötigen nur eine Abfrage den Katalog für alle Katalogelemente mit einem commitzeitstempel größer als der gespeicherte Cursor. Nachdem der Client alle neuen Katalogelemente erfolgreich verarbeitet hat, zeichnet er die neuesten commitzeitstempel von Katalogobjekten, die nur als neuen Cursor Wert verarbeitet.

Bei dieser Vorgehensweise kann der Client Achten Sie niemals alle paketereignisse leicht übersehen, die in der Paketquelle aufgetreten.
Darüber hinaus muss der Client nie alte Ereignisse vor der aufgezeichneten commitzeitstempel der Cursor erneut verarbeiten.

Dieses leistungsfähige Konzept von Cursorn dient für viele der nuget.org-Hintergrundaufträgen und wird verwendet, um die V3-API selbst auf dem neuesten Stand zu halten. 

### <a name="initial-value"></a>Anfangswert

Wenn die Katalog-Client zum ersten Mal gestartet wird (und daher keinen Cursor-Wert hat), sollten sie den Cursor Standardwert verwenden. NET `System.DateTimeOffset.MinValue` oder einige solche Analog Begriff mindestzeitstempel dargestellt werden kann.

### <a name="iterating-over-catalog-items"></a>Katalogelemente durchlaufen

Sollten der Client, für die Abfrage für den nächsten Satz von Katalogelementen verarbeiten:

1. Rufen Sie die aufgezeichneten Cursor-Wert aus einem lokalen Speicher ab.
1. Herunterladen und den Index des zu deserialisieren.
1. Alle Seiten mit einem commitzeitstempel Katalog suchen *größer als* des Cursors.
1. Deklarieren Sie eine leere Liste von Katalogelementen zu verarbeiten.
1. Für jede Seite "Katalog" abgeglichen in Schritt 3:
   1. Herunterladen und die Seite "Katalog" deserialisiert.
   1. Suchen Sie alle Katalogelemente mit einem commitzeitstempel *größer als* des Cursors.
   1. Fügen Sie der Liste, die in Schritt 4 deklariert alle übereinstimmenden Katalogelemente hinzu.
1. Sortieren Sie die Katalog-Elementliste, indem commitzeitstempel.
1. Verarbeiten Sie jede Katalogelement nacheinander aus:
   1. Herunterladen und das Katalogelement zu deserialisieren.
   1. Auf das Katalogelement Typ entsprechend reagieren.
   1. Das Katalogdokument-Element in einer Weise clientspezifische zu verarbeiten.
1. Notieren Sie die letzte Katalogobjekt commitzeitstempel als Wert der neuen Cursor.

Die Clientimplementierung kann mit diesen grundlegenden Algorithmus einen vollständigen Überblick über alle verfügbaren Pakete auf die Paketquelle erstellen. Dieser Algorithmus in regelmäßigen Abständen, um immer die neuesten Änderungen an der Paketquelle berücksichtigen muss der Client nur ausgeführt werden.

> [!Note]
> Dies ist der Algorithmus, nuget.org verwendet, um beizubehalten der [Paketmetadaten](registration-base-url-resource.md), [Paketinhalt](package-base-address-resource.md), [Suche](search-query-service-resource.md) und [AutoVervollständigen](search-autocomplete-service-resource.md) Ressourcen, die auf dem neuesten Stand sind.

### <a name="dependent-cursors"></a>Abhängige Cursor

Angenommen Sie, es gibt zwei Katalog Clients mit einer inhärenten Abhängigkeit Ausgabe des Clients, auf dem ein Client-Ausgabe hängt. 

#### <a name="example"></a>Beispiel

Z. B. auf nuget.org ein neu veröffentlichtes Pakets nicht in der Suche Ressource angezeigt werden soll, bevor er in den Metadaten-Ressource "Package" angezeigt wird. Dies ist, da der "Restore"-Vorgang vom offiziellen NuGet-Client durchgeführt wird den Metadaten-Ressource "Package" verwendet. Wenn ein Kunde ein Paket mit der Search-Dienst erkennt, sollten sie das Paket mithilfe der Metadaten-Ressource "Package" erfolgreich wiederhergestellt werden können. Die Metadaten-Ressource "Package" heißt, abhängig die suchen-Ressource. Jede Ressource weist einen Katalog Client Hintergrundauftrag Aktualisieren dieser Ressource. Jeder Client hat einen eigenen Cursor.

Da beide Ressourcen außerhalb des Katalogs und der Cursor des Clients Katalog erstellt werden, die die Ressource für die Suche aktualisiert *muss nicht hinausgehen* den Cursor über dem Paket Metadaten Katalog-Client.

#### <a name="algorithm"></a>Algorithmus

Um diese Einschränkung zu implementieren, ändern Sie einfach den Algorithmus, der oben genannten sein:

1. Rufen Sie die aufgezeichneten Cursor-Wert aus einem lokalen Speicher ab.
1. Herunterladen und den Index des zu deserialisieren.
1. Alle Seiten mit einem commitzeitstempel Katalog suchen *größer als* Cursor **kleiner oder gleich der Abhängigkeit Cursor.**
1. Deklarieren Sie eine leere Liste von Katalogelementen zu verarbeiten.
1. Für jede Seite "Katalog" abgeglichen in Schritt 3:
   1. Herunterladen und die Seite "Katalog" deserialisiert.
   1. Suchen Sie alle Katalogelemente mit einem commitzeitstempel *größer als* des Cursors **kleiner oder gleich der Abhängigkeit Cursor.**
   1. Fügen Sie der Liste, die in Schritt 4 deklariert alle übereinstimmenden Katalogelemente hinzu.
1. Sortieren Sie die Katalog-Elementliste, indem commitzeitstempel.
1. Verarbeiten Sie jede Katalogelement nacheinander aus:
   1. Herunterladen und das Katalogelement zu deserialisieren.
   1. Auf das Katalogelement Typ entsprechend reagieren.
   1. Das Katalogdokument-Element in einer Weise clientspezifische zu verarbeiten.
1. Notieren Sie die letzte Katalogobjekt commitzeitstempel als Wert der neuen Cursor.

Mithilfe dieses geänderte Algorithmus können Sie ein System von abhängigen Katalog Clients erstellen, alle erzeugen, ihre eigenen bestimmte Indizes, Elemente usw.
