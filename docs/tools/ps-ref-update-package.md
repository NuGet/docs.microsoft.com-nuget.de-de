---
title: Update-NuGet-Paket-PowerShell-Referenz
description: Referenz für die Update-Package-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5b5a11ee11d9e2cf6a90d56ac63b1f7bad750ea
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496494"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="9d8f7-103">Update-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="9d8f7-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="9d8f7-104">*Verfügbar nur in der [NuGet-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="9d8f7-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="9d8f7-105">Wird ein Paket und seine Abhängigkeiten oder alle Pakete in einem Projekt auf eine neuere Version aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="9d8f7-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="9d8f7-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="9d8f7-107">In NuGet 2.8 und höher `Update-Package` können verwendet werden, um ein vorhandenes Paket in Ihrem Projekt ein Downgrade durchführen.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="9d8f7-108">Z. B. Wenn Sie "Microsoft.Aspnet.Mvc" 5.1.0-rc1 installiert haben, würde der folgende Befehl sie ein Downgrade auf 5.0.0 durchführen:</span><span class="sxs-lookup"><span data-stu-id="9d8f7-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="9d8f7-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="9d8f7-109">Parameters</span></span>

|  <span data-ttu-id="9d8f7-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="9d8f7-110">Parameter</span></span> | <span data-ttu-id="9d8f7-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9d8f7-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9d8f7-112">Id</span><span class="sxs-lookup"><span data-stu-id="9d8f7-112">Id</span></span> | <span data-ttu-id="9d8f7-113">Der Bezeichner des Pakets aktualisiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-113">The identifier of the package to update.</span></span> <span data-ttu-id="9d8f7-114">Wenn nicht angegeben, werden alle Pakete aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-114">If omitted, updates all packages.</span></span> <span data-ttu-id="9d8f7-115">Die - Id Switch selbst ist optional.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="9d8f7-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="9d8f7-116">IgnoreDependencies</span></span> | <span data-ttu-id="9d8f7-117">Überspringt die Abhängigkeiten des Pakets aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="9d8f7-118">ProjektName</span><span class="sxs-lookup"><span data-stu-id="9d8f7-118">ProjectName</span></span> | <span data-ttu-id="9d8f7-119">Der Name des Projekts, in dem Pakete aktualisiert, es wird der Standardwert für alle Projekte.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="9d8f7-120">Version</span><span class="sxs-lookup"><span data-stu-id="9d8f7-120">Version</span></span> | <span data-ttu-id="9d8f7-121">Die Version, die für das Upgrade, standardmäßig auf die neueste Version verwendet.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="9d8f7-122">In NuGet 3.0 und höher der Wert muss einer der *niedrigste, höchste, HighestMinor*, oder *HighestPatch* (Äquivalent zu: Safe).</span><span class="sxs-lookup"><span data-stu-id="9d8f7-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="9d8f7-123">Safe</span><span class="sxs-lookup"><span data-stu-id="9d8f7-123">Safe</span></span> | <span data-ttu-id="9d8f7-124">Schränkt Upgrades nur Versionen mit der gleichen Haupt- und Nebenversionen-Version als die derzeit installierten Paket.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="9d8f7-125">Source</span><span class="sxs-lookup"><span data-stu-id="9d8f7-125">Source</span></span> | <span data-ttu-id="9d8f7-126">Der URL oder Ordner Pfad für die Paketquelle, um zu suchen.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="9d8f7-127">Lokalen Ordnerpfade können absolut oder relativ zum aktuellen Ordner sein.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="9d8f7-128">Wenn nicht angegeben, `Update-Package` die aktuell ausgewählte Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="9d8f7-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="9d8f7-129">IncludePrerelease</span></span> | <span data-ttu-id="9d8f7-130">Enthält nach Updates Vorabversionen von Paketen.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="9d8f7-131">Neuinstallation</span><span class="sxs-lookup"><span data-stu-id="9d8f7-131">Reinstall</span></span> | <span data-ttu-id="9d8f7-132">Resintalls-Pakete, die ihre aktuell installierten Versionen verwenden.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="9d8f7-133">Informationen dazu finden Sie unter [Neuinstallieren und Aktualisieren von Paketen](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="9d8f7-133">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="9d8f7-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="9d8f7-134">FileConflictAction</span></span> | <span data-ttu-id="9d8f7-135">Die auszuführende Aktion, wenn aufgefordert, die überschrieben werden soll, oder ignorieren die vorhandene Dateien, die vom Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="9d8f7-136">Mögliche Werte sind *überschreiben, die Sie keine "," OverwriteAll*, und *' ignoreall '* (3.0 und höher).</span><span class="sxs-lookup"><span data-stu-id="9d8f7-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="9d8f7-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="9d8f7-137">DependencyVersion</span></span> | <span data-ttu-id="9d8f7-138">Die Version des der abhängigkeitspakete zu verwenden, die in der folgenden Werte sind möglich:</span><span class="sxs-lookup"><span data-stu-id="9d8f7-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="9d8f7-139">*Niedrigste* (Standard): die niedrigste Version</span><span class="sxs-lookup"><span data-stu-id="9d8f7-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="9d8f7-140">*HighestPatch*: die Version mit der niedrigsten wichtigen, niedrigste kleinere, höchste Patch</span><span class="sxs-lookup"><span data-stu-id="9d8f7-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="9d8f7-141">*HighestMinor*: die Version mit der niedrigsten Hauptversion, die höchste kleinere, höchste-Patch</span><span class="sxs-lookup"><span data-stu-id="9d8f7-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="9d8f7-142">*Höchste* (Standard für Update-Package ohne Parameter): die höchste Version</span><span class="sxs-lookup"><span data-stu-id="9d8f7-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="9d8f7-143">Sie können festlegen, den Standard-Wert mit der [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) festlegen in der `Nuget.Config` Datei.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-143">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="9d8f7-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="9d8f7-144">ToHighestPatch</span></span> | <span data-ttu-id="9d8f7-145">Äquivalent zu – sicher.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="9d8f7-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="9d8f7-146">ToHighestMinor</span></span> | <span data-ttu-id="9d8f7-147">Schränkt Upgrades nur Versionen mit derselben Hauptversion als die derzeit installierten Paket.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="9d8f7-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="9d8f7-148">WhatIf</span></span> | <span data-ttu-id="9d8f7-149">Zeigt an, was geschieht, wenn der Befehl ausgeführt wird, ohne das Update ausführen.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="9d8f7-150">Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="9d8f7-151">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="9d8f7-151">Common Parameters</span></span>

<span data-ttu-id="9d8f7-152">`Update-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9d8f7-152">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="9d8f7-153">Beispiele</span><span class="sxs-lookup"><span data-stu-id="9d8f7-153">Examples</span></span>

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
