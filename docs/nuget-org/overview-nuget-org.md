---
title: Übersicht über NuGet.org
description: Übersicht über NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 2dac6ebd6367f3ed1a5ef9e81d843867a4a22f62
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901875"
---
# <a name="overview-of-nugetorg"></a><span data-ttu-id="40317-103">Übersicht über NuGet.org</span><span class="sxs-lookup"><span data-stu-id="40317-103">Overview of NuGet.org</span></span>

<span data-ttu-id="40317-104">NuGet.org ist ein öffentlicher Host für NuGet-Pakete, der täglich von Millionen von .NET- und .NET Core-Entwicklern genutzt wird.</span><span class="sxs-lookup"><span data-stu-id="40317-104">NuGet.org is a public host of NuGet packages that are employed by millions of .NET and .NET Core developers every day.</span></span>

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a><span data-ttu-id="40317-105">Rolle von NuGet.org im NuGet-Ökosystem</span><span class="sxs-lookup"><span data-stu-id="40317-105">Role of NuGet.org in the NuGet ecosystem</span></span>

<span data-ttu-id="40317-106">In seiner Rolle als öffentlicher Host verwaltet NuGet.org selbst das zentrale Repository mit über 100.000 eindeutigen Paketen auf [nuget.org](https://www.nuget.org). NuGet.org ist nicht der einzige mögliche Host für Pakete.</span><span class="sxs-lookup"><span data-stu-id="40317-106">In its role as a public host, NuGet.org itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). NuGet.org is not the only possible host for packages.</span></span> <span data-ttu-id="40317-107">Mit der NuGet-Technologie können Sie auch Pakete privat in der Cloud (z.B. in Azure DevOps), in einem privaten Netzwerk oder sogar nur auf Ihrem lokalen Dateisystem hosten.</span><span class="sxs-lookup"><span data-stu-id="40317-107">The NuGet technology also enables you to host packages privately in the cloud (such as on Azure DevOps), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="40317-108">Wenn Sie an einem anderen Host oder einer anderen Hostingoption interessiert sind, finden Sie weitere Informationen unter [Hosten eigener NuGet-Feeds](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="40317-108">If you are interested in a different host or hosting option, see [Hosting your own NuGet feeds](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="40317-109">NuGet.org dient, wie jeder andere Host für NuGet-Pakete, als Verbindungspunkt zwischen *Paketerstellern* und *Paketconsumern*.</span><span class="sxs-lookup"><span data-stu-id="40317-109">NuGet.org, like any host for NuGet packages, serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="40317-110">Paketersteller erstellen nützliche NuGet-Pakete und veröffentlichen sie.</span><span class="sxs-lookup"><span data-stu-id="40317-110">Creators build useful NuGet packages and publish them.</span></span> <span data-ttu-id="40317-111">Benutzer suchen dann nach nützlichen und kompatiblen Paketen auf zugänglichen Hosts, laden diese Pakete herunter und schließen sie in Ihre Projekte ein.</span><span class="sxs-lookup"><span data-stu-id="40317-111">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="40317-112">Nach der Installation in einem Projekt sind die Paket-APIs für den restlichen Projektcode verfügbar.</span><span class="sxs-lookup"><span data-stu-id="40317-112">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![Beziehung zwischen Paketerstellern, Pakethosts und Paketbenutzer](media/nuget-roles.png)

## <a name="accounts"></a><span data-ttu-id="40317-114">Konten</span><span class="sxs-lookup"><span data-stu-id="40317-114">Accounts</span></span>

<span data-ttu-id="40317-115">Um Pakete auf NuGet.org zu veröffentlichen, erstellen Sie zunächst ein [individuelles Benutzerkonto](individual-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="40317-115">To publish packages on NuGet.org, you first create an [individual (user) account](individual-accounts.md).</span></span> <span data-ttu-id="40317-116">Dieses Konto ist Ihre Identität auf NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="40317-116">This becomes your identity on NuGet.org.</span></span>

<span data-ttu-id="40317-117">NuGet.org ermöglicht außerdem das Erstellen von [Organisationskonten](organizations-on-nuget-org.md).</span><span class="sxs-lookup"><span data-stu-id="40317-117">NuGet.org also allows you to create an [organization account](organizations-on-nuget-org.md).</span></span> <span data-ttu-id="40317-118">Ein Organisationskonto umfasst mehrere Einzelkonten als Mitglieder.</span><span class="sxs-lookup"><span data-stu-id="40317-118">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="40317-119">Diese Mitglieder können einen Paketsatz verwalten und hierbei eine einzige Identität für den Besitz nutzen.</span><span class="sxs-lookup"><span data-stu-id="40317-119">Members can manage a set of packages while maintaining a single identity for ownership.</span></span> <span data-ttu-id="40317-120">Durch Ihr individuelles Konto können Sie Mitglied in einer beliebigen Anzahl von Organisationen sein.</span><span class="sxs-lookup"><span data-stu-id="40317-120">Through your individual account, you can be a member of any number of organizations.</span></span>

<span data-ttu-id="40317-121">Ein Paket kann einem Organisationskonto ebenso angehören wie einem individuellen Konto.</span><span class="sxs-lookup"><span data-stu-id="40317-121">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="40317-122">Paketconsumer erkennen keinen Unterschied zwischen einem individuellen Konto oder dem Organisationskonto: beide werden als Paket `owners` angezeigt.</span><span class="sxs-lookup"><span data-stu-id="40317-122">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="api-keys"></a><span data-ttu-id="40317-123">API-Schlüssel</span><span class="sxs-lookup"><span data-stu-id="40317-123">API keys</span></span>

<span data-ttu-id="40317-124">Sobald Sie über ein NuGet-Paket (*.nupkg*-Datei) für die Veröffentlichung verfügen, können Sie es zusammen mit einem von NuGet.org abgerufenen [API-Schlüssel](scoped-api-keys.md) entweder über die nuget.exe-CLI oder die dotnet.exe-CLI veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="40317-124">Once you have a NuGet package (*.nupkg* file) to publish, you publish it to NuGet.org using either the nuget.exe CLI or the dotnet.exe CLI, along with an [API key](scoped-api-keys.md) acquired from NuGet.org.</span></span>

<span data-ttu-id="40317-125">Wenn Sie ein [Paket veröffentlichen](../create-packages/creating-a-package.md), schließen Sie den API-Schlüsselwert in den CLI-Befehl ein.</span><span class="sxs-lookup"><span data-stu-id="40317-125">When you [publish a package](../create-packages/creating-a-package.md), you include the API key value in the CLI command.</span></span>

## <a name="id-prefixes"></a><span data-ttu-id="40317-126">ID-Präfixe</span><span class="sxs-lookup"><span data-stu-id="40317-126">ID prefixes</span></span>

<span data-ttu-id="40317-127">Wenn Sie Pakete veröffentlichen, können Sie Ihre Identität durch das [Reservieren von ID-Präfixen](id-prefix-reservation.md) schützen.</span><span class="sxs-lookup"><span data-stu-id="40317-127">When you publish packages, you can reserve and protect your identity by [reserving ID prefixes](id-prefix-reservation.md).</span></span> <span data-ttu-id="40317-128">Paketconsumer erhalten beim Installieren eines Pakets zusätzliche Informationen und werden darauf hingewiesen, dass das genutzte Paket hinsichtlich identifizierender Eigenschaften eindeutig ist.</span><span class="sxs-lookup"><span data-stu-id="40317-128">When installing a package, package consumers are provided with additional information indicating that the package they are consuming is not deceptive in its identifying properties.</span></span>

## <a name="api-endpoint-for-nugetorg"></a><span data-ttu-id="40317-129">API-Endpunkt für NuGet.org</span><span class="sxs-lookup"><span data-stu-id="40317-129">API endpoint for NuGet.org</span></span>

<span data-ttu-id="40317-130">Um NuGet.org als Paketrepository mit NuGet-Clients verwenden zu können, müssen Sie den folgenden V3-API-Endpunkt verwenden:</span><span class="sxs-lookup"><span data-stu-id="40317-130">To use NuGet.org as a package repository with NuGet clients, you should use the following V3 API endpoint:</span></span> 

`https://api.nuget.org/v3/index.json`

<span data-ttu-id="40317-131">Ältere Clients können weiterhin das V2-Protokoll verwenden, um NuGet.org zu erreichen. Beachten Sie jedoch, dass NuGet-Clients ab Version 3.0 oder höher bei Verwendung des V2-Protokolls über langsamere und weniger zuverlässige Dienste verfügen werden:</span><span class="sxs-lookup"><span data-stu-id="40317-131">Older clients can still use the V2 protocol to reach NuGet.org. However, please note, NuGet clients 3.0 or later will have slower and less reliable service using the V2 protocol:</span></span>

<span data-ttu-id="40317-132">`https://www.nuget.org/api/v2` (**Das V2-Protokoll ist veraltet.** )</span><span class="sxs-lookup"><span data-stu-id="40317-132">`https://www.nuget.org/api/v2` (**The V2 protocol is deprecated!**)</span></span>
