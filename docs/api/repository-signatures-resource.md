---
title: Repository-Signaturen, NuGet-API | Microsoft-Dokumentation
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: Die Repository-Signaturen-Ressource ermöglicht es Clients Paketquellen, ihrem Repository Signieren Funktionen ankündigen zu können.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: ea318446c41a0d85d3fbf959dd38c929a0d0e9a1
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2019
ms.locfileid: "59509021"
---
# <a name="repository-signatures"></a>Repository-Signaturen

Wenn eine Paketquelle hinzufügen Repository Signaturen veröffentlichte Pakete unterstützt, ist es möglich, ein Client die Signaturzertifikate zu ermitteln, die von der Paketquelle verwendet werden. Diese Ressource ermöglicht Clients erkennen, ob ein Repository signiert. Paket wurde manipuliert oder ein unerwartetes Signaturzertifikat an.

Die Ressource, die zum Abrufen von diesem Repository Signaturinformationen ist die `RepositorySignatures` Ressource finden Sie in der [dienstindex](service-index.md).

## <a name="versioning"></a>Versionskontrolle

Die folgenden `@type` Wert wird verwendet:

@type -Wert                | Hinweise
-------------------------- | -----
RepositorySignatures/4.7.0 | Die erste Version
RepositorySignatures/4.9.0 | Unterstützt durch NuGet v4.9 +-clients
RepositorySignatures/5.0.0 | Ermöglicht das Aktivieren der `allRepositorySigned`. Unterstützt durch NuGet-Clients V5. 0 +

## <a name="base-url"></a>Basis-URL

Der Eintrag-Zugriffspunkt-URL für die folgenden APIs ist der Wert des der `@id` -Eigenschaft zusammen mit den oben genannten Ressourcen `@type` Wert. In diesem Thema verwendet die Platzhalter-URL `{@id}`.

Beachten Sie, dass im Gegensatz zu anderen Ressourcen, die `{@id}` URL ist erforderlich, um über HTTPS bereitgestellt werden.

## <a name="http-methods"></a>HTTP-Methoden

Alle URLs, die in den Repositorys Signaturen Ressource unterstützt nur den HTTP-Methoden gefunden `GET` und `HEAD`.

## <a name="repository-signatures-index"></a>Index der Repository-Signaturen

Der Index der Repository-Signaturen enthält zwei Angaben:

1. Sind an, ob alle Pakete an der Quelle gefunden Repository, die von dieser Quelle signiert.
1. Die Liste der Zertifikate, die von der Paketquelle verwendet wird, um Pakete zu signieren.

In den meisten Fällen wird die Liste der Zertifikate nur angefügt werden. Neue Zertifikate würde zur Liste hinzugefügt werden, wenn das vorherige Signaturzertifikat abgelaufen ist und die Paketquelle beim Einstieg in ein neues Signaturzertifikat muss. Wenn ein Zertifikat aus der Liste entfernt wird, bedeutet, dass an, dass Signaturen für alle Pakete erstellt, mit dem entfernten Signaturzertifikat nicht mehr gültigen vom Client berücksichtigt werden soll. In diesem Fall ist der Paketsignatur (aber nicht unbedingt das Paket) ungültig. Eine Clientrichtlinie können die Installation des Pakets als ohne Vorzeichen.

Im Fall von zertifikatsperrung (z. B. schlüsselgefährdung) wird die Paketquelle erwartet, zum erneuten Signieren der alle Pakete, die durch das betroffene Zertifikat signiert. Darüber hinaus sollten die Paketquelle das betroffene Zertifikat aus der Liste der Signierung entfernen.

Die folgende Anforderung Ruft den Index der Repository-Signaturen ab.

    GET {@id}

Der Index der Repository-Signatur ist ein JSON-Dokument, das ein Objekt mit den folgenden Eigenschaften enthält:

Name                | Typ             | Erforderlich | Hinweise
------------------- | ---------------- | -------- | -----
allRepositorySigned | boolean          | ja      | Muss `false` auf 4.7.0 und 4.9.0
signingCertificates | Array von Objekten | ja      | 

Die `allRepositorySigned` boolescher Wert auf "false" festgelegt ist, wenn die Paketquelle einige Pakete gespeichert sind, die keine Repository-Signatur verfügen. Bei Verwendung der boolesche Wert auf true festgelegt ist, alle Pakete verfügbar muss die Quelle eine Repository-Signatur, die durch eines der Signaturzertifikate in erwähnten erzeugt `signingCertificates`.

> [!Warning]
> Die `allRepositorySigned` booleschen muss für die Ressourcen 4.7.0 und 4.9.0 falsch gesetzt sein. NuGet v4.9, v4. 7 und v4. 8-Clients können keine Installationspakete aus Quellen, die `allRepositorySigned` auf "true" festgelegt ist.

Es muss eine oder mehrere Signaturzertifikate in der `signingCertificates` array, wenn die `allRepositorySigned` booleschen Wert festgelegt ist auf "true". Wenn das Array leer ist und `allRepositorySigned` nastaven NA hodnotu True gibt an, alle Pakete aus der Quelle angesehen werden ungültig ist, obwohl eine Clientrichtlinie möglicherweise weiterhin die Nutzung von Paketen zulässt. Jedes Element im Array ist ein JSON-Objekt mit den folgenden Eigenschaften an.

Name         | Typ   | Erforderlich | Hinweise
------------ | ------ | -------- | -----
contentUrl   | Zeichenfolge | ja      | Das öffentliche Zertifikat von DER-codierte absolute URL
Fingerabdrücke | object | ja      |
Betreff      | Zeichenfolge | ja      | Definierter Antragstellername aus dem Zertifikat
issuer       | Zeichenfolge | ja      | Der distinguished Name des der Zertifikataussteller
notBefore    | Zeichenfolge | ja      | Der Gültigkeitszeitraum des Zertifikats den Timestamp des Starts
notAfter     | Zeichenfolge | ja      | Der Endpunkt Zeitstempel der Gültigkeitszeitraum des Zertifikats

Beachten Sie, dass die `contentUrl` ist erforderlich, um über HTTPS bereitgestellt werden. Diese URL verfügt über keine bestimmten URL-Muster und muss dynamisch ermittelt werden mit diesem Repository Signaturen Indizieren von Dokumenten. 

Alle Eigenschaften in diesem Objekt (abgesehen vom `contentUrl`) muss aus dem Zertifikat finden Sie unter Geschäftstrends `contentUrl`.
Diese Geschäftstrends Eigenschaften dienen als praktische Roundtrips zu minimieren.

Die `fingerprints` Objekt hat die folgenden Eigenschaften:

Name                   | Typ   | Erforderlich | Hinweise
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | Zeichenfolge | ja      | Der SHA-256-Fingerabdruck

Der Name des Schlüssels `2.16.840.1.101.3.4.2.1` ist die OID des SHA-256-Hashalgorithmus.

Alle Hashwerte muss hexadezimal-codierten Zeichenfolge mit Kleinbuchstaben Darstellungen des Hash-Digests.

### <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
