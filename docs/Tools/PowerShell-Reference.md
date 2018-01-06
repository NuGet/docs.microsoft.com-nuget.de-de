---
title: NuGet-PowerShell-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/2/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: cd08b869-44c6-480e-90f7-494a6d08e6d0
description: "Die vollständige Referenz zu PowerShell-Befehle in der NuGet-Paket-Manager-Konsole in Visual Studio verfügbar."
keywords: NuGet-Paket-Manager-Konsole NuGet Powershell-Befehle, NuGet Powershell-Referenz
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 64450a8bcca7f6028d4ce389d51ac35e9209cfae
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/05/2018
---
# <a name="powershell-reference"></a><span data-ttu-id="00630-104">PowerShell-Referenz</span><span class="sxs-lookup"><span data-stu-id="00630-104">PowerShell reference</span></span>

<span data-ttu-id="00630-105">Der Paket-Manager-Konsole bietet eine PowerShell-Schnittstelle innerhalb von Visual Studio unter Windows für die Interaktion mit NuGet, über die spezifischen Befehle unten aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="00630-105">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="00630-106">(Die Konsole ist nicht in Visual Studio für Mac gegenwärtig verfügbar) Eine Anleitung zur Verwendung der Konsole, finden Sie unter der [Package Manager Console](../tools/package-manager-console.md) Thema.</span><span class="sxs-lookup"><span data-stu-id="00630-106">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see the [Package Manager Console](../tools/package-manager-console.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="00630-107">Alle PowerShell-Befehle beziehen sich nur auf Paket Verbrauch.</span><span class="sxs-lookup"><span data-stu-id="00630-107">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="00630-108">Keine PowerShell-Befehle beziehen sich auf erstellen und Veröffentlichen von Paketen, außer, wenn ein Paket kann auch ein Consumer von anderen Paketen sein.</span><span class="sxs-lookup"><span data-stu-id="00630-108">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="00630-109">Die hier aufgeführten Befehle sind spezifisch für die Paket-Manager-Konsole in Visual Studio und unterscheiden sich von der [Packagemanagement-Modul Befehle](/powershell/module/packagemanagement/?view=powershell-6) , die in eine allgemeine PowerShell-Umgebung verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="00630-109">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/?view=powershell-6) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="00630-110">Insbesondere wird jede Umgebung verfügt über Befehle, die in anderen nicht verfügbar sind, und Befehle mit dem gleichen Namen unterscheidet sich auch in ihren bestimmten Argumenten.</span><span class="sxs-lookup"><span data-stu-id="00630-110">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="00630-111">Wenn Sie die Paket-Verwaltungskonsole in Visual Studio verwenden, gelten die Befehle und Argumente, die in diesem Thema vorhanden dokumentiert.</span><span class="sxs-lookup"><span data-stu-id="00630-111">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="00630-112">Häufig verwendete Befehle</span><span class="sxs-lookup"><span data-stu-id="00630-112">Common Commands</span></span> | <span data-ttu-id="00630-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="00630-113">Description</span></span> | <span data-ttu-id="00630-114">NuGet-Version</span><span class="sxs-lookup"><span data-stu-id="00630-114">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="00630-115">Install-Package</span><span class="sxs-lookup"><span data-stu-id="00630-115">Install-Package</span></span>](ps-ref-install-package.md) | <span data-ttu-id="00630-116">Installiert ein Paket und seine Abhängigkeiten im Projekt.</span><span class="sxs-lookup"><span data-stu-id="00630-116">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="00630-117">Alle</span><span class="sxs-lookup"><span data-stu-id="00630-117">All</span></span> |
| [<span data-ttu-id="00630-118">Update-Package</span><span class="sxs-lookup"><span data-stu-id="00630-118">Update-Package</span></span>](ps-ref-update-package.md) | <span data-ttu-id="00630-119">Aktualisiert ein Paket und seine Abhängigkeiten oder alle Pakete in einem Projekt.</span><span class="sxs-lookup"><span data-stu-id="00630-119">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="00630-120">Alle</span><span class="sxs-lookup"><span data-stu-id="00630-120">All</span></span> |
| [<span data-ttu-id="00630-121">Find-Package</span><span class="sxs-lookup"><span data-stu-id="00630-121">Find-Package</span></span>](ps-ref-find-package.md) | <span data-ttu-id="00630-122">Durchsucht eine Paketquelle eine Paket-ID oder Schlüsselwörter verwenden.</span><span class="sxs-lookup"><span data-stu-id="00630-122">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="00630-123">3.0+</span><span class="sxs-lookup"><span data-stu-id="00630-123">3.0+</span></span> |
| [<span data-ttu-id="00630-124">Get-Package</span><span class="sxs-lookup"><span data-stu-id="00630-124">Get-Package</span></span>](ps-ref-get-package.md) | <span data-ttu-id="00630-125">Ruft die Liste der Pakete, die im lokalen Repository installiert oder von einem Paketquelle verfügbaren Pakete aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="00630-125">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="00630-126">Alle</span><span class="sxs-lookup"><span data-stu-id="00630-126">All</span></span> |

| <span data-ttu-id="00630-127">Sekundäre Befehle</span><span class="sxs-lookup"><span data-stu-id="00630-127">Secondary Commands</span></span> | <span data-ttu-id="00630-128">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="00630-128">Description</span></span> | <span data-ttu-id="00630-129">NuGet-Version</span><span class="sxs-lookup"><span data-stu-id="00630-129">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="00630-130">Add-BindingRedirect</span><span class="sxs-lookup"><span data-stu-id="00630-130">Add-BindingRedirect</span></span>](ps-ref-add-bindingredirect.md) | <span data-ttu-id="00630-131">Untersucht alle Assemblys im Ausgabepfad auf ein Projekt und fügt Sie bindungsumleitungen zu den `app.config` oder `web.config` bei Bedarf.</span><span class="sxs-lookup"><span data-stu-id="00630-131">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="00630-132">Alle</span><span class="sxs-lookup"><span data-stu-id="00630-132">All</span></span> |
| [<span data-ttu-id="00630-133">Get-Project</span><span class="sxs-lookup"><span data-stu-id="00630-133">Get-Project</span></span>](ps-ref-get-project.md) | <span data-ttu-id="00630-134">Zeigt Informationen zu den Standardwert oder die angegebene Projekt.</span><span class="sxs-lookup"><span data-stu-id="00630-134">Displays information about the default or specified project.</span></span> | <span data-ttu-id="00630-135">3.0+</span><span class="sxs-lookup"><span data-stu-id="00630-135">3.0+</span></span> |
| [<span data-ttu-id="00630-136">Open-PackagePage</span><span class="sxs-lookup"><span data-stu-id="00630-136">Open-PackagePage</span></span>](ps-ref-open-packagepage.md) | <span data-ttu-id="00630-137">Startet den Standardbrowser mit dem Projekt, Lizenzen oder Missbrauch Berichts-URL für das angegebene Paket.</span><span class="sxs-lookup"><span data-stu-id="00630-137">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="00630-138">In 3.0 veraltet</span><span class="sxs-lookup"><span data-stu-id="00630-138">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="00630-139">Register-"tabexpansion"</span><span class="sxs-lookup"><span data-stu-id="00630-139">Register-TabExpansion</span></span>](ps-ref-register-tabexpansion.md) | <span data-ttu-id="00630-140">Registriert eine Tab-Taste für die Parameter eines Befehls, sodass Sie benutzerdefinierte Erweiterungen für häufig verwendete Parameterwerte zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="00630-140">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="00630-141">Alle</span><span class="sxs-lookup"><span data-stu-id="00630-141">All</span></span> |
| [<span data-ttu-id="00630-142">Sync-Package</span><span class="sxs-lookup"><span data-stu-id="00630-142">Sync-Package</span></span>](ps-ref-sync-package.md) | <span data-ttu-id="00630-143">Abrufen der Version des Pakets aus einer installiert Projekt angegeben und synchronisiert die Version mit den restlichen Projekten in der Projektmappe.</span><span class="sxs-lookup"><span data-stu-id="00630-143">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="00630-144">3.0+</span><span class="sxs-lookup"><span data-stu-id="00630-144">3.0+</span></span> |
| [<span data-ttu-id="00630-145">Uninstall-Package</span><span class="sxs-lookup"><span data-stu-id="00630-145">Uninstall-Package</span></span>](ps-ref-uninstall-package.md) | <span data-ttu-id="00630-146">Entfernt ein Paket aus einem Projekt, und optional die abhängigen Elemente entfernen.</span><span class="sxs-lookup"><span data-stu-id="00630-146">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="00630-147">Alle</span><span class="sxs-lookup"><span data-stu-id="00630-147">All</span></span> |

<span data-ttu-id="00630-148">Vollständige, ausführliche Hilfe zu allen diesen Befehlen in der Konsole führen Sie den folgenden nur mit den betreffenden Befehlsnamen:</span><span class="sxs-lookup"><span data-stu-id="00630-148">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="00630-149">Alle Package Manager Console Befehle unterstützen die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216):</span><span class="sxs-lookup"><span data-stu-id="00630-149">All Package Manager Console commands support the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216):</span></span>

- <span data-ttu-id="00630-150">Debug</span><span class="sxs-lookup"><span data-stu-id="00630-150">Debug</span></span>
- <span data-ttu-id="00630-151">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="00630-151">ErrorAction</span></span>
- <span data-ttu-id="00630-152">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="00630-152">ErrorVariable</span></span>
- <span data-ttu-id="00630-153">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="00630-153">OutBuffer</span></span>
- <span data-ttu-id="00630-154">OutVariable</span><span class="sxs-lookup"><span data-stu-id="00630-154">OutVariable</span></span>
- <span data-ttu-id="00630-155">Mit "pipelinevariable"</span><span class="sxs-lookup"><span data-stu-id="00630-155">PipelineVariable</span></span>
- <span data-ttu-id="00630-156">Ausführlich</span><span class="sxs-lookup"><span data-stu-id="00630-156">Verbose</span></span>
- <span data-ttu-id="00630-157">WarningAction</span><span class="sxs-lookup"><span data-stu-id="00630-157">WarningAction</span></span>
- <span data-ttu-id="00630-158">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="00630-158">WarningVariable</span></span>

<span data-ttu-id="00630-159">Weitere Informationen finden Sie in [About_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in der PowerShell-Dokumentation.</span><span class="sxs-lookup"><span data-stu-id="00630-159">For details, refer to [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in the PowerShell documentation.</span></span>
