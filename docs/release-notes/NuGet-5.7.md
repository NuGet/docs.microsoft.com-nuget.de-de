---
title: Anmerkungen zu dieser Version von nuget 5,7
description: Anmerkungen zu dieser Version von nuget 5,7, einschließlich neuer Features, Fehlerbehebungen und dcrs.
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 6c821091983ab0b5d59b759e1ee9930cf449fd9d
ms.sourcegitcommit: 6cda91f135e58cf57a2471b0c7c4a2f748f40024
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/02/2020
ms.locfileid: "89364151"
---
# <a name="nuget-57-release-notes"></a>Anmerkungen zu dieser Version von nuget 5,7

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version | Verfügbar in .NET SDK(s) |
|:---|:---|:---|
| [**5.7.0**](https://nuget.org/downloads) | [Visual Studio 2019, Version 16.7](https://visualstudio.microsoft.com/downloads/) | [3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> installiert mit Visual Studio 2019 mit .net Core-Arbeitsauslastung

## <a name="summary-whats-new-in-57"></a>Zusammenfassung: Neues in 5,7

### <a name="features-added-in-this-release"></a>In dieser Version hinzugefügte Features

* Externe Alias Unterstützung für nuget-Paket Verweise- [#4989](https://github.com/NuGet/Home/issues/4989) wurde hinzugefügt.

* Der Wechsel zwischen installierten und Aktualisierungs Registerkarten wurde beschleunigt, da Sie eine Datenquelle freigeben und resfreshing- [#8294](https://github.com/NuGet/Home/issues/8294) reduzieren können.

* Schnellere Beschleunigung von Auswertungen durch Aufrufen von MSBuild static Graph-APIs (dotnet.exe)- [#9644](https://github.com/NuGet/Home/issues/9644)

* Hinzugefügte Visual Studio-Teil Wiederherstellung für packagereferenzierungsprojekte (No-OP + +)- [#9513](https://github.com/NuGet/Home/issues/9513)

* Die Visual Studio-Paket-Manager-Benutzeroberfläche stürzt beim Suchen fehlerhafter Paketquellen, die mehr als die angeforderte Anzahl von Ergebnissen pro HTTP-Anforderung zurückgeben, weniger häufig ab. - [#8478](https://github.com/NuGet/Home/issues/8478)

* Hinzugefügte Integration von packageversion-Informationen für nicht-SDK-Stil Projekte in vs Restore- [#9236](https://github.com/NuGet/Home/issues/9236)

* Unterstützung für nuget.exe Update `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)

* Unterstützung für mehrere Konfigurationsdateien im Verzeichnis "%APPDATA%\nuget" wurde hinzugefügt [#9394](https://github.com/NuGet/Home/issues/9394)

* Deterministicsourcepath nimmt jetzt nuget-Quellpakete in Konto [#9431](https://github.com/NuGet/Home/issues/9431)

* Hinzugefügte inugetprojectservice. getinstalledpackagesasync-Erweiterbarkeits-API- [#9702](https://github.com/NuGet/Home/issues/9702)

* Die Interop-API wurde hinzugefügt, um Fall Back Ordner aufzuzählen, ohne eine Projekt Mappe/Projekt [#9395](https://github.com/NuGet/Home/issues/9395)

* Hinzugefügte `latest` Option für `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

**K**

* Wenn die `DOTNET_HOST_PATH`  Umgebungsvariable nicht definiert ist, können Sie beim Starten von Plug-Ins für Anmelde Informationen in einer dotnet-CLI-Wiederherstellung die dotnet-CLI auf dem Systempfad ausprobieren. - [#7438](https://github.com/NuGet/Home/issues/7438)

* nuget.exe Spezifikation generiert ein Copyright-Tag mit einem hart codierten Text vom Copyright-yyyy anstelle von `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)

* NuGet.exe löst die Ausnahme "Autoren erforderlich" während des Pakets eines csproj aus, das Platzhalter-und AssemblyInfo-Attribute ignoriert, wenn der Assemblyname geändert wird- [#4234](https://github.com/NuGet/Home/issues/4234)

* Httprequestmessage wird mehrmals wieder verwendet, was mit sockethttphandler- [#8661](https://github.com/NuGet/Home/issues/8661) nicht unterstützt wird.

* Nuget. Indizierung 5.6.0 Preview 3 und höher verwendet einen anderen öffentlichen Schlüssel Token- [#9481](https://github.com/NuGet/Home/issues/9481)

* Beachten Sie TreatWarningsAsErrors während der Erstellung von nuget-Paketen [#7404](https://github.com/NuGet/Home/issues/7404)

* [Cpvm] Falsch skaliergrade von Paketen für mehrere P2P-Projekte- [#9549](https://github.com/NuGet/Home/issues/9549)

* Die Registerkarte "Durchsuchen" ist nicht linksbündig ausgerichtet- [#9559](https://github.com/NuGet/Home/issues/9559)

* Die installierte Version ist inkonsistent mit dem eingebetteten Symbol auf der PM-Benutzeroberfläche auf Projektmappenebene für eine Paket-ID mit installierter Version mehrerer Versionen- [#9321](https://github.com/NuGet/Home/issues/9321)

* Leck: partkreationpolicy ("anationpolicy. NonShared") nuget. solutionrestoremanager. restoreoperationlogger- [#9595](https://github.com/NuGet/Home/issues/9595)

* Vermeiden Sie das Lesen der Assets-Datei in No-op-Wiederherstellungen [#9693](https://github.com/NuGet/Home/issues/9693)

* "Nuget. Protocol" unterstützt nicht das Herunterladen der Download Anzahl einer Version aus Search- [#9086](https://github.com/NuGet/Home/issues/9086)

* Verbessern der Arbeitsspeicher Leistung von PackageMetadataResourceV3 durch Verringern der jobject-Abhängigkeiten- [#9719](https://github.com/NuGet/Home/issues/9719)

**Design Änderungsanforderungen:**

* Das Element wurde unterdrückt, `<owners>` Wenn es redundant ist- [#5134](https://github.com/NuGet/Home/issues/5134)

* Protokollieren von intervaltrackers als ETW-Ereignisse- [#9593](https://github.com/NuGet/Home/issues/9593)

* Es wurde eine Informations Meldung zur Wiederherstellung hinzugefügt, um cpvm-Benutzern mitzuteilen, dass sich das Feature in der Vorschau befindet [#9340](https://github.com/NuGet/Home/issues/9340)

* Projektmappen-Explorer transitiv Abhängigkeiten von Paketen/Projekten von der Datei "Assets" Auffüllen [#9580](https://github.com/NuGet/Home/issues/9580)

* Die Registerkarte "installierte Pakete" sollte die Paketliste nicht paginieren [#6995](https://github.com/NuGet/Home/issues/6995)

**[Liste aller Probleme, die in dieser Version behoben wurden: 5,7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**

### <a name="community-contributions"></a>Beiträge aus der Community

Vielen Dank für alle Mitwirkenden, die dazu beigetragen haben, dass diese nuget-Version großartig ist!

|Wer|PRS|Issues|
|----|----|----|
|[Groß-und-her](https://github.com/campersau)|[3433](https://github.com/NuGet/NuGet.Client/pull/3433), [3120](https://github.com/NuGet/NuGet.Client/pull/3120)|"Nuget. Protocol" unterstützt nicht das Herunterladen der Download Anzahl einer Version aus Search- [#9086](https://github.com/NuGet/Home/issues/9086) </br>Httprequestmessage wird mehrmals wieder verwendet, was mit sockethttphandler- [#8661](https://github.com/NuGet/Home/issues/8661) nicht unterstützt wird.|
|[Joseph Musser (jnm2)](https://github.com/jnm2)|[3241](https://github.com/NuGet/NuGet.Client/pull/3241)|Das Element wurde unterdrückt, `<owners>` Wenn es redundant ist- [#5134](https://github.com/NuGet/Home/issues/5134)|
|[Volodymyr shkolka (blackgad)](https://github.com/BlackGad)|[3273](https://github.com/NuGet/NuGet.Client/pull/3273)|Nuget kann nicht aus HTTPS-Quellen wieder hergestellt werden, für die Client Zertifikate erforderlich sind [#5773](https://github.com/NuGet/Home/issues/5773)|
|[Marius Ungureanu (therzok)](https://github.com/Therzok)|[3357](https://github.com/NuGet/NuGet.Client/pull/3357)|Httpsourceauthenticationhandler SemaphoreSlim zukünftiges Nachweis- [#9463](https://github.com/NuGet/Home/issues/9463)|
|[Sunner (sunnjek)](https://github.com/SuNNjek)|[3088](https://github.com/NuGet/NuGet.Client/pull/3088)|nuget.exe Spezifikation generiert ein Copyright-Tag mit einem hart codierten Text vom Copyright-yyyy anstelle von `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)|
|[Olivier Spinelli (Olivier-Spinelli)](https://github.com/olivier-spinelli)|[3335](https://github.com/NuGet/NuGet.Client/pull/3335)|Wenn die `DOTNET_HOST_PATH`  Umgebungsvariable nicht definiert ist, können Sie beim Starten von Plug-Ins für Anmelde Informationen in einer dotnet-CLI-Wiederherstellung die dotnet-CLI auf dem Systempfad ausprobieren. - [#7438](https://github.com/NuGet/Home/issues/7438)|
|[goyzhang](https://github.com/goyzhang)|[3370](https://github.com/NuGet/NuGet.Client/pull/3370)|Hinzugefügte `latest` Option für `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)|
