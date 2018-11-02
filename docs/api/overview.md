---
title: Übersicht über die NuGet-API
description: Die NuGet-API ist eine Reihe von HTTP-Endpunkten, die zum Herunterladen von Paketen, Abrufen von Metadaten, Veröffentlichen von neuen Paketen usw. verwendet werden kann.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 770173d6b84048cf42a5da46cbc474d8cf604a08
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547502"
---
# <a name="nuget-api"></a>NuGet-API

Die NuGet-API ist eine Reihe von HTTP-Endpunkten, die dazu genutzt werden kann, Pakete herunterzuladen, Metadaten abzurufen, neue Pakete zu veröffentlichen und die meisten anderen Vorgänge durchzuführen, die in den offiziellen NuGet-Clients verfügbar sind.

Diese API wird vom NuGet-Client in Visual Studio, nuget.exe und der .NET CLI verwendet, um NuGet-Vorgänge auszuführen, z. B. [ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore), Suche in der Visual Studio-UI und [ `nuget.exe push` ](../tools/cli-ref-push.md).

Beachte, dass "nuget.org" in einigen Fällen zusätzliche Anforderungen hat, die nicht von anderen Paketquellen erzwungen werden. Diese Unterschiede sind in den [nuget.org-Protokollen](nuget-protocols.md) dokumentiert.

Für einfache Enumeration und Herunterladen der verfügbaren nuget.exe-Versionen wird der [tools.json](tools-json.md)-Endpunkt verwendet.

## <a name="service-index"></a>Dienstindex

Der Einstiegspunkt für die API ist ein JSON-Dokument an einem bekannten Speicherort. Dieses Dokument heißt **Dienstindex**. Der Speicherort des Dienstindex für nuget.org lautet `https://api.nuget.org/v3/index.json`.

Dieses JSON-Dokument enthält eine Liste an *Ressourcen*, die verschiedene Funktionalitäten bereitstellen und verschiedene Anwendungsfälle erfüllen.

Clients, die die API unterstützen, sollten eine oder mehrere dieser Dienstindex-URLs akzeptieren. Diese URLs werden benutzt, um sich mit den verschiedenen Paketquellen zu verbinden.

Weitere Informationen zum Dienstindex findest Du in [der zugehörigen API-Referenz](service-index.md).

## <a name="versioning"></a>Versionskontrolle

Die API ist Version 3 des NuGet HTTP-Protokolls. Dieses Protokoll wird manchmal als "V3-API" bezeichnet. Diese Referenzdokumentation nennt diese Version des Protokolls einfach "die API".

Die Schemaversion des Dienstindex wird in der `version`-Eigenschaft im Dienstindex angegeben. Die API erfordert, dass der Version-String eine MAJOR-Versionsnummer von `3` hat. Wenn API-kompatible Änderungen am Schema des Dienstindex durchgeführt werden, wird die MINOR-Version im Version-String erhöht.

Ältere Clients (z. B. nuget.exe 2.x) unterstützen die V3-API nicht und unterstützen nur die ältere V2-API, die hier nicht dokumentiert ist.

Die NuGet-V3-API wird so genannt, weil sie der Nachfolger der V2-API ist. Die V2-API war ein OData-basiertes Protokoll, das durch die 2.x-Version des offiziellen NuGet-Clients implementiert wurde. Die V3-API wurde zuerst durch die Version 3.0 des offiziellen NuGet-Clients unterstützt und ist weiterhin die neueste MAJOR-Protokollversion, die durch den NuGet-Client unterstützt wird.

Seit dem ersten Release wurden bereits kompatible Änderungen am Protokoll der API durchgeführt.

## <a name="resources-and-schema"></a>Ressourcen und Schema

Der **Dienstindex** beschreibt eine Reihe von Ressourcen. Die aktuell unterstützten Ressourcen sind folgende:

Ressourcenname                                                         | Erforderlich | Beschreibung
---------------------------------------------------------------------- | ------------ | ------------
[`PackagePublish`](package-publish-resource.md)                        | ja           | Pakete veröffentlichen, löschen oder aus der Liste entfernen.
[`SearchQueryService`](search-query-service-resource.md)               | ja           | Pakete mittels einem Schlüsselwort durchsuchen oder filtern.
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | ja           | Abrufen von Metadaten von Paketen.
[`PackageBaseAddress`](package-base-address-resource.md)               | ja           | Paketinhalt (.nupkg) anfordern.
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | nein         | Paket-IDs und -Versionen anhand eines Teilstrings entdecken.
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | nein         | Eine URL zum Zugriff auf eine "Missbrauch melden"-Seite konstruieren.
[`RepositorySignatures`](repository-signatures-resource.md)            | nein         | Abrufen von Zertifikaten, die für Paketquellen-Signierung verwendet werden.
[`Catalog`](catalog-resource.md)                                       | nein         | Vollständiges Protokoll aller Paket-Ereignisse.

Im Allgemeinen werden alle nicht binären Daten, die von einer API-Ressource zurückgegeben werden, mit JSON serialisiert. Das Antwortschema, das eine bestimmte Ressource zurückgibt, wird einzeln für diese Ressource definiert. Weitere Informationen zu den einzelnen Ressourcen findest Du unter den oben aufgeführten Themen.

> [!Note]
> Wenn eine Datenquelle den `SearchAutocompleteService` nicht implementiert, sollte das Auto-Vervollständigungs-Verfahren kontrolliert deaktiviert werden. Wenn `ReportAbuseUriTemplate` nicht implementiert wird, fällt der offizielle NuGet-Client auf die "Missbrauch melden"-URL von nuget.org zurück (zu verfolgen in [NuGet/Home#4924](https://github.com/NuGet/Home/issues/4924)). Andere Clients können sich dazu entscheiden, einfach keine solche URL anzuzeigen.

## <a name="timestamps"></a>Timestamps

Alle Timestamps, die von der API zurückgegeben werden, sind in UTC oder werden in der [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)-Repräsentation angegeben.

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

Jede `GET`-Anforderung an einen API-Endpunkt kann eine HTTP-Umleitung (301 oder 302) zurückgeben. Clients sollten diesen Umleitungen sauber folgen, in dem sie den `Location`-Header lesen und eine entsprechende `GET`-Anforderung abgeben. Die Dokumentation der einzelnen Endpunkte gibt nicht an, wo Umleitungen benutzt werden können.

Im Fall eines Statuscodes in der Region 500 kann der Client einen angemessenen Wiederholungsmechanismus implementieren. Der offizielle NuGet-Client führt drei Wiederholungen durch, wenn er einen Statuscode in der Region 500 oder einen TCP-/DNS-Fehler antrifft.

## <a name="http-request-headers"></a>HTTP-Anforderungsheader

name                     | Beschreibung
------------------------ | ------------
X-NuGet-ApiKey           | Erforderlich für Push und Löschen, siehe [`PackagePublish`-Ressource](package-publish-resource.md)
X-NuGet-Client-Version   | **Veraltet** und durch `X-NuGet-Protocol-Version` ersetzt
X-NuGet-Protocol-Version | Auf nuget.org nur in bestimmten Fällen erforderlich, siehe [Protokolle auf nuget.org](NuGet-Protocols.md)
X-NuGet-Session-Id      | *Optional*. NuGet-Clients mit Version 4.7 oder höher identifizieren HTTP-Anfragen, die Teil der gleichen Client-Sitzung sind. Für `PackageReference`-Wiederherstellungsoperationen gibt es eine einzelne Sitzungs-ID; für andere Szenarien wie Autovervollständigung und Wiederherstellung von `packages.config` können mehrere verschiedene Sitzungs-IDs existieren. Dies hängt mit der Programmierung des Clients zusammen.

## <a name="authentication"></a>Authentifizierung

Authentifizierung wird der Implementation der Paketquelle überlassen. Bei nuget.org erfordert nur die `PackagePublish`-Ressource Authentifizierung durch einen speziellen API-Key-Header. Details sind in der [`PackagePublish`-Ressource](package-publish-resource.md) definiert.
