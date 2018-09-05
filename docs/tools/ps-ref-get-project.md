---
title: NuGet-Get-Projekt-PowerShell-Referenz
description: Referenz für GetProject-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 849261711fafcadbab38bf6fe99340c4b79e1e21
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550436"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Paket-Manager-Konsole in Visual Studio)

*Verfügbar nur in der [NuGet-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows.*

Zeigt Informationen zu den Standardwert oder die angegebene Projekt. `Get-Project` insbesondere gibt eine Referent auf das Visual Studio DTE (Development Tools Environment)-Objekt, für das Projekt ein.

## <a name="syntax"></a>Syntax

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --- | --- |
| name | Gibt an, dass das Projekt angezeigt werden, als das standardmäßige-Projekt in der Paket-Manager-Konsole ausgewählt. Der - Name Schalter ist selbst optional. |
| Alle | Zeigt Informationen für jedes Projekt in der Projektmappe die Reihenfolge der Projekte ist nicht deterministisch. |

Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Get-Project` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```