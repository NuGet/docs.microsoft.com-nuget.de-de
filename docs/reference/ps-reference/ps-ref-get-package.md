---
title: NuGet Get-Package PowerShell-Referenz
description: Referenz zu Get-Package PowerShell-Befehl in der NuGet Paket-Manager Console in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7c91faecaac2967c7a01dd81e72b9097e7bd6cae
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901732"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Paket-Manager-Konsole in Visual Studio)

*In diesem Thema wird der Befehl in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows beschrieben. Informationen zum generischen PowerShell Get-Package-Befehl finden Sie in der [PowerShell-PackageManagement-Referenz.](/powershell/module/packagemanagement)*

Ruft die Liste der pakete ab, die im lokalen Repository installiert sind, listet pakete auf, die von einer Paketquelle verfügbar sind, wenn sie mit dem Schalter -ListAvailable verwendet werden, oder listet verfügbare Updates auf, wenn sie mit dem Schalter -Update verwendet werden.

## <a name="syntax"></a>Syntax

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Ohne Parameter zeigt die Liste der pakete an, `Get-Package` die im Standardprojekt installiert sind.

## <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --- | --- |
| `Source` | Die URL oder der Ordnerpfad für das Paket . Lokale Ordnerpfade können absolut oder relativ zum aktuellen Ordner sein. Wenn diese Option nicht angegeben ist, `Get-Package` wird die aktuell ausgewählte Paketquelle durchsucht. Bei Verwendung mit -ListAvailable wird standardmäßig nuget.org. |
| ListAvailable | Listet Pakete auf, die aus einer Paketquelle verfügbar sind, standardmäßig nuget.org. Zeigt den Standardwert von 50 Paketen an, es sei denn, -PageSize und/oder -First sind angegeben. |
| Aktualisierungen | Listet Pakete auf, für die ein Update über die Paketquelle verfügbar ist. |
| ProjectName | Das Projekt, aus dem installierte Pakete abzurufen sind. Wenn keine Angabe erfolgt, werden installierte Projekte für die gesamte Projektmappe zurückgegeben. |
| Filter | Eine Filterzeichenfolge, die verwendet wird, um die Liste der Pakete einzugrenzen, indem sie auf die Paket-ID, Beschreibung und Tags angewendet wird. |
| First | Die Anzahl der Pakete, die am Anfang der Liste zurückgegeben werden sollen. Wenn keine Angabe erfolgt, wird standardmäßig 50 verwendet. |
| Überspringen | Lässt die ersten &lt; &gt; int-Pakete aus der angezeigten Liste aus.  |
| AllVersions | Zeigt alle verfügbaren Versionen jedes Pakets anstelle der neuesten Version an. |
| IncludePrerelease | Schließt Vorabversionspakete in die Ergebnisse ein. |
| PageSize | *(3.0 und mehr)* Bei Verwendung mit -ListAvailable (erforderlich) die Anzahl der Pakete, die vor der Eingabeaufforderung zum Fortfahren aufgeführt werden müssen. |

Keiner dieser Parameter akzeptiert Pipelineeingaben oder Platzhalterzeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Get-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction und WarningVariable.

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