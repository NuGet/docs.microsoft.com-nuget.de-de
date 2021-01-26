---
title: Nuget-Register-TabExpansion PowerShell-Referenz
description: Referenz für Register-TabExpansion PowerShell-Befehl in der nuget-Paket-Manager-Konsole in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 6ad0da0e84fc2e31499c06bde013d2a256987d9a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777463"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (Paket-Manager-Konsole in Visual Studio)

*Nur in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows verfügbar.*

Registriert eine Registerkarten Erweiterung für die Parameter des angegebenen Befehls, sodass die erweiterten Werte als verfügbare Optionen für den fraglichen Parameter angezeigt werden, wenn Tab bei der Eingabe eines Befehls verwendet wird. Alle vorherigen Erweiterungen für den Befehl werden überschrieben.

## <a name="syntax"></a>Syntax

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --- | --- |
| Name | Benötigten Der Befehl, für den Erweiterungen registriert werden sollen. Der Schalter "-Name" ist optional. |
| Definition | Benötigten Ein Objekt, das das Argument in der Syntax beschreibt `@{'<parameter>' = {'<value1>', '<value2>', ...}}` `<parameter>` , wobei der Name des zu ändernden Parameters und jeder `<value>` eine bestimmte Erweiterung bereitstellt. Sowohl einfache als auch doppelte Anführungszeichen werden akzeptiert. |

Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Register-TabExpansion` unterstützt die folgenden [allgemeinen PowerShell-Parameter](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

Stellen Sie sich eine Lösung vor, die drei Projekte mit den Namen EventManager, Utilities und specialparser enthält. Der Entwickler verwendet den `Update-Package` Befehl häufig für jedes dieser Projekte zu unterschiedlichen Zeitpunkten. Sie finden es praktisch, dass der `Update-Package` Befehl die Erweiterungen für die automatische Vervollständigung für das Argument bereitstellt, `-ProjectName` sodass Sie nicht jedes Mal einen Projektnamen eingeben müssen. 

Der folgende Befehl registriert dann die drei Projektnamen als Erweiterung für den `-ProjectName` Parameter:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Der Entwickler kann dann eingeben `Update-Package -ProjectName ` , Tab drücken und die Erweiterungen als automatische Vervollständigungs Optionen anzeigen:

![Beispiel für die Verwendung von Register-TabExpansion](media/Register-TabExpansion-Example.png)