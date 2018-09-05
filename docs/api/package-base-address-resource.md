---
title: Paketinhalt, NuGet-API
description: Die Basisadresse des Pakets ist eine einfache Schnittstelle für das Paket selbst abrufen.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 740defc34077793b81fb35db73a2eee393ae3bac
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547153"
---
# <a name="package-content"></a>Paketinhalt

Es ist möglich, eine URL zum Abrufen des Pakets ein beliebiger Inhalt (die NUPKG-Datei) mithilfe der V3-API zu generieren. Die Ressource, die zum Abrufen von Paketinhalt ist die `PackageBaseAddress` Ressource finden Sie in der [dienstindex](service-index.md). Diese Ressource ermöglicht auch die Ermittlung aller Versionen des Pakets aufgelistet oder nicht aufgeführt.

Diese Ressource wird häufig als entweder die "Paket Basisadresse" oder "Flatfile-Container" bezeichnet.

## <a name="versioning"></a>Versionskontrolle

Die folgenden `@type` Wert wird verwendet:

@type-Wert              | Hinweise
------------------------ | -----
PackageBaseAddress/3.0.0 | Die erste Version

## <a name="base-url"></a>Basis-URL

Die base-URL für die folgenden APIs ist der Wert des der `@id` -Eigenschaft zusammen mit den oben genannten Ressourcen `@type` Wert. Basis-URL im folgenden Dokument der Platzhalter `{@id}` verwendet werden.

## <a name="http-methods"></a>HTTP-Methoden

Alle URLs finden Sie in die Registrierung Unterstützung der HTTP-Methoden `GET` und `HEAD`.

## <a name="enumerate-package-versions"></a>Auflisten von Paketversionen

Wenn der Client eine Paket-ID kann und ermitteln möchte, die Paket-Versionen des Pakets Quelle zur Verfügung stehen, die der Client kann eine vorhersagbare URL zum Auflisten aller Versionen des Pakets zu erstellen. Diese Liste soll eine "Liste" werden für die unten genannten Content Package-API.

> [!Note]
> Diese Liste enthält die beiden Paketversionen aufgeführt werden und nicht aufgeführte.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Anforderungsparameter

name     | In     | Typ    | Erforderlich | Hinweise
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | Zeichenfolge  | ja      | Die Paket-ID Kleinbuchstaben

Die `LOWER_ID` Wert ist die gewünschte Paket-ID Kleinbuchstaben geändert, mithilfe von implementierten Regeln entspricht. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Methode.

### <a name="response"></a>Antwort

Wenn die Paketquelle keine Versionen der angegebenen Paket-ID verfügt, wird Statuscode 404 zurückgegeben.

Wenn die Paketquelle eine oder mehrere Versionen verfügt, wird ein Statuscode "200" zurückgegeben. Der Antworttext ist ein JSON-Objekt mit der folgenden Eigenschaft:

name     | Typ             | Erforderlich | Hinweise
-------- | ---------------- | -------- | -----
Versionen | Array von Zeichenfolgen | ja      | Die Paket-IDs verfügbar

Die Zeichenfolgen in die `versions` Array sind alle Kleinbuchstaben geändert, [normalisiert NuGet-Versionszeichenfolgen](../reference/package-versioning.md#normalized-version-numbers). Die Versionszeichenfolgen enthalten keine SemVer 2.0.0-Build-Metadaten.

Die Absicht ist, finden Sie in diesem Array die Versionszeichenfolgen wörtlich können, können Sie für verwendet werden die `LOWER_VERSION` Token finden Sie in den folgenden Endpunkten.

### <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Paketinhalt (NUPKG-Datei) herunterladen

Wenn der Client weiß, ein Paket-ID und die Version dass und den Paketinhalt herunterladen möchte, müssen sie nur die folgende URL zu erstellen:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>Anforderungsparameter

name          | In     | Typ   | Erforderlich | Hinweise
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | Zeichenfolge | ja      | Die Paket-ID Kleinbuchstaben
LOWER_VERSION | URL    | Zeichenfolge | ja      | Die Paketversion, normalisiert, und klein schreiben

Beide `LOWER_ID` und `LOWER_VERSION` sind klein schreiben, die mithilfe von implementierten Regeln entspricht. NET [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
-Methode.

Die `LOWER_VERSION` wird mithilfe NuGets-Version die gewünschten Paketversion normalisiert [Normalisierungsregeln](../reference/package-versioning.md#normalized-version-numbers). Dies bedeutet, dass dieser Build-Metadaten, die von der SemVer 2.0.0-Spezifikation darf in diesem Fall ausgeschlossen werden sollen.

### <a name="response-body"></a>Antworttext

Wenn das Paket auf die Paketquelle vorhanden ist, wird ein Statuscode "200" zurückgegeben. Der Antworttext werden der Inhalt des Pakets selbst.

Wenn das Paket auf die Paketquelle nicht vorhanden ist, wird der Statuscode 404 zurückgegeben.

### <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Beispielantwort

Der binäre Stream, der die NUPKG-Datei für "newtonsoft.JSON 9.0.1" ist.

## <a name="download-package-manifest-nuspec"></a>Das Paketmanifest (.nuspec) herunterladen

Wenn der Client weiß, ein Paket-ID und die Version dass und das Paketmanifest laden möchte, müssen sie nur die folgende URL zu erstellen:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>Anforderungsparameter

name          | In     | Typ    | Erforderlich | Hinweise
------------- | ------ | ------- | -------- | -----
LOWER_ID      | URL    | Zeichenfolge  | ja      | Die Paket-ID Kleinbuchstaben
LOWER_VERSION | URL    | Ganze Zahl | ja      | Die Paketversion, normalisiert, und klein schreiben

Beide `LOWER_ID` und `LOWER_VERSION` sind klein schreiben, die mithilfe von implementierten Regeln entspricht. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Methode.

Die `LOWER_VERSION` wird mithilfe NuGets-Version die gewünschten Paketversion normalisiert [Normalisierungsregeln](../reference/package-versioning.md#normalized-version-numbers). Dies bedeutet, dass dieser Build-Metadaten, die von der SemVer 2.0.0-Spezifikation darf in diesem Fall ausgeschlossen werden sollen.

### <a name="response-body"></a>Antworttext

Wenn das Paket auf die Paketquelle vorhanden ist, wird ein Statuscode "200" zurückgegeben. Der Antworttext werden das Paketmanifest, das im Abschnitt in der entsprechenden NUPKG-Datei enthalten ist. Im Abschnitt ist ein XML-Dokument.

Wenn das Paket auf die Paketquelle nicht vorhanden ist, wird der Statuscode 404 zurückgegeben.

### <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Beispielantwort

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
