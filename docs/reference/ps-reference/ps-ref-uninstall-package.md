---
title: Nuget-Deinstallations Paket PowerShell-Referenz
description: Referenz für den PowerShell-Befehl "Uninstall-Package" in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5c963588d28cab42e5fb6a43b31a17e26e49d0d2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327277"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="e80a5-103">Uninstall-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e80a5-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e80a5-104">*In diesem Thema wird der Befehl in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows beschrieben. Den allgemeinen PowerShell-Befehl "Uninstall-Package" finden Sie in der [Referenz zu PowerShell packagemanagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="e80a5-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="e80a5-105">Entfernt ein Paket aus einem Projekt und entfernt optional seine Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="e80a5-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="e80a5-106">Wenn andere Pakete von diesem Paket abhängen, schlägt der Befehl fehl, es sei denn, die Option – Force ist angegeben.</span><span class="sxs-lookup"><span data-stu-id="e80a5-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="e80a5-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="e80a5-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="e80a5-108">Wenn andere Pakete von diesem Paket abhängen, schlägt der Befehl fehl, es sei denn, die Option – Force ist angegeben.</span><span class="sxs-lookup"><span data-stu-id="e80a5-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="e80a5-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="e80a5-109">Parameters</span></span>

| <span data-ttu-id="e80a5-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="e80a5-110">Parameter</span></span> | <span data-ttu-id="e80a5-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="e80a5-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e80a5-112">Id</span><span class="sxs-lookup"><span data-stu-id="e80a5-112">Id</span></span> | <span data-ttu-id="e80a5-113">Benötigten Der Bezeichner des zu deinstallierenden Pakets.</span><span class="sxs-lookup"><span data-stu-id="e80a5-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="e80a5-114">Der Schalter-ID selbst ist optional.</span><span class="sxs-lookup"><span data-stu-id="e80a5-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="e80a5-115">Version</span><span class="sxs-lookup"><span data-stu-id="e80a5-115">Version</span></span> | <span data-ttu-id="e80a5-116">Die Version des zu deinstallierenden Pakets, wobei die aktuell installierte Version standardmäßig installiert ist.</span><span class="sxs-lookup"><span data-stu-id="e80a5-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="e80a5-117">Removeabhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="e80a5-117">RemoveDependencies</span></span> | <span data-ttu-id="e80a5-118">Deinstallieren Sie das Paket und seine nicht verwendeten Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="e80a5-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="e80a5-119">Das heißt, wenn eine Abhängigkeit über ein anderes Paket verfügt, das davon abhängt, wird Sie übersprungen.</span><span class="sxs-lookup"><span data-stu-id="e80a5-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="e80a5-120">ProjektName</span><span class="sxs-lookup"><span data-stu-id="e80a5-120">ProjectName</span></span> | <span data-ttu-id="e80a5-121">Das Projekt, aus dem das Paket deinstalliert werden soll, und standardmäßig das Standard Projekt.</span><span class="sxs-lookup"><span data-stu-id="e80a5-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="e80a5-122">Geltende</span><span class="sxs-lookup"><span data-stu-id="e80a5-122">Force</span></span> | <span data-ttu-id="e80a5-123">Erzwingt, dass ein Paket deinstalliert wird, auch wenn andere Pakete davon abhängig sind.</span><span class="sxs-lookup"><span data-stu-id="e80a5-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="e80a5-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="e80a5-124">WhatIf</span></span> | <span data-ttu-id="e80a5-125">Zeigt, was geschehen würde, wenn der Befehl ausgeführt wird, ohne die Deinstallation tatsächlich auszuführen.</span><span class="sxs-lookup"><span data-stu-id="e80a5-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="e80a5-126">Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.</span><span class="sxs-lookup"><span data-stu-id="e80a5-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e80a5-127">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="e80a5-127">Common Parameters</span></span>

<span data-ttu-id="e80a5-128">`Uninstall-Package`unterstützt die folgenden [allgemeinen PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e80a5-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e80a5-129">Beispiele</span><span class="sxs-lookup"><span data-stu-id="e80a5-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
