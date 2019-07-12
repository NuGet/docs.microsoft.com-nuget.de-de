---
title: Deinstallieren von NuGet-Paket-PowerShell-Referenz
description: Referenz für die Uninstall-Package-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: c95479103be2cba3b4eb6964ea761870477863bd
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842473"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Paket-Manager-Konsole in Visual Studio)

*In diesem Thema wird beschrieben, den Befehl in der [-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows. Der generische PowerShell Uninstall-Package-Befehl finden Sie unter den [PowerShell PackageManagement-Verweis](/powershell/module/packagemanagement/?view=powershell-6).*

Entfernt ein Paket aus einem Projekt, und seine Abhängigkeiten optional zu entfernen. Wenn dieses Paket andere Pakete abhängig sind, wird der Befehl fehl, es sei denn, das – Force angegeben wird.

## <a name="syntax"></a>Syntax

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Wenn dieses Paket andere Pakete abhängig sind, wird der Befehl fehl, es sei denn, das – Force angegeben wird.

## <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --- | --- |
| Id | (Erforderlich) Der Bezeichner des Pakets deinstallieren. Die - Id Switch selbst ist optional. |
| Version | Die Version des Pakets zu deinstallieren, als die derzeit installierte Version. |
| RemoveDependencies | Deinstallieren Sie das Paket und seine nicht verwendeten Abhängigkeiten. D. h. wird eine Abhängigkeit ein weiteres Paket aufweist, das von ihr abhängig ist, es übersprungen. |
| ProjektName | Das Projekt aus dem Deinstallieren des Pakets, das als Standardprojekt. |
| Force | Erzwingt, dass ein Paket deinstalliert werden, auch wenn andere Pakete davon abhängig sind. |
| WhatIf | Zeigt an, was geschieht, wenn der Befehl ausgeführt wird, ohne die Deinstallation ausführen. |

Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Uninstall-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
