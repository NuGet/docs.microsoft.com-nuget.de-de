---
title: Nutzen von Paketen aus authentifizierten Feeds
description: Nutzen von Paketen aus authentifizierten Feeds in allen NuGet-Clientszenarios
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231740"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="af4ec-103">Nutzen von Paketen aus authentifizierten Feeds</span><span class="sxs-lookup"><span data-stu-id="af4ec-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="af4ec-104">Zusätzlich zum [öffentlichen Feed](https://api.nuget.org/v3/index.json) von nuget.org können NuGet-Clients mit Datei-Feeds und privaten http-Feeds interagieren.</span><span class="sxs-lookup"><span data-stu-id="af4ec-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="af4ec-105">Für das Authentifizieren mit privaten http-Feeds sind zwei Vorgehensweisen möglich:</span><span class="sxs-lookup"><span data-stu-id="af4ec-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="af4ec-106">Hinzufügen von Anmeldeinformationen in der Datei [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials),</span><span class="sxs-lookup"><span data-stu-id="af4ec-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="af4ec-107">Authentifizieren mithilfe eines der zahlreichen Erweiterbarkeitsmodelle, je nach verwendetem Client.</span><span class="sxs-lookup"><span data-stu-id="af4ec-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="af4ec-108">Erweiterbarkeit der Authentifizierung von NuGet-Clients</span><span class="sxs-lookup"><span data-stu-id="af4ec-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="af4ec-109">Bei den verschiedenen NuGet-Clients ist der Anbieter des privaten Feeds selbst für die Authentifizierung verantwortlich.</span><span class="sxs-lookup"><span data-stu-id="af4ec-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="af4ec-110">Alle NuGet-Clients verfügen über Erweiterbarkeitsmethoden, um dies zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="af4ec-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="af4ec-111">Hierbei handelt es sich entweder um eine Visual Studio-Erweiterung oder um ein Plug-In, die bzw. das mit NuGet kommunizieren kann, um Anmeldeinformationen abzurufen.</span><span class="sxs-lookup"><span data-stu-id="af4ec-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="af4ec-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="af4ec-112">Visual Studio</span></span>

<span data-ttu-id="af4ec-113">In Visual Studio macht NuGet eine Schnittstelle verfügbar, die Feed-Anbieter implementieren und ihren Kunden bereitstellen können.</span><span class="sxs-lookup"><span data-stu-id="af4ec-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="af4ec-114">Weitere Informationen finden Sie in der Dokumentation zum [Erstellen eines Visual Studio-Anmeldeinformationsanbieters](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span><span class="sxs-lookup"><span data-stu-id="af4ec-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="af4ec-115">Verfügbare NuGet-Anmeldeinformationsanbieter für Visual Studio</span><span class="sxs-lookup"><span data-stu-id="af4ec-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="af4ec-116">In Visual Studio ist ein Anmeldeinformationsanbieter integriert, der Azure DevOps unterstützt.</span><span class="sxs-lookup"><span data-stu-id="af4ec-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="af4ec-117">Folgende Plug-In-Anmeldeinformationsanbieter sind verfügbar:</span><span class="sxs-lookup"><span data-stu-id="af4ec-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="af4ec-118">MyGet Credential Provider for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="af4ec-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="af4ec-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="af4ec-119">nuget.exe</span></span>

<span data-ttu-id="af4ec-120">Wenn `nuget.exe` Anmeldeinformationen für die Authentifizierung bei einem Feed benötigt, werden diese Informationen wie folgt gesucht:</span><span class="sxs-lookup"><span data-stu-id="af4ec-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="af4ec-121">Suchen nach Anmeldeinformationen in `NuGet.config`-Dateien.</span><span class="sxs-lookup"><span data-stu-id="af4ec-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="af4ec-122">Verwenden von V2-Plug-In-Anmeldeinformationsanbietern</span><span class="sxs-lookup"><span data-stu-id="af4ec-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="af4ec-123">Verwenden von V1-Plug-In-Anmeldeinformationsanbietern</span><span class="sxs-lookup"><span data-stu-id="af4ec-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="af4ec-124">NuGet fordert dann den Benutzer zur Eingabe von Anmeldeinformationen in der Befehlszeile auf.</span><span class="sxs-lookup"><span data-stu-id="af4ec-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="af4ec-125">nuget.exe- und V2-Anmeldeinformationsanbieter</span><span class="sxs-lookup"><span data-stu-id="af4ec-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="af4ec-126">In Version `4.8` hat NuGet einen neuen Authentifizierungs-Plug-In-Mechanismus definiert, der im Folgenden als V2-Anmeldeinformationsanbieter bezeichnet wird.</span><span class="sxs-lookup"><span data-stu-id="af4ec-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="af4ec-127">Informationen zur Installation und Ermittlung dieser Anbieter finden Sie unter [Plattformübergreifende NuGet-Plug-Ins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="af4ec-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="af4ec-128">nuget.exe- und V1-Anmeldeinformationsanbieter</span><span class="sxs-lookup"><span data-stu-id="af4ec-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="af4ec-129">In Version `3.3` führte NuGet die erste Version der Authentifizierungs-Plug-ins ein.</span><span class="sxs-lookup"><span data-stu-id="af4ec-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="af4ec-130">Informationen zur Installation und Ermittlung dieser Anbieter finden Sie unter [nuget.exe-Anmeldeinformationsanbieter](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery).</span><span class="sxs-lookup"><span data-stu-id="af4ec-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="af4ec-131">Verfügbare Anmeldeinformationsanbieter für nuget.exe</span><span class="sxs-lookup"><span data-stu-id="af4ec-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="af4ec-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) oder [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="af4ec-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="af4ec-133">Seit Visual Studio 2017 Version 15.9 ist der Azure DevOps-Anmeldeinformationsanbieter in Visual Studio gebündelt.</span><span class="sxs-lookup"><span data-stu-id="af4ec-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="af4ec-134">Wenn `nuget.exe` MSBuild aus diesem speziellen Visual Studio-Toolset verwendet, wird das Plug-In automatisch erkannt.</span><span class="sxs-lookup"><span data-stu-id="af4ec-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="af4ec-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="af4ec-135">dotnet.exe</span></span>

<span data-ttu-id="af4ec-136">Wenn `dotnet.exe` Anmeldeinformationen für die Authentifizierung bei einem Feed benötigt, werden diese wie folgt gesucht:</span><span class="sxs-lookup"><span data-stu-id="af4ec-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="af4ec-137">Suchen nach Anmeldeinformationen in `NuGet.config`-Dateien.</span><span class="sxs-lookup"><span data-stu-id="af4ec-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="af4ec-138">Verwenden von V2-Plug-In-Anmeldeinformationsanbietern</span><span class="sxs-lookup"><span data-stu-id="af4ec-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="af4ec-139">`dotnet.exe` ist standardmäßig nicht interaktiv, daher müssen Sie möglicherweise ein `--interactive`-Flag übergeben, damit das Tool für die Authentifizierung gesperrt wird.</span><span class="sxs-lookup"><span data-stu-id="af4ec-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="af4ec-140">dotnet.exe- und V2-Anmeldeinformationsanbieter</span><span class="sxs-lookup"><span data-stu-id="af4ec-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="af4ec-141">In Version `2.2.100` des SDK hat NuGet einen Authentifizierungs-Plug-In-Mechanismus definiert, der bei allen Clients funktioniert.</span><span class="sxs-lookup"><span data-stu-id="af4ec-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="af4ec-142">Informationen zur Installation und Ermittlung dieser Anbieter finden Sie unter [Plattformübergreifende NuGet-Plug-Ins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="af4ec-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="af4ec-143">Verfügbare Anmeldeinformationsanbieter für dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="af4ec-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="af4ec-144">Azure Artifacts Credential Provider</span><span class="sxs-lookup"><span data-stu-id="af4ec-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="af4ec-145">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="af4ec-145">MSBuild.exe</span></span>

<span data-ttu-id="af4ec-146">Wenn `MSBuild.exe` Anmeldeinformationen für die Authentifizierung bei einem Feed benötigt, werden diese wie folgt gesucht:</span><span class="sxs-lookup"><span data-stu-id="af4ec-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="af4ec-147">Suchen nach Anmeldeinformationen in `NuGet.config`-Dateien</span><span class="sxs-lookup"><span data-stu-id="af4ec-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="af4ec-148">Verwenden von V2-Plug-In-Anmeldeinformationsanbietern</span><span class="sxs-lookup"><span data-stu-id="af4ec-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="af4ec-149">`MSBuild.exe` ist standardmäßig nicht interaktiv, sodass Sie möglicherweise die `/p:NuGetInteractive=true`-Eigenschaft festlegen müssen, damit das Tool für die Authentifizierung gesperrt wird.</span><span class="sxs-lookup"><span data-stu-id="af4ec-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="af4ec-150">MSBuild.exe- und V2-Anmeldeinformationsanbieter</span><span class="sxs-lookup"><span data-stu-id="af4ec-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="af4ec-151">In Visual Studio 2019 Update 9 hat NuGet einen Authentifizierungs-Plug-In-Mechanismus definiert, der bei allen Clients funktioniert.</span><span class="sxs-lookup"><span data-stu-id="af4ec-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="af4ec-152">Informationen zur Installation und Ermittlung dieser Anbieter finden Sie unter [Plattformübergreifende NuGet-Plug-Ins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="af4ec-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="af4ec-153">Verfügbare Anmeldeinformationsanbieter für MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="af4ec-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="af4ec-154">Azure Artifacts Credential Provider</span><span class="sxs-lookup"><span data-stu-id="af4ec-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="af4ec-155">Seit Visual Studio 2017 Update 9 ist der Azure DevOps-Anmeldeinformationsanbieter in Visual Studio gebündelt.</span><span class="sxs-lookup"><span data-stu-id="af4ec-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="af4ec-156">Weitere Schritte sind nicht erforderlich.</span><span class="sxs-lookup"><span data-stu-id="af4ec-156">No additional steps are required.</span></span>
