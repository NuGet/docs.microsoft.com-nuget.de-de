---
title: Übersicht über die nuget-Server-API
description: Die nuget-Server-API ist eine Reihe von HTTP-Endpunkten, die zum Herunterladen von Paketen, zum Abrufen von Metadaten, zum Veröffentlichen neuer Pakete usw. verwendet werden können.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: aacf56a5dc5af9abf6f60d42bc7fd530a128d0d8
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419835"
---
# <a name="nuget-server-api"></a>Nuget-Server-API

Bei der nuget-Server-API handelt es sich um einen Satz von HTTP-Endpunkten, die zum Herunterladen von Paketen, zum Abrufen von Metadaten, zum Veröffentlichen neuer Pakete und zum Ausführen der meisten anderen in den offiziellen nuget-Clients verfügbaren Vorgänge

Diese API wird vom NuGet-Client in Visual Studio, nuget.exe und der .NET-CLI verwendet, um NuGet-Vorgänge auszuführen, z.B. [`dotnet restore`](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), Suche in der Visual Studio-UI und [`nuget.exe push`](../reference/cli-reference/cli-ref-push.md).

Beachten Sie, dass "nuget.org" in einigen Fällen zusätzliche Anforderungen besitzt, die nicht von anderen Paketquellen erzwungen werden. Diese Unterschiede sind in den [nuget.org-Protokollen](nuget-protocols.md) dokumentiert.

Für die einfache Enumeration und zum Herunterladen der verfügbaren nuget.exe-Versionen wird der [tools.json](tools-json.md)-Endpunkt verwendet.

## <a name="service-index"></a>Dienstindex

Der Einstiegspunkt für die API ist ein JSON-Dokument an einem bekannten Speicherort. Dieses Dokument heißt **Dienstindex**. Der Speicherort des Dienstindex für nuget.org lautet `https://api.nuget.org/v3/index.json`.

Dieses JSON-Dokument enthält eine Liste an *Ressourcen*, die verschiedene Funktionalitäten bereitstellen und verschiedene Anwendungsfälle erfüllen.

Clients, die die API unterstützen, sollten eine oder mehrere dieser Dienstindex-URLs akzeptieren. Diese URLs werden benutzt, um sich mit den verschiedenen Paketquellen zu verbinden.

Weitere Informationen zum Dienstindex finden Sie in [der zugehörigen API-Referenz](service-index.md).

## <a name="versioning"></a>Versionskontrolle

Die API ist Version 3 des NuGet HTTP-Protokolls. Dieses Protokoll wird manchmal als "v3-API" bezeichnet. Diese Referenzdokumentation nennt diese Version des Protokolls einfach "die API".

Die Schemaversion des Dienstindex wird von der `version`-Eigenschaft im Dienstindex angegeben. Die API erfordert, dass die version-Zeichenfolge die Hautpversionsnummer `3` hat. Wenn API-kompatible Änderungen am Schema des Dienstindex durchgeführt werden, wird die Nebenversion der version-Zeichenfolge erhöht.

Ältere Clients (z. B. nuget.exe 2.x) unterstützen die V3-API nicht und unterstützen nur die ältere V2-API, die hier nicht dokumentiert ist.

Die NuGet-V3-API wird so genannt, weil sie der Nachfolger der V2-API ist. Die V2-API war ein OData-basiertes Protokoll, das durch die 2.x-Version des offiziellen NuGet-Clients implementiert wurde. Die V3-API wurde zuerst durch die Version 3.0 des offiziellen NuGet-Clients unterstützt und ist weiterhin die neueste MAJOR-Protokollversion, die durch den NuGet-Client unterstützt wird. 

An der API wurden seit der ersten Veröffentlichung nicht unterbrechende Protokoll Änderungen vorgenommen.

## <a name="resources-and-schema"></a>Ressourcen und Schema

Der **Dienst Index** beschreibt eine Vielzahl von Ressourcen. Der aktuelle Satz unterstützter Ressourcen lautet wie folgt:

Ressourcenname                                                        | Erforderlich | Beschreibung
-------------------------------------------------------------------- | -------- | -----------
[Katalog](catalog-resource.md)                                       | Nein       | Vollständiger Datensatz aller Paket Ereignisse.
[Packagebaseaddress](package-base-address-resource.md)               | ja      | Get Package Content (. nupkg).
[PackageDetailsUriTemplate](package-details-template-resource.md)    | Nein       | Erstellen Sie eine URL für den Zugriff auf die Webseite mit Paket Details.
[Packagepublish](package-publish-resource.md)                        | ja      | Pakete per Push und DELETE (oder Unlist).
[RegistrationsBaseUrl](registration-base-url-resource.md)            | ja      | Paket Metadaten erhalten.
[ReportAbuseUriTemplate](report-abuse-resource.md)                   | Nein       | Erstellen Sie eine URL für den Zugriff auf eine Website zum missbrauchen von Berichten.
[RepositorySignatures](repository-signatures-resource.md)            | Nein       | Zertifikate für die Repository-Signierung erhalten.
[SearchAutocompleteService](search-autocomplete-service-resource.md) | Nein       | Ermitteln der Paket-IDs und-Versionen nach Teil Zeichenfolge.
[SearchQueryService](search-query-service-resource.md)               | ja      | Filtern Sie nach und suchen Sie nach-Schlüsselwort.
[SymbolPackagePublish](symbol-package-publish-resource.md)           | Nein       | Push-Symbol Pakete.

Im Allgemeinen werden alle nicht binären Daten, die von einer API-Ressource zurückgegeben werden, mit JSON serialisiert. Das Antwort Schema, das von jeder Ressource im Dienst Index zurückgegeben wird, wird für diese Ressource einzeln definiert. Weitere Informationen zu den einzelnen Ressourcen finden Sie in den oben aufgeführten Themen.

In Zukunft können den JSON-Antworten neue Eigenschaften hinzugefügt werden, wenn das Protokoll weiterentwickelt wird. Damit der Client in Zukunft sicher ist, sollte die Implementierung nicht davon ausgehen, dass das Antwort Schema endgültig ist und keine zusätzlichen Daten enthalten kann. Alle Eigenschaften, die von der Implementierung nicht verstanden werden, sollten ignoriert werden.

> [!Note]
> Wenn eine Datenquelle den `SearchAutocompleteService` nicht implementiert, sollte das Auto-Vervollständigungs-Verfahren kontrolliert deaktiviert werden. Wenn `ReportAbuseUriTemplate` nicht implementiert wird, fällt der offizielle NuGet-Client auf die "Missbrauch melden"-URL von nuget.org zurück (zu verfolgen in [NuGet/Home#4924](https://github.com/NuGet/Home/issues/4924)). Andere Clients können sich dazu entscheiden, einfach keine solche URL anzuzeigen.

### <a name="undocumented-resources-on-nugetorg"></a>Nicht dokumentierte Ressourcen auf nuget.org

Der V3-Dienst Index in nuget.org verfügt über einige Ressourcen, die oben nicht dokumentiert sind. Es gibt einige Gründe, eine Ressource nicht zu dokumentieren.

Zunächst werden keine Ressourcen dokumentiert, die als Implementierungsdetail von nuget.org verwendet werden. Der `SearchGalleryQueryService` fällt in diese Kategorie. [Nugetgallery](https://github.com/NuGet/NuGetGallery) verwendet diese Ressource, um einige v2 (odata)-Abfragen an den Suchindex zu delegieren, anstatt die Datenbank zu verwenden. Diese Ressource wurde aus Gründen der Skalierbarkeit eingeführt und ist nicht für die externe Verwendung vorgesehen.

Zweitens werden keine Ressourcen dokumentiert, die nie in einer RTM-Version des offiziellen Clients ausgeliefert wurden.
`PackageDisplayMetadataUriTemplate`und `PackageVersionDisplayMetadataUriTemplate` fallen in diese Kategorie.

Drittens werden keine Ressourcen dokumentiert, die eng mit dem V2-Protokoll gekoppelt sind, das selbst absichtlich nicht dokumentiert ist. Die `LegacyGallery` Ressource fällt in diese Kategorie. Diese Ressource ermöglicht einem v3-Dienst Index, auf eine entsprechende v2-Quell-URL zu verweisen. Diese Ressource unterstützt `nuget.exe list`.

Wenn eine Ressource hier nicht dokumentiert ist, wird *dringend* empfohlen, dass Sie keine Abhängigkeit davon treffen. Wir können das Verhalten dieser nicht dokumentierten Ressourcen entfernen oder ändern, was die Implementierung auf unerwartete Weise unterbrechen könnte.

## <a name="timestamps"></a>Timestamps

Alle Zeitstempel, die von der API zurückgegeben werden, sind in UTC oder werden in der [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)-Repräsentation angegeben. 

## <a name="http-methods"></a>HTTP-Methoden

Ben   | Mit
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
401  | Die angegebenen Anmelde Informationen sind ungültig.
403  | Die Aktion ist mit den angegebenen Anmeldeinformationen nicht zulässig.
404  | Die angeforderte Ressource ist nicht vorhanden.
409  | Die Anforderung steht in Konflikt mit einer vorhandenen Ressource.
500  | Unerwarteter Fehler beim Dienst.
503  | Der Dienst ist vorübergehend nicht verfügbar.

Jede `GET`-Anforderung an einen API-Endpunkt kann eine HTTP-Umleitung (301 oder 302) zurückgeben. Clients sollten diesen Umleitungen anstandslos folgen, indem sie den `Location`-Header berücksichtigen und eine entsprechende `GET`-Anforderung ausstellen. Die Dokumentation der einzelnen Endpunkte gibt genau nicht an, wo Umleitungen benutzt werden können.

Im Fall eines Statuscodes in der Region 500 kann der Client einen angemessenen Wiederholungsmechanismus implementieren. Der offizielle NuGet-Client führt drei Wiederholungen durch, wenn er einen Statuscode in der Region 500 oder einen TCP-/DNS-Fehler antrifft.

## <a name="http-request-headers"></a>HTTP-Anforderungs Header

name                     | Beschreibung
------------------------ | -----------
X-NuGet-ApiKey           | Erforderlich für Push und Löschen, siehe [ `PackagePublish` -Ressource](package-publish-resource.md)
X-NuGet-Client-Version   | **Veraltet** und durch `X-NuGet-Protocol-Version` ersetzt
X-NuGet-Protocol-Version | Auf nuget.org nur in bestimmten Fällen erforderlich, siehe [Protokolle auf nuget.org](NuGet-Protocols.md)
X-NuGet-Session-Id       | *Optional*. NuGet-Clients mit Version 4.7 oder höher identifizieren HTTP-Anfragen, die Teil der gleichen Client-Sitzung sind.

Der `X-NuGet-Session-Id` verfügt über einen einzelnen Wert für alle Vorgänge, die sich auf eine `PackageReference`einzelne Wiederherstellung in beziehen. In anderen Szenarien, wie z. b `packages.config` . Auto Vervollständigen und Restore, gibt es möglicherweise mehrere unterschiedliche Sitzungs-IDs aufgrund der Art und Weise, wie der Code berücksichtigt wird.

## <a name="authentication"></a>Authentifizierung

Die Authentifizierung wird der Implementation der Paketquelle überlassen, die definiert werden soll. Bei nuget.org erfordert nur die `PackagePublish`-Ressource Authentifizierung durch einen speziellen API-Schlüsselheader. Details sind in der [`PackagePublish`-Ressource](package-publish-resource.md) definiert.
