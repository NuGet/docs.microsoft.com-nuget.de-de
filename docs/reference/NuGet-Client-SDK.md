---
title: NuGet-Client SDK
description: Die API wird weiterentwickelt und noch nicht dokumentiert, aber Beispiele sind im Blog von Dave Glick verfügbar.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: e89b50601deb204892536406b4ddabf7005e0642
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776125"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="2bf96-103">NuGet-Client SDK</span><span class="sxs-lookup"><span data-stu-id="2bf96-103">NuGet Client SDK</span></span>

<span data-ttu-id="2bf96-104">Das *nuget-Client-SDK* bezieht sich auf eine Gruppe von nuget-Paketen:</span><span class="sxs-lookup"><span data-stu-id="2bf96-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="2bf96-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -Wird für die Interaktion mit http-und dateibasierten nuget-Feeds verwendet</span><span class="sxs-lookup"><span data-stu-id="2bf96-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="2bf96-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) : Wird für die Interaktion mit nuget-Paketen verwendet.</span><span class="sxs-lookup"><span data-stu-id="2bf96-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="2bf96-107">`NuGet.Protocol` hängt von diesem Paket ab</span><span class="sxs-lookup"><span data-stu-id="2bf96-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="2bf96-108">Sie finden den Quellcode für diese Pakete im GitHub [-Repository nuget/nuget. Client](https://github.com/NuGet/NuGet.Client) .</span><span class="sxs-lookup"><span data-stu-id="2bf96-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>
<span data-ttu-id="2bf96-109">Den Quellcode für diese Beispiele finden Sie im [nuget. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) -Projekt auf GitHub.</span><span class="sxs-lookup"><span data-stu-id="2bf96-109">You can find the source code for these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

> [!Note]
> <span data-ttu-id="2bf96-110">Dokumentation zum nuget-Server Protokoll finden Sie in der [nuget-Server-API](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="2bf96-110">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="nugetprotocol"></a><span data-ttu-id="2bf96-111">"Nuget. Protocol"</span><span class="sxs-lookup"><span data-stu-id="2bf96-111">NuGet.Protocol</span></span>

<span data-ttu-id="2bf96-112">Installieren `NuGet.Protocol` Sie das Paket, um mit http-und Ordner basierten nuget-Paket Feeds zu interagieren:</span><span class="sxs-lookup"><span data-stu-id="2bf96-112">Install the `NuGet.Protocol` package to interact with HTTP and folder-based NuGet package feeds:</span></span>

```ps1
dotnet add package NuGet.Protocol
```

### <a name="list-package-versions"></a><span data-ttu-id="2bf96-113">Auflisten von Paketversionen</span><span class="sxs-lookup"><span data-stu-id="2bf96-113">List package versions</span></span>

<span data-ttu-id="2bf96-114">Alle Versionen von Newtonsoft.Jsmithilfe der [nuget v3-Paket Inhalts-API](../api/package-base-address-resource.md#enumerate-package-versions)suchen:</span><span class="sxs-lookup"><span data-stu-id="2bf96-114">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="2bf96-115">Herunterladen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="2bf96-115">Download a package</span></span>

<span data-ttu-id="2bf96-116">Laden Sie Newtonsoft.Jsauf v 12.0.1 mit der [nuget v3-Paket Inhalts-API](../api/package-base-address-resource.md)herunter:</span><span class="sxs-lookup"><span data-stu-id="2bf96-116">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="2bf96-117">Paket Metadaten erhalten</span><span class="sxs-lookup"><span data-stu-id="2bf96-117">Get package metadata</span></span>

<span data-ttu-id="2bf96-118">Holen Sie sich die Metadaten für das Paket "Newtonsoft.Json" mit der [nuget V3-Paketmetadaten-API](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="2bf96-118">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="2bf96-119">Suchen von Paketen</span><span class="sxs-lookup"><span data-stu-id="2bf96-119">Search packages</span></span>

<span data-ttu-id="2bf96-120">Suchen Sie mit der [nuget V3-Such-API](../api/search-query-service-resource.md)nach "JSON"-Paketen:</span><span class="sxs-lookup"><span data-stu-id="2bf96-120">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a><span data-ttu-id="2bf96-121">Pushen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="2bf96-121">Push a package</span></span>

<span data-ttu-id="2bf96-122">Übertragung eines Pakets über die [nuget V3-Push-und-DELETE-API](../api/package-publish-resource.md):</span><span class="sxs-lookup"><span data-stu-id="2bf96-122">Push a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a><span data-ttu-id="2bf96-123">Löschen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="2bf96-123">Delete a package</span></span>

<span data-ttu-id="2bf96-124">Löschen eines Pakets mit der [nuget V3-Push-und DELETE-API](../api/package-publish-resource.md):</span><span class="sxs-lookup"><span data-stu-id="2bf96-124">Delete a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

> [!Note]
> <span data-ttu-id="2bf96-125">Nuget-Server können eine Paket Löschanforderung als "Hard Delete", "Vorläufiges löschen" oder "Unlist" interpretieren.</span><span class="sxs-lookup"><span data-stu-id="2bf96-125">NuGet servers are free to interpret a package delete request as a "hard delete", "soft delete", or "unlist".</span></span>
> <span data-ttu-id="2bf96-126">Nuget.org interpretiert z. b. die DELETE-Anforderung des Pakets als "Unlist".</span><span class="sxs-lookup"><span data-stu-id="2bf96-126">For example, nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="2bf96-127">Weitere Informationen zu dieser Vorgehensweise finden Sie in der Richtlinie zum [Löschen von Paketen](../nuget-org/policies/deleting-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="2bf96-127">For more information about this practice, see the [Deleting Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span>

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a><span data-ttu-id="2bf96-128">Arbeiten mit authentifizierten Feeds</span><span class="sxs-lookup"><span data-stu-id="2bf96-128">Work with authenticated feeds</span></span>

<span data-ttu-id="2bf96-129">Verwenden [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) Sie, um mit authentifizierten Feeds zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="2bf96-129">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) to work with authenticated feeds.</span></span>

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a><span data-ttu-id="2bf96-130">Nuget. Packaging</span><span class="sxs-lookup"><span data-stu-id="2bf96-130">NuGet.Packaging</span></span>

<span data-ttu-id="2bf96-131">Installieren `NuGet.Packaging` Sie das Paket, um mit `.nupkg` -und- `.nuspec` Dateien aus einem Stream zu interagieren:</span><span class="sxs-lookup"><span data-stu-id="2bf96-131">Install the `NuGet.Packaging` package to interact with `.nupkg` and `.nuspec` files from a stream:</span></span>

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a><span data-ttu-id="2bf96-132">Erstellen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="2bf96-132">Create a package</span></span>

<span data-ttu-id="2bf96-133">Erstellen Sie ein Paket, legen Sie Metadaten fest, und fügen Sie mithilfe von Abhängigkeiten hinzu [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="2bf96-133">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2bf96-134">Es wird dringend empfohlen, dass nuget-Pakete mit den offiziellen nuget-Tools erstellt werden, **ohne** diese Low-Level-API zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="2bf96-134">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="2bf96-135">Es gibt eine Vielzahl von Merkmalen, die für ein wohl geformtes Paket wichtig sind, und die neueste Version der Tools hilft bei der Integration dieser bewährten Methoden.</span><span class="sxs-lookup"><span data-stu-id="2bf96-135">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="2bf96-136">Weitere Informationen zum Erstellen von nuget-Paketen finden Sie in der Übersicht über den [Workflow zur Paket Erstellung](../create-packages/overview-and-workflow.md) und in der Dokumentation für offizielle Paket Tools (z. b. [über die dotnet-CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="2bf96-136">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="2bf96-137">Lesen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="2bf96-137">Read a package</span></span>

<span data-ttu-id="2bf96-138">Lesen eines Pakets aus einem Datei Datenstrom mithilfe von [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="2bf96-138">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="2bf96-139">Dokumentation von Drittanbietern</span><span class="sxs-lookup"><span data-stu-id="2bf96-139">Third-party documentation</span></span>

<span data-ttu-id="2bf96-140">Beispiele und Dokumentationen für einige der APIs finden Sie in der folgenden Blog Reihe von Dave Glick, veröffentlicht 2016:</span><span class="sxs-lookup"><span data-stu-id="2bf96-140">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="2bf96-141">Erkunden der nuget V3-Bibliotheken, Teil 1: Einführung und Konzepte</span><span class="sxs-lookup"><span data-stu-id="2bf96-141">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="2bf96-142">Erkunden der nuget V3-Bibliotheken, Teil 2: Suchen nach Paketen</span><span class="sxs-lookup"><span data-stu-id="2bf96-142">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="2bf96-143">Erkunden der nuget V3-Bibliotheken, Teil 3: Installieren von Paketen</span><span class="sxs-lookup"><span data-stu-id="2bf96-143">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="2bf96-144">Diese Blogbeiträge wurden kurz nach der Veröffentlichung der **3.4.3** -Version der nuget-Client-SDK-Pakete geschrieben.</span><span class="sxs-lookup"><span data-stu-id="2bf96-144">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="2bf96-145">Neuere Versionen der Pakete sind möglicherweise nicht mit den Informationen in den Blogbeiträgen kompatibel.</span><span class="sxs-lookup"><span data-stu-id="2bf96-145">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="2bf96-146">Martin björkström hat einen nachfolgenden Blogbeitrag zur Blog Reihe von Dave Glick durchgeführt, in dem er eine andere Vorgehensweise zum Installieren von nuget-Paketen mit dem nuget-Client-SDK einführt:</span><span class="sxs-lookup"><span data-stu-id="2bf96-146">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="2bf96-147">Neubesuchen der nuget V3-Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="2bf96-147">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
