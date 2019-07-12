---
title: Referenz zu PowerShell Get-NuGet-Paket
description: Referenz für die Get-Package-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d0d25cb6e21f6d0d42389e08340b6f1e1baf8a64
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842515"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Paket-Manager-Konsole in Visual Studio)

*In diesem Thema wird beschrieben, den Befehl in der [-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows. Der generische PowerShell Get-Package-Befehl finden Sie unter den [PowerShell PackageManagement-Verweis](/powershell/module/packagemanagement/?view=powershell-6).*

Ruft die Liste der Pakete, die im lokalen Repository installiert, listet die verfügbaren Pakete aus der Paketquelle bei Verwendung mit dem Switch - ListAvailable oder listet die verfügbaren Updates, die bei der Verwendung mit dem Update-Schalter.

## <a name="syntax"></a>Syntax

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Ohne Parameter `Get-Package` zeigt die Liste der im Standardprojekt installierten Pakete.

## <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --- | --- |
| Source | Der URL oder Ordner Pfad für das Paket. Lokalen Ordnerpfade können absolut oder relativ zum aktuellen Ordner sein. Wenn nicht angegeben, `Get-Package` die aktuell ausgewählte Paketquelle durchsucht. Bei Verwendung mit - ListAvailable, der Standardwert ist "NuGet.org". |
| ListAvailable | Listet die Pakete, die aus der Paketquelle, es wird der Standardwert "NuGet.org" verfügbar. Zeigt den Standardwert 50 Pakete an, es sei denn, der PageSize - und/oder - erste angegeben werden. |
| Updates | Listet die Pakete, die ein Update verfügbar, aus der Paketquelle ist. |
| ProjektName | Das Projekt aus dem installierte Paketen abgerufen werden soll. Wenn nicht angegeben ist, installiert gibt Projekte für die gesamte Projektmappe. |
| Filter | Eine Filterzeichenfolge verwendet, um die Liste der Pakete eingrenzen, indem es auf die Paket-ID, Beschreibung und Tags angewendet. |
| Erster | Die Anzahl von Paketen ab dem Anfang der Liste zurückgegeben werden soll. Wenn nicht angegeben ist, wird standardmäßig auf 50. |
| Skip | Lässt die erste &lt;Int&gt; Pakete aus der angezeigten Liste.  |
| AllVersions | Zeigt alle verfügbare Versionen der einzelnen Pakete, anstatt nur die neueste Version. |
| IncludePrerelease | Enthält Vorabversionen von Paketen in den Ergebnissen. |
| PageSize | *(3.0 und höher)*  Bei Verwendung mit - ListAvailable (erforderlich), die Anzahl der Pakete aufgelistet, die vor der Übergabe von einer Eingabeaufforderung aus, um den Vorgang fortzusetzen. |

Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Get-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction und WarningVariable.

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
