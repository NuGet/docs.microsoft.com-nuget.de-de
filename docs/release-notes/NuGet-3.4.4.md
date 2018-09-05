---
title: Anmerkungen zu NuGet 3.4.4
description: Anmerkungen zu dieser Version für die Einbindung von NuGet 3.4.4 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 44a9f21c61f0552fdc21aab24f48eee993654b01
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547472"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="e3693-103">Anmerkungen zu NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="e3693-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="e3693-104">[Anmerkungen zu NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [Anmerkungen zu NuGet 3.5-Beta](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="e3693-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="e3693-105">Der primäre Fokus von dieser Version wurde die Verbesserungen bei der die Qualität der 3.4.3 Version von nuget.exe einige Behebungen an sowie die Visual Studio-Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="e3693-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="e3693-106">Sie können sowohl VSIX-als auch nuget.exe [hier](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="e3693-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="e3693-107">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="e3693-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="e3693-108">Vollständigen Änderungsprotokoll</span><span class="sxs-lookup"><span data-stu-id="e3693-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="e3693-109">Liste der Probleme</span><span class="sxs-lookup"><span data-stu-id="e3693-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="e3693-110">Änderungen</span><span class="sxs-lookup"><span data-stu-id="e3693-110">Changes</span></span>

- <span data-ttu-id="e3693-111">Pack-Verbesserungen: Verbesserungen bei der das Verpacken der Symbole, Packen mit `project.json` mehr [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="e3693-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="e3693-112">Ausnahme angezeigt wird, wenn Fehler beim Suchen von Projekten in der Update-Befehl [\#605](https://github.com/NuGet/NuGet.Client/pull/605)</span><span class="sxs-lookup"><span data-stu-id="e3693-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="e3693-113">Pakettyp aus dem Eingabedatenstrom gelesenen `.nuspec` und `project.json` beim Packen [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="e3693-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="e3693-114">Stellen Sie NuGet.Shared nicht in einem Projekt.</span><span class="sxs-lookup"><span data-stu-id="e3693-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="e3693-115">\#602</span><span class="sxs-lookup"><span data-stu-id="e3693-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="e3693-116">Verwenden Sie das Push-Timeout als das Timeout der HTTP-Antwort [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="e3693-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="e3693-117">Paketdateien mit zukünftigen Zeiten haben sich die Zeiten verwendet keinen [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="e3693-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="e3693-118">Aktualisieren von `NuGet.Core.dll` Version 2.12.0 um XML-Problem zu beheben [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="e3693-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="e3693-119">./NuGet.CommandLine.XPlat - V unterstützt \<Ausführlichkeit\> \<Modus\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="e3693-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="e3693-120">Anzeigen der Fehler beim Wiederherstellen ohne `project.json` oder `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="e3693-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="e3693-121">Beheben von abhängigkeitsversionen, wenn sich die erforderliche Versionen unterscheiden [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="e3693-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>