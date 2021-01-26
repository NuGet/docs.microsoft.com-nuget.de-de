---
title: NuGet-Anmeldeinformationsanbieter für Visual Studio
description: Nuget-Anmelde Informationsanbieter authentifizieren sich mit Feeds, indem die ivscredentialprovider-Schnittstelle in einer Visual Studio-Erweiterung implementiert wird.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: f324f1e27e0d718571525152fcf16b55b900dbaa
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777754"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="fb05c-103">Authentifizieren von Feeds in Visual Studio mit nuget-Anmelde Informationsanbietern</span><span class="sxs-lookup"><span data-stu-id="fb05c-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="fb05c-104">Die nuget Visual Studio-Erweiterung 3.6 und höher unterstützt Anmelde Informationsanbieter, mit denen nuget mit authentifizierten Feeds arbeiten kann.</span><span class="sxs-lookup"><span data-stu-id="fb05c-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="fb05c-105">Nachdem Sie einen nuget-Anmelde Informationsanbieter für Visual Studio installiert haben, werden die Anmelde Informationen für authentifizierte Feeds von der nuget-Erweiterung für Visual Studio nach Bedarf automatisch abgerufen und aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="fb05c-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="fb05c-106">Eine Beispiel Implementierung finden Sie im [vscredentialprovider-Beispiel](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="fb05c-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="fb05c-107">In Visual Studio verwendet nuget einen internen, `VsCredentialProviderImporter` der auch nach Plug-in-Anmelde Informationsanbietern sucht.</span><span class="sxs-lookup"><span data-stu-id="fb05c-107">Within Visual Studio, NuGet uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="fb05c-108">Diese Plug-in-Anmelde Informationsanbieter müssen als MEF-Export vom Typ erkannt werden können `IVsCredentialProvider` .</span><span class="sxs-lookup"><span data-stu-id="fb05c-108">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="fb05c-109">Ab 4.8 + nuget in Visual Studio unterstützt auch die neuen plattformübergreifenden Authentifizierungs-Plug-ins, aber Sie sind aus Leistungsgründen nicht empfehlenswert.</span><span class="sxs-lookup"><span data-stu-id="fb05c-109">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="fb05c-110">Nuget-Anmelde Informationsanbieter für Visual Studio müssen als reguläre Visual Studio-Erweiterung installiert sein und benötigen [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) oder höher.</span><span class="sxs-lookup"><span data-stu-id="fb05c-110">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="fb05c-111">Nuget-Anmelde Informationsanbieter für Visual Studio funktionieren nur in Visual Studio (nicht in dotnet Restore oder nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="fb05c-111">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="fb05c-112">Informationen zu Anmelde Informationsanbietern mit nuget.exe finden Sie unternuget.exe Anmelde Informations [ Anbietern](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="fb05c-112">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="fb05c-113">Informationen zu Anmelde Informationsanbietern in dotnet und MSBuild finden [Sie unter nuget-plattformübergreifende](nuget-cross-platform-authentication-plugin.md) Plug-ins</span><span class="sxs-lookup"><span data-stu-id="fb05c-113">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="fb05c-114">Erstellen eines nuget-Anmelde Informationsanbieters für Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fb05c-114">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="fb05c-115">Die nuget Visual Studio-Erweiterung 3.6 + implementiert einen internen "dedentialservice", der zum Abrufen von Anmelde Informationen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="fb05c-115">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="fb05c-116">Der Dienst "eigene Anmelde Informationen" enthält eine Liste integrierter und Plug-in-Anmelde Informationsanbieter.</span><span class="sxs-lookup"><span data-stu-id="fb05c-116">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="fb05c-117">Jeder Anbieter wird sequenziell ausprobiert, bis Anmelde Informationen abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="fb05c-117">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="fb05c-118">Beim Erwerb der Anmelde Informationen versucht der Anmelde Informationsdienst, Anmelde Informationsanbieter in der folgenden Reihenfolge zu verwenden, und wird beendet, sobald Anmelde Informationen abgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="fb05c-118">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="fb05c-119">Anmelde Informationen werden aus den nuget-Konfigurationsdateien abgerufen (mit dem integrierten `SettingsCredentialProvider` ).</span><span class="sxs-lookup"><span data-stu-id="fb05c-119">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="fb05c-120">Wenn sich die Paketquelle auf Visual Studio Team Services befindet, `VisualStudioAccountProvider` wird verwendet.</span><span class="sxs-lookup"><span data-stu-id="fb05c-120">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="fb05c-121">Alle anderen Plug-in-Anmelde Informationsanbieter für Visual Studio werden nacheinander ausprobiert.</span><span class="sxs-lookup"><span data-stu-id="fb05c-121">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="fb05c-122">Versuchen Sie, alle nuget-plattformübergreifenden Anmelde Informationsanbieter sequenziell zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="fb05c-122">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="fb05c-123">Wenn noch keine Anmelde Informationen abgerufen wurden, wird der Benutzer über ein Standardmäßiges Standard Authentifizierungs Dialogfeld zur Eingabe von Anmelde Informationen aufgefordert.</span><span class="sxs-lookup"><span data-stu-id="fb05c-123">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="fb05c-124">Implementieren von ivscredentialprovider. getkredentialsasync</span><span class="sxs-lookup"><span data-stu-id="fb05c-124">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="fb05c-125">Um einen nuget-Anmelde Informationsanbieter für Visual Studio zu erstellen, erstellen Sie eine Visual Studio-Erweiterung, die einen öffentlichen MEF-Export verfügbar macht, der den `IVsCredentialProvider` -Typ implementiert, und entspricht den unten beschriebenen Prinzipien.</span><span class="sxs-lookup"><span data-stu-id="fb05c-125">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="fb05c-126">Eine Beispiel Implementierung finden Sie im [vscredentialprovider-Beispiel](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="fb05c-126">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="fb05c-127">Jeder nuget-Anmelde Informationsanbieter für Visual Studio muss folgende Aktionen ausführen:</span><span class="sxs-lookup"><span data-stu-id="fb05c-127">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="fb05c-128">Bestimmen Sie, ob die Anmelde Informationen für den Ziel-URI vor dem Initiieren der Anmelde Informationen bereitgestellt werden können.</span><span class="sxs-lookup"><span data-stu-id="fb05c-128">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="fb05c-129">Wenn der Anbieter keine Anmelde Informationen für die Ziel Quelle angeben kann, sollte er zurückgeben `null` .</span><span class="sxs-lookup"><span data-stu-id="fb05c-129">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="fb05c-130">Wenn der Anbieter Anforderungen für den Ziel-URI verarbeitet, aber keine Anmelde Informationen angeben kann, sollte eine Ausnahme ausgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="fb05c-130">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="fb05c-131">Ein benutzerdefinierter nuget-Anmelde Informationsanbieter für Visual Studio muss die Schnittstelle implementieren, die `IVsCredentialProvider` im [nuget. VisualStudio-Paket](https://www.nuget.org/packages/NuGet.VisualStudio/)verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="fb05c-131">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="fb05c-132">Getkredentialasync</span><span class="sxs-lookup"><span data-stu-id="fb05c-132">GetCredentialAsync</span></span>

| <span data-ttu-id="fb05c-133">Eingabeparameter</span><span class="sxs-lookup"><span data-stu-id="fb05c-133">Input Parameter</span></span> |<span data-ttu-id="fb05c-134">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="fb05c-134">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="fb05c-135">URI-URI</span><span class="sxs-lookup"><span data-stu-id="fb05c-135">Uri uri</span></span> | <span data-ttu-id="fb05c-136">Der Paketquellen-URI, für den Anmelde Informationen angefordert werden.</span><span class="sxs-lookup"><span data-stu-id="fb05c-136">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="fb05c-137">IWebProxy-Proxy</span><span class="sxs-lookup"><span data-stu-id="fb05c-137">IWebProxy proxy</span></span> | <span data-ttu-id="fb05c-138">Der WebProxy, der für die Kommunikation im Netzwerk verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="fb05c-138">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="fb05c-139">NULL, wenn keine Proxy Authentifizierung konfiguriert ist.</span><span class="sxs-lookup"><span data-stu-id="fb05c-139">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="fb05c-140">bool isproxyrequest</span><span class="sxs-lookup"><span data-stu-id="fb05c-140">bool isProxyRequest</span></span> | <span data-ttu-id="fb05c-141">True, wenn die Anforderung besteht, Anmelde Informationen für die Proxy Authentifizierung zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="fb05c-141">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="fb05c-142">Wenn die Implementierung für den Erwerb von Proxy Anmelde Informationen nicht gültig ist, sollte NULL zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="fb05c-142">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="fb05c-143">Boolescher isretry</span><span class="sxs-lookup"><span data-stu-id="fb05c-143">bool isRetry</span></span> | <span data-ttu-id="fb05c-144">True, wenn zuvor Anmelde Informationen für diesen URI angefordert wurden, die angegebenen Anmelde Informationen aber keinen autorisierten Zugriff hatten.</span><span class="sxs-lookup"><span data-stu-id="fb05c-144">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="fb05c-145">bool nicht interaktiv</span><span class="sxs-lookup"><span data-stu-id="fb05c-145">bool nonInteractive</span></span> | <span data-ttu-id="fb05c-146">True gibt an, dass der Anmelde Informationsanbieter alle Benutzer Aufforderungen unterdrücken und stattdessen Standardwerte verwenden muss.</span><span class="sxs-lookup"><span data-stu-id="fb05c-146">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="fb05c-147">CancellationToken CancellationToken</span><span class="sxs-lookup"><span data-stu-id="fb05c-147">CancellationToken cancellationToken</span></span> | <span data-ttu-id="fb05c-148">Dieses Abbruch Token sollte geprüft werden, um zu bestimmen, ob der Vorgang zum Anfordern von Anmelde Informationen abgebrochen wurde.</span><span class="sxs-lookup"><span data-stu-id="fb05c-148">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="fb05c-149">**Rückgabewert**: ein Anmelde Informationsobjekt, das die- [ `System.Net.ICredentials` Schnittstelle](/dotnet/api/system.net.icredentials?view=netstandard-2.0)implementiert.</span><span class="sxs-lookup"><span data-stu-id="fb05c-149">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
