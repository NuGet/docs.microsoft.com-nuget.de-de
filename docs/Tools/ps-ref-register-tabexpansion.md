---
title: Register "tabexpansion" NuGet-PowerShell-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für die Register-\"tabexpansion\" PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio."
keywords: NuGet-Paket-Manager-Konsole NuGet Powershell-Befehle, NuGet Powershell-Referenz zu "Register-tabexpansion"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5691c07f9efef4bfd12680421f3b02c5a523eb6f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="40310-104">Register-"tabexpansion" (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="40310-104">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="40310-105">*Verfügbar nur innerhalb der [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="40310-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="40310-106">Registriert eine Tab-Taste für die Parameter des angegebenen Befehls an, so, dass bei der Registerkarte "verwendet wird, wenn Sie einen Befehl eingeben, die erweiterten Werte als verfügbare Optionen für den fraglichen Parameter angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="40310-106">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="40310-107">Es werden alle vorherigen Erweiterungen für den Befehl überschrieben.</span><span class="sxs-lookup"><span data-stu-id="40310-107">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="40310-108">Syntax</span><span class="sxs-lookup"><span data-stu-id="40310-108">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="40310-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="40310-109">Parameters</span></span>

| <span data-ttu-id="40310-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="40310-110">Parameter</span></span> | <span data-ttu-id="40310-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="40310-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="40310-112">name</span><span class="sxs-lookup"><span data-stu-id="40310-112">Name</span></span> | <span data-ttu-id="40310-113">(Erforderlich) Der Befehl, um Erweiterungen zu registrieren.</span><span class="sxs-lookup"><span data-stu-id="40310-113">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="40310-114">Der - Name Switch selbst ist optional.</span><span class="sxs-lookup"><span data-stu-id="40310-114">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="40310-115">Definition</span><span class="sxs-lookup"><span data-stu-id="40310-115">Definition</span></span> | <span data-ttu-id="40310-116">(Erforderlich) Ein Objekt, das Argument in der Syntax beschreibt `@{'<parameter>' = {'<value1>', '<value2>', ...}}` , in denen `<parameter>` ist der Name des Parameters ändern, und jede `<value>` bietet eine bestimmte Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="40310-116">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="40310-117">Einfachen und doppelte Anführungszeichen werden akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="40310-117">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="40310-118">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="40310-118">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="40310-119">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="40310-119">Common Parameters</span></span>

<span data-ttu-id="40310-120">`Register-TabExpansion`unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="40310-120">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="40310-121">Beispiele</span><span class="sxs-lookup"><span data-stu-id="40310-121">Examples</span></span>

<span data-ttu-id="40310-122">Erwägen Sie eine Lösung, die drei Projekte Namen EventManager, Dienstprogramme und SpecialParser enthält.</span><span class="sxs-lookup"><span data-stu-id="40310-122">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="40310-123">Der Entwickler häufig mithilfe der `Update-Package` Befehl zu unterschiedlichen Zeiten mit jedem dieser Projekte.</span><span class="sxs-lookup"><span data-stu-id="40310-123">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="40310-124">Sie sucht es praktisch, wenn die `Update-Package` Befehl angeben, automatische Vervollständigung von Erweiterungen für die `-ProjectName` Argument, damit Sie einen Projektnamen jeder Anmeldung eingeben nicht benötigt.</span><span class="sxs-lookup"><span data-stu-id="40310-124">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="40310-125">Registriert den folgende Befehl ein, dann diese drei Projektnamen als eine Erweiterung für die `-ProjectName` Parameter:</span><span class="sxs-lookup"><span data-stu-id="40310-125">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="40310-126">Der Entwickler kann dann geben `Update-Package -ProjectName `, drücken Sie Tab, und finden Sie unter der Erweiterungen als automatische Vervollständigung Optionen angeboten:</span><span class="sxs-lookup"><span data-stu-id="40310-126">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Beispiel zur Verwendung von "Register-tabexpansion"](media/Register-TabExpansion-Example.png)
