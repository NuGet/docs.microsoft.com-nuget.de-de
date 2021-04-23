---
title: NuGet Get-Package PowerShell-Referenz
description: Referenz zu Get-Package PowerShell-Befehl in der NuGet Paket-Manager Console in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7c91faecaac2967c7a01dd81e72b9097e7bd6cae
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901732"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="54a12-103">Get-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="54a12-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="54a12-104">*In diesem Thema wird der Befehl in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows beschrieben. Informationen zum generischen PowerShell Get-Package-Befehl finden Sie in der [PowerShell-PackageManagement-Referenz.](/powershell/module/packagemanagement)*</span><span class="sxs-lookup"><span data-stu-id="54a12-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="54a12-105">Ruft die Liste der pakete ab, die im lokalen Repository installiert sind, listet pakete auf, die von einer Paketquelle verfügbar sind, wenn sie mit dem Schalter -ListAvailable verwendet werden, oder listet verfügbare Updates auf, wenn sie mit dem Schalter -Update verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="54a12-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="54a12-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="54a12-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="54a12-107">Ohne Parameter zeigt die Liste der pakete an, `Get-Package` die im Standardprojekt installiert sind.</span><span class="sxs-lookup"><span data-stu-id="54a12-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="54a12-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="54a12-108">Parameters</span></span>

| <span data-ttu-id="54a12-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="54a12-109">Parameter</span></span> | <span data-ttu-id="54a12-110">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="54a12-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="54a12-111">`Source`</span><span class="sxs-lookup"><span data-stu-id="54a12-111">Source</span></span> | <span data-ttu-id="54a12-112">Die URL oder der Ordnerpfad für das Paket .</span><span class="sxs-lookup"><span data-stu-id="54a12-112">The URL or folder path for the package .</span></span> <span data-ttu-id="54a12-113">Lokale Ordnerpfade können absolut oder relativ zum aktuellen Ordner sein.</span><span class="sxs-lookup"><span data-stu-id="54a12-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="54a12-114">Wenn diese Option nicht angegeben ist, `Get-Package` wird die aktuell ausgewählte Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="54a12-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="54a12-115">Bei Verwendung mit -ListAvailable wird standardmäßig nuget.org.</span><span class="sxs-lookup"><span data-stu-id="54a12-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="54a12-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="54a12-116">ListAvailable</span></span> | <span data-ttu-id="54a12-117">Listet Pakete auf, die aus einer Paketquelle verfügbar sind, standardmäßig nuget.org. Zeigt den Standardwert von 50 Paketen an, es sei denn, -PageSize und/oder -First sind angegeben.</span><span class="sxs-lookup"><span data-stu-id="54a12-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="54a12-118">Aktualisierungen</span><span class="sxs-lookup"><span data-stu-id="54a12-118">Updates</span></span> | <span data-ttu-id="54a12-119">Listet Pakete auf, für die ein Update über die Paketquelle verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="54a12-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="54a12-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="54a12-120">ProjectName</span></span> | <span data-ttu-id="54a12-121">Das Projekt, aus dem installierte Pakete abzurufen sind.</span><span class="sxs-lookup"><span data-stu-id="54a12-121">The project from which to get installed packages.</span></span> <span data-ttu-id="54a12-122">Wenn keine Angabe erfolgt, werden installierte Projekte für die gesamte Projektmappe zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="54a12-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="54a12-123">Filter</span><span class="sxs-lookup"><span data-stu-id="54a12-123">Filter</span></span> | <span data-ttu-id="54a12-124">Eine Filterzeichenfolge, die verwendet wird, um die Liste der Pakete einzugrenzen, indem sie auf die Paket-ID, Beschreibung und Tags angewendet wird.</span><span class="sxs-lookup"><span data-stu-id="54a12-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="54a12-125">First</span><span class="sxs-lookup"><span data-stu-id="54a12-125">First</span></span> | <span data-ttu-id="54a12-126">Die Anzahl der Pakete, die am Anfang der Liste zurückgegeben werden sollen.</span><span class="sxs-lookup"><span data-stu-id="54a12-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="54a12-127">Wenn keine Angabe erfolgt, wird standardmäßig 50 verwendet.</span><span class="sxs-lookup"><span data-stu-id="54a12-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="54a12-128">Überspringen</span><span class="sxs-lookup"><span data-stu-id="54a12-128">Skip</span></span> | <span data-ttu-id="54a12-129">Lässt die ersten &lt; &gt; int-Pakete aus der angezeigten Liste aus.</span><span class="sxs-lookup"><span data-stu-id="54a12-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="54a12-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="54a12-130">AllVersions</span></span> | <span data-ttu-id="54a12-131">Zeigt alle verfügbaren Versionen jedes Pakets anstelle der neuesten Version an.</span><span class="sxs-lookup"><span data-stu-id="54a12-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="54a12-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="54a12-132">IncludePrerelease</span></span> | <span data-ttu-id="54a12-133">Schließt Vorabversionspakete in die Ergebnisse ein.</span><span class="sxs-lookup"><span data-stu-id="54a12-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="54a12-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="54a12-134">PageSize</span></span> | <span data-ttu-id="54a12-135">*(3.0 und mehr)* Bei Verwendung mit -ListAvailable (erforderlich) die Anzahl der Pakete, die vor der Eingabeaufforderung zum Fortfahren aufgeführt werden müssen.</span><span class="sxs-lookup"><span data-stu-id="54a12-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="54a12-136">Keiner dieser Parameter akzeptiert Pipelineeingaben oder Platzhalterzeichen.</span><span class="sxs-lookup"><span data-stu-id="54a12-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="54a12-137">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="54a12-137">Common Parameters</span></span>

<span data-ttu-id="54a12-138">`Get-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="54a12-138">`Get-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="54a12-139">Beispiele</span><span class="sxs-lookup"><span data-stu-id="54a12-139">Examples</span></span>

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```