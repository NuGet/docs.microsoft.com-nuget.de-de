---
title: NuGet Find-Package-PowerShell-Referenz
description: Referenz für die Find-Package-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: fee0ad0496f27d0796eddf177edc235bcb10da70
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842523"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="29212-103">Find-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="29212-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="29212-104">*Version 3.0 und höher; In diesem Thema wird beschrieben, den Befehl in der [-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows. Der generische PowerShell Find-Package-Befehl finden Sie unter den [PowerShell PackageManagement-Verweis](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="29212-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="29212-105">Ruft die remotepakete mit der angegebenen ID oder Schlüsselwörter aus der Paketquelle ab.</span><span class="sxs-lookup"><span data-stu-id="29212-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="29212-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="29212-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="29212-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="29212-107">Parameters</span></span>

| <span data-ttu-id="29212-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="29212-108">Parameter</span></span> | <span data-ttu-id="29212-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="29212-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="29212-110">ID &lt;Schlüsselwörter&gt;</span><span class="sxs-lookup"><span data-stu-id="29212-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="29212-111">(Erforderlich) Schlüsselwörter aufgelistet, die bei der Suche von der Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="29212-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="29212-112">Verwenden Sie-"exactMatch", um nur die Pakete zurückzugeben, dessen Paket-ID, die Schlüsselwörter entspricht.</span><span class="sxs-lookup"><span data-stu-id="29212-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="29212-113">Wenn keine Schlüsselwörter angegeben sind, `Find-Package` gibt eine Liste der Top-20-Pakete durch Downloads oder die Anzahl anhand des - ersten.</span><span class="sxs-lookup"><span data-stu-id="29212-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="29212-114">Beachten Sie, dass - Id optional ist und keine Aktion.</span><span class="sxs-lookup"><span data-stu-id="29212-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="29212-115">Source</span><span class="sxs-lookup"><span data-stu-id="29212-115">Source</span></span> | <span data-ttu-id="29212-116">Der URL oder Ordner Pfad für die Paketquelle, um zu suchen.</span><span class="sxs-lookup"><span data-stu-id="29212-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="29212-117">Lokalen Ordnerpfade können absolut oder relativ zum aktuellen Ordner sein.</span><span class="sxs-lookup"><span data-stu-id="29212-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="29212-118">Wenn nicht angegeben, `Find-Package` die aktuell ausgewählte Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="29212-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="29212-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="29212-119">AllVersions</span></span> | <span data-ttu-id="29212-120">Zeigt alle verfügbare Versionen der einzelnen Pakete, anstatt nur die neueste Version.</span><span class="sxs-lookup"><span data-stu-id="29212-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="29212-121">Erster</span><span class="sxs-lookup"><span data-stu-id="29212-121">First</span></span> | <span data-ttu-id="29212-122">Die Anzahl von Paketen ab dem Anfang der Liste zurückgegeben werden soll; Der Standardwert ist 20.</span><span class="sxs-lookup"><span data-stu-id="29212-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="29212-123">Skip</span><span class="sxs-lookup"><span data-stu-id="29212-123">Skip</span></span> | <span data-ttu-id="29212-124">Lässt die erste &lt;Int&gt; Pakete aus der angezeigten Liste.</span><span class="sxs-lookup"><span data-stu-id="29212-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="29212-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="29212-125">IncludePrerelease</span></span> | <span data-ttu-id="29212-126">Enthält Vorabversionen von Paketen in den Ergebnissen.</span><span class="sxs-lookup"><span data-stu-id="29212-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="29212-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="29212-127">ExactMatch</span></span> | <span data-ttu-id="29212-128">Verwendung von angegebenen &lt;Schlüsselwörter&gt; als Groß-/Kleinschreibung Paket-ID</span><span class="sxs-lookup"><span data-stu-id="29212-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="29212-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="29212-129">StartWith</span></span> | <span data-ttu-id="29212-130">Gibt Pakete, deren Paket-ID beginnt mit &lt;Schlüsselwörter&gt;.</span><span class="sxs-lookup"><span data-stu-id="29212-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="29212-131">Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="29212-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="29212-132">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="29212-132">Common Parameters</span></span>

<span data-ttu-id="29212-133">`Find-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="29212-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="29212-134">Beispiele</span><span class="sxs-lookup"><span data-stu-id="29212-134">Examples</span></span>

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
