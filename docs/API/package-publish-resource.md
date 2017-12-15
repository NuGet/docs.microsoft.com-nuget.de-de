---
title: "Push-als auch löschen, die NuGet-API | Microsoft Docs"
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
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "Der Dienst veröffentlichen kann Clients Veröffentlichen neuer Pakete und Benutzerauswahl oder löschen vorhandene Pakete."
keywords: "NuGet-API-Push-Paket-API die NuGet-Paket löschen, NuGet-API Benutzerauswahl Paket API NuGet-Paket zum Hochladen, API NuGet-Paket erstellen."
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 1fa3c0e1698a11208d9ef29fdf26a4980cb60cf5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="push-and-delete"></a>Push-als auch löschen

Es ist möglich, mithilfe von Push übertragen, und löschen (oder Benutzerauswahl, je nach serverimplementierung)-Pakete mit der NuGet-V3-API.
Beide Vorgänge basieren, der die `PackagePublish` Ressource gefunden, der [Dienst Index](service-index.md).

## <a name="versioning"></a>Versionskontrolle

Die folgenden `@type` Wert wird verwendet:

@type-Wert          | Hinweise
-------------------- | -----
PackagePublish/2.0.0 | Die erste Version

## <a name="base-url"></a>Basis-URL

Die base-URL für die folgenden APIs ist der Wert des der `@id` Eigenschaft von der `PackagePublish/2.0.0` Ressource in der Paketquelle [Dienst Index](service-index.md). Die Dokumentation wird sich der Nuget.org-URL verwendet. Betrachten Sie `https://www.nuget.org/api/v2/package` als Platzhalter für die `@id` Wert in der Service-Index gefunden.

Beachten Sie, dass diese URL verweist auf am gleichen Speicherort wie die ältere V2-Push-Endpunkt auf, da das Protokoll identisch ist.

## <a name="http-methods"></a>HTTP-Methoden

Die `PUT` und `DELETE` HTTP-Methoden werden durch diese Ressource unterstützt. Welche Methoden für jeden Endpunkt unterstützt werden finden Sie weiter unten.

## <a name="push-a-package"></a>Ein Paket mithilfe von Push übertragen

NuGet.org unterstützt, wie neue Pakete, die mithilfe der folgenden-API. Wenn das Paket mit der angegebenen ID und die Version bereits vorhanden ist, lehnt nuget.org der Push-Vorgang. Andere Paketquellen unterstützen möglicherweise das Ersetzen eines vorhandenen Pakets.

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>Anforderungsparameter

Name           | In     | Typ   | Erforderlich | Hinweise
-------------- | ------ | ------ | -------- | -----
X-NuGet-"apikey" | Header | string | ja      | Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`

API-Schlüssel ist eine nicht transparente Zeichenfolge, aus der Paketquelle vom Benutzer erhalten und in den Client konfiguriert. Wird kein bestimmtes Zeichenfolgenformat beauftragt, aber der API-Schlüssel sollte nicht länger als eine angemessene Größe für HTTP-Header-Werte.

### <a name="request-body"></a>Anforderungstext

Der Anforderungstext muss in der folgenden Form stammen:

#### <a name="multipart-form-data"></a>Mehrteiligen Formulardaten.

Der Anforderungsheader `Content-Type` ist `multipart/form-data` und das erste Element im Hauptteil Anforderung ist, das die Rohdatenbytes, die von der NUPKG per Push übermittelt. Nachfolgende Elemente in den mehrteiligen Text werden ignoriert. Der Dateiname oder eventuelle weitere Header der mehrteiligen Elemente werden ignoriert.

### <a name="response"></a>Antwort

Statuscode | Bedeutung
----------- | -------
201, 202    | Das Paket wurde erfolgreich übertragen.
400         | Das bereitgestellte Paket ist ungültig
409         | Ein Paket mit der angegebenen ID und die Version ist bereits vorhanden.

Serverimplementierungen unterscheiden sich auf dem Erfolgsstatuscode zurückgegeben, wenn ein Paket erfolgreich übertragen wird.

## <a name="delete-a-package"></a>Löschen eines Pakets

NuGet.org interpretiert die Paket-Delete-Anforderung als ein "Benutzerauswahl". Dies bedeutet, dass das Paket für vorhandene Consumer des Pakets weiterhin verfügbar ist, aber das Paket nicht mehr angezeigt, in den Suchergebnissen oder in der Webschnittstelle wird. Weitere Informationen zu dieser Vorgehensweise finden Sie unter der [Pakete gelöscht](../policies/deleting-packages.md) Richtlinie. Andere serverimplementierungen sind frei, um dieses Signal als feste Löschvorgang interpretieren, vorläufigen löschen oder Benutzerauswahl. Beispielsweise [NuGet.Server in](https://www.nuget.org/packages/NuGet.Server) (eine Server-Implementierung unterstützt nur die ältere V2-API) unterstützt diese Anforderung als ein Unlist oder ein hartes löschen, die basierend auf einer Konfigurationsoption behandeln.

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Anforderungsparameter

Name           | In     | Typ   | Erforderlich | Hinweise
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | ja      | Die ID des Pakets zu löschenden
VERSION        | URL    | string | ja      | Die Version des Pakets gelöscht
X-NuGet-"apikey" | Header | string | ja      | Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Antwort

Statuscode | Bedeutung
----------- | -------
204         | Das Paket wurde gelöscht.
404         | Kein Paket mit dem angegebenen `ID` und `VERSION` vorhanden ist
