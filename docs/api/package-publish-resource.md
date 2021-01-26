---
title: Push und DELETE, nuget-API
description: Der Veröffentlichungs Dienst ermöglicht es Clients, neue Pakete zu veröffentlichen und vorhandene Pakete zu entfernen oder zu löschen.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773921"
---
# <a name="push-and-delete"></a>Push und DELETE

Es ist möglich, abhängig von der Server Implementierung Push, DELETE (oder die Auflistung aufzuheben) und Pakete mit der nuget-V3-API zu wiederholen. Diese Vorgänge basieren auf der Ressource, die `PackagePublish` im [Dienst Index](service-index.md)gefunden wurde.

## <a name="versioning"></a>Versionsverwaltung

Der folgende `@type` Wert wird verwendet:

Wert vom Typ @type          | Hinweise
-------------------- | -----
Packagepublish/2.0.0 | Die erste Version

## <a name="base-url"></a>Basis-URL

Die Basis-URL für die folgenden APIs ist der Wert der `@id` -Eigenschaft der `PackagePublish/2.0.0` Ressource im [Dienst Index](service-index.md)der Paketquelle. In der nachfolgenden Dokumentation wird die URL von "nuget. org" verwendet. Beachten Sie `https://www.nuget.org/api/v2/package` als Platzhalter für den `@id` Wert, der im Dienst Index gefunden wurde.

Beachten Sie, dass diese URL auf denselben Speicherort wie der Legacy-v2-Push-Endpunkt verweist, da das Protokoll identisch ist.

## <a name="http-methods"></a>HTTP-Methoden

Die `PUT` `POST` http- `DELETE` Methoden, und werden von dieser Ressource unterstützt. Informationen dazu, welche Methoden an jedem Endpunkt unterstützt werden, finden Sie unten.

## <a name="push-a-package"></a>Pushen eines Pakets

> [!Note]
> nuget.org hat [zusätzliche Anforderungen](NuGet-Protocols.md) für die Interaktion mit dem Push-Endpunkt.

nuget.org unterstützt das pushen neuer Pakete mithilfe der folgenden API. Wenn das Paket mit der angegebenen ID und Version bereits vorhanden ist, lehnt nuget.org den Push ab. Andere Paketquellen unterstützen möglicherweise das Ersetzen vorhandener Pakete.

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>Anforderungsparameter

Name           | In     | Typ   | Erforderlich | Notizen
-------------- | ------ | ------ | -------- | -----
X-nuget-APIKey | Header | Zeichenfolge | ja      | Zum Beispiel, `X-NuGet-ApiKey: {USER_API_KEY}`

Der API-Schlüssel ist eine nicht transparente Zeichenfolge, die vom Benutzer aus der Paketquelle abgerufen und für den Client konfiguriert wurde. Es ist kein bestimmtes Zeichen folgen Format vorgeschrieben, aber die Länge des API-Schlüssels sollte keine angemessene Größe für HTTP-Header Werte überschreiten.

### <a name="request-body"></a>Anforderungstext

Der Anforderungs Text muss in der folgenden Form angezeigt werden:

#### <a name="multipart-form-data"></a>Mehrteilige Formulardaten

Der Anforderungs Header `Content-Type` ist `multipart/form-data` , und das erste Element im Anforderungs Text ist die unformatierten Bytes der. nupkg-Datei, die per pushübertragung durchgesetzt wird. Nachfolgende Elemente im mehrteiligen Textkörper werden ignoriert. Der Dateiname oder andere Header der mehrteiligen Elemente werden ignoriert.

### <a name="response"></a>Antwort

Statuscode | Bedeutung
----------- | -------
201, 202    | Das Paket wurde erfolgreich übermittelt.
400         | Das angegebene Paket ist ungültig.
409         | Ein Paket mit der angegebenen ID und Version ist bereits vorhanden.

Server Implementierungen variieren dem Erfolgsstatus Code, der zurückgegeben wird, wenn ein Paket erfolgreich übermittelt wurde.

## <a name="delete-a-package"></a>Löschen eines Pakets

nuget.org interpretiert die DELETE-Anforderung des Pakets als "Unlist". Dies bedeutet, dass das Paket weiterhin für vorhandene Consumer des Pakets verfügbar ist, das Paket jedoch nicht mehr in den Suchergebnissen oder der Weboberfläche angezeigt wird. Weitere Informationen zu dieser Vorgehensweise finden Sie in der Richtlinie für [gelöschte Pakete](../nuget-org/policies/deleting-packages.md) . Andere Server Implementierungen können dieses Signal als harte Löschung, vorläufiges löschen oder Unlist interpretieren. Beispielsweise unterstützt [nuget. Server](https://www.nuget.org/packages/NuGet.Server) (eine Server Implementierung, die nur die ältere v2-API unterstützt) die Verarbeitung dieser Anforderung als Auflistung oder Hard Delete basierend auf einer Konfigurationsoption.

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Anforderungsparameter

Name           | In     | Typ   | Erforderlich | Notizen
-------------- | ------ | ------ | -------- | -----
id             | URL    | Zeichenfolge | ja      | Die ID des zu löschenden Pakets.
VERSION        | URL    | Zeichenfolge | ja      | Die Version des zu löschenden Pakets.
X-nuget-APIKey | Header | Zeichenfolge | ja      | Zum Beispiel, `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Antwort

Statuscode | Bedeutung
----------- | -------
204         | Das Paket wurde gelöscht.
404         | Es ist kein Paket mit dem angegebenen vorhanden `ID` und `VERSION` vorhanden.

## <a name="relist-a-package"></a>Ein Paket erneut auflisten

Wenn ein Paket nicht aufgelistet wird, ist es möglich, dieses Paket erneut in den Suchergebnissen mit dem Endpunkt "relist" sichtbar zu machen. Dieser Endpunkt hat dieselbe Form wie der [Delete (Unlist)-Endpunkt](#delete-a-package) , verwendet jedoch die `POST` http-Methode anstelle der- `DELETE` Methode.

Wenn das Paket bereits aufgelistet ist, ist die Anforderung weiterhin erfolgreich.

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Anforderungsparameter

Name           | In     | Typ   | Erforderlich | Notizen
-------------- | ------ | ------ | -------- | -----
id             | URL    | Zeichenfolge | ja      | Die ID des wieder zu erlefenden Pakets.
VERSION        | URL    | Zeichenfolge | ja      | Die Version des Pakets, das wieder hergestellt werden soll.
X-nuget-APIKey | Header | Zeichenfolge | ja      | Zum Beispiel, `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Antwort

Statuscode | Bedeutung
----------- | -------
200         | Das Paket ist jetzt aufgeführt.
404         | Es ist kein Paket mit dem angegebenen vorhanden `ID` und `VERSION` vorhanden.
