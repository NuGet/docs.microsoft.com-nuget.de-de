---
title: PowerShell-Referenz zu nuget-Project
description: Referenz für den getproject PowerShell-Befehl in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 3343952535c2d3c822f5cac24cb30c8f5bfa5be3
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384619"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="16da9-103">Get-Project (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="16da9-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="16da9-104">*Nur in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows verfügbar.*</span><span class="sxs-lookup"><span data-stu-id="16da9-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="16da9-105">Zeigt Informationen zum Standard-oder angegebenen Projekt an.</span><span class="sxs-lookup"><span data-stu-id="16da9-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="16da9-106">`Get-Project` gibt speziell einen Referenten für das Visual Studio-DTE-Objekt (Development Tools Environment) für das Projekt zurück.</span><span class="sxs-lookup"><span data-stu-id="16da9-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="16da9-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="16da9-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="16da9-108">Parameters</span><span class="sxs-lookup"><span data-stu-id="16da9-108">Parameters</span></span>

| <span data-ttu-id="16da9-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="16da9-109">Parameter</span></span> | <span data-ttu-id="16da9-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="16da9-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="16da9-111">-Name</span><span class="sxs-lookup"><span data-stu-id="16da9-111">Name</span></span> | <span data-ttu-id="16da9-112">Gibt das anzuzeigende Projekt an. das Standard Projekt, das in der Paket-Manager-Konsole ausgewählt ist, wird standardmäßig angezeigt.</span><span class="sxs-lookup"><span data-stu-id="16da9-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="16da9-113">Der Schalter "-Name" ist optional.</span><span class="sxs-lookup"><span data-stu-id="16da9-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="16da9-114">Alle</span><span class="sxs-lookup"><span data-stu-id="16da9-114">All</span></span> | <span data-ttu-id="16da9-115">Zeigt Informationen für jedes Projekt in der Projekt Mappe an. die Reihenfolge der Projekte ist nicht deterministisch.</span><span class="sxs-lookup"><span data-stu-id="16da9-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="16da9-116">Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.</span><span class="sxs-lookup"><span data-stu-id="16da9-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="16da9-117">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="16da9-117">Common Parameters</span></span>

<span data-ttu-id="16da9-118">`Get-Project` unterstützt die folgenden [allgemeinen PowerShell-Parameter](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="16da9-118">`Get-Project` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="16da9-119">Beispiele</span><span class="sxs-lookup"><span data-stu-id="16da9-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```