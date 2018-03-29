---
title: NuGet-Get-Projekt-PowerShell-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenz für GetProject-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
keywords: NuGet-Paket-Manager-Konsole NuGet Powershell-Befehle, NuGet Powershell-Referenz, Get-Projekt
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9fcdcf7c550408cd7dfd73787ee14821c46a1df9
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="9db71-104">Get-Projekt (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="9db71-104">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="9db71-105">*Verfügbar nur innerhalb der [NuGet Package Manager Console](package-manager-console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="9db71-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="9db71-106">Zeigt Informationen zu den Standardwert oder die angegebene Projekt.</span><span class="sxs-lookup"><span data-stu-id="9db71-106">Displays information about the default or specified project.</span></span> <span data-ttu-id="9db71-107">`Get-Project` insbesondere gibt eine "Referent" mit dem Visual Studio DTE (Development Tools Environment)-Objekt für das Projekt ein.</span><span class="sxs-lookup"><span data-stu-id="9db71-107">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="9db71-108">Syntax</span><span class="sxs-lookup"><span data-stu-id="9db71-108">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="9db71-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="9db71-109">Parameters</span></span>

| <span data-ttu-id="9db71-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="9db71-110">Parameter</span></span> | <span data-ttu-id="9db71-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9db71-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9db71-112">name</span><span class="sxs-lookup"><span data-stu-id="9db71-112">Name</span></span> | <span data-ttu-id="9db71-113">Gibt an, dass das Projekt, um anzuzeigen, in der Paket-Manager-Konsole ausgewählte Standardprojekt auszuführen.</span><span class="sxs-lookup"><span data-stu-id="9db71-113">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="9db71-114">Der - Name Switch ist selbst optional.</span><span class="sxs-lookup"><span data-stu-id="9db71-114">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="9db71-115">Alle</span><span class="sxs-lookup"><span data-stu-id="9db71-115">All</span></span> | <span data-ttu-id="9db71-116">Zeigt Informationen für jedes Projekt in der Projektmappe an. die Reihenfolge der Projekte ist nicht deterministisch.</span><span class="sxs-lookup"><span data-stu-id="9db71-116">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="9db71-117">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="9db71-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="9db71-118">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="9db71-118">Common Parameters</span></span>

<span data-ttu-id="9db71-119">`Get-Project` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9db71-119">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="9db71-120">Beispiele</span><span class="sxs-lookup"><span data-stu-id="9db71-120">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```