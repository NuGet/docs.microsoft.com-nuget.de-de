---
title: PowerShell-Referenz zu nuget-PowerShell-Paketen
description: Referenz für den PowerShell-Befehl "Find-Package" in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4118b5a38f80a2300b3945738315d56bda096f9a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384632"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Paket-Manager-Konsole in Visual Studio)

*Version 3.0 und höher in diesem Thema wird der Befehl in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows beschrieben. Den allgemeinen PowerShell-Befehl "Find-Package" finden Sie in der [Referenz zu PowerShell packagemanagement](/powershell/module/packagemanagement/?view=powershell-6).*

Ruft den Satz von Remote Paketen mit der angegebenen ID oder den angegebenen Schlüsselwörtern aus der Paketquelle ab.

## <a name="syntax"></a>Syntax

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parameters

| Parameter | Beschreibung |
| --- | --- |
| ID &lt;Schlüsselwörter&gt; | Benötigten Schlüsselwörter, die beim Durchsuchen der Paketquelle verwendet werden sollen. Verwenden Sie-exactMatch, um nur Pakete zurückzugeben, deren Paket-ID mit den Schlüsselwörtern übereinstimmt. Wenn keine Schlüsselwörter angegeben werden, gibt `Find-Package` eine Liste mit den ersten 20 Paketen nach Downloads oder die durch-First angegebene Zahl zurück. Beachten Sie, dass-ID optional und ein No-op-Wert ist. |
| Quelle | Die URL oder der Ordner Pfad für die Paketquelle, die durchsucht werden soll. Lokale Ordner Pfade können absolut oder relativ zum aktuellen Ordner sein. Wenn der Wert weggelassen wird, wird `Find-Package` die aktuell ausgewählte Paketquelle durchsucht. |
| AllVersions | Zeigt alle verfügbaren Versionen der einzelnen Pakete anstelle der neuesten Version an. |
| Erster | Die Anzahl der Pakete, die ab dem Anfang der Liste zurückgegeben werden sollen. der Standardwert ist 20. |
| Überspringen | Lässt das erste &lt;int&gt; Paketen aus der angezeigten Liste aus.  |
| Incluabprerelease | Schließt vorab Pakete in die Ergebnisse ein. |
| ExactMatch | Gibt an, dass &lt;Schlüsselwörter&gt; als Paket-ID verwendet werden soll |
| StartWith | Gibt Pakete zurück, deren Paket-ID mit &lt;Schlüsselwörtern&gt;beginnt. |

Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Find-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.

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
