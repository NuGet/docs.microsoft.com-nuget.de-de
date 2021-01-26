---
title: tools.jszum Ermitteln von nuget.exe Versionen
description: Der Endpunkt für
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773820"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="78279-103">tools.jszum Ermitteln von nuget.exe Versionen</span><span class="sxs-lookup"><span data-stu-id="78279-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="78279-104">Heute gibt es mehrere Möglichkeiten, die neueste Version von nuget.exe auf Ihrem Computer in einer Skript fähigen Weise zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="78279-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="78279-105">Beispielsweise können Sie das Paket aus nuget.org herunterladen und extrahieren [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) . Dies hat eine gewisse Komplexität, da es entweder erfordert, dass Sie bereits über nuget.exe (für) verfügen, `nuget.exe install` oder Sie müssen die nupkg-Datei mit einem einfachen Entzippen Sie-Tool entzippen und die Binärdatei in suchen.</span><span class="sxs-lookup"><span data-stu-id="78279-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="78279-106">Wenn Sie bereits über nuget.exe verfügen, können Sie auch verwenden `nuget.exe update -self` . Dies erfordert jedoch auch eine vorhandene Kopie von nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="78279-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="78279-107">Bei diesem Ansatz werden Sie auch auf die neueste Version aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="78279-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="78279-108">Die Verwendung einer bestimmten Version ist nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="78279-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="78279-109">Der `tools.json` Endpunkt ist verfügbar, um das Bootstrapping-Problem zu lösen und die Kontrolle über die Version von nuget.exe zu erhalten, die Sie herunterladen.</span><span class="sxs-lookup"><span data-stu-id="78279-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="78279-110">Dies kann in CI/CD-Umgebungen oder in benutzerdefinierten Skripts verwendet werden, um eine beliebige veröffentlichte Version von nuget.exe zu ermitteln und herunterzuladen.</span><span class="sxs-lookup"><span data-stu-id="78279-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="78279-111">Der `tools.json` Endpunkt kann mit einer nicht authentifizierten http-Anforderung (z. b. `Invoke-WebRequest` in PowerShell oder) abgerufen werden `wget` .</span><span class="sxs-lookup"><span data-stu-id="78279-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="78279-112">Sie kann mit einem JSON-Deserialisierungsprogramm analysiert werden, und nachfolgende nuget.exe Download-URLs können auch mit nicht authentifizierten HTTP-Anforderungen abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="78279-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="78279-113">Der Endpunkt kann mithilfe der-Methode abgerufen werden `GET` :</span><span class="sxs-lookup"><span data-stu-id="78279-113">The endpoint can be fetched using the `GET` method:</span></span>

```
GET https://dist.nuget.org/tools.json
```

<span data-ttu-id="78279-114">Das [JSON-Schema](https://json-schema.org/) für den Endpunkt ist hier verfügbar:</span><span class="sxs-lookup"><span data-stu-id="78279-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span></span>

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a><span data-ttu-id="78279-115">Antwort</span><span class="sxs-lookup"><span data-stu-id="78279-115">Response</span></span>

<span data-ttu-id="78279-116">Die Antwort ist ein JSON-Dokument, das alle verfügbaren Versionen von nuget.exe enthält.</span><span class="sxs-lookup"><span data-stu-id="78279-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="78279-117">Das JSON-Stamm Objekt hat die folgende Eigenschaft:</span><span class="sxs-lookup"><span data-stu-id="78279-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="78279-118">Name</span><span class="sxs-lookup"><span data-stu-id="78279-118">Name</span></span>      | <span data-ttu-id="78279-119">Typ</span><span class="sxs-lookup"><span data-stu-id="78279-119">Type</span></span>             | <span data-ttu-id="78279-120">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="78279-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="78279-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="78279-121">nuget.exe</span></span> | <span data-ttu-id="78279-122">Array von Objekten</span><span class="sxs-lookup"><span data-stu-id="78279-122">array of objects</span></span> | <span data-ttu-id="78279-123">ja</span><span class="sxs-lookup"><span data-stu-id="78279-123">yes</span></span>

<span data-ttu-id="78279-124">Jedes-Objekt im- `nuget.exe` Array verfügt über die folgenden Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="78279-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="78279-125">Name</span><span class="sxs-lookup"><span data-stu-id="78279-125">Name</span></span>     | <span data-ttu-id="78279-126">Typ</span><span class="sxs-lookup"><span data-stu-id="78279-126">Type</span></span>   | <span data-ttu-id="78279-127">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="78279-127">Required</span></span> | <span data-ttu-id="78279-128">Notizen</span><span class="sxs-lookup"><span data-stu-id="78279-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="78279-129">version</span><span class="sxs-lookup"><span data-stu-id="78279-129">version</span></span>  | <span data-ttu-id="78279-130">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="78279-130">string</span></span> | <span data-ttu-id="78279-131">ja</span><span class="sxs-lookup"><span data-stu-id="78279-131">yes</span></span>      | <span data-ttu-id="78279-132">Semver 2.0.0-Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="78279-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="78279-133">url</span><span class="sxs-lookup"><span data-stu-id="78279-133">url</span></span>      | <span data-ttu-id="78279-134">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="78279-134">string</span></span> | <span data-ttu-id="78279-135">ja</span><span class="sxs-lookup"><span data-stu-id="78279-135">yes</span></span>      | <span data-ttu-id="78279-136">Eine absolute URL zum Herunterladen dieser Version von nuget.exe</span><span class="sxs-lookup"><span data-stu-id="78279-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="78279-137">Stufe</span><span class="sxs-lookup"><span data-stu-id="78279-137">stage</span></span>    | <span data-ttu-id="78279-138">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="78279-138">string</span></span> | <span data-ttu-id="78279-139">ja</span><span class="sxs-lookup"><span data-stu-id="78279-139">yes</span></span>      | <span data-ttu-id="78279-140">Eine Enumeration-Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="78279-140">An enum string</span></span>
<span data-ttu-id="78279-141">aufgeladen</span><span class="sxs-lookup"><span data-stu-id="78279-141">uploaded</span></span> | <span data-ttu-id="78279-142">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="78279-142">string</span></span> | <span data-ttu-id="78279-143">ja</span><span class="sxs-lookup"><span data-stu-id="78279-143">yes</span></span>      | <span data-ttu-id="78279-144">Der ungefähre ISO 8601-Zeitstempel, zu dem die Version verfügbar gemacht wurde.</span><span class="sxs-lookup"><span data-stu-id="78279-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="78279-145">Die Elemente im Array werden in absteigender, semver 2.0.0-Reihenfolge sortiert.</span><span class="sxs-lookup"><span data-stu-id="78279-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="78279-146">Diese Garantie soll die Belastung eines Clients verringern, der an der höchsten Versionsnummer interessiert ist.</span><span class="sxs-lookup"><span data-stu-id="78279-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="78279-147">Dies bedeutet jedoch, dass die Liste nicht in chronologischer Reihenfolge sortiert ist.</span><span class="sxs-lookup"><span data-stu-id="78279-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="78279-148">Wenn z. b. eine niedrigere Hauptversion zu einem späteren Zeitpunkt als eine höhere Hauptversion gewartet wird, wird diese Serviced Version nicht am Anfang der Liste angezeigt.</span><span class="sxs-lookup"><span data-stu-id="78279-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="78279-149">Wenn Sie die neueste Version von *Zeitstempel* veröffentlichen möchten, Sortieren Sie das Array einfach nach der `uploaded` Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="78279-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="78279-150">Dies funktioniert, da der `uploaded` Zeitstempel das [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) -Format aufweist, das mithilfe einer lexikografischen Sortierung (d.h. einer einfachen Zeichen folgen Sortierung) alphabe ologisch sortiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="78279-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="78279-151">Die- `stage` Eigenschaft gibt an, wie diese Version des Tools überprüft wurde.</span><span class="sxs-lookup"><span data-stu-id="78279-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="78279-152">Phase</span><span class="sxs-lookup"><span data-stu-id="78279-152">Stage</span></span>              | <span data-ttu-id="78279-153">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="78279-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="78279-154">Earlyaccesspview</span><span class="sxs-lookup"><span data-stu-id="78279-154">EarlyAccessPreview</span></span> | <span data-ttu-id="78279-155">Noch nicht auf der [Download Webseite](https://www.nuget.org/downloads) sichtbar und sollte von Partnern überprüft werden.</span><span class="sxs-lookup"><span data-stu-id="78279-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="78279-156">Freigegeben</span><span class="sxs-lookup"><span data-stu-id="78279-156">Released</span></span>           | <span data-ttu-id="78279-157">Verfügbar auf der Download Website, wird aber noch nicht für den breiten Verbrauch empfohlen.</span><span class="sxs-lookup"><span data-stu-id="78279-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="78279-158">Releasedandblessed</span><span class="sxs-lookup"><span data-stu-id="78279-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="78279-159">Auf der Download Website verfügbar und wird für den Verbrauch empfohlen.</span><span class="sxs-lookup"><span data-stu-id="78279-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="78279-160">Eine einfache Methode zur Verwendung der neuesten, empfohlenen Version ist die Verwendung der ersten Version in der Liste mit dem `stage` Wert von `ReleasedAndBlessed` .</span><span class="sxs-lookup"><span data-stu-id="78279-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="78279-161">Dies funktioniert, da die Versionen in der semver 2.0.0-Reihenfolge sortiert sind.</span><span class="sxs-lookup"><span data-stu-id="78279-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="78279-162">Das `NuGet.CommandLine` Paket auf nuget.org wird in der Regel nur mit `ReleasedAndBlessed` Versionen aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="78279-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="78279-163">Beispiel für eine Anforderung</span><span class="sxs-lookup"><span data-stu-id="78279-163">Sample request</span></span>

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a><span data-ttu-id="78279-164">Beispiel für eine Antwort</span><span class="sxs-lookup"><span data-stu-id="78279-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
