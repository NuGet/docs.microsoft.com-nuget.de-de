---
title: NuGet Install-Package PowerShell-Referenz
description: Referenz zu Install-Package PowerShell-Befehl in der NuGet Paket-Manager Console in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ad551b8701cfc2061f7721fb050ed9b5a4fede32
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901693"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Paket-Manager-Konsole in Visual Studio)

*In diesem Thema wird der Befehl in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows beschrieben. Informationen zum generischen PowerShell Install-Package-Befehl finden Sie in der [PowerShell-PackageManagement-Referenz.](/powershell/module/packagemanagement)*

Installiert ein Paket und seine Abhängigkeiten in einem Projekt.

## <a name="syntax"></a>Syntax

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

Ab NuGet 2.8 `Install-Package` kann ein vorhandenes Paket in Ihrem Projekt herabgestuft werden. Wenn Sie beispielsweise Microsoft.AspNet.MVC 5.1.0-rc1 installiert haben, würde der folgende Befehl sie auf 5.0.0 herabstufen:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --- | --- |
| Id | (Erforderlich) Der Bezeichner des zu installierenden Pakets. (*3.0+*) Der Bezeichner kann ein Pfad oder eine URL einer `packages.config` Datei oder Datei `.nupkg` sein. Der Schalter -Id selbst ist optional. |
| IgnoreDependencies | Installieren Sie nur dieses Paket und nicht seine Abhängigkeiten. |
| ProjectName | Das Projekt, in dem das Paket installiert werden soll, wobei standardmäßig das Standardprojekt verwendet wird. |
| `Source` | Die URL oder der Ordnerpfad für die zu durchsuchende Paketquelle. Lokale Ordnerpfade können absolut oder relativ zum aktuellen Ordner sein. Wenn diese Option nicht angegeben ist, `Install-Package` wird die aktuell ausgewählte Paketquelle durchsucht. |
| Version | Die Version des zu installierenden Pakets, standardmäßig die neueste Version. |
| IncludePrerelease | Berücksichtigt Vorabversionspakete für die Installation. Wenn dieser Parameter nicht angegeben wird, werden nur stabile Pakete berücksichtigt. |
| FileConflictAction | Die Aktion, die beim Überschreiben oder Ignorieren vorhandener Dateien, auf die vom Projekt verwiesen wird, verwendet werden soll. Mögliche Werte sind *Overwrite, Ignore, None, OverwriteAll* und *(3.0+)* *IgnoreAll.* |
| DependencyVersion | Die Version der zu verwendenden Abhängigkeitspakete, die eines der folgenden sein kann:<br/><ul><li>*Niedrigste* (Standardeinstellung): die niedrigste Version</li><li>*HighestPatch:* Die Version mit der niedrigsten Hauptversion, der niedrigsten Nebenversion, dem höchsten Patch</li><li>*HighestMinor:* Die Version mit der niedrigsten Hauptversion, der höchsten Nebenversion und dem höchsten Patch</li><li>*Höchste* (Standardeinstellung für Update-Package ohne Parameter): die höchste Version</li></ul>Sie können den Standardwert mithilfe der [`dependencyVersion`](../nuget-config-file.md#config-section) Einstellung in der Datei `Nuget.Config` festlegen. |
| WhatIf | Zeigt an, was geschieht, wenn der Befehl ausgeführt wird, ohne die Installation tatsächlich auszuführen. |

Keiner dieser Parameter akzeptiert Pipelineeingaben oder Platzhalterzeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Install-Package` unterstützt die folgenden [allgemeinen PowerShell-Parameter:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction und WarningVariable.

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