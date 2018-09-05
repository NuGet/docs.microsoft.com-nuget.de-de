---
title: NuGet-Open-PackagePage PowerShell-Referenz
description: Verweis für Open-PackagePage-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0325aa4ddd718a901dd6a09cdf86cae260e326ab
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547167"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Paket-Manager-Konsole in Visual Studio)

*In 3.0 und höher veraltet. verfügbar nur in der [NuGet-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows.*

Startet den Standardbrowser mit dem Projekt, Lizenz oder Missbrauch Berichts-URL für das angegebene Paket.

## <a name="syntax"></a>Syntax

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --- | --- |
| Id | Die Paket-ID des gewünschten Pakets. Die - Id Switch selbst ist optional. |
| Version | Die Version des Pakets, standardmäßig auf die neueste Version. |
| Quelle | Der Paketquelle in die ausgewählte Datenquelle in der Quelle Dropdown-Standardwert. |
| Lizenz | Öffnet den Browser mit des Pakets Lizenz-URL. Wenn - Lizenz weder -ReportAbuse angegeben wird, öffnet der Browser der Pakets Projekt-URL an. |
| ReportAbuse | Öffnet den Browser mit des Pakets URL für Bericht von Missbrauch. Wenn - Lizenz weder -ReportAbuse angegeben wird, öffnet der Browser der Pakets Projekt-URL an. |
| PassThru | Zeigt die URL an. Verwenden Sie unterdrückt werden, öffnen den Browser mit - WhatIf. |

Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Open-PackagePage` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction und WarningVariable.

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