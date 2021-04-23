---
title: NuGet Find-Package PowerShell-Referenz
description: Referenz zu Find-Package PowerShell-Befehl in der NuGet Paket-Manager Console in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 263835da64340a13737b32ab54ab057cb640a080
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901758"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="70fc9-103">Find-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="70fc9-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="70fc9-104">*Version 3.0+; In diesem Thema wird der Befehl in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows beschrieben. Informationen zum generischen PowerShell Find-Package-Befehl finden Sie in der [PowerShell-PackageManagement-Referenz.](/powershell/module/packagemanagement)*</span><span class="sxs-lookup"><span data-stu-id="70fc9-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="70fc9-105">Ruft den Satz von Remotepaketen mit der angegebenen ID oder den angegebenen Schlüsselwörtern aus der Paketquelle ab.</span><span class="sxs-lookup"><span data-stu-id="70fc9-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="70fc9-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="70fc9-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="70fc9-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="70fc9-107">Parameters</span></span>

| <span data-ttu-id="70fc9-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="70fc9-108">Parameter</span></span> | <span data-ttu-id="70fc9-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="70fc9-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="70fc9-110">&lt;ID-Schlüsselwörter&gt;</span><span class="sxs-lookup"><span data-stu-id="70fc9-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="70fc9-111">(Erforderlich) Schlüsselwörter, die beim Durchsuchen der Paketquelle verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="70fc9-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="70fc9-112">Verwenden Sie -ExactMatch, um nur die Pakete zurückzugeben, deren Paket-ID mit den Schlüsselwörtern übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="70fc9-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="70fc9-113">Wenn keine Schlüsselwörter angegeben werden, `Find-Package` gibt eine Liste der 20 wichtigsten Pakete nach Downloads oder die von -First angegebene Anzahl zurück.</span><span class="sxs-lookup"><span data-stu-id="70fc9-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="70fc9-114">Beachten Sie, dass -Id optional und no-op ist.</span><span class="sxs-lookup"><span data-stu-id="70fc9-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="70fc9-115">`Source`</span><span class="sxs-lookup"><span data-stu-id="70fc9-115">Source</span></span> | <span data-ttu-id="70fc9-116">Die URL oder der Ordnerpfad für die zu durchsuchende Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="70fc9-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="70fc9-117">Lokale Ordnerpfade können absolut oder relativ zum aktuellen Ordner sein.</span><span class="sxs-lookup"><span data-stu-id="70fc9-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="70fc9-118">Wenn diese Option nicht angegeben ist, `Find-Package` wird die aktuell ausgewählte Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="70fc9-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="70fc9-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="70fc9-119">AllVersions</span></span> | <span data-ttu-id="70fc9-120">Zeigt alle verfügbaren Versionen jedes Pakets anstelle der neuesten Version an.</span><span class="sxs-lookup"><span data-stu-id="70fc9-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="70fc9-121">First</span><span class="sxs-lookup"><span data-stu-id="70fc9-121">First</span></span> | <span data-ttu-id="70fc9-122">Die Anzahl der Pakete, die am Anfang der Liste zurückgegeben werden sollen. der Standardwert ist 20.</span><span class="sxs-lookup"><span data-stu-id="70fc9-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="70fc9-123">Überspringen</span><span class="sxs-lookup"><span data-stu-id="70fc9-123">Skip</span></span> | <span data-ttu-id="70fc9-124">Lässt die ersten &lt; &gt; int-Pakete aus der angezeigten Liste aus.</span><span class="sxs-lookup"><span data-stu-id="70fc9-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="70fc9-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="70fc9-125">IncludePrerelease</span></span> | <span data-ttu-id="70fc9-126">Schließt Vorabversionspakete in die Ergebnisse ein.</span><span class="sxs-lookup"><span data-stu-id="70fc9-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="70fc9-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="70fc9-127">ExactMatch</span></span> | <span data-ttu-id="70fc9-128">Wird angegeben, um Schlüsselwörter als Paket-ID zu verwenden, bei der &lt; &gt; die Groß-/Kleinschreibung beachtet wird.</span><span class="sxs-lookup"><span data-stu-id="70fc9-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="70fc9-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="70fc9-129">StartWith</span></span> | <span data-ttu-id="70fc9-130">Gibt Pakete zurück, deren Paket-ID mit den Schlüsselwörtern &lt; &gt; beginnt.</span><span class="sxs-lookup"><span data-stu-id="70fc9-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="70fc9-131">Keiner dieser Parameter akzeptiert Pipelineeingaben oder Platzhalterzeichen.</span><span class="sxs-lookup"><span data-stu-id="70fc9-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="70fc9-132">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="70fc9-132">Common Parameters</span></span>

<span data-ttu-id="70fc9-133">`Find-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="70fc9-133">`Find-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="70fc9-134">Beispiele</span><span class="sxs-lookup"><span data-stu-id="70fc9-134">Examples</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```