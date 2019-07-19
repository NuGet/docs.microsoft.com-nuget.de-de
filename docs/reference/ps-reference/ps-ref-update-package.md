---
title: Nuget-Update-Paket-PowerShell-Referenz
description: Referenz für den PowerShell-Befehl "Update-Package" in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 57e50ed805496b3511bc3b808f89da6f7ad413fc
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327267"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (Paket-Manager-Konsole in Visual Studio)

*Nur in der [nuget-Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows verfügbar.*

Aktualisiert ein Paket und seine Abhängigkeiten oder alle Pakete in einem Projekt auf eine neuere Version.

## <a name="syntax"></a>Syntax

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

In nuget 2.8 und `Update-Package` höher können Sie ein vorhandenes Paket in Ihrem Projekt herabstufen. Wenn Sie z. b. Microsoft. Aspnet. MVC 5.1.0-RC1 installiert haben, würde der folgende Befehl das Downgrade auf 5.0.0 durchführt:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parameter

|  Parameter | Beschreibung |
| --- | --- |
| Id | Der Bezeichner des zu aktualisierenden Pakets. Wenn dieser nicht ausgelassen wird, werden alle Pakete aktualisiert. Der Schalter-ID selbst ist optional. |
| IgnoreDependencies | Überspringt die Aktualisierung der Paketabhängigkeiten. |
| ProjektName | Der Name des Projekts, das die zu aktualisierenden Pakete enthält, die standardmäßig auf alle Projekte aktualisiert werden. |
| Version | Die für das Upgrade zu verwendende Version, die standardmäßig die neueste Version verwendet. In nuget 3.0 und höher muss der Versions Wert einer der *niedrigsten, höchsten, highestminor*oder *highestpatch* (äquivalent zu-Safe) sein. |
| Sauberem | Schränkt Upgrades auf Versionen ein, die die gleiche Haupt-und neben Version wie das aktuell installierte Paket haben. |
| Source | Die URL oder der Ordner Pfad für die Paketquelle, die durchsucht werden soll. Lokale Ordner Pfade können absolut oder relativ zum aktuellen Ordner sein. Wenn kein Wert `Update-Package` angezeigt wird, wird die aktuell ausgewählte Paketquelle durchsucht. |
| Incluabprerelease | Schließt vorab Pakete für Updates ein. |
| Neuinstallation | Gibt Pakete zurück, die Ihre aktuell installierten Versionen verwenden. Informationen dazu finden Sie unter [Neuinstallieren und Aktualisieren von Paketen](../../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | Die Aktion, die ausgeführt werden soll, wenn die vom Projekt referenzierten Dateien überschrieben oder ignoriert werden sollen. Mögliche Werte sind " *überschreiben", "ignorieren", "keine", "überschreiben*" und " *IgnoreAll* " (3.0 +). |
| Dependencyversion | Die Version der zu verwendenden Abhängigkeits Pakete. Dies kann eine der folgenden sein:<br/><ul><li>*Niedrigste* (Standard): die niedrigste Version</li><li>*Highestpatch*: die Version mit dem niedrigsten, niedrigsten, niedrigsten, größten Patch</li><li>*Highestminor*: die Version mit dem niedrigsten Haupt-, höchst-und Höchstwert</li><li>*Höchste* (Standardeinstellung für Update-Package ohne Parameter): die höchste Version</li></ul>Sie können den Standardwert mithilfe der [`dependencyVersion`](../nuget-config-file.md#config-section) -Einstellung in der `Nuget.Config` Datei festlegen. |
| ToHighestPatch | Äquivalent zu-Safe. |
| ToHighestMinor | Schränkt Upgrades auf Versionen ein, die dieselbe Hauptversion wie das aktuell installierte Paket haben. |
| WhatIf | Zeigt, was geschieht, wenn der Befehl ausgeführt wird, ohne die Aktualisierung tatsächlich auszuführen. |

Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.

### <a name="common-parameters"></a>Allgemeine Parameter

`Update-Package`unterstützt die folgenden [allgemeinen PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.

### <a name="examples"></a>Beispiele

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
