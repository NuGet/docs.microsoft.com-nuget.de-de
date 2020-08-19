---
title: PowerShell-Referenz zu nuget-bindingRedirect
description: Referenz für den PowerShell-Befehl "Add-bindingRedirect" in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f5ba4bd8140fa8cac7da8bf1351ad5448671b768
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623122"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="c9308-103">Add-bindingRedirect (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="c9308-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="c9308-104">*Nur in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows verfügbar.*</span><span class="sxs-lookup"><span data-stu-id="c9308-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="c9308-105">Untersucht alle Assemblys im Ausgabepfad für ein Projekt und fügt bei Bedarf Bindungs Umleitungen zur Anwendung oder Webkonfigurationsdatei hinzu.</span><span class="sxs-lookup"><span data-stu-id="c9308-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="c9308-106">Dieser Befehl wird automatisch ausgeführt, wenn ein Paket installiert wird.</span><span class="sxs-lookup"><span data-stu-id="c9308-106">This command is run automatically when installing a package.</span></span>

> [!NOTE]
> <span data-ttu-id="c9308-107">Dies gilt nur für Szenarien, in denen eine packages.config Datei verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="c9308-107">This only applies to scenarios using a packages.config file.</span></span> <span data-ttu-id="c9308-108">Weitere Informationen finden Sie unter [nuget-packages.config Dateireferenz](~/reference/packages-config.md).</span><span class="sxs-lookup"><span data-stu-id="c9308-108">For more information, see [NuGet packages.config file reference](~/reference/packages-config.md).</span></span>

<span data-ttu-id="c9308-109">Ausführliche Informationen zu Bindungs Umleitungen und deren Verwendung finden Sie unter [umleiten](/dotnet/framework/configure-apps/redirect-assembly-versions) von Assemblyversionen in der .NET-Dokumentation.</span><span class="sxs-lookup"><span data-stu-id="c9308-109">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="c9308-110">Syntax</span><span class="sxs-lookup"><span data-stu-id="c9308-110">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="c9308-111">Parameter</span><span class="sxs-lookup"><span data-stu-id="c9308-111">Parameters</span></span>

| <span data-ttu-id="c9308-112">Parameter</span><span class="sxs-lookup"><span data-stu-id="c9308-112">Parameter</span></span> | <span data-ttu-id="c9308-113">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="c9308-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c9308-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="c9308-114">ProjectName</span></span> | <span data-ttu-id="c9308-115">Benötigten Das Projekt, dem Bindungs Umleitungen hinzugefügt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="c9308-115">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="c9308-116">Der Schalter "-ProjectName" ist optional.</span><span class="sxs-lookup"><span data-stu-id="c9308-116">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="c9308-117">Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.</span><span class="sxs-lookup"><span data-stu-id="c9308-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="c9308-118">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="c9308-118">Common Parameters</span></span>

<span data-ttu-id="c9308-119">`Add-BindingRedirect` unterstützt die folgenden [allgemeinen PowerShell-Parameter](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c9308-119">`Add-BindingRedirect` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="c9308-120">Beispiele</span><span class="sxs-lookup"><span data-stu-id="c9308-120">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```
