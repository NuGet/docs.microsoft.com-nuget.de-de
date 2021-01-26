---
title: Nuget 3.4.4 Anmerkungen zu dieser Version
description: Anmerkungen zu dieser Version von nuget 3.4.4 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780230"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="3b404-103">Nuget 3.4.4 Anmerkungen zu dieser Version</span><span class="sxs-lookup"><span data-stu-id="3b404-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="3b404-104">[Nuget 3.4.3 Anmerkungen](../release-notes/nuget-3.4.3.md)  |  zu dieser Version [Anmerkungen zu dieser Version von nuget 3,5-Beta Version](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="3b404-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="3b404-105">Der Hauptschwerpunkt dieser Version bestand darin, die Qualität der 3.4.3-Version von nuget.exe mit einigen wenigen Korrekturen an der Visual Studio-Erweiterung zu verbessern.</span><span class="sxs-lookup"><span data-stu-id="3b404-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="3b404-106">Sie können die vsix-Datei und die-nuget.exe [hier](https://dist.nuget.org/index.html)herunterladen.</span><span class="sxs-lookup"><span data-stu-id="3b404-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtm-2016-05-19"></a><span data-ttu-id="3b404-107">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="3b404-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="3b404-108">Vollständiges Änderungsprotokoll</span><span class="sxs-lookup"><span data-stu-id="3b404-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="3b404-109">Liste der Probleme</span><span class="sxs-lookup"><span data-stu-id="3b404-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="3b404-110">Änderungen</span><span class="sxs-lookup"><span data-stu-id="3b404-110">Changes</span></span>

- <span data-ttu-id="3b404-111">Pack-Verbesserungen: Verbesserungen beim Packen von Symbolen, Verpacken mit `project.json` und mehr [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="3b404-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="3b404-112">Ausnahme anzeigen, wenn beim Suchen nach Projekten im Update-Befehl [605] ein Fehler auftritt. \#https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="3b404-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="3b404-113">Lesen des Pakettyps aus der Eingabe `.nuspec` und `project.json` beim Verpacken von [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="3b404-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="3b404-114">Erstellen Sie "nuget. Shared" nicht als Projekt.</span><span class="sxs-lookup"><span data-stu-id="3b404-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="3b404-115">\#602</span><span class="sxs-lookup"><span data-stu-id="3b404-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="3b404-116">Pushtimeout als HTTP-Antwort Timeout [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599) verwenden</span><span class="sxs-lookup"><span data-stu-id="3b404-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="3b404-117">Für Paketdateien mit zukünftigen Zeiten wird die Zeit nicht verwendet [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="3b404-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="3b404-118">Aktualisieren der `NuGet.Core.dll` Version auf 2.12.0, um das XML-Problem [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594) zu beheben</span><span class="sxs-lookup"><span data-stu-id="3b404-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="3b404-119">Support./NuGet.commandline.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="3b404-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="3b404-120">Fehler beim Wiederherstellen ohne `project.json` oder `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590) anzeigen</span><span class="sxs-lookup"><span data-stu-id="3b404-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="3b404-121">Beheben von Abhängigkeits Versionen, wenn die erforderlichen Versionen [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="3b404-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>