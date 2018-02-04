---
title: Anmerkungen zur Version des NuGet-3.4.3 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 3.4.3 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-3.4.3 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 68aab607659d15f96aefeab7bb90afc787710824
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="05012-104">Anmerkungen zur Version von NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="05012-104">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="05012-105">[Anmerkungen zur Version des NuGet-3.4.2](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4-Versionshinweise](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="05012-105">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="05012-106">NuGet 3.4.3 wurde freigegeben, 22 April 2016 verschiedene Probleme, die in den Versionen 3.4 und nachfolgende identifiziert wurden.</span><span class="sxs-lookup"><span data-stu-id="05012-106">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="05012-107">Sie können sowohl VSIX-als auch nuget.exe herunterladen [hier](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="05012-107">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="05012-108">Updates und Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="05012-108">Updates and Improvements</span></span>

* <span data-ttu-id="05012-109">Verbesserter Zuverlässigkeit für Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="05012-109">Improved Visual Studio reliability.</span></span> <span data-ttu-id="05012-110">Wir haben einige Probleme im NuGet behoben, die in Visual Studio abstürzen verursacht hat.</span><span class="sxs-lookup"><span data-stu-id="05012-110">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="05012-111">Fehlerbehebungen</span><span class="sxs-lookup"><span data-stu-id="05012-111">Fixes</span></span>

* <span data-ttu-id="05012-112">Einige Probleme der Autorisierung behoben mit Nuget, private kennwortgeschützt Feeds.</span><span class="sxs-lookup"><span data-stu-id="05012-112">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="05012-113">Es wurde ein Problem, um nicht auf PCL aus wiederherstellen `project.json` mit Laufzeiten angegeben.</span><span class="sxs-lookup"><span data-stu-id="05012-113">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="05012-114">Einige Kunden ausgeführt wurden in sind zwischenzeitliche Fehler die, wenn Sie Pakete installieren.</span><span class="sxs-lookup"><span data-stu-id="05012-114">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="05012-115">Dies wurde jetzt in dieser Version behoben.</span><span class="sxs-lookup"><span data-stu-id="05012-115">This has now been fixed in this release.</span></span>
* <span data-ttu-id="05012-116">Es wurde ein Problem, die in C + Wiederherstellung Fehler verursacht hat c++ / CLI-Projekten mit `project.json`.</span><span class="sxs-lookup"><span data-stu-id="05012-116">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="05012-117">Einige Pakete (z. B. ModernHttpClient), in denen nicht ordnungsgemäß entzippt Wenn Sie Nuget in Mono verwenden.</span><span class="sxs-lookup"><span data-stu-id="05012-117">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="05012-118">Dies wurde jetzt in dieser Version behoben.</span><span class="sxs-lookup"><span data-stu-id="05012-118">This has now been fixed in this release.</span></span>

<span data-ttu-id="05012-119">Die vollständige Liste der Korrekturen und Verbesserungen in dieser Version, sehen Sie sich die Liste der Probleme [hier](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="05012-119">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>