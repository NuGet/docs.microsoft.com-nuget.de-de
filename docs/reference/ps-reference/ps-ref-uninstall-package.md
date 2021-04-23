---
title: NuGetUninstall-Package PowerShell-Referenz
description: Referenz für Uninstall-Package PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 371e95c341efbce1c4a15facefc15cd51b266141
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901784"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="b5d6c-103">Uninstall-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="b5d6c-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="b5d6c-104">*In diesem Thema wird der Befehl in der [Paket-Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio Windows beschrieben. Den generischen PowerShellUninstall-Package befehl finden Sie in der [Referenz zu PowerShell PackageManagement.](/powershell/module/packagemanagement)*</span><span class="sxs-lookup"><span data-stu-id="b5d6c-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="b5d6c-105">Entfernt ein Paket aus einem Projekt und entfernt optional seine Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="b5d6c-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="b5d6c-106">Wenn andere Pakete von diesem Paket abhängen, tritt bei diesem Befehl nur dann kein Fehler auf, wenn die Option "-Force" angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="b5d6c-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="b5d6c-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="b5d6c-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="b5d6c-108">Wenn andere Pakete von diesem Paket abhängen, tritt bei diesem Befehl nur dann kein Fehler auf, wenn die Option "-Force" angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="b5d6c-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="b5d6c-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="b5d6c-109">Parameters</span></span>

| <span data-ttu-id="b5d6c-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="b5d6c-110">Parameter</span></span> | <span data-ttu-id="b5d6c-111">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="b5d6c-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b5d6c-112">Id</span><span class="sxs-lookup"><span data-stu-id="b5d6c-112">Id</span></span> | <span data-ttu-id="b5d6c-113">(Erforderlich) Der Bezeichner des zu deinstallierenden Pakets.</span><span class="sxs-lookup"><span data-stu-id="b5d6c-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="b5d6c-114">Der Schalter -Id selbst ist optional.</span><span class="sxs-lookup"><span data-stu-id="b5d6c-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="b5d6c-115">Version</span><span class="sxs-lookup"><span data-stu-id="b5d6c-115">Version</span></span> | <span data-ttu-id="b5d6c-116">Die Version des zu deinstallierenden Pakets, standardmäßig die derzeit installierte Version.</span><span class="sxs-lookup"><span data-stu-id="b5d6c-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="b5d6c-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="b5d6c-117">RemoveDependencies</span></span> | <span data-ttu-id="b5d6c-118">Deinstallieren Sie das Paket und seine nicht verwendeten Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="b5d6c-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="b5d6c-119">Das heißt, wenn eine Abhängigkeit über ein anderes Paket verfügt, das davon abhängt, wird sie übersprungen.</span><span class="sxs-lookup"><span data-stu-id="b5d6c-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="b5d6c-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="b5d6c-120">ProjectName</span></span> | <span data-ttu-id="b5d6c-121">Das Projekt, aus dem das Paket deinstalliert werden soll, standardmäßig das Standardprojekt.</span><span class="sxs-lookup"><span data-stu-id="b5d6c-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="b5d6c-122">Force</span><span class="sxs-lookup"><span data-stu-id="b5d6c-122">Force</span></span> | <span data-ttu-id="b5d6c-123">Erzwingt die Deinstallation eines Pakets, auch wenn andere Pakete davon abhängig sind.</span><span class="sxs-lookup"><span data-stu-id="b5d6c-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="b5d6c-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="b5d6c-124">WhatIf</span></span> | <span data-ttu-id="b5d6c-125">Zeigt an, was geschieht, wenn der Befehl ausgeführt wird, ohne die Deinstallation tatsächlich auszuführen.</span><span class="sxs-lookup"><span data-stu-id="b5d6c-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="b5d6c-126">Keiner dieser Parameter akzeptiert Pipelineeingaben oder Platzhalterzeichen.</span><span class="sxs-lookup"><span data-stu-id="b5d6c-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="b5d6c-127">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="b5d6c-127">Common Parameters</span></span>

<span data-ttu-id="b5d6c-128">`Uninstall-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b5d6c-128">`Uninstall-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="b5d6c-129">Beispiele</span><span class="sxs-lookup"><span data-stu-id="b5d6c-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```