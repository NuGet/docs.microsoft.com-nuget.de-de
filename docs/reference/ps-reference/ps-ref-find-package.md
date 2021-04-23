---
title: NuGet Find-Package PowerShell-Referenz
description: Referenz zu Find-Package PowerShell-Befehl in der NuGet Paket-Manager Console in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 263835da64340a13737b32ab54ab057cb640a080
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901758"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Paket-Manager-Konsole in Visual Studio)

*Version 3.0+; In diesem Thema wird der Befehl in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows beschrieben. Informationen zum generischen PowerShell Find-Package-Befehl finden Sie in der [PowerShell-PackageManagement-Referenz.](/powershell/module/packagemanagement)*

Ruft den Satz von Remotepaketen mit der angegebenen ID oder den angegebenen Schlüsselwörtern aus der Paketquelle ab.

## <a name="syntax"></a>Syntax

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --- | --- |
| &lt;ID-Schlüsselwörter&gt; | (Erforderlich) Schlüsselwörter, die beim Durchsuchen der Paketquelle verwendet werden sollen. Verwenden Sie -ExactMatch, um nur die Pakete zurückzugeben, deren Paket-ID mit den Schlüsselwörtern übereinstimmt. Wenn keine Schlüsselwörter angegeben werden, `Find-Package` gibt eine Liste der 20 wichtigsten Pakete nach Downloads oder die von -First angegebene Anzahl zurück. Beachten Sie, dass -Id optional und no-op ist. |
| `Source` | Die URL oder der Ordnerpfad für die zu durchsuchende Paketquelle. Lokale Ordnerpfade können absolut oder relativ zum aktuellen Ordner sein. Wenn diese Option nicht angegeben ist, `Find-Package` wird die aktuell ausgewählte Paketquelle durchsucht. |
| AllVersions | Zeigt alle verfügbaren Versionen jedes Pakets anstelle der neuesten Version an. |
| First | Die Anzahl der Pakete, die am Anfang der Liste zurückgegeben werden sollen. der Standardwert ist 20. |
| Überspringen | Lässt die ersten &lt; &gt; int-Pakete aus der angezeigten Liste aus.  |
| IncludePrerelease | Schließt Vorabversionspakete in die Ergebnisse ein. |
| ExactMatch | Wird angegeben, um Schlüsselwörter als Paket-ID zu verwenden, bei der &lt; &gt; die Groß-/Kleinschreibung beachtet wird. |
| StartWith | Gibt Pakete zurück, deren Paket-ID mit den Schlüsselwörtern &lt; &gt; beginnt. |

Keiner dieser Parameter akzeptiert Pipelineeingaben oder Platzhalterzeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Find-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```