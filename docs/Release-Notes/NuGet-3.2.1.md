---
title: Anmerkungen zur Version des NuGet-3.2.1 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 3.2.1 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-3.2.1 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7c9c2457c33eb3630f632c98bf0cf96703c3a548
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="ae25f-104">Anmerkungen zur Version von NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="ae25f-104">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="ae25f-105">[Anmerkungen zur Version des NuGet-3.2](../release-notes/nuget-3.2.md) | [NuGet 3.3-Versionshinweise](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="ae25f-105">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="ae25f-106">NuGet 3.2.1 für die Befehlszeile am 12. Oktober 2015 veröffentlicht wurde, eine Handvoll Optimierungen und Fehlerbehebungen für die Version 3.2 und steht über [dist.nuget.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="ae25f-106">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="ae25f-107">Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="ae25f-107">Improvements</span></span>

* <span data-ttu-id="ae25f-108">NuGet verwendet nun die Konfigurationsdatei mit dem ursprünglichen Groß-/Kleinschreibung von `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="ae25f-108">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="ae25f-109">Dies ist wichtig, auf die Groß-/Kleinschreibung Betriebssysteme [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="ae25f-109">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="ae25f-110">Wiederherstellen von NuGet ignoriert nun Dnx-Projekten (`*.xproj`), die verarbeitet werden soll, mit `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="ae25f-110">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="ae25f-111">Netzwerkauslastung optimiert, bei der Arbeit mit `index.json` und Packen Sie die Registrierungsdaten [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="ae25f-111">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="ae25f-112">Verbesserte Ressource Download behandeln, damit eine robustere mit v2-Diensten werden [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="ae25f-112">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="ae25f-113">Fehlerbehebungen</span><span class="sxs-lookup"><span data-stu-id="ae25f-113">Fixes</span></span>

* <span data-ttu-id="ae25f-114">NuGet-Update ordnungsgemäß aktualisiert `.csproj` / `.vcxproj` Verweise [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="ae25f-114">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="ae25f-115">Jetzt verhindert, dass ein Ordner "Lokaler .nuget" erstellt werden, wenn eine SpecialFolders.UserProfile kann nicht gefunden werden [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="ae25f-115">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="ae25f-116">Verbesserte Behandlung von Paketen im lokalen Cache, die während des Herunterladens beschädigt sind [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="ae25f-116">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="ae25f-117">Eine vollständige Liste der Probleme für die Befehlszeile und Visual Studio-Erweiterung Sie in der NuGet-GitHub finden [3.2.1 Meilenstein](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="ae25f-117">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="ae25f-118">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="ae25f-118">Known Issues</span></span>

<span data-ttu-id="ae25f-119">Wir weiterhin Probleme auf unserer GitHub-Problemliste zu verfolgen, die sich am befinden: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="ae25f-119">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>