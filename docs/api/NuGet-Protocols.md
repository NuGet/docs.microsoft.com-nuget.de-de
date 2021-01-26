---
title: nuget.org-Protokolle
description: Die sich entwickelnden nuget.org-Protokolle für die Interaktion mit nuget-Clients.
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773977"
---
# <a name="nugetorg-protocols"></a>nuget.org-Protokolle

Um mit nuget.org interagieren zu können, müssen Clients bestimmte Protokolle einhalten. Da diese Protokolle weiterentwickelt werden, müssen Clients die Protokollversion identifizieren, die Sie beim Aufrufen spezifischer nuget.org-APIs verwenden. Dies ermöglicht es nuget.org, Änderungen für die alten Clients in einer nicht unterbrechend orientierten Weise einzuführen.

> [!Note]
> Die auf dieser Seite dokumentierten APIs sind spezifisch für nuget.org, und es wird nicht erwartet, dass andere nuget-Server Implementierungen diese APIs einführen. 

Weitere Informationen über die nuget-API, die im gesamten nuget-Ökosystem implementiert ist, finden Sie in der [API-Übersicht](overview.md).

In diesem Thema werden verschiedene Protokolle als und wann Sie vorhanden sind aufgeführt.

## <a name="nuget-protocol-version-410"></a>Nuget-Protokollversion 4.1.0

Das 4.1.0-Protokoll gibt die Verwendung von Verify-Scope-Schlüsseln für die Interaktion mit anderen Diensten als nuget.org an, um ein Paket mit einem nuget.org-Konto zu validieren. Beachten Sie, dass die `4.1.0` Versionsnummer eine nicht transparente Zeichenfolge ist, aber mit der ersten Version des offiziellen nuget-Clients übereinstimmt, der dieses Protokoll unterstützt hat.

Bei der Validierung wird sichergestellt, dass die vom Benutzer erstellten API-Schlüssel nur mit nuget.org verwendet werden, und dass eine andere Überprüfung oder Validierung von einem Drittanbieter Dienst über die einmalige Verwendung von Verify-Scope-Schlüsseln verarbeitet wird. Diese Schlüssel zum Überprüfen des Bereichs können verwendet werden, um zu überprüfen, ob das Paket zu einem bestimmten Benutzer (Konto) auf nuget.org gehört.

### <a name="client-requirement"></a>Client Anforderung

Clients müssen den folgenden Header übergeben, wenn Sie API-Aufrufe **zum Übertragen von Paketen an** nuget.org durchführen:

```
X-NuGet-Protocol-Version: 4.1.0
```

Beachten Sie, dass der `X-NuGet-Client-Version` Header eine ähnliche Semantik hat, aber nur für den offiziellen nuget-Client verwendet werden kann. Clients von Drittanbietern sollten den `X-NuGet-Protocol-Version` -Header und den-Wert verwenden.

Das **pushprotokoll** selbst wird in der Dokumentation für die [ `PackagePublish` Ressource](package-publish-resource.md)beschrieben.

Wenn ein Client mit externen Diensten interagiert und überprüft werden muss, ob ein Paket zu einem bestimmten Benutzer (Konto) gehört, sollte er das folgende Protokoll verwenden und die Schlüssel für den Verifizierungs Bereich und nicht die API-Schlüssel von nuget.org verwenden.

### <a name="api-to-request-a-verify-scope-key"></a>API zum Anfordern eines Verifizierungs Bereichs Schlüssels

Diese API wird verwendet, um einen Schlüssel zum Überprüfen des Bereichs zu erhalten, damit ein nuget.org-Autor ein Paket überprüfen kann, das sich im Besitz von ihm befindet

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Anforderungsparameter

Name           | In     | Typ   | Erforderlich | Notizen
-------------- | ------ | ------ | -------- | -----
id             | URL    | Zeichenfolge | ja      | Der paketidentierer, für den der Gültigkeits Bereichs Schlüssel angefordert wird.
VERSION        | URL    | Zeichenfolge | nein       | Die Paketversion
X-nuget-APIKey | Header | Zeichenfolge | ja      | Zum Beispiel, `X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>Antwort

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API zum Überprüfen des Gültigkeits Bereichs Schlüssels

Diese API wird verwendet, um einen Schlüssel zum Überprüfen des Bereichs für das Paket zu überprüfen, das im Besitz von nuget.org Author ist

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Anforderungsparameter

Name           | In     | Typ   | Erforderlich | Notizen
-------------  | ------ | ------ | -------- | -----
id             | URL    | Zeichenfolge | ja      | Der Paket Bezeichner, für den der Schlüssel zum Überprüfen des Bereichs angefordert wird
VERSION        | URL    | Zeichenfolge | nein       | Die Paketversion
X-nuget-APIKey | Header | Zeichenfolge | ja      | Zum Beispiel, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> Dieser Gültigkeitsbereich-API-Schlüssel läuft in einem Tag oder bei der ersten Verwendung ab, je nachdem, welcher Fall zuerst eintritt.

#### <a name="response"></a>Antwort

Statuscode | Bedeutung
----------- | -------
200         | Der API-Schlüssel ist gültig.
403         | Der API-Schlüssel ist ungültig oder nicht zum Pushen des Pakets autorisiert.
404         | Das Paket, auf das `ID` und `VERSION` (optional) verwiesen wird, ist nicht vorhanden.
