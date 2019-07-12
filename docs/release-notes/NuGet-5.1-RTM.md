---
title: Anmerkungen zu NuGet Version 5.1 RTM
description: Anmerkungen zu NuGet 5.1, einschließlich der neuen Features, Fehlerbehebungen und DCRs.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 384145947b19af6577dc1255985df1a361c72bb5
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842583"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="8f907-103">Anmerkungen zu NuGet Version 5.1</span><span class="sxs-lookup"><span data-stu-id="8f907-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="8f907-104">Möglichkeiten der NuGet-Verteilung:</span><span class="sxs-lookup"><span data-stu-id="8f907-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="8f907-105">NuGet-Version</span><span class="sxs-lookup"><span data-stu-id="8f907-105">NuGet version</span></span> | <span data-ttu-id="8f907-106">Verfügbar in der Visual Studio-Version</span><span class="sxs-lookup"><span data-stu-id="8f907-106">Available in Visual Studio version</span></span>| <span data-ttu-id="8f907-107">Verfügbar in .NET SDK(s)</span><span class="sxs-lookup"><span data-stu-id="8f907-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="8f907-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="8f907-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="8f907-109">Visual Studio 2019-Version 16.1</span><span class="sxs-lookup"><span data-stu-id="8f907-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="8f907-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="8f907-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="8f907-111"><sup>1</sup>mit Visual Studio-2019 mit .NET Core-Workload installiert</span><span class="sxs-lookup"><span data-stu-id="8f907-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="8f907-112"><sup>2</sup>verfügbar als optionale Installation mit Visual Studio-2019 mit .NET Core-Workload</span><span class="sxs-lookup"><span data-stu-id="8f907-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="8f907-113">Zusammenfassung: Neuerungen in 5.1</span><span class="sxs-lookup"><span data-stu-id="8f907-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="8f907-114">Unterstützung für ein Paket Push zu überspringen, wenn sie bereits vorhanden ist, um eine bessere Integration mit CI/CD-Workflows – ermöglichen [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="8f907-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="8f907-115">Visual Studio bietet nun eine einfache Verknüpfung mit dem des Pakets "NuGet.org"-Katalogseite - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="8f907-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="8f907-116">Unterstützung für neue .NET Core-3.0-Ressourcen wie z. B. [Targeting Packs](https://github.com/dotnet/cli/issues/10006) und [Common Language Runtime-Packs](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="8f907-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="8f907-117">NuGet Pack "und" Restore-Unterstützung für FrameworkReferences Paketverweise Zielgruppenadressierung und -Runtime - aktivieren [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="8f907-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="8f907-118">Unterstützung für "nur herunterladen" Paket-Szenario mit PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="8f907-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="8f907-119">Exlcude-Laufzeit und die Zielversionen von Suchergebnissen und Wiederherstellung Diagramm mit PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="8f907-119">Exlcude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="8f907-120">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="8f907-120">Issues fixed in this release</span></span>

<span data-ttu-id="8f907-121">**Fehler**</span><span class="sxs-lookup"><span data-stu-id="8f907-121">**Bugs**</span></span>

* <span data-ttu-id="8f907-122">Plug-Ins: Details der Ausnahme verloren gehen, während der Erstellung des-Plug-in - [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="8f907-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="8f907-123">PackageReference-Bereich mit exklusiven Untergrenze funktioniert nicht, wenn die untere Grenze, die auf eine der Quellen vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="8f907-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="8f907-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="8f907-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="8f907-125">Verbessern IsPackableFalseError Nachricht - [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="8f907-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="8f907-126">Pakete Sperrdatei - Sperrdatei zum erneuten Generieren der, wenn Projekt Diagramm ändert - [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="8f907-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="8f907-127">Project System-Fehler: NuGet-Pakete, die erste automatische entfernt - [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="8f907-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="8f907-128">Fügen Sie ein Ziel für die Rückgabe der FrameworkReference ähnlich wie CollectPackageDownloads und CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="8f907-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="8f907-129">HTTP-Cache:  RepositoryResources Ressource wird nicht zwischengespeichert, mit versionsverwaltung durch das so - [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="8f907-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="8f907-130">Protokollierung: Ausnahme Aufruflisten werden nicht gemeldet, mit detailliertem Ausführlichkeitsgrad - [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="8f907-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="8f907-131">Ändern Sie alle URLs von NuGet-Dokumentation zur Verwendung von HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="8f907-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="8f907-132">Verbessern Sie NU3024 Warnmeldung - [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="8f907-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="8f907-133">Sperrdatei, die nicht aktualisiert, wenn "packagereference" entfernt - [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="8f907-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="8f907-134">Verbessern Sie die Fehlerbehandlung auf Groß-/Kleinschreibung bei der Überprüfung "licenseUrl" und die Lizenz-Element in der Nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="8f907-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="8f907-135">PM-UI - mit der rechten Maustaste auf die Registerkartenheader und das Ergebnis durch Klicken auf "Dateispeicherort öffnen" Fehler: [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="8f907-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="8f907-136">Plug-Ins: Melden Sie sich bei der Plug-in-Prozess wird beendet - [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="8f907-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="8f907-137">Plug-Ins: hohe Kollisionsrate in Datetime-Werten Protokollierung - [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="8f907-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="8f907-138">Manifest.ReadFrom schlägt fehl, auf alle NuSpec-Datei mit LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="8f907-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="8f907-139">RestoreLockedMode: Unerwarteter NU1004, wenn "ProjectReference" auf ein Projekt mit benutzerdefinierten AssemblyName - verweist [#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="8f907-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="8f907-140">Besser verständliche Fehlermeldung angezeigt, wenn der Start-Plug-in mit einer Ausnahme: ein Fehler auftritt [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="8f907-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="8f907-141">Wenn eine NoOp-Wiederherstellung durchführen zu können, sollten Sie vermeiden \*. dgspec.json schreiben im Verzeichnis "Obj" - [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="8f907-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="8f907-142">GeneratePathProperty = "true" kann nicht zum Generieren-Eigenschaft auf Groß-/Kleinschreibung Konflikt - [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="8f907-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="8f907-143">Einstellungen: unzulässiges Zeichen im Paketquellpfad kann VS - Absturz [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="8f907-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="8f907-144">Wenn Sperrdatei gelöscht wird, generiert Wiederherstellung keine Sperrdatei auf NoOp - [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="8f907-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="8f907-145">Lizenz-URL und die Lizenz bewirkt, dass Fehler mit Metadaten - beim Lesen der [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="8f907-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="8f907-146">Nicht behandelte Ausnahmen in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="8f907-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="8f907-147">NuGet.exe gibt Exitcode 0 (null) für ungültige Argumente - [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="8f907-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="8f907-148">Aktualisieren von Fehlern und Warnung-Dokumentation entsprechend Signieren verwandte Szenarien - [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="8f907-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="8f907-149">Assetdatei sollten relative Pfade verwenden, um die gleitenden Projekte einfacher - ermöglichen [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="8f907-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="8f907-150">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="8f907-150">**DCRs**</span></span>

* <span data-ttu-id="8f907-151">Plug-Ins: Aktivieren der diagnoseprotokollierung - [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="8f907-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="8f907-152">Stellen Tizen 6-Karte, um NetStandard 2.1 – [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="8f907-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="8f907-153">**[Liste aller Probleme, die in dieser Version – Version 5.1 RTM behoben](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="8f907-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
