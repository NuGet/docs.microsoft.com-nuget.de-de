---
title: Mithilfe von Push übertragen Sie und zu löschen Sie, NuGet-API
description: Publish-Diensts kann Clients Veröffentlichen neuer Pakete und aus der Liste entfernen oder löschen vorhandene Pakete an.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: ad66d8e0ffda13aaef744104c213863b0e111e0e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547520"
---
# <a name="push-and-delete"></a>Mithilfe von Push übertragen und löschen

Es ist möglich, mithilfe von Push übertragen, löschen (oder aus der Liste entfernen, je nach serverimplementierung), und stellen Sie Pakete mithilfe der NuGet-API V3. Diese Vorgänge sind basierend auf den `PackagePublish` Ressource finden Sie in der [dienstindex](service-index.md).

## <a name="versioning"></a>Versionskontrolle

Die folgenden `@type` Wert wird verwendet:

@type-Wert          | Hinweise
-------------------- | -----
PackagePublish/2.0.0 | Die erste Version

## <a name="base-url"></a>Basis-URL

Die base-URL für die folgenden APIs ist der Wert des der `@id` Eigenschaft der `PackagePublish/2.0.0` Ressource in der Paketquelle [dienstindex](service-index.md). Die folgende Dokumentation dient Nuget.org URL. Betrachten Sie `https://www.nuget.org/api/v2/package` als Platzhalter für die `@id` Wert in der dienstindex gefunden.

Beachten Sie, dass diese URL, am gleichen Speicherort wie die legacy-V2-Push-Endpunkt, verweist da das Protokoll identisch ist.

## <a name="http-methods"></a>HTTP-Methoden

Die `PUT`, `POST` und `DELETE` HTTP-Methoden werden durch diese Ressource unterstützt. Welche Methoden für jeden Endpunkt unterstützt werden finden Sie unten.

## <a name="push-a-package"></a>Ein Paket mithilfe von Push übertragen

> [!Note]
> "NuGet.org" verfügt über [zusätzliche Anforderungen](NuGet-Protocols.md) für die Interaktion mit der Push-Endpunkt.

NuGet.org unterstützt Ablegevorgänge neuer Pakete mithilfe der folgenden-API. Wenn das Paket mit der angegebenen ID und Version bereits vorhanden ist, lehnt nuget.org den Push. Anderen Paketquellen unterstützen möglicherweise das Ersetzen eines vorhandenen Pakets.

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a>Anforderungsparameter

name           | In     | Typ   | Erforderlich | Hinweise
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Header | Zeichenfolge | ja      | Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`

Die API-Schlüssel ist eine nicht transparente Zeichenfolge, aus der Paketquelle vom Benutzer abgerufen und in den Client konfiguriert. Kein besonderes Zeichenfolgenformat wird vorgeschrieben, aber der API-Schlüssel sollte nicht länger als eine angemessene Größe für HTTP-Headerwerte.

### <a name="request-body"></a>Anforderungstext

Der Anforderungstext muss in der folgenden Form stehen:

#### <a name="multipart-form-data"></a>Mehrteilige Formulardaten

Der Anforderungsheader `Content-Type` ist `multipart/form-data` und das erste Element im Hauptteil Anforderung ist die unformatierten Bytes des der NUPKG-Datei mithilfe von Push übertragen wird. Nachfolgende Elemente in den mehrteiligen Text werden ignoriert. Der Dateiname oder anderen Header der mehrteiligen Elemente werden ignoriert.

### <a name="response"></a>Antwort

Statuscode | Bedeutung
----------- | -------
201, 202    | Das Paket wurde erfolgreich per Push übertragen
400         | Das angegebene Paket ist ungültig.
409         | Ein Paket mit der angegebenen ID und Version ist bereits vorhanden.

Serverimplementierungen unterscheiden sich auf den Statuscode für Erfolg zurückgegeben, wenn ein Paket wurde erfolgreich per Push übertragen wird.

## <a name="delete-a-package"></a>Löschen eines Pakets

"NuGet.org" interpretiert, die Paket-Delete-Anforderung als eine "Auflistung aufheben". Dies bedeutet, dass das Paket noch für vorhandene Benutzer des Pakets verfügbar ist, aber das Paket nicht mehr angezeigt, in den Suchergebnissen oder in der Webschnittstelle wird. Weitere Informationen zu dieser Vorgehensweise finden Sie unter den [Pakete gelöscht](../policies/deleting-packages.md) Richtlinie. Andere serverimplementierungen können dieses Signal als ein hartes löschen interpretieren, vorläufiges löschen oder aus der Liste entfernen. Z. B. ["NuGet.Server"](https://www.nuget.org/packages/NuGet.Server) (eine Server-Implementierung unterstützt nur die älteren V2-API) unterstützt diese Anforderung verarbeitet, als ein Aufheben der Auflistung oder ein hartes löschen, die basierend auf einer Konfigurationsoption.

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>Anforderungsparameter

name           | In     | Typ   | Erforderlich | Hinweise
-------------- | ------ | ------ | -------- | -----
Id             | URL    | Zeichenfolge | ja      | Die ID des Pakets zu löschenden
VERSION        | URL    | Zeichenfolge | ja      | Die Version des zu löschenden Pakets
X-NuGet-ApiKey | Header | Zeichenfolge | ja      | Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Antwort

Statuscode | Bedeutung
----------- | -------
204         | Das Paket wurde gelöscht.
404         | Kein Paket mit dem angegebenen `ID` und `VERSION` vorhanden ist

## <a name="relist-a-package"></a>Neu Auflisten eines Pakets

Wenn ein Paket nicht aufgeführt ist, ist es möglich, das Paket wieder in den Suchergebnissen, die mit dem Endpunkt "Artikel" sichtbar zu machen. Dieser Endpunkt hat die gleiche Form wie die [löschen (aus der Liste entfernen) Endpunkt](#delete-a-package) verwendet jedoch die `POST` anstelle von HTTP-Methode der `DELETE` Methode.

Wenn das Paket bereits aufgeführt wird, ist die Anforderung immer noch erfolgreich.

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>Anforderungsparameter

name           | In     | Typ   | Erforderlich | Hinweise
-------------- | ------ | ------ | -------- | -----
Id             | URL    | Zeichenfolge | ja      | Die ID des Pakets, die neu auflisten
VERSION        | URL    | Zeichenfolge | ja      | Die Version des Pakets neu auflisten
X-NuGet-ApiKey | Header | Zeichenfolge | ja      | Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Antwort

Statuscode | Bedeutung
----------- | -------
300         | Das Paket wird jetzt aufgeführt.
404         | Kein Paket mit dem angegebenen `ID` und `VERSION` vorhanden ist
