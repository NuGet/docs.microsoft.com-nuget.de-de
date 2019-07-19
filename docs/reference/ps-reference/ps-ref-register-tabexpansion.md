---
title: Nuget-Register-tabexpansion PowerShell-Referenz
description: Referenz für den PowerShell-Befehl "Register-tabexpansion" in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 14cda695677e1052c78169fda097b72b460a9d43
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327297"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="07dcf-103">Register-tabexpansion (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="07dcf-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="07dcf-104">*Nur in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows verfügbar.*</span><span class="sxs-lookup"><span data-stu-id="07dcf-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="07dcf-105">Registriert eine Registerkarten Erweiterung für die Parameter des angegebenen Befehls, sodass die erweiterten Werte als verfügbare Optionen für den fraglichen Parameter angezeigt werden, wenn Tab bei der Eingabe eines Befehls verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="07dcf-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="07dcf-106">Alle vorherigen Erweiterungen für den Befehl werden überschrieben.</span><span class="sxs-lookup"><span data-stu-id="07dcf-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="07dcf-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="07dcf-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="07dcf-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="07dcf-108">Parameters</span></span>

| <span data-ttu-id="07dcf-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="07dcf-109">Parameter</span></span> | <span data-ttu-id="07dcf-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="07dcf-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="07dcf-111">Name</span><span class="sxs-lookup"><span data-stu-id="07dcf-111">Name</span></span> | <span data-ttu-id="07dcf-112">Benötigten Der Befehl, für den Erweiterungen registriert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="07dcf-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="07dcf-113">Der Schalter "-Name" ist optional.</span><span class="sxs-lookup"><span data-stu-id="07dcf-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="07dcf-114">Definition</span><span class="sxs-lookup"><span data-stu-id="07dcf-114">Definition</span></span> | <span data-ttu-id="07dcf-115">Benötigten Ein Objekt, das das Argument in der `@{'<parameter>' = {'<value1>', '<value2>', ...}}` Syntax `<parameter>` beschreibt, wobei der Name des zu ändernden Parameters `<value>` und jeder eine bestimmte Erweiterung bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="07dcf-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="07dcf-116">Sowohl einfache als auch doppelte Anführungszeichen werden akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="07dcf-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="07dcf-117">Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.</span><span class="sxs-lookup"><span data-stu-id="07dcf-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="07dcf-118">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="07dcf-118">Common Parameters</span></span>

<span data-ttu-id="07dcf-119">`Register-TabExpansion`unterstützt die folgenden [allgemeinen PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="07dcf-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="07dcf-120">Beispiele</span><span class="sxs-lookup"><span data-stu-id="07dcf-120">Examples</span></span>

<span data-ttu-id="07dcf-121">Stellen Sie sich eine Lösung vor, die drei Projekte mit den Namen EventManager, Utilities und specialparser enthält.</span><span class="sxs-lookup"><span data-stu-id="07dcf-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="07dcf-122">Der Entwickler verwendet den `Update-Package` Befehl häufig für jedes dieser Projekte zu unterschiedlichen Zeitpunkten.</span><span class="sxs-lookup"><span data-stu-id="07dcf-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="07dcf-123">Sie finden es praktisch, dass der `Update-Package` Befehl die Erweiterungen für die automatische Vervollständigung `-ProjectName` für das Argument bereitstellt, sodass Sie nicht jedes Mal einen Projektnamen eingeben müssen.</span><span class="sxs-lookup"><span data-stu-id="07dcf-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="07dcf-124">Der folgende Befehl registriert dann die drei Projektnamen als Erweiterung für den `-ProjectName` Parameter:</span><span class="sxs-lookup"><span data-stu-id="07dcf-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="07dcf-125">Der Entwickler kann dann eingeben `Update-Package -ProjectName `, Tab drücken und die Erweiterungen als automatische Vervollständigungs Optionen anzeigen:</span><span class="sxs-lookup"><span data-stu-id="07dcf-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Beispiel für die Verwendung von "Register-tabexpansion"](media/Register-TabExpansion-Example.png)
