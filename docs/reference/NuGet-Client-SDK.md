---
title: NuGet-Client SDK
description: Die API wird weiterentwickelt und noch nicht dokumentiert, aber Beispiele finden Sie im Blog von Dave Glick.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 6417c971dc13cf9ed05dcec4e4156af94c0ea058
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387386"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="80cef-103">NuGet-Client SDK</span><span class="sxs-lookup"><span data-stu-id="80cef-103">NuGet Client SDK</span></span>

<span data-ttu-id="80cef-104">Das *NuGet Client SDK* bezieht sich auf eine Gruppe von NuGet-Paketen:</span><span class="sxs-lookup"><span data-stu-id="80cef-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="80cef-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) – Wird für die Interaktion mit HTTP- und dateibasierten NuGet-Feeds verwendet.</span><span class="sxs-lookup"><span data-stu-id="80cef-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="80cef-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) – Wird für die Interaktion mit NuGet-Paketen verwendet.</span><span class="sxs-lookup"><span data-stu-id="80cef-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="80cef-107">`NuGet.Protocol` hängt von diesem Paket ab.</span><span class="sxs-lookup"><span data-stu-id="80cef-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="80cef-108">Den Quellcode für diese Pakete finden Sie im GitHub-Repository [NuGet/NuGet.Client.](https://github.com/NuGet/NuGet.Client)</span><span class="sxs-lookup"><span data-stu-id="80cef-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>
<span data-ttu-id="80cef-109">Den Quellcode für diese Beispiele finden Sie im Projekt [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) auf GitHub.</span><span class="sxs-lookup"><span data-stu-id="80cef-109">You can find the source code for these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) project on GitHub.</span></span>

> [!Note]
> <span data-ttu-id="80cef-110">Die Dokumentation zum NuGet-Serverprotokoll finden Sie in der [NuGet-Server-API.](~/api/overview.md)</span><span class="sxs-lookup"><span data-stu-id="80cef-110">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="nugetprotocol"></a><span data-ttu-id="80cef-111">NuGet.Protocol</span><span class="sxs-lookup"><span data-stu-id="80cef-111">NuGet.Protocol</span></span>

<span data-ttu-id="80cef-112">Installieren Sie das `NuGet.Protocol` Paket für die Interaktion mit HTTP- und ordnerbasierten NuGet-Paketfeeds:</span><span class="sxs-lookup"><span data-stu-id="80cef-112">Install the `NuGet.Protocol` package to interact with HTTP and folder-based NuGet package feeds:</span></span>

```ps1
dotnet add package NuGet.Protocol
```

> [!Tip]
> <span data-ttu-id="80cef-113">`Repository.Factory` wird im `NuGet.Protocol.Core.Types` -Namespace definiert, und die `GetCoreV3` -Methode ist eine erweiterungsmethode, die im -Namespace definiert `NuGet.Protocol` ist.</span><span class="sxs-lookup"><span data-stu-id="80cef-113">`Repository.Factory` is defined in the `NuGet.Protocol.Core.Types` namespace, and the `GetCoreV3` method is an extension method defined in the `NuGet.Protocol` namespace.</span></span> <span data-ttu-id="80cef-114">Daher müssen Sie `using` -Anweisungen für beide Namespaces hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="80cef-114">Therefore, you will need to add `using` statements for both namespaces.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="80cef-115">Auflisten von Paketversionen</span><span class="sxs-lookup"><span data-stu-id="80cef-115">List package versions</span></span>

<span data-ttu-id="80cef-116">Suchen Sie alle Versionen von Newtonsoft.Jsmithilfe der [NuGet V3-Paketinhalts-API:](../api/package-base-address-resource.md#enumerate-package-versions)</span><span class="sxs-lookup"><span data-stu-id="80cef-116">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="80cef-117">Herunterladen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="80cef-117">Download a package</span></span>

<span data-ttu-id="80cef-118">Laden Sie Newtonsoft.Jsunter v12.0.1 mithilfe der [NuGet V3-Paketinhalts-API](../api/package-base-address-resource.md)herunter:</span><span class="sxs-lookup"><span data-stu-id="80cef-118">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="80cef-119">Abrufen von Paketmetadaten</span><span class="sxs-lookup"><span data-stu-id="80cef-119">Get package metadata</span></span>

<span data-ttu-id="80cef-120">Abrufen der Metadaten für das Paket "Newtonsoft.Json" mithilfe der [NuGet V3-Paketmetadaten-API:](../api/registration-base-url-resource.md)</span><span class="sxs-lookup"><span data-stu-id="80cef-120">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="80cef-121">Suchen von Paketen</span><span class="sxs-lookup"><span data-stu-id="80cef-121">Search packages</span></span>

<span data-ttu-id="80cef-122">Suchen Sie mithilfe der [NuGet V3-Such-API nach JSON-Paketen:](../api/search-query-service-resource.md)</span><span class="sxs-lookup"><span data-stu-id="80cef-122">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a><span data-ttu-id="80cef-123">Pushen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="80cef-123">Push a package</span></span>

<span data-ttu-id="80cef-124">Pushen eines Pakets mithilfe der [NuGet V3-PUSH- und DELETE-API:](../api/package-publish-resource.md)</span><span class="sxs-lookup"><span data-stu-id="80cef-124">Push a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a><span data-ttu-id="80cef-125">Löschen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="80cef-125">Delete a package</span></span>

<span data-ttu-id="80cef-126">Löschen Sie ein Paket mithilfe der [NuGet V3-PUSH- und DELETE-API:](../api/package-publish-resource.md)</span><span class="sxs-lookup"><span data-stu-id="80cef-126">Delete a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

> [!Note]
> <span data-ttu-id="80cef-127">NuGet-Server können eine Paketlöschanforderung als "hard delete", "soft delete" oder "unlist" interpretieren.</span><span class="sxs-lookup"><span data-stu-id="80cef-127">NuGet servers are free to interpret a package delete request as a "hard delete", "soft delete", or "unlist".</span></span>
> <span data-ttu-id="80cef-128">Beispielsweise interpretiert nuget.org die Paketlöschanforderung als "Unlist".</span><span class="sxs-lookup"><span data-stu-id="80cef-128">For example, nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="80cef-129">Weitere Informationen zu dieser Vorgehensweise finden Sie unter Löschen [von Paketen.](../nuget-org/policies/deleting-packages.md)</span><span class="sxs-lookup"><span data-stu-id="80cef-129">For more information about this practice, see the [Deleting Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span>

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a><span data-ttu-id="80cef-130">Arbeiten mit authentifizierten Feeds</span><span class="sxs-lookup"><span data-stu-id="80cef-130">Work with authenticated feeds</span></span>

<span data-ttu-id="80cef-131">Verwenden [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) Sie , um mit authentifizierten Feeds zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="80cef-131">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) to work with authenticated feeds.</span></span>

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a><span data-ttu-id="80cef-132">NuGet.Packaging</span><span class="sxs-lookup"><span data-stu-id="80cef-132">NuGet.Packaging</span></span>

<span data-ttu-id="80cef-133">Installieren Sie das `NuGet.Packaging` Paket für die Interaktion mit - und `.nupkg` `.nuspec` -Dateien aus einem Stream:</span><span class="sxs-lookup"><span data-stu-id="80cef-133">Install the `NuGet.Packaging` package to interact with `.nupkg` and `.nuspec` files from a stream:</span></span>

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a><span data-ttu-id="80cef-134">Erstellen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="80cef-134">Create a package</span></span>

<span data-ttu-id="80cef-135">Erstellen Sie mit ein Paket, legen Sie Metadaten fest, und fügen Sie Abhängigkeiten [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) hinzu.</span><span class="sxs-lookup"><span data-stu-id="80cef-135">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80cef-136">Es wird dringend empfohlen, NuGet-Pakete mit den  offiziellen NuGet-Tools und nicht mit dieser low-level-API zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="80cef-136">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="80cef-137">Es gibt eine Vielzahl von Merkmalen, die für ein wohlgeformte Paket wichtig sind, und die neueste Version der Tools hilft, diese bewährten Methoden zu integrieren.</span><span class="sxs-lookup"><span data-stu-id="80cef-137">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="80cef-138">Weitere Informationen zum Erstellen von NuGet-Paketen finden Sie in der Übersicht über den Workflow zur Paketerstellung und in der Dokumentation zu offiziellen Pakettools (z. B. mithilfe der [dotnet-CLI).](../create-packages/creating-a-package-dotnet-cli.md) [](../create-packages/overview-and-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="80cef-138">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="80cef-139">Lesen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="80cef-139">Read a package</span></span>

<span data-ttu-id="80cef-140">Lesen eines Pakets aus einem Dateistream mithilfe von [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="80cef-140">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="80cef-141">Dokumentation von Drittanbietern</span><span class="sxs-lookup"><span data-stu-id="80cef-141">Third-party documentation</span></span>

<span data-ttu-id="80cef-142">Beispiele und Dokumentation für einige der APIs finden Sie in der folgenden Blogreihe von Dave Glick, veröffentlicht 2016:</span><span class="sxs-lookup"><span data-stu-id="80cef-142">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="80cef-143">Erkunden der NuGet v3-Bibliotheken, Teil 1: Einführung und Konzepte</span><span class="sxs-lookup"><span data-stu-id="80cef-143">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="80cef-144">Erkunden der NuGet v3-Bibliotheken, Teil 2: Suchen nach Paketen</span><span class="sxs-lookup"><span data-stu-id="80cef-144">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="80cef-145">Erkunden der NuGet v3-Bibliotheken, Teil 3: Installieren von Paketen</span><span class="sxs-lookup"><span data-stu-id="80cef-145">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="80cef-146">Diese Blogbeiträge wurden kurz nach der Veröffentlichung der **Version 3.4.3** der NuGet-Client-SDK-Pakete geschrieben.</span><span class="sxs-lookup"><span data-stu-id="80cef-146">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="80cef-147">Neuere Versionen der Pakete sind möglicherweise nicht mit den Informationen in den Blogbeiträgen kompatibel.</span><span class="sxs-lookup"><span data-stu-id="80cef-147">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="80cef-148">Martin Björkzweig hat einen Folgeblogbeitrag zu Dave Glicks Blogreihe geschrieben, in dem er einen anderen Ansatz zur Verwendung des NuGet-Client-SDK zum Installieren von NuGet-Paketen vorstellt:</span><span class="sxs-lookup"><span data-stu-id="80cef-148">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="80cef-149">Erneutes Aufarbeiten der NuGet v3-Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="80cef-149">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
