---
title: Hinzufügen von NuGet-BindingRedirect-PowerShell-Referenz
description: Referenz für die Add-BindingRedirect-PowerShell-Befehl in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: dec7db04c5cf239863b9c00e9f5bc0dde42c7e47
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551656"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (Paket-Manager-Konsole in Visual Studio)

*Verfügbar nur in der [NuGet-Paket-Manager-Konsole](package-manager-console.md) in Visual Studio unter Windows.*

Untersucht alle Assemblys im Ausgabepfad für ein Projekt, und der Konfigurationsdatei Anwendungs- oder Webkonfigurationsdatei bindungsweiterleitungen hinzugefügt, bei Bedarf. Mit diesem Befehl wird automatisch ausgeführt, wenn Sie ein Paket zu installieren.

Ausführliche Informationen zum Binden von umleitungen und warum sie verwendet werden, finden Sie unter [Umleiten von Assemblyversionen](/dotnet/framework/configure-apps/redirect-assembly-versions) in der .NET-Dokumentation.

## <a name="syntax"></a>Syntax

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --- | --- |
| ProjektName | (Erforderlich) Das Projekt, dem bindungsweiterleitungen hinzugefügt werden soll. Der Schalter - Projektname ist optional. |

Keine Parameter akzeptieren Pipeline Eingabe- oder Platzhalter-Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Add-BindingRedirect` unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216): Debuggen, Fehleraktion, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```