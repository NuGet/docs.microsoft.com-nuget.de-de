---
title: -Dienst Index, NuGet-API
description: Der dienstindex ist der Einstiegspunkt, der die NuGet-HTTP-API und listet die Funktionen des Servers.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1dcfb87690b728280b494d4434f9c1d7ee7a7e74
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324720"
---
# <a name="service-index"></a>Dienstindex

Dienstindex ist ein JSON-Dokument, ist der Einstiegspunkt für eine NuGet-Paketquelle und eine Client-Implementierung der Paketquelle Funktionen ermitteln kann. Der dienstindex ist ein JSON-Objekt mit zwei erforderliche Eigenschaften: `version` (die Schemaversion des dienstindex) und `resources` (Endpunkte oder Funktionen der Paketquelle).

NuGet.org dienstindex befindet sich unter `https://api.nuget.org/v3/index.json`.

## <a name="versioning"></a>Versionskontrolle

Die `version` Wert ist eine analysierbare SemVer 2.0.0-Versionszeichenfolge, womit die Schemaversion der dienstindex. Die API erfordert, dass die version-Zeichenfolge die Hautpversionsnummer `3` hat. Wenn API-kompatible Änderungen am Schema des Dienstindex durchgeführt werden, wird die Nebenversion der version-Zeichenfolge erhöht.

Jede Ressource im dienstindex ist unabhängig von der Schemaversion des Dienst-Index mit Versionsangabe.

Die aktuelle Version des Datenbankschemas ist `3.0.0`. Die `3.0.0` Version ist funktionell gleichwertig mit dem älteren `3.0.0-beta.1` Version aber sollten bevorzugt werden, wie das stabile, definierte Schema deutlicher kommuniziert.

## <a name="http-methods"></a>HTTP-Methoden

Dienstindex kann zugegriffen werden, mithilfe von HTTP-Methoden `GET` und `HEAD`.

## <a name="resources"></a>Ressourcen

Die `resources` Eigenschaft enthält eine Reihe von Ressourcen, die von diesem Paketquelle unterstützt werden.

### <a name="resource"></a>Ressource

Eine Ressource ist ein Objekt in der `resources` Array. Es stellt eine Funktion mit versionsverwaltung durch das der Paketquelle dar. Eine Ressource hat die folgenden Eigenschaften:

name          | Typ   | Erforderlich | Hinweise
------------- | ------ | -------- | -----
@id           | Zeichenfolge | ja      | Die URL der Ressource
@type         | Zeichenfolge | ja      | Eine Zeichenfolgenkonstante, die den Ressourcentyp darstellt.
Kommentar       | Zeichenfolge | Nein       | Eine lesbare Beschreibung der Ressource

Die `@id` ist eine URL, die muss absolut sein und muss entweder das HTTP- oder HTTPS-Schema aufweisen.

Die `@type` wird verwendet, um das bestimmte Protokoll verwenden, bei der Interaktion mit Ressourcen zu identifizieren. Der Typ der Ressource ist eine nicht transparente Zeichenfolge, aber im Allgemeinen weist das Format auf:

    {RESOURCE_NAME}/{RESOURCE_VERSION}

Clients wird vorausgesetzt, durch hartcodierung der `@type` Werte, die diese Partner kennen, und suchen sie in eine Paketquelle dienstindex. Die genaue `@type` Werte heute werden aufgezählt, auf die einzelne Ressource Referenzdokumente aufgeführt, die der [-API – Übersicht](overview.md#resources-and-schema).

Aus Gründen der dieser Dokumentation wird die Dokumentation zu anderen Ressourcen im Wesentlichen nach gruppiert werden die `{RESOURCE_NAME}` in dienstindex handelt es sich analog zur Gruppierung nach Szenario gefunden. 

Es ist nicht erforderlich, dass jede Ressource eine eindeutige hat `@id` oder `@type`. Es ist Aufgabe der Clientimplementierung, um zu bestimmen, welche Ressourcen vor anderen bevorzugen. Eine mögliche Implementierung ist, die Ressourcen, die von der gleichen oder einen kompatiblen `@type` in eine Roundrobin-bei einem Verbindungsfehler oder verwendet werden kann.

### <a name="sample-request"></a>Beispiel für eine Anforderung

    GET https://api.nuget.org/v3/index.json

### <a name="sample-response"></a>Beispielantwort

[!code-JSON [service-index.json](./_data/service-index.json)]
