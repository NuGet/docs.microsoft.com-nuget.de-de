---
title: NuGet-Open-PackagePage PowerShell-Referenz
description: Verweis für Open-PackagePage-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0325aa4ddd718a901dd6a09cdf86cae260e326ab
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547167"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="be789-103">Open-PackagePage (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="be789-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="be789-104">*In 3.0 und höher veraltet. verfügbar nur in der [NuGet-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="be789-104">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="be789-105">Startet den Standardbrowser mit dem Projekt, Lizenz oder Missbrauch Berichts-URL für das angegebene Paket.</span><span class="sxs-lookup"><span data-stu-id="be789-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="be789-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="be789-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="be789-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="be789-107">Parameters</span></span>

| <span data-ttu-id="be789-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="be789-108">Parameter</span></span> | <span data-ttu-id="be789-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="be789-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="be789-110">Id</span><span class="sxs-lookup"><span data-stu-id="be789-110">Id</span></span> | <span data-ttu-id="be789-111">Die Paket-ID des gewünschten Pakets.</span><span class="sxs-lookup"><span data-stu-id="be789-111">The package ID of the desired package.</span></span> <span data-ttu-id="be789-112">Die - Id Switch selbst ist optional.</span><span class="sxs-lookup"><span data-stu-id="be789-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="be789-113">Version</span><span class="sxs-lookup"><span data-stu-id="be789-113">Version</span></span> | <span data-ttu-id="be789-114">Die Version des Pakets, standardmäßig auf die neueste Version.</span><span class="sxs-lookup"><span data-stu-id="be789-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="be789-115">Quelle</span><span class="sxs-lookup"><span data-stu-id="be789-115">Source</span></span> | <span data-ttu-id="be789-116">Der Paketquelle in die ausgewählte Datenquelle in der Quelle Dropdown-Standardwert.</span><span class="sxs-lookup"><span data-stu-id="be789-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="be789-117">Lizenz</span><span class="sxs-lookup"><span data-stu-id="be789-117">License</span></span> | <span data-ttu-id="be789-118">Öffnet den Browser mit des Pakets Lizenz-URL.</span><span class="sxs-lookup"><span data-stu-id="be789-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="be789-119">Wenn - Lizenz weder -ReportAbuse angegeben wird, öffnet der Browser der Pakets Projekt-URL an.</span><span class="sxs-lookup"><span data-stu-id="be789-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="be789-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="be789-120">ReportAbuse</span></span> | <span data-ttu-id="be789-121">Öffnet den Browser mit des Pakets URL für Bericht von Missbrauch.</span><span class="sxs-lookup"><span data-stu-id="be789-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="be789-122">Wenn - Lizenz weder -ReportAbuse angegeben wird, öffnet der Browser der Pakets Projekt-URL an.</span><span class="sxs-lookup"><span data-stu-id="be789-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="be789-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="be789-123">PassThru</span></span> | <span data-ttu-id="be789-124">Zeigt die URL an. Verwenden Sie unterdrückt werden, öffnen den Browser mit - WhatIf.</span><span class="sxs-lookup"><span data-stu-id="be789-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="be789-125">Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="be789-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="be789-126">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="be789-126">Common Parameters</span></span>

<span data-ttu-id="be789-127">`Open-PackagePage` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="be789-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="be789-128">Beispiele</span><span class="sxs-lookup"><span data-stu-id="be789-128">Examples</span></span>

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```