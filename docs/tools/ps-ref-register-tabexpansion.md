---
title: Register "tabexpansion" NuGet-PowerShell-Referenz
description: Referenz für die Register-"tabexpansion" PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8011c0e6aa951a32114d460803c493810964a7e0
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818412"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="0dbbd-103">Register-"tabexpansion" (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="0dbbd-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="0dbbd-104">*Verfügbar nur innerhalb der [NuGet Package Manager Console](package-manager-console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="0dbbd-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="0dbbd-105">Registriert eine Tab-Taste für die Parameter des angegebenen Befehls an, so, dass bei der Registerkarte "verwendet wird, wenn Sie einen Befehl eingeben, die erweiterten Werte als verfügbare Optionen für den fraglichen Parameter angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="0dbbd-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="0dbbd-106">Es werden alle vorherigen Erweiterungen für den Befehl überschrieben.</span><span class="sxs-lookup"><span data-stu-id="0dbbd-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="0dbbd-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="0dbbd-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="0dbbd-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="0dbbd-108">Parameters</span></span>

| <span data-ttu-id="0dbbd-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="0dbbd-109">Parameter</span></span> | <span data-ttu-id="0dbbd-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="0dbbd-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0dbbd-111">name</span><span class="sxs-lookup"><span data-stu-id="0dbbd-111">Name</span></span> | <span data-ttu-id="0dbbd-112">(Erforderlich) Der Befehl, um Erweiterungen zu registrieren.</span><span class="sxs-lookup"><span data-stu-id="0dbbd-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="0dbbd-113">Der - Name Switch selbst ist optional.</span><span class="sxs-lookup"><span data-stu-id="0dbbd-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="0dbbd-114">Definition</span><span class="sxs-lookup"><span data-stu-id="0dbbd-114">Definition</span></span> | <span data-ttu-id="0dbbd-115">(Erforderlich) Ein Objekt, das Argument in der Syntax beschreibt `@{'<parameter>' = {'<value1>', '<value2>', ...}}` , in denen `<parameter>` ist der Name des Parameters ändern, und jede `<value>` bietet eine bestimmte Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="0dbbd-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="0dbbd-116">Einfachen und doppelte Anführungszeichen werden akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="0dbbd-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="0dbbd-117">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="0dbbd-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="0dbbd-118">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="0dbbd-118">Common Parameters</span></span>

<span data-ttu-id="0dbbd-119">`Register-TabExpansion` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="0dbbd-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="0dbbd-120">Beispiele</span><span class="sxs-lookup"><span data-stu-id="0dbbd-120">Examples</span></span>

<span data-ttu-id="0dbbd-121">Erwägen Sie eine Lösung, die drei Projekte Namen EventManager, Dienstprogramme und SpecialParser enthält.</span><span class="sxs-lookup"><span data-stu-id="0dbbd-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="0dbbd-122">Der Entwickler häufig mithilfe der `Update-Package` Befehl zu unterschiedlichen Zeiten mit jedem dieser Projekte.</span><span class="sxs-lookup"><span data-stu-id="0dbbd-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="0dbbd-123">Sie sucht es praktisch, wenn die `Update-Package` Befehl angeben, automatische Vervollständigung von Erweiterungen für die `-ProjectName` Argument, damit Sie einen Projektnamen jeder Anmeldung eingeben nicht benötigt.</span><span class="sxs-lookup"><span data-stu-id="0dbbd-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="0dbbd-124">Registriert den folgende Befehl ein, dann diese drei Projektnamen als eine Erweiterung für die `-ProjectName` Parameter:</span><span class="sxs-lookup"><span data-stu-id="0dbbd-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="0dbbd-125">Der Entwickler kann dann geben `Update-Package -ProjectName `, drücken Sie Tab, und finden Sie unter der Erweiterungen als automatische Vervollständigung Optionen angeboten:</span><span class="sxs-lookup"><span data-stu-id="0dbbd-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Beispiel zur Verwendung von "Register-tabexpansion"](media/Register-TabExpansion-Example.png)
