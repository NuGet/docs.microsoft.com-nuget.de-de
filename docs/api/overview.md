---
title: Übersicht über die NuGet-API
description: Der NuGet-API ist eine Reihe von HTTP-Endpunkten, die zum Herunterladen von Paketen, Metadaten abzurufen, veröffentlichen neue Pakete usw. verwendet werden kann.
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

Der NuGet-API ist eine Reihe von HTTP-Endpunkten, die verwendet werden kann, um das Herunterladen von Paketen, Metadaten abzurufen, veröffentlichen neue Pakete und führen Sie die meisten anderen Vorgänge in der offiziellen NuGet-Clients verfügbar sind.

Diese API wird vom NuGet-Client in Visual Studio, nuget.exe und der .NET CLI verwendet, um NuGet-Vorgänge auszuführen, z. B. [ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore), suchen Sie in der Visual Studio-Benutzeroberfläche und [ `nuget.exe push` ](../tools/cli-ref-push.md).

Beachten Sie in einigen Fällen "NuGet.org" verfügt über zusätzliche Anforderungen, die nicht von anderen Paketquellen erzwungen werden. Diese Unterschiede werden durch die ["nuget.org"-Protokolle](nuget-protocols.md).

Eine einfache Enumeration und Herunterladen der verfügbaren nuget.exe-Versionen finden Sie in der [tools.json](tools-json.md) Endpunkt.

## <a name="service-index"></a>Dienstindex

Der Einstiegspunkt für die API ist ein JSON-Dokument an einem bekannten Speicherort. In diesem Dokument wird aufgerufen, die **dienstindex**. Der Speicherort der dienstindex für nuget.org ist `https://api.nuget.org/v3/index.json`.

Dieses JSON-Dokument enthält eine Liste der *Ressourcen* die eine andere Funktionalität bereit und erfüllen Sie verschiedene Anwendungsfälle.

Clients, die die API zu unterstützen, sollte eine oder mehrere der folgenden Index-Dienst-URL als Mittel zum Herstellen einer Verbindung mit der entsprechenden Paketquellen akzeptieren.

Weitere Informationen zu den dienstindex, finden Sie unter [der API-Referenz](service-index.md).

## <a name="versioning"></a>Versionskontrolle

Die API ist Version 3 des NuGet HTTP-Protokoll. Dieses Protokoll wird manchmal als "V3-API." bezeichnet Diese Dokumente Verweis bezieht sich auf diese Version des Protokolls einfach als "die API".

Die Schemaversion des Dienst-Index wird angegeben, indem die `version` -Eigenschaft in der Service-Index. Die API erfordert, dass die Versionszeichenfolge eine Hauptversionsnummer des verfügt `3`. Als nicht fehlerhafte Änderungen an das Schema des Diensts Index vorgenommen werden, wird die Versionszeichenfolge Nebenversion erhöht.

Ältere Clients (z. B. nuget.exe 2.x) unterstützen nicht die V3-API und unterstützen nur die älteren V2-API, die hier nicht dokumentiert ist.

Der NuGet-V3-API wird als solche bezeichnet werden, da der Nachfolger der V2-API ist, die das OData-basierte Protokoll, das von der offiziellen NuGet-Client 2.x-Version implementiert wurde. Die V3-API wurde zuerst die Version 3.0 des offiziellen NuGet-Clients unterstützt, und die neuesten wichtigen Protokollversion wird weiterhin unterstützt werden, vom Client NuGet 4.0 und auf. 

Geschütztes Protokoll an die API wurde geändert seit dem ersten Version.

## <a name="resources-and-schema"></a>Ressourcen und schema

Die **dienstindex** beschreibt eine Reihe von Ressourcen. Der aktuelle Satz von unterstützten Ressourcen lauten wie folgt aus:

Ressourcenname                                                          | Erforderlich | Beschreibung
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | ja      | Mithilfe von Push übertragen und löschen (oder aus der Liste entfernen) Pakete.
[`SearchQueryService`](search-query-service-resource.md)               | ja      | Filtern und Pakete nach Schlüsselwort suchen.
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | ja      | Abrufen von Metadaten von Paketen.
[`PackageBaseAddress`](package-base-address-resource.md)               | ja      | Paketinhalt (NUPKG) zu erhalten.
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | Nein       | Entdecken Sie die Paket-IDs und Versionen von Teilzeichenfolge.
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | Nein       | Erstellen Sie eine URL für den Zugriff auf eine Webseite "Missbrauch melden".
[`RepositorySignatures`](repository-signatures-resource.md)            | Nein       | Abrufen von Zertifikaten, die zum Signieren von Repository verwendet.
[`Catalog`](catalog-resource.md)                                       | Nein       | Vollständigen Datensatz aller Ereignisse für Paket.

Im Allgemeinen werden alle nicht binären Daten zurückgegeben, die von einer API-Ressource mit JSON serialisiert. Das Antwortschema von jeder Ressource im dienstindex zurückgegeben wird einzeln für diese Ressource definiert. Weitere Informationen zu jeder Ressource finden Sie unter den oben aufgeführten Themen.

> [!Note]
> Wenn eine Datenquelle implementiert nicht den `SearchAutocompleteService` jedes Autocomplete-Verhalten ordnungsgemäß deaktiviert werden sollen. Wenn `ReportAbuseUriTemplate` nicht implementiert wird, wird der offiziellen NuGet-Client fällt an Nuget.org Bericht-Missbrauch-URL (von überwachten [und nach Hause NuGet #4924](https://github.com/NuGet/Home/issues/4924)). Andere Clients können entscheiden, um einfach keine Missbrauch Berichts-URL für dem Benutzer anzuzeigen.

## <a name="timestamps"></a>Timestamps

Alle Zeitstempel, die von der API zurückgegebenen werden in UTC angegeben ist, oder werden anders angegeben verwenden [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) Darstellung. 

## <a name="http-methods"></a>HTTP-Methoden

Verb   | Mit
------ | -----------
GET    | Führt einen schreibgeschützten Vorgang, der in der Regel Abrufen von Daten an.
HEAD-,   | Ruft die Antwortheader für den entsprechenden `GET` Anforderung.
PUT    | Erstellt eine Ressource, die nicht vorhanden, oder, wenn es vorhanden ist, wird aktualisiert. Einige Ressourcen unterstützen möglicherweise nicht aktualisieren.
DELETE | Löscht oder hebt dessen Auflistung auf eine Ressource.

## <a name="http-status-codes"></a>HTTP-Statuscodes

Code | Beschreibung
---- | -----
300  | Erfolg, und es gibt ein Antworttext.
201  | Erfolg und die Ressource wurde erstellt.
202  | Erfolg die Anforderung akzeptiert wurde, aber einige Aufgaben möglicherweise trotzdem unvollständig und abgeschlossenen asynchron.
204  | Erfolg, aber es kein Antworttext ist.
301  | Eine permanente Umleitung.
302  | Eine temporäre Umleitung.
400  | Die Parameter in der URL oder im Hauptteil Anforderung sind ungültig.
401  | Die angegebenen Anmeldeinformationen sind ungültig.
403  | Die Aktion ist nicht zulässig, die bereitgestellten Anmeldeinformationen angegeben.
404  | Die angeforderte Ressource ist nicht vorhanden.
409  | Die Anforderung steht in Konflikt mit einer vorhandenen Ressource.
500  | Der Dienst hat einen unerwarteten Fehler festgestellt.
503  | Der Dienst ist vorübergehend nicht verfügbar.

Alle `GET` Anforderungen an einen API-Endpunkt kann eine HTTP-Umleitung (301 oder 302) zurückgeben. Clients sollten sauber solche umleitungen durch Überwachen der `Location` Header und Ausstellen einer nachfolgenden `GET`. Dokumentation zu bestimmten Endpunkten wird nicht explizit aufrufen, wobei umleitungen verwendet werden kann.

Im Fall von einen Statuscode 500-Ebene kann der Client einen angemessenen Wiederholungsmechanismus implementieren. Die offiziellen NuGet-Client Wiederholungen drei Mal, wenn alle Statuscode 500 auf Serverebene oder die TCP/DNS-Fehler auftreten.

## <a name="http-request-headers"></a>HTTP-Anforderungsheader

name                     | Beschreibung
------------------------ | -----------
X-NuGet-ApiKey           | Erforderlich für Push- und löschen, siehe [ `PackagePublish` Ressource](package-publish-resource.md)
X-NuGet-Client-Version   | **Als veraltet markiert** und durch ersetzt `X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | In bestimmten Fällen nur auf nuget.org erforderlich, siehe ["nuget.org"-Protokolle](NuGet-Protocols.md)
X-NuGet-Sitzungs-Id       | *Optionale*. NuGet-Clients Version 4.7 + identifizieren HTTP-Anforderungen, die Teil der gleichen Sitzung des NuGet-Client. Für `PackageReference` Wiederherstellungsvorgänge vorhanden ist, eine einzelne Sitzungs-Id, für andere Szenarien, z. B. der automatischen Abschluss des Vorgangs und `packages.config` Wiederherstellung möglicherweise gibt es mehrere andere Sitzungs-Id des aufgrund wie der Code berücksichtigt wurden.

## <a name="authentication"></a>Authentifizierung

Authentifizierung wird die Paket-Source-Implementierung definieren überlassen. Für "nuget.org" nur die `PackagePublish` Ressource erfordert eine Authentifizierung über ein spezieller Header der API-Schlüssel. Finden Sie unter [ `PackagePublish` Ressource](package-publish-resource.md) Details.
