---
title: PowerShell-Referenz zu nuget-Paketen
description: Verweis auf den PowerShell-Befehl "Get-Package" in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 1c39fea2131b8f4b8a91314347a19366d5a582c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385192"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Paket-Manager-Konsole in Visual Studio)

*In diesem Thema wird der Befehl in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows beschrieben. Den allgemeinen PowerShell-Befehl Get-Package finden Sie in der [Referenz zu PowerShell packagemanagement](/powershell/module/packagemanagement/?view=powershell-6).*

Ruft die Liste der im lokalen Repository installierten Pakete ab, listet bei der Verwendung mit dem Schalter "-listavailable" die Pakete auf, die in einer Paketquelle verfügbar sind, oder listet verfügbare Updates auf, wenn Sie mit dem Schalter-Update verwendet werden.

## <a name="syntax"></a>Syntax

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Ohne Parameter zeigt `Get-Package` die Liste der Pakete an, die im Standard Projekt installiert sind.

## <a name="parameters"></a>Parameters

| Parameter | Beschreibung |
| --- | --- |
| Quelle | Die URL oder der Ordner Pfad für das Paket. Lokale Ordner Pfade können absolut oder relativ zum aktuellen Ordner sein. Wenn der Wert weggelassen wird, wird `Get-Package` die aktuell ausgewählte Paketquelle durchsucht. Bei Verwendung mit-listavailable wird standardmäßig auf nuget.org festgelegt. |
| ListAvailable | Listet die Pakete auf, die in einer Paketquelle verfügbar sind, und standardmäßig nuget.org. Zeigt einen Standardwert von 50-Paketen an, es sei denn, es werden-PageSize und/oder-First angegeben |
| Updates | Listet Pakete auf, für die ein Update in der Paketquelle verfügbar ist. |
| ProjektName | Das Projekt, aus dem installierte Pakete zu erhalten sind. Wenn der Wert nicht angezeigt wird, gibt die installierten Projekte für die gesamte Projekt Mappe |
| Filter | Eine Filter Zeichenfolge, die verwendet wird, um die Liste der Pakete einzugrenzen, indem Sie Sie auf die Paket-ID, die Beschreibung und Tags anwenden. |
| Erster | Die Anzahl der Pakete, die vom Anfang der Liste zurückgegeben werden sollen. Wenn nicht angegeben, wird standardmäßig 50 verwendet. |
| Überspringen | Lässt das erste &lt;int&gt; Paketen aus der angezeigten Liste aus.  |
| AllVersions | Zeigt alle verfügbaren Versionen der einzelnen Pakete anstelle der neuesten Version an. |
| Incluabprerelease | Schließt vorab Pakete in die Ergebnisse ein. |
| PageSize | *(3.0* und höher) Bei Verwendung mit-listavailable (erforderlich) die Anzahl der Pakete, die aufgelistet werden sollen, bevor eine Aufforderung zum Fortfahren angezeigt wird. |

Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Get-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.

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
