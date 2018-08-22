---
title: Tools.JSON für die Ermittlung von nuget.exe-Versionen
description: Der Endpunkt für
author: jver
ms.author: jver
manager: skofman
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d11e79cd9109e1760189e848e35ff322be026a4d
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/21/2018
ms.locfileid: "40247959"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="e3bdc-103">Tools.JSON für die Ermittlung von nuget.exe-Versionen</span><span class="sxs-lookup"><span data-stu-id="e3bdc-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="e3bdc-104">Heute stehen mehrere Möglichkeiten, um die neueste Version von nuget.exe auf Ihrem Computer in skriptfähiger Weise zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="e3bdc-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="e3bdc-105">Sie können z. B. herunterladen und extrahieren Sie die [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) Paket von nuget.org. Dies hat gewisse Komplexität, da sie entweder erfordert, dass Sie bereits nuget.exe (für `nuget.exe install`), oder Sie über Entzippen der NUPKG-Datei mit einem einfachen Unzip-Tool, und suchen den binären inneren.</span><span class="sxs-lookup"><span data-stu-id="e3bdc-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="e3bdc-106">Wenn Sie bereits nuget.exe verfügen, können Sie auch `nuget.exe update -self`, aber auch dafür müssen eine Kopie von nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="e3bdc-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="e3bdc-107">Dadurch werden auch Sie auf die neueste Version aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="e3bdc-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="e3bdc-108">Es lässt sich nicht auf die Verwendung einer bestimmten Version aus.</span><span class="sxs-lookup"><span data-stu-id="e3bdc-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="e3bdc-109">Die `tools.json` Endpunkt ist verfügbar, um sowohl das bootstrapping Problem lösen, und Steuern der Version von nuget.exe zu können, die Sie herunterladen.</span><span class="sxs-lookup"><span data-stu-id="e3bdc-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="e3bdc-110">Dies dient in der CI/CD-Umgebungen oder benutzerdefinierte Skripts zum Ermitteln und alle endgültigen Produktversion von nuget.exe herunterladen.</span><span class="sxs-lookup"><span data-stu-id="e3bdc-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="e3bdc-111">Die `tools.json` Endpunkt mit einer nicht authentifizierten HTTP-Anforderung abgerufen werden (z. B. `Invoke-WebRequest` in PowerShell oder `wget`).</span><span class="sxs-lookup"><span data-stu-id="e3bdc-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="e3bdc-112">Sie können mit einer JSON-Deserialisierung analysiert werden, und nachfolgende nuget.exe-Download, die URLs auch abgerufen werden können, mit nicht authentifizierten HTTP-Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="e3bdc-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="e3bdc-113">Der Endpunkt kann abgerufen werden, mithilfe der `GET` Methode:</span><span class="sxs-lookup"><span data-stu-id="e3bdc-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="e3bdc-114">Die [JSON-Schema](http://json-schema.org/) für der Endpunkt hier verfügbar ist:</span><span class="sxs-lookup"><span data-stu-id="e3bdc-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="e3bdc-115">Antwort</span><span class="sxs-lookup"><span data-stu-id="e3bdc-115">Response</span></span>

<span data-ttu-id="e3bdc-116">Die Antwort ist ein JSON-Dokument, das alle verfügbaren Versionen der nuget.exe enthält.</span><span class="sxs-lookup"><span data-stu-id="e3bdc-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="e3bdc-117">Die JSON-Stammobjekt hat die folgende Eigenschaft:</span><span class="sxs-lookup"><span data-stu-id="e3bdc-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="e3bdc-118">name</span><span class="sxs-lookup"><span data-stu-id="e3bdc-118">Name</span></span>      | <span data-ttu-id="e3bdc-119">Typ</span><span class="sxs-lookup"><span data-stu-id="e3bdc-119">Type</span></span>             | <span data-ttu-id="e3bdc-120">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="e3bdc-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="e3bdc-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="e3bdc-121">nuget.exe</span></span> | <span data-ttu-id="e3bdc-122">Array von Objekten</span><span class="sxs-lookup"><span data-stu-id="e3bdc-122">array of objects</span></span> | <span data-ttu-id="e3bdc-123">ja</span><span class="sxs-lookup"><span data-stu-id="e3bdc-123">yes</span></span>

<span data-ttu-id="e3bdc-124">Jedes Objekt in der `nuget.exe` Array verfügt über die folgenden Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="e3bdc-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="e3bdc-125">name</span><span class="sxs-lookup"><span data-stu-id="e3bdc-125">Name</span></span>     | <span data-ttu-id="e3bdc-126">Typ</span><span class="sxs-lookup"><span data-stu-id="e3bdc-126">Type</span></span>   | <span data-ttu-id="e3bdc-127">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="e3bdc-127">Required</span></span> | <span data-ttu-id="e3bdc-128">Hinweise</span><span class="sxs-lookup"><span data-stu-id="e3bdc-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="e3bdc-129">Version</span><span class="sxs-lookup"><span data-stu-id="e3bdc-129">version</span></span>  | <span data-ttu-id="e3bdc-130">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="e3bdc-130">string</span></span> | <span data-ttu-id="e3bdc-131">ja</span><span class="sxs-lookup"><span data-stu-id="e3bdc-131">yes</span></span>      | <span data-ttu-id="e3bdc-132">Eine Zeichenfolge SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="e3bdc-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="e3bdc-133">url</span><span class="sxs-lookup"><span data-stu-id="e3bdc-133">url</span></span>      | <span data-ttu-id="e3bdc-134">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="e3bdc-134">string</span></span> | <span data-ttu-id="e3bdc-135">ja</span><span class="sxs-lookup"><span data-stu-id="e3bdc-135">yes</span></span>      | <span data-ttu-id="e3bdc-136">Eine absolute URL für das Herunterladen dieser Version von nuget.exe</span><span class="sxs-lookup"><span data-stu-id="e3bdc-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="e3bdc-137">Phase</span><span class="sxs-lookup"><span data-stu-id="e3bdc-137">stage</span></span>    | <span data-ttu-id="e3bdc-138">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="e3bdc-138">string</span></span> | <span data-ttu-id="e3bdc-139">ja</span><span class="sxs-lookup"><span data-stu-id="e3bdc-139">yes</span></span>      | <span data-ttu-id="e3bdc-140">Eine Enum-Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="e3bdc-140">An enum string</span></span>
<span data-ttu-id="e3bdc-141">hochgeladen</span><span class="sxs-lookup"><span data-stu-id="e3bdc-141">uploaded</span></span> | <span data-ttu-id="e3bdc-142">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="e3bdc-142">string</span></span> | <span data-ttu-id="e3bdc-143">ja</span><span class="sxs-lookup"><span data-stu-id="e3bdc-143">yes</span></span>      | <span data-ttu-id="e3bdc-144">Wenn die Version zur Verfügung gestellt wurde eine ungefähre Zeitstempel</span><span class="sxs-lookup"><span data-stu-id="e3bdc-144">An approximate timestamp of when the version was made available</span></span>

<span data-ttu-id="e3bdc-145">Die Elemente im Array werden in absteigender, SemVer 2.0.0-Reihenfolge sortiert werden.</span><span class="sxs-lookup"><span data-stu-id="e3bdc-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="e3bdc-146">Diese Garantie ist vorgesehen, um die Last auf einem Client, suchen Sie die neueste Version zu erleichtern.</span><span class="sxs-lookup"><span data-stu-id="e3bdc-146">This guarantee is meant to ease the burden on a client looking for the latest version.</span></span> 

<span data-ttu-id="e3bdc-147">Die `stage` Eigenschaft gibt an, wie Vettect für diese Version des Tools ist.</span><span class="sxs-lookup"><span data-stu-id="e3bdc-147">The `stage` property indicates how vettect this version of the tool is.</span></span> 

<span data-ttu-id="e3bdc-148">Stufe</span><span class="sxs-lookup"><span data-stu-id="e3bdc-148">Stage</span></span>              | <span data-ttu-id="e3bdc-149">Bedeutung</span><span class="sxs-lookup"><span data-stu-id="e3bdc-149">Meaning</span></span>
------------------ | ------
<span data-ttu-id="e3bdc-150">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="e3bdc-150">EarlyAccessPreview</span></span> | <span data-ttu-id="e3bdc-151">Nicht noch sichtbar ist, auf die [Webseite herunterladen](https://www.nuget.org/downloads) und überprüft werden soll, von Partnern</span><span class="sxs-lookup"><span data-stu-id="e3bdc-151">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="e3bdc-152">Freigegeben</span><span class="sxs-lookup"><span data-stu-id="e3bdc-152">Released</span></span>           | <span data-ttu-id="e3bdc-153">Verfügbar auf der Downloadwebsite aber noch nicht für die umfassende Nutzung empfohlen</span><span class="sxs-lookup"><span data-stu-id="e3bdc-153">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="e3bdc-154">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="e3bdc-154">ReleasedAndBlessed</span></span> | <span data-ttu-id="e3bdc-155">Auf der Downloadwebsite verfügbar und wird empfohlen, für die Nutzung</span><span class="sxs-lookup"><span data-stu-id="e3bdc-155">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="e3bdc-156">Ein einfacher Ansatz dafür, die neueste empfohlene Version ist, wird von der ersten Version in der Liste, die die `stage` Wert `ReleasedAndBlessed`.</span><span class="sxs-lookup"><span data-stu-id="e3bdc-156">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span>

<span data-ttu-id="e3bdc-157">Die `NuGet.CommandLine` Pakets auf nuget.org werden in der Regel nur mit aktualisiert `ReleasedAndBlessed` Versionen.</span><span class="sxs-lookup"><span data-stu-id="e3bdc-157">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e3bdc-158">Beispiel für eine Anforderung</span><span class="sxs-lookup"><span data-stu-id="e3bdc-158">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="e3bdc-159">Beispielantwort</span><span class="sxs-lookup"><span data-stu-id="e3bdc-159">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
