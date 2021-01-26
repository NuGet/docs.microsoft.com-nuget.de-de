---
title: Nuget-Install-Package PowerShell-Referenz
description: Referenz für Install-Package PowerShell-Befehl in der nuget-Paket-Manager-Konsole in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 110b41e830636d60741b14292c17840aa5a63dfd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777447"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="74e9b-103">Install-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="74e9b-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="74e9b-104">*In diesem Thema wird der Befehl in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows beschrieben. Den allgemeinen PowerShell-Install-Package Befehl finden Sie in der [Referenz zu PowerShell packagemanagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="74e9b-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="74e9b-105">Installiert ein Paket und seine Abhängigkeiten in einem-Projekt.</span><span class="sxs-lookup"><span data-stu-id="74e9b-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="74e9b-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="74e9b-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="74e9b-107">In nuget 2.8 und höher `Install-Package` kann ein vorhandenes Paket in Ihrem Projekt herabstufen.</span><span class="sxs-lookup"><span data-stu-id="74e9b-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="74e9b-108">Wenn Sie z. b. Microsoft. Aspnet. MVC 5.1.0-RC1 installiert haben, würde der folgende Befehl das Downgrade auf 5.0.0 durchführt:</span><span class="sxs-lookup"><span data-stu-id="74e9b-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="74e9b-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="74e9b-109">Parameters</span></span>

| <span data-ttu-id="74e9b-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="74e9b-110">Parameter</span></span> | <span data-ttu-id="74e9b-111">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="74e9b-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="74e9b-112">Id</span><span class="sxs-lookup"><span data-stu-id="74e9b-112">Id</span></span> | <span data-ttu-id="74e9b-113">Benötigten Der Bezeichner des zu installierenden Pakets.</span><span class="sxs-lookup"><span data-stu-id="74e9b-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="74e9b-114">(*3.0* und höher) Der Bezeichner kann ein Pfad oder eine URL einer `packages.config` Datei oder eine `.nupkg` Datei sein.</span><span class="sxs-lookup"><span data-stu-id="74e9b-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="74e9b-115">Der Schalter-ID selbst ist optional.</span><span class="sxs-lookup"><span data-stu-id="74e9b-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="74e9b-116">Ignoreabhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="74e9b-116">IgnoreDependencies</span></span> | <span data-ttu-id="74e9b-117">Installieren Sie nur dieses Paket und nicht seine Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="74e9b-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="74e9b-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="74e9b-118">ProjectName</span></span> | <span data-ttu-id="74e9b-119">Das Projekt, in dem das Paket installiert werden soll, und standardmäßig das Standard Projekt.</span><span class="sxs-lookup"><span data-stu-id="74e9b-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="74e9b-120">`Source`</span><span class="sxs-lookup"><span data-stu-id="74e9b-120">Source</span></span> | <span data-ttu-id="74e9b-121">Die URL oder der Ordner Pfad für die Paketquelle, die durchsucht werden soll.</span><span class="sxs-lookup"><span data-stu-id="74e9b-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="74e9b-122">Lokale Ordner Pfade können absolut oder relativ zum aktuellen Ordner sein.</span><span class="sxs-lookup"><span data-stu-id="74e9b-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="74e9b-123">Wenn kein Wert angezeigt wird, wird `Install-Package` die aktuell ausgewählte Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="74e9b-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="74e9b-124">Version</span><span class="sxs-lookup"><span data-stu-id="74e9b-124">Version</span></span> | <span data-ttu-id="74e9b-125">Die Version des zu installierenden Pakets, standardmäßig auf die neueste Version.</span><span class="sxs-lookup"><span data-stu-id="74e9b-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="74e9b-126">Incluabprerelease</span><span class="sxs-lookup"><span data-stu-id="74e9b-126">IncludePrerelease</span></span> | <span data-ttu-id="74e9b-127">Berücksichtigt vorab Pakete für die Installation.</span><span class="sxs-lookup"><span data-stu-id="74e9b-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="74e9b-128">Wenn dieser Parameter nicht angegeben wird, werden nur stabile Pakete berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="74e9b-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="74e9b-129">Fileconflictaction</span><span class="sxs-lookup"><span data-stu-id="74e9b-129">FileConflictAction</span></span> | <span data-ttu-id="74e9b-130">Die Aktion, die ausgeführt werden soll, wenn die vom Projekt referenzierten Dateien überschrieben oder ignoriert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="74e9b-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="74e9b-131">Mögliche Werte sind " *überschreiben", "ignorieren", "keine", "überschreiben*" und " *(3.0 +)* *IgnoreAll*".</span><span class="sxs-lookup"><span data-stu-id="74e9b-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="74e9b-132">Dependencyversion</span><span class="sxs-lookup"><span data-stu-id="74e9b-132">DependencyVersion</span></span> | <span data-ttu-id="74e9b-133">Die Version der zu verwendenden Abhängigkeits Pakete. Dies kann eine der folgenden sein:</span><span class="sxs-lookup"><span data-stu-id="74e9b-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="74e9b-134">*Niedrigste* (Standard): die niedrigste Version</span><span class="sxs-lookup"><span data-stu-id="74e9b-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="74e9b-135">*Highestpatch*: die Version mit dem niedrigsten, niedrigsten, niedrigsten, größten Patch</span><span class="sxs-lookup"><span data-stu-id="74e9b-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="74e9b-136">*Highestminor*: die Version mit dem niedrigsten Haupt-, höchst-und Höchstwert</span><span class="sxs-lookup"><span data-stu-id="74e9b-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="74e9b-137">*Höchste* (Standardeinstellung für Update-Package ohne Parameter): die höchste Version</span><span class="sxs-lookup"><span data-stu-id="74e9b-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="74e9b-138">Sie können den Standardwert mithilfe der- [`dependencyVersion`](../nuget-config-file.md#config-section) Einstellung in der `Nuget.Config` Datei festlegen.</span><span class="sxs-lookup"><span data-stu-id="74e9b-138">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="74e9b-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="74e9b-139">WhatIf</span></span> | <span data-ttu-id="74e9b-140">Zeigt, was geschehen würde, wenn der Befehl ausgeführt wird, ohne die Installation tatsächlich auszuführen.</span><span class="sxs-lookup"><span data-stu-id="74e9b-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="74e9b-141">Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.</span><span class="sxs-lookup"><span data-stu-id="74e9b-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="74e9b-142">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="74e9b-142">Common Parameters</span></span>

<span data-ttu-id="74e9b-143">`Install-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="74e9b-143">`Install-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="74e9b-144">Beispiele</span><span class="sxs-lookup"><span data-stu-id="74e9b-144">Examples</span></span>

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