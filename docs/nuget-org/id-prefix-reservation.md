---
title: ID-Präfixreservierung
description: Beschreibung der Reservierung für Paket-ID-Präfixe und Anleitung.
author: karann-msft
ms.author: karann
ms.date: 09/07/2019
ms.topic: reference
ms.reviewer: karann
ms.openlocfilehash: f6c4a18366b4df20fb210f718d3779e85c08d550
ms.sourcegitcommit: 188ade66b7ac807ba1667c77cfb9325bf89a8a4a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71248121"
---
# <a name="package-id-prefix-reservation"></a>Reservierung für Paket-ID-Präfixe

Paketbesitzer können ihre Identität schützen, indem sie ID-Präfixe reservieren. Paketnutzer erhalten zusätzliche Informationen, wenn die von ihnen genutzten Pakete bezüglich deren identifizierenden Eigenschaften nicht irreführend sind. 

Auf [nuget.org](https://www.nuget.org/) und in Visual Studio 2017 Version 15.4 oder höher wird für ein Paket eine Meldung angezeigt, dessen Besitzer mit einem reservierten Paket-ID-Präfix arbeitet, solange das Paket dem Namensmuster für reservierte ID-Präfixe entspricht. Im Verlauf dieses Artikels wird beschrieben, welche Aspekte bei der ID-Präfixreservierung zu beachten sind und wie ein Besitzer einen ID-Präfix anfordern kann.

## <a name="id-prefix-reservation-details"></a>Details zur ID-Präfixreservierung

Wenn ein Paket-ID-Präfix reserviert ist, hat das unterschiedliche Folgen im [nuget.org](https://www.nuget.org/)-Katalog und in Visual Studio. Die ID-Präfixreservierung unterstützt auch fortgeschrittenere Szenarios, z. B. das Festlegen eines Präfixes auf „public“ (öffentlich) oder das Delegieren von Präfixteilmengen für mehrere Besitzer.

### <a name="id-prefix-reservation-on-nugetorg"></a>ID-Präfixreservierung auf nuget.org

Wenn ein Präfix auf [nuget.org](https://www.nuget.org/) reserviert wird, geschieht Folgendes:

1. Eine Präfixreservierung wird einem oder mehreren Besitzern auf [nuget.org](https://www.nuget.org/) zugeordnet.

1. Jedes Mal, wenn ein Paket auf [nuget.org](https://www.nuget.org/) mit einer ID veröffentlicht wird, die mit dem reservierten ID-Präfix übereinstimmt, wird das Paket abgelehnt, es sei denn, es wird von den Besitzer veröffentlicht, die das ID-Präfix reserviert haben.

1. Jedes Paket, das mit dem reservierten ID-Präfix übereinstimmt und von den Besitzern veröffentlicht wird, die das ID-Präfix reserviert haben, werden in Visual Studio 2017 Version 15.4 und höher und auf [nuget.org](https://www.nuget.org/) Meldungen angezeigt. Dies gilt sowohl für neue als auch bereits vorhandene Pakete des Besitzers oder der Besitzer. **Hinweis**: Die Meldung in Visual Studio wird nur angezeigt, wenn nur ein Feed als Paketquelle ausgewählt wurde.

1. Alle vorherigen vorhandenen Pakete, die mit dem reservierten ID-Präfix übereinstimmen aber *nicht* im Besitz des Besitzers des reservierten Präfixes sind, bleiben unverändert (sie werden nicht aus der Auflistung entfernt, aber es wird auch keine Meldung angezeigt). Außerdem können Besitzer dieser Pakete weiterhin neue Paketversionen veröffentlichen.

Diese Änderungen basieren auf den folgenden Bedingungen und führen zu einigen weiteren Einschränkungen:

- Bei Paketen mit mehreren Besitzer muss nur einer der Besitzer ein reserviertes Präfix haben, damit für das Paket eine Meldung angezeigt markiert.

- Wenn es mehrere Paketbesitzer gibt und einer oder mehrere Besitzer ein reserviertes Präfix haben und einer oder mehrere Besitzer kein reserviertes Präfix haben, können nur die Besitzer mit den reservierten Präfixen andere Besitzer mit reservierten Präfixen entfernen. Die Besitzer ohne reserviertes Präfix können keine Besitzer mit reserviertem Präfix entfernen. Sie können aber Besitzer ohne reserviertes Präfix entfernen.

- Wenn für ein Paket eine Meldung angezeigt wird, sollte dies auch *weiterhin* geschehen. So wird sichergestellt, dass mindestens ein Besitzer mit dem reservierten Präfix auch weiterhin Besitzer bleibt.

### <a name="advanced-prefix-reservation-scenarios"></a>Komplexe Präfixreservierungsszenarios

Es gibt einige weitere komplexere Präfixreservierungsszenarios, die im weiteren Verlauf beschrieben werden, z. B. die Delegierung von Subpräfixen und das Festlegen öffentlicher Präfixe. Im Folgenden sind komplexere Präfixreservierungen aufgelistet. 

- Bei der Präfixreservierung kann der Besitzer die Delegierung von Präfixteilmengen (oder des Präfixes) an andere Besitzer anfordern. Wenn z. B. [Microsoft](https://www.nuget.org/profiles/microsoft) „Microsoft.\*“ besitzt, aber [aspnet](https://www.nuget.org/profiles/aspnet) möchte „Microsoft.AspNet.\*“ reservieren, dann kann [Microsoft](https://www.nuget.org/profiles/microsoft) anfordern, dass „Microsoft.AspNet.\*“ an das Konto [aspnet](https://www.nuget.org/profiles/aspnet) delegiert wird.

- Bei der Präfixreservierung kann der Besitzer ein Präfix öffentlich machen. Dadurch wird weiterhin die Meldung angezeigt, dass das Paket ursprünglich ein reserviertes Präfix hat, aber zukünftige Paketveröffentlichungen mit dem Präfix durch einen beliebigen Besitzer werden **nicht** blockiert. Das ist besonders bei Open-Source-Projekten mit vielen Beitragenden nützlich – die primären oder Hauptbeiträger können das Präfix reservieren, aber es können dennoch alle Mitwirkenden etwas beitragen. 

### <a name="prefix-reservation-visual-indicator"></a>Meldung für reservierte Präfixe

Wenn ein Paket ein reserviertes Präfix aufweist, wird die unten gezeigte Meldung im [nuget.org](https://www.nuget.org/)-Katalog und in Visual Studio 2017 Version 15.4 und höher angezeigt:

**nuget.org-Katalog**
![nuget.org-Katalog](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Anforderungsprozess für eine ID-Präfixreservierung

1. Sehen Sie sich die [Anforderungskriterien für eine ID-Präfixreservierung](#id-prefix-reservation-criteria) an.

2. Bestimmen Sie die Präfixe, die Sie reservieren möchten, sowie [komplexere Präfixreservierungsszenarios](#advanced-prefix-reservation-scenarios), die Sie benötigen.

3. Senden Sie eine E-Mail an [account@nuget.org](mailto:account@nuget.org) mit dem Anzeigenamen des Besitzers auf [nuget.org](https://www.nuget.org/) sowie mit den angeforderten reservierten Präfixen. Wenn Sie Präfixteilmengen an mehrere Besitzer delegieren, achten Sie darauf, dass Sie die Anzeigenamen aller Besitzer und die Präfixteilmengen nennen.

Nachdem die Anforderung eingereicht wurde, werden Sie informiert, ob diese angenommen oder angelehnt wurde (ggf. mit den Gründen für die Ablehnung). Es kann sein, dass Sie zusätzliche Fragen beantworten müssen, um Ihre Identität zu klären.

### <a name="id-prefix-reservation-criteria"></a>Kriterien für die ID-Präfixreservierung

Bei der Prüfung von Anforderungen für ID-Präfixreservierungen prüft das [nuget.org](https://www.nuget.org/)-Team die Anforderung anhand der unten aufgeführten Kriterien. Nicht alle Kriterien müssen erfüllt werden, damit ein Präfix reserviert wird, aber es kann sein, dass eine Anforderung abgelehnt wird, wenn nicht nachgewiesen werden kann, dass ein Kriterium erfüllt wird (mit einer entsprechenden Erklärung):

1. Gibt das Paket-ID-Präfix den Paketbesitzer eindeutig und ordnungsgemäß an?

1. Hat der Paketbesitzer die [zweistufige Authentifizierung für sein NuGet.org-Konto](individual-accounts.md#enable-two-factor-authentication-2fa) aktiviert?

1. Wurden viele der Pakete des Besitzers bereits mit diesem Paket-ID-Präfix veröffentlicht?

1. Ist das Paket-ID-Präfix zu allgemein, als dass es einem einzelnen Besitzer oder einer Organisation zugeordnet werden kann?

1. Wenn das Paket-ID-Präfix *nicht* reserviert würde, würde dies zu Mehrdeutigkeit und Verwirrung in der Community führen?

1. Sind die identifizierenden Eigenschaften der Pakete, die mit dem Paket-ID-Präfix übereinstimmen, eindeutig und konsistent (insbesondere der Paketersteller)?

1. Haben die Pakete eine Lizenz (durch das Metadatenelement [license](../reference/nuspec.md#license) angegeben, nicht durch das veraltete licenseUrl)?

1. Wenn die Pakete über ein Symbol verfügen (mit dem Metadatenelement „IconUrl“), verwenden sie dann auch das Metadatenelement [icon](../reference/nuspec.md#icon) (es ist nicht erforderlich, das Element „IconUrl“ zu entfernen)?

## <a name="third-party-feed-provider-scenarios"></a>Szenarios mit externen Feedanbietern

Wenn ein externen Feedanbieter daran interessiert ist, seinen eigenen Dienst zu implementieren, um Präfixreservierungen zu ermöglichen, können Sie dies erreichen, indem Sie den Suchdienst in den NuGet v3-Feedanbieter anpassen. Fügen Sie dazu im Feedsuchdienst die Eigenschaft *verified* mit Beispielen für den v3-Feed hinzu. Der NuGet-Client unterstützt die hinzugefügte Eigenschaft nicht im v2-Feed.

Weitere Informationen finden Sie in der [Dokumentation zum Suchdienst der API](../api/search-query-service-resource.md).

## <a name="package-id-prefix-reservation-dispute-policy"></a>Anfechtungsrichtlinie für die Reservierung von Paket-ID-Präfixen
Wenn Sie der Meinung sind, dass einem Besitzer auf [nuget.org](https://www.nuget.org) ein Paket-ID-Präfix zugewiesen wurde, das die aufgelisteten Kriterien nicht erfüllt oder gegen eingetragene Markenzeichen oder Copyrights verstößt, senden Sie eine E-Mail mit dem betreffenden ID-Präfix, dem Besitzer des ID-Präfixes und dem Grund für die Anfechtung der Zuweisung dieser Präfixreservierung an [support@nuget.org](mailto:support@nuget.org).

