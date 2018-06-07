---
title: Hinzufügen von NuGet-BindingRedirect-PowerShell-Referenz
description: Referenz für die Add-BindingRedirect-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f3addd95b64d78eac201deeb2c64915ea935cd71
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817622"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="4af0d-103">Add-BindingRedirect (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="4af0d-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4af0d-104">*Verfügbar nur innerhalb der [NuGet Package Manager Console](package-manager-console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="4af0d-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="4af0d-105">Untersucht alle Assemblys im Ausgabepfad auf ein Projekt, und der Anwendungs- oder Webkonfigurationsdatei Konfigurationsdatei umleitungen für Bindungen hinzugefügt, bei Bedarf.</span><span class="sxs-lookup"><span data-stu-id="4af0d-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="4af0d-106">Mit diesem Befehl wird automatisch ausgeführt, wenn Sie ein Paket zu installieren.</span><span class="sxs-lookup"><span data-stu-id="4af0d-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="4af0d-107">Ausführliche Informationen zu binden, leitet und warum sie verwendet werden, finden Sie unter [Umleiten von Assemblyversionen](/dotnet/framework/configure-apps/redirect-assembly-versions) in der Dokumentation zu .NET.</span><span class="sxs-lookup"><span data-stu-id="4af0d-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="4af0d-108">Syntax</span><span class="sxs-lookup"><span data-stu-id="4af0d-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="4af0d-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="4af0d-109">Parameters</span></span>

| <span data-ttu-id="4af0d-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="4af0d-110">Parameter</span></span> | <span data-ttu-id="4af0d-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="4af0d-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4af0d-112">ProjektName</span><span class="sxs-lookup"><span data-stu-id="4af0d-112">ProjectName</span></span> | <span data-ttu-id="4af0d-113">(Erforderlich) Das Projekt, dem umleitungen für Bindungen hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="4af0d-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="4af0d-114">Der Projektname - Schalter ist optional.</span><span class="sxs-lookup"><span data-stu-id="4af0d-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="4af0d-115">Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="4af0d-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4af0d-116">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="4af0d-116">Common Parameters</span></span>

<span data-ttu-id="4af0d-117">`Add-BindingRedirect` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="4af0d-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4af0d-118">Beispiele</span><span class="sxs-lookup"><span data-stu-id="4af0d-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```