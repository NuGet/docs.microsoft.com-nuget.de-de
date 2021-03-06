---
title: Push-Symbol Pakete, nuget-API | Microsoft-Dokumentation
author: cristinamanum
ms.author: cmanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Der Veröffentlichungs Dienst ermöglicht Clients das Veröffentlichen neuer Symbol Pakete.
keywords: Nuget-API-Push-Symbol Paket
ms.reviewer: karann
ms.openlocfilehash: 91bb4c9ca77fd7f1ff35831e02eb4f9d65d641c5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773890"
---
# <a name="push-symbol-packages"></a>Push-Symbol Pakete

Es ist möglich, Symbol Pakete ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) mithilfe der nuget-V3-API per Push zu übermitteln.
Diese Vorgänge basieren auf der Ressource, die `SymbolPackagePublish` im [Dienst Index](service-index.md)gefunden wurde.

## <a name="versioning"></a>Versionsverwaltung

Der folgende `@type` Wert wird verwendet:

Wert vom Typ @type                 | Hinweise
--------------------        | -----
Symbolpackagepublish/4.9.0  | Die erste Version

## <a name="base-url"></a>Basis-URL

Die Basis-URL für die folgenden APIs ist der Wert der `@id` -Eigenschaft der `SymbolPackagePublish/4.9.0` Ressource im [Dienst Index](service-index.md)der Paketquelle. In der nachfolgenden Dokumentation wird die URL von "nuget. org" verwendet. Beachten Sie `https://www.nuget.org/api/v2/symbolpackage` als Platzhalter für den `@id` Wert, der im Dienst Index gefunden wurde.

## <a name="http-methods"></a>HTTP-Methoden

Die `PUT` http-Methode wird von dieser Ressource unterstützt. 

## <a name="push-a-symbol-package"></a>Symbol Paket per Push übersetzen

nuget.org unterstützt das Pushen des neuen Symbol Paket Formats ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) mithilfe der folgenden API. 

```
PUT https://www.nuget.org/api/v2/symbolpackage
```

Symbol Pakete mit derselben ID und Version können mehrmals übermittelt werden. Ein Symbol Paket wird in den folgenden Fällen zurückgewiesen.
- Ein Paket mit derselben ID und Version ist nicht vorhanden.
- Ein Symbol Paket mit derselben ID und Version wurde per pushübertragung übermittelt, aber noch nicht veröffentlicht.
- Das Symbol Paket ("[snupkg](../create-packages/Symbol-Packages-snupkg.md)") ist ungültig (siehe [Symbol Paket Einschränkungen](../create-packages/Symbol-Packages-snupkg.md)).

### <a name="request-parameters"></a>Anforderungsparameter

Name           | In     | Typ   | Erforderlich | Notizen
-------------- | ------ | ------ | -------- | -----
X-nuget-APIKey | Header | Zeichenfolge | ja      | Zum Beispiel, `X-NuGet-ApiKey: {USER_API_KEY}`

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

