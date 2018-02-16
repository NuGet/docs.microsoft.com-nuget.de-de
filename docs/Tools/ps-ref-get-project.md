---
title: NuGet-Get-Projekt-PowerShell-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für GetProject-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio."
keywords: NuGet-Paket-Manager-Konsole NuGet Powershell-Befehle, NuGet Powershell-Referenz, Get-Projekt
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c347a6104d89bb29626ad7c2f33bec150eb38cd2
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/14/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="408e6-104">Get-Projekt (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="408e6-104">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="408e6-105">*Verfügbar nur innerhalb der [NuGet Package Manager Console](package-manager-console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="408e6-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="408e6-106">Zeigt Informationen zu den Standardwert oder die angegebene Projekt.</span><span class="sxs-lookup"><span data-stu-id="408e6-106">Displays information about the default or specified project.</span></span> <span data-ttu-id="408e6-107">`Get-Project` insbesondere gibt eine "Referent" mit dem Visual Studio DTE (Development Tools Environment)-Objekt für das Projekt ein.</span><span class="sxs-lookup"><span data-stu-id="408e6-107">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="408e6-108">Syntax</span><span class="sxs-lookup"><span data-stu-id="408e6-108">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="408e6-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="408e6-109">Parameters</span></span>

| <span data-ttu-id="408e6-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="408e6-110">Parameter</span></span> | <span data-ttu-id="408e6-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="408e6-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="408e6-112">name</span><span class="sxs-lookup"><span data-stu-id="408e6-112">Name</span></span> | <span data-ttu-id="408e6-113">Gibt an, dass das Projekt, um anzuzeigen, in der Paket-Manager-Konsole ausgewählte Standardprojekt auszuführen.</span><span class="sxs-lookup"><span data-stu-id="408e6-113">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="408e6-114">Der - Name Switch ist selbst optional.</span><span class="sxs-lookup"><span data-stu-id="408e6-114">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="408e6-115">Alle</span><span class="sxs-lookup"><span data-stu-id="408e6-115">All</span></span> | <span data-ttu-id="408e6-116">Zeigt Informationen für jedes Projekt in der Projektmappe an. die Reihenfolge der Projekte ist nicht deterministisch.</span><span class="sxs-lookup"><span data-stu-id="408e6-116">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="408e6-117">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="408e6-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="408e6-118">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="408e6-118">Common Parameters</span></span>

<span data-ttu-id="408e6-119">`Get-Project` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="408e6-119">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="408e6-120">Beispiele</span><span class="sxs-lookup"><span data-stu-id="408e6-120">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```