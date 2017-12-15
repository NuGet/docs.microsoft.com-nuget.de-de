---
title: Anmerkungen zur Version des NuGet-3.4.4 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6f0aa9bb-75e5-429d-9954-3cb41a909c14
description: "Versionshinweise für NuGet 3.4.4 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-3.4.4 versionsanmerkungen aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 51ddb918d2269990588e9cba4d15ffeb878de5f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="5ec1e-104">Anmerkungen zur Version von NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="5ec1e-104">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="5ec1e-105">[Anmerkungen zur Version des NuGet-3.4.3](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 Beta-Versionshinweise](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="5ec1e-105">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="5ec1e-106">Der Schwerpunkt dieser Version wurde verbessert die Qualität der 3.4.3-Versionen nuget.exe mit wenigen Korrekturen, die Visual Studio-Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="5ec1e-106">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="5ec1e-107">Sie können sowohl VSIX-als auch nuget.exe herunterladen [hier](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="5ec1e-107">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="5ec1e-108">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="5ec1e-108">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="5ec1e-109">Vollständige Änderungsprotokoll</span><span class="sxs-lookup"><span data-stu-id="5ec1e-109">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="5ec1e-110">Liste der Probleme</span><span class="sxs-lookup"><span data-stu-id="5ec1e-110">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="5ec1e-111">Änderungen</span><span class="sxs-lookup"><span data-stu-id="5ec1e-111">Changes</span></span>

- <span data-ttu-id="5ec1e-112">Pack-Verbesserungen: Verbesserungen zum Packen von Symbolen mit Packen `project.json` und weitere [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="5ec1e-112">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="5ec1e-113">Ausnahme angezeigt wird, wenn Fehler beim Suchen von Projekten in der Update-Befehl [\#605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="5ec1e-113">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="5ec1e-114">Eingabe Pakettyp auslesen `.nuspec` und `project.json` beim Packen [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="5ec1e-114">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="5ec1e-115">Stellen Sie NuGet.Shared nicht in einem Projekt.</span><span class="sxs-lookup"><span data-stu-id="5ec1e-115">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="5ec1e-116">\#602</span><span class="sxs-lookup"><span data-stu-id="5ec1e-116">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="5ec1e-117">Verwenden Sie das Push-Timeout als das HTTP-Antwort-Timeout [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="5ec1e-117">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="5ec1e-118">Paketdateien mit zukünftigen Uhrzeiten keine sich die Zeiten verwendet [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="5ec1e-118">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="5ec1e-119">Aktualisieren von `NuGet.Core.dll` Version 2.12.0 XML-Problems [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="5ec1e-119">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="5ec1e-120">./NuGet.CommandLine.XPlat - V unterstützt \<Ausführlichkeit\> \<Modus\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="5ec1e-120">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="5ec1e-121">Anzeige Fehler wiederherstellen, ohne `project.json` oder `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="5ec1e-121">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="5ec1e-122">Abhängigkeit Versionen behoben, wenn sich die erforderliche Versionen unterscheiden [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="5ec1e-122">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>