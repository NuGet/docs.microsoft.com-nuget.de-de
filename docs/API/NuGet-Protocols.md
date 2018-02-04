---
title: NuGet.org-Protokolle | Microsoft Docs
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: Die Interaktion mit NuGet-Clients sich entwickelnden nuget.org-Protokolle.
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 488a86a36a6bc83c91f0182bf437ddb83e707e31
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="nugetorg-protocols"></a>NuGet.org-Protokolle

Um mit nuget.org interagieren, müssen Clients bestimmte Protokolle zu befolgen. Da diese Protokolle weiterentwickelt beizubehalten, müssen Clients die Protokollversion identifizieren nutzen, wenn bestimmte nuget.org-APIs aufrufen. Dadurch können nuget.org einführen von Änderungen auf eine nicht unterbrechende Weise für die alten Clients.

> [!Note]
> Auf dieser Seite dokumentierten APIs für nuget.org spezifisch sind, und es ist nicht davon ausgehen, bei anderen Implementierungen des NuGet-Server diese APIs einzuführen. 

Weitere Informationen über die NuGet-API, die allgemein für den NuGet-Ökosystem implementiert, finden Sie unter der [Übersicht über die API](overview.md).

Dieses Thema enthält verschiedene Protokolle wie und wann sie auf Vorhandensein eintreffen.

## <a name="nuget-protocol-version-410"></a>NuGet-Protokollversion 4.1.0

Die 4.1.0 Protokoll gibt die Verwendung der überprüfen Bereich Schlüssel für die Interaktion mit Dienste als nuget.org, um ein Paket mit einem nuget.org-Konto zu überprüfen. Beachten Sie, dass die `4.1.0` Version ist eine nicht transparente Zeichenfolge jedoch geschieht mit den in der Regel mit der ersten Version des offiziellen NuGet-Clients, die dieses Protokoll unterstützt.

Überprüfung wird sichergestellt, dass die benutzerdefinierte API-Schlüssel werden nur mit nuget.org verwendet, und dieser anderen Überprüfung oder Validierung von einem Drittanbieter-Dienst über einen einmaligen Verwendung überprüfen Bereich Schlüssel behandelt wird. Diese Schlüssel überprüfen Bereich können verwendet werden, um sicherzustellen, dass das Paket nach einem bestimmten Benutzer (Konto) auf nuget.org gehört.

### <a name="client-requirement"></a>Client-Anforderung

Clients müssen die folgenden Header übergeben werden soll, wenn sie API-Aufrufe an Stellen **Push** zu nuget.org Pakete:

    X-NuGet-Protocol-Version: 4.1.0

Beachten Sie, dass die `X-NuGet-Client-Version` Header weist eine ähnliche Semantik jedoch reserviert nur durch den offiziellen NuGet-Client verwendet werden. Clients von Drittanbietern verwenden sollten die `X-NuGet-Protocol-Version` Header und Wert.

Die **Push** Protokoll selbst wird beschrieben, in der Dokumentation für die [ `PackagePublish` Ressource](package-publish-resource.md).

Wenn ein Client mit externen Diensten und Anforderungen interagiert zu prüfen, ob ein Paket zu einem bestimmten Benutzer (Konto) gehört, sollte Schlüssel überprüfen-Bereich und nicht der API-Schlüssel nuget.org verwenden das folgende Protokoll und verwendet werden.

### <a name="api-to-request-a-verify-scope-key"></a>API zum Anfordern eines Schlüssels überprüfen-Bereich

Diese API wird verwendet, um einen Schlüssel überprüfen-Bereich für einen nuget.org-Autor zum Überprüfen von Paketen im Besitz von ihn abzurufen.

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>Anforderungsparameter

name           | In     | Typ   | Erforderlich | Hinweise
-------------- | ------ | ------ | -------- | -----
Id             | URL    | Zeichenfolge | ja      | Die Paket-Identidier für die der überprüfen Bereich Schlüssel angefordert wird
VERSION        | URL    | Zeichenfolge | Nein       | Die Paketversion
X-NuGet-ApiKey | Header | Zeichenfolge | ja      | Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>Antwort

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>-API, um den Bereich-Schlüssel überprüfen Überprüfen

Diese API dient zum Überprüfen Bereich Schlüssel für den Autor nuget.org gehörige Paket zu überprüfen.

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>Anforderungsparameter

name           | In     | Typ   | Erforderlich | Hinweise
-------------  | ------ | ------ | -------- | -----
Id             | URL    | Zeichenfolge | ja      | Die Paket-ID für die der überprüfen Bereich Schlüssel angefordert wird
VERSION        | URL    | Zeichenfolge | Nein       | Die Paketversion
X-NuGet-ApiKey | Header | Zeichenfolge | ja      | Beispiel: `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> Diese überprüfen Bereich API-Schlüssel läuft ab, in einem Tag oder bei der ersten Verwendung, welcher Fall zuerst eintritt.

#### <a name="response"></a>Antwort

Statuscode | Bedeutung
----------- | -------
300         | Die API-Schlüssel ist ungültig
403         | API-Schlüssel ist ungültig oder nicht autorisierte für das Paket mithilfe von Push übertragen
404         | Das Paket verweist auf `ID` und `VERSION` (optional) ist nicht vorhanden
