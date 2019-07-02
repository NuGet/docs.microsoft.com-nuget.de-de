---
title: Update-NuGet-Paket-PowerShell-Referenz
description: Referenz für die Update-Package-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5b5a11ee11d9e2cf6a90d56ac63b1f7bad750ea
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496494"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (Paket-Manager-Konsole in Visual Studio)

*Verfügbar nur in der [NuGet-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows.*

Wird ein Paket und seine Abhängigkeiten oder alle Pakete in einem Projekt auf eine neuere Version aktualisiert.

## <a name="syntax"></a>Syntax

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

In NuGet 2.8 und höher `Update-Package` können verwendet werden, um ein vorhandenes Paket in Ihrem Projekt ein Downgrade durchführen. Z. B. Wenn Sie "Microsoft.Aspnet.Mvc" 5.1.0-rc1 installiert haben, würde der folgende Befehl sie ein Downgrade auf 5.0.0 durchführen:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parameter

|  Parameter | Beschreibung |
| --- | --- |
| Id | Der Bezeichner des Pakets aktualisiert werden soll. Wenn nicht angegeben, werden alle Pakete aktualisiert. Die - Id Switch selbst ist optional. |
| IgnoreDependencies | Überspringt die Abhängigkeiten des Pakets aktualisieren. |
| ProjektName | Der Name des Projekts, in dem Pakete aktualisiert, es wird der Standardwert für alle Projekte. |
| Version | Die Version, die für das Upgrade, standardmäßig auf die neueste Version verwendet. In NuGet 3.0 und höher der Wert muss einer der *niedrigste, höchste, HighestMinor*, oder *HighestPatch* (Äquivalent zu: Safe). |
| Safe | Schränkt Upgrades nur Versionen mit der gleichen Haupt- und Nebenversionen-Version als die derzeit installierten Paket. |
| Source | Der URL oder Ordner Pfad für die Paketquelle, um zu suchen. Lokalen Ordnerpfade können absolut oder relativ zum aktuellen Ordner sein. Wenn nicht angegeben, `Update-Package` die aktuell ausgewählte Paketquelle durchsucht. |
| IncludePrerelease | Enthält nach Updates Vorabversionen von Paketen. |
| Neuinstallation | Resintalls-Pakete, die ihre aktuell installierten Versionen verwenden. Informationen dazu finden Sie unter [Neuinstallieren und Aktualisieren von Paketen](../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | Die auszuführende Aktion, wenn aufgefordert, die überschrieben werden soll, oder ignorieren die vorhandene Dateien, die vom Projekt verwiesen wird. Mögliche Werte sind *überschreiben, die Sie keine "," OverwriteAll*, und *' ignoreall '* (3.0 und höher). |
| DependencyVersion | Die Version des der abhängigkeitspakete zu verwenden, die in der folgenden Werte sind möglich:<br/><ul><li>*Niedrigste* (Standard): die niedrigste Version</li><li>*HighestPatch*: die Version mit der niedrigsten wichtigen, niedrigste kleinere, höchste Patch</li><li>*HighestMinor*: die Version mit der niedrigsten Hauptversion, die höchste kleinere, höchste-Patch</li><li>*Höchste* (Standard für Update-Package ohne Parameter): die höchste Version</li></ul>Sie können festlegen, den Standard-Wert mit der [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) festlegen in der `Nuget.Config` Datei. |
| ToHighestPatch | Äquivalent zu – sicher. |
| ToHighestMinor | Schränkt Upgrades nur Versionen mit derselben Hauptversion als die derzeit installierten Paket. |
| WhatIf | Zeigt an, was geschieht, wenn der Befehl ausgeführt wird, ohne das Update ausführen. |

Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.

### <a name="common-parameters"></a>Allgemeine Parameter

`Update-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction und WarningVariable.

### <a name="examples"></a>Beispiele

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
