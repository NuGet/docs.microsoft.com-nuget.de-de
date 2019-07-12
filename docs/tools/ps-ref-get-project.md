---
title: NuGet-Get-Projekt-PowerShell-Referenz
description: Referenz für GetProject-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 2ceb1557eafd213c148d3ab870925ef5bbbee145
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842278"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="3c14a-103">Get-Project (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="3c14a-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3c14a-104">*Verfügbar nur in der [-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="3c14a-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="3c14a-105">Zeigt Informationen zu den Standardwert oder die angegebene Projekt.</span><span class="sxs-lookup"><span data-stu-id="3c14a-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="3c14a-106">`Get-Project` insbesondere gibt eine Referent auf das Visual Studio DTE (Development Tools Environment)-Objekt, für das Projekt ein.</span><span class="sxs-lookup"><span data-stu-id="3c14a-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="3c14a-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="3c14a-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="3c14a-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="3c14a-108">Parameters</span></span>

| <span data-ttu-id="3c14a-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="3c14a-109">Parameter</span></span> | <span data-ttu-id="3c14a-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3c14a-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3c14a-111">Name</span><span class="sxs-lookup"><span data-stu-id="3c14a-111">Name</span></span> | <span data-ttu-id="3c14a-112">Gibt an, dass das Projekt angezeigt werden, als das standardmäßige-Projekt in der Paket-Manager-Konsole ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="3c14a-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="3c14a-113">Der - Name Schalter ist selbst optional.</span><span class="sxs-lookup"><span data-stu-id="3c14a-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="3c14a-114">All</span><span class="sxs-lookup"><span data-stu-id="3c14a-114">All</span></span> | <span data-ttu-id="3c14a-115">Zeigt Informationen für jedes Projekt in der Projektmappe die Reihenfolge der Projekte ist nicht deterministisch.</span><span class="sxs-lookup"><span data-stu-id="3c14a-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="3c14a-116">Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="3c14a-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3c14a-117">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="3c14a-117">Common Parameters</span></span>

<span data-ttu-id="3c14a-118">`Get-Project` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3c14a-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3c14a-119">Beispiele</span><span class="sxs-lookup"><span data-stu-id="3c14a-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```