---
title: Nuget-installationspaketpowershell-Referenz
description: Referenz für den PowerShell-Befehl "Install-Package" in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: a65ba63ed070f40e82c43d12e5fad12d86f28112
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384440"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Paket-Manager-Konsole in Visual Studio)

*In diesem Thema wird der Befehl in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows beschrieben. Den allgemeinen PowerShell-Befehl install-Package finden Sie in der [Referenz zu PowerShell packagemanagement](/powershell/module/packagemanagement/?view=powershell-6).*

Installiert ein Paket und seine Abhängigkeiten in einem-Projekt.

## <a name="syntax"></a>Syntax

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

In nuget 2.8 und höher können `Install-Package` ein vorhandenes Paket in Ihrem Projekt herabstufen. Wenn Sie z. b. Microsoft. Aspnet. MVC 5.1.0-RC1 installiert haben, würde der folgende Befehl das Downgrade auf 5.0.0 durchführt:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parameters

| Parameter | Beschreibung |
| --- | --- |
| ID | Benötigten Der Bezeichner des zu installierenden Pakets. (*3.0*und höher) Der Bezeichner kann ein Pfad oder eine URL einer `packages.config` Datei oder einer `.nupkg`-Datei sein. Der Schalter-ID selbst ist optional. |
| IgnoreDependencies | Installieren Sie nur dieses Paket und nicht seine Abhängigkeiten. |
| ProjektName | Das Projekt, in dem das Paket installiert werden soll, und standardmäßig das Standard Projekt. |
| Quelle | Die URL oder der Ordner Pfad für die Paketquelle, die durchsucht werden soll. Lokale Ordner Pfade können absolut oder relativ zum aktuellen Ordner sein. Wenn der Wert weggelassen wird, wird `Install-Package` die aktuell ausgewählte Paketquelle durchsucht. |
| Version | Die Version des zu installierenden Pakets, standardmäßig auf die neueste Version. |
| Incluabprerelease | Berücksichtigt vorab Pakete für die Installation. Wenn dieser Parameter nicht angegeben wird, werden nur stabile Pakete berücksichtigt. |
| FileConflictAction | Die Aktion, die ausgeführt werden soll, wenn die vom Projekt referenzierten Dateien überschrieben oder ignoriert werden sollen. Mögliche Werte sind " *überschreiben", "ignorieren", "keine", "überschreiben*" und " *(3.0 +)* *IgnoreAll*". |
| Dependencyversion | Die Version der zu verwendenden Abhängigkeits Pakete. Dies kann eine der folgenden sein:<br/><ul><li>*Niedrigste* (Standard): die niedrigste Version</li><li>*Highestpatch*: die Version mit dem niedrigsten, niedrigsten, niedrigsten, größten Patch</li><li>*Highestminor*: die Version mit dem niedrigsten Haupt-, höchst-und Höchstwert</li><li>*Höchste* (Standardeinstellung für Update-Package ohne Parameter): die höchste Version</li></ul>Sie können den Standardwert mithilfe der Einstellung [`dependencyVersion`](../nuget-config-file.md#config-section) in der `Nuget.Config`-Datei festlegen. |
| WhatIf | Zeigt, was geschehen würde, wenn der Befehl ausgeführt wird, ohne die Installation tatsächlich auszuführen. |

Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Install-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
