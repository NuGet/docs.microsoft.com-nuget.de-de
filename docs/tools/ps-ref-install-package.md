---
title: NuGet-Install-Package-PowerShell-Referenz
description: Referenz für Install-Package-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 6b2326d7b1ada8a337ae50ffd09f9deea80545af
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817953"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="adbaf-103">Install-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="adbaf-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="adbaf-104">*In diesem Thema wird beschrieben, den Befehl innerhalb der [NuGet Package Manager Console](package-manager-console.md) in Visual Studio unter Windows. Der generische PowerShell Install-Package-Befehl finden Sie unter der [PowerShell PackageManagement-Verweis](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="adbaf-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="adbaf-105">Installiert ein Paket und seine Abhängigkeiten in einem Projekt.</span><span class="sxs-lookup"><span data-stu-id="adbaf-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="adbaf-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="adbaf-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="adbaf-107">Im NuGet 2.8 + `Install-Package` können Sie ein downgrade ein vorhandenes Paket im Projekt.</span><span class="sxs-lookup"><span data-stu-id="adbaf-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="adbaf-108">Z. B. Wenn Sie Microsoft.AspNet.MVC 5.1.0-rc1 installiert haben, würde der folgende Befehl es 5.0.0 downgrade auf:</span><span class="sxs-lookup"><span data-stu-id="adbaf-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="adbaf-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="adbaf-109">Parameters</span></span>

| <span data-ttu-id="adbaf-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="adbaf-110">Parameter</span></span> | <span data-ttu-id="adbaf-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="adbaf-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="adbaf-112">Id</span><span class="sxs-lookup"><span data-stu-id="adbaf-112">Id</span></span> | <span data-ttu-id="adbaf-113">(Erforderlich) Der Bezeichner des zu installierenden Pakets an.</span><span class="sxs-lookup"><span data-stu-id="adbaf-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="adbaf-114">(*3.0 +*) der Bezeichner kann sein, einen Pfad oder URL des ein `packages.config` Datei oder ein `.nupkg` Datei.</span><span class="sxs-lookup"><span data-stu-id="adbaf-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="adbaf-115">Die - Id Schalter ist optional.</span><span class="sxs-lookup"><span data-stu-id="adbaf-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="adbaf-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="adbaf-116">IgnoreDependencies</span></span> | <span data-ttu-id="adbaf-117">Installieren Sie nur dieses Paket und nicht seine Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="adbaf-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="adbaf-118">ProjektName</span><span class="sxs-lookup"><span data-stu-id="adbaf-118">ProjectName</span></span> | <span data-ttu-id="adbaf-119">Das Projekt, in dem das Paket, auf das Standardprojekt direktionales installiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="adbaf-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="adbaf-120">Quelle</span><span class="sxs-lookup"><span data-stu-id="adbaf-120">Source</span></span> | <span data-ttu-id="adbaf-121">Die URL oder einen Ordnerpfad für die Paketquelle, gesucht werden soll.</span><span class="sxs-lookup"><span data-stu-id="adbaf-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="adbaf-122">Lokale Ordnerpfaden kann absolut oder relativ zum aktuellen Ordner.</span><span class="sxs-lookup"><span data-stu-id="adbaf-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="adbaf-123">Wenn nicht angegeben, `Install-Package` die aktuell ausgewählten Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="adbaf-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="adbaf-124">Version</span><span class="sxs-lookup"><span data-stu-id="adbaf-124">Version</span></span> | <span data-ttu-id="adbaf-125">Die Version des Pakets zu installieren, auf die neueste Version auszuführen.</span><span class="sxs-lookup"><span data-stu-id="adbaf-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="adbaf-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="adbaf-126">IncludePrerelease</span></span> | <span data-ttu-id="adbaf-127">Vorabversionen von Paketen für die Installation wird berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="adbaf-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="adbaf-128">Wenn nicht angegeben, werden nur stabile Pakete berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="adbaf-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="adbaf-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="adbaf-129">FileConflictAction</span></span> | <span data-ttu-id="adbaf-130">Die zu ergreifende Maßnahme beim aufgefordert, überschreiben oder ignorieren Sie vorhandene Dateien, die vom Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="adbaf-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="adbaf-131">Mögliche Werte sind *überschreiben, ignorieren, None, OverwriteAll*, und *(3.0 und höher)* *' ignoreall '*.</span><span class="sxs-lookup"><span data-stu-id="adbaf-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="adbaf-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="adbaf-132">DependencyVersion</span></span> | <span data-ttu-id="adbaf-133">Die Version der abhängigkeitspakete zu verwenden, die in der folgenden Werte sind möglich:</span><span class="sxs-lookup"><span data-stu-id="adbaf-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="adbaf-134">*Niedrigste* (Standard): die niedrigste Version</span><span class="sxs-lookup"><span data-stu-id="adbaf-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="adbaf-135">*HighestPatch*: die Version mit der niedrigsten wichtigen, niedrigste Nebenversion, höchste Patch</span><span class="sxs-lookup"><span data-stu-id="adbaf-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="adbaf-136">*HighestMinor*: die Version mit der niedrigsten Hauptversion, die höchste Nebenversion, höchste Patch</span><span class="sxs-lookup"><span data-stu-id="adbaf-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="adbaf-137">*Höchste* (Standard für Update-Paket ohne Parameter): die höchste Version</span><span class="sxs-lookup"><span data-stu-id="adbaf-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="adbaf-138">Sie können festlegen, den Standard-Wert mit der [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) festlegen in der `Nuget.Config` Datei.</span><span class="sxs-lookup"><span data-stu-id="adbaf-138">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="adbaf-139">"WhatIf"</span><span class="sxs-lookup"><span data-stu-id="adbaf-139">WhatIf</span></span> | <span data-ttu-id="adbaf-140">Zeigt an, was passieren würde, wenn der Befehl ausgeführt wird, ohne die Installation ausführen.</span><span class="sxs-lookup"><span data-stu-id="adbaf-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="adbaf-141">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="adbaf-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="adbaf-142">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="adbaf-142">Common Parameters</span></span>

<span data-ttu-id="adbaf-143">`Install-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="adbaf-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="adbaf-144">Beispiele</span><span class="sxs-lookup"><span data-stu-id="adbaf-144">Examples</span></span>

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
