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
# <a name="licensesnugetorg"></a><span data-ttu-id="99d05-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="99d05-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="99d05-103">Begründung</span><span class="sxs-lookup"><span data-stu-id="99d05-103">Rationale</span></span>

<span data-ttu-id="99d05-104">Mit der Einführung der [Lizenz Ausdrücke](nuspec.md#license), gebracht, die eine Anforderung ein zuverlässigen Diensts verfügen, die einen Verweis Text für Einzelbenutzerlizenz Bezeichner, die Bezeichner der Ausnahme oder die Lizenz Ausdrücke bieten würde.</span><span class="sxs-lookup"><span data-stu-id="99d05-104">With the introduction of the [license expressions](nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="99d05-105">Eine weitere Anforderung für diesen Dienst ist ein stabiler URL-Schema haben, die nicht anfällig für Rot, verknüpfen, damit wir sie problemlos auf der Abwärtskompatibilität für ältere Clients verwenden können.</span><span class="sxs-lookup"><span data-stu-id="99d05-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="99d05-106">Diese Funktion wird von Licenses.NuGet.org erfüllt.</span><span class="sxs-lookup"><span data-stu-id="99d05-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="99d05-107">"NuGet.org" verwendet, um den Lizenz-Text-Verweis für Pakete bereitstellen, die die Lizenz, die mithilfe eines Ausdrucks Lizenz angeben.</span><span class="sxs-lookup"><span data-stu-id="99d05-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> `nuget pack` <span data-ttu-id="99d05-108">oder mit anderen Verpackung [Clienttools](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) legen Sie die [ `licenseUrl` ](nuspec.md#licenseurl) Element, zeigen Sie auf licenses.nuget.org um Abwärtskompatibilität auf Kompatibilität mit älteren Clients bereitzustellen, die nicht unterstützen die `license` Element.</span><span class="sxs-lookup"><span data-stu-id="99d05-108">or packing with other [client tools](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) set the [`licenseUrl`](nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="99d05-109">Protokoll</span><span class="sxs-lookup"><span data-stu-id="99d05-109">Protocol</span></span>

<span data-ttu-id="99d05-110">Licenses.NuGet.org von Personen in ihrem Browser angezeigt werden soll, werden keine maschinenlesbaren Antworten bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="99d05-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="99d05-111">HTTPS-Protokoll muss verwendet werden, und Anforderungen auf eine bestimmte Weise erstellt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="99d05-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="99d05-112">Unterstützt nur `GET` Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="99d05-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="99d05-113">Es akzeptiert als Eingabe in einer Weise, die unten angegebenen Lizenz-Ausdrücken oder Lizenz Ausnahme Bezeichner.</span><span class="sxs-lookup"><span data-stu-id="99d05-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="99d05-114">Beachten Sie, dass alle Elemente der Lizenz Ausdrücken Groß-/Kleinschreibung beachtet werden, und daher alle Eingaben für licenses.nuget.org ist Groß-/ Kleinschreibung sowie.</span><span class="sxs-lookup"><span data-stu-id="99d05-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="99d05-115">Lizenz-Ausdrücke</span><span class="sxs-lookup"><span data-stu-id="99d05-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="99d05-116">Anforderung</span><span class="sxs-lookup"><span data-stu-id="99d05-116">Request</span></span>

<span data-ttu-id="99d05-117">Lizenz-Ausdrücke (einschließlich der einfachen Fällen auf, wenn es sich bei Ausdruck besteht aus einer einzelnen-Lizenz) müssen [URL-codierte](https://tools.ietf.org/html/rfc3986#section-2.1) und als Pfad für die Anforderung zum licenses.nuget.org verwendet.</span><span class="sxs-lookup"><span data-stu-id="99d05-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="99d05-118">Lizenz-Ausdruck</span><span class="sxs-lookup"><span data-stu-id="99d05-118">License expression</span></span> | <span data-ttu-id="99d05-119">URL zu verwenden</span><span class="sxs-lookup"><span data-stu-id="99d05-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="99d05-120">MIT</span><span class="sxs-lookup"><span data-stu-id="99d05-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="99d05-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="99d05-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="99d05-122">(LGPL-2.0-only mit FLTK-Ausnahme oder Apache-2.0)</span><span class="sxs-lookup"><span data-stu-id="99d05-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="99d05-123">Der Dienst unterstützt nur Lizenz und Lizenz-Ausnahme-Bezeichner, die von "NuGet.org" akzeptiert werden. Alle Lizenzen-Ausdrücke, die nicht unterstützte Lizenz Bezeichner oder Bezeichner der Lizenz-Ausnahme enthalten werden oder entsprechen, die nicht zur Ausdruckssyntax Lizenz, werden als ungültig betrachtet.</span><span class="sxs-lookup"><span data-stu-id="99d05-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="99d05-124">Antwort</span><span class="sxs-lookup"><span data-stu-id="99d05-124">Response</span></span>

<span data-ttu-id="99d05-125">Licenses.NuGet.org reagiert auf Anforderungen, die mit Ausdrücken, die gültige Lizenz mit einem HTTP 200-Statuscode und einer Webseite, die mit einer Beschreibung des Ausdrucks Lizenz:</span><span class="sxs-lookup"><span data-stu-id="99d05-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="99d05-126">Lizenz-Ausdruck bereitgestellt enthält eine einzelne Lizenz-ID, die einer Webseite zurückgegeben wird, die diese Lizenz Verweis Text enthält;</span><span class="sxs-lookup"><span data-stu-id="99d05-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="99d05-127">Wenn die angegebene Lizenz-Ausdruck ist ein zusammengesetztes Lizenz-Ausdruck, wird eine Webseite zurückgegeben, die den Ausdruck "Lizenz" mit Links zu einzelnen Lizenz- oder Lizenz Ausnahme Verweise enthält.</span><span class="sxs-lookup"><span data-stu-id="99d05-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="99d05-128">Alle Anforderungen, die eine ungültige Lizenz Ergebnis des Ausdrucks in einer HTTP 404-Antwort enthalten.</span><span class="sxs-lookup"><span data-stu-id="99d05-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="99d05-129">Lizenz-Ausnahmen</span><span class="sxs-lookup"><span data-stu-id="99d05-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="99d05-130">Anforderung</span><span class="sxs-lookup"><span data-stu-id="99d05-130">Request</span></span>

<span data-ttu-id="99d05-131">Lizenz Ausnahme Bezeichner muss URL-codiert und als Pfad für die Anforderung zum licenses.nuget.org verwendet. Nur der Bezeichner eine Einzellizenz-Ausnahme kann in einer einzelnen Anforderung angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="99d05-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="99d05-132">Keine zusätzlichen Zeichen außer Ausnahme Lizenz-ID können im Pfadteil der URL vorhanden.</span><span class="sxs-lookup"><span data-stu-id="99d05-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="99d05-133">Lizenz-Ausnahme-ID</span><span class="sxs-lookup"><span data-stu-id="99d05-133">License exception identifier</span></span> | <span data-ttu-id="99d05-134">URL zu verwenden</span><span class="sxs-lookup"><span data-stu-id="99d05-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="99d05-135">FLTK-Ausnahme</span><span class="sxs-lookup"><span data-stu-id="99d05-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="99d05-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="99d05-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="99d05-137">Antwort</span><span class="sxs-lookup"><span data-stu-id="99d05-137">Response</span></span>

<span data-ttu-id="99d05-138">Licenses.NuGet.org reagiert auf eine Anforderung mit einem bekannten Lizenz Ausnahme Bezeichner mit einer HTTP 200-Antwort und eine Webseite mit dem Verweis-Text für die angegebene Lizenz-Ausnahme.</span><span class="sxs-lookup"><span data-stu-id="99d05-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="99d05-139">Jede Anforderung mit einem nicht unterstützten Lizenz Ausnahme Bezeichner führt zu einer HTTP 404-Antwort.</span><span class="sxs-lookup"><span data-stu-id="99d05-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>