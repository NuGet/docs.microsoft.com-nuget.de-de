---
title: Nuget-Uninstall-Package PowerShell-Referenz
description: Referenz für Uninstall-Package PowerShell-Befehl in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: d164176355e32e5bbe0a017fc2b291cbc9ef326a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237126"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Paket-Manager-Konsole in Visual Studio)

*In diesem Thema wird der Befehl in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows beschrieben. Den allgemeinen PowerShell-Uninstall-Package Befehl finden Sie in der [Referenz zu PowerShell packagemanagement](/powershell/module/packagemanagement/?view=powershell-6).*

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
| Id | Benötigten Der Bezeichner des zu deinstallierenden Pakets. Der Schalter-ID selbst ist optional. |
| Version | Die Version des zu deinstallierenden Pakets, wobei die aktuell installierte Version standardmäßig installiert ist. |
| Removeabhängigkeiten | Deinstallieren Sie das Paket und seine nicht verwendeten Abhängigkeiten. Das heißt, wenn eine Abhängigkeit über ein anderes Paket verfügt, das davon abhängt, wird Sie übersprungen. |
| ProjectName | Das Projekt, aus dem das Paket deinstalliert werden soll, und standardmäßig das Standard Projekt. |
| Force | Erzwingt, dass ein Paket deinstalliert wird, auch wenn andere Pakete davon abhängig sind. |
| WhatIf | Zeigt, was geschehen würde, wenn der Befehl ausgeführt wird, ohne die Deinstallation tatsächlich auszuführen. |

Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Uninstall-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```