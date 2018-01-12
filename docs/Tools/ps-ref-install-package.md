---
title: NuGet-Install-Package-PowerShell-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 879db0ef-6b72-4a4a-bb68-f9e3a00f64b8
description: "Referenz für Install-Package-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio."
keywords: NuGet-Paket-Manager-Konsole NuGet Powershell-Befehle, NuGet Powershell-Referenz, Install-Package
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5da523d8b517a6867a86998dceaa1eba7b55b5fc
ms.sourcegitcommit: 51eae111f0fec4fbb21e5e702629beaa3e8abc2b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/10/2018
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Paket-Manager-Konsole in Visual Studio)

*In diesem Thema wird beschrieben, den Befehl innerhalb der [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio unter Windows. Der generische PowerShell Install-Package-Befehl finden Sie unter der [PowerShell PackageManagement-Verweis](/powershell/module/packagemanagement/?view=powershell-6).*

Installiert ein Paket und seine Abhängigkeiten in einem Projekt.

## <a name="syntax"></a>Syntax

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

Im NuGet 2.8 + `Install-Package` können Sie ein downgrade ein vorhandenes Paket im Projekt. Z. B. Wenn Sie Microsoft.AspNet.MVC 5.1.0-rc1 installiert haben, würde der folgende Befehl es 5.0.0 downgrade auf:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

NuGet 2.7 und früher erhalten eine Fehlermeldung, dass bereits eine neuere Version installiert ist.
  
## <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --- | --- |
| Id | (Erforderlich) Der Bezeichner des zu installierenden Pakets an. (*3.0 +*) der Bezeichner kann sein, einen Pfad oder URL des ein `packages.config` Datei oder ein `.nupkg` Datei. Die - Id Schalter ist optional. |
| MSI | Installieren Sie nur dieses Paket und nicht seine Abhängigkeiten. |
| ProjektName | Das Projekt, in dem das Paket, auf das Standardprojekt direktionales installiert werden soll. |
| Quelle | Die URL oder einen Ordnerpfad für die Paketquelle, gesucht werden soll. Lokale Ordnerpfaden kann absolut oder relativ zum aktuellen Ordner. Wenn nicht angegeben, `Install-Package` die aktuell ausgewählten Paketquelle durchsucht. |
| Version | Die Version des Pakets zu installieren, auf die neueste Version auszuführen. |
| IncludePrerelease | Vorabversionen von Paketen für die Installation wird berücksichtigt. Wenn nicht angegeben, werden nur stabile Pakete berücksichtigt. |
| FileConflictAction | Die zu ergreifende Maßnahme beim aufgefordert, überschreiben oder ignorieren Sie vorhandene Dateien, die vom Projekt verwiesen wird. Mögliche Werte sind *überschreiben, ignorieren, None, OverwriteAll*, und *(3.0 und höher)* *' ignoreall '*. |
| DependencyVersion | Die Version der abhängigkeitspakete zu verwenden, die in der folgenden Werte sind möglich:<br/><ul><li>*Niedrigste* (Standard): die niedrigste Version</li><li>*HighestPatch*: die Version mit der niedrigsten wichtigen, niedrigste Nebenversion, höchste Patch</li><li>*HighestMinor*: die Version mit der niedrigsten Hauptversion, die höchste Nebenversion, höchste Patch</li><li>*Höchste* (Standard für Update-Paket ohne Parameter): die höchste Version</li></ul>Sie können festlegen, den Standard-Wert mit der [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) festlegen in der `Nuget.Config` Datei. |
| "WhatIf" | Zeigt an, was passieren würde, wenn der Befehl ausgeführt wird, ohne die Installation ausführen. |

Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Install-Package`unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.

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
