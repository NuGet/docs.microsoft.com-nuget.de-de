---
title: Sync-NuGet-Pakets PowerShell-Referenz
description: Referenz für die Synchronisierung-Package-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: de0b612e1335cafdcd6a0b802d54f2182d27ad22
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842251"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="e788d-103">Sync-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e788d-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e788d-104">*Version 3.0 und höher; verfügbar nur in der [-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="e788d-104">*Version 3.0+; available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e788d-105">Ruft die Version des installierten Pakets vom angegebenen (oder Standard), project und synchronisiert die Version für den Rest der Projekte in der Projektmappe.</span><span class="sxs-lookup"><span data-stu-id="e788d-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="e788d-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="e788d-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="e788d-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="e788d-107">Parameters</span></span>

| <span data-ttu-id="e788d-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="e788d-108">Parameter</span></span> | <span data-ttu-id="e788d-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="e788d-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e788d-110">Id</span><span class="sxs-lookup"><span data-stu-id="e788d-110">Id</span></span> | <span data-ttu-id="e788d-111">(Erforderlich) Der Bezeichner des Pakets zu synchronisieren. Die - Id Switch selbst ist optional.</span><span class="sxs-lookup"><span data-stu-id="e788d-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="e788d-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="e788d-112">IgnoreDependencies</span></span> | <span data-ttu-id="e788d-113">Installieren Sie nur dieses Paket und nicht seine Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="e788d-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="e788d-114">ProjektName</span><span class="sxs-lookup"><span data-stu-id="e788d-114">ProjectName</span></span> | <span data-ttu-id="e788d-115">Das Projekt, das Paket aus, die als Standardprojekt zu synchronisieren.</span><span class="sxs-lookup"><span data-stu-id="e788d-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="e788d-116">Version</span><span class="sxs-lookup"><span data-stu-id="e788d-116">Version</span></span> | <span data-ttu-id="e788d-117">Die Version des Pakets zu synchronisieren, als die derzeit installierte Version.</span><span class="sxs-lookup"><span data-stu-id="e788d-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="e788d-118">Source</span><span class="sxs-lookup"><span data-stu-id="e788d-118">Source</span></span> | <span data-ttu-id="e788d-119">Der URL oder Ordner Pfad für die Paketquelle, um zu suchen.</span><span class="sxs-lookup"><span data-stu-id="e788d-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="e788d-120">Lokalen Ordnerpfade können absolut oder relativ zum aktuellen Ordner sein.</span><span class="sxs-lookup"><span data-stu-id="e788d-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="e788d-121">Wenn nicht angegeben, `Sync-Package` die aktuell ausgewählte Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="e788d-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="e788d-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="e788d-122">IncludePrerelease</span></span> | <span data-ttu-id="e788d-123">Enthält Vorabversionen von Paketen, bei der Synchronisierung.</span><span class="sxs-lookup"><span data-stu-id="e788d-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="e788d-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="e788d-124">FileConflictAction</span></span> | <span data-ttu-id="e788d-125">Die auszuführende Aktion, wenn aufgefordert, die überschrieben werden soll, oder ignorieren die vorhandene Dateien, die vom Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="e788d-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="e788d-126">Mögliche Werte sind *überschreiben, die Sie keine "," OverwriteAll*, und *(3.0 und höher)* *' ignoreall '* .</span><span class="sxs-lookup"><span data-stu-id="e788d-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="e788d-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="e788d-127">DependencyVersion</span></span> | <span data-ttu-id="e788d-128">Die Version des der abhängigkeitspakete zu verwenden, die in der folgenden Werte sind möglich:</span><span class="sxs-lookup"><span data-stu-id="e788d-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="e788d-129">*Niedrigste* (Standard): die niedrigste Version</span><span class="sxs-lookup"><span data-stu-id="e788d-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="e788d-130">*HighestPatch*: die Version mit der niedrigsten wichtigen, niedrigste kleinere, höchste Patch</span><span class="sxs-lookup"><span data-stu-id="e788d-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="e788d-131">*HighestMinor*: die Version mit der niedrigsten Hauptversion, die höchste kleinere, höchste-Patch</span><span class="sxs-lookup"><span data-stu-id="e788d-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="e788d-132">*Höchste* (Standard für Update-Package ohne Parameter): die höchste Version</span><span class="sxs-lookup"><span data-stu-id="e788d-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="e788d-133">Sie können festlegen, den Standard-Wert mit der [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) festlegen in der `Nuget.Config` Datei.</span><span class="sxs-lookup"><span data-stu-id="e788d-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="e788d-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="e788d-134">WhatIf</span></span> | <span data-ttu-id="e788d-135">Zeigt an, was geschieht, wenn der Befehl ausgeführt wird, ohne die Synchronisierung ausführen.</span><span class="sxs-lookup"><span data-stu-id="e788d-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="e788d-136">Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="e788d-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e788d-137">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="e788d-137">Common Parameters</span></span>

<span data-ttu-id="e788d-138">`Sync-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e788d-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e788d-139">Beispiele</span><span class="sxs-lookup"><span data-stu-id="e788d-139">Examples</span></span>

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
