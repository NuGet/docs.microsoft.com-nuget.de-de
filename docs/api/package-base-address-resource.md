---
title: Paket Inhalt, nuget-API
description: Die Paketbasis Adresse ist eine einfache Schnittstelle zum Abrufen des Pakets selbst.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 8ea03ece635aa06e22032c4fb43ce932dbdf717c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773929"
---
# <a name="package-content"></a>Paketinhalt

Es ist möglich, eine URL zum Abrufen des Inhalts eines beliebigen Pakets (die nupkg-Datei) mit der V3-API zu generieren. Die Ressource, die zum Abrufen von Paket Inhalten verwendet wird, ist die Ressource, die `PackageBaseAddress` im [Dienst Index](service-index.md)gefunden wurde. Diese Ressource ermöglicht außerdem die Ermittlung aller Versionen eines Pakets, die aufgelistet oder nicht aufgelistet sind.

Diese Ressource wird im Allgemeinen als "Paketbasis Adresse" oder als "flatcontainer" bezeichnet.

## <a name="versioning"></a>Versionsverwaltung

Der folgende `@type` Wert wird verwendet:

Wert vom Typ @type              | Hinweise
------------------------ | -----
Packagebaseaddress/3.0.0 | Die erste Version

## <a name="base-url"></a>Basis-URL

Die Basis-URL für die folgenden APIs ist der Wert der `@id` Eigenschaft, die dem oben erwähnten Ressourcen Wert zugeordnet ist `@type` . Im folgenden Dokument wird die Platzhalter-Basis-URL `{@id}` verwendet.

## <a name="http-methods"></a>HTTP-Methoden

Alle URLs, die in der Registrierungs Ressource gefunden werden, unterstützen die HTTP `GET` -Methoden und `HEAD` .

## <a name="enumerate-package-versions"></a>Auflisten von Paketversionen

Wenn der Client eine Paket-ID kennt und ermitteln möchte, welche Paketversionen von der Paketquelle verfügbar sind, kann der Client eine vorhersagbare URL zum Auflisten aller Paketversionen erstellen. Diese Liste ist als "Verzeichnis Auflistung" für die weiter unten erwähnte Paket Inhalts-API gedacht.

> [!Note]
> Diese Liste enthält sowohl die aufgelisteten als auch die nicht aufgelisteten Paketversionen.

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a>Anforderungsparameter

Name     | In     | Typ    | Erforderlich | Notizen
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | Zeichenfolge  | ja      | Die Paket-ID, Kleinbuchstaben

Der `LOWER_ID` Wert ist die gewünschte Paket-ID in Kleinbuchstaben unter Verwendung der Regeln, die von implementiert werden. NET- [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) Methode.

### <a name="response"></a>Antwort

Wenn die Paketquelle keine Versionen der angegebenen Paket-ID enthält, wird ein 404-Statuscode zurückgegeben.

Wenn die Paketquelle mindestens eine Version aufweist, wird ein 200-Statuscode zurückgegeben. Der Antworttext ist ein JSON-Objekt mit der folgenden Eigenschaft:

Name     | Typ             | Erforderlich | Notizen
-------- | ---------------- | -------- | -----
versions | array of strings | ja      | Verfügbare Versionen

Die Zeichen folgen im `versions` Array sind alle in Kleinbuchstaben, [normalisierten nuget-Versions](../concepts/package-versioning.md#normalized-version-numbers)Zeichenfolgen. Die Versions Zeichenfolgen enthalten keine semver 2.0.0 Build-Metadaten.

Der Zweck ist, dass die in diesem Array gefundenen Versions Zeichenfolgen wörtlich für die Token verwendet werden können, die `LOWER_VERSION` in den folgenden Endpunkten gefunden werden.

### <a name="sample-request"></a>Beispiel für eine Anforderung

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a>Beispiel für eine Antwort

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Paket Inhalt herunterladen (nupkg-Datei)

Wenn der Client eine Paket-ID und-Version kennt und den Paket Inhalt herunterladen möchte, muss er lediglich die folgende URL erstellen:

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a>Anforderungsparameter

Name          | In     | Typ   | Erforderlich | Notizen
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | Zeichenfolge | ja      | Die Paket-ID, Kleinbuchstaben
LOWER_VERSION | URL    | Zeichenfolge | ja      | Die Paketversion, normalisierte und Kleinbuchstaben

Sowohl `LOWER_ID` als auch `LOWER_VERSION` werden mithilfe der von implementierten Regeln in Kleinbuchstaben geschrieben. NET es [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true)
-Methode.

Die `LOWER_VERSION` ist die gewünschte Paketversion, die mithilfe von nuget-Versions [normalisierungs Regeln](../concepts/package-versioning.md#normalized-version-numbers)normalisiert wird. Dies bedeutet, dass buildmetadaten, die von der semver 2.0.0-Spezifikation zugelassen werden, in diesem Fall ausgeschlossen werden müssen.

### <a name="response-body"></a>Antworttext

Wenn das Paket in der Paketquelle vorhanden ist, wird ein 200-Statuscode zurückgegeben. Der Antworttext ist der Paket Inhalt selbst.

Wenn das Paket nicht in der Paketquelle vorhanden ist, wird der Statuscode 404 zurückgegeben.

### <a name="sample-request"></a>Beispiel für eine Anforderung

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a>Beispiel für eine Antwort

Der binäre Stream, bei dem es sich um die. nupkg-Newtonsoft.Jsauf 9.0.1 handelt.

## <a name="download-package-manifest-nuspec"></a>Paket Manifest herunterladen (. nuspec)

Wenn der Client eine Paket-ID und-Version kennt und das Paket Manifest herunterladen möchte, muss nur die folgende URL erstellt werden:

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a>Anforderungsparameter

Name          | In     | Typ   | Erforderlich | Notizen
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | Zeichenfolge | ja      | Die Paket-ID, Kleinbuchstaben
LOWER_VERSION | URL    | Zeichenfolge | ja      | Die Paketversion, normalisierte und Kleinbuchstaben

Sowohl `LOWER_ID` als auch `LOWER_VERSION` werden mithilfe der von implementierten Regeln in Kleinbuchstaben geschrieben. NET- [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) Methode.

Die `LOWER_VERSION` ist die gewünschte Paketversion, die mithilfe von nuget-Versions [normalisierungs Regeln](../concepts/package-versioning.md#normalized-version-numbers)normalisiert wird. Dies bedeutet, dass buildmetadaten, die von der semver 2.0.0-Spezifikation zugelassen werden, in diesem Fall ausgeschlossen werden müssen.

### <a name="response-body"></a>Antworttext

Wenn das Paket in der Paketquelle vorhanden ist, wird ein 200-Statuscode zurückgegeben. Der Antworttext ist das Paket Manifest, bei dem es sich um die nuspec-Datei im entsprechenden nupkg-Element handelt. Die nuspec-Datei ist ein XML-Dokument.

Wenn das Paket nicht in der Paketquelle vorhanden ist, wird der Statuscode 404 zurückgegeben.

### <a name="sample-request"></a>Beispiel für eine Anforderung

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a>Beispiel für eine Antwort

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
