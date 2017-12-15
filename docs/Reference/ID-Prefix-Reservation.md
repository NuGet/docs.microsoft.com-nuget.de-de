---
title: "ID-Präfix Reservierung Verweis | Microsoft Docs"
author: diverdan92
ms.author: diverdan92
manager: unniravindranathan
ms.date: 10/9/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 76c0bb7f-9aaf-4c09-b3fd-f6802f9dd602
description: "Paket-ID-Präfix Reservierung featurebeschreibung und Autor-Handbuch."
keywords: "NuGet-Paket-ID-Präfix, Reservierung"
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.openlocfilehash: e94d1431667ec17347165ac0a3993c0b552e6a60
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="package-id-prefix-reservation"></a>Paket-ID-Präfix-Reservierung
[NuGet.org](https://www.nuget.org/) und Visual Studio 2017 15.4 oder höher einen visuellen Indikator für Pakete, die vom Besitzer mit einem reservierten Paket-ID-Präfix übermittelt werden, solange das Paket der reservierte ID übereinstimmt, Benennungsschema Präfix. Die folgenden Verweis wird erläutert, was die ID-Präfix-Reservierung umfasst, und wie ein Besitzer für ein ID-Präfix anwenden kann.

## <a name="what-is-package-id-prefix-reservation"></a>Was ist die Paket-ID-Präfix Reservierung?
Die Paketeigentümer können reserviert werden sollen, und schützen ihre Identität durch ID Präfixe reservieren. Mit zusätzlichen Informationen bei der Nutzung von Paketen das Paket, das sie in Anspruch genommen sind nicht in ihre identifizierenden Eigenschaften betrügerische erhalten paketverbrauchern. Erfahren Sie hier Funktionsweise von ID-Präfix-Reservierung in Details.

## <a name="id-prefix-reservation-details"></a>ID-Präfix Reservierung details 
Wenn ein Paket-ID-Präfix reserviert ist, mehrere Aktionen ausgeführt, auf die [nuget.org](https://www.nuget.org/) -Katalog als auch in Visual Studio. Darüber hinaus sind es Szenarien erweiterte, die vom ID-Präfix-Reservierungen ein Präfix als "public" delegieren Präfix Teilmengen zu mehreren Besitzern legt er z. B. unterstützt werden.

Die im folgenden Abschnitt wird beschrieben, die Funktion im Detail als auch die erweiterte Funktionalität.

### <a name="id-prefix-reservation-on-nugetorg"></a>ID-Präfix-Reservierung für nuget.org
Wenn ein Präfix auf reserviert [nuget.org](https://www.nuget.org/), passiert Folgendes:
1. Eine Reservierung Präfix zugeordnet ist ein Besitzer oder eine Gruppe von Besitzern für [nuget.org](https://www.nuget.org/). 
2. Wenn ein Paket an übermittelt [nuget.org](https://www.nuget.org/) mit der ID, die der reservierte ID-Präfix entspricht, wird das Paket abgelehnt, es sei denn, sie von den Besitzern stammt, der das ID-Präfix reserviert.
3. Alle Pakete, die der reservierte ID-Präfix entspricht, stammen aus den Besitzern, der das ID-Präfix reserviert haben einen visuellen Indikator aus, in Visual Studio 2017 Version 15.4 oder höher, und klicken Sie auf [nuget.org](https://www.nuget.org/) , der angibt, dem das Paket unter ein reserviertes ID-Präfix. Dies gilt für sowohl neue Paket Übermittlungen sowie vorhandene Pakete unter den Besitzern. **Hinweis:** der Indikator in Visual Studio wird nur angezeigt, wenn Sie ein einzelner Feed als Paketquelle ausgewählt ist. 
4. Jedoch werden alle zuvor vorhandene Pakete, die der reservierte ID-Präfix entsprechen *nicht* gehören dem Besitzer des reservierten Präfix bleiben jedoch unverändert (nicht aufgelistete nicht auf sein, aber er auch keinen visuellen Indikator). Darüber hinaus werden Besitzer dieser Pakete kann neue Versionen auf das Paket gesendet.

Diese Änderungen werden entsprechend den folgenden Bedingungen und einige zusätzliche Einschränkungen zu erzwingen:
* Nur einen Besitzer für ein Paket muss dem reservierten Präfix für den visuellen Indikator (für Pakete mit mehreren Besitzern) angezeigt werden.
* Wenn mehr als ein Besitzer eines Pakets, in denen eine oder mehrere Besitzer hat reservierte Präfix und einen oder mehrere Besitzer verfügt nicht über die reserviertes Präfix, vorhanden ist, können nur die sperrenüberwachung mit dem reservierten Präfix anderen Besitzern mit ein reserviertes Präfix entfernen. Die, die nicht das Präfix reserviert haben Besitzern können nicht Besitzer mit dem Präfix reservierte entfernt werden. Dennoch können andere Besitzer entfernen, auf denen auch kein reserviertes Präfix.
  * Sobald ein Paket den visuellen Indikator ist, sollten sie *immer* den visuellen Indikator haben (dieser über mindestens ein Besitzer mit dem reservierten Präfix garantiert immer bleibt ein Besitzer)

### <a name="advanced-prefix-reservation-scenarios"></a>Erweiterte Präfix Reservierung Szenarien
Es gibt mehrere erweiterte Präfix Reservierung Szenarien einschließlich Subprefix Delegierung und Kennzeichnung Präfixe als öffentliche unten beschriebenen. Im folgenden sind die erweiterten Präfix Reservierungen, die vorgenommen werden können. 

* Während der Präfix-Reservierung kann der Besitzer zu anderen Besitzern Delegierung Präfix Teilmengen (oder das Präfix) anfordern. Z. B. wenn "[Microsoft](https://www.nuget.org/profiles/microsoft)" besitzt ' Microsoft.\*", aber"[Aspnet](https://www.nuget.org/profiles/aspnet)"reservieren möchte" Microsoft.AspNet.\*","[Microsoft](https://www.nuget.org/profiles/microsoft)"kann Wählen Sie zum Delegieren "Microsoft.AspNet. \*"auf die [Aspnet](https://www.nuget.org/profiles/aspnet) Konto.
*  Während der Präfix-Reservierung können der Besitzer ein Präfix als öffentliches Profil festzulegen. Weiterhin erhalten sie die visuellen Indikator, der anzeigt, dass das Paket aus der ein reserviertes Präfix stammt, aber es wird **nicht** zukünftige Paket Übermittlungen anhand des Präfixes für jeden Besitzer blockieren. Dies ist nützlich für open Source-Projekte mit viele Mitwirkende – Top oder Core Contributors können das Präfix reserviert haben, aber es kann immer noch geöffnet sein, um allen Contributors. 

### <a name="prefix-reservation-visual-indicator"></a>Präfix Reservierung visuellen Indikator
Wenn ein Paket ein reserviertes Präfix stammen, sehen Sie die unten von visuellen Indikatoren auf der [nuget.org](https://www.nuget.org/) Katalog und in Visual Studio 2017 15.4 oder höher:

**NuGet.org Katalog**
![nuget.org-Katalog](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>ID-Präfix Reservierung Anwendungsprozess
Um eine Reservierung Präfix beantragen, befolgen Sie die unten aufgeführten Schritten. 
1. Überprüfen Sie die Annahme [Kriterien für die Präfix-ID Reservierung](#id-prefix-reservation-criteria).
2. Bestimmen Sie die Namespaces, die Sie reservieren sowie jegliche, möchten [erweiterte Szenarien der Präfix-Reservierung](#advanced-prefix-reservation-scenarios) möglicherweise benötigt.
3. Senden Sie eine e-Mail an [ account@nuget.org ](mailto:account@nuget.org) mit dem Besitzer Anzeigename auf [nuget.org](https://www.nuget.org/), sowie alle reservierte Präfixe, die Sie anfordern. Wenn Sie die Präfix-Teilmengen zu mehreren Besitzern delegieren, stellen Sie sicher, nennen Sie die Anzeigenamen für alle Besitzer und Teilmengen Präfix.

Nachdem die Anwendung gesendet wird, werden Sie benachrichtigt werden, der Annahme oder Ablehnung (mit den Kriterien, die Ablehnung verursacht hat). Wir müssen möglicherweise weitere identifizierende Besitzer Identität bestätigen Fragen. 

### <a name="id-prefix-reservation-criteria"></a>ID-Präfix Reservierung Kriterium
Beim Überprüfen von einer Anwendung über ID-Präfix-Reservierung, die [nuget.org](https://www.nuget.org/) Team Evalaute wird die Anwendung unter Verwendung der folgenden Kriterien. Nicht alle Kriterien erfüllt sein, damit ein Präfix reserviert werden muss, aber die Anwendung kann verweigert werden, besteht kein erhebliche Beweis der Kriterien (mit einer Erklärung, angegebenen) erfüllt werden:
1. Gibt die Paket-ID-Präfix richtig und eindeutig Besitzer des Pakets an?
2. Sind eine erhebliche Anzahl von den Paketen, die bereits gesendet wurde, die dem Besitzer unter den Paket-ID-Präfix?
3. Ist das Paket-ID-Präfix allgemeine etwas, das nicht auf einzelner Besitzer oder Organisation gehören soll?
4. Würde *nicht* Reservieren der Paket-ID-Präfix dazu führen, dass Mehrdeutigkeiten und Gefahren zu Verwechslungen für die Community?
5. Gibt die identifizierenden Eigenschaften der Pakete, die mit der Paket-ID-Präfix klar und konsistent (insbesondere Paketersteller) übereinstimmen?

## <a name="3rd-party-feed-provider-scenarios"></a>3. Partei, die feed-Anbieter-Szenarien
Wenn eine 3rd Party datenfeedanbieter implementieren ihre eigenen Dienst zum Bereitstellen von Präfix Reservierungen interessiert ist, können Sie tun, damit durch Ändern der Search-Dienst im NuGet V3--Anbieter Feed. Feed-Suchdienst ist zum Hinzufügen der *überprüft* Eigenschaft zusammen mit Beispielen für die folgenden V3-Feeds. Die NuGet-Clients wird der hinzugefügte Eigenschaft in der feed V2 nicht unterstützt.

Weitere Informationen finden Sie unter der [Dokumentation über die API-Suchdienst](../api/search-query-service-resource.md).
