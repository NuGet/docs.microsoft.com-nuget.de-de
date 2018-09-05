---
title: Hinzufügen von NuGet-BindingRedirect-PowerShell-Referenz
description: Referenz für die Add-BindingRedirect-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: dec7db04c5cf239863b9c00e9f5bc0dde42c7e47
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551656"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="78cf9-103">Add-BindingRedirect (Paket-Manager-Konsole in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="78cf9-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="78cf9-104">*Verfügbar nur in der [NuGet-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows.*</span><span class="sxs-lookup"><span data-stu-id="78cf9-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="78cf9-105">Untersucht alle Assemblys im Ausgabepfad für ein Projekt, und der Konfigurationsdatei Anwendungs- oder Webkonfigurationsdatei bindungsweiterleitungen hinzugefügt, bei Bedarf.</span><span class="sxs-lookup"><span data-stu-id="78cf9-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="78cf9-106">Mit diesem Befehl wird automatisch ausgeführt, wenn Sie ein Paket zu installieren.</span><span class="sxs-lookup"><span data-stu-id="78cf9-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="78cf9-107">Ausführliche Informationen zum Binden von umleitungen und warum sie verwendet werden, finden Sie unter [Umleiten von Assemblyversionen](/dotnet/framework/configure-apps/redirect-assembly-versions) in der .NET-Dokumentation.</span><span class="sxs-lookup"><span data-stu-id="78cf9-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="78cf9-108">Syntax</span><span class="sxs-lookup"><span data-stu-id="78cf9-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="78cf9-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="78cf9-109">Parameters</span></span>

| <span data-ttu-id="78cf9-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="78cf9-110">Parameter</span></span> | <span data-ttu-id="78cf9-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="78cf9-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="78cf9-112">ProjektName</span><span class="sxs-lookup"><span data-stu-id="78cf9-112">ProjectName</span></span> | <span data-ttu-id="78cf9-113">(Erforderlich) Das Projekt, dem bindungsweiterleitungen hinzugefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="78cf9-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="78cf9-114">Der Schalter - Projektname ist optional.</span><span class="sxs-lookup"><span data-stu-id="78cf9-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="78cf9-115">Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.</span><span class="sxs-lookup"><span data-stu-id="78cf9-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="78cf9-116">Allgemeine Parameter</span><span class="sxs-lookup"><span data-stu-id="78cf9-116">Common Parameters</span></span>

<span data-ttu-id="78cf9-117">`Add-BindingRedirect` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction und WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="78cf9-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="78cf9-118">Beispiele</span><span class="sxs-lookup"><span data-stu-id="78cf9-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```