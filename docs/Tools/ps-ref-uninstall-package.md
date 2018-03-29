---
title: Deinstallieren Sie NuGet-Paket-PowerShell-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenz für Uninstall-Package-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
keywords: NuGet-Paket-Manager-Konsole NuGet Powershell-Befehle, NuGet Powershell-Referenz, Uninstall-Package
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: b53a36a6456522aa0d9d0d7cdf412de464ba9e08
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="20529-104">Uninstall-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="20529-104">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="20529-105">*In diesem Thema wird beschrieben, den Befehl innerhalb der [NuGet Package Manager Console](package-manager-console.md) in Visual Studio unter Windows. Der generische Deinstallationspaket für PowerShell-Befehl finden Sie unter der [PowerShell PackageManagement-Verweis](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="20529-105">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="20529-106">Entfernt ein Paket aus einem Projekt, und optional die abhängigen Elemente entfernen.</span><span class="sxs-lookup"><span data-stu-id="20529-106">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="20529-107">Wenn andere Pakete von diesem Paket abhängen, wird der Befehl fehl, es sei denn, der "– Force" angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="20529-107">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="20529-108">Syntax</span><span class="sxs-lookup"><span data-stu-id="20529-108">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="20529-109">Wenn andere Pakete von diesem Paket abhängen, wird der Befehl fehl, es sei denn, der "– Force" angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="20529-109">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="20529-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="20529-110">Parameters</span></span>

| <span data-ttu-id="20529-111">Parameter</span><span class="sxs-lookup"><span data-stu-id="20529-111">Parameter</span></span> | <span data-ttu-id="20529-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="20529-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="20529-113">Id</span><span class="sxs-lookup"><span data-stu-id="20529-113">Id</span></span> | <span data-ttu-id="20529-114">(Erforderlich) Der Bezeichner der zu deinstallierenden Pakets.</span><span class="sxs-lookup"><span data-stu-id="20529-114">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="20529-115">Die - Id Schalter ist optional.</span><span class="sxs-lookup"><span data-stu-id="20529-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="20529-116">Version</span><span class="sxs-lookup"><span data-stu-id="20529-116">Version</span></span> | <span data-ttu-id="20529-117">Die Version des Pakets zu deinstallieren, die derzeit installierte Version auszuführen.</span><span class="sxs-lookup"><span data-stu-id="20529-117">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="20529-118">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="20529-118">RemoveDependencies</span></span> | <span data-ttu-id="20529-119">Deinstallieren Sie das Paket und alle nicht verwendeten Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="20529-119">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="20529-120">D. h., wenn eine der Abhängigkeiten ein anderes Paket, das von ihm abhängig ist aufweist, wird sie übersprungen.</span><span class="sxs-lookup"><span data-stu-id="20529-120">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="20529-121">ProjektName</span><span class="sxs-lookup"><span data-stu-id="20529-121">ProjectName</span></span> | <span data-ttu-id="20529-122">Das Projekt, von dem das Paket, auf das Standardprojekt direktionales deinstalliert werden soll.</span><span class="sxs-lookup"><span data-stu-id="20529-122">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="20529-123">Force</span><span class="sxs-lookup"><span data-stu-id="20529-123">Force</span></span> | <span data-ttu-id="20529-124">Erzwingt, dass ein Paket deinstalliert werden, auch wenn andere Pakete von ihm abhängen.</span><span class="sxs-lookup"><span data-stu-id="20529-124">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="20529-125">WhatIf</span><span class="sxs-lookup"><span data-stu-id="20529-125">WhatIf</span></span> | <span data-ttu-id="20529-126">Zeigt an, was passieren würde, wenn der Befehl ausgeführt wird, ohne die Deinstallation ausführen.</span><span class="sxs-lookup"><span data-stu-id="20529-126">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="20529-127">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="20529-127">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="20529-128">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="20529-128">Common Parameters</span></span>

<span data-ttu-id="20529-129">`Uninstall-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="20529-129">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="20529-130">Beispiele</span><span class="sxs-lookup"><span data-stu-id="20529-130">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
