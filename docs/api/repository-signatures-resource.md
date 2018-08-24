---
title: Repository-Signaturen, NuGet-API | Microsoft-Dokumentation
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 3/2/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Die Repository-Signaturen-Ressource ermöglicht es Clients Paketquellen, ihrem Repository Signieren Funktionen ankündigen zu können.
keywords: NuGet-API-Repository-Signaturen, Signieren von Zertifikaten, nuget.org nuget.org-paketsignierung
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 32dd2ee19261488a2b1b92724095a11ced69ae68
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/21/2018
ms.locfileid: "42793234"
---
# <a name="repository-signatures"></a>Repository-Signaturen

Wenn eine Paketquelle hinzufügen Repository Signaturen veröffentlichte Pakete unterstützt, ist es möglich, ein Client die Signaturzertifikate zu ermitteln, die von der Paketquelle verwendet werden. Diese Ressource ermöglicht Clients erkennen, ob ein Repository signiert. Paket wurde manipuliert oder ein unerwartetes Signaturzertifikat an.

Die Ressource, die zum Abrufen von diesem Repository Signaturinformationen ist die `RepositorySignatures` Ressource finden Sie in der [dienstindex](service-index.md).

> [!Note]
> "NuGet.org" startet die Ankündigung der `RepositorySignatures` Ressource in der nahen Zukunft.

## <a name="versioning"></a>Versionskontrolle

Die folgenden `@type` Wert wird verwendet:

@type-Wert                | Hinweise
-------------------------- | -----
RepositorySignatures/4.7.0 | Die erste Version

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

name                | Typ             | Erforderlich
------------------- | ---------------- | --------
allRepositorySigned | boolean          | ja
signingCertificates | Array von Objekten | ja

Die `allRepositorySigned` boolescher Wert auf "false" festgelegt ist, wenn die Paketquelle einige Pakete gespeichert sind, die keine Repository-Signatur verfügen. Bei Verwendung der boolesche Wert auf true festgelegt ist, alle Pakete verfügbar muss die Quelle eine Repository-Signatur, die durch eines der Signaturzertifikate in erwähnten erzeugt `signingCertificates`.

Es muss eine oder mehrere Signaturzertifikate in der `signingCertificates` array, wenn die `allRepositorySigned` booleschen Wert festgelegt ist auf "true". Wenn das Array leer ist und `allRepositorySigned` nastaven NA hodnotu True gibt an, alle Pakete aus der Quelle angesehen werden ungültig ist, obwohl eine Clientrichtlinie möglicherweise weiterhin die Nutzung von Paketen zulässt. Jedes Element im Array ist ein JSON-Objekt mit den folgenden Eigenschaften an.

name         | Typ   | Erforderlich | Hinweise
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

name                   | Typ   | Erforderlich | Hinweise
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | Zeichenfolge | ja      | Der SHA-256-Fingerabdruck

Der Name des Schlüssels `2.16.840.1.101.3.4.2.1` ist die OID des SHA-256-Hashalgorithmus.

Alle Hashwerte muss hexadezimal-codierten Zeichenfolge mit Kleinbuchstaben Darstellungen des Hash-Digests.

### <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
