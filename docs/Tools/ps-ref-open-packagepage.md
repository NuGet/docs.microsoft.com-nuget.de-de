---
title: "NuGet-öffnen-PackagePage-PowerShell-Referenz | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für Open PackagePage-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio."
keywords: NuGet-Paket-Manager-Konsole, die NuGet Powershell-Befehle, die NuGet Powershell-Referenz, Open PackagePage
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 389bad37940f05dd864adfc06080bf746464365d
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Paket-Manager-Konsole in Visual Studio)

*In 3.0 veraltet. verfügbar nur innerhalb der [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio unter Windows.*

Startet den Standardbrowser mit dem Projekt, Lizenzen oder Missbrauch Berichts-URL für das angegebene Paket.

## <a name="syntax"></a>Syntax

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --- | --- |
| Id | Die Paket-ID mit dem gewünschten Paket. Die - Id Schalter ist optional. |
| Version | Die Version des Pakets, auf die neueste Version auszuführen. |
| Quelle | Die ausgewählte Quelle in der Quelle Dropdownelement direktionales Paketquelle. |
| Lizenz | Öffnet den Browser, um des Pakets Lizenz-URL an. Wenn - Lizenz weder -ReportAbuse angegeben wird, öffnet der Browser die Paket-Projekt-URL an. |
| ReportAbuse | Öffnet den Browser, um des Pakets Berichts Missbrauch-URL an. Wenn - Lizenz weder -ReportAbuse angegeben wird, öffnet der Browser die Paket-Projekt-URL an. |
| PassThru | Zeigt die URL an. Verwenden Sie mit "-WhatIf" unterdrückt werden, öffnen den Browser. |

Keines dieser Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Open-PackagePage`unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Fehleraktion, ErrorVariable, -OutBuffer, OutVariable, mit "pipelinevariable", ausführlich, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```