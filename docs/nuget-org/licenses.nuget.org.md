---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 717cf8c47335c620410be71300b07de82799e1d3
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427115"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="d5e84-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="d5e84-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="d5e84-103">Begründung</span><span class="sxs-lookup"><span data-stu-id="d5e84-103">Rationale</span></span>

<span data-ttu-id="d5e84-104">Mit der Einführung von [Lizenzausdrücken](../reference/nuspec.md#license) entstand der Bedarf nach einem zuverlässigen Dienst, der einen Referenztext für einzelne Lizenzbezeichner, Ausnahmebezeichner oder Lizenzausdrücke bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="d5e84-104">With the introduction of the [license expressions](../reference/nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="d5e84-105">Eine zusätzliche Anforderung an diesen Dienst ist ein stabiles URL-Schema, das nicht für tote Links anfällig ist und sicher verwendet werden kann, um Abwärtskompatibilität für ältere Clients zu gewährleisten.</span><span class="sxs-lookup"><span data-stu-id="d5e84-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="d5e84-106">Licenses.nuget.org erfüllt diese Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="d5e84-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="d5e84-107">Nuget.org nutzt Licenses.nuget.org, um die Lizenztextreferenz für Pakete bereitzustellen, die ihre Lizenz über einen Lizenzausdruck angeben.</span><span class="sxs-lookup"><span data-stu-id="d5e84-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="d5e84-108">Über `nuget pack` oder bei einer Paketierung mit anderen [Clienttools](../install-nuget-client-tools.md) wird das [`licenseUrl`](../reference/nuspec.md#licenseurl)-Element zum Verweis auf licenses.nuget.org festgelegt, um Abwärtskompatibilität mit älteren Clients bereitzustellen, die das `license`-Element nicht unterstützen.</span><span class="sxs-lookup"><span data-stu-id="d5e84-108">`nuget pack` or packing with other [client tools](../install-nuget-client-tools.md) set the [`licenseUrl`](../reference/nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="d5e84-109">Protokoll</span><span class="sxs-lookup"><span data-stu-id="d5e84-109">Protocol</span></span>

<span data-ttu-id="d5e84-110">Licenses.nuget.org ist für die Anzeige in einem Browser durch Personen vorgesehen, es werden keine maschinenlesbaren Antworten bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="d5e84-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="d5e84-111">Das HTTPS-Protokoll ist erforderlich, und Anforderungen müssen in einer bestimmten Weise erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="d5e84-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="d5e84-112">Es werden nur `GET`-Anforderungen unterstützt.</span><span class="sxs-lookup"><span data-stu-id="d5e84-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="d5e84-113">Lizenzausdrücke oder Lizenzausnahmebezeichner werden in der unten angegebenen Weise als Eingabe akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="d5e84-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="d5e84-114">Beachten Sie, dass für alle Elemente von Lizenzausdrücken die Groß-/Kleinschreibung beachtet werden muss, deshalb gilt für alle Eingaben in licenses.nuget.org ebenfalls die Beachtung der Groß-/Kleinschreibung.</span><span class="sxs-lookup"><span data-stu-id="d5e84-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="d5e84-115">Lizenzausdrücke</span><span class="sxs-lookup"><span data-stu-id="d5e84-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="d5e84-116">Anforderung</span><span class="sxs-lookup"><span data-stu-id="d5e84-116">Request</span></span>

<span data-ttu-id="d5e84-117">Lizenzausdrücke (einschließlich trivialer Fälle, in denen ein Ausdruck nur aus einer Lizenz besteht) müssen [URL-codiert](https://tools.ietf.org/html/rfc3986#section-2.1) sein und als Pfad in der Anforderung an licenses.nuget.org verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="d5e84-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="d5e84-118">Lizenzausdruck</span><span class="sxs-lookup"><span data-stu-id="d5e84-118">License expression</span></span> | <span data-ttu-id="d5e84-119">Zu verwendende URL</span><span class="sxs-lookup"><span data-stu-id="d5e84-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="d5e84-120">MIT</span><span class="sxs-lookup"><span data-stu-id="d5e84-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="d5e84-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="d5e84-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="d5e84-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span><span class="sxs-lookup"><span data-stu-id="d5e84-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="d5e84-123">Der Dienst unterstützt nur Lizenzbezeichner und Lizenzausnahmebezeichner, die von nuget.org akzeptiert werden. Alle Lizenzausdrücke, die nicht unterstützte Lizenzbezeichner oder Lizenzausnahmebezeichner enthalten oder nicht der Syntax für Lizenzausdrücke entsprechen, werden als ungültig betrachtet.</span><span class="sxs-lookup"><span data-stu-id="d5e84-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="d5e84-124">Antwort</span><span class="sxs-lookup"><span data-stu-id="d5e84-124">Response</span></span>

<span data-ttu-id="d5e84-125">Licenses.nuget.org antwortet auf Anforderungen, die einen gültigen Lizenzausdruck enthalten, mit einem HTTP 200-Statuscode und einer Webseite mit einer Beschreibung des Lizenzausdrucks:</span><span class="sxs-lookup"><span data-stu-id="d5e84-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="d5e84-126">Wenn der angegebene Lizenzausdruck einen einzelnen Lizenzbezeichner umfasst, wird eine Webseite zurückgegeben, die diesen Lizenzreferenztext enthält.</span><span class="sxs-lookup"><span data-stu-id="d5e84-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="d5e84-127">Wenn der angegebene Lizenzausdruck ein zusammengesetzter Lizenzausdruck ist, wird eine Webseite zurückgegeben, die den Lizenzausdruck mit Links zu den einzelnen Lizenz- oder Lizenzausnahmereferenzen enthält.</span><span class="sxs-lookup"><span data-stu-id="d5e84-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="d5e84-128">Alle Anforderungen, die einen ungültigen Lizenzausdruck enthalten, führen zu einer HTTP 404-Antwort.</span><span class="sxs-lookup"><span data-stu-id="d5e84-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="d5e84-129">Lizenzausnahmen</span><span class="sxs-lookup"><span data-stu-id="d5e84-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="d5e84-130">Anforderung</span><span class="sxs-lookup"><span data-stu-id="d5e84-130">Request</span></span>

<span data-ttu-id="d5e84-131">Lizenzausnahmebezeichner müssen URL-codiert sein und als Pfad in der Anforderung an licenses.nuget.org verwendet werden. In einer Anforderung kann nur ein einziger Lizenzausnahmebezeichner angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="d5e84-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="d5e84-132">Neben dem Lizenzausnahmebezeichner dürfen im Pfadbestandteil der URL keine weiteren Zeichen enthalten sein.</span><span class="sxs-lookup"><span data-stu-id="d5e84-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="d5e84-133">Lizenzausnahmebezeichner</span><span class="sxs-lookup"><span data-stu-id="d5e84-133">License exception identifier</span></span> | <span data-ttu-id="d5e84-134">Zu verwendende URL</span><span class="sxs-lookup"><span data-stu-id="d5e84-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="d5e84-135">FLTK-exception</span><span class="sxs-lookup"><span data-stu-id="d5e84-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="d5e84-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="d5e84-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="d5e84-137">Antwort</span><span class="sxs-lookup"><span data-stu-id="d5e84-137">Response</span></span>

<span data-ttu-id="d5e84-138">Licenses.nuget.org antwortet auf eine Anforderung mit einem bekannten Lizenzausnahmebezeichner mit einer HTTP 200-Antwort und einer Webseite, die den Referenztext für die angegebene Lizenzausnahme enthält.</span><span class="sxs-lookup"><span data-stu-id="d5e84-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="d5e84-139">Alle Anforderungen, die einen nicht unterstützten Lizenzausnahmebezeichner enthalten, führen zu einer HTTP 404-Antwort.</span><span class="sxs-lookup"><span data-stu-id="d5e84-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>