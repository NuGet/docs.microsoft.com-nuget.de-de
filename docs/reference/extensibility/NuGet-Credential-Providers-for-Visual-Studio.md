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
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Authentifizieren von Datenfeeds in Visual Studio mit NuGet-Anmeldeinformationsanbieter

Die NuGet-Erweiterung für Visual Studio 3.6 unterstützt Anmeldeinformationsanbieter, die NuGet authentifizierten Feeds portzuweisung zu ermöglichen.
Nach der Installation eines NuGet-Anmeldeinformationsanbieters für Visual Studio NuGet Visual Studio-Erweiterung automatisch abrufen und aktualisieren die Anmeldeinformationen für authentifizierte Feeds nach Bedarf.

Eine beispielimplementierung finden Sie im [im Beispiel VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

> [!Note]
> NuGet-Anmeldeinformationsanbieter für Visual Studio muss installiert sein, als reguläre Visual Studio-Erweiterung, und benötigen [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (zurzeit als Vorschau verfügbar) oder höher.
>
> NuGet-Anmeldeinformationsanbieter für Visual Studio funktionieren nur in Visual Studio (nicht im Dotnet wiederherstellen oder nuget.exe). Der Anmeldeinformationsanbieter mit nuget.exe, finden Sie unter [nuget.exe Anmeldeinformationsanbieter](nuget-exe-Credential-providers.md).

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Verfügbare NuGet Anmeldeinformationsanbieter für Visual Studio

Es ist ein Anmeldeinformationsanbieter zur Unterstützung von Visual Studio Team Services in Visual Studio NuGet-Erweiterung erstellt.

Die NuGet-Erweiterung für Visual Studio verwendet eine interne `VsCredentialProviderImporter` die sucht auch nach Anmeldeinformationsanbieter-Plug-in. Diese Anmeldeinformationsanbieter-Plug-in müssen als eine MEF-Export vom Typ sichtbar sein `IVsCredentialProvider`.

-Plug-In für anmeldeinformationenanbieter verfügbar sind:

- [MyGet Anmeldeinformationsanbieter für Visual Studio-2017](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Erstellen einen NuGet-Anmeldeinformationsanbieter für Visual Studio

Die NuGet-Erweiterung für Visual Studio 3.6 implementiert ein internes CredentialService, die verwendet wird, um die Anmeldeinformationen abzurufen. Die CredentialService umfasst eine Liste der integrierten und Plug-in-Anmeldeinformationsanbieter. Jeder Anbieter wird nacheinander ausprobiert, bis Anmeldeinformationen abgerufen werden.

Während der Übernahme von Anmeldeinformationen versucht der Anmeldeinformationsdienst Anmeldeinformationsanbieter in der folgenden Reihenfolge und hört auf, sobald Anmeldeinformationen abgerufen werden:

1. Anmeldeinformationen werden vom NuGet-Konfigurationsdateien abgerufen werden (unter Verwendung der integrierten `SettingsCredentialProvider`).
1. Wenn die Paketquelle auf Visual Studio Team Services ist die `VisualStudioAccountProvider` verwendet werden.
1. Alle anderen Plug-Ins Anmeldeinformationsanbieter werden nacheinander ausprobiert.
1. Wenn noch keine Anmeldeinformationen abgerufen wurden, wird der Benutzer zum Eingeben von Anmeldeinformationen mithilfe einer standard-Standardauthentifizierung-Dialogfeld aufgefordert werden.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implementieren von IVsCredentialProvider.GetCredentialsAsync

Um ein NuGet-Anmeldeinformationsanbieter für Visual Studio zu erstellen, erstellen Sie eine Visual Studio-Erweiterung, die einen öffentlichen MEF-Export implementieren verfügbar macht die `IVsCredentialProvider` geben, und mit den unten beschriebenen Regeln entspricht.

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

Eine beispielimplementierung finden Sie im [im Beispiel VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Jede Anmeldeinformationsanbieter NuGet für Visual Studio muss:

1. Bestimmen Sie, ob sie Anmeldeinformationen für den Ziel-URI bereitstellen kann, vor dem Initiieren der Übernahme von Anmeldeinformationen. Wenn der Anbieter kann nicht die Anmeldeinformationen für die targeted Quelle, sollte zurückgegeben `null`.
1. Wenn der Anbieter Anforderungen für den Ziel-URI behandelt, jedoch keine Anmeldeinformationen bereitstellen, sollte eine Ausnahme ausgelöst werden.

Eine benutzerdefinierte NuGet-Anmeldeinformationsanbieter für Visual Studio muss implementieren die `IVsCredentialProvider` -Schnittstelle in der [NuGet.VisualStudio Paket](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Eingabeparameter |Beschreibung|
| ----------------|-----------|
| URI-uri | Die Paket-Quell-Uri für die Anmeldeinformationen angefordert werden.|
| IWebProxy proxy | Der Webproxy verwendet, bei der Kommunikation im Netzwerk. NULL, wenn es keine Proxyauthentifizierung konfiguriert ist. |
| Bool isProxyRequest | "True", wenn die Anforderung beim Authentifizierungsanmeldeinformationen abrufen ist. Wenn die Implementierung für den Erwerb von Proxy-Anmeldeinformationen ungültig ist, sollte Null zurückgegeben. |
| Bool isRetry | "True", wenn Anmeldeinformationen für diesen Uri bereits zuvor angefordert wurden, aber die angegebenen Anmeldeinformationen wurde aufgrund nicht autorisierten Zugriff zugelassen. |
| nicht interaktive bool | Bei "true", muss die Anmeldeinformationsanbieter werden alle benutzeraufforderungen unterdrückt und verwenden Sie stattdessen Default-Werte. |
| CancellationToken cancellationToken | Dieses Abbruchtoken sollte überprüft werden, um festzustellen, ob der Vorgang Anfordern von Anmeldeinformationen wurde abgebrochen. |

**Rückgabewert**: Anmeldeinformationen Objekt implementiert die [ `System.Net.ICredentials` Schnittstelle](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
