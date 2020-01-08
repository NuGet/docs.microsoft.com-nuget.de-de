---
title: Nuget-installationspaketpowershell-Referenz
description: Referenz für den PowerShell-Befehl "Install-Package" in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: a65ba63ed070f40e82c43d12e5fad12d86f28112
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384440"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="7c4a4-103">Install-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="7c4a4-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="7c4a4-104">*In diesem Thema wird der Befehl in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows beschrieben. Den allgemeinen PowerShell-Befehl install-Package finden Sie in der [Referenz zu PowerShell packagemanagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="7c4a4-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="7c4a4-105">Installiert ein Paket und seine Abhängigkeiten in einem-Projekt.</span><span class="sxs-lookup"><span data-stu-id="7c4a4-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="7c4a4-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="7c4a4-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="7c4a4-107">In nuget 2.8 und höher können `Install-Package` ein vorhandenes Paket in Ihrem Projekt herabstufen.</span><span class="sxs-lookup"><span data-stu-id="7c4a4-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="7c4a4-108">Wenn Sie z. b. Microsoft. Aspnet. MVC 5.1.0-RC1 installiert haben, würde der folgende Befehl das Downgrade auf 5.0.0 durchführt:</span><span class="sxs-lookup"><span data-stu-id="7c4a4-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="7c4a4-109">Parameters</span><span class="sxs-lookup"><span data-stu-id="7c4a4-109">Parameters</span></span>

| <span data-ttu-id="7c4a4-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="7c4a4-110">Parameter</span></span> | <span data-ttu-id="7c4a4-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="7c4a4-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7c4a4-112">ID</span><span class="sxs-lookup"><span data-stu-id="7c4a4-112">Id</span></span> | <span data-ttu-id="7c4a4-113">Benötigten Der Bezeichner des zu installierenden Pakets.</span><span class="sxs-lookup"><span data-stu-id="7c4a4-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="7c4a4-114">(*3.0*und höher) Der Bezeichner kann ein Pfad oder eine URL einer `packages.config` Datei oder einer `.nupkg`-Datei sein.</span><span class="sxs-lookup"><span data-stu-id="7c4a4-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="7c4a4-115">Der Schalter-ID selbst ist optional.</span><span class="sxs-lookup"><span data-stu-id="7c4a4-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="7c4a4-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="7c4a4-116">IgnoreDependencies</span></span> | <span data-ttu-id="7c4a4-117">Installieren Sie nur dieses Paket und nicht seine Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="7c4a4-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="7c4a4-118">ProjektName</span><span class="sxs-lookup"><span data-stu-id="7c4a4-118">ProjectName</span></span> | <span data-ttu-id="7c4a4-119">Das Projekt, in dem das Paket installiert werden soll, und standardmäßig das Standard Projekt.</span><span class="sxs-lookup"><span data-stu-id="7c4a4-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="7c4a4-120">Quelle</span><span class="sxs-lookup"><span data-stu-id="7c4a4-120">Source</span></span> | <span data-ttu-id="7c4a4-121">Die URL oder der Ordner Pfad für die Paketquelle, die durchsucht werden soll.</span><span class="sxs-lookup"><span data-stu-id="7c4a4-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="7c4a4-122">Lokale Ordner Pfade können absolut oder relativ zum aktuellen Ordner sein.</span><span class="sxs-lookup"><span data-stu-id="7c4a4-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="7c4a4-123">Wenn der Wert weggelassen wird, wird `Install-Package` die aktuell ausgewählte Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="7c4a4-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="7c4a4-124">Version</span><span class="sxs-lookup"><span data-stu-id="7c4a4-124">Version</span></span> | <span data-ttu-id="7c4a4-125">Die Version des zu installierenden Pakets, standardmäßig auf die neueste Version.</span><span class="sxs-lookup"><span data-stu-id="7c4a4-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="7c4a4-126">Incluabprerelease</span><span class="sxs-lookup"><span data-stu-id="7c4a4-126">IncludePrerelease</span></span> | <span data-ttu-id="7c4a4-127">Berücksichtigt vorab Pakete für die Installation.</span><span class="sxs-lookup"><span data-stu-id="7c4a4-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="7c4a4-128">Wenn dieser Parameter nicht angegeben wird, werden nur stabile Pakete berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="7c4a4-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="7c4a4-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="7c4a4-129">FileConflictAction</span></span> | <span data-ttu-id="7c4a4-130">Die Aktion, die ausgeführt werden soll, wenn die vom Projekt referenzierten Dateien überschrieben oder ignoriert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="7c4a4-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="7c4a4-131">Mögliche Werte sind " *überschreiben", "ignorieren", "keine", "überschreiben*" und " *(3.0 +)* *IgnoreAll*".</span><span class="sxs-lookup"><span data-stu-id="7c4a4-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="7c4a4-132">Dependencyversion</span><span class="sxs-lookup"><span data-stu-id="7c4a4-132">DependencyVersion</span></span> | <span data-ttu-id="7c4a4-133">Die Version der zu verwendenden Abhängigkeits Pakete. Dies kann eine der folgenden sein:</span><span class="sxs-lookup"><span data-stu-id="7c4a4-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="7c4a4-134">*Niedrigste* (Standard): die niedrigste Version</span><span class="sxs-lookup"><span data-stu-id="7c4a4-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="7c4a4-135">*Highestpatch*: die Version mit dem niedrigsten, niedrigsten, niedrigsten, größten Patch</span><span class="sxs-lookup"><span data-stu-id="7c4a4-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="7c4a4-136">*Highestminor*: die Version mit dem niedrigsten Haupt-, höchst-und Höchstwert</span><span class="sxs-lookup"><span data-stu-id="7c4a4-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="7c4a4-137">*Höchste* (Standardeinstellung für Update-Package ohne Parameter): die höchste Version</span><span class="sxs-lookup"><span data-stu-id="7c4a4-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="7c4a4-138">Sie können den Standardwert mithilfe der Einstellung [`dependencyVersion`](../nuget-config-file.md#config-section) in der `Nuget.Config`-Datei festlegen.</span><span class="sxs-lookup"><span data-stu-id="7c4a4-138">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="7c4a4-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="7c4a4-139">WhatIf</span></span> | <span data-ttu-id="7c4a4-140">Zeigt, was geschehen würde, wenn der Befehl ausgeführt wird, ohne die Installation tatsächlich auszuführen.</span><span class="sxs-lookup"><span data-stu-id="7c4a4-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="7c4a4-141">Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.</span><span class="sxs-lookup"><span data-stu-id="7c4a4-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="7c4a4-142">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="7c4a4-142">Common Parameters</span></span>

<span data-ttu-id="7c4a4-143">`Install-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="7c4a4-143">`Install-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="7c4a4-144">Beispiele</span><span class="sxs-lookup"><span data-stu-id="7c4a4-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
