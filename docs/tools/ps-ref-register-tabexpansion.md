---
title: Register "tabexpansion" NuGet-PowerShell-Referenz
description: Referenz für "Register-tabexpansion" PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8adb80af85e2e32fa8c35e5272cf90ff0c0ddcbb
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842484"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-"tabexpansion" (Paket-Manager-Konsole in Visual Studio)

*Verfügbar nur in der [-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows.*

Registriert eine Erweiterung der Registerkarte für die Parameter des angegebenen Befehls, so, dass wenn Registerkarte verwendet wird, wenn Sie einen Befehl eingeben, die erweiterten Werte als verfügbare Optionen für den betreffenden Parameter angezeigt werden. Es werden alle vorherigen Erweiterungen für den Befehl überschrieben.

## <a name="syntax"></a>Syntax

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --- | --- |
| Name | (Erforderlich) Der Befehl, um Erweiterungen zu registrieren. Der - Name Switch selbst ist optional. |
| Definition | (Erforderlich) Ein Objekt, das das Argument in der Syntax beschreibt `@{'<parameter>' = {'<value1>', '<value2>', ...}}` , in denen `<parameter>` ist der Name des Parameters ändern, und jede `<value>` bietet eine spezielle Erweiterung. Einfacher und doppelte Anführungszeichen werden akzeptiert. |

Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Register-TabExpansion` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

Erwägen Sie eine Lösung, die drei Projekte Namen EventManager, Dienstprogramme und SpecialParser enthält. Der Entwickler häufig verwendet die `Update-Package` Befehl zu unterschiedlichen Zeiten mit jedes dieser Projekte. Sie sucht es praktisch, wenn die `Update-Package` Befehl geben, automatische Vervollständigung von Erweiterungen für die `-ProjectName` Argument, damit sie nicht, einen Projektnamen ein, die jedes Mal erneut eingeben muss. 

Registriert den folgende Befehl aus, dann diese drei Projektnamen als Erweiterung für die `-ProjectName` Parameter:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Entwickler kann dann eingeben `Update-Package -ProjectName `, drücken Sie Tab, und finden Sie unter den Erweiterungen, die als Optionen zur automatischen Vervollständigung angeboten:

![Beispiel zur Verwendung von "Register-tabexpansion"](media/Register-TabExpansion-Example.png)
