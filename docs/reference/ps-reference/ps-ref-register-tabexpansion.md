---
title: Nuget-Register-tabexpansion PowerShell-Referenz
description: Referenz für den PowerShell-Befehl "Register-tabexpansion" in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 37aed96760e642b03c02bf31fe47a54f0e3cb74a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384453"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="acc6f-103">Register-tabexpansion (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="acc6f-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="acc6f-104">*Nur in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows verfügbar.*</span><span class="sxs-lookup"><span data-stu-id="acc6f-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="acc6f-105">Registriert eine Registerkarten Erweiterung für die Parameter des angegebenen Befehls, sodass die erweiterten Werte als verfügbare Optionen für den fraglichen Parameter angezeigt werden, wenn Tab bei der Eingabe eines Befehls verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="acc6f-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="acc6f-106">Alle vorherigen Erweiterungen für den Befehl werden überschrieben.</span><span class="sxs-lookup"><span data-stu-id="acc6f-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="acc6f-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="acc6f-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="acc6f-108">Parameters</span><span class="sxs-lookup"><span data-stu-id="acc6f-108">Parameters</span></span>

| <span data-ttu-id="acc6f-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="acc6f-109">Parameter</span></span> | <span data-ttu-id="acc6f-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="acc6f-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="acc6f-111">-Name</span><span class="sxs-lookup"><span data-stu-id="acc6f-111">Name</span></span> | <span data-ttu-id="acc6f-112">Benötigten Der Befehl, für den Erweiterungen registriert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="acc6f-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="acc6f-113">Der Schalter "-Name" ist optional.</span><span class="sxs-lookup"><span data-stu-id="acc6f-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="acc6f-114">Definition</span><span class="sxs-lookup"><span data-stu-id="acc6f-114">Definition</span></span> | <span data-ttu-id="acc6f-115">Benötigten Ein Objekt, das das Argument in der Syntax beschreibt `@{'<parameter>' = {'<value1>', '<value2>', ...}}` wobei `<parameter>` der Name des Parameters ist, der geändert werden soll, und jeder `<value>` eine bestimmte Erweiterung bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="acc6f-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="acc6f-116">Sowohl einfache als auch doppelte Anführungszeichen werden akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="acc6f-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="acc6f-117">Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.</span><span class="sxs-lookup"><span data-stu-id="acc6f-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="acc6f-118">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="acc6f-118">Common Parameters</span></span>

<span data-ttu-id="acc6f-119">`Register-TabExpansion` unterstützt die folgenden [allgemeinen PowerShell-Parameter](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="acc6f-119">`Register-TabExpansion` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="acc6f-120">Beispiele</span><span class="sxs-lookup"><span data-stu-id="acc6f-120">Examples</span></span>

<span data-ttu-id="acc6f-121">Stellen Sie sich eine Lösung vor, die drei Projekte mit den Namen EventManager, Utilities und specialparser enthält.</span><span class="sxs-lookup"><span data-stu-id="acc6f-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="acc6f-122">Der Entwickler verwendet häufig den `Update-Package` Befehl zu unterschiedlichen Zeitpunkten für jedes dieser Projekte.</span><span class="sxs-lookup"><span data-stu-id="acc6f-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="acc6f-123">Sie finden es praktisch, dass der `Update-Package` Befehl Erweiterungen für die automatische Vervollständigung für das `-ProjectName` Argument bereitstellen muss, damit Sie nicht jedes Mal einen Projektnamen eingeben müssen.</span><span class="sxs-lookup"><span data-stu-id="acc6f-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="acc6f-124">Der folgende Befehl registriert dann die drei Projektnamen als Erweiterung für den `-ProjectName`-Parameter:</span><span class="sxs-lookup"><span data-stu-id="acc6f-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="acc6f-125">Der Entwickler kann dann `Update-Package -ProjectName `eingeben, die Tab-Taste drücken und die Erweiterungen als automatische Vervollständigungs Optionen anzeigen:</span><span class="sxs-lookup"><span data-stu-id="acc6f-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Beispiel für die Verwendung von "Register-tabexpansion"](media/Register-TabExpansion-Example.png)
