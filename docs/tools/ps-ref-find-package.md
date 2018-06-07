---
title: NuGet-Find-Package-PowerShell-Referenz
description: Referenz für Find-Package-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: ebecb3818c063d11a2d613a85e2b7baef649dee6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816918"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="b55bc-103">Find-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="b55bc-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="b55bc-104">*Version 3.0 +; In diesem Thema wird beschrieben, den Befehl innerhalb der [NuGet Package Manager Console](package-manager-console.md) in Visual Studio unter Windows. Der generische PowerShell Find-Package-Befehl finden Sie unter der [PowerShell PackageManagement-Verweis](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="b55bc-104">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="b55bc-105">Ruft die Sammlung der remotepakete mit der angegebenen ID oder Schlüsselwörter aus der Paketquelle ab.</span><span class="sxs-lookup"><span data-stu-id="b55bc-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="b55bc-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="b55bc-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="b55bc-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="b55bc-107">Parameters</span></span>

| <span data-ttu-id="b55bc-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="b55bc-108">Parameter</span></span> | <span data-ttu-id="b55bc-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="b55bc-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b55bc-110">ID &lt;Schlüsselwörter&gt;</span><span class="sxs-lookup"><span data-stu-id="b55bc-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="b55bc-111">(Erforderlich) Schlüsselwörter verwenden, wenn die Paketquelle zu suchen.</span><span class="sxs-lookup"><span data-stu-id="b55bc-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="b55bc-112">Verwenden Sie-"exactMatch", um nur die Pakete zurück, dessen Paket-ID der Schlüsselwörter übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="b55bc-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="b55bc-113">Wenn keine Schlüsselwörter angegeben sind, `Find-Package` -Rückgaben eine Liste der Top-20-Pakete von Downloads oder die Anzahl von - zuerst.</span><span class="sxs-lookup"><span data-stu-id="b55bc-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="b55bc-114">Beachten Sie, dass - Id optional ist und nicht ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="b55bc-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="b55bc-115">Quelle</span><span class="sxs-lookup"><span data-stu-id="b55bc-115">Source</span></span> | <span data-ttu-id="b55bc-116">Die URL oder einen Ordnerpfad für die Paketquelle, gesucht werden soll.</span><span class="sxs-lookup"><span data-stu-id="b55bc-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="b55bc-117">Lokale Ordnerpfaden kann absolut oder relativ zum aktuellen Ordner.</span><span class="sxs-lookup"><span data-stu-id="b55bc-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="b55bc-118">Wenn nicht angegeben, `Find-Package` die aktuell ausgewählten Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="b55bc-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="b55bc-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="b55bc-119">AllVersions</span></span> | <span data-ttu-id="b55bc-120">Zeigt alle verfügbaren Versionen der einzelnen Pakete, anstatt nur die neueste Version.</span><span class="sxs-lookup"><span data-stu-id="b55bc-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="b55bc-121">First</span><span class="sxs-lookup"><span data-stu-id="b55bc-121">First</span></span> | <span data-ttu-id="b55bc-122">Die Anzahl der Pakete an, ab dem Anfang der Liste zurückgegeben werden soll; Der Standardwert ist 20.</span><span class="sxs-lookup"><span data-stu-id="b55bc-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="b55bc-123">Skip</span><span class="sxs-lookup"><span data-stu-id="b55bc-123">Skip</span></span> | <span data-ttu-id="b55bc-124">Lässt die erste &lt;Int&gt; Pakete aus der angezeigten Liste.</span><span class="sxs-lookup"><span data-stu-id="b55bc-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="b55bc-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="b55bc-125">IncludePrerelease</span></span> | <span data-ttu-id="b55bc-126">Enthält Vorabversionen von Paketen in den Ergebnissen an.</span><span class="sxs-lookup"><span data-stu-id="b55bc-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="b55bc-127">"ExactMatch"</span><span class="sxs-lookup"><span data-stu-id="b55bc-127">ExactMatch</span></span> | <span data-ttu-id="b55bc-128">Mit angegebenen &lt;Schlüsselwörter&gt; als Groß-/Kleinschreibung Paket-ID</span><span class="sxs-lookup"><span data-stu-id="b55bc-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="b55bc-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="b55bc-129">StartWith</span></span> | <span data-ttu-id="b55bc-130">Gibt Pakete, deren ID beginnt mit Paket &lt;Schlüsselwörter&gt;.</span><span class="sxs-lookup"><span data-stu-id="b55bc-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="b55bc-131">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="b55bc-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="b55bc-132">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="b55bc-132">Common Parameters</span></span>

<span data-ttu-id="b55bc-133">`Find-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b55bc-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="b55bc-134">Beispiele</span><span class="sxs-lookup"><span data-stu-id="b55bc-134">Examples</span></span>

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
