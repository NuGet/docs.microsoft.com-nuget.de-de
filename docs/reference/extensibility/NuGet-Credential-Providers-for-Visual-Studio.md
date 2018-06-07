---
title: NuGet-Anmeldeinformationsanbieter für Visual Studio
description: NuGet-Anmeldeinformationsanbieter authentifizieren, mit Feeds durch Implementieren der IVsCredentialProvider-Schnittstelle in einer Visual Studio-Erweiterung.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: d4dbcab7c4005efcdc7efe96df3a70e666c558cc
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817836"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="1a6e9-103">Authentifizieren von Datenfeeds in Visual Studio mit NuGet-Anmeldeinformationsanbieter</span><span class="sxs-lookup"><span data-stu-id="1a6e9-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="1a6e9-104">Die NuGet-Erweiterung für Visual Studio 3.6 unterstützt Anmeldeinformationsanbieter, die NuGet authentifizierten Feeds portzuweisung zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="1a6e9-105">Nach der Installation eines NuGet-Anmeldeinformationsanbieters für Visual Studio NuGet Visual Studio-Erweiterung automatisch abrufen und aktualisieren die Anmeldeinformationen für authentifizierte Feeds nach Bedarf.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="1a6e9-106">Eine beispielimplementierung finden Sie im [im Beispiel VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="1a6e9-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

> [!Note]
> <span data-ttu-id="1a6e9-107">NuGet-Anmeldeinformationsanbieter für Visual Studio muss installiert sein, als reguläre Visual Studio-Erweiterung, und benötigen [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (zurzeit als Vorschau verfügbar) oder höher.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-107">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (currently in preview) or above.</span></span>
>
> <span data-ttu-id="1a6e9-108">NuGet-Anmeldeinformationsanbieter für Visual Studio funktionieren nur in Visual Studio (nicht im Dotnet wiederherstellen oder nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="1a6e9-108">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="1a6e9-109">Der Anmeldeinformationsanbieter mit nuget.exe, finden Sie unter [nuget.exe Anmeldeinformationsanbieter](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="1a6e9-109">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="1a6e9-110">Verfügbare NuGet Anmeldeinformationsanbieter für Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1a6e9-110">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="1a6e9-111">Es ist ein Anmeldeinformationsanbieter zur Unterstützung von Visual Studio Team Services in Visual Studio NuGet-Erweiterung erstellt.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-111">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="1a6e9-112">Die NuGet-Erweiterung für Visual Studio verwendet eine interne `VsCredentialProviderImporter` die sucht auch nach Anmeldeinformationsanbieter-Plug-in.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-112">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="1a6e9-113">Diese Anmeldeinformationsanbieter-Plug-in müssen als eine MEF-Export vom Typ sichtbar sein `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-113">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="1a6e9-114">-Plug-In für anmeldeinformationenanbieter verfügbar sind:</span><span class="sxs-lookup"><span data-stu-id="1a6e9-114">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="1a6e9-115">MyGet Anmeldeinformationsanbieter für Visual Studio-2017</span><span class="sxs-lookup"><span data-stu-id="1a6e9-115">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="1a6e9-116">Erstellen einen NuGet-Anmeldeinformationsanbieter für Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1a6e9-116">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="1a6e9-117">Die NuGet-Erweiterung für Visual Studio 3.6 implementiert ein internes CredentialService, die verwendet wird, um die Anmeldeinformationen abzurufen.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-117">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="1a6e9-118">Die CredentialService umfasst eine Liste der integrierten und Plug-in-Anmeldeinformationsanbieter.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-118">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="1a6e9-119">Jeder Anbieter wird nacheinander ausprobiert, bis Anmeldeinformationen abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-119">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="1a6e9-120">Während der Übernahme von Anmeldeinformationen versucht der Anmeldeinformationsdienst Anmeldeinformationsanbieter in der folgenden Reihenfolge und hört auf, sobald Anmeldeinformationen abgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="1a6e9-120">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="1a6e9-121">Anmeldeinformationen werden vom NuGet-Konfigurationsdateien abgerufen werden (unter Verwendung der integrierten `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="1a6e9-121">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="1a6e9-122">Wenn die Paketquelle auf Visual Studio Team Services ist die `VisualStudioAccountProvider` verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-122">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="1a6e9-123">Alle anderen Plug-Ins Anmeldeinformationsanbieter werden nacheinander ausprobiert.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-123">All other plug-in credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="1a6e9-124">Wenn noch keine Anmeldeinformationen abgerufen wurden, wird der Benutzer zum Eingeben von Anmeldeinformationen mithilfe einer standard-Standardauthentifizierung-Dialogfeld aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-124">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="1a6e9-125">Implementieren von IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="1a6e9-125">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="1a6e9-126">Um ein NuGet-Anmeldeinformationsanbieter für Visual Studio zu erstellen, erstellen Sie eine Visual Studio-Erweiterung, die einen öffentlichen MEF-Export implementieren verfügbar macht die `IVsCredentialProvider` geben, und mit den unten beschriebenen Regeln entspricht.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-126">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="1a6e9-127">Eine beispielimplementierung finden Sie im [im Beispiel VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="1a6e9-127">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="1a6e9-128">Jede Anmeldeinformationsanbieter NuGet für Visual Studio muss:</span><span class="sxs-lookup"><span data-stu-id="1a6e9-128">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="1a6e9-129">Bestimmen Sie, ob sie Anmeldeinformationen für den Ziel-URI bereitstellen kann, vor dem Initiieren der Übernahme von Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-129">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="1a6e9-130">Wenn der Anbieter kann nicht die Anmeldeinformationen für die targeted Quelle, sollte zurückgegeben `null`.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-130">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="1a6e9-131">Wenn der Anbieter Anforderungen für den Ziel-URI behandelt, jedoch keine Anmeldeinformationen bereitstellen, sollte eine Ausnahme ausgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-131">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="1a6e9-132">Eine benutzerdefinierte NuGet-Anmeldeinformationsanbieter für Visual Studio muss implementieren die `IVsCredentialProvider` -Schnittstelle in der [NuGet.VisualStudio Paket](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="1a6e9-132">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="1a6e9-133">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="1a6e9-133">GetCredentialAsync</span></span>

| <span data-ttu-id="1a6e9-134">Eingabeparameter</span><span class="sxs-lookup"><span data-stu-id="1a6e9-134">Input Parameter</span></span> |<span data-ttu-id="1a6e9-135">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1a6e9-135">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="1a6e9-136">URI-uri</span><span class="sxs-lookup"><span data-stu-id="1a6e9-136">Uri uri</span></span> | <span data-ttu-id="1a6e9-137">Die Paket-Quell-Uri für die Anmeldeinformationen angefordert werden.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-137">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="1a6e9-138">IWebProxy proxy</span><span class="sxs-lookup"><span data-stu-id="1a6e9-138">IWebProxy proxy</span></span> | <span data-ttu-id="1a6e9-139">Der Webproxy verwendet, bei der Kommunikation im Netzwerk.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-139">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="1a6e9-140">NULL, wenn es keine Proxyauthentifizierung konfiguriert ist.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-140">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="1a6e9-141">Bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="1a6e9-141">bool isProxyRequest</span></span> | <span data-ttu-id="1a6e9-142">"True", wenn die Anforderung beim Authentifizierungsanmeldeinformationen abrufen ist.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-142">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="1a6e9-143">Wenn die Implementierung für den Erwerb von Proxy-Anmeldeinformationen ungültig ist, sollte Null zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-143">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="1a6e9-144">Bool isRetry</span><span class="sxs-lookup"><span data-stu-id="1a6e9-144">bool isRetry</span></span> | <span data-ttu-id="1a6e9-145">"True", wenn Anmeldeinformationen für diesen Uri bereits zuvor angefordert wurden, aber die angegebenen Anmeldeinformationen wurde aufgrund nicht autorisierten Zugriff zugelassen.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-145">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="1a6e9-146">nicht interaktive bool</span><span class="sxs-lookup"><span data-stu-id="1a6e9-146">bool nonInteractive</span></span> | <span data-ttu-id="1a6e9-147">Bei "true", muss die Anmeldeinformationsanbieter werden alle benutzeraufforderungen unterdrückt und verwenden Sie stattdessen Default-Werte.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-147">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="1a6e9-148">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="1a6e9-148">CancellationToken cancellationToken</span></span> | <span data-ttu-id="1a6e9-149">Dieses Abbruchtoken sollte überprüft werden, um festzustellen, ob der Vorgang Anfordern von Anmeldeinformationen wurde abgebrochen.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-149">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="1a6e9-150">**Rückgabewert**: Anmeldeinformationen Objekt implementiert die [ `System.Net.ICredentials` Schnittstelle](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="1a6e9-150">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
