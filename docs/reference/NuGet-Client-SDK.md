---
title: Nuget-Client-SDK
description: Die API wird weiterentwickelt und noch nicht dokumentiert, aber Beispiele sind im Blog von Dave Glick verfügbar.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 873bde467a39653b818b49173d53bc983e99d1b9
ms.sourcegitcommit: f9645fc5f49c18978e12a292a3f832e162e069d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/25/2019
ms.locfileid: "72924607"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="aa4c6-103">Nuget-Client-SDK</span><span class="sxs-lookup"><span data-stu-id="aa4c6-103">NuGet Client SDK</span></span>

<span data-ttu-id="aa4c6-104">Das *nuget-Client-SDK* bezieht sich auf eine Gruppe von nuget-Paketen, die auf [nuget-Befehle](https://www.nuget.org/packages/NuGet.Commands), [nuget. Packaging](https://www.nuget.org/packages/NuGet.Packaging)und [nuget. Protocol](https://www.nuget.org/packages/NuGet.Protocol)zentriert sind.</span><span class="sxs-lookup"><span data-stu-id="aa4c6-104">The *NuGet Client SDK* refers to a group of NuGet packages centered around [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="aa4c6-105">Diese Pakete ersetzen die frühere [nuget. Core](https://www.nuget.org/packages/NuGet.Core/) -Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="aa4c6-105">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

> [!Note]
>  <span data-ttu-id="aa4c6-106">Dokumentation zum nuget-Server Protokoll finden Sie in der [nuget-Server-API](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="aa4c6-106">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="source-code"></a><span data-ttu-id="aa4c6-107">Quellcode</span><span class="sxs-lookup"><span data-stu-id="aa4c6-107">Source code</span></span>

<span data-ttu-id="aa4c6-108">Der Quellcode wird auf GitHub im Projekt " [nuget/nuget. Client](https://github.com/NuGet/NuGet.Client)" veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="aa4c6-108">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="aa4c6-109">Dokumentation von Drittanbietern</span><span class="sxs-lookup"><span data-stu-id="aa4c6-109">Third-party documentation</span></span>

<span data-ttu-id="aa4c6-110">Beispiele und Dokumentationen für einige der APIs finden Sie in der folgenden Blog Reihe von Dave Glick, veröffentlicht 2016:</span><span class="sxs-lookup"><span data-stu-id="aa4c6-110">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="aa4c6-111">Erkunden der nuget V3-Bibliotheken, Teil 1: Einführung und Konzepte</span><span class="sxs-lookup"><span data-stu-id="aa4c6-111">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="aa4c6-112">Erkunden der nuget V3-Bibliotheken, Teil 2: Suchen nach Paketen</span><span class="sxs-lookup"><span data-stu-id="aa4c6-112">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="aa4c6-113">Erkunden der nuget V3-Bibliotheken, Teil 3: Installieren von Paketen</span><span class="sxs-lookup"><span data-stu-id="aa4c6-113">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="aa4c6-114">Diese Blogbeiträge wurden kurz nach der Veröffentlichung der **3.4.3** -Version der nuget-Client-SDK-Pakete geschrieben.</span><span class="sxs-lookup"><span data-stu-id="aa4c6-114">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="aa4c6-115">Neuere Versionen der Pakete sind möglicherweise nicht mit den Informationen in den Blogbeiträgen kompatibel.</span><span class="sxs-lookup"><span data-stu-id="aa4c6-115">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="aa4c6-116">Martin björkström hat einen nachfolgenden Blogbeitrag zur Blog Reihe von Dave Glick durchgeführt, in dem er einen anderen Ansatz zur Verwendung des nuget-Client-SDK für die Installation von nuget-Paketen einführt:</span><span class="sxs-lookup"><span data-stu-id="aa4c6-116">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="aa4c6-117">Neubesuchen der nuget V3-Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="aa4c6-117">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
