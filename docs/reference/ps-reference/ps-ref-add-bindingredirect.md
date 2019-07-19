---
title: PowerShell-Referenz zu nuget-bindingRedirect
description: Referenz für den PowerShell-Befehl "Add-bindingRedirect" in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b1e88d32deb3ff34833ef22a9cbb8cad3f0d4354
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327457"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="a328a-103">Add-BindingRedirect (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="a328a-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a328a-104">*Nur in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows verfügbar.*</span><span class="sxs-lookup"><span data-stu-id="a328a-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="a328a-105">Untersucht alle Assemblys im Ausgabepfad für ein Projekt und fügt bei Bedarf Bindungs Umleitungen zur Anwendung oder Webkonfigurationsdatei hinzu.</span><span class="sxs-lookup"><span data-stu-id="a328a-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="a328a-106">Dieser Befehl wird automatisch ausgeführt, wenn ein Paket installiert wird.</span><span class="sxs-lookup"><span data-stu-id="a328a-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="a328a-107">Ausführliche Informationen zu Bindungs Umleitungen und deren Verwendung finden Sie unter [umleiten](/dotnet/framework/configure-apps/redirect-assembly-versions) von Assemblyversionen in der .NET-Dokumentation.</span><span class="sxs-lookup"><span data-stu-id="a328a-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="a328a-108">Syntax</span><span class="sxs-lookup"><span data-stu-id="a328a-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="a328a-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="a328a-109">Parameters</span></span>

| <span data-ttu-id="a328a-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="a328a-110">Parameter</span></span> | <span data-ttu-id="a328a-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="a328a-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a328a-112">ProjektName</span><span class="sxs-lookup"><span data-stu-id="a328a-112">ProjectName</span></span> | <span data-ttu-id="a328a-113">Benötigten Das Projekt, dem Bindungs Umleitungen hinzugefügt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="a328a-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="a328a-114">Der Schalter "-ProjectName" ist optional.</span><span class="sxs-lookup"><span data-stu-id="a328a-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="a328a-115">Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.</span><span class="sxs-lookup"><span data-stu-id="a328a-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a328a-116">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="a328a-116">Common Parameters</span></span>

<span data-ttu-id="a328a-117">`Add-BindingRedirect`unterstützt die folgenden [allgemeinen PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="a328a-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a328a-118">Beispiele</span><span class="sxs-lookup"><span data-stu-id="a328a-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```