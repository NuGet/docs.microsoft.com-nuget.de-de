---
title: Deinstallieren von NuGet-Paket-PowerShell-Referenz
description: Referenz für die Uninstall-Package-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: c95479103be2cba3b4eb6964ea761870477863bd
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842473"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="7cb66-103">Uninstall-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="7cb66-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="7cb66-104">*In diesem Thema wird beschrieben, den Befehl in der [-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows. Der generische PowerShell Uninstall-Package-Befehl finden Sie unter den [PowerShell PackageManagement-Verweis](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="7cb66-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="7cb66-105">Entfernt ein Paket aus einem Projekt, und seine Abhängigkeiten optional zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="7cb66-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="7cb66-106">Wenn dieses Paket andere Pakete abhängig sind, wird der Befehl fehl, es sei denn, das – Force angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="7cb66-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="7cb66-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="7cb66-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="7cb66-108">Wenn dieses Paket andere Pakete abhängig sind, wird der Befehl fehl, es sei denn, das – Force angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="7cb66-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="7cb66-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="7cb66-109">Parameters</span></span>

| <span data-ttu-id="7cb66-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="7cb66-110">Parameter</span></span> | <span data-ttu-id="7cb66-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="7cb66-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7cb66-112">Id</span><span class="sxs-lookup"><span data-stu-id="7cb66-112">Id</span></span> | <span data-ttu-id="7cb66-113">(Erforderlich) Der Bezeichner des Pakets deinstallieren.</span><span class="sxs-lookup"><span data-stu-id="7cb66-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="7cb66-114">Die - Id Switch selbst ist optional.</span><span class="sxs-lookup"><span data-stu-id="7cb66-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="7cb66-115">Version</span><span class="sxs-lookup"><span data-stu-id="7cb66-115">Version</span></span> | <span data-ttu-id="7cb66-116">Die Version des Pakets zu deinstallieren, als die derzeit installierte Version.</span><span class="sxs-lookup"><span data-stu-id="7cb66-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="7cb66-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="7cb66-117">RemoveDependencies</span></span> | <span data-ttu-id="7cb66-118">Deinstallieren Sie das Paket und seine nicht verwendeten Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="7cb66-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="7cb66-119">D. h. wird eine Abhängigkeit ein weiteres Paket aufweist, das von ihr abhängig ist, es übersprungen.</span><span class="sxs-lookup"><span data-stu-id="7cb66-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="7cb66-120">ProjektName</span><span class="sxs-lookup"><span data-stu-id="7cb66-120">ProjectName</span></span> | <span data-ttu-id="7cb66-121">Das Projekt aus dem Deinstallieren des Pakets, das als Standardprojekt.</span><span class="sxs-lookup"><span data-stu-id="7cb66-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="7cb66-122">Force</span><span class="sxs-lookup"><span data-stu-id="7cb66-122">Force</span></span> | <span data-ttu-id="7cb66-123">Erzwingt, dass ein Paket deinstalliert werden, auch wenn andere Pakete davon abhängig sind.</span><span class="sxs-lookup"><span data-stu-id="7cb66-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="7cb66-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="7cb66-124">WhatIf</span></span> | <span data-ttu-id="7cb66-125">Zeigt an, was geschieht, wenn der Befehl ausgeführt wird, ohne die Deinstallation ausführen.</span><span class="sxs-lookup"><span data-stu-id="7cb66-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="7cb66-126">Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="7cb66-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="7cb66-127">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="7cb66-127">Common Parameters</span></span>

<span data-ttu-id="7cb66-128">`Uninstall-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="7cb66-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="7cb66-129">Beispiele</span><span class="sxs-lookup"><span data-stu-id="7cb66-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
