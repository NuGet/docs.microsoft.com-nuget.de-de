---
title: PowerShell-Referenz zu nuget-Project
description: Referenz für den getproject PowerShell-Befehl in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 3343952535c2d3c822f5cac24cb30c8f5bfa5be3
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384619"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Paket-Manager-Konsole in Visual Studio)

*Nur in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows verfügbar.*

Zeigt Informationen zum Standard-oder angegebenen Projekt an. `Get-Project` gibt speziell einen Referenten für das Visual Studio-DTE-Objekt (Development Tools Environment) für das Projekt zurück.

## <a name="syntax"></a>Syntax

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parameters

| Parameter | Beschreibung |
| --- | --- |
| -Name | Gibt das anzuzeigende Projekt an. das Standard Projekt, das in der Paket-Manager-Konsole ausgewählt ist, wird standardmäßig angezeigt. Der Schalter "-Name" ist optional. |
| Alle | Zeigt Informationen für jedes Projekt in der Projekt Mappe an. die Reihenfolge der Projekte ist nicht deterministisch. |

Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Get-Project` unterstützt die folgenden [allgemeinen PowerShell-Parameter](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```