---
title: Dienst Index, nuget-API
description: Der Dienst Index ist der Einstiegspunkt der nuget-HTTP-API und listet die Funktionen des Servers auf.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775360"
---
# <a name="service-index"></a>Dienstindex

Der Dienst Index ist ein JSON-Dokument, das den Einstiegspunkt für eine nuget-Paketquelle ist und es einer Client Implementierung ermöglicht, die Funktionen der Paketquelle zu ermitteln. Der Dienst Index ist ein JSON-Objekt mit zwei erforderlichen Eigenschaften: `version` (die Schema Version des Dienst Indexes) und `resources`  (die Endpunkte oder Funktionen der Paketquelle).

der Dienst Index von nuget. org befindet sich unter `https://api.nuget.org/v3/index.json` .

## <a name="versioning"></a>Versionsverwaltung

Der `version` Wert ist eine zu semver 2.0.0 ausführbare Versions Zeichenfolge, die die Schema Version des Dienst Indexes angibt. Die API gibt an, dass die Versions Zeichenfolge eine Hauptversionsnummer von aufweist `3` . Da nicht unterbrechende Änderungen am Dienst Index Schema vorgenommen werden, wird die neben Version der Versions Zeichenfolge erweitert.

Jede Ressource im Dienst Index wird unabhängig von der Dienst Index Schema-Version versioniert.

Die aktuelle Schema Version ist `3.0.0` . Die `3.0.0` Version ist funktional gleichwertig mit der älteren `3.0.0-beta.1` Version, sollte aber bevorzugt werden, da Sie das stabile, definierte Schema deutlicher kommuniziert.

## <a name="http-methods"></a>HTTP-Methoden

Auf den Dienst Index kann mithilfe der HTTP `GET` -Methoden und zugegriffen werden `HEAD` .

## <a name="resources"></a>Ressourcen

Die- `resources` Eigenschaft enthält ein Array von Ressourcen, die von dieser Paketquelle unterstützt werden.

### <a name="resource"></a>Resource

Eine Ressource ist ein Objekt im `resources` Array. Sie stellt eine versionierte Funktion einer Paketquelle dar. Eine Ressource verfügt über die folgenden Eigenschaften:

Name          | Typ   | Erforderlich | Notizen
------------- | ------ | -------- | -----
@id           | Zeichenfolge | ja      | Die URL der Ressource.
@type         | Zeichenfolge | ja      | Eine Zeichen folgen Konstante, die den Ressourcentyp darstellt.
comment       | Zeichenfolge | nein       | Eine lesbare Beschreibung der Ressource.

Bei `@id` handelt es sich um eine URL, die absolut sein muss und entweder über das http-oder HTTPS-Schema verfügen muss.

`@type`Wird verwendet, um das Protokoll zu identifizieren, das bei der Interaktion mit der Ressource verwendet werden soll. Der Typ der Ressource ist eine nicht transparente Zeichenfolge, hat jedoch im Allgemeinen das folgende Format:

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

Clients sollten die `@type` Werte, die Sie verstehen, hart codieren und im Dienst Index einer Paketquelle nachschlagen. Die aktuell `@type` verwendeten Werte werden in den einzelnen Ressourcen Verweis Dokumenten aufgelistet, die in der API- [Übersicht](overview.md#resources-and-schema)aufgeführt sind.

Im Rahmen dieser Dokumentation wird die Dokumentation zu verschiedenen Ressourcen im Wesentlichen nach dem `{RESOURCE_NAME}` im Dienst Index gefundenen gruppiert, der der Gruppierung nach Szenario entspricht. 

Es ist nicht erforderlich, dass jede Ressource über eine eindeutige `@id` oder verfügt `@type` . Es liegt an der Client Implementierung, die bevorzugte Ressource zu bestimmen. Eine mögliche Implementierung besteht darin, dass Ressourcen des gleichen oder kompatiblen bei `@type` Verbindungsfehlern oder Server Fehlern im Roundrobin-Verfahren verwendet werden können.

### <a name="sample-request"></a>Beispiel für eine Anforderung

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a>Beispiel für eine Antwort

[!code-JSON [service-index.json](./_data/service-index.json)]
