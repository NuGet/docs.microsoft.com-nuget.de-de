---
title: Update-NuGet-Paket-PowerShell-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für das Updatepaket PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio."
keywords: NuGet-Paket-Manager-Konsole, die NuGet Powershell-Befehle, die NuGet Powershell-Referenz, Update-Paket
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 293d9a7fdcce633eb5a97e5f76398deb5c13bdb4
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="73668-104">Update-Paket (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="73668-104">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="73668-105">*Verfügbar nur innerhalb der [NuGet Package Manager Console](package-manager-console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="73668-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="73668-106">Aktualisiert ein Paket und seine Abhängigkeiten oder alle Pakete in einem Projekt auf eine neuere Version.</span><span class="sxs-lookup"><span data-stu-id="73668-106">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="73668-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="73668-107">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="73668-108">Im NuGet 2.8 + `Update-Package` herabgestuft werden, ein vorhandenes Paket im Projekt verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="73668-108">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="73668-109">Z. B. Wenn Sie Microsoft.AspNet.MVC 5.1.0-rc1 installiert haben, würde der folgende Befehl es 5.0.0 downgrade auf:</span><span class="sxs-lookup"><span data-stu-id="73668-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="73668-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="73668-110">Parameters</span></span>

|  <span data-ttu-id="73668-111">Parameter</span><span class="sxs-lookup"><span data-stu-id="73668-111">Parameter</span></span> | <span data-ttu-id="73668-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="73668-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="73668-113">Id</span><span class="sxs-lookup"><span data-stu-id="73668-113">Id</span></span> | <span data-ttu-id="73668-114">Der Bezeichner des Pakets aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="73668-114">The identifier of the package to update.</span></span> <span data-ttu-id="73668-115">Wenn nicht angegeben, aktualisiert alle Pakete aus.</span><span class="sxs-lookup"><span data-stu-id="73668-115">If omitted, updates all packages.</span></span> <span data-ttu-id="73668-116">Die - Id Schalter ist optional.</span><span class="sxs-lookup"><span data-stu-id="73668-116">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="73668-117">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="73668-117">IgnoreDependencies</span></span> | <span data-ttu-id="73668-118">Überspringt die Abhängigkeiten des Pakets aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="73668-118">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="73668-119">ProjektName</span><span class="sxs-lookup"><span data-stu-id="73668-119">ProjectName</span></span> | <span data-ttu-id="73668-120">Der Name des Projekts, enthält die Pakete zu aktualisieren, die Standardwerte für alle Projekte.</span><span class="sxs-lookup"><span data-stu-id="73668-120">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="73668-121">Version</span><span class="sxs-lookup"><span data-stu-id="73668-121">Version</span></span> | <span data-ttu-id="73668-122">Die Version, die für das Upgrade auf die neueste Version standardmäßig verwendet.</span><span class="sxs-lookup"><span data-stu-id="73668-122">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="73668-123">In 3.0 + NuGet der Versionswert möglich *niedrigste, höchste, HighestMinor*, oder *HighestPatch* (gleichwertig mit "- Safe).</span><span class="sxs-lookup"><span data-stu-id="73668-123">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="73668-124">Safe</span><span class="sxs-lookup"><span data-stu-id="73668-124">Safe</span></span> | <span data-ttu-id="73668-125">Schränkt Upgrades auf nur Versionen mit der gleichen Haupt- und Version als der derzeit installierten Paket.</span><span class="sxs-lookup"><span data-stu-id="73668-125">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="73668-126">Quelle</span><span class="sxs-lookup"><span data-stu-id="73668-126">Source</span></span> | <span data-ttu-id="73668-127">Die URL oder einen Ordnerpfad für die Paketquelle, gesucht werden soll.</span><span class="sxs-lookup"><span data-stu-id="73668-127">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="73668-128">Lokale Ordnerpfaden kann absolut oder relativ zum aktuellen Ordner.</span><span class="sxs-lookup"><span data-stu-id="73668-128">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="73668-129">Wenn nicht angegeben, `Uninstall-Package` die aktuell ausgewählten Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="73668-129">If omitted, `Uninstall-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="73668-130">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="73668-130">IncludePrerelease</span></span> | <span data-ttu-id="73668-131">Enthält nach Updates Vorabversionen von Paketen.</span><span class="sxs-lookup"><span data-stu-id="73668-131">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="73668-132">Neuinstallation</span><span class="sxs-lookup"><span data-stu-id="73668-132">Reinstall</span></span> | <span data-ttu-id="73668-133">Resintalls-Pakete, die ihre aktuell installierten Versionen verwenden.</span><span class="sxs-lookup"><span data-stu-id="73668-133">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="73668-134">Informationen dazu finden Sie unter [Neuinstallieren und Aktualisieren von Paketen](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="73668-134">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="73668-135">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="73668-135">FileConflictAction</span></span> | <span data-ttu-id="73668-136">Die zu ergreifende Maßnahme beim aufgefordert, überschreiben oder ignorieren Sie vorhandene Dateien, die vom Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="73668-136">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="73668-137">Mögliche Werte sind *überschreiben, ignorieren, None, OverwriteAll*, und *' ignoreall '* (3.0 und höher).</span><span class="sxs-lookup"><span data-stu-id="73668-137">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="73668-138">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="73668-138">DependencyVersion</span></span> | <span data-ttu-id="73668-139">Die Version der abhängigkeitspakete zu verwenden, die in der folgenden Werte sind möglich:</span><span class="sxs-lookup"><span data-stu-id="73668-139">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="73668-140">*Niedrigste* (Standard): die niedrigste Version</span><span class="sxs-lookup"><span data-stu-id="73668-140">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="73668-141">*HighestPatch*: die Version mit der niedrigsten wichtigen, niedrigste Nebenversion, höchste Patch</span><span class="sxs-lookup"><span data-stu-id="73668-141">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="73668-142">*HighestMinor*: die Version mit der niedrigsten Hauptversion, die höchste Nebenversion, höchste Patch</span><span class="sxs-lookup"><span data-stu-id="73668-142">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="73668-143">*Höchste* (Standard für Update-Paket ohne Parameter): die höchste Version</span><span class="sxs-lookup"><span data-stu-id="73668-143">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="73668-144">Sie können festlegen, den Standard-Wert mit der [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) festlegen in der `Nuget.Config` Datei.</span><span class="sxs-lookup"><span data-stu-id="73668-144">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="73668-145">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="73668-145">ToHighestPatch</span></span> | <span data-ttu-id="73668-146">Schränkt Upgrades nur Versionen mit der gleichen Nebenversion als der derzeit installierten Paket.</span><span class="sxs-lookup"><span data-stu-id="73668-146">Constrains upgrades to only versions with the same Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="73668-147">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="73668-147">ToHighestMinor</span></span> | <span data-ttu-id="73668-148">Schränkt Upgrades nur Versionen mit der gleichen Hauptversion als der derzeit installierten Paket.</span><span class="sxs-lookup"><span data-stu-id="73668-148">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="73668-149">WhatIf</span><span class="sxs-lookup"><span data-stu-id="73668-149">WhatIf</span></span> | <span data-ttu-id="73668-150">Zeigt an, was passieren würde, wenn der Befehl ausgeführt wird, ohne das Update ausführen.</span><span class="sxs-lookup"><span data-stu-id="73668-150">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="73668-151">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="73668-151">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="73668-152">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="73668-152">Common Parameters</span></span>

<span data-ttu-id="73668-153">`Update-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="73668-153">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="73668-154">Beispiele</span><span class="sxs-lookup"><span data-stu-id="73668-154">Examples</span></span>

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