---
title: Nuget-Get-Project PowerShell-Referenz
description: Referenz für den getproject PowerShell-Befehl in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 6d9e1d48c8e1838f193878cab3483b1bfba7d7f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238074"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="3f348-103">Get-Project (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="3f348-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3f348-104">*Nur in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows verfügbar.*</span><span class="sxs-lookup"><span data-stu-id="3f348-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="3f348-105">Zeigt Informationen zum Standard-oder angegebenen Projekt an.</span><span class="sxs-lookup"><span data-stu-id="3f348-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="3f348-106">`Get-Project` gibt speziell einen Referenten für das Visual Studio DTE-Objekt (Development Tools Environment) für das Projekt zurück.</span><span class="sxs-lookup"><span data-stu-id="3f348-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="3f348-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="3f348-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="3f348-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="3f348-108">Parameters</span></span>

| <span data-ttu-id="3f348-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="3f348-109">Parameter</span></span> | <span data-ttu-id="3f348-110">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="3f348-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3f348-111">Name</span><span class="sxs-lookup"><span data-stu-id="3f348-111">Name</span></span> | <span data-ttu-id="3f348-112">Gibt das anzuzeigende Projekt an. das Standard Projekt, das in der Paket-Manager-Konsole ausgewählt ist, wird standardmäßig angezeigt.</span><span class="sxs-lookup"><span data-stu-id="3f348-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="3f348-113">Der Schalter "-Name" ist optional.</span><span class="sxs-lookup"><span data-stu-id="3f348-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="3f348-114">Alle</span><span class="sxs-lookup"><span data-stu-id="3f348-114">All</span></span> | <span data-ttu-id="3f348-115">Zeigt Informationen für jedes Projekt in der Projekt Mappe an. die Reihenfolge der Projekte ist nicht deterministisch.</span><span class="sxs-lookup"><span data-stu-id="3f348-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="3f348-116">Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.</span><span class="sxs-lookup"><span data-stu-id="3f348-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3f348-117">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="3f348-117">Common Parameters</span></span>

<span data-ttu-id="3f348-118">`Get-Project` unterstützt die folgenden [allgemeinen PowerShell-Parameter](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3f348-118">`Get-Project` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3f348-119">Beispiele</span><span class="sxs-lookup"><span data-stu-id="3f348-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```