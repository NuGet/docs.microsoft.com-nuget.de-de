---
title: Sync-NuGet-Pakets PowerShell-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für die Sync-Paket-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio."
keywords: NuGet-Paket-Manager-Konsole, die NuGet Powershell-Befehle, die NuGet Powershell-Referenz, Sync-Pakets
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 02233cd0532fab2338e65e0d58b9afc3e2dab6af
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Paket (Paket-Manager-Konsole in Visual Studio)

*Version 3.0 +; verfügbar nur innerhalb der [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio unter Windows.*

Ruft die Version des installierten Pakets aus einer angegebenen (oder Standard)-Projekt und synchronisiert die Version mit den restlichen Projekten in der Projektmappe.

## <a name="syntax"></a>Syntax

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --- | --- |
| Id | (Erforderlich) Der Bezeichner des Pakets zu synchronisieren. Die - Id Schalter ist optional. |
| IgnoreDependencies | Installieren Sie nur dieses Paket und nicht seine Abhängigkeiten. |
| ProjektName | Das Projekt, um das Paket aus, auf das Standardprojekt direktionales zu synchronisieren. |
| Version | Die Version des Pakets zu synchronisieren, die derzeit installierte Version auszuführen. |
| Quelle | Die URL oder einen Ordnerpfad für die Paketquelle, gesucht werden soll. Lokale Ordnerpfaden kann absolut oder relativ zum aktuellen Ordner. Wenn nicht angegeben, `Sync-Package` die aktuell ausgewählten Paketquelle durchsucht. |
| IncludePrerelease | Enthält vorabversionspakete in die Synchronisierung. |
| FileConflictAction | Die zu ergreifende Maßnahme beim aufgefordert, überschreiben oder ignorieren Sie vorhandene Dateien, die vom Projekt verwiesen wird. Mögliche Werte sind *überschreiben, ignorieren, None, OverwriteAll*, und *(3.0 und höher)* *' ignoreall '*. |
| DependencyVersion | Die Version der abhängigkeitspakete zu verwenden, die in der folgenden Werte sind möglich:<br/><ul><li>*Niedrigste* (Standard): die niedrigste Version</li><li>*HighestPatch*: die Version mit der niedrigsten wichtigen, niedrigste Nebenversion, höchste Patch</li><li>*HighestMinor*: die Version mit der niedrigsten Hauptversion, die höchste Nebenversion, höchste Patch</li><li>*Höchste* (Standard für Update-Paket ohne Parameter): die höchste Version</li></ul>Sie können festlegen, den Standard-Wert mit der [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) festlegen in der `Nuget.Config` Datei. |
| WhatIf | Zeigt an, was passieren würde, wenn der Befehl ausgeführt wird, ohne die Synchronisierung ausführen. |

Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Sync-Package`unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.

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
