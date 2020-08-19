---
title: PowerShell-Referenz zu nuget-bindingRedirect
description: Referenz für den PowerShell-Befehl "Add-bindingRedirect" in der nuget-Paket-Manager-Konsole in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f5ba4bd8140fa8cac7da8bf1351ad5448671b768
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623122"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-bindingRedirect (Paket-Manager-Konsole in Visual Studio)

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

`Add-BindingRedirect` unterstützt die folgenden [allgemeinen PowerShell-Parameter](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, pipelinevariable, Verbose, WarningAction und WarningVariable.

## <a name="examples"></a>Beispiele

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```
