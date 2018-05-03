---
title: NuGet-öffnen-PackagePage-PowerShell-Referenz
description: Referenz für Open PackagePage-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: df4bea390105a7e3fc5d2abd476f2908d92bbcf8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="548dd-103">Open-PackagePage (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="548dd-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="548dd-104">*In 3.0 veraltet. verfügbar nur innerhalb der [NuGet Package Manager Console](package-manager-console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="548dd-104">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="548dd-105">Startet den Standardbrowser mit dem Projekt, Lizenzen oder Missbrauch Berichts-URL für das angegebene Paket.</span><span class="sxs-lookup"><span data-stu-id="548dd-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="548dd-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="548dd-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="548dd-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="548dd-107">Parameters</span></span>

| <span data-ttu-id="548dd-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="548dd-108">Parameter</span></span> | <span data-ttu-id="548dd-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="548dd-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="548dd-110">Id</span><span class="sxs-lookup"><span data-stu-id="548dd-110">Id</span></span> | <span data-ttu-id="548dd-111">Die Paket-ID mit dem gewünschten Paket.</span><span class="sxs-lookup"><span data-stu-id="548dd-111">The package ID of the desired package.</span></span> <span data-ttu-id="548dd-112">Die - Id Schalter ist optional.</span><span class="sxs-lookup"><span data-stu-id="548dd-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="548dd-113">Version</span><span class="sxs-lookup"><span data-stu-id="548dd-113">Version</span></span> | <span data-ttu-id="548dd-114">Die Version des Pakets, auf die neueste Version auszuführen.</span><span class="sxs-lookup"><span data-stu-id="548dd-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="548dd-115">Quelle</span><span class="sxs-lookup"><span data-stu-id="548dd-115">Source</span></span> | <span data-ttu-id="548dd-116">Die ausgewählte Quelle in der Quelle Dropdownelement direktionales Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="548dd-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="548dd-117">Lizenz</span><span class="sxs-lookup"><span data-stu-id="548dd-117">License</span></span> | <span data-ttu-id="548dd-118">Öffnet den Browser, um des Pakets Lizenz-URL an.</span><span class="sxs-lookup"><span data-stu-id="548dd-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="548dd-119">Wenn - Lizenz weder -ReportAbuse angegeben wird, öffnet der Browser die Paket-Projekt-URL an.</span><span class="sxs-lookup"><span data-stu-id="548dd-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="548dd-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="548dd-120">ReportAbuse</span></span> | <span data-ttu-id="548dd-121">Öffnet den Browser, um des Pakets Berichts Missbrauch-URL an.</span><span class="sxs-lookup"><span data-stu-id="548dd-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="548dd-122">Wenn - Lizenz weder -ReportAbuse angegeben wird, öffnet der Browser die Paket-Projekt-URL an.</span><span class="sxs-lookup"><span data-stu-id="548dd-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="548dd-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="548dd-123">PassThru</span></span> | <span data-ttu-id="548dd-124">Zeigt die URL an. Verwenden Sie mit "-WhatIf" unterdrückt werden, öffnen den Browser.</span><span class="sxs-lookup"><span data-stu-id="548dd-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="548dd-125">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="548dd-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="548dd-126">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="548dd-126">Common Parameters</span></span>

<span data-ttu-id="548dd-127">`Open-PackagePage` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="548dd-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="548dd-128">Beispiele</span><span class="sxs-lookup"><span data-stu-id="548dd-128">Examples</span></span>

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