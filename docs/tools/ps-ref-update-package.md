---
title: Update-NuGet-Paket-PowerShell-Referenz
description: Referenz für das Updatepaket PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 621e59633117a29c58fe643860ee7e2b40a4fbe2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Paket (Paket-Manager-Konsole in Visual Studio)

*Verfügbar nur innerhalb der [NuGet Package Manager Console](package-manager-console.md) in Visual Studio unter Windows.*

Aktualisiert ein Paket und seine Abhängigkeiten oder alle Pakete in einem Projekt auf eine neuere Version.

## <a name="syntax"></a>Syntax

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

Im NuGet 2.8 + `Update-Package` herabgestuft werden, ein vorhandenes Paket im Projekt verwendet werden können. Z. B. Wenn Sie Microsoft.AspNet.MVC 5.1.0-rc1 installiert haben, würde der folgende Befehl es 5.0.0 downgrade auf:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parameter

|  Parameter | Beschreibung |
| --- | --- |
| Id | Der Bezeichner des Pakets aktualisieren. Wenn nicht angegeben, aktualisiert alle Pakete aus. Die - Id Schalter ist optional. |
| IgnoreDependencies | Überspringt die Abhängigkeiten des Pakets aktualisieren. |
| ProjektName | Der Name des Projekts, enthält die Pakete zu aktualisieren, die Standardwerte für alle Projekte. |
| Version | Die Version, die für das Upgrade auf die neueste Version standardmäßig verwendet. In 3.0 + NuGet der Versionswert möglich *niedrigste, höchste, HighestMinor*, oder *HighestPatch* (gleichwertig mit "- Safe). |
| Safe | Schränkt Upgrades auf nur Versionen mit der gleichen Haupt- und Version als der derzeit installierten Paket. |
| Quelle | Die URL oder einen Ordnerpfad für die Paketquelle, gesucht werden soll. Lokale Ordnerpfaden kann absolut oder relativ zum aktuellen Ordner. Wenn nicht angegeben, `Update-Package` die aktuell ausgewählten Paketquelle durchsucht. |
| IncludePrerelease | Enthält nach Updates Vorabversionen von Paketen. |
| Neuinstallation | Resintalls-Pakete, die ihre aktuell installierten Versionen verwenden. Informationen dazu finden Sie unter [Neuinstallieren und Aktualisieren von Paketen](../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | Die zu ergreifende Maßnahme beim aufgefordert, überschreiben oder ignorieren Sie vorhandene Dateien, die vom Projekt verwiesen wird. Mögliche Werte sind *überschreiben, ignorieren, None, OverwriteAll*, und *' ignoreall '* (3.0 und höher). |
| DependencyVersion | Die Version der abhängigkeitspakete zu verwenden, die in der folgenden Werte sind möglich:<br/><ul><li>*Niedrigste* (Standard): die niedrigste Version</li><li>*HighestPatch*: die Version mit der niedrigsten wichtigen, niedrigste Nebenversion, höchste Patch</li><li>*HighestMinor*: die Version mit der niedrigsten Hauptversion, die höchste Nebenversion, höchste Patch</li><li>*Höchste* (Standard für Update-Paket ohne Parameter): die höchste Version</li></ul>Sie können festlegen, den Standard-Wert mit der [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) festlegen in der `Nuget.Config` Datei. |
| ToHighestPatch | Schränkt Upgrades nur Versionen mit der gleichen Nebenversion als der derzeit installierten Paket. |
| ToHighestMinor | Schränkt Upgrades nur Versionen mit der gleichen Hauptversion als der derzeit installierten Paket. |
| "WhatIf" | Zeigt an, was passieren würde, wenn der Befehl ausgeführt wird, ohne das Update ausführen. |

Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.

### <a name="common-parameters"></a>Allgemeine Parameter

`Update-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.

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
