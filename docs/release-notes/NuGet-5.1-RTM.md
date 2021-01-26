---
title: Anmerkungen zu dieser Version von nuget 5,1 RTM
description: Anmerkungen zu dieser Version von nuget 5,1, einschließlich neuer Features, Fehlerbehebungen und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: d6f6bffc6b5fda9ee1b9d9830f6d7d3c0f5be654
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780138"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="adbda-103">Anmerkungen zu dieser Version von nuget 5,1</span><span class="sxs-lookup"><span data-stu-id="adbda-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="adbda-104">Möglichkeiten der NuGet-Verteilung:</span><span class="sxs-lookup"><span data-stu-id="adbda-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="adbda-105">NuGet-Version</span><span class="sxs-lookup"><span data-stu-id="adbda-105">NuGet version</span></span> | <span data-ttu-id="adbda-106">Verfügbar in der Visual Studio-Version</span><span class="sxs-lookup"><span data-stu-id="adbda-106">Available in Visual Studio version</span></span>| <span data-ttu-id="adbda-107">Verfügbar in .NET SDK(s)</span><span class="sxs-lookup"><span data-stu-id="adbda-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="adbda-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="adbda-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="adbda-109">Visual Studio 2019 Version 16.1</span><span class="sxs-lookup"><span data-stu-id="adbda-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="adbda-110">[2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="adbda-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="adbda-111"><sup>1</sup> Installiert mit Visual Studio 2019 mit .net Core-Arbeitsauslastung</span><span class="sxs-lookup"><span data-stu-id="adbda-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="adbda-112"><sup>2</sup> Verfügbar als optionale Installation mit Visual Studio 2019 mit .net Core-Arbeitsauslastung</span><span class="sxs-lookup"><span data-stu-id="adbda-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="adbda-113">Zusammenfassung: Neues in 5,1</span><span class="sxs-lookup"><span data-stu-id="adbda-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="adbda-114">Unterstützung zum Überspringen eines Package Push, wenn es bereits vorhanden ist, um eine bessere Integration in CI/CD-Workflows zu ermöglichen, [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="adbda-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="adbda-115">Visual Studio bietet nun einen bequemen Link zur nuget.org-Katalogseite des Pakets [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="adbda-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="adbda-116">Unterstützung für neue .net Core [3,0-Assets](https://github.com/dotnet/cli/issues/10007) , wie z. b. [Ziel Pakete](https://github.com/dotnet/cli/issues/10006)</span><span class="sxs-lookup"><span data-stu-id="adbda-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="adbda-117">Unterstützung für das nuget-Paket und die Wiederherstellung von frameworkreferences zum Aktivieren von Ziel-und Lauf Zeit Paketen- [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="adbda-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="adbda-118">Unterstützen des Paket Szenarios "nur herunterladen" mit packagedownload- [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="adbda-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="adbda-119">Ausschließen von Lauf Zeit-und Ziel Paketen aus Suchergebnissen & Restore Graph mithilfe von PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="adbda-119">Exclude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="adbda-120">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="adbda-120">Issues fixed in this release</span></span>

<span data-ttu-id="adbda-121">**Fehler**</span><span class="sxs-lookup"><span data-stu-id="adbda-121">**Bugs**</span></span>

* <span data-ttu-id="adbda-122">Plug-ins: Ausnahme Details bei der Erstellung des Plug-ins verloren [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="adbda-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="adbda-123">Der packagereferenzierungsbereich mit exklusiver niedrigerer Grenze funktioniert nicht, wenn die untere Grenze in einer der Quellen vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="adbda-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="adbda-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="adbda-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="adbda-125">Verbessern der ispackablefalseerror-Meldung- [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="adbda-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="adbda-126">Paket Sperrdatei-Datei bei Änderung des Projekt Diagramms neu generieren- [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="adbda-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="adbda-127">Projectsystem-Bug: nuget-Pakete werden automatisch entfernt- [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="adbda-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="adbda-128">Fügen Sie ein Ziel für die Rückgabe der frameworkreferenzierung hinzu, ähnlich wie collectpackagedownloads und collectpackagereferences- [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="adbda-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="adbda-129">HTTP-Cache: RepositoryResources Resource wird nicht in einer versionierten Weise zwischengespeichert- [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="adbda-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="adbda-130">Protokollierung: Ausnahme Aufruf Stapel werden nicht mit ausführlicherer Ausführlichkeit gemeldet [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="adbda-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="adbda-131">Alle URLs für nuget-Dokumente für die Verwendung von HTTPS- [#7950](https://github.com/NuGet/Home/issues/7950) ändern</span><span class="sxs-lookup"><span data-stu-id="adbda-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="adbda-132">Verbessern der NU3024-Warnmeldung- [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="adbda-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="adbda-133">Sperrdatei wird nicht aktualisiert, wenn packagereferenzierung entfernt- [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="adbda-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="adbda-134">Verbessern der Fehlerfall Behandlung beim Validieren von licenserver URL und License-Element in nuspec- [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="adbda-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="adbda-135">PM-Benutzeroberfläche: Klicken Sie mit der rechten Maustaste auf die Registerkarten Kopfzeile, und klicken Sie auf "Datei Speicherort öffnen [#7913](https://github.com/NuGet/Home/issues/7913) "</span><span class="sxs-lookup"><span data-stu-id="adbda-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="adbda-136">Plug-ins: protokollieren beim Beenden des Plug-Ins [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="adbda-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="adbda-137">Plug-ins: hohe Kollisionsrate bei der Protokollierung von DateTime-Werten- [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="adbda-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="adbda-138">Manifest. Read from schlägt für beliebige nuspec-Ausdrücke mit licen\*- [#7894](https://github.com/NuGet/Home/issues/7894) fehl.</span><span class="sxs-lookup"><span data-stu-id="adbda-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="adbda-139">Restorelockedmode: Unerwartetes NU1004, wenn projectreferenauf ein Projekt mit benutzerdefiniertem AssemblyName- [#7889](https://github.com/NuGet/Home/issues/7889) verweist</span><span class="sxs-lookup"><span data-stu-id="adbda-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="adbda-140">Bessere Fehlermeldung, wenn der Plug-in-Start mit einer Ausnahme fehlschlägt [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="adbda-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="adbda-141">Vermeiden Sie bei einer NOOP-Wiederherstellung \* .dgspec.jsim Verzeichnis "obj", [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="adbda-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="adbda-142">Generatepathproperty = true generiert keine Eigenschaft für die Groß-/Kleinschreibung [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="adbda-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="adbda-143">Einstellungen: unzulässiges Zeichen im Paket Quell Pfad können abstürzen im vs- [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="adbda-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="adbda-144">Wenn die Sperrdatei gelöscht wird, generiert Restore keine Sperrdatei auf NOOP- [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="adbda-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="adbda-145">Lizenz-URL und-Lizenz verursacht Lesefehler mit Metadaten- [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="adbda-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="adbda-146">Nicht behandelte Ausnahmen in V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="adbda-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="adbda-147">nuget.exe gibt den Exitcode NULL für ungültige Argumente zurück [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="adbda-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="adbda-148">Aktualisieren von Fehlern und Warnungs Dokumenten, um Signierungs bezogene Szenarios widerzuspiegeln [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="adbda-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="adbda-149">In der Ressourcen Datei sollten relative Pfade verwendet werden, um das Verschieben von Projekten leichter zu ermöglichen [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="adbda-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="adbda-150">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="adbda-150">**DCRs**</span></span>

* <span data-ttu-id="adbda-151">Plug-ins: Aktivieren der Diagnoseprotokollierung- [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="adbda-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="adbda-152">Zuordnung von tizen 6 zu netstandard 2,1- [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="adbda-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="adbda-153">**[Liste aller in dieser Version behobene Probleme-5,1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="adbda-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
