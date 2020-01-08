---
title: Nuget-Register-tabexpansion PowerShell-Referenz
description: Referenz für den PowerShell-Befehl "Register-tabexpansion" in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 37aed96760e642b03c02bf31fe47a54f0e3cb74a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384453"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-tabexpansion (Paket-Manager-Konsole in Visual Studio)

*Nur in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows verfügbar.*

Registriert eine Registerkarten Erweiterung für die Parameter des angegebenen Befehls, sodass die erweiterten Werte als verfügbare Optionen für den fraglichen Parameter angezeigt werden, wenn Tab bei der Eingabe eines Befehls verwendet wird. Alle vorherigen Erweiterungen für den Befehl werden überschrieben.

## <a name="syntax"></a>Syntax

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parameters

| Parameter | Beschreibung |
| --- | --- |
| -Name | Benötigten Der Befehl, für den Erweiterungen registriert werden sollen. Der Schalter "-Name" ist optional. |
| Definition | Benötigten Ein Objekt, das das Argument in der Syntax beschreibt `@{'<parameter>' = {'<value1>', '<value2>', ...}}` wobei `<parameter>` der Name des Parameters ist, der geändert werden soll, und jeder `<value>` eine bestimmte Erweiterung bereitstellt. Sowohl einfache als auch doppelte Anführungszeichen werden akzeptiert. |

Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Register-TabExpansion` unterstützt die folgenden [allgemeinen PowerShell-Parameter](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

Stellen Sie sich eine Lösung vor, die drei Projekte mit den Namen EventManager, Utilities und specialparser enthält. Der Entwickler verwendet häufig den `Update-Package` Befehl zu unterschiedlichen Zeitpunkten für jedes dieser Projekte. Sie finden es praktisch, dass der `Update-Package` Befehl Erweiterungen für die automatische Vervollständigung für das `-ProjectName` Argument bereitstellen muss, damit Sie nicht jedes Mal einen Projektnamen eingeben müssen. 

Der folgende Befehl registriert dann die drei Projektnamen als Erweiterung für den `-ProjectName`-Parameter:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Der Entwickler kann dann `Update-Package -ProjectName `eingeben, die Tab-Taste drücken und die Erweiterungen als automatische Vervollständigungs Optionen anzeigen:

![Beispiel für die Verwendung von "Register-tabexpansion"](media/Register-TabExpansion-Example.png)
