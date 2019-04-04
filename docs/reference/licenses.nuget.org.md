---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 4a40cc1f7d333e8d35a721f3eed2e6b9365faf7b
ms.sourcegitcommit: 8793f528a11bd8e8fb229cd12e9abba50d61e104
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2019
ms.locfileid: "58921558"
---
# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>Begründung

Mit der Einführung der [Lizenz Ausdrücke](nuspec.md#license), gebracht, die eine Anforderung ein zuverlässigen Diensts verfügen, die einen Verweis Text für Einzelbenutzerlizenz Bezeichner, die Bezeichner der Ausnahme oder die Lizenz Ausdrücke bieten würde.
Eine weitere Anforderung für diesen Dienst ist ein stabiler URL-Schema haben, die nicht anfällig für Rot, verknüpfen, damit wir sie problemlos auf der Abwärtskompatibilität für ältere Clients verwenden können.

Diese Funktion wird von Licenses.NuGet.org erfüllt. "NuGet.org" verwendet, um den Lizenz-Text-Verweis für Pakete bereitstellen, die die Lizenz, die mithilfe eines Ausdrucks Lizenz angeben. `nuget pack` oder mit anderen Verpackung [Clienttools](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) legen Sie die [ `licenseUrl` ](nuspec.md#licenseurl) Element, zeigen Sie auf licenses.nuget.org um Abwärtskompatibilität auf Kompatibilität mit älteren Clients bereitzustellen, die nicht unterstützen die `license` Element.

## <a name="protocol"></a>Protokoll

Licenses.NuGet.org von Personen in ihrem Browser angezeigt werden soll, werden keine maschinenlesbaren Antworten bereitgestellt werden.
HTTPS-Protokoll muss verwendet werden, und Anforderungen auf eine bestimmte Weise erstellt werden sollen. Unterstützt nur `GET` Anforderungen.
Es akzeptiert als Eingabe in einer Weise, die unten angegebenen Lizenz-Ausdrücken oder Lizenz Ausnahme Bezeichner. Beachten Sie, dass alle Elemente der Lizenz Ausdrücken Groß-/Kleinschreibung beachtet werden, und daher alle Eingaben für licenses.nuget.org ist Groß-/ Kleinschreibung sowie.

### <a name="license-expressions"></a>Lizenz-Ausdrücke

#### <a name="request"></a>Anforderung

Lizenz-Ausdrücke (einschließlich der einfachen Fällen auf, wenn es sich bei Ausdruck besteht aus einer einzelnen-Lizenz) müssen [URL-codierte](https://tools.ietf.org/html/rfc3986#section-2.1) und als Pfad für die Anforderung zum licenses.nuget.org verwendet.

| Lizenz-Ausdruck | URL zu verwenden |
|:---|:---|
| MIT                                                | <https://licenses.nuget.org/MIT> |
| (MIT)                                              | <https://licenses.nuget.org/(MIT)> |
| (LGPL-2.0-only mit FLTK-Ausnahme oder Apache-2.0) | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

Der Dienst unterstützt nur Lizenz und Lizenz-Ausnahme-Bezeichner, die von "NuGet.org" akzeptiert werden. Alle Lizenzen-Ausdrücke, die nicht unterstützte Lizenz Bezeichner oder Bezeichner der Lizenz-Ausnahme enthalten werden oder entsprechen, die nicht zur Ausdruckssyntax Lizenz, werden als ungültig betrachtet.

#### <a name="response"></a>Antwort

Licenses.NuGet.org reagiert auf Anforderungen, die mit Ausdrücken, die gültige Lizenz mit einem HTTP 200-Statuscode und einer Webseite, die mit einer Beschreibung des Ausdrucks Lizenz:

* Lizenz-Ausdruck bereitgestellt enthält eine einzelne Lizenz-ID, die einer Webseite zurückgegeben wird, die diese Lizenz Verweis Text enthält;
* Wenn die angegebene Lizenz-Ausdruck ist ein zusammengesetztes Lizenz-Ausdruck, wird eine Webseite zurückgegeben, die den Ausdruck "Lizenz" mit Links zu einzelnen Lizenz- oder Lizenz Ausnahme Verweise enthält.

Alle Anforderungen, die eine ungültige Lizenz Ergebnis des Ausdrucks in einer HTTP 404-Antwort enthalten.

### <a name="license-exceptions"></a>Lizenz-Ausnahmen

#### <a name="request"></a>Anforderung

Lizenz Ausnahme Bezeichner muss URL-codiert und als Pfad für die Anforderung zum licenses.nuget.org verwendet. Nur der Bezeichner eine Einzellizenz-Ausnahme kann in einer einzelnen Anforderung angegeben werden. Keine zusätzlichen Zeichen außer Ausnahme Lizenz-ID können im Pfadteil der URL vorhanden.

| Lizenz-Ausnahme-ID | URL zu verwenden |
|:---|:---|
|FLTK-Ausnahme            | <https://licenses.nuget.org/FLTK-exception> |
|openvpn-openssl-exception | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a>Antwort

Licenses.NuGet.org reagiert auf eine Anforderung mit einem bekannten Lizenz Ausnahme Bezeichner mit einer HTTP 200-Antwort und eine Webseite mit dem Verweis-Text für die angegebene Lizenz-Ausnahme.

Jede Anforderung mit einem nicht unterstützten Lizenz Ausnahme Bezeichner führt zu einer HTTP 404-Antwort.