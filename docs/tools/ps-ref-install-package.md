---
title: NuGet-Installationspaket PowerShell-Referenz
description: Referenz für die Install-Package-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 755c87bbc68d3b688c81e16edbc1faabdc9e0520
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842499"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="63dbd-103">Install-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="63dbd-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="63dbd-104">*In diesem Thema wird beschrieben, den Befehl in der [-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows. Der generische Befehl der PowerShell-Install-Package, finden Sie unter den [PowerShell PackageManagement-Verweis](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="63dbd-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="63dbd-105">Installiert ein Paket und seine Abhängigkeiten in ein Projekt an.</span><span class="sxs-lookup"><span data-stu-id="63dbd-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="63dbd-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="63dbd-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="63dbd-107">In NuGet 2.8 und höher `Install-Package` kann ein vorhandenes Paket im Projekt "heruntergestuft".</span><span class="sxs-lookup"><span data-stu-id="63dbd-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="63dbd-108">Z. B. Wenn Sie "Microsoft.Aspnet.Mvc" 5.1.0-rc1 installiert haben, würde der folgende Befehl sie ein Downgrade auf 5.0.0 durchführen:</span><span class="sxs-lookup"><span data-stu-id="63dbd-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="63dbd-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="63dbd-109">Parameters</span></span>

| <span data-ttu-id="63dbd-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="63dbd-110">Parameter</span></span> | <span data-ttu-id="63dbd-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="63dbd-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="63dbd-112">Id</span><span class="sxs-lookup"><span data-stu-id="63dbd-112">Id</span></span> | <span data-ttu-id="63dbd-113">(Erforderlich) Der Bezeichner der zu installierenden Pakets an.</span><span class="sxs-lookup"><span data-stu-id="63dbd-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="63dbd-114">(*3.0 +* ) der Bezeichner kann sein, einen Pfad oder URL von einem `packages.config` Datei oder ein `.nupkg` Datei.</span><span class="sxs-lookup"><span data-stu-id="63dbd-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="63dbd-115">Die - Id Switch selbst ist optional.</span><span class="sxs-lookup"><span data-stu-id="63dbd-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="63dbd-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="63dbd-116">IgnoreDependencies</span></span> | <span data-ttu-id="63dbd-117">Installieren Sie nur dieses Paket und nicht seine Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="63dbd-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="63dbd-118">ProjektName</span><span class="sxs-lookup"><span data-stu-id="63dbd-118">ProjectName</span></span> | <span data-ttu-id="63dbd-119">Das Projekt in die zum Installieren des Pakets, das als Standardprojekt.</span><span class="sxs-lookup"><span data-stu-id="63dbd-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="63dbd-120">Source</span><span class="sxs-lookup"><span data-stu-id="63dbd-120">Source</span></span> | <span data-ttu-id="63dbd-121">Der URL oder Ordner Pfad für die Paketquelle, um zu suchen.</span><span class="sxs-lookup"><span data-stu-id="63dbd-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="63dbd-122">Lokalen Ordnerpfade können absolut oder relativ zum aktuellen Ordner sein.</span><span class="sxs-lookup"><span data-stu-id="63dbd-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="63dbd-123">Wenn nicht angegeben, `Install-Package` die aktuell ausgewählte Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="63dbd-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="63dbd-124">Version</span><span class="sxs-lookup"><span data-stu-id="63dbd-124">Version</span></span> | <span data-ttu-id="63dbd-125">Die Version des Pakets installiert werden, standardmäßig auf die neueste Version.</span><span class="sxs-lookup"><span data-stu-id="63dbd-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="63dbd-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="63dbd-126">IncludePrerelease</span></span> | <span data-ttu-id="63dbd-127">Vorabversionen von Paketen für die Installation wird berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="63dbd-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="63dbd-128">Wenn nicht angegeben, werden nur stabile Pakete berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="63dbd-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="63dbd-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="63dbd-129">FileConflictAction</span></span> | <span data-ttu-id="63dbd-130">Die auszuführende Aktion, wenn aufgefordert, die überschrieben werden soll, oder ignorieren die vorhandene Dateien, die vom Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="63dbd-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="63dbd-131">Mögliche Werte sind *überschreiben, die Sie keine "," OverwriteAll*, und *(3.0 und höher)* *' ignoreall '* .</span><span class="sxs-lookup"><span data-stu-id="63dbd-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="63dbd-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="63dbd-132">DependencyVersion</span></span> | <span data-ttu-id="63dbd-133">Die Version des der abhängigkeitspakete zu verwenden, die in der folgenden Werte sind möglich:</span><span class="sxs-lookup"><span data-stu-id="63dbd-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="63dbd-134">*Niedrigste* (Standard): die niedrigste Version</span><span class="sxs-lookup"><span data-stu-id="63dbd-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="63dbd-135">*HighestPatch*: die Version mit der niedrigsten wichtigen, niedrigste kleinere, höchste Patch</span><span class="sxs-lookup"><span data-stu-id="63dbd-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="63dbd-136">*HighestMinor*: die Version mit der niedrigsten Hauptversion, die höchste kleinere, höchste-Patch</span><span class="sxs-lookup"><span data-stu-id="63dbd-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="63dbd-137">*Höchste* (Standard für Update-Package ohne Parameter): die höchste Version</span><span class="sxs-lookup"><span data-stu-id="63dbd-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="63dbd-138">Sie können festlegen, den Standard-Wert mit der [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) festlegen in der `Nuget.Config` Datei.</span><span class="sxs-lookup"><span data-stu-id="63dbd-138">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="63dbd-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="63dbd-139">WhatIf</span></span> | <span data-ttu-id="63dbd-140">Zeigt an, was geschieht, wenn der Befehl ausgeführt wird, ohne die Installation ausführen.</span><span class="sxs-lookup"><span data-stu-id="63dbd-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="63dbd-141">Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="63dbd-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="63dbd-142">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="63dbd-142">Common Parameters</span></span>

<span data-ttu-id="63dbd-143">`Install-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="63dbd-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="63dbd-144">Beispiele</span><span class="sxs-lookup"><span data-stu-id="63dbd-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
