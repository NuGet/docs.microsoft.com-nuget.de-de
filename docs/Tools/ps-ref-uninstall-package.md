---
title: Deinstallieren Sie NuGet-Paket-PowerShell-Referenz
description: Referenz für Uninstall-Package-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5969526a12cb6e06f23f35a2481d0385bb9780ab
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="51294-103">Uninstall-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="51294-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="51294-104">*In diesem Thema wird beschrieben, den Befehl innerhalb der [NuGet Package Manager Console](package-manager-console.md) in Visual Studio unter Windows. Der generische Deinstallationspaket für PowerShell-Befehl finden Sie unter der [PowerShell PackageManagement-Verweis](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="51294-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="51294-105">Entfernt ein Paket aus einem Projekt, und optional die abhängigen Elemente entfernen.</span><span class="sxs-lookup"><span data-stu-id="51294-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="51294-106">Wenn andere Pakete von diesem Paket abhängen, wird der Befehl fehl, es sei denn, der "– Force" angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="51294-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="51294-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="51294-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="51294-108">Wenn andere Pakete von diesem Paket abhängen, wird der Befehl fehl, es sei denn, der "– Force" angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="51294-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="51294-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="51294-109">Parameters</span></span>

| <span data-ttu-id="51294-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="51294-110">Parameter</span></span> | <span data-ttu-id="51294-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="51294-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="51294-112">Id</span><span class="sxs-lookup"><span data-stu-id="51294-112">Id</span></span> | <span data-ttu-id="51294-113">(Erforderlich) Der Bezeichner der zu deinstallierenden Pakets.</span><span class="sxs-lookup"><span data-stu-id="51294-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="51294-114">Die - Id Schalter ist optional.</span><span class="sxs-lookup"><span data-stu-id="51294-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="51294-115">Version</span><span class="sxs-lookup"><span data-stu-id="51294-115">Version</span></span> | <span data-ttu-id="51294-116">Die Version des Pakets zu deinstallieren, die derzeit installierte Version auszuführen.</span><span class="sxs-lookup"><span data-stu-id="51294-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="51294-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="51294-117">RemoveDependencies</span></span> | <span data-ttu-id="51294-118">Deinstallieren Sie das Paket und alle nicht verwendeten Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="51294-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="51294-119">D. h., wenn eine der Abhängigkeiten ein anderes Paket, das von ihm abhängig ist aufweist, wird sie übersprungen.</span><span class="sxs-lookup"><span data-stu-id="51294-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="51294-120">ProjektName</span><span class="sxs-lookup"><span data-stu-id="51294-120">ProjectName</span></span> | <span data-ttu-id="51294-121">Das Projekt, von dem das Paket, auf das Standardprojekt direktionales deinstalliert werden soll.</span><span class="sxs-lookup"><span data-stu-id="51294-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="51294-122">Force</span><span class="sxs-lookup"><span data-stu-id="51294-122">Force</span></span> | <span data-ttu-id="51294-123">Erzwingt, dass ein Paket deinstalliert werden, auch wenn andere Pakete von ihm abhängen.</span><span class="sxs-lookup"><span data-stu-id="51294-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="51294-124">"WhatIf"</span><span class="sxs-lookup"><span data-stu-id="51294-124">WhatIf</span></span> | <span data-ttu-id="51294-125">Zeigt an, was passieren würde, wenn der Befehl ausgeführt wird, ohne die Deinstallation ausführen.</span><span class="sxs-lookup"><span data-stu-id="51294-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="51294-126">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="51294-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="51294-127">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="51294-127">Common Parameters</span></span>

<span data-ttu-id="51294-128">`Uninstall-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="51294-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="51294-129">Beispiele</span><span class="sxs-lookup"><span data-stu-id="51294-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
