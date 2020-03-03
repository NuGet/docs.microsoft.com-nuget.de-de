---
title: Nuget-Client-SDK
description: Die API wird weiterentwickelt und noch nicht dokumentiert, aber Beispiele sind im Blog von Dave Glick verfügbar.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: a5c542379318f24ee35ccf25651d0e8de91253ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231239"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="0d1ee-103">Nuget-Client-SDK</span><span class="sxs-lookup"><span data-stu-id="0d1ee-103">NuGet Client SDK</span></span>

<span data-ttu-id="0d1ee-104">Das *nuget-Client-SDK* bezieht sich auf eine Gruppe von nuget-Paketen:</span><span class="sxs-lookup"><span data-stu-id="0d1ee-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="0d1ee-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) : für die Interaktion mit http-und dateibasierten nuget-Feeds verwendet</span><span class="sxs-lookup"><span data-stu-id="0d1ee-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="0d1ee-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) , die für die Interaktion mit nuget-Paketen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="0d1ee-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="0d1ee-107">`NuGet.Protocol` hängt von diesem Paket ab.</span><span class="sxs-lookup"><span data-stu-id="0d1ee-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="0d1ee-108">Sie finden den Quellcode für diese Pakete im GitHub [-Repository nuget/nuget. Client](https://github.com/NuGet/NuGet.Client) .</span><span class="sxs-lookup"><span data-stu-id="0d1ee-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="0d1ee-109">Dokumentation zum nuget-Server Protokoll finden Sie in der [nuget-Server-API](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="0d1ee-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="0d1ee-110">Erste Schritte</span><span class="sxs-lookup"><span data-stu-id="0d1ee-110">Getting started</span></span>

### <a name="install-the-package"></a><span data-ttu-id="0d1ee-111">Installieren des Pakets</span><span class="sxs-lookup"><span data-stu-id="0d1ee-111">Install the package</span></span>

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a><span data-ttu-id="0d1ee-112">Beispiele</span><span class="sxs-lookup"><span data-stu-id="0d1ee-112">Examples</span></span>

<span data-ttu-id="0d1ee-113">Diese Beispiele finden Sie im [nuget. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) -Projekt auf GitHub.</span><span class="sxs-lookup"><span data-stu-id="0d1ee-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="0d1ee-114">Auflisten von Paketversionen</span><span class="sxs-lookup"><span data-stu-id="0d1ee-114">List package versions</span></span>

<span data-ttu-id="0d1ee-115">Suchen Sie alle Versionen von "newtonsoft. JSON" mithilfe der [nuget v3-Paket Inhalts-API](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="0d1ee-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="0d1ee-116">Herunterladen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="0d1ee-116">Download a package</span></span>

<span data-ttu-id="0d1ee-117">Laden Sie Newton Soft. JSON v 12.0.1 mit der [nuget v3-Paket Inhalts-API](../api/package-base-address-resource.md)herunter:</span><span class="sxs-lookup"><span data-stu-id="0d1ee-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="0d1ee-118">Paket Metadaten erhalten</span><span class="sxs-lookup"><span data-stu-id="0d1ee-118">Get package metadata</span></span>

<span data-ttu-id="0d1ee-119">Holen Sie sich die Metadaten für das Paket "newtonsoft. JSON" mit der [nuget V3-Paketmetadaten-API](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="0d1ee-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="0d1ee-120">Suchen von Paketen</span><span class="sxs-lookup"><span data-stu-id="0d1ee-120">Search packages</span></span>

<span data-ttu-id="0d1ee-121">Suchen Sie mit der [nuget V3-Such-API](../api/search-query-service-resource.md)nach "JSON"-Paketen:</span><span class="sxs-lookup"><span data-stu-id="0d1ee-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a><span data-ttu-id="0d1ee-122">Dokumentation von Drittanbietern</span><span class="sxs-lookup"><span data-stu-id="0d1ee-122">Third-party documentation</span></span>

<span data-ttu-id="0d1ee-123">Beispiele und Dokumentationen für einige der APIs finden Sie in der folgenden Blog Reihe von Dave Glick, veröffentlicht 2016:</span><span class="sxs-lookup"><span data-stu-id="0d1ee-123">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="0d1ee-124">Erkunden der nuget V3-Bibliotheken, Teil 1: Einführung und Konzepte</span><span class="sxs-lookup"><span data-stu-id="0d1ee-124">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="0d1ee-125">Erkunden der nuget V3-Bibliotheken, Teil 2: Suchen nach Paketen</span><span class="sxs-lookup"><span data-stu-id="0d1ee-125">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="0d1ee-126">Erkunden der nuget V3-Bibliotheken, Teil 3: Installieren von Paketen</span><span class="sxs-lookup"><span data-stu-id="0d1ee-126">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="0d1ee-127">Diese Blogbeiträge wurden kurz nach der Veröffentlichung der **3.4.3** -Version der nuget-Client-SDK-Pakete geschrieben.</span><span class="sxs-lookup"><span data-stu-id="0d1ee-127">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="0d1ee-128">Neuere Versionen der Pakete sind möglicherweise nicht mit den Informationen in den Blogbeiträgen kompatibel.</span><span class="sxs-lookup"><span data-stu-id="0d1ee-128">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="0d1ee-129">Martin björkström hat einen nachfolgenden Blogbeitrag zur Blog Reihe von Dave Glick durchgeführt, in dem er eine andere Vorgehensweise zum Installieren von nuget-Paketen mit dem nuget-Client-SDK einführt:</span><span class="sxs-lookup"><span data-stu-id="0d1ee-129">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="0d1ee-130">Neubesuchen der nuget V3-Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="0d1ee-130">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
