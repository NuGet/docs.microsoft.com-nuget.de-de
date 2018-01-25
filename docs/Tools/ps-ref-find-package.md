---
title: NuGet-Find-Package-PowerShell-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für Find-Package-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio."
keywords: NuGet-Paket-Manager-Konsole NuGet Powershell-Befehle, NuGet Powershell-Referenz, Find-Package
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 47b8420cc49d0a76709cf3268af69fcff310d165
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="04a8e-104">Find-Package (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="04a8e-104">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="04a8e-105">*Version 3.0 +; In diesem Thema wird beschrieben, den Befehl innerhalb der [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio unter Windows. Der generische PowerShell Find-Package-Befehl finden Sie unter der [PowerShell PackageManagement-Verweis](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="04a8e-105">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="04a8e-106">Ruft die Sammlung der remotepakete mit der angegebenen ID oder Schlüsselwörter aus der Paketquelle ab.</span><span class="sxs-lookup"><span data-stu-id="04a8e-106">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="04a8e-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="04a8e-107">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="04a8e-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="04a8e-108">Parameters</span></span>

| <span data-ttu-id="04a8e-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="04a8e-109">Parameter</span></span> | <span data-ttu-id="04a8e-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="04a8e-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="04a8e-111">ID &lt;Schlüsselwörter&gt;</span><span class="sxs-lookup"><span data-stu-id="04a8e-111">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="04a8e-112">(Erforderlich) Schlüsselwörter verwenden, wenn die Paketquelle zu suchen.</span><span class="sxs-lookup"><span data-stu-id="04a8e-112">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="04a8e-113">Verwenden Sie-"exactMatch", um nur die Pakete zurück, dessen Paket-ID der Schlüsselwörter übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="04a8e-113">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="04a8e-114">Wenn keine Schlüsselwörter angegeben sind, `Find-Package` -Rückgaben eine Liste der Top-20-Pakete von Downloads oder die Anzahl von - zuerst.</span><span class="sxs-lookup"><span data-stu-id="04a8e-114">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="04a8e-115">Beachten Sie, dass - Id optional ist und nicht ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="04a8e-115">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="04a8e-116">Quelle</span><span class="sxs-lookup"><span data-stu-id="04a8e-116">Source</span></span> | <span data-ttu-id="04a8e-117">Die URL oder einen Ordnerpfad für die Paketquelle, gesucht werden soll.</span><span class="sxs-lookup"><span data-stu-id="04a8e-117">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="04a8e-118">Lokale Ordnerpfaden kann absolut oder relativ zum aktuellen Ordner.</span><span class="sxs-lookup"><span data-stu-id="04a8e-118">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="04a8e-119">Wenn nicht angegeben, `Find-Package` die aktuell ausgewählten Paketquelle durchsucht.</span><span class="sxs-lookup"><span data-stu-id="04a8e-119">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="04a8e-120">AllVersions</span><span class="sxs-lookup"><span data-stu-id="04a8e-120">AllVersions</span></span> | <span data-ttu-id="04a8e-121">Zeigt alle verfügbaren Versionen der einzelnen Pakete, anstatt nur die neueste Version.</span><span class="sxs-lookup"><span data-stu-id="04a8e-121">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="04a8e-122">First</span><span class="sxs-lookup"><span data-stu-id="04a8e-122">First</span></span> | <span data-ttu-id="04a8e-123">Die Anzahl der Pakete an, ab dem Anfang der Liste zurückgegeben werden soll; Der Standardwert ist 20.</span><span class="sxs-lookup"><span data-stu-id="04a8e-123">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="04a8e-124">Skip</span><span class="sxs-lookup"><span data-stu-id="04a8e-124">Skip</span></span> | <span data-ttu-id="04a8e-125">Lässt die erste &lt;Int&gt; Pakete aus der angezeigten Liste.</span><span class="sxs-lookup"><span data-stu-id="04a8e-125">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="04a8e-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="04a8e-126">IncludePrerelease</span></span> | <span data-ttu-id="04a8e-127">Enthält Vorabversionen von Paketen in den Ergebnissen an.</span><span class="sxs-lookup"><span data-stu-id="04a8e-127">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="04a8e-128">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="04a8e-128">ExactMatch</span></span> | <span data-ttu-id="04a8e-129">Mit angegebenen &lt;Schlüsselwörter&gt; als Groß-/Kleinschreibung Paket-ID</span><span class="sxs-lookup"><span data-stu-id="04a8e-129">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="04a8e-130">StartWith</span><span class="sxs-lookup"><span data-stu-id="04a8e-130">StartWith</span></span> | <span data-ttu-id="04a8e-131">Gibt Pakete, deren ID beginnt mit Paket &lt;Schlüsselwörter&gt;.</span><span class="sxs-lookup"><span data-stu-id="04a8e-131">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="04a8e-132">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="04a8e-132">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="04a8e-133">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="04a8e-133">Common Parameters</span></span>

<span data-ttu-id="04a8e-134">`Find-Package`unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="04a8e-134">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="04a8e-135">Beispiele</span><span class="sxs-lookup"><span data-stu-id="04a8e-135">Examples</span></span>

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
