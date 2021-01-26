---
title: Paket Details-URL-Vorlage, nuget-API
description: Mit der Vorlage "Paket Details-URL" können Clients in der Benutzeroberfläche einen Weblink zu weiteren Paket Details anzeigen.
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: aaeedea9750c11099b34e927bd8442656839d784
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773945"
---
# <a name="package-details-url-template"></a>Paket Details-URL-Vorlage

Es ist möglich, dass ein Client eine URL erstellt, die vom Benutzer verwendet werden kann, um weitere Paket Details in seinem Webbrowser anzuzeigen. Dies ist hilfreich, wenn eine Paketquelle zusätzliche Informationen zu einem Paket anzeigen möchte, die möglicherweise nicht in den Bereich der nuget-Client Anwendung passen.

Die Ressource, die zum aufbauen dieser URL verwendet wird, ist die Ressource, die `PackageDetailsUriTemplate` im [Dienst Index](service-index.md)gefunden wurde.

## <a name="versioning"></a>Versionsverwaltung

Die folgenden `@type` Werte werden verwendet:

Wert vom Typ @type                     | Hinweise
------------------------------- | -----
Packagedetailsuritemplate/5.1.0 | Die erste Version

## <a name="url-template"></a>URL-Vorlage

Die URL für die folgende API ist der Wert der Eigenschaft, die `@id` mit einem der oben erwähnten Ressourcen `@type` Werte verknüpft ist.

## <a name="http-methods"></a>HTTP-Methoden

Obwohl der Client nicht dafür vorgesehen ist, Anforderungen an die Paket Details-URL für den Benutzer zu senden, sollte die Webseite die-Methode unterstützen, `GET` damit eine angeklickte URL problemlos in einem Webbrowser geöffnet werden kann.

## <a name="construct-the-url"></a>Erstellen der URL

Wenn eine bekannte Paket-ID und-Version angegeben ist, kann die Client Implementierung eine URL für den Zugriff auf eine Weboberfläche erstellen. Die Client Implementierung sollte diese erstellte URL (oder einen klickbaren Link) dem Benutzer anzeigen, sodass Sie einen Webbrowser für die URL öffnen und weitere Informationen zum Paket erhalten können. Der Inhalt der Seite Paket Details wird von der Server Implementierung bestimmt.

Die URL muss eine absolute URL sein, und das Schema (Protokoll) muss https sein.

Der Wert von `@id` im Dienst Index ist eine URL-Zeichenfolge, die eines der folgenden Platzhalter Token enthält:

### <a name="url-placeholders"></a>URL-Platzhalter

Name        | Typ    | Erforderlich | Notizen
----------- | ------- | -------- | -----
`{id}`      | Zeichenfolge  | nein       | Die Paket-ID, für die Details zu erhalten sind.
`{version}` | Zeichenfolge  | nein       | Die Paketversion, für die Details zu erhalten sind

Der Server sollte `{id}` -und- `{version}` Werte mit beliebiger Schreibweise akzeptieren. Außerdem sollte der Server nicht darauf achten, ob die Version [normalisiert](../concepts/package-versioning.md#normalized-version-numbers)ist. Das heißt, der Server sollte auch akzeptieren, dass nicht normalisierte Versionen akzeptiert werden.

Beispielsweise sieht die Paket Detail Vorlage von nuget. org wie folgt aus:

```http
https://www.nuget.org/packages/{id}/{version}
```

Wenn die Client Implementierung einen Link zu den Paket Details für "nuget. Versionierung 4.3.0" anzeigen muss, würde Sie die folgende URL erstellen und für den Benutzer bereitstellen:

```http
https://www.nuget.org/packages/NuGet.Versioning/4.3.0
```
