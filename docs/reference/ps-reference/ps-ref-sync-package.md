---
title: Nuget-Sync-Package PowerShell-Referenz
description: Referenz für Sync-Package PowerShell-Befehl in der nuget-Paket-Manager-Konsole in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 4261b0a20a4fd4183f7b08096c3477e6f9d0a02d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777399"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (Paket-Manager-Konsole in Visual Studio)

*Version 3.0 und höher nur in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows verfügbar.*

Ruft die Version des installierten Pakets aus dem angegebenen (oder standardmäßigen) Projekt ab und synchronisiert die Version mit dem Rest der Projekte in der Projekt Mappe.

## <a name="syntax"></a>Syntax

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --- | --- |
| Id | Benötigten Der Bezeichner des zu synchronisierenden Pakets. Der Schalter-ID selbst ist optional. |
| Ignoreabhängigkeiten | Installieren Sie nur dieses Paket und nicht seine Abhängigkeiten. |
| ProjectName | Das Projekt, von dem das Paket synchronisiert wird, und standardmäßig das Standard Projekt. |
| Version | Die Version des zu synchronisierenden Pakets, wobei die aktuell installierte Version standardmäßig installiert ist. |
| `Source` | Die URL oder der Ordner Pfad für die Paketquelle, die durchsucht werden soll. Lokale Ordner Pfade können absolut oder relativ zum aktuellen Ordner sein. Wenn kein Wert angezeigt wird, wird `Sync-Package` die aktuell ausgewählte Paketquelle durchsucht. |
| Incluabprerelease | Schließt vorab Pakete in die Synchronisierung ein. |
| Fileconflictaction | Die Aktion, die ausgeführt werden soll, wenn die vom Projekt referenzierten Dateien überschrieben oder ignoriert werden sollen. Mögliche Werte sind " *überschreiben", "ignorieren", "keine", "überschreiben*" und " *(3.0 +)* *IgnoreAll*". |
| Dependencyversion | Die Version der zu verwendenden Abhängigkeits Pakete. Dies kann eine der folgenden sein:<br/><ul><li>*Niedrigste* (Standard): die niedrigste Version</li><li>*Highestpatch*: die Version mit dem niedrigsten, niedrigsten, niedrigsten, größten Patch</li><li>*Highestminor*: die Version mit dem niedrigsten Haupt-, höchst-und Höchstwert</li><li>*Höchste* (Standardeinstellung für Update-Package ohne Parameter): die höchste Version</li></ul>Sie können den Standardwert mithilfe der- [`dependencyVersion`](../nuget-config-file.md#config-section) Einstellung in der `Nuget.Config` Datei festlegen. |
| WhatIf | Zeigt, was geschehen würde, wenn der Befehl ausgeführt wird, ohne die Synchronisierung tatsächlich auszuführen. |

Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Sync-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.

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