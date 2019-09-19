---
title: Paket Inhalt, nuget-API
description: Die Paketbasis Adresse ist eine einfache Schnittstelle zum Abrufen des Pakets selbst.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 7aea28d6224a89149aa33be035c82a45db3058f0
ms.sourcegitcommit: 1eda83ab537c86cc27316e7bc67f95a358766e63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2019
ms.locfileid: "71094116"
---
# <a name="package-content"></a>Paket Inhalt

Es ist möglich, eine URL zum Abrufen des Inhalts eines beliebigen Pakets (die nupkg-Datei) mit der V3-API zu generieren. Die Ressource, die zum Abrufen von Paket Inhalten verwendet `PackageBaseAddress` wird, ist die Ressource, die im [Dienst Index](service-index.md)gefunden wurde. Diese Ressource ermöglicht außerdem die Ermittlung aller Versionen eines Pakets, die aufgelistet oder nicht aufgelistet sind.

Diese Ressource wird im Allgemeinen als "Paketbasis Adresse" oder als "flatcontainer" bezeichnet.

## <a name="versioning"></a>Versionskontrolle

Der folgende `@type` Wert wird verwendet:

@type -Wert              | Hinweise
------------------------ | -----
PackageBaseAddress/3.0.0 | Die erste Version

## <a name="base-url"></a>Basis-URL

Die Basis-URL für die folgenden APIs ist der Wert der `@id` Eigenschaft, die dem oben erwähnten `@type` Ressourcen Wert zugeordnet ist. Im folgenden Dokument wird die Platzhalter-Basis- `{@id}` URL verwendet.

## <a name="http-methods"></a>HTTP-Methoden

Alle URLs, die in der Registrierungs Ressource gefunden werden, `GET` unter `HEAD`stützen die HTTP-Methoden und.

## <a name="enumerate-package-versions"></a>Auflisten von Paketversionen

Wenn der Client eine Paket-ID kennt und ermitteln möchte, welche Paketversionen von der Paketquelle verfügbar sind, kann der Client eine vorhersagbare URL zum Auflisten aller Paketversionen erstellen. Diese Liste ist als "Verzeichnis Auflistung" für die weiter unten erwähnte Paket Inhalts-API gedacht.

> [!Note]
> Diese Liste enthält sowohl die aufgelisteten als auch die nicht aufgelisteten Paketversionen.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Anforderungs Parameter

name     | In     | Typ    | Erforderlich | Hinweise
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | Zeichenfolge  | ja      | Die Paket-ID, Kleinbuchstaben

Der `LOWER_ID` Wert ist die gewünschte Paket-ID in Kleinbuchstaben unter Verwendung der Regeln, die von implementiert werden. NET- [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Methode.

### <a name="response"></a>Antwort

Wenn die Paketquelle keine Versionen der angegebenen Paket-ID enthält, wird ein 404-Statuscode zurückgegeben.

Wenn die Paketquelle mindestens eine Version aufweist, wird ein 200-Statuscode zurückgegeben. Der Antworttext ist ein JSON-Objekt mit der folgenden Eigenschaft:

Name     | Typ             | Erforderlich | Hinweise
-------- | ---------------- | -------- | -----
Versionen | Array von Zeichen folgen | ja      | Verfügbare Versionen

Die Zeichen folgen im `versions` Array sind alle in Kleinbuchstaben, [normalisierten nuget-Versions](../concepts/package-versioning.md#normalized-version-numbers)Zeichenfolgen. Die Versions Zeichenfolgen enthalten keine semver 2.0.0 Build-Metadaten.

Der Zweck ist, dass die in diesem Array gefundenen Versions Zeichenfolgen wörtlich für die `LOWER_VERSION` Token verwendet werden können, die in den folgenden Endpunkten gefunden werden.

### <a name="sample-request"></a>Beispiel Anforderung

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Beispiel Antwort

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Paket Inhalt herunterladen (nupkg-Datei)

Wenn der Client eine Paket-ID und-Version kennt und den Paket Inhalt herunterladen möchte, muss er lediglich die folgende URL erstellen:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>Anforderungs Parameter

name          | In     | Typ   | Erforderlich | Hinweise
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | Zeichenfolge | ja      | Die Paket-ID, Kleinbuchstaben
LOWER_VERSION | URL    | Zeichenfolge | ja      | Die Paketversion, normalisierte und Kleinbuchstaben

Sowohl `LOWER_ID` als `LOWER_VERSION` auch werden mithilfe der von implementierten Regeln in Kleinbuchstaben geschrieben. NET es[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
-Methode.

Die `LOWER_VERSION` ist die gewünschte Paketversion, die mithilfe von nuget-Versions [normalisierungs Regeln](../concepts/package-versioning.md#normalized-version-numbers)normalisiert wird. Dies bedeutet, dass buildmetadaten, die von der semver 2.0.0-Spezifikation zugelassen werden, in diesem Fall ausgeschlossen werden müssen.

### <a name="response-body"></a>Antworttext

Wenn das Paket in der Paketquelle vorhanden ist, wird ein 200-Statuscode zurückgegeben. Der Antworttext ist der Paket Inhalt selbst.

Wenn das Paket nicht in der Paketquelle vorhanden ist, wird der Statuscode 404 zurückgegeben.

### <a name="sample-request"></a>Beispiel Anforderung

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Beispiel Antwort

Der binäre Stream, bei dem es sich um die nupkg-9.0.1 für newtonsoft. JSON handelt.

## <a name="download-package-manifest-nuspec"></a>Paket Manifest herunterladen (. nuspec)

Wenn der Client eine Paket-ID und-Version kennt und das Paket Manifest herunterladen möchte, muss nur die folgende URL erstellt werden:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>Anforderungs Parameter

name          | In     | Typ   | Erforderlich | Hinweise
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | Zeichenfolge | ja      | Die Paket-ID, Kleinbuchstaben
LOWER_VERSION | URL    | Zeichenfolge | ja      | Die Paketversion, normalisierte und Kleinbuchstaben

Sowohl `LOWER_ID` als `LOWER_VERSION` auch werden mithilfe der von implementierten Regeln in Kleinbuchstaben geschrieben. NET- [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Methode.

Die `LOWER_VERSION` ist die gewünschte Paketversion, die mithilfe von nuget-Versions [normalisierungs Regeln](../concepts/package-versioning.md#normalized-version-numbers)normalisiert wird. Dies bedeutet, dass buildmetadaten, die von der semver 2.0.0-Spezifikation zugelassen werden, in diesem Fall ausgeschlossen werden müssen.

### <a name="response-body"></a>Antworttext

Wenn das Paket in der Paketquelle vorhanden ist, wird ein 200-Statuscode zurückgegeben. Der Antworttext ist das Paket Manifest, bei dem es sich um die nuspec-Datei im entsprechenden nupkg-Element handelt. Die nuspec-Datei ist ein XML-Dokument.

Wenn das Paket nicht in der Paketquelle vorhanden ist, wird der Statuscode 404 zurückgegeben.

### <a name="sample-request"></a>Beispiel Anforderung

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Beispiel Antwort

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
