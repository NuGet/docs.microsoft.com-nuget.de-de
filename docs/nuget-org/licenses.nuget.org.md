---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 717cf8c47335c620410be71300b07de82799e1d3
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427115"
---
# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>Begründung

Mit der Einführung von [Lizenzausdrücken](../reference/nuspec.md#license) entstand der Bedarf nach einem zuverlässigen Dienst, der einen Referenztext für einzelne Lizenzbezeichner, Ausnahmebezeichner oder Lizenzausdrücke bereitstellt.
Eine zusätzliche Anforderung an diesen Dienst ist ein stabiles URL-Schema, das nicht für tote Links anfällig ist und sicher verwendet werden kann, um Abwärtskompatibilität für ältere Clients zu gewährleisten.

Licenses.nuget.org erfüllt diese Anforderungen. Nuget.org nutzt Licenses.nuget.org, um die Lizenztextreferenz für Pakete bereitzustellen, die ihre Lizenz über einen Lizenzausdruck angeben. Über `nuget pack` oder bei einer Paketierung mit anderen [Clienttools](../install-nuget-client-tools.md) wird das [`licenseUrl`](../reference/nuspec.md#licenseurl)-Element zum Verweis auf licenses.nuget.org festgelegt, um Abwärtskompatibilität mit älteren Clients bereitzustellen, die das `license`-Element nicht unterstützen.

## <a name="protocol"></a>Protokoll

Licenses.nuget.org ist für die Anzeige in einem Browser durch Personen vorgesehen, es werden keine maschinenlesbaren Antworten bereitgestellt.
Das HTTPS-Protokoll ist erforderlich, und Anforderungen müssen in einer bestimmten Weise erstellt werden. Es werden nur `GET`-Anforderungen unterstützt.
Lizenzausdrücke oder Lizenzausnahmebezeichner werden in der unten angegebenen Weise als Eingabe akzeptiert. Beachten Sie, dass für alle Elemente von Lizenzausdrücken die Groß-/Kleinschreibung beachtet werden muss, deshalb gilt für alle Eingaben in licenses.nuget.org ebenfalls die Beachtung der Groß-/Kleinschreibung.

### <a name="license-expressions"></a>Lizenzausdrücke

#### <a name="request"></a>Anforderung

Lizenzausdrücke (einschließlich trivialer Fälle, in denen ein Ausdruck nur aus einer Lizenz besteht) müssen [URL-codiert](https://tools.ietf.org/html/rfc3986#section-2.1) sein und als Pfad in der Anforderung an licenses.nuget.org verwendet werden.

| Lizenzausdruck | Zu verwendende URL |
|:---|:---|
| MIT                                                | <https://licenses.nuget.org/MIT> |
| (MIT)                                              | <https://licenses.nuget.org/(MIT)> |
| (LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+) | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

Der Dienst unterstützt nur Lizenzbezeichner und Lizenzausnahmebezeichner, die von nuget.org akzeptiert werden. Alle Lizenzausdrücke, die nicht unterstützte Lizenzbezeichner oder Lizenzausnahmebezeichner enthalten oder nicht der Syntax für Lizenzausdrücke entsprechen, werden als ungültig betrachtet.

#### <a name="response"></a>Antwort

Licenses.nuget.org antwortet auf Anforderungen, die einen gültigen Lizenzausdruck enthalten, mit einem HTTP 200-Statuscode und einer Webseite mit einer Beschreibung des Lizenzausdrucks:

* Wenn der angegebene Lizenzausdruck einen einzelnen Lizenzbezeichner umfasst, wird eine Webseite zurückgegeben, die diesen Lizenzreferenztext enthält.
* Wenn der angegebene Lizenzausdruck ein zusammengesetzter Lizenzausdruck ist, wird eine Webseite zurückgegeben, die den Lizenzausdruck mit Links zu den einzelnen Lizenz- oder Lizenzausnahmereferenzen enthält.

Alle Anforderungen, die einen ungültigen Lizenzausdruck enthalten, führen zu einer HTTP 404-Antwort.

### <a name="license-exceptions"></a>Lizenzausnahmen

#### <a name="request"></a>Anforderung

Lizenzausnahmebezeichner müssen URL-codiert sein und als Pfad in der Anforderung an licenses.nuget.org verwendet werden. In einer Anforderung kann nur ein einziger Lizenzausnahmebezeichner angegeben werden. Neben dem Lizenzausnahmebezeichner dürfen im Pfadbestandteil der URL keine weiteren Zeichen enthalten sein.

| Lizenzausnahmebezeichner | Zu verwendende URL |
|:---|:---|
|FLTK-exception            | <https://licenses.nuget.org/FLTK-exception> |
|openvpn-openssl-exception | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a>Antwort

Licenses.nuget.org antwortet auf eine Anforderung mit einem bekannten Lizenzausnahmebezeichner mit einer HTTP 200-Antwort und einer Webseite, die den Referenztext für die angegebene Lizenzausnahme enthält.

Alle Anforderungen, die einen nicht unterstützten Lizenzausnahmebezeichner enthalten, führen zu einer HTTP 404-Antwort.