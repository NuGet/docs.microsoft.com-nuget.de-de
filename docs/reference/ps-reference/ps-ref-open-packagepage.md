---
title: PowerShell-Referenz für nuget-Open-packagepage
description: Referenz für den PowerShell-Befehl "Open-packagepage" in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 39199ebfc37756ed40158a1c07afca7709067350
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384427"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Paket-Manager-Konsole in Visual Studio)

*Veraltet in 3.0 und höher nur in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows verfügbar.*

Hiermit wird der Standardbrowser mit der URL für das Projekt, die Lizenz oder den Berichts Missbrauch für das angegebene Paket gestartet.

## <a name="syntax"></a>Syntax

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parameters

| Parameter | Beschreibung |
| --- | --- |
| ID | Die Paket-ID des gewünschten Pakets. Der Schalter-ID selbst ist optional. |
| Version | Die Version des Pakets, standardmäßig auf die neueste Version. |
| Quelle | Die Paketquelle, standardmäßig auf die ausgewählte Quelle in der Dropdown-Dropdown-Dropdown-Datei. |
| Lizenz | Öffnet den Browser mit der Lizenz-URL des Pakets. Wenn weder-License noch-Report Abuse angegeben ist, öffnet der Browser die Projekt-URL des Pakets. |
| Report Abuse | Öffnet den Browser mit der Berichts Missbrauch-URL des Pakets. Wenn weder-License noch-Report Abuse angegeben ist, öffnet der Browser die Projekt-URL des Pakets. |
| PassThru | Zeigt die URL an. Verwenden Sie with-WhatIf, um das Öffnen des Browsers zu unterdrücken. |

Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Open-PackagePage` unterstützt die folgenden [allgemeinen PowerShell-Parameter](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.

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