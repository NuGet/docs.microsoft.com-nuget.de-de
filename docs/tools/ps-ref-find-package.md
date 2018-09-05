---
title: NuGet Find-Package-PowerShell-Referenz
description: Referenz für die Find-Package-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: c6797e3778c7095a9abfc6cd87e2337313988c20
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550977"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Paket-Manager-Konsole in Visual Studio)

*Version 3.0 und höher; In diesem Thema wird beschrieben, den Befehl in der [NuGet-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows. Der generische PowerShell Find-Package-Befehl finden Sie unter den [PowerShell PackageManagement-Verweis](/powershell/module/packagemanagement/?view=powershell-6).*

Ruft die remotepakete mit der angegebenen ID oder Schlüsselwörter aus der Paketquelle ab.

## <a name="syntax"></a>Syntax

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --- | --- |
| ID &lt;Schlüsselwörter&gt; | (Erforderlich) Schlüsselwörter aufgelistet, die bei der Suche von der Paketquelle. Verwenden Sie-"exactMatch", um nur die Pakete zurückzugeben, dessen Paket-ID, die Schlüsselwörter entspricht. Wenn keine Schlüsselwörter angegeben sind, `Find-Package` gibt eine Liste der Top-20-Pakete durch Downloads oder die Anzahl anhand des - ersten. Beachten Sie, dass - Id optional ist und keine Aktion. |
| Quelle | Der URL oder Ordner Pfad für die Paketquelle, um zu suchen. Lokalen Ordnerpfade können absolut oder relativ zum aktuellen Ordner sein. Wenn nicht angegeben, `Find-Package` die aktuell ausgewählte Paketquelle durchsucht. |
| AllVersions | Zeigt alle verfügbare Versionen der einzelnen Pakete, anstatt nur die neueste Version. |
| First | Die Anzahl von Paketen ab dem Anfang der Liste zurückgegeben werden soll; Der Standardwert ist 20. |
| Skip | Lässt die erste &lt;Int&gt; Pakete aus der angezeigten Liste.  |
| IncludePrerelease | Enthält Vorabversionen von Paketen in den Ergebnissen. |
| "ExactMatch" | Verwendung von angegebenen &lt;Schlüsselwörter&gt; als Groß-/Kleinschreibung Paket-ID |
| StartWith | Gibt Pakete, deren Paket-ID beginnt mit &lt;Schlüsselwörter&gt;. |

Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Find-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction und WarningVariable.

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
