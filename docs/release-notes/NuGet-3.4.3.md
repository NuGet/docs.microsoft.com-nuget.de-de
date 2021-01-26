---
title: Nuget 3.4.3 Anmerkungen zu dieser Version
description: Anmerkungen zu dieser Version von nuget 3.4.3 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776471"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="29ef7-103">Nuget 3.4.3 Anmerkungen zu dieser Version</span><span class="sxs-lookup"><span data-stu-id="29ef7-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="29ef7-104">[Nuget 3.4.2 Anmerkungen](../release-notes/nuget-3.4.2.md)  |  zu dieser Version [Nuget 3.4.4 Anmerkungen](../release-notes/nuget-3.4.4.md) zu dieser Version</span><span class="sxs-lookup"><span data-stu-id="29ef7-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="29ef7-105">Nuget 3.4.3 wurde am 22. April 2016 veröffentlicht, um verschiedene Probleme zu beheben, die in den 3,4 und nachfolgenden Releases identifiziert wurden.</span><span class="sxs-lookup"><span data-stu-id="29ef7-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="29ef7-106">Sie können die vsix-Datei und die-nuget.exe [hier](https://dist.nuget.org/index.html)herunterladen.</span><span class="sxs-lookup"><span data-stu-id="29ef7-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="29ef7-107">Updates und Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="29ef7-107">Updates and Improvements</span></span>

* <span data-ttu-id="29ef7-108">Verbesserte Visual Studio-Zuverlässigkeit.</span><span class="sxs-lookup"><span data-stu-id="29ef7-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="29ef7-109">Wir haben einige Probleme in nuget behoben, die Abstürze in Visual Studio verursacht haben.</span><span class="sxs-lookup"><span data-stu-id="29ef7-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="29ef7-110">Fehlerbehebungen</span><span class="sxs-lookup"><span data-stu-id="29ef7-110">Fixes</span></span>

* <span data-ttu-id="29ef7-111">Einige Autorisierungs Probleme wurden durch Kenn Wort geschützte private nuget-Feeds behoben.</span><span class="sxs-lookup"><span data-stu-id="29ef7-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="29ef7-112">Es wurde ein Problem behoben, das die Verwendung von PCL aus `project.json` mit angegebenen Laufzeiten nicht wiederherstellen konnte.</span><span class="sxs-lookup"><span data-stu-id="29ef7-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="29ef7-113">Einige Kunden haben bei der Installation von Paketen zeitweilig auftretende Fehler fest.</span><span class="sxs-lookup"><span data-stu-id="29ef7-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="29ef7-114">Dies wurde nun in dieser Version behoben.</span><span class="sxs-lookup"><span data-stu-id="29ef7-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="29ef7-115">Es wurde ein Problem behoben, das Wiederherstellungs Fehler in C++/CLI-Projekten mit verursacht hat `project.json` .</span><span class="sxs-lookup"><span data-stu-id="29ef7-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="29ef7-116">Einige Pakete (z. b. modernhttpclient), in denen Sie nicht ordnungsgemäß entpackt werden, wenn Sie nuget in Mono verwenden.</span><span class="sxs-lookup"><span data-stu-id="29ef7-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="29ef7-117">Dies wurde nun in dieser Version behoben.</span><span class="sxs-lookup"><span data-stu-id="29ef7-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="29ef7-118">Eine umfassende Liste der Fehlerbehebungen und Verbesserungen in dieser Version finden Sie in der Liste [der Probleme.](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="29ef7-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>