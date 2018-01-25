---
title: "Hinzufügen von NuGet-BindingRedirect-PowerShell-Referenz | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für die Add-BindingRedirect-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio."
keywords: NuGet-Paket-Manager-Konsole, die NuGet Powershell-Befehle, die NuGet Powershell-Referenz, Add-BindingRedirect
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b755970402f29a72b9a10f1a94e4a799e9cb71cf
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="dccfd-104">Hinzufügen-BindingRedirect (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="dccfd-104">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="dccfd-105">*Verfügbar nur innerhalb der [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="dccfd-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="dccfd-106">Untersucht alle Assemblys im Ausgabepfad auf ein Projekt, und der Anwendungs- oder Webkonfigurationsdatei Konfigurationsdatei umleitungen für Bindungen hinzugefügt, bei Bedarf.</span><span class="sxs-lookup"><span data-stu-id="dccfd-106">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="dccfd-107">Mit diesem Befehl wird automatisch ausgeführt, wenn Sie ein Paket zu installieren.</span><span class="sxs-lookup"><span data-stu-id="dccfd-107">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="dccfd-108">Ausführliche Informationen zu binden, leitet und warum sie verwendet werden, finden Sie unter [Umleiten von Assemblyversionen](/dotnet/framework/configure-apps/redirect-assembly-versions) in der Dokumentation zu .NET.</span><span class="sxs-lookup"><span data-stu-id="dccfd-108">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="dccfd-109">Syntax</span><span class="sxs-lookup"><span data-stu-id="dccfd-109">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="dccfd-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="dccfd-110">Parameters</span></span>

| <span data-ttu-id="dccfd-111">Parameter</span><span class="sxs-lookup"><span data-stu-id="dccfd-111">Parameter</span></span> | <span data-ttu-id="dccfd-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="dccfd-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dccfd-113">ProjektName</span><span class="sxs-lookup"><span data-stu-id="dccfd-113">ProjectName</span></span> | <span data-ttu-id="dccfd-114">(Erforderlich) Das Projekt, dem umleitungen für Bindungen hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="dccfd-114">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="dccfd-115">Der Projektname - Schalter ist optional.</span><span class="sxs-lookup"><span data-stu-id="dccfd-115">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="dccfd-116">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="dccfd-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="dccfd-117">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="dccfd-117">Common Parameters</span></span>

<span data-ttu-id="dccfd-118">`Add-BindingRedirect`unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="dccfd-118">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="dccfd-119">Beispiele</span><span class="sxs-lookup"><span data-stu-id="dccfd-119">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```