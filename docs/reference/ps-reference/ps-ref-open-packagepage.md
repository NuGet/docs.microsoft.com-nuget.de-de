---
title: Nuget-Open-PackagePage PowerShell-Referenz
description: Referenz für Open-PackagePage PowerShell-Befehl in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: ba90e09c017ec66d73c35a60025474bc77cf65a7
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238061"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="fd22f-103">Open-PackagePage (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="fd22f-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="fd22f-104">*Veraltet in 3.0 und höher nur in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows verfügbar.*</span><span class="sxs-lookup"><span data-stu-id="fd22f-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="fd22f-105">Hiermit wird der Standardbrowser mit der URL für das Projekt, die Lizenz oder den Berichts Missbrauch für das angegebene Paket gestartet.</span><span class="sxs-lookup"><span data-stu-id="fd22f-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="fd22f-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="fd22f-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="fd22f-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="fd22f-107">Parameters</span></span>

| <span data-ttu-id="fd22f-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="fd22f-108">Parameter</span></span> | <span data-ttu-id="fd22f-109">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="fd22f-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fd22f-110">Id</span><span class="sxs-lookup"><span data-stu-id="fd22f-110">Id</span></span> | <span data-ttu-id="fd22f-111">Die Paket-ID des gewünschten Pakets.</span><span class="sxs-lookup"><span data-stu-id="fd22f-111">The package ID of the desired package.</span></span> <span data-ttu-id="fd22f-112">Der Schalter-ID selbst ist optional.</span><span class="sxs-lookup"><span data-stu-id="fd22f-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="fd22f-113">Version</span><span class="sxs-lookup"><span data-stu-id="fd22f-113">Version</span></span> | <span data-ttu-id="fd22f-114">Die Version des Pakets, standardmäßig auf die neueste Version.</span><span class="sxs-lookup"><span data-stu-id="fd22f-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="fd22f-115">`Source`</span><span class="sxs-lookup"><span data-stu-id="fd22f-115">Source</span></span> | <span data-ttu-id="fd22f-116">Die Paketquelle, standardmäßig auf die ausgewählte Quelle in der Dropdown-Dropdown-Dropdown-Datei.</span><span class="sxs-lookup"><span data-stu-id="fd22f-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="fd22f-117">Lizenz</span><span class="sxs-lookup"><span data-stu-id="fd22f-117">License</span></span> | <span data-ttu-id="fd22f-118">Öffnet den Browser mit der Lizenz-URL des Pakets.</span><span class="sxs-lookup"><span data-stu-id="fd22f-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="fd22f-119">Wenn weder-License noch-Report Abuse angegeben ist, öffnet der Browser die Projekt-URL des Pakets.</span><span class="sxs-lookup"><span data-stu-id="fd22f-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="fd22f-120">Report Abuse</span><span class="sxs-lookup"><span data-stu-id="fd22f-120">ReportAbuse</span></span> | <span data-ttu-id="fd22f-121">Öffnet den Browser mit der Berichts Missbrauch-URL des Pakets.</span><span class="sxs-lookup"><span data-stu-id="fd22f-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="fd22f-122">Wenn weder-License noch-Report Abuse angegeben ist, öffnet der Browser die Projekt-URL des Pakets.</span><span class="sxs-lookup"><span data-stu-id="fd22f-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="fd22f-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="fd22f-123">PassThru</span></span> | <span data-ttu-id="fd22f-124">Zeigt die URL an. Verwenden Sie with-WhatIf, um das Öffnen des Browsers zu unterdrücken.</span><span class="sxs-lookup"><span data-stu-id="fd22f-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="fd22f-125">Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.</span><span class="sxs-lookup"><span data-stu-id="fd22f-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="fd22f-126">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="fd22f-126">Common Parameters</span></span>

<span data-ttu-id="fd22f-127">`Open-PackagePage` unterstützt die folgenden [allgemeinen PowerShell-Parameter](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="fd22f-127">`Open-PackagePage` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="fd22f-128">Beispiele</span><span class="sxs-lookup"><span data-stu-id="fd22f-128">Examples</span></span>

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