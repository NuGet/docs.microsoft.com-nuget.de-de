---
title: ID-Präfix-Reservierung Verweis
description: Paket-ID-Präfix-Reservierung funktionsbeschreibung und Autor-Handbuch.
author: diverdan92
ms.author: diverdan92
manager: unnir
ms.date: 10/09/2017
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 10d017d67cf2bd49812c5d54f9fca063f32cc052
ms.sourcegitcommit: 6cffa6ef59b922df2d87aa9c24034d00542983cd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2018
ms.locfileid: "37948394"
---
# <a name="package-id-prefix-reservation"></a>Paket-ID-präfixreservierung

Paketbesitzern können reservieren und ihre Identität schützen, indem Sie die ID-Präfixe reservieren. Paketverbraucher stehen mit zusätzlichen Informationen bei der Nutzung von Paketen das Paket, das sie nutzen sind nicht in ihre identifizierenden Eigenschaften irreführend. 

["NuGet.org"](https://www.nuget.org/) und Visual Studio 2017 Version 15.4 oder höher einen visuellen Indikator für Pakete, die von den Besitzern mit einem Präfix reserviertes Paket-ID gesendet werden, solange das Paket die reservierte ID entspricht Benennungsmuster Präfix. Die folgenden Verweis wird erläutert, was ist mit der ID-präfixreservierung verbunden, und wie ein Besitzer für ein ID-Präfix anwenden kann.

## <a name="id-prefix-reservation-details"></a>Reservierungsdetails für ID-Präfix

Wenn ein Paket-ID-Präfix reserviert wurde, geschehen mehrere Dinge auf die [nuget.org](https://www.nuget.org/) Katalog auch wie in Visual Studio. Darüber hinaus sind es Szenarien erweiterte, die vom ID-Präfix-Reservierungen, z. B. das Festlegen von Präfix als 'public', delegieren Präfix Teilmengen zu mehreren Besitzern unterstützt werden.

### <a name="id-prefix-reservation-on-nugetorg"></a>ID-präfixreservierung auf nuget.org

Wenn ein Präfix auf reserviert [nuget.org](https://www.nuget.org/), passiert Folgendes:

1. Eine präfixreservierung zugeordnet ist ein Besitzer oder Besitzer auf [nuget.org](https://www.nuget.org/).

1. Jedes Mal, wenn ein Paket gesendet wird, um [nuget.org](https://www.nuget.org/) mit einer ID, die reservierte ID-Präfix entspricht, wird das Paket abgelehnt, es sei denn, sie der Besitzer stammt, der das ID-Präfix reserviert.

1. Alle Pakete, die der reservierte ID-Präfix entspricht und stammt aus dem der Besitzer, der das ID-Präfix reserviert haben einen visuellen Indikator in Visual Studio 2017 Version 15.4 oder höher, und klicken Sie auf [nuget.org](https://www.nuget.org/) , der angibt, der das Paket wird ein reserviertes ID-Präfix. Dies gilt für sowohl neue Paket Übermittlungen sowie vorhandene Pakete unter den Besitzern genehmigt. **Hinweis:** der Indikator in Visual Studio, das angezeigt wird, nur, wenn Sie ein einzelner Feed als Paketquelle ausgewählt ist.

1. Gibt alle bereits vorhandenen Pakete, die die reservierte ID-Präfix, entsprechen jedoch *nicht* gehören dem Besitzer des reservierten Präfix bleiben unverändert (sie werden nicht aufgehoben werden, aber sie müssen auch nicht des visuellen Indikators). Darüber hinaus werden Besitzer dieser Pakete kann neue Versionen für das Paket gesendet.

Diese Änderungen basieren auf den folgenden Bedingungen und einige zusätzliche Einschränkungen zu erzwingen:

- Nur einen Besitzer für ein Paket benötigt die reservierte Präfix für der visuelle Indikator (für Pakete mit mehreren-Besitzern) angezeigt werden.

- Wenn mehr als ein Besitzer eines Pakets, in dem einen oder mehrere Besitzer hat das reservierte Präfix und einen oder mehrere Besitzer verfügt nicht über dem reservierten Präfix, vorhanden ist, können nur der Besitzer mit dem reservierten Präfix mit anderen Besitzer mit einem reservierten Präfix entfernen. Die Besitzer, die nicht mit das reservierten Präfix verfügen, können nicht Besitzer mit dem reservierten Präfix entfernt. Sie können immer noch andere Besitzer entfernt werden, die nicht auch das reservierten Präfix besitzen.

- Nachdem ein Paket den visuellen Indikator enthält, sollten sie *immer* haben den visuellen Indikator (& lt; 15ms, mindestens einen Besitzer mit dem reservierten Präfix ist immer weiterhin Besitzer)

### <a name="advanced-prefix-reservation-scenarios"></a>Szenarien für erweiterte Präfix-Reservierung

Es gibt mehrere erweiterte Präfix-Reservierung Szenarien unten beschriebenen, einschließlich Subprefix Delegierung und Kennzeichnung von Präfixen als öffentlich. Im folgenden sind die erweiterten Präfix-Reservierungen, die vorgenommen werden können. 

- Während der Präfix-Reservierung kann der Besitzer Delegierung Präfix Teilmengen (oder das Präfix) für andere Besitzer anfordern. Z. B. wenn "[Microsoft](https://www.nuget.org/profiles/microsoft)" besitzt "Microsoft.\*", aber "[Aspnet](https://www.nuget.org/profiles/aspnet)" möchte, reservieren "Microsoft.AspNet.\*','[Microsoft](https://www.nuget.org/profiles/microsoft)' kann delegieren, "Microsoft.AspNet. \*"auf die [Aspnet](https://www.nuget.org/profiles/aspnet) Konto.

- Während der Präfix-Reservierung können der Besitzer ein Präfix öffentlich zu machen. Auf diese Weise noch erhalten sie die visuellen Indikator, der anzeigt, dass das Paket ein reserviertes Präfix stammt, aber es wird **nicht** Übermittlungen von zukünftigen Paket auf dem Präfix für alle Besitzer blockieren. Dies ist nützlich für open Source-Projekte mit vielen Mitwirkenden – die oberen oder Core-Contributors haben das Präfix reserviert, aber es kann immer noch offen sein, um alle Mitwirkenden. 

### <a name="prefix-reservation-visual-indicator"></a>Visuellen Indikator zu Präfix-Reservierung

Wenn ein Paket ein reserviertes Präfix stammen, sehen Sie die unten visuelle Indikatoren für die [nuget.org](https://www.nuget.org/) Katalog und in Visual Studio 2017 Version 15.4 oder höher:

**Katalog von NuGet.org**
![NuGet-Katalog](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>ID-Präfix-Reservierung Anwendungsprozess

1. Überprüfen Sie die Annahme [Kriterien für die ID-präfixreservierung](#id-prefix-reservation-criteria).

2. Bestimmen Sie die Namespaces, die Sie reservieren möchten, zusätzlich zu [erweiterte Szenarien der Präfix-Reservierung](#advanced-prefix-reservation-scenarios) benötigen Sie möglicherweise.

3. Senden eine e-Mail an [ account@nuget.org ](mailto:account@nuget.org) mit dem Besitzer Anzeigenamen auf [nuget.org](https://www.nuget.org/), sowie alle reservierte Präfixe, die Sie anfordern. Wenn Sie die Präfix-Teilmengen zu mehreren Besitzern delegieren sind, stellen Sie sicher Sie erwähnen Sie alle Besitzer Anzeigenamen Präfix Teilmengen.

Nachdem die Anwendung gesendet wurde, werden Sie benachrichtigt der Annahme oder Ablehnung (mit den Kriterien, die Ablehnung verursacht hat). Wir müssen zusätzliche identifizierende, besitzeridentität zu bestätigen, Fragen zu stellen.

### <a name="id-prefix-reservation-criteria"></a>ID-Präfix-Reservierung Kriterium

Beim Überprüfen von jeder Anwendung für ID-präfixreservierung der [nuget.org](https://www.nuget.org/) Team ergibt die Anwendung für die folgenden Kriterien. Nicht alle Kriterien erfüllt sein, damit ein Präfix reserviert werden muss, aber die Anwendung kann verweigert werden, wenn keine erhebliche Beweise für die Kriterien erfüllt wird, (mit der angegebenen Erläuterung) vorhanden ist:

1. Identifiziert das Paket-ID-Präfix richtig und eindeutig den Besitzer des Pakets?

1. Sind Sie eine große Anzahl von den Paketen, die bereits übermittelt wurden, durch den Besitzer der unter dem Paket-ID-Präfix?

1. Ist das Paket-ID-Präfix häufig etwas, das nicht auf einzelner Besitzer oder Organisation angehören soll?

1. Würde *nicht* reservieren das Paket-ID-Präfix dazu führen, dass Mehrdeutigkeiten und Verwirrung für die Community?

1. Gibt die identifizierenden Eigenschaften der Pakete, die mit der Paket-ID-Präfix klare und einheitliche (insbesondere Paketersteller) übereinstimmen?

## <a name="third-party-feed-provider-scenarios"></a>Von Drittanbietern, die feed-Anbieter-Szenarien

Ist ein Drittanbieter datenfeedanbieter Präfix Reservierungen sind ihre eigenen Dienst implementieren möchten, können Sie dies durch Ändern der Search-Dienst in der NuGet-V3-Anbieter feed tun. In den feed Search-Dienst ist zum Hinzufügen der *überprüft* Eigenschaft, die mit Beispielen für die folgenden V3-Feeds. Der NuGet-Client wird die hinzugefügte Eigenschaft in der V2-feed nicht unterstützt werden.

Weitere Informationen finden Sie unter den [Dokumentation zu API Search-Dienst](../api/search-query-service-resource.md).

## <a name="package-id-prefix-reservation-dispute-policy"></a>Paket-ID-Präfix-Reservierung im Fall von Streitigkeiten Richtlinie
Wenn Sie glauben, einen Besitzer auf [NuGet.org](https://www.nuget.org) zugewiesen wurde eine Paket-ID-Präfix-Reservierung, die verstößt gegen die oben aufgeführten Kriterien aus, oder Sie e-Mail-Adresse auf Urheberrechte, Marken oder verletzt [ support@nuget.org ](mailto:support@nuget.org)mit der ID-Präfix, das fragliche, den Besitzer für das ID-Präfix und den Grund für die zugewiesene präfixreservierung disputing.

