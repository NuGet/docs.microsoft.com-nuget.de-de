---
title: Nuget-Get-Package PowerShell-Referenz
description: Referenz für Get-Package PowerShell-Befehl in der nuget-Paket-Manager-Konsole in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8394f888ec3d5e57eacd351a4867173da1070ead
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777496"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Paket-Manager-Konsole in Visual Studio)

*In diesem Thema wird der Befehl in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows beschrieben. Den allgemeinen PowerShell-Get-Package Befehl finden Sie in der [Referenz zu PowerShell packagemanagement](/powershell/module/packagemanagement/?view=powershell-6).*

Ruft die Liste der im lokalen Repository installierten Pakete ab, listet bei der Verwendung mit dem Schalter "-listavailable" die Pakete auf, die in einer Paketquelle verfügbar sind, oder listet verfügbare Updates auf, wenn Sie mit dem Schalter-Update verwendet werden.

## <a name="syntax"></a>Syntax

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Ohne Parameter `Get-Package` zeigt die Liste der Pakete an, die im Standard Projekt installiert sind.

## <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --- | --- |
| `Source` | Die URL oder der Ordner Pfad für das Paket. Lokale Ordner Pfade können absolut oder relativ zum aktuellen Ordner sein. Wenn kein Wert angezeigt wird, wird `Get-Package` die aktuell ausgewählte Paketquelle durchsucht. Bei Verwendung mit-listavailable wird standardmäßig auf nuget.org festgelegt. |
| ListAvailable | Listet die Pakete auf, die in einer Paketquelle verfügbar sind, und standardmäßig nuget.org. Zeigt einen Standardwert von 50-Paketen an, es sei denn, es werden-PageSize und/oder-First angegeben |
| Aktualisierungen | Listet Pakete auf, für die ein Update in der Paketquelle verfügbar ist. |
| ProjectName | Das Projekt, aus dem installierte Pakete zu erhalten sind. Wenn der Wert nicht angezeigt wird, gibt die installierten Projekte für die gesamte Projekt Mappe |
| Filtern | Eine Filter Zeichenfolge, die verwendet wird, um die Liste der Pakete einzugrenzen, indem Sie Sie auf die Paket-ID, die Beschreibung und Tags anwenden. |
| First | Die Anzahl der Pakete, die vom Anfang der Liste zurückgegeben werden sollen. Wenn nicht angegeben, wird standardmäßig 50 verwendet. |
| Überspringen | Lässt die ersten &lt; int- &gt; Pakete aus der angezeigten Liste aus.  |
| AllVersions | Zeigt alle verfügbaren Versionen der einzelnen Pakete anstelle der neuesten Version an. |
| Incluabprerelease | Schließt vorab Pakete in die Ergebnisse ein. |
| PageSize | *(3.0* und höher) Bei Verwendung mit-listavailable (erforderlich) die Anzahl der Pakete, die aufgelistet werden sollen, bevor eine Aufforderung zum Fortfahren angezeigt wird. |

Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Get-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```