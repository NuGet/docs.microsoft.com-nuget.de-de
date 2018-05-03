---
title: -Dienst Index NuGet-API
description: Der Dienst-Index ist der Einstiegspunkt der NuGet-HTTP-API und listet die Funktionen des Servers.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 84e623e8480e4d17edad2ec3b2da6dcb6e53d21b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="service-index"></a>Dienst-index

Der Dienst-Index ist ein JSON-Dokument, ist der Einstiegspunkt für die Quelle ein NuGet-Paket und eine Clientimplementierung der Paketquelle Funktionen ermitteln kann. Der Dienst-Index ist ein JSON-Objekt, mit zwei erforderliche Eigenschaften: `version` (die Schemaversion des Indexes Service) und `resources` (die Endpunkte oder die Funktionen des die Paketquelle).

sich der NuGet.org-Dienst Index befindet sich unter `https://api.nuget.org/v3/index.json`.

## <a name="versioning"></a>Versionskontrolle

Die `version` Wert ist eine Zeichenfolge der SemVer 2.0.0-Schemakontexts Version gibt die Schemaversion des Dienst-Indexes an. Die API ordnet an, dass die Versionszeichenfolge eine höhere Versionsnummer hat `3`. Das IndexSchema Service nicht maßgebliche Änderungen vorgenommen werden, wird die Versionszeichenfolge Nebenversion erhöht werden.

Jede Ressource in die Dienst-Index ist unabhängig von der Dienst Index Schemaversion versionsspezifisch.

Die aktuelle Schemaversion ist `3.0.0`. Die `3.0.0` Version ist funktionell gleichwertig mit der älteren `3.0.0-beta.1` Version jedoch sollte bevorzugt werden, wie es deutlich stabile, definierte Schema kommuniziert.

## <a name="http-methods"></a>HTTP-Methoden

Der Dienst-Index ist über HTTP-Methoden möglich `GET` und `HEAD`.

## <a name="resources"></a>Ressourcen

Die `resources` -Eigenschaft enthält ein Array von Ressourcen, die von diesem Paketquelle unterstützt.

### <a name="resource"></a>Ressource

Eine Ressource ist ein Objekt in der `resources` Array. Es stellt eine Möglichkeit, eine Paketquelle mit Versionsangabe. Eine Ressource hat die folgenden Eigenschaften:

name          | Typ   | Erforderlich | Hinweise
------------- | ------ | -------- | -----
@id           | Zeichenfolge | ja      | Die URL der Ressource
@type         | Zeichenfolge | ja      | Eine Zeichenfolgenkonstante, die den Ressourcentyp darstellt.
Kommentar       | Zeichenfolge | Nein       | Eine lesbare Beschreibung der Ressource

Die `@id` ist eine URL, die muss absolut sein und muss entweder das HTTP- oder HTTPS-Schema vorhanden sein.

Die `@type` wird verwendet, um das bestimmte Protokoll verwenden, bei der Interaktion mit Ressourcen zu identifizieren. Der Typ der Ressource ist eine nicht transparente Zeichenfolge, aber im Allgemeinen weist das Format:

    {RESOURCE_NAME}/{RESOURCE_VERSION}

Clients voraussichtlich hartcodieren der `@type` Werte, die sie kennen und effizient in eine Paketquelle Dienst Index gesucht werden. Die genaue `@type` Werte heute werden aufgelistet, auf die einzelne Ressource Referenzdokumente aufgeführt, die der [Übersicht über die API](overview.md#resources-and-schema).

In dieser Dokumentation wird die Dokumentation zu anderen Ressourcen im Wesentlichen durch gruppiert werden die `{RESOURCE_NAME}` gefunden, in die Dienst-Index, der Gruppierung nach Szenario entspricht. 

Es ist nicht erforderlich, dass jede Ressource eine eindeutige weist `@id` oder `@type`. Es ist Aufgabe der Clientimplementierung, um zu bestimmen, welche Ressourcen zu vor anderen bevorzugen. Eine mögliche Implementierung ist, die die Ressourcen der denselben oder einen kompatiblen `@type` kann in einem Roundrobin bei einem Verbindungsfehler oder verwendet werden.

### <a name="sample-request"></a>Beispielanforderung

ERHALTEN https://api.nuget.org/v3/index.json

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [service-index.json](./_data/service-index.json)]
