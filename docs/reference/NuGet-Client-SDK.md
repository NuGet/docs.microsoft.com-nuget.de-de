---
title: NuGet-Client SDK
description: Die API wird weiterentwickelt und noch nicht dokumentiert, aber Beispiele sind im Blog von Dave Glick verfügbar.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 39a4de4071eec70c88a2add158f2a3a734f7d7b7
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622927"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="977cb-103">NuGet-Client SDK</span><span class="sxs-lookup"><span data-stu-id="977cb-103">NuGet Client SDK</span></span>

<span data-ttu-id="977cb-104">Das *nuget-Client-SDK* bezieht sich auf eine Gruppe von nuget-Paketen:</span><span class="sxs-lookup"><span data-stu-id="977cb-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="977cb-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -Wird für die Interaktion mit http-und dateibasierten nuget-Feeds verwendet</span><span class="sxs-lookup"><span data-stu-id="977cb-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="977cb-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) : Wird für die Interaktion mit nuget-Paketen verwendet.</span><span class="sxs-lookup"><span data-stu-id="977cb-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="977cb-107">`NuGet.Protocol` hängt von diesem Paket ab</span><span class="sxs-lookup"><span data-stu-id="977cb-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="977cb-108">Sie finden den Quellcode für diese Pakete im GitHub [-Repository nuget/nuget. Client](https://github.com/NuGet/NuGet.Client) .</span><span class="sxs-lookup"><span data-stu-id="977cb-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="977cb-109">Dokumentation zum nuget-Server Protokoll finden Sie in der [nuget-Server-API](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="977cb-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="977cb-110">Erste Schritte</span><span class="sxs-lookup"><span data-stu-id="977cb-110">Getting started</span></span>

### <a name="install-the-packages"></a><span data-ttu-id="977cb-111">Installieren der Pakete</span><span class="sxs-lookup"><span data-stu-id="977cb-111">Install the packages</span></span>

```ps1
dotnet add package NuGet.Protocol  # interact with HTTP and folder-based NuGet package feeds, includes NuGet.Packaging

dotnet add package NuGet.Packaging # interact with .nupkg and .nuspec files from a stream
```

## <a name="examples"></a><span data-ttu-id="977cb-112">Beispiele</span><span class="sxs-lookup"><span data-stu-id="977cb-112">Examples</span></span>

<span data-ttu-id="977cb-113">Diese Beispiele finden Sie im [nuget. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) -Projekt auf GitHub.</span><span class="sxs-lookup"><span data-stu-id="977cb-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="977cb-114">Auflisten von Paketversionen</span><span class="sxs-lookup"><span data-stu-id="977cb-114">List package versions</span></span>

<span data-ttu-id="977cb-115">Alle Versionen von Newtonsoft.Jsmithilfe der [nuget v3-Paket Inhalts-API](../api/package-base-address-resource.md#enumerate-package-versions)suchen:</span><span class="sxs-lookup"><span data-stu-id="977cb-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="977cb-116">Herunterladen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="977cb-116">Download a package</span></span>

<span data-ttu-id="977cb-117">Laden Sie Newtonsoft.Jsauf v 12.0.1 mit der [nuget v3-Paket Inhalts-API](../api/package-base-address-resource.md)herunter:</span><span class="sxs-lookup"><span data-stu-id="977cb-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="977cb-118">Paket Metadaten erhalten</span><span class="sxs-lookup"><span data-stu-id="977cb-118">Get package metadata</span></span>

<span data-ttu-id="977cb-119">Holen Sie sich die Metadaten für das Paket "Newtonsoft.Json" mit der [nuget V3-Paketmetadaten-API](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="977cb-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="977cb-120">Suchen von Paketen</span><span class="sxs-lookup"><span data-stu-id="977cb-120">Search packages</span></span>

<span data-ttu-id="977cb-121">Suchen Sie mit der [nuget V3-Such-API](../api/search-query-service-resource.md)nach "JSON"-Paketen:</span><span class="sxs-lookup"><span data-stu-id="977cb-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="create-a-package"></a><span data-ttu-id="977cb-122">Erstellen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="977cb-122">Create a package</span></span>

<span data-ttu-id="977cb-123">Erstellen Sie ein Paket, legen Sie Metadaten fest, und fügen Sie mithilfe von Abhängigkeiten hinzu [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="977cb-123">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="977cb-124">Es wird dringend empfohlen, dass nuget-Pakete mit den offiziellen nuget-Tools erstellt werden, **ohne** diese Low-Level-API zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="977cb-124">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="977cb-125">Es gibt eine Vielzahl von Merkmalen, die für ein wohl geformtes Paket wichtig sind, und die neueste Version der Tools hilft bei der Integration dieser bewährten Methoden.</span><span class="sxs-lookup"><span data-stu-id="977cb-125">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="977cb-126">Weitere Informationen zum Erstellen von nuget-Paketen finden Sie in der Übersicht über den [Workflow zur Paket Erstellung](../create-packages/overview-and-workflow.md) und in der Dokumentation für offizielle Paket Tools (z. b. [über die dotnet-CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="977cb-126">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="977cb-127">Lesen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="977cb-127">Read a package</span></span>

<span data-ttu-id="977cb-128">Lesen eines Pakets aus einem Datei Datenstrom mithilfe von [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="977cb-128">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="977cb-129">Dokumentation von Drittanbietern</span><span class="sxs-lookup"><span data-stu-id="977cb-129">Third-party documentation</span></span>

<span data-ttu-id="977cb-130">Beispiele und Dokumentationen für einige der APIs finden Sie in der folgenden Blog Reihe von Dave Glick, veröffentlicht 2016:</span><span class="sxs-lookup"><span data-stu-id="977cb-130">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="977cb-131">Erkunden der nuget V3-Bibliotheken, Teil 1: Einführung und Konzepte</span><span class="sxs-lookup"><span data-stu-id="977cb-131">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="977cb-132">Erkunden der nuget V3-Bibliotheken, Teil 2: Suchen nach Paketen</span><span class="sxs-lookup"><span data-stu-id="977cb-132">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="977cb-133">Erkunden der nuget V3-Bibliotheken, Teil 3: Installieren von Paketen</span><span class="sxs-lookup"><span data-stu-id="977cb-133">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="977cb-134">Diese Blogbeiträge wurden kurz nach der Veröffentlichung der **3.4.3** -Version der nuget-Client-SDK-Pakete geschrieben.</span><span class="sxs-lookup"><span data-stu-id="977cb-134">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="977cb-135">Neuere Versionen der Pakete sind möglicherweise nicht mit den Informationen in den Blogbeiträgen kompatibel.</span><span class="sxs-lookup"><span data-stu-id="977cb-135">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="977cb-136">Martin björkström hat einen nachfolgenden Blogbeitrag zur Blog Reihe von Dave Glick durchgeführt, in dem er eine andere Vorgehensweise zum Installieren von nuget-Paketen mit dem nuget-Client-SDK einführt:</span><span class="sxs-lookup"><span data-stu-id="977cb-136">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="977cb-137">Neubesuchen der nuget V3-Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="977cb-137">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
