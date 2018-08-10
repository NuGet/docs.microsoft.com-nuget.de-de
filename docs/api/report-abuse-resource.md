---
title: Melden von Missbrauch URL-Vorlage, NuGet-API
description: Die Bericht Missbrauch URL-Vorlage kann Clients einen Missbrauch Berichtslink in ihrer Benutzeroberfläche angezeigt.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b1fd65b12590a6c5eeb23d946eec6ca4a1c661bc
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020439"
---
# <a name="report-abuse-url-template"></a>Bericht-Missbrauch-URL-Vorlage

Es ist möglich, dass ein Client eine URL zu erstellen, die vom Benutzer zum Angeben des Missbrauchs zu einem bestimmten Paket verwendet werden können. Dies ist nützlich, wenn möchte, dass eine Paketquelle alle Clientumgebungen, Missbrauch Berichte für die Paketquelle zu delegieren (sogar 3rd Party) zu aktivieren.

Die Ressource, die zum Erstellen von dieser URL ist die `ReportAbuseUriTemplate` Ressource finden Sie in der [dienstindex](service-index.md).

## <a name="versioning"></a>Versionskontrolle

Die folgenden `@type` Werte werden verwendet:

@type-Wert                       | Hinweise
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | Die erste Version
ReportAbuseUriTemplate/3.0.0-rc   | Alias der `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>URL-Vorlage

Die URL für die folgende API wird der Wert des der `@id` Eigenschaft, die einer der oben genannten Ressource zugeordneten `@type` Werte.

## <a name="http-methods"></a>HTTP-Methoden

Der Client nicht gedacht ist, um Anforderungen an die URL des Berichts Missbrauch im Auftrag des Benutzers zu senden, sollte die Webseite unterstützen die `GET` Methode, um eine geklickte URL ganz einfach in einem Webbrowser geöffnet werden können.

## <a name="construct-the-url"></a>Erstellen Sie die URL

Wenn eine bekannte Paket-ID und Version, kann die Client-Implementierung eine URL für den Zugriff auf eine Weboberfläche erstellen. Die Clientimplementierung sollte diese erstellte URL (oder einen klickbaren Link) anzeigen, um dem Benutzer, öffnen einen Webbrowser an die URL, und nehmen alle erforderlichen Missbrauch-Bericht. Die Implementierung den Missbrauch Berichtsformular wird durch die Implementierung der Server bestimmt.

Der Wert des der `@id` ist eine URL-Zeichenfolge, die mit der eines der folgenden Platzhalter-Token:

### <a name="url-placeholders"></a>URL-Platzhalter

name        | Typ    | Erforderlich | Hinweise
----------- | ------- | -------- | -----
`{id}`      | Zeichenfolge  | Nein       | Die Paket-ID zum Angeben des Missbrauchs für
`{version}` | Zeichenfolge  | Nein       | Die Paketversion zum Angeben des Missbrauchs für

Die `{id}` und `{version}` Werte interpretiert werden, durch die Implementierung der Server muss Groß-/Kleinschreibung und nicht vertrauliche gibt an, ob die Version normalisiert ist.

Beispielsweise sieht die Nuget.org Missbrauch Berichtsvorlage folgendermaßen aus:

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

Wenn die Clientimplementierung eine Verknüpfung zum Missbrauch Berichts angezeigt wird, für die NuGet.Versioning 4.3.0 muss, würde er erzeugt die folgende URL, und geben Sie sie für den Benutzer:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
