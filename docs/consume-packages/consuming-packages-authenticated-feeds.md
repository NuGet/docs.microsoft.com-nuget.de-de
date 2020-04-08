---
title: Nutzen von Paketen aus authentifizierten Feeds
description: Nutzen von Paketen aus authentifizierten Feeds in allen NuGet-Clientszenarios
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231740"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>Nutzen von Paketen aus authentifizierten Feeds

Zusätzlich zum [öffentlichen Feed](https://api.nuget.org/v3/index.json) von nuget.org können NuGet-Clients mit Datei-Feeds und privaten http-Feeds interagieren.


Für das Authentifizieren mit privaten http-Feeds sind zwei Vorgehensweisen möglich:

* Hinzufügen von Anmeldeinformationen in der Datei [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials),
* Authentifizieren mithilfe eines der zahlreichen Erweiterbarkeitsmodelle, je nach verwendetem Client.

## <a name="nuget-clients-authentication-extensibility"></a>Erweiterbarkeit der Authentifizierung von NuGet-Clients

Bei den verschiedenen NuGet-Clients ist der Anbieter des privaten Feeds selbst für die Authentifizierung verantwortlich.
Alle NuGet-Clients verfügen über Erweiterbarkeitsmethoden, um dies zu unterstützen. Hierbei handelt es sich entweder um eine Visual Studio-Erweiterung oder um ein Plug-In, die bzw. das mit NuGet kommunizieren kann, um Anmeldeinformationen abzurufen.

### <a name="visual-studio"></a>Visual Studio

In Visual Studio macht NuGet eine Schnittstelle verfügbar, die Feed-Anbieter implementieren und ihren Kunden bereitstellen können. Weitere Informationen finden Sie in der Dokumentation zum [Erstellen eines Visual Studio-Anmeldeinformationsanbieters](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>Verfügbare NuGet-Anmeldeinformationsanbieter für Visual Studio

In Visual Studio ist ein Anmeldeinformationsanbieter integriert, der Azure DevOps unterstützt.


Folgende Plug-In-Anmeldeinformationsanbieter sind verfügbar:

* [MyGet Credential Provider for Visual Studio](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

Wenn `nuget.exe` Anmeldeinformationen für die Authentifizierung bei einem Feed benötigt, werden diese wie folgt gesucht:

1. Suchen nach Anmeldeinformationen in `NuGet.config`-Dateien.
1. Verwenden von V2-Plug-In-Anmeldeinformationsanbietern
1. Verwenden von V1-Plug-In-Anmeldeinformationsanbietern
1. NuGet fordert dann den Benutzer zur Eingabe von Anmeldeinformationen in der Befehlszeile auf.

#### <a name="nugetexe-and-v2-credential-providers"></a>nuget.exe- und V2-Anmeldeinformationsanbieter

In Version `4.8` hat NuGet einen neuen Authentifizierungs-Plug-In-Mechanismus definiert, der im Folgenden als V2-Anmeldeinformationsanbieter bezeichnet wird.
Informationen zur Installation und Ermittlung dieser Anbieter finden Sie unter [Plattformübergreifende NuGet-Plug-Ins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="nugetexe-and-v1-credential-providers"></a>nuget.exe- und V1-Anmeldeinformationsanbieter

In Version `3.3` führte NuGet die erste Version der Authentifizierungs-Plug-ins ein.
Informationen zur Installation und Ermittlung dieser Anbieter finden Sie unter [nuget.exe-Anmeldeinformationsanbieter](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery).

#### <a name="available-credential-providers-for-nugetexe"></a>Verfügbare Anmeldeinformationsanbieter für nuget.exe

* [Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) oder [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)

Seit Visual Studio 2017 Version 15.9 ist der Azure DevOps-Anmeldeinformationsanbieter in Visual Studio gebündelt.
Wenn `nuget.exe` MSBuild aus diesem speziellen Visual Studio-Toolset verwendet, wird das Plug-In automatisch erkannt.

### <a name="dotnetexe"></a>dotnet.exe

Wenn `dotnet.exe` Anmeldeinformationen für die Authentifizierung bei einem Feed benötigt, werden diese wie folgt gesucht:

1. Suchen nach Anmeldeinformationen in `NuGet.config`-Dateien.
1. Verwenden von V2-Plug-In-Anmeldeinformationsanbietern

`dotnet.exe` ist standardmäßig nicht interaktiv, daher müssen Sie möglicherweise ein `--interactive`-Flag übergeben, damit das Tool für die Authentifizierung gesperrt wird.

#### <a name="dotnetexe-and-v2-credential-providers"></a>dotnet.exe- und V2-Anmeldeinformationsanbieter

In Version `2.2.100` des SDK hat NuGet einen Authentifizierungs-Plug-In-Mechanismus definiert, der bei allen Clients funktioniert.
Informationen zur Installation und Ermittlung dieser Anbieter finden Sie unter [Plattformübergreifende NuGet-Plug-Ins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-dotnetexe"></a>Verfügbare Anmeldeinformationsanbieter für dotnet.exe

* [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>MSBuild.exe

Wenn `MSBuild.exe` Anmeldeinformationen für die Authentifizierung bei einem Feed benötigt, werden diese wie folgt gesucht:

1. Suchen nach Anmeldeinformationen in `NuGet.config`-Dateien
1. Verwenden von V2-Plug-In-Anmeldeinformationsanbietern

`MSBuild.exe` ist standardmäßig nicht interaktiv, sodass Sie möglicherweise die `/p:NuGetInteractive=true`-Eigenschaft festlegen müssen, damit das Tool für die Authentifizierung gesperrt wird.

#### <a name="msbuildexe-and-v2-credential-providers"></a>MSBuild.exe- und V2-Anmeldeinformationsanbieter

In Visual Studio 2019 Update 9 hat NuGet einen Authentifizierungs-Plug-In-Mechanismus definiert, der bei allen Clients funktioniert.
Informationen zur Installation und Ermittlung dieser Anbieter finden Sie unter [Plattformübergreifende NuGet-Plug-Ins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-msbuildexe"></a>Verfügbare Anmeldeinformationsanbieter für MSBuild.exe

* [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)

Seit Visual Studio 2017 Update 9 ist der Azure DevOps-Anmeldeinformationsanbieter in Visual Studio gebündelt. Weitere Schritte sind nicht erforderlich.
