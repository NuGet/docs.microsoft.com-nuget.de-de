---
title: NuGet-Anmeldeinformationsanbieter für Visual Studio
description: Nuget-Anmelde Informationsanbieter authentifizieren sich mit Feeds, indem die ivscredentialprovider-Schnittstelle in einer Visual Studio-Erweiterung implementiert wird.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 4e781a2462871bceeb1c7f02220320daabdab98a
ms.sourcegitcommit: a0807671386782021acb7588741390e6f07e94e1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/05/2019
ms.locfileid: "70384432"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="5b2b6-103">Authentifizieren von Feeds in Visual Studio mit nuget-Anmelde Informationsanbietern</span><span class="sxs-lookup"><span data-stu-id="5b2b6-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="5b2b6-104">Die nuget Visual Studio-Erweiterung 3.6 und höher unterstützt Anmelde Informationsanbieter, mit denen nuget mit authentifizierten Feeds arbeiten kann.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="5b2b6-105">Nachdem Sie einen nuget-Anmelde Informationsanbieter für Visual Studio installiert haben, werden die Anmelde Informationen für authentifizierte Feeds von der nuget-Erweiterung für Visual Studio nach Bedarf automatisch abgerufen und aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="5b2b6-106">Eine Beispiel Implementierung finden Sie im [vscredentialprovider-Beispiel](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="5b2b6-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="5b2b6-107">Ab 4.8 + nuget in Visual Studio unterstützt auch die neuen plattformübergreifenden Authentifizierungs-Plug-ins, aber Sie sind aus Leistungsgründen nicht empfehlenswert.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="5b2b6-108">Nuget-Anmelde Informationsanbieter für Visual Studio müssen als reguläre Visual Studio-Erweiterung installiert sein und benötigen [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) oder höher.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="5b2b6-109">Nuget-Anmelde Informationsanbieter für Visual Studio funktionieren nur in Visual Studio (nicht in dotnet Restore oder nuget. exe).</span><span class="sxs-lookup"><span data-stu-id="5b2b6-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="5b2b6-110">Informationen zu Anmelde Informationsanbietern mit nuget. exe finden [Sie unter nuget. exe](nuget-exe-Credential-providers.md)-Anmelde Informationsanbieter.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="5b2b6-111">Informationen zu Anmelde Informationsanbietern in dotnet und MSBuild finden [Sie unter nuget-plattformübergreifende](nuget-cross-platform-authentication-plugin.md) Plug-ins</span><span class="sxs-lookup"><span data-stu-id="5b2b6-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="5b2b6-112">Verfügbare nuget-Anmelde Informationsanbieter für Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5b2b6-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="5b2b6-113">In der nuget-Erweiterung von Visual Studio ist ein Anmelde Informationsanbieter integriert, um Visual Studio Team Services zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="5b2b6-114">Die nuget Visual Studio-Erweiterung verwendet ein `VsCredentialProviderImporter` internes, das auch nach Plug-in-Anmelde Informationsanbietern sucht.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="5b2b6-115">Diese Plug-in-Anmelde Informationsanbieter müssen als MEF-Export vom Typ `IVsCredentialProvider`erkannt werden können.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="5b2b6-116">Folgende Plug-in-Anmelde Informationsanbieter sind verfügbar:</span><span class="sxs-lookup"><span data-stu-id="5b2b6-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="5b2b6-117">Myget-Anmelde Informationsanbieter für Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5b2b6-117">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="5b2b6-118">Erstellen eines nuget-Anmelde Informationsanbieters für Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5b2b6-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="5b2b6-119">Die nuget Visual Studio-Erweiterung 3.6 + implementiert einen internen "dedentialservice", der zum Abrufen von Anmelde Informationen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="5b2b6-120">Der Dienst "eigene Anmelde Informationen" enthält eine Liste integrierter und Plug-in-Anmelde Informationsanbieter.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="5b2b6-121">Jeder Anbieter wird sequenziell ausprobiert, bis Anmelde Informationen abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="5b2b6-122">Beim Erwerb der Anmelde Informationen versucht der Anmelde Informationsdienst, Anmelde Informationsanbieter in der folgenden Reihenfolge zu verwenden, und wird beendet, sobald Anmelde Informationen abgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="5b2b6-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="5b2b6-123">Anmelde Informationen werden aus den nuget-Konfigurationsdateien abgerufen (mit dem integrierten `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="5b2b6-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="5b2b6-124">Wenn sich die Paketquelle auf Visual Studio Team Services befindet, `VisualStudioAccountProvider` wird verwendet.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="5b2b6-125">Alle anderen Plug-in-Anmelde Informationsanbieter für Visual Studio werden nacheinander ausprobiert.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="5b2b6-126">Versuchen Sie, alle nuget-plattformübergreifenden Anmelde Informationsanbieter sequenziell zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="5b2b6-127">Wenn noch keine Anmelde Informationen abgerufen wurden, wird der Benutzer über ein Standardmäßiges Standard Authentifizierungs Dialogfeld zur Eingabe von Anmelde Informationen aufgefordert.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="5b2b6-128">Implementieren von ivscredentialprovider. getkredentialsasync</span><span class="sxs-lookup"><span data-stu-id="5b2b6-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="5b2b6-129">Um einen nuget-Anmelde Informationsanbieter für Visual Studio zu erstellen, erstellen Sie eine Visual Studio-Erweiterung, die einen öffentlichen MEF-Export verfügbar macht, der den `IVsCredentialProvider` -Typ implementiert, und entspricht den unten beschriebenen Prinzipien.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="5b2b6-130">Eine Beispiel Implementierung finden Sie im [vscredentialprovider-Beispiel](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="5b2b6-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="5b2b6-131">Jeder nuget-Anmelde Informationsanbieter für Visual Studio muss folgende Aktionen ausführen:</span><span class="sxs-lookup"><span data-stu-id="5b2b6-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="5b2b6-132">Bestimmen Sie, ob die Anmelde Informationen für den Ziel-URI vor dem Initiieren der Anmelde Informationen bereitgestellt werden können.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="5b2b6-133">Wenn der Anbieter keine Anmelde Informationen für die Ziel Quelle angeben kann, sollte er `null`zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="5b2b6-134">Wenn der Anbieter Anforderungen für den Ziel-URI verarbeitet, aber keine Anmelde Informationen angeben kann, sollte eine Ausnahme ausgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="5b2b6-135">Ein benutzerdefinierter nuget-Anmelde Informationsanbieter für Visual Studio muss `IVsCredentialProvider` die Schnittstelle implementieren, die im [nuget. VisualStudio-Paket](https://www.nuget.org/packages/NuGet.VisualStudio/)verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="5b2b6-136">Getkredentialasync</span><span class="sxs-lookup"><span data-stu-id="5b2b6-136">GetCredentialAsync</span></span>

| <span data-ttu-id="5b2b6-137">Eingabe Parameter</span><span class="sxs-lookup"><span data-stu-id="5b2b6-137">Input Parameter</span></span> |<span data-ttu-id="5b2b6-138">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="5b2b6-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="5b2b6-139">URI-URI</span><span class="sxs-lookup"><span data-stu-id="5b2b6-139">Uri uri</span></span> | <span data-ttu-id="5b2b6-140">Der Paketquellen-URI, für den Anmelde Informationen angefordert werden.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="5b2b6-141">IWebProxy-Proxy</span><span class="sxs-lookup"><span data-stu-id="5b2b6-141">IWebProxy proxy</span></span> | <span data-ttu-id="5b2b6-142">Der WebProxy, der für die Kommunikation im Netzwerk verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="5b2b6-143">NULL, wenn keine Proxy Authentifizierung konfiguriert ist.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="5b2b6-144">bool isproxyrequest</span><span class="sxs-lookup"><span data-stu-id="5b2b6-144">bool isProxyRequest</span></span> | <span data-ttu-id="5b2b6-145">True, wenn die Anforderung besteht, Anmelde Informationen für die Proxy Authentifizierung zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="5b2b6-146">Wenn die Implementierung für den Erwerb von Proxy Anmelde Informationen nicht gültig ist, sollte NULL zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="5b2b6-147">Boolescher isretry</span><span class="sxs-lookup"><span data-stu-id="5b2b6-147">bool isRetry</span></span> | <span data-ttu-id="5b2b6-148">True, wenn zuvor Anmelde Informationen für diesen URI angefordert wurden, die angegebenen Anmelde Informationen aber keinen autorisierten Zugriff hatten.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="5b2b6-149">bool nicht interaktiv</span><span class="sxs-lookup"><span data-stu-id="5b2b6-149">bool nonInteractive</span></span> | <span data-ttu-id="5b2b6-150">True gibt an, dass der Anmelde Informationsanbieter alle Benutzer Aufforderungen unterdrücken und stattdessen Standardwerte verwenden muss.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="5b2b6-151">CancellationToken CancellationToken</span><span class="sxs-lookup"><span data-stu-id="5b2b6-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="5b2b6-152">Dieses Abbruch Token sollte geprüft werden, um zu bestimmen, ob der Vorgang zum Anfordern von Anmelde Informationen abgebrochen wurde.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="5b2b6-153">**Rückgabewert**: Ein Anmelde Informationsobjekt, das die [ `System.Net.ICredentials` -Schnittstelle](/dotnet/api/system.net.icredentials?view=netstandard-2.0)implementiert.</span><span class="sxs-lookup"><span data-stu-id="5b2b6-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
