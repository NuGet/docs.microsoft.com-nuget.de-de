---
title: "Hinzufügen von NuGet-BindingRedirect-PowerShell-Referenz | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 90f4dcb0-6e5a-4948-8ea9-62e0d061d95a
description: "Referenz für die Add-BindingRedirect-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio."
keywords: NuGet-Paket-Manager-Konsole, die NuGet Powershell-Befehle, die NuGet Powershell-Referenz, Add-BindingRedirect
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6a3232af925f75713168421e68f2773060c5ebaa
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/05/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="3b369-104">Hinzufügen-BindingRedirect (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="3b369-104">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3b369-105">*Verfügbar nur innerhalb der [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="3b369-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="3b369-106">Untersucht alle Assemblys im Ausgabepfad auf ein Projekt, und der Anwendungs- oder Webkonfigurationsdatei Konfigurationsdatei umleitungen für Bindungen hinzugefügt, bei Bedarf.</span><span class="sxs-lookup"><span data-stu-id="3b369-106">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="3b369-107">Mit diesem Befehl wird automatisch ausgeführt, wenn Sie ein Paket zu installieren.</span><span class="sxs-lookup"><span data-stu-id="3b369-107">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="3b369-108">Ausführliche Informationen zu binden, leitet und warum sie verwendet werden, finden Sie unter [Umleiten von Assemblyversionen](/dotnet/framework/configure-apps/redirect-assembly-versions) in der Dokumentation zu .NET.</span><span class="sxs-lookup"><span data-stu-id="3b369-108">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="3b369-109">Syntax</span><span class="sxs-lookup"><span data-stu-id="3b369-109">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="3b369-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="3b369-110">Parameters</span></span>

| <span data-ttu-id="3b369-111">Parameter</span><span class="sxs-lookup"><span data-stu-id="3b369-111">Parameter</span></span> | <span data-ttu-id="3b369-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3b369-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3b369-113">ProjektName</span><span class="sxs-lookup"><span data-stu-id="3b369-113">ProjectName</span></span> | <span data-ttu-id="3b369-114">(Erforderlich) Das Projekt, dem umleitungen für Bindungen hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="3b369-114">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="3b369-115">Der Projektname - Schalter ist optional.</span><span class="sxs-lookup"><span data-stu-id="3b369-115">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="3b369-116">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="3b369-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3b369-117">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="3b369-117">Common Parameters</span></span>

<span data-ttu-id="3b369-118">`Add-BindingRedirect`unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3b369-118">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3b369-119">Beispiele</span><span class="sxs-lookup"><span data-stu-id="3b369-119">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```