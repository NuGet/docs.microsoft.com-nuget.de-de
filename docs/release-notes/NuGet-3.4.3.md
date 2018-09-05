---
title: Anmerkungen zu NuGet 3.4.3
description: Anmerkungen zu dieser Version für die Einbindung von NuGet 3.4.3 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549164"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="f09ba-103">Anmerkungen zu NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="f09ba-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="f09ba-104">[Anmerkungen zu NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [Anmerkungen zu NuGet 3.4.4](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="f09ba-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="f09ba-105">NuGet 3.4.3 wurde veröffentlicht, auf dem 22. April 2016, mehrere Probleme zu beheben, die in den Versionen 3.4 und nachfolgende identifiziert wurden.</span><span class="sxs-lookup"><span data-stu-id="f09ba-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="f09ba-106">Sie können sowohl VSIX-als auch nuget.exe [hier](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="f09ba-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="f09ba-107">Updates und Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="f09ba-107">Updates and Improvements</span></span>

* <span data-ttu-id="f09ba-108">Verbesserte Zuverlässigkeit von Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f09ba-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="f09ba-109">Wir haben einige Probleme in NuGet behoben, die Visual Studio Abstürze verursacht haben.</span><span class="sxs-lookup"><span data-stu-id="f09ba-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="f09ba-110">Fehlerbehebungen</span><span class="sxs-lookup"><span data-stu-id="f09ba-110">Fixes</span></span>

* <span data-ttu-id="f09ba-111">Einige Autorisierungsprobleme behoben mit Kennwortgeschützte private Nuget Feeds.</span><span class="sxs-lookup"><span data-stu-id="f09ba-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="f09ba-112">Korrigiert: rund um die nicht auf die PCL von wiederherstellen `project.json` mit Laufzeiten angegeben.</span><span class="sxs-lookup"><span data-stu-id="f09ba-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="f09ba-113">Beim Installieren von Paketen, wurden einige Kunden in kann auch zeitweilige Ausfälle ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="f09ba-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="f09ba-114">Dies wurde jetzt in dieser Version behoben.</span><span class="sxs-lookup"><span data-stu-id="f09ba-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="f09ba-115">Ein Problem wurde behoben, die aufgrund von Fehlern bei der datenbankwiederherstellung in C++ / CLI-Projekte mit `project.json`.</span><span class="sxs-lookup"><span data-stu-id="f09ba-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="f09ba-116">Einige Pakete (z. B. ModernHttpClient), in denen nicht ordnungsgemäß entpackt bei Verwendung von Nuget in Mono.</span><span class="sxs-lookup"><span data-stu-id="f09ba-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="f09ba-117">Dies wurde jetzt in dieser Version behoben.</span><span class="sxs-lookup"><span data-stu-id="f09ba-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="f09ba-118">Die vollständige Liste der Korrekturen und Verbesserungen in dieser Version, sehen Sie sich die Liste der Probleme [hier](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="f09ba-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>