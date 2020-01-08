---
title: Nuget-Deinstallations Paket PowerShell-Referenz
description: Referenz für den PowerShell-Befehl "Uninstall-Package" in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 05b7bf0e8abad0904b9e851ea6b7a5317e74229d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384414"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Paket-Manager-Konsole in Visual Studio)

*In diesem Thema wird der Befehl in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows beschrieben. Den allgemeinen PowerShell-Befehl "Uninstall-Package" finden Sie in der [Referenz zu PowerShell packagemanagement](/powershell/module/packagemanagement/?view=powershell-6).*

Entfernt ein Paket aus einem Projekt und entfernt optional seine Abhängigkeiten. Wenn andere Pakete von diesem Paket abhängen, tritt bei diesem Befehl nur dann kein Fehler auf, wenn die Option "-Force" angegeben wird.

## <a name="syntax"></a>Syntax

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Wenn andere Pakete von diesem Paket abhängen, tritt bei diesem Befehl nur dann kein Fehler auf, wenn die Option "-Force" angegeben wird.

## <a name="parameters"></a>Parameters

| Parameter | Beschreibung |
| --- | --- |
| ID | Benötigten Der Bezeichner des zu deinstallierenden Pakets. Der Schalter-ID selbst ist optional. |
| Version | Die Version des zu deinstallierenden Pakets, wobei die aktuell installierte Version standardmäßig installiert ist. |
| Removeabhängigkeiten | Deinstallieren Sie das Paket und seine nicht verwendeten Abhängigkeiten. Das heißt, wenn eine Abhängigkeit über ein anderes Paket verfügt, das davon abhängt, wird Sie übersprungen. |
| ProjektName | Das Projekt, aus dem das Paket deinstalliert werden soll, und standardmäßig das Standard Projekt. |
| Force | Erzwingt, dass ein Paket deinstalliert wird, auch wenn andere Pakete davon abhängig sind. |
| WhatIf | Zeigt, was geschehen würde, wenn der Befehl ausgeführt wird, ohne die Deinstallation tatsächlich auszuführen. |

Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Uninstall-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
