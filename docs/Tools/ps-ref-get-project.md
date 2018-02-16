---
title: NuGet-Get-Projekt-PowerShell-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für GetProject-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio."
keywords: NuGet-Paket-Manager-Konsole NuGet Powershell-Befehle, NuGet Powershell-Referenz, Get-Projekt
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c347a6104d89bb29626ad7c2f33bec150eb38cd2
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/14/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Projekt (Paket-Manager-Konsole in Visual Studio)

*Verfügbar nur innerhalb der [NuGet Package Manager Console](package-manager-console.md) in Visual Studio unter Windows.*

Zeigt Informationen zu den Standardwert oder die angegebene Projekt. `Get-Project` insbesondere gibt eine "Referent" mit dem Visual Studio DTE (Development Tools Environment)-Objekt für das Projekt ein.

## <a name="syntax"></a>Syntax

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --- | --- |
| name | Gibt an, dass das Projekt, um anzuzeigen, in der Paket-Manager-Konsole ausgewählte Standardprojekt auszuführen. Der - Name Switch ist selbst optional. |
| Alle | Zeigt Informationen für jedes Projekt in der Projektmappe an. die Reihenfolge der Projekte ist nicht deterministisch. |

Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Get-Project` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```