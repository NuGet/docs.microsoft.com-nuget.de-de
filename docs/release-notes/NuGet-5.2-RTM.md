---
title: Anmerkungen zu dieser Version von nuget 5,2 RTM
description: Anmerkungen zu dieser Version von nuget 5,2, einschließlich neuer Features, Fehlerbehebungen und dcrs.
author: karann-msft
ms.author: karann
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: f94bd8ddb8fac8bf47c2826bf5b417595b0efa8b
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471183"
---
# <a name="nuget-52-release-notes"></a><span data-ttu-id="f2c9d-103">Anmerkungen zu dieser Version von nuget 5,2</span><span class="sxs-lookup"><span data-stu-id="f2c9d-103">NuGet 5.2 Release Notes</span></span>

<span data-ttu-id="f2c9d-104">Möglichkeiten der NuGet-Verteilung:</span><span class="sxs-lookup"><span data-stu-id="f2c9d-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="f2c9d-105">NuGet-Version</span><span class="sxs-lookup"><span data-stu-id="f2c9d-105">NuGet version</span></span> | <span data-ttu-id="f2c9d-106">Verfügbar in der Visual Studio-Version</span><span class="sxs-lookup"><span data-stu-id="f2c9d-106">Available in Visual Studio version</span></span>| <span data-ttu-id="f2c9d-107">Verfügbar in .NET SDK(s)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="f2c9d-108">**verweisen**</span><span class="sxs-lookup"><span data-stu-id="f2c9d-108">**5.2.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="f2c9d-109">Visual Studio 2019, Version 16,2</span><span class="sxs-lookup"><span data-stu-id="f2c9d-109">Visual Studio 2019 version 16.2</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="f2c9d-110">[2.1.80 X](https://dotnet.microsoft.com/download/dotnet-core/2.1) <sup>1</sup>, [2.2.40 X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="f2c9d-110">[2.1.80X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="f2c9d-111"><sup>1</sup> Installiert mit Visual Studio 2019 mit .net Core-Arbeitsauslastung</span><span class="sxs-lookup"><span data-stu-id="f2c9d-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="f2c9d-112"><sup>2</sup> Verfügbar als optionale Installation mit Visual Studio 2019 mit .net Core-Arbeitsauslastung</span><span class="sxs-lookup"><span data-stu-id="f2c9d-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-52"></a><span data-ttu-id="f2c9d-113">Zusammenfassung: Neuerungen in 5,2</span><span class="sxs-lookup"><span data-stu-id="f2c9d-113">Summary: What's New in 5.2</span></span>

* <span data-ttu-id="f2c9d-114">Es wurde ein kritischer Fehler behoben, der gelegentlich zu Fehlern beim nuget-Vorgang aufgrund von Pfad Problemen auf Linux-& Mac- [#7341](https://github.com/NuGet/Home/issues/7341)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-114">Fixed a critical bug that caused occasional NuGet operation failures due to path issues on Linux & Mac - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

* <span data-ttu-id="f2c9d-115">Verbesserte Reaktionsfähigkeit der Benutzeroberfläche beim Durchsuchen von Paketen mithilfe der Benutzeroberfläche des nuget-Paket-Managers in Visual Studio besonders bemerkbar für langsame Quellen [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-115">Improved UI responsiveness when browsing packages using the NuGet package manager UI in Visual Studio especially noticeable for slow sources - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="f2c9d-116">Fehlerbehebungen für Fehlerbehebungen für Sperrdateien ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) und das Authentifizierungs-Plug-in ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))</span><span class="sxs-lookup"><span data-stu-id="f2c9d-116">Tons of reliability fixes for lock file ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) and authentication plugin ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="f2c9d-117">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="f2c9d-117">Issues fixed in this release</span></span>

<span data-ttu-id="f2c9d-118">**Fehler**</span><span class="sxs-lookup"><span data-stu-id="f2c9d-118">**Bugs**</span></span>

* <span data-ttu-id="f2c9d-119">Leistungs Paket-Manager-Konsole:  UI-Verzögerungs Aktualisierung "Standard Projekt" Kombinations Feld "Standard Projekt" ausgewählter Wert- [#8235](https://github.com/NuGet/Home/issues/8235)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-119">Perf: Package Manager Console:  UI delay updating "Default project" combobox selected value - [#8235](https://github.com/NuGet/Home/issues/8235)</span></span>

* <span data-ttu-id="f2c9d-120">Leistungs Leistungsverbesserungen in der PM-Benutzeroberfläche- [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-120">Perf: Performance improvements in the PM UI - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="f2c9d-121">Leistungs UI-Verzögerung beim Lesen des Standard Projekts in der PMC- [#6824](https://github.com/NuGet/Home/issues/6824)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-121">Perf: UI Delay when reading Default Project in PMC - [#6824](https://github.com/NuGet/Home/issues/6824)</span></span>

* <span data-ttu-id="f2c9d-122">Perf: [vsfeedback] Registerkarte "nuget-Update" friert für eine lokale Paketquelle ein [#6470](https://github.com/NuGet/Home/issues/6470)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-122">Perf: [vsfeedback] NuGet Update tab freezes for a local package source - [#6470](https://github.com/NuGet/Home/issues/6470)</span></span>

* <span data-ttu-id="f2c9d-123">Plugins  Nuget wartet das vollständige Handshake-Timeout, wenn das Plug-in nicht gestartet oder vorzeitig beendet wird [#8300](https://github.com/NuGet/Home/issues/8300)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-123">Plugins:  NuGet waits full handshake timeout if plugin fails to launch or terminates early - [#8300](https://github.com/NuGet/Home/issues/8300)</span></span>

* <span data-ttu-id="f2c9d-124">Plug-ins: verbessern der Diagnosemöglichkeiten für Plug-in-Starts- [#8271](https://github.com/NuGet/Home/issues/8271)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-124">Plugins:  improve diagnosability of plugin launch failure - [#8271](https://github.com/NuGet/Home/issues/8271)</span></span>

* <span data-ttu-id="f2c9d-125">Plugins Problem mit der nuget. exe-Ermittlung von integrierten Plug-Ins [#8269](https://github.com/NuGet/Home/issues/8269)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-125">Plugins: Issue with nuget.exe discovery of built in plugins - [#8269](https://github.com/NuGet/Home/issues/8269)</span></span>

* <span data-ttu-id="f2c9d-126">Plug-ins: die Cachedatei wird nie gelesen [#8210](https://github.com/NuGet/Home/issues/8210)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-126">Plugins:  cache file is never read - [#8210](https://github.com/NuGet/Home/issues/8210)</span></span>

* <span data-ttu-id="f2c9d-127">Plugins  "Eine Aufgabe wurde abgebrochen."</span><span class="sxs-lookup"><span data-stu-id="f2c9d-127">Plugins:  "A task was canceled."</span></span> <span data-ttu-id="f2c9d-128">Fehler mit Authentifizierungs-Plug-in während der Wiederherstellung [#8198](https://github.com/NuGet/Home/issues/8198)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-128">errors with authentication plugin during restore - [#8198](https://github.com/NuGet/Home/issues/8198)</span></span>

* <span data-ttu-id="f2c9d-129">Der Plug-in-Cache kann auf Linux-Plattformen nicht zeitweise erkannt werden [#7845](https://github.com/NuGet/Home/issues/7845)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-129">Plugins cache not discoverable intermittently on linux platforms - [#7845](https://github.com/NuGet/Home/issues/7845)</span></span>

* <span data-ttu-id="f2c9d-130">Lockfile: bei ATF hat der Wert false NU1004 aufgrund einer ungültigen Überprüfung des Framework-Gleichheits- [#8187](https://github.com/NuGet/Home/issues/8187)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-130">LockFile: with ATF, it has false NU1004 due to a bad target framework equality check - [#8187](https://github.com/NuGet/Home/issues/8187)</span></span>

* <span data-ttu-id="f2c9d-131">Lockfile: das Wiederherstellungs Flag "--Locked-Mode" wird nicht berücksichtigt, wenn die Sperrdatei leer oder falsch formatiert ist [#8160](https://github.com/NuGet/Home/issues/8160)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-131">LockFile: '--locked-mode' restore flag not respected if lock file is empty or malformed - [#8160](https://github.com/NuGet/Home/issues/8160)</span></span>

* <span data-ttu-id="f2c9d-132">Lockfile: Projekte mit benutzerdefinierten Assemblynamen in Paketen Sperrdatei nicht in Kleinbuchstaben [#8114](https://github.com/NuGet/Home/issues/8114)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-132">LockFile: Don't lowercase projects with custom assembly names in packages lock file - [#8114](https://github.com/NuGet/Home/issues/8114)</span></span>

* <span data-ttu-id="f2c9d-133">Lockfile: Projekt Verweis als Kleinbuchstaben in Sperrdatei erstellen- [#7840](https://github.com/NuGet/Home/issues/7840)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-133">LockFile: Make project reference lower case in lock file  - [#7840](https://github.com/NuGet/Home/issues/7840)</span></span>

* <span data-ttu-id="f2c9d-134">Wiederherstellung: das Installieren eines manipuliert signierten Pakets führt zu mehreren fehlgeschlagenen Installations versuchen (mit wiederholter Ausgabe)- [#8175](https://github.com/NuGet/Home/issues/8175)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-134">Restore:  installing a tampered signed package results in multiple failed install attempts (with repeated output) - [#8175](https://github.com/NuGet/Home/issues/8175)</span></span>

* <span data-ttu-id="f2c9d-135">VS: die Benutzeroptionen für die Lösung können nach dem nuget-Update- [#8166](https://github.com/NuGet/Home/issues/8166) nicht deserialisiert werden.</span><span class="sxs-lookup"><span data-stu-id="f2c9d-135">VS: solution user options fail to deserialize after NuGet update - [#8166](https://github.com/NuGet/Home/issues/8166)</span></span>

* <span data-ttu-id="f2c9d-136">DotNet-List-Package in einem UnitTest-Projekt gibt einen Fehler zurück [#8154](https://github.com/NuGet/Home/issues/8154)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-136">dotnet-list-package in a UnitTest project returns an error - [#8154](https://github.com/NuGet/Home/issues/8154)</span></span>

* <span data-ttu-id="f2c9d-137">Nuget-Paketgruppe für vs-Installer erstellen: beheben einiger VSIX-Setup Probleme- [#8033](https://github.com/NuGet/Home/issues/8033)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-137">Create NuGet package group for VS installer - fixing some VSIX setup problems - [#8033](https://github.com/NuGet/Home/issues/8033)</span></span>

* <span data-ttu-id="f2c9d-138">Generatepackageonbuild sollte nobuild nicht festlegen.</span><span class="sxs-lookup"><span data-stu-id="f2c9d-138">GeneratePackageOnBuild should not set NoBuild.</span></span><span data-ttu-id="f2c9d-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span></span>

* <span data-ttu-id="f2c9d-140">Die neue Option "-symbolpackageformat schnupkg" generiert einen Fehler, wenn die nuspec-Datei ein explizites assemblyverweiselement enthält [#7638](https://github.com/NuGet/Home/issues/7638)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-140">The new option "-SymbolPackageFormat snupkg" generates an error when the .nuspec file contains an explicit assembly reference element - [#7638](https://github.com/NuGet/Home/issues/7638)</span></span>

* <span data-ttu-id="f2c9d-141">NuGet.targets(498,5): error : Ein Teil des Pfads "/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341) wurde nicht gefunden.</span><span class="sxs-lookup"><span data-stu-id="f2c9d-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

<span data-ttu-id="f2c9d-142">**DCR:**</span><span class="sxs-lookup"><span data-stu-id="f2c9d-142">**DCR:**</span></span>

* <span data-ttu-id="f2c9d-143">Fügen Sie eine MSBuild-Eigenschaft hinzu, die angibt, dass packagedownload unterstützt wird: [#8106](https://github.com/NuGet/Home/issues/8106)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-143">Add an msbuild property that indicates that PackageDownload is supported - [#8106](https://github.com/NuGet/Home/issues/8106)</span></span>

* <span data-ttu-id="f2c9d-144">Frameworkreferenzierung unterdrückt den Abhängigkeits Fluss über "frameworkreferen. privateassets- [#7988](https://github.com/NuGet/Home/issues/7988)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-144">FrameworkReference suppress dependency flow via FrameworkReference.PrivateAssets - [#7988](https://github.com/NuGet/Home/issues/7988)</span></span>

* <span data-ttu-id="f2c9d-145">Mechanismus zur Bereitstellung von "Runtime. JSON" außerhalb eines Pakets [#7351](https://github.com/NuGet/Home/issues/7351)</span><span class="sxs-lookup"><span data-stu-id="f2c9d-145">Mechanism for supplying runtime.json outside of a package - [#7351](https://github.com/NuGet/Home/issues/7351)</span></span>

<span data-ttu-id="f2c9d-146">**[Liste aller in dieser Version behobene Probleme-5,2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span><span class="sxs-lookup"><span data-stu-id="f2c9d-146">**[List of all issues fixed in this release - 5.2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span></span>


