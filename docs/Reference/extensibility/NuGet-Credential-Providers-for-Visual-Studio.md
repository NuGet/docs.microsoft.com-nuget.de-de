---
title: "NuGet-Anmeldeinformationsanbieter für Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 9c7f6d16-f437-47c4-82d4-6c996e0b18ec
description: NuGet-Anmeldeinformationsanbieter authentifizieren, mit Feeds durch Implementieren der IVsCredentialProvider-Schnittstelle in einer Visual Studio-Erweiterung.
keywords: NuGet-Anmeldeinformationsanbieter, authentifizieren sich mit dem Feed, authentifizieren sich mit visual Studio-Erweiterung von NuGet-Katalog
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2b2fac23102865a08509acc1cc3d09f0cd375f26
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="a0bc2-104">Authentifizieren von Datenfeeds in Visual Studio mit NuGet-Anmeldeinformationsanbieter</span><span class="sxs-lookup"><span data-stu-id="a0bc2-104">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="a0bc2-105">Die NuGet-Erweiterung für Visual Studio 3.6 unterstützt Anmeldeinformationsanbieter, die NuGet authentifizierten Feeds portzuweisung zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-105">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="a0bc2-106">Nach der Installation eines NuGet-Anmeldeinformationsanbieters für Visual Studio NuGet Visual Studio-Erweiterung automatisch abrufen und aktualisieren die Anmeldeinformationen für authentifizierte Feeds nach Bedarf.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-106">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="a0bc2-107">Eine beispielimplementierung finden Sie im [im Beispiel VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="a0bc2-107">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

> [!Note]
> <span data-ttu-id="a0bc2-108">NuGet-Anmeldeinformationsanbieter für Visual Studio muss installiert sein, als reguläre Visual Studio-Erweiterung, und benötigen [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (zurzeit als Vorschau verfügbar) oder höher.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (currently in preview) or above.</span></span>
>
> <span data-ttu-id="a0bc2-109">NuGet-Anmeldeinformationsanbieter für Visual Studio funktionieren nur in Visual Studio (nicht im Dotnet wiederherstellen oder nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="a0bc2-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="a0bc2-110">Der Anmeldeinformationsanbieter mit nuget.exe, finden Sie unter [nuget.exe Anmeldeinformationsanbieter](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="a0bc2-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="a0bc2-111">Verfügbare NuGet Anmeldeinformationsanbieter für Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a0bc2-111">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="a0bc2-112">Es ist ein Anmeldeinformationsanbieter zur Unterstützung von Visual Studio Team Services in Visual Studio NuGet-Erweiterung erstellt.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-112">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="a0bc2-113">Die NuGet-Erweiterung für Visual Studio verwendet eine interne `VsCredentialProviderImporter` die sucht auch nach Anmeldeinformationsanbieter-Plug-in.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-113">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="a0bc2-114">Diese Anmeldeinformationsanbieter-Plug-in müssen als eine MEF-Export vom Typ sichtbar sein `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-114">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="a0bc2-115">-Plug-In für anmeldeinformationenanbieter verfügbar sind:</span><span class="sxs-lookup"><span data-stu-id="a0bc2-115">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="a0bc2-116">MyGet Anmeldeinformationsanbieter für Visual Studio-2017</span><span class="sxs-lookup"><span data-stu-id="a0bc2-116">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="a0bc2-117">Erstellen einen NuGet-Anmeldeinformationsanbieter für Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a0bc2-117">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="a0bc2-118">Die NuGet-Erweiterung für Visual Studio 3.6 implementiert ein internes CredentialService, die verwendet wird, um die Anmeldeinformationen abzurufen.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-118">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="a0bc2-119">Die CredentialService umfasst eine Liste der integrierten und Plug-in-Anmeldeinformationsanbieter.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-119">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="a0bc2-120">Jeder Anbieter wird nacheinander ausprobiert, bis Anmeldeinformationen abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-120">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="a0bc2-121">Während der Übernahme von Anmeldeinformationen versucht der Anmeldeinformationsdienst Anmeldeinformationsanbieter in der folgenden Reihenfolge und hört auf, sobald Anmeldeinformationen abgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="a0bc2-121">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="a0bc2-122">Anmeldeinformationen werden vom NuGet-Konfigurationsdateien abgerufen werden (unter Verwendung der integrierten `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="a0bc2-122">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="a0bc2-123">Wenn die Paketquelle auf Visual Studio Team Services ist die `VisualStudioAccountProvider` verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-123">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="a0bc2-124">Alle anderen Plug-Ins Anmeldeinformationsanbieter werden nacheinander ausprobiert.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-124">All other plug-in credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="a0bc2-125">Wenn noch keine Anmeldeinformationen abgerufen wurden, wird der Benutzer zum Eingeben von Anmeldeinformationen mithilfe einer standard-Standardauthentifizierung-Dialogfeld aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-125">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="a0bc2-126">Implementieren von IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="a0bc2-126">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="a0bc2-127">Um ein NuGet-Anmeldeinformationsanbieter für Visual Studio zu erstellen, erstellen Sie eine Visual Studio-Erweiterung, die einen öffentlichen MEF-Export implementieren verfügbar macht die `IVsCredentialProvider` geben, und mit den unten beschriebenen Regeln entspricht.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-127">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

```cs
public interface IVsCredentialProvider
{
    Task<ICredentials> GetCredentialsAsync(
        Uri uri,
        IWebProxy proxy,
        bool isProxyRequest,
        bool isRetry,
        bool nonInteractive,
        CancellationToken cancellationToken);
}
```

<span data-ttu-id="a0bc2-128">Eine beispielimplementierung finden Sie im [im Beispiel VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="a0bc2-128">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="a0bc2-129">Jede Anmeldeinformationsanbieter NuGet für Visual Studio muss:</span><span class="sxs-lookup"><span data-stu-id="a0bc2-129">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="a0bc2-130">Bestimmen Sie, ob sie Anmeldeinformationen für den Ziel-URI bereitstellen kann, vor dem Initiieren der Übernahme von Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-130">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="a0bc2-131">Wenn der Anbieter kann nicht die Anmeldeinformationen für die targeted Quelle, sollte zurückgegeben `null`.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-131">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="a0bc2-132">Wenn der Anbieter Anforderungen für den Ziel-URI behandelt, jedoch keine Anmeldeinformationen bereitstellen, sollte eine Ausnahme ausgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-132">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="a0bc2-133">Eine benutzerdefinierte NuGet-Anmeldeinformationsanbieter für Visual Studio muss implementieren die `IVsCredentialProvider` -Schnittstelle in der [NuGet.VisualStudio Paket](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="a0bc2-133">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="a0bc2-134">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="a0bc2-134">GetCredentialAsync</span></span>

| <span data-ttu-id="a0bc2-135">Eingabeparameter</span><span class="sxs-lookup"><span data-stu-id="a0bc2-135">Input Parameter</span></span> |<span data-ttu-id="a0bc2-136">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="a0bc2-136">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="a0bc2-137">URI-uri</span><span class="sxs-lookup"><span data-stu-id="a0bc2-137">Uri uri</span></span> | <span data-ttu-id="a0bc2-138">Die Paket-Quell-Uri für die Anmeldeinformationen angefordert werden.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-138">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="a0bc2-139">IWebProxy proxy</span><span class="sxs-lookup"><span data-stu-id="a0bc2-139">IWebProxy proxy</span></span> | <span data-ttu-id="a0bc2-140">Der Webproxy verwendet, bei der Kommunikation im Netzwerk.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-140">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="a0bc2-141">NULL, wenn es keine Proxyauthentifizierung konfiguriert ist.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-141">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="a0bc2-142">Bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="a0bc2-142">bool isProxyRequest</span></span> | <span data-ttu-id="a0bc2-143">"True", wenn die Anforderung beim Authentifizierungsanmeldeinformationen abrufen ist.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-143">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="a0bc2-144">Wenn die Implementierung für den Erwerb von Proxy-Anmeldeinformationen ungültig ist, sollte Null zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-144">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="a0bc2-145">Bool isRetry</span><span class="sxs-lookup"><span data-stu-id="a0bc2-145">bool isRetry</span></span> | <span data-ttu-id="a0bc2-146">"True", wenn Anmeldeinformationen für diesen Uri bereits zuvor angefordert wurden, aber die angegebenen Anmeldeinformationen wurde aufgrund nicht autorisierten Zugriff zugelassen.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-146">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="a0bc2-147">nicht interaktive bool</span><span class="sxs-lookup"><span data-stu-id="a0bc2-147">bool nonInteractive</span></span> | <span data-ttu-id="a0bc2-148">Bei "true", muss die Anmeldeinformationsanbieter werden alle benutzeraufforderungen unterdrückt und verwenden Sie stattdessen Default-Werte.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-148">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="a0bc2-149">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="a0bc2-149">CancellationToken cancellationToken</span></span> | <span data-ttu-id="a0bc2-150">Dieses Abbruchtoken sollte überprüft werden, um festzustellen, ob der Vorgang Anfordern von Anmeldeinformationen wurde abgebrochen.</span><span class="sxs-lookup"><span data-stu-id="a0bc2-150">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |
  
<span data-ttu-id="a0bc2-151">**Rückgabewert**: Anmeldeinformationen Objekt implementiert die [ `System.Net.ICredentials` Schnittstelle](https://msdn.microsoft.com/library/system.net.icredentials.aspx).</span><span class="sxs-lookup"><span data-stu-id="a0bc2-151">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](https://msdn.microsoft.com/library/system.net.icredentials.aspx).</span></span>
