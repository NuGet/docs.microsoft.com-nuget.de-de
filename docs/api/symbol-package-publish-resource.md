---
title: Push-Symbolpakete, NuGet-API | Microsoft-Dokumentation
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Publish-Diensts kann Clients neue Symbolpakete zu veröffentlichen.
keywords: NuGet-API-Push-Symbolpaket
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580413"
---
# <a name="push-symbol-packages"></a>Push-Symbolpaketen

Es ist möglich, Push-Symbolpakete ([Snupkg](../create-packages/Symbol-Packages-snupkg.md)) mithilfe der NuGet-V3-API.
Diese Vorgänge sind basierend auf den `SymbolPackagePublish` Ressource finden Sie in der [dienstindex](service-index.md).

## <a name="versioning"></a>Versionskontrolle

Die folgenden `@type` Wert wird verwendet:

@type-Wert                 | Hinweise
--------------------        | -----
SymbolPackagePublish/4.9.0  | Die erste Version

## <a name="base-url"></a>Basis-URL

Die base-URL für die folgenden APIs ist der Wert des der `@id` Eigenschaft der `SymbolPackagePublish/4.9.0` Ressource in der Paketquelle [dienstindex](service-index.md). Die folgende Dokumentation dient Nuget.org URL. Betrachten Sie `https://www.nuget.org/api/v2/symbolpackage` als Platzhalter für die `@id` Wert in der dienstindex gefunden.

## <a name="http-methods"></a>HTTP-Methoden

Die `PUT` HTTP-Methode wird durch diese Ressource unterstützt. 

## <a name="push-a-symbol-package"></a>Ein Symbolpaket mithilfe von Push übertragen

NuGet.org unterstützt Ablegevorgänge neues Format für die Symbol-Pakete ([Snupkg](../create-packages/Symbol-Packages-snupkg.md)) mithilfe der folgenden-API. 

    PUT https://www.nuget.org/api/v2/symbolpackage

Symbolpakete, mit der gleichen ID und Version können mehrere Male gesendet werden. Ein Symbolpaket werden in den folgenden Fällen zurückgewiesen.
- Ein Paket mit der gleichen ID und Version ist nicht vorhanden.
- Ein Symbolpaket, mit der gleichen ID und Version mithilfe von Push übertragen wurde, aber es wurde noch nicht veröffentlicht.
- Das Symbolpaket ([Snupkg](../create-packages/Symbol-Packages-snupkg.md)) ist ungültig (finden Sie unter [symbol Paket Einschränkungen](../create-packages/Symbol-Packages-snupkg.md)).

### <a name="request-parameters"></a>Anforderungsparameter

name           | In     | Typ   | Erforderlich | Hinweise
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Header | String | ja      | Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`

Die API-Schlüssel ist eine nicht transparente Zeichenfolge, aus der Paketquelle vom Benutzer abgerufen und in den Client konfiguriert. Kein besonderes Zeichenfolgenformat wird vorgeschrieben, aber der API-Schlüssel sollte nicht länger als eine angemessene Größe für HTTP-Headerwerte.

### <a name="request-body"></a>Anforderungstext

Der Anforderungstext für die Symbol-Push ist identisch mit dem Anforderungstext, der eine Anforderung zum Paketimport Push (finden Sie unter [Push-Paket, und Löschen von](package-publish-resource.md)). 

### <a name="response"></a>Antwort

Statuscode | Bedeutung
----------- | -------
201         | Das Symbolpaket wurde erfolgreich per Push übertragen.
400         | Das angegebene Symbolpaket ist ungültig.
401         | Der Benutzer ist nicht zum Ausführen dieser Aktion autorisiert.
404         | Eine entsprechende Paket mit der angegebenen ID und Version ist nicht vorhanden.
409         | Ein Symbolpaket, mit der angegebenen ID und Version wurde per Push übertragen, aber es ist noch nicht verfügbar.
413         | Das Paket ist zu groß.

