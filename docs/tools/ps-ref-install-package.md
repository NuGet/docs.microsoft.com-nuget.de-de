---
title: NuGet-Installationspaket PowerShell-Referenz
description: Referenz für die Install-Package-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 755c87bbc68d3b688c81e16edbc1faabdc9e0520
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842499"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Paket-Manager-Konsole in Visual Studio)

*In diesem Thema wird beschrieben, den Befehl in der [-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows. Der generische Befehl der PowerShell-Install-Package, finden Sie unter den [PowerShell PackageManagement-Verweis](/powershell/module/packagemanagement/?view=powershell-6).*

Installiert ein Paket und seine Abhängigkeiten in ein Projekt an.

## <a name="syntax"></a>Syntax

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

In NuGet 2.8 und höher `Install-Package` kann ein vorhandenes Paket im Projekt "heruntergestuft". Z. B. Wenn Sie "Microsoft.Aspnet.Mvc" 5.1.0-rc1 installiert haben, würde der folgende Befehl sie ein Downgrade auf 5.0.0 durchführen:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --- | --- |
| Id | (Erforderlich) Der Bezeichner der zu installierenden Pakets an. (*3.0 +* ) der Bezeichner kann sein, einen Pfad oder URL von einem `packages.config` Datei oder ein `.nupkg` Datei. Die - Id Switch selbst ist optional. |
| IgnoreDependencies | Installieren Sie nur dieses Paket und nicht seine Abhängigkeiten. |
| ProjektName | Das Projekt in die zum Installieren des Pakets, das als Standardprojekt. |
| Source | Der URL oder Ordner Pfad für die Paketquelle, um zu suchen. Lokalen Ordnerpfade können absolut oder relativ zum aktuellen Ordner sein. Wenn nicht angegeben, `Install-Package` die aktuell ausgewählte Paketquelle durchsucht. |
| Version | Die Version des Pakets installiert werden, standardmäßig auf die neueste Version. |
| IncludePrerelease | Vorabversionen von Paketen für die Installation wird berücksichtigt. Wenn nicht angegeben, werden nur stabile Pakete berücksichtigt. |
| FileConflictAction | Die auszuführende Aktion, wenn aufgefordert, die überschrieben werden soll, oder ignorieren die vorhandene Dateien, die vom Projekt verwiesen wird. Mögliche Werte sind *überschreiben, die Sie keine "," OverwriteAll*, und *(3.0 und höher)* *' ignoreall '* . |
| DependencyVersion | Die Version des der abhängigkeitspakete zu verwenden, die in der folgenden Werte sind möglich:<br/><ul><li>*Niedrigste* (Standard): die niedrigste Version</li><li>*HighestPatch*: die Version mit der niedrigsten wichtigen, niedrigste kleinere, höchste Patch</li><li>*HighestMinor*: die Version mit der niedrigsten Hauptversion, die höchste kleinere, höchste-Patch</li><li>*Höchste* (Standard für Update-Package ohne Parameter): die höchste Version</li></ul>Sie können festlegen, den Standard-Wert mit der [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) festlegen in der `Nuget.Config` Datei. |
| WhatIf | Zeigt an, was geschieht, wenn der Befehl ausgeführt wird, ohne die Installation ausführen. |

Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Install-Package` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
