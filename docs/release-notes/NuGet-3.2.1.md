---
title: Anmerkungen zu NuGet 3.2.1
description: Anmerkungen zu dieser Version für die Einbindung von NuGet-Version 3.2.1 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548189"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="ec2d5-103">Anmerkungen zu NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="ec2d5-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="ec2d5-104">[Anmerkungen zu NuGet 3.2](../release-notes/nuget-3.2.md) | [Anmerkungen zu NuGet 3.3](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="ec2d5-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="ec2d5-105">NuGet 3.2.1 für die Befehlszeile am 12. Oktober 2015 kann durch eine Reihe von Optimierungen und Korrekturen für die 3.2-Version wurde veröffentlicht und steht über ["dist.NuGet.org"](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="ec2d5-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="ec2d5-106">Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="ec2d5-106">Improvements</span></span>

* <span data-ttu-id="ec2d5-107">NuGet verwendet nun die Konfigurationsdatei mit dem ursprünglichen Groß-/Kleinschreibung der `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="ec2d5-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="ec2d5-108">Dies ist wichtig für die Groß-/Kleinschreibung Betriebssysteme [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="ec2d5-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="ec2d5-109">NuGet-Wiederherstellung ignoriert nun Dnx-Projekte (`*.xproj`), die verarbeitet werden sollen, mit `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="ec2d5-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="ec2d5-110">Optimierung der netzwerknutzung, bei der Arbeit mit `index.json` und Packen Sie die Registrierungsdaten [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="ec2d5-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="ec2d5-111">Verbesserte Ressourcendownload mit v2-Diensten unter Umständen stabiler sind die Verarbeitung [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="ec2d5-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="ec2d5-112">Fehlerbehebungen</span><span class="sxs-lookup"><span data-stu-id="ec2d5-112">Fixes</span></span>

* <span data-ttu-id="ec2d5-113">NuGet ordnungsgemäß zur Aktualisierung der `.csproj` / `.vcxproj` Verweise [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="ec2d5-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="ec2d5-114">Jetzt verhindern, dass einen lokale .nuget-Ordner erstellt werden, wenn eine SpecialFolders.UserProfile nicht gefunden werden kann [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="ec2d5-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="ec2d5-115">Verbesserte Behandlung von Paketen im lokalen Cache, die während des Herunterladens beschädigt sind [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="ec2d5-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="ec2d5-116">Eine vollständige Liste der Probleme, die für die Befehlszeile und Visual Studio-Erweiterung Sie im NuGet GitHub finden [3.2.1 Meilenstein](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="ec2d5-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="ec2d5-117">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="ec2d5-117">Known Issues</span></span>

<span data-ttu-id="ec2d5-118">Wir fahren fort, um Probleme in der Liste unserer GitHub-Probleme nachzuverfolgen, die finden Sie unter: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="ec2d5-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>