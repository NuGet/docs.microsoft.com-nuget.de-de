---
title: NuGetUninstall-Package PowerShell-Referenz
description: Referenz für Uninstall-Package PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 371e95c341efbce1c4a15facefc15cd51b266141
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901784"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Paket-Manager-Konsole in Visual Studio)

*In diesem Thema wird der Befehl in der [Paket-Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio Windows beschrieben. Den generischen PowerShellUninstall-Package befehl finden Sie in der [Referenz zu PowerShell PackageManagement.](/powershell/module/packagemanagement)*

Entfernt ein Paket aus einem Projekt und entfernt optional seine Abhängigkeiten. Wenn andere Pakete von diesem Paket abhängen, tritt bei diesem Befehl nur dann kein Fehler auf, wenn die Option "-Force" angegeben wird.

## <a name="syntax"></a>Syntax

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Wenn andere Pakete von diesem Paket abhängen, tritt bei diesem Befehl nur dann kein Fehler auf, wenn die Option "-Force" angegeben wird.

## <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --- | --- |
| Id | (Erforderlich) Der Bezeichner des zu deinstallierenden Pakets. Der Schalter -Id selbst ist optional. |
| Version | Die Version des zu deinstallierenden Pakets, standardmäßig die derzeit installierte Version. |
| RemoveDependencies | Deinstallieren Sie das Paket und seine nicht verwendeten Abhängigkeiten. Das heißt, wenn eine Abhängigkeit über ein anderes Paket verfügt, das davon abhängt, wird sie übersprungen. |
| ProjectName | Das Projekt, aus dem das Paket deinstalliert werden soll, standardmäßig das Standardprojekt. |
| Force | Erzwingt die Deinstallation eines Pakets, auch wenn andere Pakete davon abhängig sind. |
| WhatIf | Zeigt an, was geschieht, wenn der Befehl ausgeführt wird, ohne die Deinstallation tatsächlich auszuführen. |

Keiner dieser Parameter akzeptiert Pipelineeingaben oder Platzhalterzeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Uninstall-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```