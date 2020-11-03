---
title: Nuget-Sync-Package PowerShell-Referenz
description: Referenz für Sync-Package PowerShell-Befehl in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fc4c875b5dcb0b90e4d048daf5984ed265370090
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238048"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="39f0e-103">Sync-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="39f0e-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="39f0e-104">*Version 3.0 und höher nur in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows verfügbar.*</span><span class="sxs-lookup"><span data-stu-id="39f0e-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="39f0e-105">Ruft die Version des installierten Pakets aus dem angegebenen (oder standardmäßigen) Projekt ab und synchronisiert die Version mit dem Rest der Projekte in der Projekt Mappe.</span><span class="sxs-lookup"><span data-stu-id="39f0e-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="39f0e-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="39f0e-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="39f0e-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="39f0e-107">Parameters</span></span>

| <span data-ttu-id="39f0e-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="39f0e-108">Parameter</span></span> | <span data-ttu-id="39f0e-109">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="39f0e-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="39f0e-110">Id</span><span class="sxs-lookup"><span data-stu-id="39f0e-110">Id</span></span> | <span data-ttu-id="39f0e-111">Benötigten Der Bezeichner des zu synchronisierenden Pakets. Der Schalter-ID selbst ist optional.</span><span class="sxs-lookup"><span data-stu-id="39f0e-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="39f0e-112">Ignoreabhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="39f0e-112">IgnoreDependencies</span></span> | <span data-ttu-id="39f0e-113">Installieren Sie nur dieses Paket und nicht seine Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="39f0e-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="39f0e-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="39f0e-114">ProjectName</span></span> | <span data-ttu-id="39f0e-115">Das Projekt, von dem das Paket synchronisiert wird, und standardmäßig das Standard Projekt.</span><span class="sxs-lookup"><span data-stu-id="39f0e-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="39f0e-116">Version</span><span class="sxs-lookup"><span data-stu-id="39f0e-116">Version</span></span> | <span data-ttu-id="39f0e-117">Die Version des zu synchronisierenden Pakets, wobei die aktuell installierte Version standardmäßig installiert ist.</span><span class="sxs-lookup"><span data-stu-id="39f0e-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="39f0e-118">`Source`</span><span class="sxs-lookup"><span data-stu-id="39f0e-118">Source</span></span> | <span data-ttu-id="39f0e-119">Die URL oder der Ordner Pfad für die Paketquelle, die durchsucht werden soll.</span><span class="sxs-lookup"><span data-stu-id="39f0e-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="39f0e-120">Lokale Ordner Pfade können absolut oder relativ zum aktuellen Ordner sein.</span><span class="sxs-lookup"><span data-stu-id="39f0e-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="39f0e-121">Wenn kein Wert angezeigt wird, wird `Sync-Package` die aktuell ausgewählte Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="39f0e-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="39f0e-122">Incluabprerelease</span><span class="sxs-lookup"><span data-stu-id="39f0e-122">IncludePrerelease</span></span> | <span data-ttu-id="39f0e-123">Schließt vorab Pakete in die Synchronisierung ein.</span><span class="sxs-lookup"><span data-stu-id="39f0e-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="39f0e-124">Fileconflictaction</span><span class="sxs-lookup"><span data-stu-id="39f0e-124">FileConflictAction</span></span> | <span data-ttu-id="39f0e-125">Die Aktion, die ausgeführt werden soll, wenn die vom Projekt referenzierten Dateien überschrieben oder ignoriert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="39f0e-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="39f0e-126">Mögliche Werte sind " *überschreiben", "ignorieren", "keine", "überschreiben* " und " *(3.0 +)* *IgnoreAll* ".</span><span class="sxs-lookup"><span data-stu-id="39f0e-126">Possible values are *Overwrite, Ignore, None, OverwriteAll* , and *(3.0+)* *IgnoreAll* .</span></span> |
| <span data-ttu-id="39f0e-127">Dependencyversion</span><span class="sxs-lookup"><span data-stu-id="39f0e-127">DependencyVersion</span></span> | <span data-ttu-id="39f0e-128">Die Version der zu verwendenden Abhängigkeits Pakete. Dies kann eine der folgenden sein:</span><span class="sxs-lookup"><span data-stu-id="39f0e-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="39f0e-129">*Niedrigste* (Standard): die niedrigste Version</span><span class="sxs-lookup"><span data-stu-id="39f0e-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="39f0e-130">*Highestpatch* : die Version mit dem niedrigsten, niedrigsten, niedrigsten, größten Patch</span><span class="sxs-lookup"><span data-stu-id="39f0e-130">*HighestPatch* : the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="39f0e-131">*Highestminor* : die Version mit dem niedrigsten Haupt-, höchst-und Höchstwert</span><span class="sxs-lookup"><span data-stu-id="39f0e-131">*HighestMinor* : the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="39f0e-132">*Höchste* (Standardeinstellung für Update-Package ohne Parameter): die höchste Version</span><span class="sxs-lookup"><span data-stu-id="39f0e-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="39f0e-133">Sie können den Standardwert mithilfe der- [`dependencyVersion`](../nuget-config-file.md#config-section) Einstellung in der `Nuget.Config` Datei festlegen.</span><span class="sxs-lookup"><span data-stu-id="39f0e-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="39f0e-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="39f0e-134">WhatIf</span></span> | <span data-ttu-id="39f0e-135">Zeigt, was geschehen würde, wenn der Befehl ausgeführt wird, ohne die Synchronisierung tatsächlich auszuführen.</span><span class="sxs-lookup"><span data-stu-id="39f0e-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="39f0e-136">Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.</span><span class="sxs-lookup"><span data-stu-id="39f0e-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="39f0e-137">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="39f0e-137">Common Parameters</span></span>

<span data-ttu-id="39f0e-138">`Sync-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="39f0e-138">`Sync-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="39f0e-139">Beispiele</span><span class="sxs-lookup"><span data-stu-id="39f0e-139">Examples</span></span>

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