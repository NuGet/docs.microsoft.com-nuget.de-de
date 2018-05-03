---
title: Anmerkungen zur Version von NuGet 3.4.3
description: Versionshinweise für NuGet 3.4.3 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6c25d3b678e6e72eca3e1157f91a75bfa8cbb18e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="219f8-103">Anmerkungen zur Version von NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="219f8-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="219f8-104">[Anmerkungen zur Version des NuGet-3.4.2](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4-Versionshinweise](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="219f8-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="219f8-105">NuGet 3.4.3 wurde freigegeben, 22 April 2016 verschiedene Probleme, die in den Versionen 3.4 und nachfolgende identifiziert wurden.</span><span class="sxs-lookup"><span data-stu-id="219f8-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="219f8-106">Sie können sowohl VSIX-als auch nuget.exe herunterladen [hier](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="219f8-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="219f8-107">Updates und Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="219f8-107">Updates and Improvements</span></span>

* <span data-ttu-id="219f8-108">Verbesserter Zuverlässigkeit für Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="219f8-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="219f8-109">Wir haben einige Probleme im NuGet behoben, die in Visual Studio abstürzen verursacht hat.</span><span class="sxs-lookup"><span data-stu-id="219f8-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="219f8-110">Fehlerbehebungen</span><span class="sxs-lookup"><span data-stu-id="219f8-110">Fixes</span></span>

* <span data-ttu-id="219f8-111">Einige Probleme der Autorisierung behoben mit Nuget, private kennwortgeschützt Feeds.</span><span class="sxs-lookup"><span data-stu-id="219f8-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="219f8-112">Es wurde ein Problem, um nicht auf PCL aus wiederherstellen `project.json` mit Laufzeiten angegeben.</span><span class="sxs-lookup"><span data-stu-id="219f8-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="219f8-113">Einige Kunden ausgeführt wurden in sind zwischenzeitliche Fehler die, wenn Sie Pakete installieren.</span><span class="sxs-lookup"><span data-stu-id="219f8-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="219f8-114">Dies wurde jetzt in dieser Version behoben.</span><span class="sxs-lookup"><span data-stu-id="219f8-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="219f8-115">Es wurde ein Problem, die in C + Wiederherstellung Fehler verursacht hat c++ / CLI-Projekten mit `project.json`.</span><span class="sxs-lookup"><span data-stu-id="219f8-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="219f8-116">Einige Pakete (z. B. ModernHttpClient), in denen nicht ordnungsgemäß entzippt Wenn Sie Nuget in Mono verwenden.</span><span class="sxs-lookup"><span data-stu-id="219f8-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="219f8-117">Dies wurde jetzt in dieser Version behoben.</span><span class="sxs-lookup"><span data-stu-id="219f8-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="219f8-118">Die vollständige Liste der Korrekturen und Verbesserungen in dieser Version, sehen Sie sich die Liste der Probleme [hier](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="219f8-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>