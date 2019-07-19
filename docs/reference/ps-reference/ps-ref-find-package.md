---
title: PowerShell-Referenz zu nuget-PowerShell-Paketen
description: Referenz für den PowerShell-Befehl "Find-Package" in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4bb6d090b97dd55fc1be0625855aab27a0d181c4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327387"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Paket-Manager-Konsole in Visual Studio)

*Version 3.0 und höher in diesem Thema wird der Befehl in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows beschrieben. Den allgemeinen PowerShell-Befehl "Find-Package" finden Sie in der [Referenz zu PowerShell packagemanagement](/powershell/module/packagemanagement/?view=powershell-6).*

Ruft den Satz von Remote Paketen mit der angegebenen ID oder den angegebenen Schlüsselwörtern aus der Paketquelle ab.

## <a name="syntax"></a>Syntax

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --- | --- |
| ID &lt;-Schlüsselwörter&gt; | Benötigten Schlüsselwörter, die beim Durchsuchen der Paketquelle verwendet werden sollen. Verwenden Sie-exactMatch, um nur Pakete zurückzugeben, deren Paket-ID mit den Schlüsselwörtern übereinstimmt. Wenn keine Schlüsselwörter angegeben werden `Find-Package` , wird von eine Liste mit den Top 20 Paketen nach Downloads oder der durch-First angegebenen Zahl zurückgegeben. Beachten Sie, dass-ID optional und ein No-op-Wert ist. |
| Source | Die URL oder der Ordner Pfad für die Paketquelle, die durchsucht werden soll. Lokale Ordner Pfade können absolut oder relativ zum aktuellen Ordner sein. Wenn kein Wert `Find-Package` angezeigt wird, wird die aktuell ausgewählte Paketquelle durchsucht. |
| AllVersions | Zeigt alle verfügbaren Versionen der einzelnen Pakete anstelle der neuesten Version an. |
| Erster | Die Anzahl der Pakete, die ab dem Anfang der Liste zurückgegeben werden sollen. der Standardwert ist 20. |
| Skip | Lässt die ersten &lt;int&gt; -Pakete aus der angezeigten Liste aus.  |
| Incluabprerelease | Schließt vorab Pakete in die Ergebnisse ein. |
| "ExactMatch" | Wird angegeben, &lt;um&gt; Schlüsselwörter als Paket-ID zu verwenden |
| Startmit | Gibt Pakete zurück, deren Paket- &lt;ID&gt;mit Schlüsselwörtern beginnt. |

Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Find-Package`unterstützt die folgenden [allgemeinen PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.

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
