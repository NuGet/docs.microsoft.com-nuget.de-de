---
title: Nuget-Get-Project PowerShell-Referenz
description: Referenz für den getproject PowerShell-Befehl in der nuget-Paket-Manager-Konsole in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 16b3ffc0a375b8027c615020243a7289520715f8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777473"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Paket-Manager-Konsole in Visual Studio)

*Nur in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows verfügbar.*

Zeigt Informationen zum Standard-oder angegebenen Projekt an. `Get-Project` gibt speziell einen Referenten für das Visual Studio DTE-Objekt (Development Tools Environment) für das Projekt zurück.

## <a name="syntax"></a>Syntax

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --- | --- |
| Name | Gibt das anzuzeigende Projekt an. das Standard Projekt, das in der Paket-Manager-Konsole ausgewählt ist, wird standardmäßig angezeigt. Der Schalter "-Name" ist optional. |
| All | Zeigt Informationen für jedes Projekt in der Projekt Mappe an. die Reihenfolge der Projekte ist nicht deterministisch. |

Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Get-Project` unterstützt die folgenden [allgemeinen PowerShell-Parameter](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```