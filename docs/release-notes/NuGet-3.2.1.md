---
title: Anmerkungen zu dieser Version von nuget 3.2.1
description: Anmerkungen zu dieser Version von nuget 3.2.1 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776523"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="05302-103">Anmerkungen zu dieser Version von nuget 3.2.1</span><span class="sxs-lookup"><span data-stu-id="05302-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="05302-104">Anmerkungen zu dieser [Version von nuget 3,2](../release-notes/nuget-3.2.md)  |  [Anmerkungen zu dieser Version von nuget 3,3](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="05302-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="05302-105">Nuget 3.2.1 für die Befehlszeile wurde am 12. Oktober 2015 mit einigen Optimierungen und Korrekturen für die 3,2-Version veröffentlicht und ist über [Dist.nuget.org](http://dist.nuget.org/index.html)verfügbar.</span><span class="sxs-lookup"><span data-stu-id="05302-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="05302-106">Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="05302-106">Improvements</span></span>

* <span data-ttu-id="05302-107">Nuget verwendet nun die Konfigurationsdatei mit der ursprünglichen Schreibweise von `NuGet.Config` .</span><span class="sxs-lookup"><span data-stu-id="05302-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="05302-108">Dies ist bei Betriebs [1427](https://github.com/NuGet/Home/issues/1427) Systemen mit Unterscheidung nach Groß-/Kleinschreibung wichtig</span><span class="sxs-lookup"><span data-stu-id="05302-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="05302-109">Die nuget-Wiederherstellung ignoriert nun DNX-Projekte ( `*.xproj` ), die mit `dnu` [1227](https://github.com/NuGet/Home/issues/1227) verarbeitet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="05302-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="05302-110">Optimierte Netzwerk Auslastung bei der Arbeit mit `index.json` und Paket Registrierungsdaten [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="05302-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="05302-111">Verbesserte Behandlung von Ressourcen Downloads, um mit den V2-Diensten [1448](https://github.com/NuGet/Home/issues/1448) robuster zu sein</span><span class="sxs-lookup"><span data-stu-id="05302-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="05302-112">Fehlerbehebungen</span><span class="sxs-lookup"><span data-stu-id="05302-112">Fixes</span></span>

* <span data-ttu-id="05302-113">Aktualisieren von nuget-Updates ordnungsgemäß, `.csproj` / `.vcxproj` Verweise [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="05302-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="05302-114">Nun wird verhindert, dass ein lokaler nuget-Ordner erstellt wird, wenn "SpecialFolders. USERPROFILE" nicht gefunden werden kann [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="05302-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="05302-115">Verbesserte Behandlung von Paketen im lokalen Cache, die während Download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157) beschädigt sind</span><span class="sxs-lookup"><span data-stu-id="05302-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="05302-116">Eine umfassende Liste der Probleme, die für die Befehlszeile und die Visual Studio-Erweiterung behoben wurden, finden Sie im nuget GitHub [3.2.1-Meilenstein](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed) .</span><span class="sxs-lookup"><span data-stu-id="05302-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="05302-117">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="05302-117">Known Issues</span></span>

<span data-ttu-id="05302-118">Wir verfolgen weiterhin Probleme in unserer GitHub-Liste mit Problemen, die unter folgenden Themen zu finden sind: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="05302-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>