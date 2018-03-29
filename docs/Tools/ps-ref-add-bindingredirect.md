---
title: Hinzufügen von NuGet-BindingRedirect-PowerShell-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenz für die Add-BindingRedirect-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
keywords: NuGet-Paket-Manager-Konsole, die NuGet Powershell-Befehle, die NuGet Powershell-Referenz, Add-BindingRedirect
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 2a337bd61295f436b49c56c1680d07ccc6a8c403
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="518cd-104">Hinzufügen-BindingRedirect (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="518cd-104">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="518cd-105">*Verfügbar nur innerhalb der [NuGet Package Manager Console](package-manager-console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="518cd-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="518cd-106">Untersucht alle Assemblys im Ausgabepfad auf ein Projekt, und der Anwendungs- oder Webkonfigurationsdatei Konfigurationsdatei umleitungen für Bindungen hinzugefügt, bei Bedarf.</span><span class="sxs-lookup"><span data-stu-id="518cd-106">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="518cd-107">Mit diesem Befehl wird automatisch ausgeführt, wenn Sie ein Paket zu installieren.</span><span class="sxs-lookup"><span data-stu-id="518cd-107">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="518cd-108">Ausführliche Informationen zu binden, leitet und warum sie verwendet werden, finden Sie unter [Umleiten von Assemblyversionen](/dotnet/framework/configure-apps/redirect-assembly-versions) in der Dokumentation zu .NET.</span><span class="sxs-lookup"><span data-stu-id="518cd-108">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="518cd-109">Syntax</span><span class="sxs-lookup"><span data-stu-id="518cd-109">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="518cd-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="518cd-110">Parameters</span></span>

| <span data-ttu-id="518cd-111">Parameter</span><span class="sxs-lookup"><span data-stu-id="518cd-111">Parameter</span></span> | <span data-ttu-id="518cd-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="518cd-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="518cd-113">ProjektName</span><span class="sxs-lookup"><span data-stu-id="518cd-113">ProjectName</span></span> | <span data-ttu-id="518cd-114">(Erforderlich) Das Projekt, dem umleitungen für Bindungen hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="518cd-114">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="518cd-115">Der Projektname - Schalter ist optional.</span><span class="sxs-lookup"><span data-stu-id="518cd-115">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="518cd-116">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="518cd-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="518cd-117">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="518cd-117">Common Parameters</span></span>

<span data-ttu-id="518cd-118">`Add-BindingRedirect` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="518cd-118">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="518cd-119">Beispiele</span><span class="sxs-lookup"><span data-stu-id="518cd-119">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```