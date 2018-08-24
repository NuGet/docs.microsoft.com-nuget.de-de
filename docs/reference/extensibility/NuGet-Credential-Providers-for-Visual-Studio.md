---
title: NuGet-Anmeldeinformationsanbieter für Visual Studio
description: NuGet-Anmeldeinformationsanbieter, mit Feeds durch Implementieren der IVsCredentialProvider-Schnittstelle in Visual Studio-Erweiterung authentifizieren.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e8d8ae22300b55b93badb65864163d959105dca2
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/23/2018
ms.locfileid: "42793902"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="d34d6-103">Authentifizieren von Datenfeeds in Visual Studio mit NuGet-Anmeldeinformationsanbieter</span><span class="sxs-lookup"><span data-stu-id="d34d6-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="d34d6-104">Die Visual Studio-Erweiterung für NuGet 3.6 unterstützt Anmeldeinformationsanbieter, bei die NuGet mit authentifizierte Feeds arbeiten können.</span><span class="sxs-lookup"><span data-stu-id="d34d6-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="d34d6-105">Nachdem Sie einen NuGet-Anmeldeinformationsanbieter für Visual Studio installieren, NuGet Visual Studio-Erweiterung automatisch abrufen und aktualisieren die Anmeldeinformationen für authentifizierte Feeds nach Bedarf.</span><span class="sxs-lookup"><span data-stu-id="d34d6-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="d34d6-106">Eine beispielimplementierung finden Sie im [VsCredentialProvider Beispiel](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="d34d6-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="d34d6-107">4.8 ab NuGet in Visual Studio unterstützt die neue plattformübergreifende Authentifizierung Plug-Ins auch, aber sie sind nicht die empfohlene Vorgehensweise zur Verbesserung der Leistung.</span><span class="sxs-lookup"><span data-stu-id="d34d6-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="d34d6-108">NuGet-Anmeldeinformationsanbieter für Visual Studio muss als reguläre Visual Studio-Erweiterung installiert werden und müssen [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) oder höher.</span><span class="sxs-lookup"><span data-stu-id="d34d6-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="d34d6-109">NuGet-Anmeldeinformationsanbieter für Visual Studio funktionieren nur in Visual Studio (nicht im Dotnet Restore "oder" nuget.exe ").</span><span class="sxs-lookup"><span data-stu-id="d34d6-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="d34d6-110">Der Anmeldeinformationsanbieter bei nuget.exe, finden Sie unter [nuget.exe-Anmeldeinformationsanbieter](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="d34d6-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="d34d6-111">Anmeldeinformationen-Anbieter in Dotnet und Msbuild finden Sie unter [NuGet cross-Platform-Plug-Ins](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="d34d6-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="d34d6-112">Verfügbare NuGet-Anmeldeinformationsanbieter für Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d34d6-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="d34d6-113">Es gibt einen Anmeldeinformationsanbieter erstellt, in der Visual Studio-NuGet-Erweiterung zur Unterstützung von Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="d34d6-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="d34d6-114">Die NuGet-Erweiterung für Visual Studio verwendet eine interne `VsCredentialProviderImporter` das für Anmeldeinformationsanbieter-Plug-Ins werden überprüft.</span><span class="sxs-lookup"><span data-stu-id="d34d6-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="d34d6-115">Diese Anmeldeinformationsanbieter--Plug-in müssen als ein MEF-Export vom Typ erkannt werden, `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="d34d6-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="d34d6-116">-Plug-in-Anmeldeinformationsanbieter verfügbar sind:</span><span class="sxs-lookup"><span data-stu-id="d34d6-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="d34d6-117">MyGet-Anmeldeinformationsanbieter für Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d34d6-117">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="d34d6-118">Erstellen einen NuGet-Anmeldeinformationsanbieter für Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d34d6-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="d34d6-119">Die Visual Studio-Erweiterung für NuGet 3.6 implementiert eine interne CredentialService, die zum Abrufen der Anmeldeinformationen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="d34d6-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="d34d6-120">Die CredentialService hat es sich um eine Liste der integrierten und Plug-in-Anmeldeinformationsanbieter.</span><span class="sxs-lookup"><span data-stu-id="d34d6-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="d34d6-121">Jeder Anbieter wird nacheinander ausprobiert, bis Anmeldeinformationen abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="d34d6-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="d34d6-122">Beim Abrufen von Anmeldeinformationen versucht der Anmeldeinformationsdienst Anmeldeinformationsanbieter in der folgenden Reihenfolge und hört auf, sobald Anmeldeinformationen abgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="d34d6-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="d34d6-123">Anmeldeinformationen werden von NuGet-Konfigurationsdateien abgerufen werden (unter Verwendung der integrierten `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="d34d6-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="d34d6-124">Wenn die Paketquelle in Visual Studio Team Services ist die `VisualStudioAccountProvider` verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="d34d6-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="d34d6-125">Alle anderen-Plug-in Visual Studio Anmeldeinformationsanbieter werden nacheinander ausprobiert.</span><span class="sxs-lookup"><span data-stu-id="d34d6-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="d34d6-126">Versuchen Sie es, alle NuGet cross-Platform-Anmeldeinformationsanbieter sequenziell zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="d34d6-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="d34d6-127">Wenn noch keine Anmeldeinformationen abgerufen wurden, wird der Benutzer zur Eingabe von Anmeldeinformationen mithilfe einer standard Standardauthentifizierung-Dialogfelds aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="d34d6-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="d34d6-128">Implementieren von IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="d34d6-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="d34d6-129">Um ein NuGet-Anmeldeinformationsanbieter für Visual Studio zu erstellen, erstellen Sie eine Visual Studio-Erweiterung, die einen öffentlichen MEF-Export Implementierung verfügbar macht die `IVsCredentialProvider` geben, und die unten beschriebenen Prinzipien folgt.</span><span class="sxs-lookup"><span data-stu-id="d34d6-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="d34d6-130">Eine beispielimplementierung finden Sie im [VsCredentialProvider Beispiel](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="d34d6-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="d34d6-131">Jedes NuGet-Anmeldeinformationsanbieter für Visual Studio muss:</span><span class="sxs-lookup"><span data-stu-id="d34d6-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="d34d6-132">Bestimmen Sie, ob sie Anmeldeinformationen für den Ziel-URI angeben kann, vor dem Abrufen von Anmeldeinformationen zu initiieren.</span><span class="sxs-lookup"><span data-stu-id="d34d6-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="d34d6-133">Wenn der Anbieter kann Anmeldeinformationen für die entsprechenden Quelle nicht bereitstellen, sollte zurückgegeben `null`.</span><span class="sxs-lookup"><span data-stu-id="d34d6-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="d34d6-134">Wenn der Anbieter Anforderungen für den Ziel-URI behandelt, aber Sie können keine Anmeldeinformationen bereitstellen, sollte eine Ausnahme ausgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="d34d6-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="d34d6-135">Implementieren Sie einen benutzerdefinierten NuGet-Anmeldeinformationsanbieter für Visual Studio muss die `IVsCredentialProvider` -Schnittstelle in der [NuGet.VisualStudio Paket](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="d34d6-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="d34d6-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="d34d6-136">GetCredentialAsync</span></span>

| <span data-ttu-id="d34d6-137">Eingabeparameter</span><span class="sxs-lookup"><span data-stu-id="d34d6-137">Input Parameter</span></span> |<span data-ttu-id="d34d6-138">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d34d6-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="d34d6-139">URI-uri</span><span class="sxs-lookup"><span data-stu-id="d34d6-139">Uri uri</span></span> | <span data-ttu-id="d34d6-140">Die Paket-Quell-Uri für den Anmeldeinformationen angefordert werden.</span><span class="sxs-lookup"><span data-stu-id="d34d6-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="d34d6-141">IWebProxy-proxy</span><span class="sxs-lookup"><span data-stu-id="d34d6-141">IWebProxy proxy</span></span> | <span data-ttu-id="d34d6-142">Der Webproxy verwenden, bei der Kommunikation über das Netzwerk.</span><span class="sxs-lookup"><span data-stu-id="d34d6-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="d34d6-143">NULL, wenn es keine Proxyauthentifizierung konfiguriert gibt.</span><span class="sxs-lookup"><span data-stu-id="d34d6-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="d34d6-144">"bool" isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="d34d6-144">bool isProxyRequest</span></span> | <span data-ttu-id="d34d6-145">"True", wenn die Anforderung beim Anmeldeinformationen für die Authentifizierung abrufen ist.</span><span class="sxs-lookup"><span data-stu-id="d34d6-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="d34d6-146">Wenn die Implementierung für den Erwerb von Proxy-Anmeldeinformationen ungültig ist, sollte Null zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="d34d6-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="d34d6-147">"bool" isRetry</span><span class="sxs-lookup"><span data-stu-id="d34d6-147">bool isRetry</span></span> | <span data-ttu-id="d34d6-148">True, wenn die Anmeldeinformationen wurden für diesen Uri bereits zuvor angefordert, aber die angegebenen Anmeldeinformationen wurde nicht autorisierten Zugriff zugelassen.</span><span class="sxs-lookup"><span data-stu-id="d34d6-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="d34d6-149">nicht interaktive "bool"</span><span class="sxs-lookup"><span data-stu-id="d34d6-149">bool nonInteractive</span></span> | <span data-ttu-id="d34d6-150">Bei "true", muss der Anmeldeinformationsanbieter werden alle benutzeraufforderungen unterdrückt und verwenden Sie stattdessen die Standardwerte.</span><span class="sxs-lookup"><span data-stu-id="d34d6-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="d34d6-151">CancellationToken-cancellationToken</span><span class="sxs-lookup"><span data-stu-id="d34d6-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="d34d6-152">Dieses Abbruchtoken sollte überprüft werden, um festzustellen, ob der Vorgang Anfordern von Anmeldeinformationen wurde abgebrochen.</span><span class="sxs-lookup"><span data-stu-id="d34d6-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="d34d6-153">**Rückgabewert**: eine objektimplementierung Anmeldeinformationen der [ `System.Net.ICredentials` Schnittstelle](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="d34d6-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
