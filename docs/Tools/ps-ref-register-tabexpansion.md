---
title: Register "tabexpansion" NuGet-PowerShell-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für die Register-\"tabexpansion\" PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio."
keywords: NuGet-Paket-Manager-Konsole NuGet Powershell-Befehle, NuGet Powershell-Referenz zu "Register-tabexpansion"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5691c07f9efef4bfd12680421f3b02c5a523eb6f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-"tabexpansion" (Paket-Manager-Konsole in Visual Studio)

*Verfügbar nur innerhalb der [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio unter Windows.*

Registriert eine Tab-Taste für die Parameter des angegebenen Befehls an, so, dass bei der Registerkarte "verwendet wird, wenn Sie einen Befehl eingeben, die erweiterten Werte als verfügbare Optionen für den fraglichen Parameter angezeigt werden. Es werden alle vorherigen Erweiterungen für den Befehl überschrieben.

## <a name="syntax"></a>Syntax

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --- | --- |
| name | (Erforderlich) Der Befehl, um Erweiterungen zu registrieren. Der - Name Switch selbst ist optional. |
| Definition | (Erforderlich) Ein Objekt, das Argument in der Syntax beschreibt `@{'<parameter>' = {'<value1>', '<value2>', ...}}` , in denen `<parameter>` ist der Name des Parameters ändern, und jede `<value>` bietet eine bestimmte Erweiterung. Einfachen und doppelte Anführungszeichen werden akzeptiert. |

Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Register-TabExpansion`unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

Erwägen Sie eine Lösung, die drei Projekte Namen EventManager, Dienstprogramme und SpecialParser enthält. Der Entwickler häufig mithilfe der `Update-Package` Befehl zu unterschiedlichen Zeiten mit jedem dieser Projekte. Sie sucht es praktisch, wenn die `Update-Package` Befehl angeben, automatische Vervollständigung von Erweiterungen für die `-ProjectName` Argument, damit Sie einen Projektnamen jeder Anmeldung eingeben nicht benötigt. 

Registriert den folgende Befehl ein, dann diese drei Projektnamen als eine Erweiterung für die `-ProjectName` Parameter:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Der Entwickler kann dann geben `Update-Package -ProjectName `, drücken Sie Tab, und finden Sie unter der Erweiterungen als automatische Vervollständigung Optionen angeboten:

![Beispiel zur Verwendung von "Register-tabexpansion"](media/Register-TabExpansion-Example.png)
