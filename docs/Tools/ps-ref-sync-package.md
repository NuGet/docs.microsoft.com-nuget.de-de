---
title: Sync-NuGet-Pakets PowerShell-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für die Sync-Paket-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio."
keywords: NuGet-Paket-Manager-Konsole, die NuGet Powershell-Befehle, die NuGet Powershell-Referenz, Sync-Pakets
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8e4b627cff01a353440c47883b98cd93f9edd6cb
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/14/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="4c025-104">Sync-Paket (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="4c025-104">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4c025-105">*Version 3.0 +; verfügbar nur innerhalb der [NuGet Package Manager Console](package-manager-console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="4c025-105">*Version 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="4c025-106">Ruft die Version des installierten Pakets aus einer angegebenen (oder Standard)-Projekt und synchronisiert die Version mit den restlichen Projekten in der Projektmappe.</span><span class="sxs-lookup"><span data-stu-id="4c025-106">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="4c025-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="4c025-107">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="4c025-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="4c025-108">Parameters</span></span>

| <span data-ttu-id="4c025-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="4c025-109">Parameter</span></span> | <span data-ttu-id="4c025-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="4c025-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4c025-111">Id</span><span class="sxs-lookup"><span data-stu-id="4c025-111">Id</span></span> | <span data-ttu-id="4c025-112">(Erforderlich) Der Bezeichner des Pakets zu synchronisieren. Die - Id Schalter ist optional.</span><span class="sxs-lookup"><span data-stu-id="4c025-112">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="4c025-113">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="4c025-113">IgnoreDependencies</span></span> | <span data-ttu-id="4c025-114">Installieren Sie nur dieses Paket und nicht seine Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="4c025-114">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="4c025-115">ProjektName</span><span class="sxs-lookup"><span data-stu-id="4c025-115">ProjectName</span></span> | <span data-ttu-id="4c025-116">Das Projekt, um das Paket aus, auf das Standardprojekt direktionales zu synchronisieren.</span><span class="sxs-lookup"><span data-stu-id="4c025-116">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="4c025-117">Version</span><span class="sxs-lookup"><span data-stu-id="4c025-117">Version</span></span> | <span data-ttu-id="4c025-118">Die Version des Pakets zu synchronisieren, die derzeit installierte Version auszuführen.</span><span class="sxs-lookup"><span data-stu-id="4c025-118">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="4c025-119">Quelle</span><span class="sxs-lookup"><span data-stu-id="4c025-119">Source</span></span> | <span data-ttu-id="4c025-120">Die URL oder einen Ordnerpfad für die Paketquelle, gesucht werden soll.</span><span class="sxs-lookup"><span data-stu-id="4c025-120">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="4c025-121">Lokale Ordnerpfaden kann absolut oder relativ zum aktuellen Ordner.</span><span class="sxs-lookup"><span data-stu-id="4c025-121">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="4c025-122">Wenn nicht angegeben, `Sync-Package` die aktuell ausgewählten Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="4c025-122">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="4c025-123">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="4c025-123">IncludePrerelease</span></span> | <span data-ttu-id="4c025-124">Enthält vorabversionspakete in die Synchronisierung.</span><span class="sxs-lookup"><span data-stu-id="4c025-124">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="4c025-125">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="4c025-125">FileConflictAction</span></span> | <span data-ttu-id="4c025-126">Die zu ergreifende Maßnahme beim aufgefordert, überschreiben oder ignorieren Sie vorhandene Dateien, die vom Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="4c025-126">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="4c025-127">Mögliche Werte sind *überschreiben, ignorieren, None, OverwriteAll*, und *(3.0 und höher)* *' ignoreall '*.</span><span class="sxs-lookup"><span data-stu-id="4c025-127">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="4c025-128">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="4c025-128">DependencyVersion</span></span> | <span data-ttu-id="4c025-129">Die Version der abhängigkeitspakete zu verwenden, die in der folgenden Werte sind möglich:</span><span class="sxs-lookup"><span data-stu-id="4c025-129">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="4c025-130">*Niedrigste* (Standard): die niedrigste Version</span><span class="sxs-lookup"><span data-stu-id="4c025-130">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="4c025-131">*HighestPatch*: die Version mit der niedrigsten wichtigen, niedrigste Nebenversion, höchste Patch</span><span class="sxs-lookup"><span data-stu-id="4c025-131">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="4c025-132">*HighestMinor*: die Version mit der niedrigsten Hauptversion, die höchste Nebenversion, höchste Patch</span><span class="sxs-lookup"><span data-stu-id="4c025-132">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="4c025-133">*Höchste* (Standard für Update-Paket ohne Parameter): die höchste Version</span><span class="sxs-lookup"><span data-stu-id="4c025-133">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="4c025-134">Sie können festlegen, den Standard-Wert mit der [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) festlegen in der `Nuget.Config` Datei.</span><span class="sxs-lookup"><span data-stu-id="4c025-134">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="4c025-135">WhatIf</span><span class="sxs-lookup"><span data-stu-id="4c025-135">WhatIf</span></span> | <span data-ttu-id="4c025-136">Zeigt an, was passieren würde, wenn der Befehl ausgeführt wird, ohne die Synchronisierung ausführen.</span><span class="sxs-lookup"><span data-stu-id="4c025-136">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="4c025-137">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="4c025-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4c025-138">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="4c025-138">Common Parameters</span></span>

<span data-ttu-id="4c025-139">`Sync-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="4c025-139">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4c025-140">Beispiele</span><span class="sxs-lookup"><span data-stu-id="4c025-140">Examples</span></span>

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```
