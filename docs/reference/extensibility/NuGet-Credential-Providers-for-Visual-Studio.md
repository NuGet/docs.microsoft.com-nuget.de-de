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
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Authentifizieren von Datenfeeds in Visual Studio mit NuGet-Anmeldeinformationsanbieter

Die Visual Studio-Erweiterung für NuGet 3.6 unterstützt Anmeldeinformationsanbieter, bei die NuGet mit authentifizierte Feeds arbeiten können.
Nachdem Sie einen NuGet-Anmeldeinformationsanbieter für Visual Studio installieren, NuGet Visual Studio-Erweiterung automatisch abrufen und aktualisieren die Anmeldeinformationen für authentifizierte Feeds nach Bedarf.

Eine beispielimplementierung finden Sie im [VsCredentialProvider Beispiel](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

4.8 ab NuGet in Visual Studio unterstützt die neue plattformübergreifende Authentifizierung Plug-Ins auch, aber sie sind nicht die empfohlene Vorgehensweise zur Verbesserung der Leistung.

> [!Note]
> NuGet-Anmeldeinformationsanbieter für Visual Studio muss als reguläre Visual Studio-Erweiterung installiert werden und müssen [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) oder höher.
>
> NuGet-Anmeldeinformationsanbieter für Visual Studio funktionieren nur in Visual Studio (nicht im Dotnet Restore "oder" nuget.exe "). Der Anmeldeinformationsanbieter bei nuget.exe, finden Sie unter [nuget.exe-Anmeldeinformationsanbieter](nuget-exe-Credential-providers.md).
> Anmeldeinformationen-Anbieter in Dotnet und Msbuild finden Sie unter [NuGet cross-Platform-Plug-Ins](nuget-cross-platform-authentication-plugin.md)

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Verfügbare NuGet-Anmeldeinformationsanbieter für Visual Studio

Es gibt einen Anmeldeinformationsanbieter erstellt, in der Visual Studio-NuGet-Erweiterung zur Unterstützung von Visual Studio Team Services.

Die NuGet-Erweiterung für Visual Studio verwendet eine interne `VsCredentialProviderImporter` das für Anmeldeinformationsanbieter-Plug-Ins werden überprüft. Diese Anmeldeinformationsanbieter--Plug-in müssen als ein MEF-Export vom Typ erkannt werden, `IVsCredentialProvider`.

-Plug-in-Anmeldeinformationsanbieter verfügbar sind:

- [MyGet-Anmeldeinformationsanbieter für Visual Studio 2017](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Erstellen einen NuGet-Anmeldeinformationsanbieter für Visual Studio

Die Visual Studio-Erweiterung für NuGet 3.6 implementiert eine interne CredentialService, die zum Abrufen der Anmeldeinformationen verwendet wird. Die CredentialService hat es sich um eine Liste der integrierten und Plug-in-Anmeldeinformationsanbieter. Jeder Anbieter wird nacheinander ausprobiert, bis Anmeldeinformationen abgerufen werden.

Beim Abrufen von Anmeldeinformationen versucht der Anmeldeinformationsdienst Anmeldeinformationsanbieter in der folgenden Reihenfolge und hört auf, sobald Anmeldeinformationen abgerufen werden:

1. Anmeldeinformationen werden von NuGet-Konfigurationsdateien abgerufen werden (unter Verwendung der integrierten `SettingsCredentialProvider`).
1. Wenn die Paketquelle in Visual Studio Team Services ist die `VisualStudioAccountProvider` verwendet werden.
1. Alle anderen-Plug-in Visual Studio Anmeldeinformationsanbieter werden nacheinander ausprobiert.
1. Versuchen Sie es, alle NuGet cross-Platform-Anmeldeinformationsanbieter sequenziell zu verwenden.
1. Wenn noch keine Anmeldeinformationen abgerufen wurden, wird der Benutzer zur Eingabe von Anmeldeinformationen mithilfe einer standard Standardauthentifizierung-Dialogfelds aufgefordert werden.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implementieren von IVsCredentialProvider.GetCredentialsAsync

Um ein NuGet-Anmeldeinformationsanbieter für Visual Studio zu erstellen, erstellen Sie eine Visual Studio-Erweiterung, die einen öffentlichen MEF-Export Implementierung verfügbar macht die `IVsCredentialProvider` geben, und die unten beschriebenen Prinzipien folgt.

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

Eine beispielimplementierung finden Sie im [VsCredentialProvider Beispiel](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Jedes NuGet-Anmeldeinformationsanbieter für Visual Studio muss:

1. Bestimmen Sie, ob sie Anmeldeinformationen für den Ziel-URI angeben kann, vor dem Abrufen von Anmeldeinformationen zu initiieren. Wenn der Anbieter kann Anmeldeinformationen für die entsprechenden Quelle nicht bereitstellen, sollte zurückgegeben `null`.
1. Wenn der Anbieter Anforderungen für den Ziel-URI behandelt, aber Sie können keine Anmeldeinformationen bereitstellen, sollte eine Ausnahme ausgelöst werden.

Implementieren Sie einen benutzerdefinierten NuGet-Anmeldeinformationsanbieter für Visual Studio muss die `IVsCredentialProvider` -Schnittstelle in der [NuGet.VisualStudio Paket](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Eingabeparameter |Beschreibung|
| ----------------|-----------|
| URI-uri | Die Paket-Quell-Uri für den Anmeldeinformationen angefordert werden.|
| IWebProxy-proxy | Der Webproxy verwenden, bei der Kommunikation über das Netzwerk. NULL, wenn es keine Proxyauthentifizierung konfiguriert gibt. |
| "bool" isProxyRequest | "True", wenn die Anforderung beim Anmeldeinformationen für die Authentifizierung abrufen ist. Wenn die Implementierung für den Erwerb von Proxy-Anmeldeinformationen ungültig ist, sollte Null zurückgegeben werden. |
| "bool" isRetry | True, wenn die Anmeldeinformationen wurden für diesen Uri bereits zuvor angefordert, aber die angegebenen Anmeldeinformationen wurde nicht autorisierten Zugriff zugelassen. |
| nicht interaktive "bool" | Bei "true", muss der Anmeldeinformationsanbieter werden alle benutzeraufforderungen unterdrückt und verwenden Sie stattdessen die Standardwerte. |
| CancellationToken-cancellationToken | Dieses Abbruchtoken sollte überprüft werden, um festzustellen, ob der Vorgang Anfordern von Anmeldeinformationen wurde abgebrochen. |

**Rückgabewert**: eine objektimplementierung Anmeldeinformationen der [ `System.Net.ICredentials` Schnittstelle](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
