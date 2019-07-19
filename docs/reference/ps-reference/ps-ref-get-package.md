---
title: PowerShell-Referenz zu nuget-Paketen
description: Verweis auf den PowerShell-Befehl "Get-Package" in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 431e5f292f069ad5eb0c9f7f511d6b06810c8760
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327347"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="8e167-103">Get-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="8e167-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="8e167-104">*In diesem Thema wird der Befehl in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows beschrieben. Den allgemeinen PowerShell-Befehl Get-Package finden Sie in der [Referenz zu PowerShell packagemanagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="8e167-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="8e167-105">Ruft die Liste der im lokalen Repository installierten Pakete ab, listet bei der Verwendung mit dem Schalter "-listavailable" die Pakete auf, die in einer Paketquelle verfügbar sind, oder listet verfügbare Updates auf, wenn Sie mit dem Schalter-Update verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="8e167-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="8e167-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="8e167-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="8e167-107">Ohne Parameter zeigt die `Get-Package` Liste der Pakete an, die im Standard Projekt installiert sind.</span><span class="sxs-lookup"><span data-stu-id="8e167-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="8e167-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="8e167-108">Parameters</span></span>

| <span data-ttu-id="8e167-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="8e167-109">Parameter</span></span> | <span data-ttu-id="8e167-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8e167-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8e167-111">Source</span><span class="sxs-lookup"><span data-stu-id="8e167-111">Source</span></span> | <span data-ttu-id="8e167-112">Die URL oder der Ordner Pfad für das Paket.</span><span class="sxs-lookup"><span data-stu-id="8e167-112">The URL or folder path for the package .</span></span> <span data-ttu-id="8e167-113">Lokale Ordner Pfade können absolut oder relativ zum aktuellen Ordner sein.</span><span class="sxs-lookup"><span data-stu-id="8e167-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="8e167-114">Wenn kein Wert `Get-Package` angezeigt wird, wird die aktuell ausgewählte Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="8e167-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="8e167-115">Bei Verwendung mit-listavailable wird standardmäßig auf nuget.org festgelegt.</span><span class="sxs-lookup"><span data-stu-id="8e167-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="8e167-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="8e167-116">ListAvailable</span></span> | <span data-ttu-id="8e167-117">Listet die Pakete auf, die in einer Paketquelle verfügbar sind, und standardmäßig nuget.org. Zeigt einen Standardwert von 50-Paketen an, es sei denn, es werden-PageSize und/oder-First angegeben</span><span class="sxs-lookup"><span data-stu-id="8e167-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="8e167-118">Updates</span><span class="sxs-lookup"><span data-stu-id="8e167-118">Updates</span></span> | <span data-ttu-id="8e167-119">Listet Pakete auf, für die ein Update in der Paketquelle verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="8e167-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="8e167-120">ProjektName</span><span class="sxs-lookup"><span data-stu-id="8e167-120">ProjectName</span></span> | <span data-ttu-id="8e167-121">Das Projekt, aus dem installierte Pakete zu erhalten sind.</span><span class="sxs-lookup"><span data-stu-id="8e167-121">The project from which to get installed packages.</span></span> <span data-ttu-id="8e167-122">Wenn der Wert nicht angezeigt wird, gibt die installierten Projekte für die gesamte Projekt Mappe</span><span class="sxs-lookup"><span data-stu-id="8e167-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="8e167-123">Filter</span><span class="sxs-lookup"><span data-stu-id="8e167-123">Filter</span></span> | <span data-ttu-id="8e167-124">Eine Filter Zeichenfolge, die verwendet wird, um die Liste der Pakete einzugrenzen, indem Sie Sie auf die Paket-ID, die Beschreibung und Tags anwenden.</span><span class="sxs-lookup"><span data-stu-id="8e167-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="8e167-125">Erster</span><span class="sxs-lookup"><span data-stu-id="8e167-125">First</span></span> | <span data-ttu-id="8e167-126">Die Anzahl der Pakete, die vom Anfang der Liste zurückgegeben werden sollen.</span><span class="sxs-lookup"><span data-stu-id="8e167-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="8e167-127">Wenn nicht angegeben, wird standardmäßig 50 verwendet.</span><span class="sxs-lookup"><span data-stu-id="8e167-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="8e167-128">Skip</span><span class="sxs-lookup"><span data-stu-id="8e167-128">Skip</span></span> | <span data-ttu-id="8e167-129">Lässt die ersten &lt;int&gt; -Pakete aus der angezeigten Liste aus.</span><span class="sxs-lookup"><span data-stu-id="8e167-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="8e167-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="8e167-130">AllVersions</span></span> | <span data-ttu-id="8e167-131">Zeigt alle verfügbaren Versionen der einzelnen Pakete anstelle der neuesten Version an.</span><span class="sxs-lookup"><span data-stu-id="8e167-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="8e167-132">Incluabprerelease</span><span class="sxs-lookup"><span data-stu-id="8e167-132">IncludePrerelease</span></span> | <span data-ttu-id="8e167-133">Schließt vorab Pakete in die Ergebnisse ein.</span><span class="sxs-lookup"><span data-stu-id="8e167-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="8e167-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="8e167-134">PageSize</span></span> | <span data-ttu-id="8e167-135">*(3.0* und höher) Bei Verwendung mit-listavailable (erforderlich) die Anzahl der Pakete, die aufgelistet werden sollen, bevor eine Aufforderung zum Fortfahren angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="8e167-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="8e167-136">Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.</span><span class="sxs-lookup"><span data-stu-id="8e167-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="8e167-137">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="8e167-137">Common Parameters</span></span>

<span data-ttu-id="8e167-138">`Get-Package`unterstützt die folgenden [allgemeinen PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="8e167-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="8e167-139">Beispiele</span><span class="sxs-lookup"><span data-stu-id="8e167-139">Examples</span></span>

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
