---
title: Übersicht über die nuget-Server-API
description: Die nuget-Server-API ist eine Reihe von HTTP-Endpunkten, die zum Herunterladen von Paketen, zum Abrufen von Metadaten, zum Veröffentlichen neuer Pakete usw. verwendet werden können.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: aacf56a5dc5af9abf6f60d42bc7fd530a128d0d8
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237808"
---
# <a name="nuget-server-api"></a>NuGet-Server-API

Bei der nuget-Server-API handelt es sich um einen Satz von HTTP-Endpunkten, die zum Herunterladen von Paketen, zum Abrufen von Metadaten, zum Veröffentlichen neuer Pakete und zum Ausführen der meisten anderen in den offiziellen nuget-Clients verfügbaren Vorgänge

Diese API wird vom nuget-Client in Visual Studio, nuget.exe und der .net-CLI verwendet, um nuget-Vorgänge auszuführen, z [`dotnet restore`](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) . b. Durchsuchen in der Visual Studio-Benutzeroberfläche und [`nuget.exe push`](../reference/cli-reference/cli-ref-push.md) .

Beachten Sie, dass nuget.org in einigen Fällen zusätzliche Anforderungen hat, die nicht von anderen Paketquellen erzwungen werden. Diese Unterschiede werden durch die [nuget.org-Protokolle](nuget-protocols.md)dokumentiert.

Eine einfache Enumeration und das Herunterladen verfügbarer nuget.exe Versionen finden Sie im [tools.jsauf](tools-json.md) dem Endpunkt.

## <a name="service-index"></a>Dienstindex

Der Einstiegspunkt für die API ist ein JSON-Dokument an einem bekannten Speicherort. Dieses Dokument wird als **Dienst Index** bezeichnet. Der Speicherort des Dienst Indexes für nuget.org ist `https://api.nuget.org/v3/index.json` .

Dieses JSON-Dokument enthält eine Liste mit *Ressourcen* , die unterschiedliche Funktionen bereitstellen und verschiedene Anwendungsfälle erfüllen.

Clients, die die API unterstützen, sollten eine oder mehrere dieser Dienst Index-URLs annehmen, um eine Verbindung mit den jeweiligen Paketquellen herzustellen.

Weitere Informationen zum Dienst Index finden Sie in der zugehörigen [API-Referenz](service-index.md).

## <a name="versioning"></a>Versionsverwaltung

Die API ist Version 3 des HTTP-Protokolls von nuget. Dieses Protokoll wird manchmal als "v3-API" bezeichnet. Diese Referenzdokumente verweisen auf diese Version des Protokolls, einfach auf die API.

Die Schema Version des Dienst Indexes wird durch die- `version` Eigenschaft im Dienst Index angegeben. Die API gibt an, dass die Versions Zeichenfolge eine Hauptversionsnummer von aufweist `3` . Da nicht unterbrechende Änderungen am Dienst Index Schema vorgenommen werden, wird die neben Version der Versions Zeichenfolge erweitert.

Ältere Clients (z. b. nuget.exe 2. x) unterstützen die V3-API nicht und unterstützen nur die ältere v2-API. Dies ist hier nicht dokumentiert.

Die nuget V3-API heißt so, dass Sie der Nachfolger der V2-API ist. dabei handelt es sich um das odata-basierte Protokoll, das von der 2. x-Version des offiziellen nuget-Clients implementiert wird. Die V3-API wurde zunächst von Version 3,0 des offiziellen nuget-Clients unterstützt und ist weiterhin die neueste Hauptprotokoll Version, die vom nuget-Client unterstützt wird, 4,0 und höher. 

An der API wurden seit der ersten Veröffentlichung nicht unterbrechende Protokoll Änderungen vorgenommen.

## <a name="resources-and-schema"></a>Ressourcen und Schema

Der **Dienst Index** beschreibt eine Vielzahl von Ressourcen. Der aktuelle Satz unterstützter Ressourcen lautet wie folgt:

Ressourcenname                                                        | Erforderlich | BESCHREIBUNG
-------------------------------------------------------------------- | -------- | -----------
[Katalog](catalog-resource.md)                                       | nein       | Vollständiger Datensatz aller Paket Ereignisse.
[Packagebaseaddress](package-base-address-resource.md)               | ja      | Get Package Content (. nupkg).
[Packagedetailsuritemplate](package-details-template-resource.md)    | nein       | Erstellen Sie eine URL für den Zugriff auf die Webseite mit Paket Details.
[Packagepublish](package-publish-resource.md)                        | ja      | Pakete per Push und DELETE (oder Unlist).
[Registrationsbaseurl](registration-base-url-resource.md)            | ja      | Paket Metadaten erhalten.
[Reportabuseuritemplate](report-abuse-resource.md)                   | nein       | Erstellen Sie eine URL für den Zugriff auf eine Website zum missbrauchen von Berichten.
[RepositorySignatures](repository-signatures-resource.md)            | nein       | Zertifikate für die Repository-Signierung erhalten.
[Searchautocompleteservice](search-autocomplete-service-resource.md) | nein       | Ermitteln der Paket-IDs und-Versionen nach Teil Zeichenfolge.
[Searchqueryservice](search-query-service-resource.md)               | ja      | Filtern Sie nach und suchen Sie nach-Schlüsselwort.
[Symbolpackagepublish](symbol-package-publish-resource.md)           | nein       | Push-Symbol Pakete.

Im Allgemeinen werden alle nicht binären Daten, die von einer API-Ressource zurückgegeben werden, mit JSON serialisiert. Das Antwort Schema, das von jeder Ressource im Dienst Index zurückgegeben wird, wird für diese Ressource einzeln definiert. Weitere Informationen zu den einzelnen Ressourcen finden Sie in den oben aufgeführten Themen.

In Zukunft können den JSON-Antworten neue Eigenschaften hinzugefügt werden, wenn das Protokoll weiterentwickelt wird. Damit der Client in Zukunft sicher ist, sollte die Implementierung nicht davon ausgehen, dass das Antwort Schema endgültig ist und keine zusätzlichen Daten enthalten kann. Alle Eigenschaften, die von der Implementierung nicht verstanden werden, sollten ignoriert werden.

> [!Note]
> Wenn eine Quelle kein Auto Vervollständigen-Verhalten implementiert, sollte das Verhalten ordnungsgemäß `SearchAutocompleteService` deaktiviert werden. Wenn `ReportAbuseUriTemplate` nicht implementiert ist, greift der offizielle nuget-Client auf die Report Abuse-URL von "nuget. org" zurück (nachverfolgt von [nuget/Home # 4924](https://github.com/NuGet/Home/issues/4924)). Andere Clients entscheiden sich möglicherweise dafür, dem Benutzer keine Berichts Missbrauch-URL anzuzeigen.

### <a name="undocumented-resources-on-nugetorg"></a>Nicht dokumentierte Ressourcen auf nuget.org

Der V3-Dienst Index in nuget.org verfügt über einige Ressourcen, die oben nicht dokumentiert sind. Es gibt einige Gründe, eine Ressource nicht zu dokumentieren.

Zunächst werden keine Ressourcen dokumentiert, die als Implementierungsdetail von nuget.org verwendet werden. Der `SearchGalleryQueryService` fällt in diese Kategorie. [Nugetgallery](https://github.com/NuGet/NuGetGallery) verwendet diese Ressource, um einige v2 (odata)-Abfragen an den Suchindex zu delegieren, anstatt die Datenbank zu verwenden. Diese Ressource wurde aus Gründen der Skalierbarkeit eingeführt und ist nicht für die externe Verwendung vorgesehen.

Zweitens werden keine Ressourcen dokumentiert, die nie in einer RTM-Version des offiziellen Clients ausgeliefert wurden.
`PackageDisplayMetadataUriTemplate` und `PackageVersionDisplayMetadataUriTemplate` fallen in diese Kategorie.

Drittens werden keine Ressourcen dokumentiert, die eng mit dem V2-Protokoll gekoppelt sind, das selbst absichtlich nicht dokumentiert ist. Die `LegacyGallery` Ressource fällt in diese Kategorie. Diese Ressource ermöglicht einem v3-Dienst Index, auf eine entsprechende v2-Quell-URL zu verweisen. Diese Ressource unterstützt `nuget.exe list` .

Wenn eine Ressource hier nicht dokumentiert ist, wird *dringend* empfohlen, dass Sie keine Abhängigkeit davon treffen. Wir können das Verhalten dieser nicht dokumentierten Ressourcen entfernen oder ändern, was die Implementierung auf unerwartete Weise unterbrechen könnte.

## <a name="timestamps"></a>Zeitstempel

Alle von der API zurückgegebenen Zeitstempel sind UTC oder werden anderweitig mithilfe der [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) -Darstellung angegeben. 

## <a name="http-methods"></a>HTTP-Methoden

Verb   | Verwendung
------ | -----------
GET    | Führt einen schreibgeschützten Vorgang aus, der in der Regel Daten abruft.
HEAD   | Ruft die Antwortheader für die entsprechende `GET` Anforderung ab.
PUT    | Erstellt eine Ressource, die nicht vorhanden ist, oder aktualisiert Sie, wenn Sie vorhanden ist. Einige Ressourcen unterstützen möglicherweise keine Updates.
Delete | Löscht eine Ressource oder hebt die Auflistung auf.

## <a name="http-status-codes"></a>HTTP-Statuscodes

Code | BESCHREIBUNG
---- | -----
200  | Erfolg, und es gibt einen Antworttext.
201  | Erfolg, und die Ressource wurde erstellt.
202  | Erfolg: die Anforderung wurde akzeptiert, aber einige Arbeiten sind möglicherweise noch unvollständig und asynchron abgeschlossen.
204  | Erfolg, aber es ist kein Antworttext vorhanden.
301  | Eine permanente Umleitung.
302  | Eine temporäre Umleitung.
400  | Die Parameter in der URL oder im Anforderungs Text sind ungültig.
401  | Die angegebenen Anmelde Informationen sind ungültig.
403  | Die Aktion ist aufgrund der angegebenen Anmelde Informationen nicht zulässig.
404  | Die angeforderte Ressource ist nicht vorhanden.
409  | Die Anforderung steht in Konflikt mit einer vorhandenen Ressource.
500  | Unerwarteter Fehler beim Dienst.
503  | Der Dienst ist vorübergehend nicht verfügbar.

Jede `GET` Anforderung, die an einen API-Endpunkt gerichtet ist, kann eine HTTP-Umleitung (301 oder 302) zurückgeben. Clients sollten diese Umleitungen ordnungsgemäß behandeln, indem Sie den `Location` -Header beobachten und einen nachfolgenden ausgeben `GET` . Die Dokumentation zu bestimmten Endpunkten führt nicht explizit aus, wo Umleitungen verwendet werden können.

Im Fall eines Statuscodes der 500-Ebene kann der Client einen angemessenen Wiederholungs Mechanismus implementieren. Der offizielle nuget-Client wird dreimal wiederholt, wenn ein Statuscode der 500-Ebene oder ein TCP/DNS-Fehler aufgetreten ist.

## <a name="http-request-headers"></a>HTTP-Anforderungsheader

Name                     | BESCHREIBUNG
------------------------ | -----------
X-nuget-APIKey           | Erforderlich für Push und DELETE, siehe [ `PackagePublish` Ressource](package-publish-resource.md)
X-nuget-Client-Version   | **Veraltet** und ersetzt durch `X-NuGet-Protocol-Version`
X-nuget-Protocol-Version | In bestimmten Fällen nur auf nuget.org erforderlich, siehe [nuget.org-Protokolle](NuGet-Protocols.md) .
X-nuget-Session-ID       | *Optional:* Die nuget-Clients v 4.7 und identifizieren HTTP-Anforderungen, die Teil derselben nuget-Client Sitzung sind.

Der `X-NuGet-Session-Id` verfügt über einen einzelnen Wert für alle Vorgänge, die sich auf eine einzelne Wiederherstellung in beziehen `PackageReference` . In anderen Szenarien, wie z. b. Auto Vervollständigen und `packages.config` Restore, gibt es möglicherweise mehrere unterschiedliche Sitzungs-IDs aufgrund der Art und Weise, wie der Code berücksichtigt wird.

## <a name="authentication"></a>Authentifizierung

Die Authentifizierung wird von der Paketquellen Implementierung bis zum Definieren beibehalten. Für nuget.org erfordert nur die- `PackagePublish` Ressource eine Authentifizierung über einen speziellen API-Schlüssel Header. Weitere Informationen finden Sie in der [ `PackagePublish` Ressource](package-publish-resource.md) .
