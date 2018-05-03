---
title: Anmerkungen zur Version von NuGet 3.4.4
description: Versionshinweise für NuGet 3.4.4 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 891d5c7ee884d31f405118739b57a169b9cd93b3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="e8525-103">Anmerkungen zur Version von NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="e8525-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="e8525-104">[Anmerkungen zur Version des NuGet-3.4.3](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 Beta-Versionshinweise](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="e8525-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="e8525-105">Der Schwerpunkt dieser Version wurde verbessert die Qualität der 3.4.3-Versionen nuget.exe mit wenigen Korrekturen, die Visual Studio-Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="e8525-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="e8525-106">Sie können sowohl VSIX-als auch nuget.exe herunterladen [hier](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="e8525-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="e8525-107">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="e8525-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="e8525-108">Vollständige Änderungsprotokoll</span><span class="sxs-lookup"><span data-stu-id="e8525-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="e8525-109">Liste der Probleme</span><span class="sxs-lookup"><span data-stu-id="e8525-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="e8525-110">Änderungen</span><span class="sxs-lookup"><span data-stu-id="e8525-110">Changes</span></span>

- <span data-ttu-id="e8525-111">Pack-Verbesserungen: Verbesserungen zum Packen von Symbolen mit Packen `project.json` und weitere [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="e8525-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="e8525-112">Ausnahme angezeigt wird, wenn Fehler beim Suchen von Projekten in der Update-Befehl [\#605] ()https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="e8525-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="e8525-113">Eingabe Pakettyp auslesen `.nuspec` und `project.json` beim Packen [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="e8525-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="e8525-114">Stellen Sie NuGet.Shared nicht in einem Projekt.</span><span class="sxs-lookup"><span data-stu-id="e8525-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="e8525-115">\#602</span><span class="sxs-lookup"><span data-stu-id="e8525-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="e8525-116">Verwenden Sie das Push-Timeout als das HTTP-Antwort-Timeout [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="e8525-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="e8525-117">Paketdateien mit zukünftigen Uhrzeiten keine sich die Zeiten verwendet [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="e8525-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="e8525-118">Aktualisieren von `NuGet.Core.dll` Version 2.12.0 XML-Problems [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="e8525-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="e8525-119">./NuGet.CommandLine.XPlat - V unterstützt \<Ausführlichkeit\> \<Modus\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="e8525-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="e8525-120">Anzeige Fehler wiederherstellen, ohne `project.json` oder `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="e8525-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="e8525-121">Abhängigkeit Versionen behoben, wenn sich die erforderliche Versionen unterscheiden [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="e8525-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>