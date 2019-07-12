---
title: Register "tabexpansion" NuGet-PowerShell-Referenz
description: Referenz für "Register-tabexpansion" PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8adb80af85e2e32fa8c35e5272cf90ff0c0ddcbb
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842484"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="18e6b-103">Register-"tabexpansion" (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="18e6b-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="18e6b-104">*Verfügbar nur in der [-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="18e6b-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="18e6b-105">Registriert eine Erweiterung der Registerkarte für die Parameter des angegebenen Befehls, so, dass wenn Registerkarte verwendet wird, wenn Sie einen Befehl eingeben, die erweiterten Werte als verfügbare Optionen für den betreffenden Parameter angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="18e6b-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="18e6b-106">Es werden alle vorherigen Erweiterungen für den Befehl überschrieben.</span><span class="sxs-lookup"><span data-stu-id="18e6b-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="18e6b-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="18e6b-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="18e6b-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="18e6b-108">Parameters</span></span>

| <span data-ttu-id="18e6b-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="18e6b-109">Parameter</span></span> | <span data-ttu-id="18e6b-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="18e6b-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="18e6b-111">Name</span><span class="sxs-lookup"><span data-stu-id="18e6b-111">Name</span></span> | <span data-ttu-id="18e6b-112">(Erforderlich) Der Befehl, um Erweiterungen zu registrieren.</span><span class="sxs-lookup"><span data-stu-id="18e6b-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="18e6b-113">Der - Name Switch selbst ist optional.</span><span class="sxs-lookup"><span data-stu-id="18e6b-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="18e6b-114">Definition</span><span class="sxs-lookup"><span data-stu-id="18e6b-114">Definition</span></span> | <span data-ttu-id="18e6b-115">(Erforderlich) Ein Objekt, das das Argument in der Syntax beschreibt `@{'<parameter>' = {'<value1>', '<value2>', ...}}` , in denen `<parameter>` ist der Name des Parameters ändern, und jede `<value>` bietet eine spezielle Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="18e6b-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="18e6b-116">Einfacher und doppelte Anführungszeichen werden akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="18e6b-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="18e6b-117">Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="18e6b-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="18e6b-118">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="18e6b-118">Common Parameters</span></span>

<span data-ttu-id="18e6b-119">`Register-TabExpansion` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="18e6b-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="18e6b-120">Beispiele</span><span class="sxs-lookup"><span data-stu-id="18e6b-120">Examples</span></span>

<span data-ttu-id="18e6b-121">Erwägen Sie eine Lösung, die drei Projekte Namen EventManager, Dienstprogramme und SpecialParser enthält.</span><span class="sxs-lookup"><span data-stu-id="18e6b-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="18e6b-122">Der Entwickler häufig verwendet die `Update-Package` Befehl zu unterschiedlichen Zeiten mit jedes dieser Projekte.</span><span class="sxs-lookup"><span data-stu-id="18e6b-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="18e6b-123">Sie sucht es praktisch, wenn die `Update-Package` Befehl geben, automatische Vervollständigung von Erweiterungen für die `-ProjectName` Argument, damit sie nicht, einen Projektnamen ein, die jedes Mal erneut eingeben muss.</span><span class="sxs-lookup"><span data-stu-id="18e6b-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="18e6b-124">Registriert den folgende Befehl aus, dann diese drei Projektnamen als Erweiterung für die `-ProjectName` Parameter:</span><span class="sxs-lookup"><span data-stu-id="18e6b-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="18e6b-125">Entwickler kann dann eingeben `Update-Package -ProjectName `, drücken Sie Tab, und finden Sie unter den Erweiterungen, die als Optionen zur automatischen Vervollständigung angeboten:</span><span class="sxs-lookup"><span data-stu-id="18e6b-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Beispiel zur Verwendung von "Register-tabexpansion"](media/Register-TabExpansion-Example.png)
