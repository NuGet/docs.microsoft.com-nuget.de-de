---
title: Sync-NuGet-Pakets PowerShell-Referenz
description: Referenz für die Synchronisierung-Package-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: de0b612e1335cafdcd6a0b802d54f2182d27ad22
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842251"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (Paket-Manager-Konsole in Visual Studio)

*Version 3.0 und höher; verfügbar nur in der [-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows.*

Ruft die Version des installierten Pakets vom angegebenen (oder Standard), project und synchronisiert die Version für den Rest der Projekte in der Projektmappe.

## <a name="syntax"></a>Syntax

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --- | --- |
| Id | (Erforderlich) Der Bezeichner des Pakets zu synchronisieren. Die - Id Switch selbst ist optional. |
| IgnoreDependencies | Installieren Sie nur dieses Paket und nicht seine Abhängigkeiten. |
| ProjektName | Das Projekt, das Paket aus, die als Standardprojekt zu synchronisieren. |
| Version | Die Version des Pakets zu synchronisieren, als die derzeit installierte Version. |
| Source | Der URL oder Ordner Pfad für die Paketquelle, um zu suchen. Lokalen Ordnerpfade können absolut oder relativ zum aktuellen Ordner sein. Wenn nicht angegeben, `Sync-Package` die aktuell ausgewählte Paketquelle durchsucht. |
| IncludePrerelease | Enthält Vorabversionen von Paketen, bei der Synchronisierung. |
| FileConflictAction | Die auszuführende Aktion, wenn aufgefordert, die überschrieben werden soll, oder ignorieren die vorhandene Dateien, die vom Projekt verwiesen wird. Mögliche Werte sind *überschreiben, die Sie keine "," OverwriteAll*, und *(3.0 und höher)* *' ignoreall '* . |
| DependencyVersion | Die Version des der abhängigkeitspakete zu verwenden, die in der folgenden Werte sind möglich:<br/><ul><li>*Niedrigste* (Standard): die niedrigste Version</li><li>*HighestPatch*: die Version mit der niedrigsten wichtigen, niedrigste kleinere, höchste Patch</li><li>*HighestMinor*: die Version mit der niedrigsten Hauptversion, die höchste kleinere, höchste-Patch</li><li>*Höchste* (Standard für Update-Package ohne Parameter): die höchste Version</li></ul>Sie können festlegen, den Standard-Wert mit der [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) festlegen in der `Nuget.Config` Datei. |
| WhatIf | Zeigt an, was geschieht, wenn der Befehl ausgeführt wird, ohne die Synchronisierung ausführen. |

Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Sync-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```
