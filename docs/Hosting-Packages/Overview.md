---
title: "Überblick über das Hosten eigener NuGet-Feeds | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 97577ddd-c294-432d-81a7-b4aebe88bd1c
description: "Ein Überblick über die Möglichkeiten, eigene Feeds oder Kataloge für NuGet-Pakete lokal oder remote zu hosten"
keywords: "NuGet-Feed, NuGet-Katalog, Feeds für benutzerdefinierte Pakete, NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: c3c6b17cdeb4fe959adbc56bdc6ace73202a98fc
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="hosting-your-own-nuget-feeds"></a><span data-ttu-id="8c9e1-104">Hosten eigener NuGet-Feeds</span><span class="sxs-lookup"><span data-stu-id="8c9e1-104">Hosting your own NuGet feeds</span></span>

<span data-ttu-id="8c9e1-105">Möglicherweise möchten Sie Ihre Pakete nur für einen eingeschränkten Personenkreis freigeben, z.B. Ihre Organisation oder Arbeitsgruppe, anstatt diese öffentlich verfügbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="8c9e1-105">Instead of making packages publicly available, you might want to release packages to only a limited audience, such as your organization or workgroup.</span></span> <span data-ttu-id="8c9e1-106">Darüber hinaus möchten einige Unternehmen ggf. vorgeben, welche Bibliotheken von Drittanbietern ihre Entwickler verwenden. Daher weisen diese die Entwickler an, auf eine spezielle Paketquelle zurückzugreifen, anstatt auf nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8c9e1-106">In addition, some companies may want to restrict which third-party libraries their developers may use, and thus direct those developers to draw from a limited package source rather than nuget.org.</span></span>

<span data-ttu-id="8c9e1-107">Zu diesen Zwecken unterstützt NuGet das Einrichten privater Paketquellen auf folgende Arten:</span><span class="sxs-lookup"><span data-stu-id="8c9e1-107">For all such purposes, NuGet supports setting up private package sources in the following ways:</span></span>

- <span data-ttu-id="8c9e1-108">Lokaler Feed: Pakete werden einfach an einem passenden Netzwerkfreigabeort abgelegt. Idealerweise wurde mithilfe von `nuget init` und `nuget add` eine hierarchische Ordnerstruktur angelegt (NuGet 3.3 und höher).</span><span class="sxs-lookup"><span data-stu-id="8c9e1-108">Local feed: Packages are simply placed on a suitable network file share, ideally using `nuget init` and `nuget add` to create a hierarchical folder structure (NuGet 3.3+).</span></span> <span data-ttu-id="8c9e1-109">Weitere Einzelheiten finden Sie unter [Lokale Feeds](../hosting-packages/local-feeds.md).</span><span class="sxs-lookup"><span data-stu-id="8c9e1-109">For details, see [Local Feeds](../hosting-packages/local-feeds.md).</span></span>
- <span data-ttu-id="8c9e1-110">NuGet.Server: Pakete werden über einen lokalen HTTP-Server verfügbar gemacht.</span><span class="sxs-lookup"><span data-stu-id="8c9e1-110">NuGet.Server: Packages are made available through a local HTTP server.</span></span> <span data-ttu-id="8c9e1-111">Weitere Einzelheiten finden Sie unter [NuGet.Server](../hosting-packages/NuGet-Server.md).</span><span class="sxs-lookup"><span data-stu-id="8c9e1-111">For details, see [NuGet.Server](../hosting-packages/NuGet-Server.md).</span></span>
- <span data-ttu-id="8c9e1-112">NuGet-Katalog: Pakete werden mithilfe von [NuGet Gallery Project (Projekt „NuGet-Katalog“)](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com) auf einem Internet-Server gehostet.</span><span class="sxs-lookup"><span data-stu-id="8c9e1-112">NuGet Gallery: Packages are hosted on an Internet server using the [NuGet Gallery Project](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span></span> <span data-ttu-id="8c9e1-113">Der NuGet-Katalog bietet Benutzerverwaltung und diverse Funktionen, z.B. eine umfangreiche Webbenutzeroberfläche, die es ermöglicht, direkt im Browser nach Paketen zu suchen und sich diese näher anzusehen, ähnlich wie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8c9e1-113">NuGet Gallery provides user management and features such as an extensive web UI that allows searching and exploring packages from within the browser, similar to nuget.org.</span></span>

<span data-ttu-id="8c9e1-114">Es gibt zudem verschiedene andere NuGet-Produkte zum Hosten, die remote private Feeds unterstützen, z.B:</span><span class="sxs-lookup"><span data-stu-id="8c9e1-114">There are also several other NuGet hosting products that support remote private feeds, including the following:</span></span>

- <span data-ttu-id="8c9e1-115">[Visual Studio Team Services-Paketverwaltung](https://www.visualstudio.com/docs/package/nuget/publish) (auch bei Team Foundation Server 2017 und höher verfügbar)</span><span class="sxs-lookup"><span data-stu-id="8c9e1-115">[Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), which is also available on Team Foundation Server 2017 and later.</span></span>
- [<span data-ttu-id="8c9e1-116">MyGet</span><span class="sxs-lookup"><span data-stu-id="8c9e1-116">MyGet</span></span>](http://myget.org)
- <span data-ttu-id="8c9e1-117">[ProGet](http://inedo.com/proget) von Inedo</span><span class="sxs-lookup"><span data-stu-id="8c9e1-117">[ProGet](http://inedo.com/proget) from Inedo</span></span>
- <span data-ttu-id="8c9e1-118">[NuGet Server](http://nugetserver.net/), ein Communityprojekt von Inedo</span><span class="sxs-lookup"><span data-stu-id="8c9e1-118">[NuGet Server](http://nugetserver.net/), a community project from Inedo</span></span>
- <span data-ttu-id="8c9e1-119">[NuGet Server (Open Source)](http://nuget-server.net), eine Open-Source-Implementierung, die NuGet Server von Inedo ähnelt</span><span class="sxs-lookup"><span data-stu-id="8c9e1-119">[NuGet Server (Open Source)](http://nuget-server.net), an open-source implementation similar to Inedo's NuGet Server</span></span>
- <span data-ttu-id="8c9e1-120">[Artifactory](https://www.jfrog.com/artifactory/) von JFrog</span><span class="sxs-lookup"><span data-stu-id="8c9e1-120">[Artifactory](https://www.jfrog.com/artifactory/) from JFrog.</span></span>
- <span data-ttu-id="8c9e1-121">[Nexus](http://www.sonatype.org/nexus/) von Sonatype</span><span class="sxs-lookup"><span data-stu-id="8c9e1-121">[Nexus](http://www.sonatype.org/nexus/) from Sonatype.</span></span>
- <span data-ttu-id="8c9e1-122">[TeamCity](https://www.jetbrains.com/teamcity/) von JetBrains</span><span class="sxs-lookup"><span data-stu-id="8c9e1-122">[TeamCity](https://www.jetbrains.com/teamcity/) from JetBrains.</span></span>

<span data-ttu-id="8c9e1-123">Unabhängig davon, wie Pakete gehostet werden, können Sie auf diese zugreifen, indem Sie diese der Liste verfügbarer Datenquellen in `NuGet.Config` hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="8c9e1-123">Regardless of how packages are hosted, you access them by adding them to the list of available sources in `NuGet.Config`.</span></span> <span data-ttu-id="8c9e1-124">Dies kann in Visual Studio ausgeführt werden, wie im Absatz zum Thema [Paketquellen](../tools/package-manager-ui.md#package-sources) beschrieben, oder über die Befehlszeile mithilfe von [`nuget sources`](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="8c9e1-124">This can be done in Visual Studio as described in [Package Sources](../tools/package-manager-ui.md#package-sources), or from the command line using [`nuget sources`](../tools/cli-ref-sources.md).</span></span> <span data-ttu-id="8c9e1-125">Bei dem Pfad zu einer Datenquelle kann es sich um einen Pfadnamen für einen lokalen Ordner, um einen Netzwerknamen oder eine URL handeln.</span><span class="sxs-lookup"><span data-stu-id="8c9e1-125">The path to a source can be a local folder pathname, a network name, or a URL.</span></span>
