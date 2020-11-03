---
title: Nuget-Add-BindingRedirect PowerShell-Referenz
description: Referenz für Add-BindingRedirect PowerShell-Befehl in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 382ba9b179428c70e3eb16db86a363e095207d61
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237256"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (Paket-Manager-Konsole in Visual Studio)

*Nur in der [Paket-Manager-Konsole](../../consume-packages/install-use-packages-powershell.md) in Visual Studio unter Windows verfügbar.*

Untersucht alle Assemblys im Ausgabepfad für ein Projekt und fügt bei Bedarf Bindungs Umleitungen zur Anwendung oder Webkonfigurationsdatei hinzu. Dieser Befehl wird automatisch ausgeführt, wenn ein Paket installiert wird.

> [!NOTE]
> Dies gilt nur für Szenarien, in denen eine packages.config Datei verwendet wird. Weitere Informationen finden Sie unter [nuget-packages.config Dateireferenz](~/reference/packages-config.md).

Ausführliche Informationen zu Bindungs Umleitungen und deren Verwendung finden Sie unter [umleiten](/dotnet/framework/configure-apps/redirect-assembly-versions) von Assemblyversionen in der .NET-Dokumentation.

## <a name="syntax"></a>Syntax

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --- | --- |
| ProjectName | Benötigten Das Projekt, dem Bindungs Umleitungen hinzugefügt werden sollen. Der Schalter "-ProjectName" ist optional. |

Keiner dieser Parameter akzeptiert Pipeline Eingabe-oder Platzhalter Zeichen.

## <a name="common-parameters"></a>Allgemeine Parameter

`Add-BindingRedirect` unterstützt die folgenden [allgemeinen PowerShell-Parameter](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```