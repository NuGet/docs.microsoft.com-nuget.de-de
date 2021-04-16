---
title: Versionshinweise zu NuGet 5.7
description: Versionshinweise für NuGet 5.7, einschließlich neuer Features, Fehlerbehebungen und DCRs.
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 58ab481f0c6a6cb5549c269788170b8c3ff6002f
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508786"
---
# <a name="nuget-57-release-notes"></a>Versionshinweise zu NuGet 5.7

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version | Verfügbar in .NET SDK(s) |
|:---|:---|:---|
| [**5.7.0**](https://nuget.org/downloads) | [Visual Studio 2019, Version 16.7](https://visualstudio.microsoft.com/downloads/) | [3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |
| [**5.7.1**](https://nuget.org/downloads) | [Visual Studio 2019, Version 16.7](https://visualstudio.microsoft.com/downloads/) | [3.1.408](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Installiert mit Visual Studio 2019 mit .NET Core-Workload

## <a name="summary-whats-new-in-57"></a>Zusammenfassung: Neuerungen in 5.7

### <a name="features-added-in-this-release"></a>In dieser Version hinzugefügte Features

* Unterstützung für externe Aliase für NuGet-Paketverweise hinzugefügt – [#4989](https://github.com/NuGet/Home/issues/4989)

* Schnelleres Wechseln zwischen den Registerkarten "Installiert" und "Updates", indem es ihnen ermöglicht wurde, eine Datenquelle freizugeben und das Erneute Hochskalieren zu reduzieren – [#8294](https://github.com/NuGet/Home/issues/8294)

* Schnellere Wiederherstellung – Beschleunigung von Auswertungen durch Aufrufen von STATISCHEN MSBuild-Graph-APIs (dotnet.exe) [– #9644](https://github.com/NuGet/Home/issues/9644)

* Visual Studio Teilwiederherstellung für PackageReference-Projekte (no-op++) hinzugefügt – [#9513](https://github.com/NuGet/Home/issues/9513)

* Visual Studio Paket-Manager Benutzeroberfläche stürzt seltener ab, wenn fehlerhafte Paketquellen durchsucht werden, die mehr als die angeforderte Anzahl von Ergebnissen pro HTTP-Anforderung zurückgeben. - [#8478](https://github.com/NuGet/Home/issues/8478)

* Integration von PackageVersion-Informationen für Projekte im Nicht-SDK-Stil in VS-Wiederherstellung hinzugefügt – [#9236](https://github.com/NuGet/Home/issues/9236)

* Unterstützung für nuget.exe `-self -Source` https://feed  -  [Update-#1783](https://github.com/NuGet/Home/issues/1783) hinzugefügt

* Unterstützung für mehrere Konfigurationsdateien im Verzeichnis %APPDATA%\NuGet hinzugefügt – [#9394](https://github.com/NuGet/Home/issues/9394)

* DeterministicSourcePaths berücksichtigt jetzt NuGet-Quellpakete [– #9431](https://github.com/NuGet/Home/issues/9431)

* INuGetProjectService.GetInstalledPackagesAsync-Erweiterbarkeits-API [hinzugefügt – #9702](https://github.com/NuGet/Home/issues/9702)

* Die Interop-API wurde hinzugefügt, um Fallbackordner aufzählen zu können, ohne dass eine Projektmappe/ein Projekt erforderlich [ist – #9395](https://github.com/NuGet/Home/issues/9395)

* Option `latest` für #8808 `-MSBuildVersion`  -  [](https://github.com/NuGet/Home/issues/8808)

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

**Fehler:**

* Versuchen Sie bei einer dotnet-CLI-Wiederherstellung beim Starten von Anmeldeinformations-Plug-Ins die dotnet-CLI im Systempfad, wenn die Umgebungsvariable `DOTNET_HOST_PATH`  nicht definiert ist. - [#7438](https://github.com/NuGet/Home/issues/7438)

* nuget.exe Spezifikation generiert ein Copyrighttag mit hart codiertem Text copyright YYYY anstelle `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)

* NuGet.exe löst die Ausnahme "Authors required" während des Pakets einer CSPROJ-Datei aus, die Platzhalter und Assemblyinfo-Attribute ignoriert, wenn der Assemblyname [geändert wird – #4234](https://github.com/NuGet/Home/issues/4234)

* HttpRequestMessage wird mehrmals wiederverwendet, was bei SocketHttpHandler nicht unterstützt [#8661](https://github.com/NuGet/Home/issues/8661)

* NuGet.Indexing 5.6.0 Preview 3 und höher verwenden ein anderes Öffentliches Schlüsseltoken [– #9481](https://github.com/NuGet/Home/issues/9481)

* TreatWarningsAsErrors während der Erstellung des NuGet-Pakets [#7404](https://github.com/NuGet/Home/issues/7404)

* [CPVM] Falsche Paket downgrades für mehrere p2p-Projekte [– #9549](https://github.com/NuGet/Home/issues/9549)

* Die Registerkarte "Durchsuchen" ist nicht links mit dem Suchfeld ausgerichtet – [#9559](https://github.com/NuGet/Home/issues/9559)

* Die installierte Version ist inkonsistent mit dem eingebetteten Symbol in der PM-Benutzeroberfläche auf Projektmappenebene für eine Paket-ID mit mehreren installierten [Versionen – #9321](https://github.com/NuGet/Home/issues/9321)

* Leak: PartCreationPolicy(CreationPolicy.NonShared) NuGet.SolutionRestoreManager.RestoreOperationLogger [– #9595](https://github.com/NuGet/Home/issues/9595)

* Vermeiden Sie das Lesen der Ressourcendatei in No-Op-Wiederherstellungen [– #9693](https://github.com/NuGet/Home/issues/9693)

* NuGet.Protocol unterstützt nicht das Abrufen der Downloadanzahl einer Version aus der Suche – [#9086](https://github.com/NuGet/Home/issues/9086)

* Verbessern der Speicherleistung von PackageMetadataResourceV3 durch Reduzieren der JObject-Abhängigkeiten [– #9719](https://github.com/NuGet/Home/issues/9719)

**Entwurfsänderungsanforderungen:**

* Das Element wurde `<owners>` unterdrückt, wenn es redundant ist [– #5134](https://github.com/NuGet/Home/issues/5134)

* Protokollieren von IntervalTrackers als ETW-Ereignisse [– #9593](https://github.com/NuGet/Home/issues/9593)

* Bei der Wiederherstellung wurde eine Informationsmeldung hinzugefügt, um CPVM-Benutzer darüber zu informieren, dass sich das Feature in der Vorschau befindet [– #9340](https://github.com/NuGet/Home/issues/9340)

* Auffüllen Projektmappen-Explorer transitiven Paket-/Projektabhängigkeiten aus der Assets-Datei [– #9580](https://github.com/NuGet/Home/issues/9580)

* Die Registerkarte "Installierte Pakete" sollte die Paketliste nicht [paginieren – #6995](https://github.com/NuGet/Home/issues/6995)

**[Liste aller in dieser Version behobenen Probleme: 5.7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**

### <a name="community-contributions"></a>Beiträge aus der Community

Vielen Dank an alle Mitwirkenden, die dieses NuGet-Release super gemacht haben!

|Wer|Prs|Probleme|
|----|----|----|
|[- und -nau](https://github.com/campersau)|[3433](https://github.com/NuGet/NuGet.Client/pull/3433), [3120](https://github.com/NuGet/NuGet.Client/pull/3120)|NuGet.Protocol unterstützt nicht das Abrufen der Downloadanzahl einer Version aus der Suche [– #9086](https://github.com/NuGet/Home/issues/9086) </br>HttpRequestMessage wird mehrmals wiederverwendet, was mit SocketHttpHandler – [#8661](https://github.com/NuGet/Home/issues/8661)|
|[Musser (jnm2)](https://github.com/jnm2)|[3241](https://github.com/NuGet/NuGet.Client/pull/3241)|Das `<owners>` Element wurde unterdrückt, wenn es redundant [ist– #5134](https://github.com/NuGet/Home/issues/5134)|
|[Volodymyr Shkolka (BlackGad)](https://github.com/BlackGad)|[3273](https://github.com/NuGet/NuGet.Client/pull/3273)|NuGet kann keine Wiederherstellung aus HTTPS-Quellen vornehmen, die Clientzertifikate erfordern [– #5773](https://github.com/NuGet/Home/issues/5773)|
|[Sollus Ungureakus (Therzok)](https://github.com/Therzok)|[3357](https://github.com/NuGet/NuGet.Client/pull/3357)|HttpSourceAuthenticationHandler SemaphoreSlim – zukünftige Proofing – [#9463](https://github.com/NuGet/Home/issues/9463)|
|[Sunner (SuNNjek)](https://github.com/SuNNjek)|[3088](https://github.com/NuGet/NuGet.Client/pull/3088)|nuget.exe Spezifikation generiert ein Copyrighttag mit hart codiertem Text Copyright YYYY anstelle `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)|
|[Lip Spinelli ():/spinelli](https://github.com/olivier-spinelli)|[3335](https://github.com/NuGet/NuGet.Client/pull/3335)|Versuchen Sie bei einer dotnet-CLI-Wiederherstellung beim Starten von Anmeldeinformations-Plug-Ins die dotnet-CLI im Systempfad, wenn die Umgebungsvariable `DOTNET_HOST_PATH`  nicht definiert ist. - [#7438](https://github.com/NuGet/Home/issues/7438)|
|[goyzhang](https://github.com/goyzhang)|[3370](https://github.com/NuGet/NuGet.Client/pull/3370)|Option `latest` für #8808 `-MSBuildVersion`  -  [](https://github.com/NuGet/Home/issues/8808)|

## <a name="summary-whats-new-in-571"></a>Zusammenfassung: Neues in Version 5.7.1

* Erweitern Sie die Datei .nupkg.metadata, [](https://github.com/NuGet/Home/issues/10354) um die Installationsquelle ein#10354

* Protokollpaketinhalthash während der Wiederherstellungsprotokollierung (während der [Extraktion)](https://github.com/NuGet/Home/issues/10384) – #10384

* Protokollieren Sie bei der Wiederherstellung bei normaler Ausführlichkeit, von welcher Quelle ein Paket wiederhergestellt wird– [#10461](https://github.com/NuGet/Home/issues/10461)

**[Liste aller in diesem Release behobenen Probleme: 5.7.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f5724f84579cc29a79ee)**

**[Liste der Commits in diesem Release : 5.7.1](https://github.com/NuGet/NuGet.Client/compare/80512866a2c127e52ce3e86fd803fff77e9b9b52...5.7.1.4)**
