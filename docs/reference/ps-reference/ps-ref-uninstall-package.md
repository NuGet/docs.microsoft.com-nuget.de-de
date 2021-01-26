---
title: Nuget-Uninstall-Package PowerShell-Referenz
description: Referenz für Uninstall-Package PowerShell-Befehl in der nuget-Paket-Manager-Konsole in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 961a9d68e5cba09030401fc871a93bf1145b23a3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777393"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="3d53a-103">Uninstall-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="3d53a-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3d53a-104">*In diesem Thema wird der Befehl in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows beschrieben. Den allgemeinen PowerShell-Uninstall-Package Befehl finden Sie in der [Referenz zu PowerShell packagemanagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="3d53a-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="3d53a-105">Entfernt ein Paket aus einem Projekt und entfernt optional seine Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="3d53a-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="3d53a-106">Wenn andere Pakete von diesem Paket abhängen, tritt bei diesem Befehl nur dann kein Fehler auf, wenn die Option "-Force" angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="3d53a-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="3d53a-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="3d53a-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="3d53a-108">Wenn andere Pakete von diesem Paket abhängen, tritt bei diesem Befehl nur dann kein Fehler auf, wenn die Option "-Force" angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="3d53a-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="3d53a-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="3d53a-109">Parameters</span></span>

| <span data-ttu-id="3d53a-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="3d53a-110">Parameter</span></span> | <span data-ttu-id="3d53a-111">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="3d53a-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3d53a-112">Id</span><span class="sxs-lookup"><span data-stu-id="3d53a-112">Id</span></span> | <span data-ttu-id="3d53a-113">Benötigten Der Bezeichner des zu deinstallierenden Pakets.</span><span class="sxs-lookup"><span data-stu-id="3d53a-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="3d53a-114">Der Schalter-ID selbst ist optional.</span><span class="sxs-lookup"><span data-stu-id="3d53a-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="3d53a-115">Version</span><span class="sxs-lookup"><span data-stu-id="3d53a-115">Version</span></span> | <span data-ttu-id="3d53a-116">Die Version des zu deinstallierenden Pakets, wobei die aktuell installierte Version standardmäßig installiert ist.</span><span class="sxs-lookup"><span data-stu-id="3d53a-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="3d53a-117">Removeabhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="3d53a-117">RemoveDependencies</span></span> | <span data-ttu-id="3d53a-118">Deinstallieren Sie das Paket und seine nicht verwendeten Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="3d53a-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="3d53a-119">Das heißt, wenn eine Abhängigkeit über ein anderes Paket verfügt, das davon abhängt, wird Sie übersprungen.</span><span class="sxs-lookup"><span data-stu-id="3d53a-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="3d53a-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="3d53a-120">ProjectName</span></span> | <span data-ttu-id="3d53a-121">Das Projekt, aus dem das Paket deinstalliert werden soll, und standardmäßig das Standard Projekt.</span><span class="sxs-lookup"><span data-stu-id="3d53a-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="3d53a-122">Force</span><span class="sxs-lookup"><span data-stu-id="3d53a-122">Force</span></span> | <span data-ttu-id="3d53a-123">Erzwingt, dass ein Paket deinstalliert wird, auch wenn andere Pakete davon abhängig sind.</span><span class="sxs-lookup"><span data-stu-id="3d53a-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="3d53a-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="3d53a-124">WhatIf</span></span> | <span data-ttu-id="3d53a-125">Zeigt, was geschehen würde, wenn der Befehl ausgeführt wird, ohne die Deinstallation tatsächlich auszuführen.</span><span class="sxs-lookup"><span data-stu-id="3d53a-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="3d53a-126">Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.</span><span class="sxs-lookup"><span data-stu-id="3d53a-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3d53a-127">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="3d53a-127">Common Parameters</span></span>

<span data-ttu-id="3d53a-128">`Uninstall-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3d53a-128">`Uninstall-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3d53a-129">Beispiele</span><span class="sxs-lookup"><span data-stu-id="3d53a-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```