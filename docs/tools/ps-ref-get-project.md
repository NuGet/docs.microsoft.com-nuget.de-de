---
title: NuGet-Get-Projekt-PowerShell-Referenz
description: Referenz für GetProject-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 849261711fafcadbab38bf6fe99340c4b79e1e21
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550436"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="835f4-103">Get-Project (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="835f4-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="835f4-104">*Verfügbar nur in der [NuGet-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="835f4-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="835f4-105">Zeigt Informationen zu den Standardwert oder die angegebene Projekt.</span><span class="sxs-lookup"><span data-stu-id="835f4-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="835f4-106">`Get-Project` insbesondere gibt eine Referent auf das Visual Studio DTE (Development Tools Environment)-Objekt, für das Projekt ein.</span><span class="sxs-lookup"><span data-stu-id="835f4-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="835f4-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="835f4-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="835f4-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="835f4-108">Parameters</span></span>

| <span data-ttu-id="835f4-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="835f4-109">Parameter</span></span> | <span data-ttu-id="835f4-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="835f4-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="835f4-111">name</span><span class="sxs-lookup"><span data-stu-id="835f4-111">Name</span></span> | <span data-ttu-id="835f4-112">Gibt an, dass das Projekt angezeigt werden, als das standardmäßige-Projekt in der Paket-Manager-Konsole ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="835f4-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="835f4-113">Der - Name Schalter ist selbst optional.</span><span class="sxs-lookup"><span data-stu-id="835f4-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="835f4-114">Alle</span><span class="sxs-lookup"><span data-stu-id="835f4-114">All</span></span> | <span data-ttu-id="835f4-115">Zeigt Informationen für jedes Projekt in der Projektmappe die Reihenfolge der Projekte ist nicht deterministisch.</span><span class="sxs-lookup"><span data-stu-id="835f4-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="835f4-116">Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="835f4-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="835f4-117">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="835f4-117">Common Parameters</span></span>

<span data-ttu-id="835f4-118">`Get-Project` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="835f4-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="835f4-119">Beispiele</span><span class="sxs-lookup"><span data-stu-id="835f4-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```