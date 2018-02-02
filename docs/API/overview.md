---
title: "Übersicht über die, die NuGet-API | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Die NuGet-API ist eine Sammlung von HTTP-Endpunkten, die zum Herunterladen von Paketen, Metadaten abzurufen, veröffentlichen neue Pakete usw. verwendet werden kann."
keywords: "NuGet-V3-API, NuGet V2-API, NuGet JSON, NuGet-Registrierung API NuGet-API-Flatfile-Container, NuGet Nupkg API, NuGet-Metadaten-API, NuGet-Such-API, NuGet-Push-API, NuGe veröffentlichen API NuGet API löschen, NuGet Benutzerauswahl-API das NuGet Protokoll"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c28b0912be6dbccab06078100cb71821c3658e08
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-api"></a>NuGet-API

Die NuGet-API ist eine Sammlung von HTTP-Endpunkten, die verwendet werden können, um Pakete herunterzuladen, Metadaten abzurufen, veröffentlichen neue Pakete und die meisten andere Vorgänge in der offiziellen NuGet-Clients verfügbar.

Diese API wird vom NuGet-Client in Visual Studio, nuget.exe und die CLI .NET NuGet-Vorgänge ausführen, z. B. verwendet [ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore), suchen Sie in der Visual Studio-Benutzeroberfläche und [ `nuget.exe push` ](../tools/cli-ref-push.md).

Beachten Sie in einigen Fällen nuget.org zusätzliche Anforderungen hat, die nicht von anderen Paketquellen erzwungen werden. Diese Unterschiede sind dokumentiert, durch die [nuget.org Protokolle](nuget-protocols.md).

## <a name="service-index"></a>Dienst-index

Der Einstiegspunkt für die API ist ein JSON-Dokument in einem bekannten Speicherort. Dieses Dokument wird aufgerufen, die **Dienst Index**.
Der Speicherort des Indexes, Dienst für nuget.org ist `https://api.nuget.org/v3/index.json`.

Dieses JSON-Dokument enthält eine Liste von *Ressourcen* die eine andere Funktionalität bereit und erfüllen Sie verschiedene Anwendungsfälle.

Clients, die die API unterstützt, sollte eine oder mehrere der folgenden Index-Dienst-URL als Mittel zum Herstellen einer Verbindung mit der jeweiligen Paketquellen akzeptieren.

Weitere Informationen zu den Service-Index, finden Sie unter [seine API-Referenz](service-index.md).

## <a name="versioning"></a>Versionskontrolle

Die API ist Version 3 des NuGet HTTP-Protokoll. Dieses Protokoll wird manchmal als "V3-API." bezeichnet Diese Referenzdokumente bezieht sich auf diese Version des Protokolls einfach als "-API."

Die Schemaversion des Dienst-Index wird angegeben, indem die `version` Eigenschaft im Dienst-Index. Die API ordnet an, dass die Versionszeichenfolge eine höhere Versionsnummer hat `3`. Das IndexSchema Service nicht maßgebliche Änderungen vorgenommen werden, wird die Versionszeichenfolge Nebenversion erhöht werden.

Ältere Clients (z. B. nuget.exe 2.x) nicht unterstützen die API V3 und unterstützen nur die ältere V2-API, die hier nicht dokumentiert ist.

Die NuGet-V3-API wird als solche bezeichnet, da der Nachfolger von der V2-API ist, die das OData-basierte Protokoll von der Version 2.x des offiziellen NuGet-Clients implementiert wurde. Die V3-API wurde zuerst durch die Version 3.0 des offiziellen NuGet-Clients unterstützt, und die neuesten wichtigen Protokollversion wird weiterhin unterstützt werden, von dem NuGet-Client 4.0 sowie auf. 

Nicht unterbrechend wurden der API vorgenommenen protokolländerungen seit der ersten Version.

## <a name="resources-and-schema"></a>Ressourcen und schema

Die **Dienst Index** beschreibt eine Vielzahl von Ressourcen. Der aktuelle Satz von unterstützte Ressourcen sind wie folgt aus:

Ressourcenname                                                          | Erforderlich | Beschreibung
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | ja      | Mithilfe von Push übertragen und löschen (oder Benutzerauswahl) Pakete.
[`SearchQueryService`](search-query-service-resource.md)               | ja      | Filtern Sie und suchen Sie nach der Pakete nach Schlüsselwort.
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | ja      | Abrufen von Metadaten von Paketen.
[`PackageBaseAddress`](package-base-address-resource.md)               | ja      | Abrufen von Paketinhalt (.nupkg).
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | Nein       | Ermitteln Sie die Paket-IDs und Versionen von Teilzeichenfolge.
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | Nein       | Erstellen Sie eine URL für den Zugriff auf eine Webseite "Melden des Missbrauchs".
[`Catalog`](catalog-resource.md)                                       | Nein       | Vollständigen Datensatz aller Ereignisse für Paket.

Im Allgemeinen werden alle nicht binären Daten zurückgegeben, die von einer API-Ressource mit JSON serialisiert. Jede Ressource im Index Dienst zurückgegebene Antwortschema ist für diese Ressource einzeln definiert. Weitere Informationen zu jeder Ressource finden Sie unter den oben aufgeführten Themen.

> [!Note]
> Wenn eine Datenquelle nicht implementiert `SearchAutocompleteService` automatische Verhalten für den ordnungsgemäßen deaktiviert werden sollte. Wenn `ReportAbuseUriTemplate` nicht implementiert wird, wird der offiziellen NuGet-Client fällt an sich der Nuget.org-Bericht-Missbrauch-URL (von überwachten [NuGet/Home #4924](https://github.com/NuGet/Home/issues/4924)). Andere Clients können sich entscheiden, um einfach keine Missbrauch Berichts-URL für dem Benutzer anzuzeigen.

## <a name="timestamps"></a>Timestamps

Alle Zeitstempel, die von der API zurückgegebenen UTC werden oder sind anderweitig mit [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) Darstellung. 

## <a name="http-methods"></a>HTTP-Methoden

Verb   | Mit
------ | -----------
GET    | Führt einen schreibgeschützten Vorgang, der in der Regel Abrufen von Daten an.
HEAD-,   | Ruft die Antwortheader für den entsprechenden `GET` Anforderung.
PUT    | Erstellt eine Ressource, die nicht vorhanden ist oder wenn es vorhanden ist, wird aktualisiert. Einige Ressourcen unterstützen möglicherweise nicht aktualisieren.
DELETE | Löscht oder unlists eine Ressource.

## <a name="http-status-codes"></a>HTTP-Statuscodes

Code | Beschreibung
---- | -----
300  | Erfolg, und es gibt ein Antworttext.
201  | Erfolgs- und die Ressource wurde erstellt.
202  | Erfolg der Anforderung akzeptiert wurde, aber Arbeit möglicherweise trotzdem unvollständig und abgeschlossenen asynchron.
204  | Erfolg, aber es kein Antworttext ist.
301  | Eine permanente Umleitung.
302  | Eine temporäre Umleitung.
400  | Die Parameter in der URL oder im Hauptteil Anforderung sind ungültig.
401  | Die angegebenen Anmeldeinformationen sind ungültig.
403  | Die Aktion ist nicht zulässig, die bereitgestellten Anmeldeinformationen angegeben.
404  | Die angeforderte Ressource ist nicht vorhanden.
409  | Die Anforderung steht in Konflikt mit einer vorhandenen Ressource.
500  | Der Dienst ist ein unerwarteten Fehler aufgetreten.
503  | Der Dienst ist vorübergehend nicht verfügbar.

Alle `GET` Anforderung an einen API-Endpunkt möglicherweise eine HTTP-Umleitung (301 oder 302) zurück. Clients sollten sauber solche leitet durch genaues Betrachten der `Location` Header und einer nachfolgenden akustischen `GET`. Dokumentation zu bestimmten Endpunkten wird nicht explizit aufrufen, wobei leitet verwendet werden können.

Im Fall einer auf 500-Statuscode kann der Client einen angemessene Wiederholungsmechanismus implementieren. Die offiziellen NuGet Client Wiederholungen dreimal so groß wie bei der alle-Ebene 500-Statuscode oder TCP/DNS-Fehler festgestellt wurde.

## <a name="http-request-headers"></a>HTTP-Anforderungsheader

name                     | Beschreibung
------------------------ | -----------
X-NuGet-ApiKey           | Erforderlich für Push-als auch löschen, siehe [ `PackagePublish` Ressource](package-publish-resource.md)
X-NuGet-Client-Version   | **Als veraltet markiert** und ersetzt durch`X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | In bestimmten Fällen auf nuget.org nur erforderlich, siehe [nuget.org-Protokolle](NuGet-Protocols.md)

## <a name="authentication"></a>Authentifizierung

Authentifizierung bleibt bis zu der Paket-Source-Implementierung zu definieren. Für nuget.org, nur die `PackagePublish` Ressource ist eine Authentifizierung über ein spezieller Header der API-Schlüssel erforderlich. Finden Sie unter [ `PackagePublish` Ressource](package-publish-resource.md) Details.
