---
title: NuGet-Get-Package-PowerShell-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenz für die Get-Package-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
keywords: NuGet-Paket-Manager-Konsole NuGet Powershell-Befehle, NuGet Powershell-Referenz, Get-Package
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: ca80d95df309d8afce2ce6cff26c19980affde7a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Paket (Paket-Manager-Konsole in Visual Studio)

*In diesem Thema wird beschrieben, den Befehl innerhalb der [NuGet Package Manager Console](package-manager-console.md) in Visual Studio unter Windows. Der generische PowerShell Get-Package-Befehl finden Sie unter der [PowerShell PackageManagement-Verweis](/powershell/module/packagemanagement/?view=powershell-6).*

Ruft die Liste der Pakete, die im lokalen Repository installiert, listet die verfügbaren Pakete aus einem Paketquelle bei Verwendung mit dem Switch - ListAvailable oder verfügbaren Updates bei Verwendung mit dem Schalter Update aufgeführt.

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
| Quelle | Der URL oder einen Ordner Pfad für das Paket. Lokale Ordnerpfaden kann absolut oder relativ zum aktuellen Ordner. Wenn nicht angegeben, `Get-Package` die aktuell ausgewählten Paketquelle durchsucht. Bei Verwendung mit - ListAvailable, standardmäßig nuget.org. |
| ListAvailable | Listet die verfügbaren Pakete aus einem Paketquelle nuget.org direktionales. Zeigt den Standardwert von 50 Paketen an, es sei denn, - PageSize und/oder -erste angegeben werden. |
| Updates | Listet die Pakete, die in der Paketquelle ein Update verfügbar ist. |
| ProjektName | Das Projekt aus dem installierte Pakete abgerufen werden soll. Wenn nicht angegeben ist, installiert gibt Projekte für die gesamte Projektmappe. |
| Filter | Eine Filterzeichenfolge verwendet, um die Liste der Pakete eingrenzen, indem Sie die Paket-ID, die Beschreibung und den Tags zuweisen. |
| First | Die Anzahl der Pakete an, ab dem Anfang der Liste zurückgegeben. Wenn nicht angegeben ist, wird standardmäßig auf 50. |
| Skip | Lässt die erste &lt;Int&gt; Pakete aus der angezeigten Liste.  |
| AllVersions | Zeigt alle verfügbaren Versionen der einzelnen Pakete, anstatt nur die neueste Version. |
| IncludePrerelease | Enthält Vorabversionen von Paketen in den Ergebnissen an. |
| PageSize | *(3.0 +)*  Bei Verwendung mit - ListAvailable (erforderlich), die Anzahl der Pakete auflisten, die vor der Übergabe einer Eingabeaufforderung aus, um den Vorgang fortzusetzen. |

Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Get-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.

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
