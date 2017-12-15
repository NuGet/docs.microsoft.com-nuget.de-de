---
title: NuGet-Get-Projekt-PowerShell-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 09c10ea3-ba26-4bfa-999e-de5350e6e920
description: "Referenz für GetProject-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio."
keywords: NuGet-Paket-Manager-Konsole NuGet Powershell-Befehle, NuGet Powershell-Referenz, Get-Projekt
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 40c986164c3f6bd6a02877e15827541aae77d8ad
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="3192c-104">Get-Projekt (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="3192c-104">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3192c-105">*Verfügbar nur innerhalb der [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="3192c-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="3192c-106">Zeigt Informationen zu den Standardwert oder die angegebene Projekt.</span><span class="sxs-lookup"><span data-stu-id="3192c-106">Displays information about the default or specified project.</span></span> <span data-ttu-id="3192c-107">`Get-Project`insbesondere gibt eine "Referent" mit dem Visual Studio DTE (Development Tools Environment)-Objekt für das Projekt ein.</span><span class="sxs-lookup"><span data-stu-id="3192c-107">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="3192c-108">Syntax</span><span class="sxs-lookup"><span data-stu-id="3192c-108">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="3192c-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="3192c-109">Parameters</span></span>

| <span data-ttu-id="3192c-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="3192c-110">Parameter</span></span> | <span data-ttu-id="3192c-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3192c-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3192c-112">Name</span><span class="sxs-lookup"><span data-stu-id="3192c-112">Name</span></span> | <span data-ttu-id="3192c-113">Gibt an, dass das Projekt, um anzuzeigen, in der Paket-Manager-Konsole ausgewählte Standardprojekt auszuführen.</span><span class="sxs-lookup"><span data-stu-id="3192c-113">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="3192c-114">Der - Name Switch ist selbst optional.</span><span class="sxs-lookup"><span data-stu-id="3192c-114">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="3192c-115">Alle</span><span class="sxs-lookup"><span data-stu-id="3192c-115">All</span></span> | <span data-ttu-id="3192c-116">Zeigt Informationen für jedes Projekt in der Projektmappe an. die Reihenfolge der Projekte ist nicht deterministisch.</span><span class="sxs-lookup"><span data-stu-id="3192c-116">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="3192c-117">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="3192c-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3192c-118">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="3192c-118">Common Parameters</span></span>

<span data-ttu-id="3192c-119">`Get-Project`unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3192c-119">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3192c-120">Beispiele</span><span class="sxs-lookup"><span data-stu-id="3192c-120">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```