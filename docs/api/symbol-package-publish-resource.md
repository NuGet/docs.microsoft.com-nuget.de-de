---
title: Push-Symbol Pakete, nuget-API | Microsoft-Dokumentation
author: cristinamanum
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Der Veröffentlichungs Dienst ermöglicht Clients das Veröffentlichen neuer Symbol Pakete.
keywords: Nuget-API-Push-Symbol Paket
ms.reviewer: karann
ms.openlocfilehash: 27e557bf15ce31152243a409eddc4112eeb6c38b
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235106"
---
# <a name="push-symbol-packages"></a>Push-Symbol Pakete

Es ist möglich, Symbol Pakete ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) mithilfe der nuget-V3-API per Push zu übermitteln.
Diese Vorgänge basieren `SymbolPackagePublish` auf der Ressource, die im [Dienst Index](service-index.md)gefunden wurde.

## <a name="versioning"></a>Versionskontrolle

Der folgende `@type` Wert wird verwendet:

@type -Wert                 | Hinweise
--------------------        | -----
Symbolpackagepublish/4.9.0  | Die erste Version

## <a name="base-url"></a>Basis-URL

Die Basis-URL für die folgenden APIs ist der Wert der `@id` -Eigenschaft `SymbolPackagePublish/4.9.0` der Ressource im [Dienst Index](service-index.md)der Paketquelle. In der nachfolgenden Dokumentation wird die URL von "nuget. org" verwendet. Beachten `https://www.nuget.org/api/v2/symbolpackage` Sie als Platzhalter für den `@id` Wert, der im Dienst Index gefunden wurde.

## <a name="http-methods"></a>HTTP-Methoden

Die `PUT` HTTP-Methode wird von dieser Ressource unterstützt. 

## <a name="push-a-symbol-package"></a>Symbol Paket per Push übersetzen

nuget.org unterstützt das Pushen des neuen Symbol Paket Formats ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) mithilfe der folgenden API. 

    PUT https://www.nuget.org/api/v2/symbolpackage

Symbol Pakete mit derselben ID und Version können mehrmals übermittelt werden. Ein Symbol Paket wird in den folgenden Fällen zurückgewiesen.
- Ein Paket mit derselben ID und Version ist nicht vorhanden.
- Ein Symbol Paket mit derselben ID und Version wurde per pushübertragung übermittelt, aber noch nicht veröffentlicht.
- Das Symbol Paket ("[snupkg](../create-packages/Symbol-Packages-snupkg.md)") ist ungültig (siehe [Symbol Paket Einschränkungen](../create-packages/Symbol-Packages-snupkg.md)).

### <a name="request-parameters"></a>Anforderungs Parameter

name           | In     | Typ   | Erforderlich | Hinweise
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Header | String | ja      | Beispiel: `X-NuGet-ApiKey: {USER_API_KEY}`

Der API-Schlüssel ist eine nicht transparente Zeichenfolge, die vom Benutzer aus der Paketquelle abgerufen und für den Client konfiguriert wurde. Es ist kein bestimmtes Zeichen folgen Format vorgeschrieben, aber die Länge des API-Schlüssels sollte keine angemessene Größe für HTTP-Header Werte überschreiten.

### <a name="request-body"></a>Anforderungstext

Der Anforderungs Text für das Symbol Push entspricht dem Anforderungs Text einer paketpushanforderung (siehe [Package Push und DELETE](package-publish-resource.md)). 

### <a name="response"></a>Antwort

Statuscode | Bedeutung
----------- | -------
201         | Das Symbol Paket wurde erfolgreich per pushübertragung übermittelt.
400         | Das angegebene Symbol Paket ist ungültig.
401         | Der Benutzer ist nicht autorisiert, diese Aktion auszuführen.
404         | Ein entsprechendes Paket mit der angegebenen ID und der angegebenen Version ist nicht vorhanden.
409         | Ein Symbol Paket mit der angegebenen ID und Version wurde per Pushvorgang übermittelt, ist aber noch nicht verfügbar.
413         | Das Paket ist zu groß.

