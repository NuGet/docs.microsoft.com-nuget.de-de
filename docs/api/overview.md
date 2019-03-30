---
title: Übersicht über die NuGet-API
description: Die NuGet-API ist eine Reihe von HTTP-Endpunkten, die zum Herunterladen von Paketen, Abrufen von Metadaten, Veröffentlichen von neuen Paketen usw. verwendet werden kann.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: bb15b4decef104f1aefe37fd18f3358181a848af
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/29/2019
ms.locfileid: "58637661"
---
# <a name="nuget-api"></a>NuGet-API

Die NuGet-API ist eine Reihe von HTTP-Endpunkten, die dazu genutzt werden kann, Pakete herunterzuladen, Metadaten abzurufen, neue Pakete zu veröffentlichen und die meisten anderen Vorgänge durchzuführen, die in den offiziellen NuGet-Clients verfügbar sind.

Diese API wird vom NuGet-Client in Visual Studio, nuget.exe und der .NET-CLI verwendet, um NuGet-Vorgänge auszuführen, z.B. [`dotnet restore`](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), Suche in der Visual Studio-UI und [`nuget.exe push`](../tools/cli-ref-push.md).

Beachten Sie, dass "nuget.org" in einigen Fällen zusätzliche Anforderungen besitzt, die nicht von anderen Paketquellen erzwungen werden. Diese Unterschiede sind in den [nuget.org-Protokollen](nuget-protocols.md) dokumentiert.

Für die einfache Enumeration und zum Herunterladen der verfügbaren nuget.exe-Versionen wird der [tools.json](tools-json.md)-Endpunkt verwendet.

## <a name="service-index"></a>Dienstindex

Der Einstiegspunkt für die API ist ein JSON-Dokument an einem bekannten Speicherort. Dieses Dokument heißt **Dienstindex**. Der Speicherort des Dienstindex für nuget.org lautet `https://api.nuget.org/v3/index.json`.

Dieses JSON-Dokument enthält eine Liste an *Ressourcen*, die verschiedene Funktionalitäten bereitstellen und verschiedene Anwendungsfälle erfüllen.

Clients, die die API unterstützen, sollten eine oder mehrere dieser Dienstindex-URLs akzeptieren. Diese URLs werden benutzt, um sich mit den verschiedenen Paketquellen zu verbinden.

Weitere Informationen zum Dienstindex finden Sie in [der zugehörigen API-Referenz](service-index.md).

## <a name="versioning"></a>Versionskontrolle

Die API ist Version 3 des NuGet HTTP-Protokolls. Dieses Protokoll wird manchmal als "API V3" bezeichnet. Diese Referenzdokumentation nennt diese Version des Protokolls einfach "die API".

Die Schemaversion des Dienstindex wird von der `version`-Eigenschaft im Dienstindex angegeben. Die API erfordert, dass die version-Zeichenfolge die Hautpversionsnummer `3` hat. Wenn API-kompatible Änderungen am Schema des Dienstindex durchgeführt werden, wird die Nebenversion der version-Zeichenfolge erhöht.

Ältere Clients (z. B. nuget.exe 2.x) unterstützen die V3-API nicht und unterstützen nur die ältere V2-API, die hier nicht dokumentiert ist.

Die NuGet-V3-API wird so genannt, weil sie der Nachfolger der V2-API ist. Die V2-API war ein OData-basiertes Protokoll, das durch die 2.x-Version des offiziellen NuGet-Clients implementiert wurde. Die V3-API wurde zuerst durch die Version 3.0 des offiziellen NuGet-Clients unterstützt und ist weiterhin die neueste MAJOR-Protokollversion, die durch den NuGet-Client unterstützt wird. 

Geschütztes Protokoll an die API wurde geändert, da es veröffentlicht wurde.

## <a name="resources-and-schema"></a>Ressourcen und schema

Die **dienstindex** beschreibt eine Reihe von Ressourcen. Der aktuelle Satz von unterstützten Ressourcen lauten wie folgt aus:

Ressourcenname                                                        | Erforderlich | Beschreibung
-------------------------------------------------------------------- | -------- | -----------
[Katalog](catalog-resource.md)                                       | Nein       | Vollständigen Datensatz aller Ereignisse für Paket.
[PackageBaseAddress](package-base-address-resource.md)               | ja      | Paketinhalt (NUPKG) zu erhalten.
[PackageDetailsUriTemplate](package-details-template-resource.md)    | Nein       | Erstellen Sie eine URL für den Zugriff auf eine Webseite des Paket-Details.
[PackagePublish](package-publish-resource.md)                        | ja      | Mithilfe von Push übertragen und löschen (oder aus der Liste entfernen) Pakete.
[RegistrationsBaseUrl](registration-base-url-resource.md)            | ja      | Abrufen von Metadaten von Paketen.
[ReportAbuseUriTemplate](report-abuse-resource.md)                   | Nein       | Erstellen Sie eine URL für den Zugriff auf eine Webseite des Bericht-Missbrauch.
[RepositorySignatures](repository-signatures-resource.md)            | Nein       | Abrufen von Zertifikaten, die zum Signieren von Repository verwendet.
[SearchAutocompleteService](search-autocomplete-service-resource.md) | Nein       | Entdecken Sie die Paket-IDs und Versionen von Teilzeichenfolge.
[SearchQueryService](search-query-service-resource.md)               | ja      | Filtern und Pakete nach Schlüsselwort suchen.
[SymbolPackagePublish](symbol-package-publish-resource.md)           | Nein       | Push-Symbolpaketen an.

Im Allgemeinen werden alle nicht binären Daten zurückgegeben, die von einer API-Ressource mit JSON serialisiert. Das Antwortschema von jeder Ressource im dienstindex zurückgegeben wird einzeln für diese Ressource definiert. Weitere Informationen zu jeder Ressource finden Sie unter den oben aufgeführten Themen.

Der Weiterentwicklung des Protokolls, möglicherweise in Zukunft neue Eigenschaften zu JSON-Antworten hinzugefügt werden. Der Client zukunftssicher ist sollte die Implementierung nicht ausgegangen, dass das Antwortschema endgültig ist und kann nicht die zusätzliche Daten enthalten. Alle Eigenschaften, die die Implementierung nicht interpretieren kann ignoriert werden sollen.

> [!Note]
> Wenn eine Datenquelle den `SearchAutocompleteService` nicht implementiert, sollte das Auto-Vervollständigungs-Verfahren kontrolliert deaktiviert werden. Wenn `ReportAbuseUriTemplate` nicht implementiert wird, fällt der offizielle NuGet-Client auf die "Missbrauch melden"-URL von nuget.org zurück (zu verfolgen in [NuGet/Home#4924](https://github.com/NuGet/Home/issues/4924)). Andere Clients können sich dazu entscheiden, einfach keine solche URL anzuzeigen.

### <a name="undocumented-resources-on-nugetorg"></a>Nicht dokumentierte Ressourcen auf nuget.org

Dienstindex auf nuget.org V3 verfügt über einige Ressourcen, die oben nicht dokumentiert sind. Es gibt einige Gründe für die Dokumentierung nicht auf einer Ressourcensatzes.

Wir dokumentieren nicht zuerst als Implementierungsdetail beibehalten von nuget.org verwendete Ressourcen. Die `SearchGalleryQueryService` in diese Kategorie fällt. [NuGetGallery](https://github.com/NuGet/NuGetGallery) verwendet diese Ressource, delegieren einige V2 (OData) Abfragen in unserer Search-Index mit der Datenbank. Diese Ressource wurde aus Gründen der Skalierbarkeit eingeführt und ist nicht für die externe Verwendung vorgesehen.

Zweitens, nicht wir Ressourcen dokumentieren, die in der RTM-Version von der offiziellen Client nie ausgeliefert wurden.
`PackageDisplayMetadataUriTemplate` und `PackageVersionDisplayMetadataUriTemplate` fallen in diese Kategorie.

Drittens nicht wir dokumentieren Sie Ressourcen, die eng gekoppelt mit dem V2-Protokoll, die wiederum ist absichtlich nicht dokumentiert. Die `LegacyGallery` Ressource in diese Kategorie fällt. Diese Ressource ermöglicht eine V3-dienstindex, um auf eine entsprechende V2-Quell-URL zu verweisen. Diese Ressource unterstützt die `nuget.exe list`.

Wenn eine Ressource hier nicht dokumentiert ist es *stark* wird empfohlen, dass Sie nicht über eine Abhängigkeit auf diesen führen. Wir können entfernen oder ändern das Verhalten der folgenden nicht dokumentierten Ressourcen, die Ihre Implementierung auf unerwartete Weise unterbrechen kann.

## <a name="timestamps"></a>Timestamps

Alle Zeitstempel, die von der API zurückgegeben werden, sind in UTC oder werden in der [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)-Repräsentation angegeben. 

## <a name="http-methods"></a>HTTP-Methoden

Verb   | Mit
------ | -----------
GET    | Führt eine Nur-Lesen-Operation aus, meistens ein Abruf von Daten.
HEAD   | Ruft die Antwortheader für die zusammenhängende `GET`-Anfrage ab.
PUT    | Erstellt eine Ressource, die nicht vorhanden ist, oder aktualisiert sie, wenn sie bereits existiert. Einige Ressourcen unterstützen Aktualisierungen vielleicht nicht.
DELETE | Löscht eine Ressource oder entfernt sie aus der Liste.

## <a name="http-status-codes"></a>HTTP-Statuscodes

Code | Beschreibung
---- | -----
200  | Erfolg, es gibt einen Antworttext.
201  | Erfolg, die Ressource wurde erstellt.
202  | Erfolg, die Anfrage wurde akzeptiert, aber einige Arbeiten sind vielleicht noch unvollständig und werden asynchron durchgeführt.
204  | Erfolg, es gibt aber keinen Antworttext.
301  | Eine permanente Umleitung.
302  | Eine temporäre Umleitung.
400  | Die Parameter in der URL oder im Anfragetext sind ungültig.
401  | Die angegebenen Anmeldeinformationen sind ungültig.
403  | Die Aktion ist mit den angegebenen Anmeldeinformationen nicht zulässig.
404  | Die angeforderte Ressource ist nicht vorhanden.
409  | Die Anforderung steht in Konflikt mit einer vorhandenen Ressource.
500  | Der Dienst hat einen unerwarteten Fehler festgestellt.
503  | Der Dienst ist vorübergehend nicht verfügbar.

Jede `GET`-Anforderung an einen API-Endpunkt kann eine HTTP-Umleitung (301 oder 302) zurückgeben. Clients sollten diesen Umleitungen anstandslos folgen, indem sie den `Location`-Header berücksichtigen und eine entsprechende `GET`-Anforderung ausstellen. Die Dokumentation der einzelnen Endpunkte gibt genau nicht an, wo Umleitungen benutzt werden können.

Im Fall eines Statuscodes in der Region 500 kann der Client einen angemessenen Wiederholungsmechanismus implementieren. Der offizielle NuGet-Client führt drei Wiederholungen durch, wenn er einen Statuscode in der Region 500 oder einen TCP-/DNS-Fehler antrifft.

## <a name="http-request-headers"></a>HTTP-Anforderungsheader

name                     | Beschreibung
------------------------ | -----------
X-NuGet-ApiKey           | Erforderlich für Push und Löschen, siehe [ `PackagePublish` -Ressource](package-publish-resource.md)
X-NuGet-Client-Version   | **Veraltet** und durch `X-NuGet-Protocol-Version` ersetzt
X-NuGet-Protocol-Version | Auf nuget.org nur in bestimmten Fällen erforderlich, siehe [Protokolle auf nuget.org](NuGet-Protocols.md)
X-NuGet-Session-Id       | *Optional*. NuGet-Clients mit Version 4.7 oder höher identifizieren HTTP-Anfragen, die Teil der gleichen Client-Sitzung sind.

Die `X-NuGet-Session-Id` hat einen einzigen Wert für alle Vorgänge im Zusammenhang mit einer einzigen Wiederherstellung an `PackageReference`. Für andere Szenarios wie AutoVervollständigen und `packages.config` Wiederherstellung möglicherweise gibt es mehrere andere Sitzung IDs aufgrund wie der Code berücksichtigt wurden.

## <a name="authentication"></a>Authentifizierung

Die Authentifizierung wird der Implementation der Paketquelle überlassen, die definiert werden soll. Bei nuget.org erfordert nur die `PackagePublish`-Ressource Authentifizierung durch einen speziellen API-Schlüsselheader. Details sind in der [`PackagePublish`-Ressource](package-publish-resource.md) definiert.
