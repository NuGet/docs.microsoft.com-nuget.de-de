---
title: URL-Vorlage zum Melden von Missbrauch, nuget-API
description: Mit der Vorlage "Report Abuse URL" können Clients in der Benutzeroberfläche den Link "Missbrauch melden" anzeigen.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775224"
---
# <a name="report-abuse-url-template"></a>URL-Vorlage zum Melden von Missbrauch

Es ist möglich, dass ein Client eine URL erstellt, die vom Benutzer zum Melden von Missbrauch über ein bestimmtes Paket verwendet werden kann. Dies ist hilfreich, wenn eine Paketquelle die Übertragung von Missbrauchs Berichten an die Paketquelle durch eine Paketquelle ermöglichen möchte (auch von Drittanbietern).

Die Ressource, die zum aufbauen dieser URL verwendet wird, ist die Ressource, die `ReportAbuseUriTemplate` im [Dienst Index](service-index.md)gefunden wurde.

## <a name="versioning"></a>Versionsverwaltung

Die folgenden `@type` Werte werden verwendet:

Wert vom Typ @type                       | Hinweise
--------------------------------- | -----
Reportabuseuritemplate/3.0.0-Beta | Die erste Version
Reportabuseuritemplate/3.0.0-RC   | Alias von `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>URL-Vorlage

Die URL für die folgende API ist der Wert der Eigenschaft, die `@id` mit einem der oben erwähnten Ressourcen `@type` Werte verknüpft ist.

## <a name="http-methods"></a>HTTP-Methoden

Obwohl der Client nicht für das Senden von Anforderungen an die URL zum Melden von Missbrauch im Namen des Benutzers vorgesehen ist, sollte die Webseite die-Methode unterstützen, `GET` damit eine angeklickte URL problemlos in einem Webbrowser geöffnet werden kann.

## <a name="construct-the-url"></a>Erstellen der URL

Wenn eine bekannte Paket-ID und-Version angegeben ist, kann die Client Implementierung eine URL für den Zugriff auf eine Weboberfläche erstellen. Die Client Implementierung sollte diese erstellte URL (oder einen klickbaren Link) dem Benutzer anzeigen, sodass Sie einen Webbrowser mit der URL öffnen und einen erforderlichen Missbrauchsbericht erstellen können. Die Implementierung des Formular für den Missbrauch von Berichten wird von der Server Implementierung bestimmt.

Der Wert von `@id` ist eine URL-Zeichenfolge, die eines der folgenden Platzhalter Token enthält:

### <a name="url-placeholders"></a>URL-Platzhalter

Name        | Typ    | Erforderlich | Notizen
----------- | ------- | -------- | -----
`{id}`      | Zeichenfolge  | nein       | Die Paket-ID, für die Missbrauch gemeldet werden soll.
`{version}` | Zeichenfolge  | nein       | Die Paketversion, für die Missbrauch gemeldet werden soll.

Der `{id}` -Wert und der- `{version}` Wert, der von der Server Implementierung interpretiert wird, müssen die Groß-/Kleinschreibung nicht beachtet werden.

Beispielsweise sieht die Vorlage "Bericht Missbrauch" von nuget. org wie folgt aus:

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

Wenn die Client Implementierung einen Link zum berichtsmissbrauchs-Formular für nuget. Versionierung 4.3.0 anzeigen muss, würde Sie die folgende URL erstellen und für den Benutzer bereitstellen:

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
