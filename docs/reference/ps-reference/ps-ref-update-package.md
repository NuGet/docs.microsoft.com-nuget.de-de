---
title: Nuget-Update-Package PowerShell-Referenz
description: Referenz für Update-Package PowerShell-Befehl in der nuget-Paket-Manager-Konsole in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 159817e56d978d6432e989d2027907c0d2445222
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777379"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="f8eb8-103">Update-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f8eb8-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f8eb8-104">*Nur in der [nuget-Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows verfügbar.*</span><span class="sxs-lookup"><span data-stu-id="f8eb8-104">*Available only within the [NuGet Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f8eb8-105">Aktualisiert ein Paket und seine Abhängigkeiten oder alle Pakete in einem Projekt auf eine neuere Version.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="f8eb8-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="f8eb8-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="f8eb8-107">In nuget 2.8 und höher `Update-Package` können Sie ein vorhandenes Paket in Ihrem Projekt herabstufen.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="f8eb8-108">Wenn Sie z. b. Microsoft. Aspnet. MVC 5.1.0-RC1 installiert haben, würde der folgende Befehl das Downgrade auf 5.0.0 durchführt:</span><span class="sxs-lookup"><span data-stu-id="f8eb8-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="f8eb8-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="f8eb8-109">Parameters</span></span>

|  <span data-ttu-id="f8eb8-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="f8eb8-110">Parameter</span></span> | <span data-ttu-id="f8eb8-111">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="f8eb8-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f8eb8-112">Id</span><span class="sxs-lookup"><span data-stu-id="f8eb8-112">Id</span></span> | <span data-ttu-id="f8eb8-113">Der Bezeichner des zu aktualisierenden Pakets.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-113">The identifier of the package to update.</span></span> <span data-ttu-id="f8eb8-114">Wenn dieser nicht ausgelassen wird, werden alle Pakete aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-114">If omitted, updates all packages.</span></span> <span data-ttu-id="f8eb8-115">Der Schalter-ID selbst ist optional.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="f8eb8-116">Ignoreabhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="f8eb8-116">IgnoreDependencies</span></span> | <span data-ttu-id="f8eb8-117">Überspringt die Aktualisierung der Paketabhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="f8eb8-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="f8eb8-118">ProjectName</span></span> | <span data-ttu-id="f8eb8-119">Der Name des Projekts, das die zu aktualisierenden Pakete enthält, die standardmäßig auf alle Projekte aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="f8eb8-120">Version</span><span class="sxs-lookup"><span data-stu-id="f8eb8-120">Version</span></span> | <span data-ttu-id="f8eb8-121">Die für das Upgrade zu verwendende Version, die standardmäßig die neueste Version verwendet.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="f8eb8-122">In nuget 3.0 und höher muss der Versions Wert einer der *niedrigsten, höchsten, highestminor* oder *highestpatch* (äquivalent zu-Safe) sein.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="f8eb8-123">Safe</span><span class="sxs-lookup"><span data-stu-id="f8eb8-123">Safe</span></span> | <span data-ttu-id="f8eb8-124">Schränkt Upgrades auf Versionen ein, die die gleiche Haupt-und neben Version wie das aktuell installierte Paket haben.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="f8eb8-125">`Source`</span><span class="sxs-lookup"><span data-stu-id="f8eb8-125">Source</span></span> | <span data-ttu-id="f8eb8-126">Die URL oder der Ordner Pfad für die Paketquelle, die durchsucht werden soll.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="f8eb8-127">Lokale Ordner Pfade können absolut oder relativ zum aktuellen Ordner sein.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="f8eb8-128">Wenn kein Wert angezeigt wird, wird `Update-Package` die aktuell ausgewählte Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="f8eb8-129">Incluabprerelease</span><span class="sxs-lookup"><span data-stu-id="f8eb8-129">IncludePrerelease</span></span> | <span data-ttu-id="f8eb8-130">Schließt vorab Pakete für Updates ein.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="f8eb8-131">Neuinstallation</span><span class="sxs-lookup"><span data-stu-id="f8eb8-131">Reinstall</span></span> | <span data-ttu-id="f8eb8-132">Gibt Pakete zurück, die Ihre aktuell installierten Versionen verwenden.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="f8eb8-133">Weitere Informationen finden Sie unter [Neuinstallieren und Aktualisieren von Paketen](../../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="f8eb8-133">See [Reinstalling and updating packages](../../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="f8eb8-134">Fileconflictaction</span><span class="sxs-lookup"><span data-stu-id="f8eb8-134">FileConflictAction</span></span> | <span data-ttu-id="f8eb8-135">Die Aktion, die ausgeführt werden soll, wenn die vom Projekt referenzierten Dateien überschrieben oder ignoriert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="f8eb8-136">Mögliche Werte sind " *überschreiben", "ignorieren", "keine", "überschreiben*" und " *IgnoreAll* " (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="f8eb8-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="f8eb8-137">Dependencyversion</span><span class="sxs-lookup"><span data-stu-id="f8eb8-137">DependencyVersion</span></span> | <span data-ttu-id="f8eb8-138">Die Version der zu verwendenden Abhängigkeits Pakete. Dies kann eine der folgenden sein:</span><span class="sxs-lookup"><span data-stu-id="f8eb8-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="f8eb8-139">*Niedrigste* (Standard): die niedrigste Version</span><span class="sxs-lookup"><span data-stu-id="f8eb8-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="f8eb8-140">*Highestpatch*: die Version mit dem niedrigsten, niedrigsten, niedrigsten, größten Patch</span><span class="sxs-lookup"><span data-stu-id="f8eb8-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="f8eb8-141">*Highestminor*: die Version mit dem niedrigsten Haupt-, höchst-und Höchstwert</span><span class="sxs-lookup"><span data-stu-id="f8eb8-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="f8eb8-142">*Höchste* (Standardeinstellung für Update-Package ohne Parameter): die höchste Version</span><span class="sxs-lookup"><span data-stu-id="f8eb8-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="f8eb8-143">Sie können den Standardwert mithilfe der- [`dependencyVersion`](../nuget-config-file.md#config-section) Einstellung in der `Nuget.Config` Datei festlegen.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-143">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="f8eb8-144">"Thighestpatch"</span><span class="sxs-lookup"><span data-stu-id="f8eb8-144">ToHighestPatch</span></span> | <span data-ttu-id="f8eb8-145">Äquivalent zu-Safe.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="f8eb8-146">"" Zu ""</span><span class="sxs-lookup"><span data-stu-id="f8eb8-146">ToHighestMinor</span></span> | <span data-ttu-id="f8eb8-147">Schränkt Upgrades auf Versionen ein, die dieselbe Hauptversion wie das aktuell installierte Paket haben.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="f8eb8-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="f8eb8-148">WhatIf</span></span> | <span data-ttu-id="f8eb8-149">Zeigt, was geschieht, wenn der Befehl ausgeführt wird, ohne die Aktualisierung tatsächlich auszuführen.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="f8eb8-150">Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="f8eb8-151">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="f8eb8-151">Common Parameters</span></span>

<span data-ttu-id="f8eb8-152">`Update-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f8eb8-152">`Update-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="f8eb8-153">Beispiele</span><span class="sxs-lookup"><span data-stu-id="f8eb8-153">Examples</span></span>

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
Update-Package Elmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package Elmah –reinstall -ignoreDependencies
```
