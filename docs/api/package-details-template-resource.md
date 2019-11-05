---
title: Paket Details-URL-Vorlage, nuget-API
description: Mit der Vorlage "Paket Details-URL" können Clients in der Benutzeroberfläche einen Weblink zu weiteren Paket Details anzeigen.
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 3102cb9a20f354e92a0da8bba6457dc2ad0f0f2d
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610955"
---
# <a name="package-details-url-template"></a>Paket Details-URL-Vorlage

Es ist möglich, dass ein Client eine URL erstellt, die vom Benutzer verwendet werden kann, um weitere Paket Details in seinem Webbrowser anzuzeigen. Dies ist hilfreich, wenn eine Paketquelle zusätzliche Informationen zu einem Paket anzeigen möchte, die möglicherweise nicht in den Bereich der nuget-Client Anwendung passen.

Die Ressource, die zum aufbauen dieser URL verwendet wird, ist die `PackageDetailsUriTemplate` Ressource, die im [Dienst Index](service-index.md)gefunden wurde.

## <a name="versioning"></a>Versionskontrolle

Die folgenden `@type` Werte werden verwendet:

@type -Wert                     | Notizen
------------------------------- | -----
Packagedetailsuritemplate/5.1.0 | Die erste Version

## <a name="url-template"></a>URL-Vorlage

Die URL für die folgende API ist der Wert der `@id`-Eigenschaft, die einem der oben erwähnten Ressourcen `@type` Werte zugeordnet ist.

## <a name="http-methods"></a>HTTP-Methoden

Obwohl der Client nicht dafür vorgesehen ist, Anforderungen an die Paket Details-URL für den Benutzer zu senden, sollte die Webseite die `GET`-Methode unterstützen, damit eine angeklickte URL problemlos in einem Webbrowser geöffnet werden kann.

## <a name="construct-the-url"></a>Erstellen der URL

Wenn eine bekannte Paket-ID und-Version angegeben ist, kann die Client Implementierung eine URL für den Zugriff auf eine Weboberfläche erstellen. Die Client Implementierung sollte diese erstellte URL (oder einen klickbaren Link) dem Benutzer anzeigen, sodass Sie einen Webbrowser für die URL öffnen und weitere Informationen zum Paket erhalten können. Der Inhalt der Seite Paket Details wird von der Server Implementierung bestimmt.

Die URL muss eine absolute URL sein, und das Schema (Protokoll) muss https sein.

Der Wert der `@id` im Dienst Index ist eine URL-Zeichenfolge, die eines der folgenden Platzhalter Token enthält:

### <a name="url-placeholders"></a>URL-Platzhalter

-Name        | Geben Sie Folgendes ein:    | Erforderlich | Notizen
----------- | ------- | -------- | -----
`{id}`      | string  | Nein       | Die Paket-ID, für die Details zu erhalten sind.
`{version}` | string  | Nein       | Die Paketversion, für die Details zu erhalten sind

Der Server sollte `{id}` und `{version}` Werte in beliebiger Groß-/Kleinschreibung akzeptieren. Außerdem sollte der Server nicht darauf achten, ob die Version [normalisiert](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers)ist. Das heißt, der Server sollte auch akzeptieren, dass nicht normalisierte Versionen akzeptiert werden.

Beispielsweise sieht die Paket Detail Vorlage von nuget. org wie folgt aus:

    https://www.nuget.org/packages/{id}/{version}

Wenn die Client Implementierung einen Link zu den Paket Details für "nuget. Versionierung 4.3.0" anzeigen muss, würde Sie die folgende URL erstellen und für den Benutzer bereitstellen:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
