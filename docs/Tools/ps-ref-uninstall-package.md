---
title: Deinstallieren Sie NuGet-Paket-PowerShell-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für Uninstall-Package-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio."
keywords: NuGet-Paket-Manager-Konsole NuGet Powershell-Befehle, NuGet Powershell-Referenz, Uninstall-Package
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: db7cf9b2282bf40988eee2308c256381c4fd5124
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Paket-Manager-Konsole in Visual Studio)

*In diesem Thema wird beschrieben, den Befehl innerhalb der [NuGet Package Manager Console](package-manager-console.md) in Visual Studio unter Windows. Der generische Deinstallationspaket für PowerShell-Befehl finden Sie unter der [PowerShell PackageManagement-Verweis](/powershell/module/packagemanagement/?view=powershell-6).*

Entfernt ein Paket aus einem Projekt, und optional die abhängigen Elemente entfernen. Wenn andere Pakete von diesem Paket abhängen, wird der Befehl fehl, es sei denn, der "– Force" angegeben wird.

## <a name="syntax"></a>Syntax

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Wenn andere Pakete von diesem Paket abhängen, wird der Befehl fehl, es sei denn, der "– Force" angegeben wird.

## <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --- | --- |
| Id | (Erforderlich) Der Bezeichner der zu deinstallierenden Pakets. Die - Id Schalter ist optional. |
| Version | Die Version des Pakets zu deinstallieren, die derzeit installierte Version auszuführen. |
| RemoveDependencies | Deinstallieren Sie das Paket und alle nicht verwendeten Abhängigkeiten. D. h., wenn eine der Abhängigkeiten ein anderes Paket, das von ihm abhängig ist aufweist, wird sie übersprungen. |
| ProjektName | Das Projekt, von dem das Paket, auf das Standardprojekt direktionales deinstalliert werden soll. |
| Force | Erzwingt, dass ein Paket deinstalliert werden, auch wenn andere Pakete von ihm abhängen. |
| WhatIf | Zeigt an, was passieren würde, wenn der Befehl ausgeführt wird, ohne die Deinstallation ausführen. |

Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Uninstall-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
