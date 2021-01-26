---
title: Repository-Signaturen, nuget-API | Microsoft-Dokumentation
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: Mithilfe der Repository Signature-Ressource können von Clients Paketquellen Ihre Repository-Signatur Funktionen bekanntgegeben werden.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775336"
---
# <a name="repository-signatures"></a>Repository-Signaturen

Wenn eine Paketquelle das Hinzufügen von Repository-Signaturen zu veröffentlichten Paketen unterstützt, kann ein Client die Signatur Zertifikate ermitteln, die von der Paketquelle verwendet werden. Mit dieser Ressource können Clients erkennen, ob ein Repository-signiertes Paket manipuliert wurde oder über ein unerwartetes Signaturzertifikat verfügt.

Die Ressource, die zum Abrufen dieser Repository-Signatur Informationen verwendet wird, ist die Ressource, die `RepositorySignatures` im [Dienst Index](service-index.md)gefunden wurde.

## <a name="versioning"></a>Versionsverwaltung

Der folgende `@type` Wert wird verwendet:

Wert vom Typ @type                | Hinweise
-------------------------- | -----
RepositorySignatures/4.7.0 | Die erste Version
RepositorySignatures/4.9.0 | Unterstützt von nuget-Clients mit Version 4.9 und höher
RepositorySignatures/5.0.0 | Ermöglicht das Aktivieren von `allRepositorySigned` . Unterstützt von nuget-Clients mit Version 5.0 und höher

## <a name="base-url"></a>Basis-URL

Die Einstiegspunkt-URL für die folgenden APIs ist der Wert der `@id` Eigenschaft, die dem oben erwähnten Ressourcen Wert zugeordnet ist `@type` . In diesem Thema wird die Platzhalter-URL verwendet `{@id}` .

Beachten Sie, dass die URL im Gegensatz zu anderen Ressourcen `{@id}` über HTTPS bereitgestellt werden muss.

## <a name="http-methods"></a>HTTP-Methoden

Alle URLs, die in der Repository Signature-Ressource gefunden werden, unterstützen nur die HTTP `GET` -Methoden und `HEAD` .

## <a name="repository-signatures-index"></a>Repository-Signaturen-Index

Der Repository-Signatur Index enthält zwei Informationen:

1. Ob alle Pakete, die in der Quelle gefunden werden, von dieser Paketquelle signiert wurden.
1. Die Liste der Zertifikate, die von der Paketquelle zum Signieren von Paketen verwendet werden.

In den meisten Fällen wird die Liste der Zertifikate nur an angefügt. Neue Zertifikate werden der Liste hinzugefügt, wenn das vorherige Signaturzertifikat abgelaufen ist und die Paketquelle mit der Verwendung eines neuen Signatur Zertifikats beginnen muss. Wenn ein Zertifikat aus der Liste entfernt wird, bedeutet dies, dass alle mit dem entfernten Signaturzertifikat erstellten Paket Signaturen vom Client nicht mehr als gültig eingestuft werden. In diesem Fall ist die Paket Signatur (aber nicht unbedingt das Paket) ungültig. In einer Client Richtlinie kann die Installation des Pakets als nicht signiert zugelassen werden.

Im Fall einer Zertifikat Sperrung (z. b. ein wichtiger Kompromiss), wird von der Paketquelle erwartet, dass alle vom betroffenen Zertifikat signierten Pakete neu signiert werden. Außerdem sollte die Paketquelle das betroffene Zertifikat aus der Liste der Signatur Zertifikate entfernen.

Die folgende Anforderung Ruft den Repository-Signatur Index ab.

```
GET {@id}
```

Der Repository-Signatur Index ist ein JSON-Dokument, das ein-Objekt mit den folgenden Eigenschaften enthält:

Name                | Typ             | Erforderlich | Notizen
------------------- | ---------------- | -------- | -----
allRepositorySigned | boolean          | ja      | Muss sich `false` auf 4.7.0-und 4.9.0-Ressourcen befinden
signingzertifikate | Array von Objekten | ja      | 

Der `allRepositorySigned` boolesche Wert ist auf "false" festgelegt, wenn die Paketquelle über einige Pakete ohne Repository-Signatur verfügt. Wenn der boolesche Wert auf true festgelegt ist, müssen alle Pakete, die in der Quelle verfügbar sind, über eine Repository-Signatur verfügen, die von einem der Signatur Zertifikate in erstellt wird `signingCertificates` .

> [!Warning]
> Der `allRepositorySigned` boolesche Wert muss für die 4.7.0-und 4.9.0-Ressourcen den Wert false aufweisen. Die Clients für nuget v 4.7, v 4.8 und v 4.9 können Pakete nicht aus Quellen installieren, bei denen `allRepositorySigned` auf "true" festgelegt ist.

`signingCertificates`Wenn der `allRepositorySigned` boolesche Wert auf true festgelegt ist, muss ein oder mehrere Signatur Zertifikate im Array vorhanden sein. Wenn das Array leer ist und `allRepositorySigned` auf true festgelegt ist, sollten alle Pakete aus der Quelle als ungültig eingestuft werden, obwohl eine Client Richtlinie weiterhin die Verwendung von Paketen zulässt. Jedes Element in diesem Array ist ein JSON-Objekt mit den folgenden Eigenschaften.

Name         | Typ   | Erforderlich | Notizen
------------ | ------ | -------- | -----
contentUrl   | Zeichenfolge | ja      | Absolute URL zum der der-codierten öffentlichen Zertifikat
Abdrücke | object | ja      |
subject      | Zeichenfolge | ja      | Der Distinguished Name des Antragstellers aus dem Zertifikat.
Issuer (Aussteller)       | Zeichenfolge | ja      | Der Distinguished Name des Zertifikat Ausstellers.
notBefore    | Zeichenfolge | ja      | Der Start Zeitstempel für die Gültigkeitsdauer des Zertifikats.
NotAfter     | Zeichenfolge | ja      | Der Endzeit Stempel der Gültigkeitsdauer des Zertifikats.

Beachten Sie, dass `contentUrl` erforderlich ist, um über HTTPS bedient zu werden. Diese URL weist kein bestimmtes URL-Muster auf und muss mithilfe dieses Repository-Signatur Index Dokuments dynamisch erkannt werden. 

Alle Eigenschaften in diesem Objekt (abgesehen von `contentUrl` ) müssen aus dem Zertifikat abgeleitet werden, das sich unter befindet `contentUrl` .
Diese derisierbaren Eigenschaften dienen als praktische Möglichkeit zur Minimierung von Roundtrips.

Das `fingerprints`-Objekt weist die folgenden Eigenschaften auf:

Name                   | Typ   | Erforderlich | Notizen
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | Zeichenfolge | ja      | Der SHA-256-Fingerabdruck

Der Schlüssel Name `2.16.840.1.101.3.4.2.1` ist die OID des SHA-256-Hash Algorithmus.

Alle Hashwerte müssen aus Kleinbuchstaben und hexadezimal codierten Zeichen folgen Darstellungen des Hash Digest bestehen.

### <a name="sample-request"></a>Beispiel für eine Anforderung

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a>Beispiel für eine Antwort

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
