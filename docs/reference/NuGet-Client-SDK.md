---
title: NuGet-Client-SDK
description: Die API sich entwickelnden und noch nicht dokumentiert, aber Beispiele stehen Dave Glicks-Blog.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 8f96bf289e8121fd25262fb95c2f36dfc89045c5
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911035"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="0cf30-103">NuGet-Client-SDK</span><span class="sxs-lookup"><span data-stu-id="0cf30-103">NuGet Client SDK</span></span>

> [!Note]
> <span data-ttu-id="0cf30-104">Nicht zu verwechseln mit der [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span><span class="sxs-lookup"><span data-stu-id="0cf30-104">Not to be confused with the [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span></span>

<span data-ttu-id="0cf30-105">Die *NuGet-Client-SDK* bezieht sich auf eine Gruppe von Bibliotheken für .NET zentraler Punkt [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), und [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="0cf30-105">The *NuGet Client SDK* refers to a group of .NET libraries centered around [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="0cf30-106">Diese Pakete ersetzt die frühere [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="0cf30-106">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

<span data-ttu-id="0cf30-107">Wir arbeiten, haben Sie eine stabile Oberfläche, die wir in Kürze dokumentiert werden können.</span><span class="sxs-lookup"><span data-stu-id="0cf30-107">We are working on having a stable surface area that we can document soon.</span></span>

## <a name="source-code"></a><span data-ttu-id="0cf30-108">Quellcode</span><span class="sxs-lookup"><span data-stu-id="0cf30-108">Source code</span></span>

<span data-ttu-id="0cf30-109">Der Quellcode ist im Projekt auf GitHub veröffentlichten [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span><span class="sxs-lookup"><span data-stu-id="0cf30-109">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="0cf30-110">Drittanbieter-Dokumentation</span><span class="sxs-lookup"><span data-stu-id="0cf30-110">Third-party documentation</span></span>

<span data-ttu-id="0cf30-111">Sie finden Beispiele und Dokumentation für einige der API in den folgenden Blog von Dave Glick, 2016 veröffentlicht:</span><span class="sxs-lookup"><span data-stu-id="0cf30-111">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="0cf30-112">Untersuchen die NuGet-v3-Bibliotheken, Teil 1: Einführung und Konzepte</span><span class="sxs-lookup"><span data-stu-id="0cf30-112">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="0cf30-113">Untersuchen die NuGet-v3-Bibliotheken, Teil 2: Pakete werden gesucht</span><span class="sxs-lookup"><span data-stu-id="0cf30-113">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="0cf30-114">Untersuchen die NuGet-v3-Bibliotheken, Teil 3: Installieren von Paketen</span><span class="sxs-lookup"><span data-stu-id="0cf30-114">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="0cf30-115">Diese Blogbeiträge wurde kurz nach der **3.4.3** Version des NuGet Client-SDK-Pakete wurden veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="0cf30-115">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="0cf30-116">Neuere Versionen der Pakete möglicherweise nicht kompatibel mit den Informationen in den Blogbeiträgen.</span><span class="sxs-lookup"><span data-stu-id="0cf30-116">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="0cf30-117">Martin Björkström hat einen Blogbeitrag zur nachverfolgung Dave Glicks Blog-Reihe, in denen führt er eines anderen Ansatzes zur Verwendung des NuGet-Client-SDK für die Installation von NuGet-Pakete:</span><span class="sxs-lookup"><span data-stu-id="0cf30-117">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="0cf30-118">Öffnen Sie erneut die NuGet-v3-Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="0cf30-118">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
