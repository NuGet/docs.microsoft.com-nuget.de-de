---
title: NuGet-Open-PackagePage PowerShell-Referenz
description: Verweis für Open-PackagePage-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fd738f15b461051c4e9413b3035456c687979b97
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842264"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="b2432-103">Open-PackagePage (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="b2432-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="b2432-104">*In 3.0 und höher veraltet. verfügbar nur in der [-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="b2432-104">*Deprecated in 3.0+; available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="b2432-105">Startet den Standardbrowser mit dem Projekt, Lizenz oder Missbrauch Berichts-URL für das angegebene Paket.</span><span class="sxs-lookup"><span data-stu-id="b2432-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="b2432-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="b2432-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="b2432-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="b2432-107">Parameters</span></span>

| <span data-ttu-id="b2432-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="b2432-108">Parameter</span></span> | <span data-ttu-id="b2432-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="b2432-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b2432-110">Id</span><span class="sxs-lookup"><span data-stu-id="b2432-110">Id</span></span> | <span data-ttu-id="b2432-111">Die Paket-ID des gewünschten Pakets.</span><span class="sxs-lookup"><span data-stu-id="b2432-111">The package ID of the desired package.</span></span> <span data-ttu-id="b2432-112">Die - Id Switch selbst ist optional.</span><span class="sxs-lookup"><span data-stu-id="b2432-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="b2432-113">Version</span><span class="sxs-lookup"><span data-stu-id="b2432-113">Version</span></span> | <span data-ttu-id="b2432-114">Die Version des Pakets, standardmäßig auf die neueste Version.</span><span class="sxs-lookup"><span data-stu-id="b2432-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="b2432-115">Source</span><span class="sxs-lookup"><span data-stu-id="b2432-115">Source</span></span> | <span data-ttu-id="b2432-116">Der Paketquelle in die ausgewählte Datenquelle in der Quelle Dropdown-Standardwert.</span><span class="sxs-lookup"><span data-stu-id="b2432-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="b2432-117">Lizenz</span><span class="sxs-lookup"><span data-stu-id="b2432-117">License</span></span> | <span data-ttu-id="b2432-118">Öffnet den Browser mit des Pakets Lizenz-URL.</span><span class="sxs-lookup"><span data-stu-id="b2432-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="b2432-119">Wenn - Lizenz weder -ReportAbuse angegeben wird, öffnet der Browser der Pakets Projekt-URL an.</span><span class="sxs-lookup"><span data-stu-id="b2432-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="b2432-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="b2432-120">ReportAbuse</span></span> | <span data-ttu-id="b2432-121">Öffnet den Browser mit des Pakets URL für Bericht von Missbrauch.</span><span class="sxs-lookup"><span data-stu-id="b2432-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="b2432-122">Wenn - Lizenz weder -ReportAbuse angegeben wird, öffnet der Browser der Pakets Projekt-URL an.</span><span class="sxs-lookup"><span data-stu-id="b2432-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="b2432-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="b2432-123">PassThru</span></span> | <span data-ttu-id="b2432-124">Zeigt die URL an. Verwenden Sie unterdrückt werden, öffnen den Browser mit - WhatIf.</span><span class="sxs-lookup"><span data-stu-id="b2432-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="b2432-125">Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="b2432-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="b2432-126">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="b2432-126">Common Parameters</span></span>

<span data-ttu-id="b2432-127">`Open-PackagePage` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b2432-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="b2432-128">Beispiele</span><span class="sxs-lookup"><span data-stu-id="b2432-128">Examples</span></span>

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