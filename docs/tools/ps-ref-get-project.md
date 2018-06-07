---
title: NuGet-Get-Projekt-PowerShell-Referenz
description: Referenz für GetProject-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: afdf9f762bbd34531f9d9093238a2fed27e3f4d3
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817755"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="ec761-103">Get-Project (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="ec761-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ec761-104">*Verfügbar nur innerhalb der [NuGet Package Manager Console](package-manager-console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="ec761-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="ec761-105">Zeigt Informationen zu den Standardwert oder die angegebene Projekt.</span><span class="sxs-lookup"><span data-stu-id="ec761-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="ec761-106">`Get-Project` insbesondere gibt eine "Referent" mit dem Visual Studio DTE (Development Tools Environment)-Objekt für das Projekt ein.</span><span class="sxs-lookup"><span data-stu-id="ec761-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="ec761-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="ec761-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="ec761-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="ec761-108">Parameters</span></span>

| <span data-ttu-id="ec761-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="ec761-109">Parameter</span></span> | <span data-ttu-id="ec761-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="ec761-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ec761-111">name</span><span class="sxs-lookup"><span data-stu-id="ec761-111">Name</span></span> | <span data-ttu-id="ec761-112">Gibt an, dass das Projekt, um anzuzeigen, in der Paket-Manager-Konsole ausgewählte Standardprojekt auszuführen.</span><span class="sxs-lookup"><span data-stu-id="ec761-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="ec761-113">Der - Name Switch ist selbst optional.</span><span class="sxs-lookup"><span data-stu-id="ec761-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="ec761-114">Alle</span><span class="sxs-lookup"><span data-stu-id="ec761-114">All</span></span> | <span data-ttu-id="ec761-115">Zeigt Informationen für jedes Projekt in der Projektmappe an. die Reihenfolge der Projekte ist nicht deterministisch.</span><span class="sxs-lookup"><span data-stu-id="ec761-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="ec761-116">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="ec761-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ec761-117">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="ec761-117">Common Parameters</span></span>

<span data-ttu-id="ec761-118">`Get-Project` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="ec761-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ec761-119">Beispiele</span><span class="sxs-lookup"><span data-stu-id="ec761-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```