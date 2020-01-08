---
title: PowerShell-Referenz zu nuget-PowerShell-Paketen
description: Referenz für den PowerShell-Befehl "Find-Package" in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4118b5a38f80a2300b3945738315d56bda096f9a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384632"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="41257-103">Find-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="41257-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="41257-104">*Version 3.0 und höher in diesem Thema wird der Befehl in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows beschrieben. Den allgemeinen PowerShell-Befehl "Find-Package" finden Sie in der [Referenz zu PowerShell packagemanagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="41257-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="41257-105">Ruft den Satz von Remote Paketen mit der angegebenen ID oder den angegebenen Schlüsselwörtern aus der Paketquelle ab.</span><span class="sxs-lookup"><span data-stu-id="41257-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="41257-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="41257-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="41257-107">Parameters</span><span class="sxs-lookup"><span data-stu-id="41257-107">Parameters</span></span>

| <span data-ttu-id="41257-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="41257-108">Parameter</span></span> | <span data-ttu-id="41257-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="41257-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="41257-110">ID &lt;Schlüsselwörter&gt;</span><span class="sxs-lookup"><span data-stu-id="41257-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="41257-111">Benötigten Schlüsselwörter, die beim Durchsuchen der Paketquelle verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="41257-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="41257-112">Verwenden Sie-exactMatch, um nur Pakete zurückzugeben, deren Paket-ID mit den Schlüsselwörtern übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="41257-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="41257-113">Wenn keine Schlüsselwörter angegeben werden, gibt `Find-Package` eine Liste mit den ersten 20 Paketen nach Downloads oder die durch-First angegebene Zahl zurück.</span><span class="sxs-lookup"><span data-stu-id="41257-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="41257-114">Beachten Sie, dass-ID optional und ein No-op-Wert ist.</span><span class="sxs-lookup"><span data-stu-id="41257-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="41257-115">Quelle</span><span class="sxs-lookup"><span data-stu-id="41257-115">Source</span></span> | <span data-ttu-id="41257-116">Die URL oder der Ordner Pfad für die Paketquelle, die durchsucht werden soll.</span><span class="sxs-lookup"><span data-stu-id="41257-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="41257-117">Lokale Ordner Pfade können absolut oder relativ zum aktuellen Ordner sein.</span><span class="sxs-lookup"><span data-stu-id="41257-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="41257-118">Wenn der Wert weggelassen wird, wird `Find-Package` die aktuell ausgewählte Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="41257-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="41257-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="41257-119">AllVersions</span></span> | <span data-ttu-id="41257-120">Zeigt alle verfügbaren Versionen der einzelnen Pakete anstelle der neuesten Version an.</span><span class="sxs-lookup"><span data-stu-id="41257-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="41257-121">Erster</span><span class="sxs-lookup"><span data-stu-id="41257-121">First</span></span> | <span data-ttu-id="41257-122">Die Anzahl der Pakete, die ab dem Anfang der Liste zurückgegeben werden sollen. der Standardwert ist 20.</span><span class="sxs-lookup"><span data-stu-id="41257-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="41257-123">Überspringen</span><span class="sxs-lookup"><span data-stu-id="41257-123">Skip</span></span> | <span data-ttu-id="41257-124">Lässt das erste &lt;int&gt; Paketen aus der angezeigten Liste aus.</span><span class="sxs-lookup"><span data-stu-id="41257-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="41257-125">Incluabprerelease</span><span class="sxs-lookup"><span data-stu-id="41257-125">IncludePrerelease</span></span> | <span data-ttu-id="41257-126">Schließt vorab Pakete in die Ergebnisse ein.</span><span class="sxs-lookup"><span data-stu-id="41257-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="41257-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="41257-127">ExactMatch</span></span> | <span data-ttu-id="41257-128">Gibt an, dass &lt;Schlüsselwörter&gt; als Paket-ID verwendet werden soll</span><span class="sxs-lookup"><span data-stu-id="41257-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="41257-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="41257-129">StartWith</span></span> | <span data-ttu-id="41257-130">Gibt Pakete zurück, deren Paket-ID mit &lt;Schlüsselwörtern&gt;beginnt.</span><span class="sxs-lookup"><span data-stu-id="41257-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="41257-131">Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.</span><span class="sxs-lookup"><span data-stu-id="41257-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="41257-132">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="41257-132">Common Parameters</span></span>

<span data-ttu-id="41257-133">`Find-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="41257-133">`Find-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="41257-134">Beispiele</span><span class="sxs-lookup"><span data-stu-id="41257-134">Examples</span></span>

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
