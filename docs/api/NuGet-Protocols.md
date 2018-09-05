---
title: "\"NuGet.org\"-Protokolle"
description: Der sich entwickelnden "nuget.org"-Protokolle für die Interaktion mit NuGet-Clients.
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547272"
---
# <a name="nugetorg-protocols"></a>"NuGet.org"-Protokolle

Zum interagieren mit nuget.org müssen Sie bestimmte Protokolle zu folgen. Da diese Protokolle Weiterentwicklung zu halten, müssen Clients die Version des Protokolls identifizieren nutzen, wenn bestimmte nuget.org APIs aufrufen. Dadurch wird ein "NuGet.org", um die Änderungen auf eine nicht unterbrechende Weise eingeführt werden, für die alten Clients.

> [!Note]
> Auf dieser Seite dokumentierten APIs beziehen sich auf nuget.org aus, und es gibt keine Erwartungen an andere NuGet-Server-Implementierungen diese APIs einführen. 

Weitere Informationen über die NuGet-API, die allgemein für die NuGet-Ökosystem implementiert, finden Sie unter den [-API – Übersicht](overview.md).

Dieses Thema enthält verschiedene Protokolle wie und wann sie zu Vorhandensein stammen.

## <a name="nuget-protocol-version-410"></a>NuGet Protocol, Version 4.1.0

Die 4.1.0 Protokoll gibt an, die Nutzung der überprüfen-Scope-Schlüssel für die Interaktion mit anderen Diensten als "NuGet.org", um ein Paket mit einem nuget.org-Konto zu überprüfen. Beachten Sie, dass die `4.1.0` Version ist eine nicht transparente Zeichenfolge wurden jedoch zufällig mit der ersten Version des offiziellen NuGet-Clients übereinstimmen, die dieses Protokoll unterstützt.

Überprüfung wird sichergestellt, dass der Benutzer erstellte API-Schlüssel werden nur mit nuget.org verwendet, und diese anderen der Überprüfung oder der Überprüfung von einem Drittanbieter-Dienst über eine einmalige Verwendung überprüfen-Scope-Schlüssel erfolgt. Diese überprüfen-Scope-Schlüssel können verwendet werden, um sicherzustellen, dass das Paket an einen bestimmten Benutzer (Konto), die auf nuget.org gehört.

### <a name="client-requirement"></a>Client-Anforderung

Clients müssen die folgenden Header übergeben werden soll, wenn sie API-Aufrufen **Push** Pakete auf nuget.org:

    X-NuGet-Protocol-Version: 4.1.0

Beachten Sie, dass die `X-NuGet-Client-Version` Header weist eine ähnliche Semantik, sondern wird reserviert, um nur von der offiziellen NuGet-Client verwendet werden. Clients von Drittanbietern verwenden, sollten die `X-NuGet-Protocol-Version` Header und Wert.

Die **Push** Protokoll selbst wird beschrieben, in der Dokumentation für die [ `PackagePublish` Ressource](package-publish-resource.md).

Wenn ein Client mit externen Diensten und Anforderungen interagiert zu prüfen, ob ein Paket zu einem bestimmten Benutzer (Konto) gehört, muss das folgende Protokoll verwenden und überprüfen-Scope-Schlüssel und nicht die API-Schlüssel von nuget.org verwenden.

### <a name="api-to-request-a-verify-scope-key"></a>-API, um einen Bereich überprüfen Schlüssel anfordern

Abrufen eines Schlüssels überprüfen-Bereich für den Autor eines "NuGet.org", um ein Paket, das im Besitz von eines Gastbenutzers zu überprüfen, wird diese API verwendet.

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>Anforderungsparameter

name           | In     | Typ   | Erforderlich | Hinweise
-------------- | ------ | ------ | -------- | -----
Id             | URL    | Zeichenfolge | ja      | Die Paket-Identidier für die der Schlüssel des überprüfen Bereich angefordert wird
VERSION        | URL    | Zeichenfolge | Nein       | Die Paketversion
X-NuGet-ApiKey | Header | Zeichenfolge | ja      | Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>Antwort

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API, um zu überprüfen, ob den Schlüssel der überprüfen-Bereich

Diese API wird verwendet, um überprüfen-Scope-Schlüssel für der Autor von "NuGet.org" gehörige Paket zu überprüfen.

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>Anforderungsparameter

name           | In     | Typ   | Erforderlich | Hinweise
-------------  | ------ | ------ | -------- | -----
Id             | URL    | Zeichenfolge | ja      | Die Paket-ID für die der Schlüssel des überprüfen Bereich angefordert wird
VERSION        | URL    | Zeichenfolge | Nein       | Die Paketversion
X-NuGet-ApiKey | Header | Zeichenfolge | ja      | Beispiel: `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> Dieser Bereich API-Schlüssel stellen Sie sicher, die in einen ganzen Tag läuft ab, oder bei der ersten Verwendung, welcher Fall zuerst eintritt.

#### <a name="response"></a>Antwort

Statuscode | Bedeutung
----------- | -------
300         | Der API-Schlüssel ist gültig.
403         | Die API-Schlüssel ist ungültig oder nicht autorisiert, für das Paket mithilfe von Push übertragen
404         | Das Paket verweist `ID` und `VERSION` (optional) ist nicht vorhanden
