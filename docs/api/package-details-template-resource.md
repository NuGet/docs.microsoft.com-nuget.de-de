---
title: Paket-Details-URL-Vorlage, NuGet-API
description: Die Paket-Details-URL-Vorlage kann Clients in ihrer Benutzeroberfläche, die eine Web-link auf Weitere Paketinformationen zu anzeigen
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638073"
---
# <a name="package-details-url-template"></a>Paket-Details-URL-Vorlage

Es ist möglich, dass ein Client eine URL zu erstellen, die vom Benutzer verwendet werden können, um weitere Paketdetails in ihrem Webbrowser anzuzeigen. Dies ist nützlich, wenn eine Paketquelle will, um zusätzliche Informationen zu einem Paket, die nicht passen möglicherweise innerhalb des Bereichs, was die NuGet-Client-Anwendung zeigt anzuzeigen.

Die Ressource, die zum Erstellen von dieser URL ist die `PackageDetailsUriTemplate` Ressource finden Sie in der [dienstindex](service-index.md).

## <a name="versioning"></a>Versionskontrolle

Die folgenden `@type` Werte werden verwendet:

@type-Wert                     | Hinweise
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | Die erste Version

## <a name="url-template"></a>URL-Vorlage

Die URL für die folgende API wird der Wert des der `@id` Eigenschaft, die einer der oben genannten Ressource zugeordneten `@type` Werte.

## <a name="http-methods"></a>HTTP-Methoden

Der Client nicht gedacht ist, um Anforderungen an die URL des Pakets Details im Auftrag des Benutzers zu senden, sollte die Webseite unterstützen die `GET` Methode, um eine geklickte URL ganz einfach in einem Webbrowser geöffnet werden können.

## <a name="construct-the-url"></a>Erstellen Sie die URL

Wenn eine bekannte Paket-ID und Version, kann die Client-Implementierung eine URL für den Zugriff auf eine Weboberfläche erstellen. Die Clientimplementierung sollte diese erstellte URL (oder einen klickbaren Link) um dem Benutzer um einen Webbrowser an die URL zu öffnen und Weitere Informationen zu dem Paket angezeigt werden. Den Inhalt der Detailseite des Pakets wird durch die Implementierung der Server bestimmt.

Die URL muss eine absolute URL sein, und die (Protokoll)-Schema muss HTTPS sein.

Der Wert des der `@id` im Dienst-Index ist eine URL-Zeichenfolge, die mit einem der folgenden Platzhalter-Token:

### <a name="url-placeholders"></a>URL-Platzhalter

Name        | Typ    | Erforderlich | Hinweise
----------- | ------- | -------- | -----
`{id}`      | Zeichenfolge  | Nein       | Die Paket-ID zum Abrufen von Details für
`{version}` | Zeichenfolge  | Nein       | Die Paketversion, um Details zu erhalten

Es sollte der Server akzeptiert `{id}` und `{version}` Werte mit jedem Groß-/Kleinschreibung. Darüber hinaus der Server sollte nicht anfällig für gibt an, ob die Version ist [normalisierte](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers). Das heißt, der Server annehmen sollte auch nicht normalisierte Versionen akzeptieren.

Beispielsweise sieht die Nuget.org Paket-Details-Vorlage wie folgt aus:

    https://www.nuget.org/packages/{id}/{version}

Wenn die Clientimplementierung einen Link auf die Paketdetails für NuGet.Versioning 4.3.0 angezeigt werden soll muss, würde er erzeugt die folgende URL, und geben Sie sie für den Benutzer:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
