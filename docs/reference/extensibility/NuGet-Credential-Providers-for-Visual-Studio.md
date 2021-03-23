---
title: NuGet-Anmeldeinformationsanbieter für Visual Studio
description: Nuget-Anmelde Informationsanbieter authentifizieren sich mit Feeds, indem die ivscredentialprovider-Schnittstelle in einer Visual Studio-Erweiterung implementiert wird.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: ab3bde0d320375f854a8f0a98fb90acfecf54aa3
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859095"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Authentifizieren von Feeds in Visual Studio mit nuget-Anmelde Informationsanbietern

Die nuget Visual Studio-Erweiterung 3.6 und höher unterstützt Anmelde Informationsanbieter, mit denen nuget mit authentifizierten Feeds arbeiten kann.
Nachdem Sie einen nuget-Anmelde Informationsanbieter für Visual Studio installiert haben, werden die Anmelde Informationen für authentifizierte Feeds von der nuget-Erweiterung für Visual Studio nach Bedarf automatisch abgerufen und aktualisiert.

Eine Beispiel Implementierung finden Sie im [vscredentialprovider-Beispiel](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider).

In Visual Studio verwendet nuget einen internen, `VsCredentialProviderImporter` der auch nach Plug-in-Anmelde Informationsanbietern sucht. Diese Plug-in-Anmelde Informationsanbieter müssen als MEF-Export vom Typ erkannt werden können `IVsCredentialProvider` .

Ab 4.8 + nuget in Visual Studio unterstützt auch die neuen plattformübergreifenden Authentifizierungs-Plug-ins, aber Sie sind aus Leistungsgründen nicht empfehlenswert.

> [!Note]
> Nuget-Anmelde Informationsanbieter für Visual Studio müssen als reguläre Visual Studio-Erweiterung installiert sein und benötigen [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) oder höher.
>
> Nuget-Anmelde Informationsanbieter für Visual Studio funktionieren nur in Visual Studio (nicht in dotnet Restore oder nuget.exe). Informationen zu Anmelde Informationsanbietern mit nuget.exe finden Sie unternuget.exe Anmelde Informations [ Anbietern](nuget-exe-Credential-providers.md).
> Informationen zu Anmelde Informationsanbietern in dotnet und MSBuild finden [Sie unter nuget-plattformübergreifende](nuget-cross-platform-authentication-plugin.md) Plug-ins

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Erstellen eines nuget-Anmelde Informationsanbieters für Visual Studio

Die nuget Visual Studio-Erweiterung 3.6 + implementiert einen internen "dedentialservice", der zum Abrufen von Anmelde Informationen verwendet wird. Der Dienst "eigene Anmelde Informationen" enthält eine Liste integrierter und Plug-in-Anmelde Informationsanbieter. Jeder Anbieter wird sequenziell ausprobiert, bis Anmelde Informationen abgerufen werden.

Beim Erwerb der Anmelde Informationen versucht der Anmelde Informationsdienst, Anmelde Informationsanbieter in der folgenden Reihenfolge zu verwenden, und wird beendet, sobald Anmelde Informationen abgerufen werden:

1. Anmelde Informationen werden aus den nuget-Konfigurationsdateien abgerufen (mit dem integrierten `SettingsCredentialProvider` ).
1. Wenn sich die Paketquelle auf Visual Studio Team Services befindet, `VisualStudioAccountProvider` wird verwendet.
1. Alle anderen Plug-in-Anmelde Informationsanbieter für Visual Studio werden nacheinander ausprobiert.
1. Versuchen Sie, alle nuget-plattformübergreifenden Anmelde Informationsanbieter sequenziell zu verwenden.
1. Wenn noch keine Anmelde Informationen abgerufen wurden, wird der Benutzer über ein Standardmäßiges Standard Authentifizierungs Dialogfeld zur Eingabe von Anmelde Informationen aufgefordert.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implementieren von ivscredentialprovider. getkredentialsasync

Um einen nuget-Anmelde Informationsanbieter für Visual Studio zu erstellen, erstellen Sie eine Visual Studio-Erweiterung, die einen öffentlichen MEF-Export verfügbar macht, der den `IVsCredentialProvider` -Typ implementiert, und entspricht den unten beschriebenen Prinzipien.

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

Eine Beispiel Implementierung finden Sie im [vscredentialprovider-Beispiel](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider).

Jeder nuget-Anmelde Informationsanbieter für Visual Studio muss folgende Aktionen ausführen:

1. Bestimmen Sie, ob die Anmelde Informationen für den Ziel-URI vor dem Initiieren der Anmelde Informationen bereitgestellt werden können. Wenn der Anbieter keine Anmelde Informationen für die Ziel Quelle angeben kann, sollte er zurückgeben `null` .
1. Wenn der Anbieter Anforderungen für den Ziel-URI verarbeitet, aber keine Anmelde Informationen angeben kann, sollte eine Ausnahme ausgelöst werden.

Ein benutzerdefinierter nuget-Anmelde Informationsanbieter für Visual Studio muss die Schnittstelle implementieren, die `IVsCredentialProvider` im [nuget. VisualStudio-Paket](https://www.nuget.org/packages/NuGet.VisualStudio/)verfügbar ist.

#### <a name="getcredentialasync"></a>Getkredentialasync

| Eingabeparameter |BESCHREIBUNG|
| ----------------|-----------|
| URI-URI | Der Paketquellen-URI, für den Anmelde Informationen angefordert werden.|
| IWebProxy-Proxy | Der WebProxy, der für die Kommunikation im Netzwerk verwendet werden soll. NULL, wenn keine Proxy Authentifizierung konfiguriert ist. |
| bool isproxyrequest | True, wenn die Anforderung besteht, Anmelde Informationen für die Proxy Authentifizierung zu erhalten. Wenn die Implementierung für den Erwerb von Proxy Anmelde Informationen nicht gültig ist, sollte NULL zurückgegeben werden. |
| Boolescher isretry | True, wenn zuvor Anmelde Informationen für diesen URI angefordert wurden, die angegebenen Anmelde Informationen aber keinen autorisierten Zugriff hatten. |
| bool nicht interaktiv | True gibt an, dass der Anmelde Informationsanbieter alle Benutzer Aufforderungen unterdrücken und stattdessen Standardwerte verwenden muss. |
| CancellationToken CancellationToken | Dieses Abbruch Token sollte geprüft werden, um zu bestimmen, ob der Vorgang zum Anfordern von Anmelde Informationen abgebrochen wurde. |

**Rückgabewert**: ein Anmelde Informationsobjekt, das die- [ `System.Net.ICredentials` Schnittstelle](/dotnet/api/system.net.icredentials)implementiert.
