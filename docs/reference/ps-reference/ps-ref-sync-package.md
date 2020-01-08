---
title: Nuget-Synchronisierungs Paket PowerShell-Referenz
description: Referenz für den PowerShell-Befehl "Sync-Package" in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 12a3d5f32056539a75da9e17b15d67e72a8a42c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384902"
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

## <a name="parameters"></a>Parameters

| Parameter | Beschreibung |
| --- | --- |
| ID | Benötigten Der Bezeichner des zu synchronisierenden Pakets. Der Schalter-ID selbst ist optional. |
| IgnoreDependencies | Installieren Sie nur dieses Paket und nicht seine Abhängigkeiten. |
| ProjektName | Das Projekt, von dem das Paket synchronisiert wird, und standardmäßig das Standard Projekt. |
| Version | Die Version des zu synchronisierenden Pakets, wobei die aktuell installierte Version standardmäßig installiert ist. |
| Quelle | Die URL oder der Ordner Pfad für die Paketquelle, die durchsucht werden soll. Lokale Ordner Pfade können absolut oder relativ zum aktuellen Ordner sein. Wenn der Wert weggelassen wird, wird `Sync-Package` die aktuell ausgewählte Paketquelle durchsucht. |
| Incluabprerelease | Schließt vorab Pakete in die Synchronisierung ein. |
| FileConflictAction | Die Aktion, die ausgeführt werden soll, wenn die vom Projekt referenzierten Dateien überschrieben oder ignoriert werden sollen. Mögliche Werte sind " *überschreiben", "ignorieren", "keine", "überschreiben*" und " *(3.0 +)* *IgnoreAll*". |
| Dependencyversion | Die Version der zu verwendenden Abhängigkeits Pakete. Dies kann eine der folgenden sein:<br/><ul><li>*Niedrigste* (Standard): die niedrigste Version</li><li>*Highestpatch*: die Version mit dem niedrigsten, niedrigsten, niedrigsten, größten Patch</li><li>*Highestminor*: die Version mit dem niedrigsten Haupt-, höchst-und Höchstwert</li><li>*Höchste* (Standardeinstellung für Update-Package ohne Parameter): die höchste Version</li></ul>Sie können den Standardwert mithilfe der Einstellung [`dependencyVersion`](../nuget-config-file.md#config-section) in der `Nuget.Config`-Datei festlegen. |
| WhatIf | Zeigt, was geschehen würde, wenn der Befehl ausgeführt wird, ohne die Synchronisierung tatsächlich auszuführen. |

Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Sync-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.

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
