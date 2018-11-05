---
title: nuget.org-Protokolle
description: Die sich entwickelnden Protokolle bei nuget.org für die Interaktion mit NuGet-Clients.
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
# <a name="nugetorg-protocols"></a>nuget.org-Protokolle

Zum Interagieren mit nuget.org müssen Clients bestimmte Protokolle nutzen. Da diese Protokolle sich immer weiterentwickeln, müssen Clients die von ihnen genutzte Protokollversion angeben, wenn sie bestimmte nuget.org-APIs aufrufen. Dadurch kann nuget.org Änderungen einführen und mit alten Clients kompatibel bleiben.

> [!Note]
> Die hier dokumentierten APIs sind spezifisch für nuget.org, und es wird von anderen NuGet-Serverimplementierungen nicht erwartet, dass sie diese APIs einführen. 

Weitere Informationen zur NuGet-API, die im NuGet-Ökosystem weitgehend implementiert ist, finden Sie in der [API-Übersicht](overview.md).

Dieses Thema listet verschiedene Protokolle auf, sobald diese eingeführt werden.

## <a name="nuget-protocol-version-410"></a>NuGet-Protokoll, Version 4.1.0

Die 4.1.0 Protokoll gibt an, die Nutzung der überprüfen-Scope-Schlüssel für die Interaktion mit anderen Diensten als "NuGet.org", um ein Paket mit einem nuget.org-Konto zu überprüfen. Beachten Sie, dass die `4.1.0` Version ist eine nicht transparente Zeichenfolge wurden jedoch zufällig mit der ersten Version des offiziellen NuGet-Clients übereinstimmen, die dieses Protokoll unterstützt.

Überprüfung wird sichergestellt, dass der Benutzer erstellte API-Schlüssel werden nur mit nuget.org verwendet, und diese anderen der Überprüfung oder der Überprüfung von einem Drittanbieter-Dienst über eine einmalige Verwendung überprüfen-Scope-Schlüssel erfolgt. Diese überprüfen-Scope-Schlüssel können verwendet werden, um sicherzustellen, dass das Paket an einen bestimmten Benutzer (Konto), die auf nuget.org gehört.

### <a name="client-requirement"></a>Client-Anforderung

Clients müssen die folgenden Header übergeben werden soll, wenn sie API-Aufrufen **Push** Pakete auf nuget.org:

    X-NuGet-Protocol-Version: 4.1.0

Beachten Sie, dass der Header `X-NuGet-Client-Version` eine ähnliche Semantik benutzt, aber für die ausschließliche Nutzung durch den offiziellen NuGet-Client vorgesehen ist. Clients von Drittanbietern sollten den Header und Wert `X-NuGet-Protocol-Version` nutzen.

Das **Push**-Protokoll selbst wird in der Dokumentation für die [`PackagePublish`-Ressource](package-publish-resource.md) beschrieben.

Wenn ein Client mit externen Diensten und Anforderungen interagiert und überprüfen muss, ob ein Paket einem bestimmten Benutzer (Konto) gehört, sollte er das folgende Protokoll und die "Verify Scope"-Schlüssel, nicht die API-Schlüssel von nuget.org, verwenden.

### <a name="api-to-request-a-verify-scope-key"></a>API, um einen "Verify Scope"-Schlüssel anzufordern

Diese API wird genutzt, um einen "Verify Scope"-Schlüssel anzufordern, damit ein nuget.org-Autor ein Paket validieren kann, das ihm/ihr gehört.

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>Anforderungsparameter

Name           | In     | Typ   | Erforderlich | Hinweise
-------------- | ------ | ------ | -------- | -----
ID             | URL    | String | ja      | Die Paket-ID, für die der Schlüssel angefordert wird
VERSION        | URL    | String | nein       | Die Paketversion
X-NuGet-ApiKey | Header | String | ja      | beispielsweise `X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>Antwort

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API, um den "Verify Scope"-Schlüssel zu überprüfen

Diese API wird verwendet, um einen "Verify Scope"-Schlüssel für ein Paket zu überprüfen.

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>Anforderungsparameter

name           | In     | Typ   | Erforderlich | Hinweise
-------------  | ------ | ------ | -------- | -----
Id             | URL    | Zeichenfolge | ja      | Die Paket-ID für die der Schlüssel des überprüfen Bereich angefordert wird
VERSION        | URL    | Zeichenfolge | Nein       | Die Paketversion
X-NuGet-ApiKey | Header | Zeichenfolge | ja      | Beispiel: `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> Dieser "Verify Scope"-Schlüssel läuft nach einem Tag oder der ersten Nutzung ab.

#### <a name="response"></a>Antwort

Statuscode | Bedeutung
----------- | -------
200         | Der API-Schlüssel ist gültig.
403         | Der API-Schlüssel ist ungültig oder für dieses Paket nicht autorisiert
404         | Das Paket, das mit `ID` und (optional) `VERSION` angegeben wurde, existiert nicht
