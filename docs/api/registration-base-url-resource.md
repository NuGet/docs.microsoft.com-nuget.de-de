---
title: Paket Metadaten, nuget-API
description: Die Basis-URL für die Paket Registrierung ermöglicht das Abrufen von Metadaten zu Paketen.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 852dca8c70b09d941e844b1f7cd03b38e2192481
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237522"
---
# <a name="package-metadata"></a>Paketmetadaten

Mithilfe der nuget V3-API können Sie Metadaten zu den Paketen abrufen, die in einer Paketquelle verfügbar sind. Diese Metadaten können mithilfe der Ressource abgerufen werden, `RegistrationsBaseUrl` die im [Dienst Index](service-index.md)gefunden wurde.

Die Sammlung der Dokumente, die unter gefunden `RegistrationsBaseUrl` werden, wird häufig als "Registrierungen" oder "registrierungsblob" bezeichnet. Der Satz von Dokumenten unter einem einzelnen `RegistrationsBaseUrl` wird als "Registrierungs Struktur" bezeichnet. Eine Registrierungs Struktur enthält alle Metadaten zu jedem Paket, das in einer Paketquelle verfügbar ist.

## <a name="versioning"></a>Versionsverwaltung

Die folgenden `@type` Werte werden verwendet:

Wert vom Typ @type                     | Notizen
------------------------------- | -----
Registrationsbaseurl            | Die erste Version
Registrationsbaseurl/3.0.0-Beta | Alias von `RegistrationsBaseUrl`
Registrationsbaseurl/3.0.0-RC   | Alias von `RegistrationsBaseUrl`
Registrationsbaseurl/3.4.0      | Gzip-Antworten
Registrationsbaseurl/3.6.0      | Umfasst semver 2.0.0-Pakete

Dies stellt drei unterschiedliche Registrierungs Strukturen dar, die für verschiedene Client Versionen verfügbar sind.

### <a name="registrationsbaseurl"></a>Registrationsbaseurl

Diese Registrierungen werden nicht komprimiert (was bedeutet, dass Sie einen impliziten verwenden `Content-Encoding: identity` ). Semver 2.0.0-Pakete werden aus dieser Hive **ausgeschlossen** .

### <a name="registrationsbaseurl340"></a>Registrationsbaseurl/3.4.0

Diese Registrierungen werden mithilfe von komprimiert `Content-Encoding: gzip` . Semver 2.0.0-Pakete werden aus dieser Hive **ausgeschlossen** .

### <a name="registrationsbaseurl360"></a>Registrationsbaseurl/3.6.0

Diese Registrierungen werden mithilfe von komprimiert `Content-Encoding: gzip` . Semver 2.0.0-Pakete sind in dieser Hive **enthalten** .
Weitere Informationen zu semver 2.0.0 finden Sie [unter semver 2.0.0-Unterstützung für nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>Basis-URL

Die Basis-URL für die folgenden APIs ist der Wert der `@id` Eigenschaft, die den oben erwähnten Ressourcen Werten zugeordnet ist `@type` . Im folgenden Dokument wird die Platzhalter-Basis-URL `{@id}` verwendet.

## <a name="http-methods"></a>HTTP-Methoden

Alle URLs, die in der Registrierungs Ressource gefunden werden, unterstützen die HTTP `GET` -Methoden und `HEAD` .

## <a name="registration-index"></a>Registrierungs Index

Die Registrierungs Ressource gruppiert Paket Metadaten nach Paket-ID. Es ist nicht möglich, gleichzeitig Daten zu mehr als einer Paket-ID zu erhalten. Diese Ressource bietet keine Möglichkeit, Paket-IDs zu ermitteln. Stattdessen wird angenommen, dass der Client die gewünschte Paket-ID bereits kennt. Verfügbare Metadaten zu den einzelnen Paketversionen variieren je nach Server Implementierung. Die paketregistrierungsblobare haben die folgende hierarchische Struktur:

- **Index** : der Einstiegspunkt für die Paket Metadaten, der von allen Paketen in einer Quelle mit der gleichen Paket-ID gemeinsam verwendet wird.
- **Seite** : eine Gruppierung von Paketversionen. Die Anzahl der Paketversionen in einer Seite wird durch die Server Implementierung definiert.
- **Blatt** : ein Dokument, das für eine einzelne Paketversion spezifisch ist.

Die URL des Registrierungs Indexes ist vorhersagbar und kann vom Client festgelegt werden, wenn eine Paket-ID und der Wert der Registrierungs Ressource `@id` aus dem Dienst Index angegeben werden. Die URLs für die Registrierungsseiten und Blätter werden erkannt, indem der Registrierungs Index überprüft wird.

### <a name="registration-pages-and-leaves"></a>Registrierungsseiten und-Blätter

Obwohl es nicht unbedingt erforderlich ist, dass eine Server Implementierung Registrierungs Blätter in separaten Registrierungsseiten Dokumenten speichert, empfiehlt es sich, Client seitigen Speicher zu sparen. Anstatt alle Registrierungs Blätter im Index zu Inlining oder die Blätter in Seiten Dokumenten sofort zu speichern, wird empfohlen, dass die Server Implementierung eine heuristische definiert, um zwischen den beiden Ansätzen basierend auf der Anzahl der Paketversionen oder der kumulativen Größe von Paket Blättern zu wählen.

Wenn alle Paketversionen (Blätter) im Registrierungs Index gespeichert werden, wird die Anzahl von HTTP-Anforderungen gespeichert, die zum Abrufen von Paket Metadaten erforderlich sind, aber ein größeres Dokument muss heruntergeladen werden, und es muss mehr Client Arbeitsspeicher zugeordnet werden. Wenn die Server Implementierung hingegen sofort Registrierungs Blätter in separaten Seiten Dokumenten speichert, muss der Client weitere HTTP-Anforderungen ausführen, um die benötigten Informationen zu erhalten.

Die Heuristik, die von nuget.org verwendet wird, lautet wie folgt: Wenn es 128 oder mehr Versionen eines Pakets gibt, unterbrechen Sie die Blätter in Seiten der Größe 64. Wenn weniger als 128 Versionen vorhanden sind, werden alle Blätter in den Registrierungs Index verschoben. Beachten Sie, dass Pakete mit 65-127-Versionen zwei Seiten im Index aufweisen, beide Seiten jedoch Inline sind.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Anforderungsparameter

Name     | In     | type    | Erforderlich | Notizen
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | ja      | Die Paket-ID, Kleinbuchstaben

Der `LOWER_ID` Wert ist die gewünschte Paket-ID in Kleinbuchstaben unter Verwendung der Regeln, die von implementiert werden. NET- [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Methode.

### <a name="response"></a>Antwort

Die Antwort ist ein JSON-Dokument, das ein Root-Objekt mit den folgenden Eigenschaften enthält:

Name  | type             | Erforderlich | Notizen
----- | ---------------- | -------- | -----
count | integer          | ja      | Die Anzahl der Registrierungsseiten im Index.
items | Array von Objekten | ja      | Das Array der Registrierungsseiten

Jedes Element im Array des Index Objekts `items` ist ein JSON-Objekt, das eine Registrierungsseite darstellt.

#### <a name="registration-page-object"></a>Objekt der Registrierungsseite

Das Registrierungsseiten Objekt im Registrierungs Index verfügt über die folgenden Eigenschaften:

Name   | type             | Erforderlich | Notizen
------ | ---------------- | -------- | -----
@id    | string           | ja      | Die URL zur Registrierungsseite.
count  | integer          | ja      | Die Anzahl der Registrierungs Blätter auf der Seite.
items  | Array von Objekten | nein       | Das Array der Registrierungs Blätter und ihre zugehörigen Metadaten.
lower  | string           | ja      | Die niedrigste semver 2.0.0-Version auf der Seite (einschließlich)
parent | Zeichenfolge           | nein       | Die URL zum Registrierungs Index.
upper  | string           | ja      | Die höchste semver 2.0.0-Version auf der Seite (einschließlich)

Die `lower` `upper` Begrenzungen und des Page-Objekts sind nützlich, wenn die Metadaten für eine bestimmte Seiten Version benötigt werden.
Diese Begrenzungen können verwendet werden, um die einzige erforderliche Registrierungsseite abzurufen. Die Versions [Zeichenfolgen entsprechen den Versions Regeln von nuget](../concepts/package-versioning.md). Die Versions Zeichenfolgen werden normalisiert und enthalten keine buildmetadaten. Wie bei allen Versionen im nuget-Ökosystem wird der Vergleich der Versions [Zeichenfolgen mit den Versions Rang Folge Regeln von semver 2.0.0](https://semver.org/spec/v2.0.0.html#spec-item-11)implementiert.

Die- `parent` Eigenschaft wird nur angezeigt, wenn das Registrierungsseiten Objekt über die- `items` Eigenschaft verfügt.

Wenn die `items` Eigenschaft nicht im Registrierungsseiten Objekt vorhanden ist, muss die in angegebene URL `@id` zum Abrufen von Metadaten zu einzelnen Paketversionen verwendet werden. Das `items` Array wird manchmal als Optimierung vom Seiten Objekt ausgeschlossen. Wenn die Anzahl der Versionen einer einzelnen Paket-ID sehr groß ist, ist das Registrierungs Index Dokument sehr groß und verschwendet für einen Client, der nur eine bestimmte Version oder einen kleinen Bereich von Versionen kümmert, zu verarbeiten.

Beachten Sie, dass `items` die-Eigenschaft nicht verwendet werden muss, wenn die-Eigenschaft vorhanden ist, `@id` da alle Seiten Daten bereits in der- `items` Eigenschaft Inline sind.

Jedes Element im Array des Page-Objekts `items` ist ein JSON-Objekt, das ein Registrierungs Blatt und zugehörige Metadaten darstellt.

#### <a name="registration-leaf-object-in-a-page"></a>Registrierungs Blatt Objekt in einer Seite

Das Registrierungs Blatt Objekt auf einer Registrierungsseite verfügt über die folgenden Eigenschaften:

Name           | type   | Erforderlich | Notizen
-------------- | ------ | -------- | -----
@id            | string | ja      | Die URL zum Registrierungs Blatt.
catalogentry   | Objekt | ja      | Der Katalogeintrag, der die Paket Metadaten enthält.
packagecontent | string | ja      | Die URL zum Paket Inhalt (. nupkg).

Jedes Registrierungs Blatt Objekt stellt Daten dar, die einer einzelnen Paketversion zugeordnet sind.

#### <a name="catalog-entry"></a>Katalogeintrag

Die- `catalogEntry` Eigenschaft im Blatt "Registrierung" verfügt über die folgenden Eigenschaften:

Name                     | type                       | Erforderlich | Notizen
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | ja      | Die URL des Dokuments, das zum entwickeln dieses Objekts verwendet wird.
authors                  | Zeichenfolge oder Array von Zeichenfolgen | nein       | 
dependencygroups         | Array von Objekten           | nein       | Die Abhängigkeiten des Pakets, gruppiert nach Ziel Framework
veraltungs              | Objekt                     | nein       | Die dem Paket zugeordnete Veraltung
description              | Zeichenfolge                     | nein       | 
iconUrl                  | Zeichenfolge                     | nein       | 
id                       | Zeichenfolge                     | ja      | Die ID des Pakets.
licenseUrl               | Zeichenfolge                     | nein       |
licensexpression        | Zeichenfolge                     | nein       | 
Liste                   | boolean                    | nein       | Sollte als "aufgelistet" betrachtet werden, wenn nicht vorhanden
minClientVersion         | Zeichenfolge                     | nein       | 
projectUrl               | Zeichenfolge                     | nein       | 
published                | Zeichenfolge                     | nein       | Eine Zeichenfolge, die den ISO 8601-Zeitstempel der Veröffentlichung des Pakets enthält.
requireLicenseAcceptance | boolean                    | nein       | 
Zusammenfassung                  | Zeichenfolge                     | nein       | 
tags                     | Zeichenfolge oder Zeichen folgen Array  | nein       | 
title                    | Zeichenfolge                     | nein       | 
version                  | Zeichenfolge                     | ja      | Die vollständige Versions Zeichenfolge nach der Normalisierung

Die Paket `version` Eigenschaft ist die vollständige Versions Zeichenfolge nach der Normalisierung. Dies bedeutet, dass die Build-Daten von semver 2.0.0 hier eingefügt werden können.

Die- `dependencyGroups` Eigenschaft ist ein Array von-Objekten, die die Abhängigkeiten des Pakets nach Ziel Framework gruppiert darstellen. Wenn das Paket keine Abhängigkeiten aufweist, fehlt die- `dependencyGroups` Eigenschaft, ein leeres Array, oder die- `dependencies` Eigenschaft aller Gruppen ist leer oder fehlt.

Der Wert der- `licenseExpression` Eigenschaft entspricht der [Syntax für den nuget-Lizenz Ausdruck](../reference/nuspec.md#license).

> [!Note]
> Auf nuget.org wird der `published` Wert auf Jahr 1900 festgelegt, wenn das Paket nicht aufgelistet ist.

#### <a name="package-dependency-group"></a>Paket Abhängigkeits Gruppe

Jedes Abhängigkeits Gruppen Objekt verfügt über die folgenden Eigenschaften:

Name            | type             | Erforderlich | Notizen
--------------- | ---------------- | -------- | -----
targetFramework | Zeichenfolge           | nein       | Das Ziel Framework, auf das diese Abhängigkeiten anwendbar sind
Abhängigkeiten    | Array von Objekten | nein       |

Die `targetFramework` Zeichenfolge verwendet das Format, das von der .NET-Bibliothek [nuget. Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/)von nuget implementiert wird. Wenn kein `targetFramework` angegeben ist, gilt die Abhängigkeits Gruppe für alle Ziel-Frameworks.

Die- `dependencies` Eigenschaft ist ein Array von-Objekten, die jeweils eine Paketabhängigkeit des aktuellen Pakets darstellen.

#### <a name="package-dependency"></a>Paketabhängigkeit

Jede Paketabhängigkeit verfügt über die folgenden Eigenschaften:

Name         | type   | Erforderlich | Notizen
------------ | ------ | -------- | -----
id           | Zeichenfolge | ja      | Die ID der Paketabhängigkeit.
range        | Objekt | nein       | Der zulässige [Versions Bereich](../concepts/package-versioning.md#version-ranges) der Abhängigkeit.
Registrierung | Zeichenfolge | nein       | Die URL zum Registrierungs Index für diese Abhängigkeit.

Wenn die `range` Eigenschaft ausgeschlossen oder eine leere Zeichenfolge ist, sollte der Client standardmäßig den Versions Bereich haben `(, )` . Das heißt, jede Version der Abhängigkeit ist zulässig. Der Wert von `*` ist für die Eigenschaft nicht zulässig `range` .

#### <a name="package-deprecation"></a>Veraltetes Paket

Jedes Paket ist veraltet und verfügt über die folgenden Eigenschaften:

Name             | type             | Erforderlich | Notizen
---------------- | ---------------- | -------- | -----
rechtlichen          | array of strings | ja      | Die Gründe, aus denen das Paket veraltet ist
message          | Zeichenfolge           | nein       | Weitere Details zu dieser Veraltung
Alternative ACKAGE | Objekt           | nein       | Das alternative Paket, das stattdessen verwendet werden soll.

Die `reasons` -Eigenschaft muss mindestens eine Zeichenfolge enthalten und sollte nur Zeichen folgen aus der folgenden Tabelle enthalten:

`Reason`       | BESCHREIBUNG             
------------ | -----------
Alt       | Das Paket wird nicht mehr verwaltet.
Criticalbugs | Das Paket weist Fehler auf, die für die Verwendung ungeeignet sind.
Andere        | Das Paket ist aufgrund eines Grunds, der nicht in dieser Liste enthalten ist, veraltet.

Wenn die Eigenschaft Zeichen folgen enthält, die `reasons` nicht aus dem bekannten Satz stammen, sollten Sie ignoriert werden. Bei den Zeichen folgen wird die Groß-/Kleinschreibung nicht beachtet, sollte daher genauso `legacy` behandelt werden wie `Legacy` . Es gibt keine Sortier Einschränkung für das Array, sodass die Zeichen folgen in beliebiger Reihenfolge angeordnet werden können. Wenn die Eigenschaft außerdem nur Zeichen folgen enthält, die nicht aus der bekannten Menge stammen, sollte Sie so behandelt werden, als ob Sie nur die "andere" Zeichenfolge enthielt.

#### <a name="alternate-package"></a>Alternatives Paket

Das alternative Paket Objekt verfügt über die folgenden Eigenschaften:

Name         | type   | Erforderlich | Notizen
------------ | ------ | -------- | -----
id           | Zeichenfolge | ja      | Die ID des alternativen Pakets
range        | Objekt | nein       | Der zulässige [Versions Bereich](../concepts/package-versioning.md#version-ranges)oder, `*` Wenn eine beliebige Version zulässig ist.

### <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Beispiel für eine Antwort

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

In diesem speziellen Fall hat der Registrierungs Index die Registrierungsseite Inline, sodass keine zusätzlichen Anforderungen zum Abrufen von Metadaten zu einzelnen Paketversionen erforderlich sind.

## <a name="registration-page"></a>Registrierungsseite

Die Registrierungsseite enthält Registrierungs Blätter. Die URL zum Abrufen einer Registrierungsseite wird von der- `@id` Eigenschaft im oben erwähnten [Registrierungsseiten Objekt](#registration-page-object) bestimmt. Die URL ist nicht als vorhersagbar gedacht und sollte immer mithilfe des Index Dokuments erkannt werden.

> [!Warning]
> Auf nuget.org enthält die URL für das Dokument der Registrierungsseite zufälligerweise die untere und obere Grenze der Seite. Diese Annahme sollte jedoch nie von einem Client vorgenommen werden, da Server Implementierungen die Form der URL ändern können, solange das Index Dokument über einen gültigen Link verfügt.

Wenn das `items` Array nicht im Registrierungs Index bereitgestellt wird, gibt eine HTTP GET-Anforderung des `@id` Werts ein JSON-Dokument zurück, das ein Objekt als Stamm hat. Das Objekt hat die folgenden Eigenschaften:

Name   | type             | Erforderlich | Notizen
------ | ---------------- | -------- | -----
@id    | string           | ja      | Die URL zur Registrierungsseite.
count  | integer          | ja      | Die Anzahl der Registrierungs Blätter auf der Seite.
items  | Array von Objekten | ja      | Das Array der Registrierungs Blätter und ihre zugehörigen Metadaten.
lower  | string           | ja      | Die niedrigste semver 2.0.0-Version auf der Seite (einschließlich)
parent | string           | ja      | Die URL zum Registrierungs Index.
upper  | string           | ja      | Die höchste semver 2.0.0-Version auf der Seite (einschließlich)

Die Form der Registrierungs Blattobjekte ist die gleiche wie im [obigen](#registration-leaf-object-in-a-page)Registrierungs Index.

## <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Beispiel für eine Antwort

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Registrierungs Blatt

Das Blatt Registrierung enthält Informationen über eine bestimmte Paket-ID und-Version. Die Metadaten für die jeweilige Version sind möglicherweise in diesem Dokument nicht verfügbar. Paket Metadaten sollten aus dem [Registrierungs Index](#registration-index) oder der [Registrierungsseite](#registration-page) abgerufen werden (wird mit dem Registrierungs Index ermittelt).

Die URL zum Abrufen eines Registrierungs Blatts wird aus der- `@id` Eigenschaft eines Registrierungs Blatt Objekts entweder in einem Registrierungs Index oder auf einer Registrierungsseite abgerufen. Wie beim Seiten Dokument. die URL ist nicht als vorhersagbar gedacht und sollte immer mithilfe des Registrierungsseiten Objekts ermittelt werden.

> [!Warning]
> Auf nuget.org enthält die URL für das Registrierungs Blatt Dokument zufälligerweise die Paketversion. Diese Annahme sollte jedoch nie von einem Client vorgenommen werden, da Server Implementierungen die Form der URL ändern können, solange das übergeordnete Dokument über einen gültigen Link verfügt. 

Das Registrierungs Blatt ist ein JSON-Dokument mit einem Root-Objekt mit den folgenden Eigenschaften:

Name           | type    | Erforderlich | Notizen
-------------- | ------- | -------- | -----
@id            | string  | ja      | Die URL zum Registrierungs Blatt.
catalogentry   | Zeichenfolge  | nein       | Die URL zum Katalogeintrag, der dieses Blatt erzeugt hat.
Liste         | boolean | nein       | Sollte als "aufgelistet" betrachtet werden, wenn nicht vorhanden
packagecontent | Zeichenfolge  | nein       | Die URL zum Paket Inhalt (. nupkg).
published      | Zeichenfolge  | nein       | Eine Zeichenfolge, die den ISO 8601-Zeitstempel der Veröffentlichung des Pakets enthält.
Registrierung   | Zeichenfolge  | nein       | Die URL zum Registrierungs Index.

> [!Note]
> Auf nuget.org wird der `published` Wert auf Jahr 1900 festgelegt, wenn das Paket nicht aufgelistet ist.

### <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Beispiel für eine Antwort

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
