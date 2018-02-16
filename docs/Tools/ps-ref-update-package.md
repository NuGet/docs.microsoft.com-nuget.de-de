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
ms.openlocfilehash: 7ebb5a420e469c70a9dd790231a92fedbc4713b6
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/14/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="ce361-104">Update-Paket (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="ce361-104">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ce361-105">*Verfügbar nur innerhalb der [NuGet Package Manager Console](package-manager-console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="ce361-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="ce361-106">Aktualisiert ein Paket und seine Abhängigkeiten oder alle Pakete in einem Projekt auf eine neuere Version.</span><span class="sxs-lookup"><span data-stu-id="ce361-106">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="ce361-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="ce361-107">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="ce361-108">Im NuGet 2.8 + `Update-Package` herabgestuft werden, ein vorhandenes Paket im Projekt verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="ce361-108">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="ce361-109">Z. B. Wenn Sie Microsoft.AspNet.MVC 5.1.0-rc1 installiert haben, würde der folgende Befehl es 5.0.0 downgrade auf:</span><span class="sxs-lookup"><span data-stu-id="ce361-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

<span data-ttu-id="ce361-110">NuGet 2.7 und früher erhalten eine Fehlermeldung, dass bereits eine neuere Version installiert ist.</span><span class="sxs-lookup"><span data-stu-id="ce361-110">NuGet 2.7 and earlier gives an error saying that a newer version is already installed.</span></span>

## <a name="parameters"></a><span data-ttu-id="ce361-111">Parameter</span><span class="sxs-lookup"><span data-stu-id="ce361-111">Parameters</span></span>

|  <span data-ttu-id="ce361-112">Parameter</span><span class="sxs-lookup"><span data-stu-id="ce361-112">Parameter</span></span> | <span data-ttu-id="ce361-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="ce361-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ce361-114">Id</span><span class="sxs-lookup"><span data-stu-id="ce361-114">Id</span></span> | <span data-ttu-id="ce361-115">Der Bezeichner des Pakets aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="ce361-115">The identifier of the package to update.</span></span> <span data-ttu-id="ce361-116">Wenn nicht angegeben, aktualisiert alle Pakete aus.</span><span class="sxs-lookup"><span data-stu-id="ce361-116">If omitted, updates all packages.</span></span> <span data-ttu-id="ce361-117">Die - Id Schalter ist optional.</span><span class="sxs-lookup"><span data-stu-id="ce361-117">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="ce361-118">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="ce361-118">IgnoreDependencies</span></span> | <span data-ttu-id="ce361-119">Überspringt die Abhängigkeiten des Pakets aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="ce361-119">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="ce361-120">ProjektName</span><span class="sxs-lookup"><span data-stu-id="ce361-120">ProjectName</span></span> | <span data-ttu-id="ce361-121">Der Name des Projekts, enthält die Pakete zu aktualisieren, die Standardwerte für alle Projekte.</span><span class="sxs-lookup"><span data-stu-id="ce361-121">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="ce361-122">Version</span><span class="sxs-lookup"><span data-stu-id="ce361-122">Version</span></span> | <span data-ttu-id="ce361-123">Die Version, die für das Upgrade auf die neueste Version standardmäßig verwendet.</span><span class="sxs-lookup"><span data-stu-id="ce361-123">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="ce361-124">In 3.0 + NuGet der Versionswert möglich *niedrigste, höchste, HighestMinor*, oder *HighestPatch* (gleichwertig mit "- Safe).</span><span class="sxs-lookup"><span data-stu-id="ce361-124">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="ce361-125">Safe</span><span class="sxs-lookup"><span data-stu-id="ce361-125">Safe</span></span> | <span data-ttu-id="ce361-126">Schränkt Upgrades auf nur Versionen mit der gleichen Haupt- und Version als der derzeit installierten Paket.</span><span class="sxs-lookup"><span data-stu-id="ce361-126">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="ce361-127">Quelle</span><span class="sxs-lookup"><span data-stu-id="ce361-127">Source</span></span> | <span data-ttu-id="ce361-128">Die URL oder einen Ordnerpfad für die Paketquelle, gesucht werden soll.</span><span class="sxs-lookup"><span data-stu-id="ce361-128">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="ce361-129">Lokale Ordnerpfaden kann absolut oder relativ zum aktuellen Ordner.</span><span class="sxs-lookup"><span data-stu-id="ce361-129">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="ce361-130">Wenn nicht angegeben, `Uninstall-Package` die aktuell ausgewählten Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="ce361-130">If omitted, `Uninstall-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="ce361-131">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="ce361-131">IncludePrerelease</span></span> | <span data-ttu-id="ce361-132">Enthält nach Updates Vorabversionen von Paketen.</span><span class="sxs-lookup"><span data-stu-id="ce361-132">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="ce361-133">Neuinstallation</span><span class="sxs-lookup"><span data-stu-id="ce361-133">Reinstall</span></span> | <span data-ttu-id="ce361-134">Resintalls-Pakete, die ihre aktuell installierten Versionen verwenden.</span><span class="sxs-lookup"><span data-stu-id="ce361-134">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="ce361-135">Informationen dazu finden Sie unter [Neuinstallieren und Aktualisieren von Paketen](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="ce361-135">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="ce361-136">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="ce361-136">FileConflictAction</span></span> | <span data-ttu-id="ce361-137">Die zu ergreifende Maßnahme beim aufgefordert, überschreiben oder ignorieren Sie vorhandene Dateien, die vom Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="ce361-137">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="ce361-138">Mögliche Werte sind *überschreiben, ignorieren, None, OverwriteAll*, und *' ignoreall '* (3.0 und höher).</span><span class="sxs-lookup"><span data-stu-id="ce361-138">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="ce361-139">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="ce361-139">DependencyVersion</span></span> | <span data-ttu-id="ce361-140">Die Version der abhängigkeitspakete zu verwenden, die in der folgenden Werte sind möglich:</span><span class="sxs-lookup"><span data-stu-id="ce361-140">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="ce361-141">*Niedrigste* (Standard): die niedrigste Version</span><span class="sxs-lookup"><span data-stu-id="ce361-141">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="ce361-142">*HighestPatch*: die Version mit der niedrigsten wichtigen, niedrigste Nebenversion, höchste Patch</span><span class="sxs-lookup"><span data-stu-id="ce361-142">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="ce361-143">*HighestMinor*: die Version mit der niedrigsten Hauptversion, die höchste Nebenversion, höchste Patch</span><span class="sxs-lookup"><span data-stu-id="ce361-143">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="ce361-144">*Höchste* (Standard für Update-Paket ohne Parameter): die höchste Version</span><span class="sxs-lookup"><span data-stu-id="ce361-144">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="ce361-145">Sie können festlegen, den Standard-Wert mit der [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) festlegen in der `Nuget.Config` Datei.</span><span class="sxs-lookup"><span data-stu-id="ce361-145">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="ce361-146">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="ce361-146">ToHighestPatch</span></span> | <span data-ttu-id="ce361-147">Schränkt Upgrades nur Versionen mit der gleichen Nebenversion als der derzeit installierten Paket.</span><span class="sxs-lookup"><span data-stu-id="ce361-147">Constrains upgrades to only versions with the same Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="ce361-148">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="ce361-148">ToHighestMinor</span></span> | <span data-ttu-id="ce361-149">Schränkt Upgrades nur Versionen mit der gleichen Hauptversion als der derzeit installierten Paket.</span><span class="sxs-lookup"><span data-stu-id="ce361-149">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="ce361-150">WhatIf</span><span class="sxs-lookup"><span data-stu-id="ce361-150">WhatIf</span></span> | <span data-ttu-id="ce361-151">Zeigt an, was passieren würde, wenn der Befehl ausgeführt wird, ohne das Update ausführen.</span><span class="sxs-lookup"><span data-stu-id="ce361-151">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="ce361-152">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="ce361-152">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="ce361-153">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="ce361-153">Common Parameters</span></span>

<span data-ttu-id="ce361-154">`Update-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="ce361-154">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="ce361-155">Beispiele</span><span class="sxs-lookup"><span data-stu-id="ce361-155">Examples</span></span>

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