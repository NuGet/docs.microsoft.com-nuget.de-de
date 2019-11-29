---
title: Als veraltet gekennzeichnete Pakete auf nuget.org
description: Ausführliche Beschreibung der als veraltet gekennzeichneten Pakete und der Art und Weise, wie diese Informationen von den Clients angezeigt werden
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096881"
---
# <a name="deprecating-packages"></a>Als veraltet gekennzeichnete Pakete

Sie können ein Paket als veraltet kennzeichnen, wenn Sie es nicht mehr verwalten oder wenn Sie möchten, dass die Nutzer Ihres Pakets zu einem anderen Paket wechseln. 

Pakete als veraltet zu kennzeichnen, ist nicht das gleiche wie das **Aufheben der Auflistung** eines Pakets:
* Durch das **Aufheben der Auflistung** eines Pakets wird dessen Ermittlung verhindert, weil es in den Suchergebnissen ausgeblendet ist. 
* Wenn Sie ein Paket **als veraltet kennzeichnen**, können die vorhandenen Nutzer des Pakets ermitteln, ob sie das Paket in ihren Projekten installiert haben oder es verwenden. Außerdem teilt es ihnen mit, wieso das Paket als veraltet gekennzeichnet wurde, und schlägt ein alternatives, von Ihnen (dem Paketherausgeber) empfohlenes Paket vor. Wenn Sie ein Paket als veraltet kennzeichnen, wird die Auflistung des Pakets nicht aufgehoben. 

Als Herausgeber können Sie entscheiden, ob Sie die Auflistung der Pakete sowohl aufheben als auch als veraltet kennzeichnen möchten.

## <a name="deprecation-workflow"></a>Workflow zum Kennzeichnen eines Pakets als veraltet
1. Wechseln Sie zu **Pakete verwalten**, und wählen Sie **Deprecation** (als veraltet kennzeichnen) aus, um ein Paket als veraltet zu kennzeichnen:

    ![Option „Paket als veraltet kennzeichnen“](media/deprecation-select-option.png)

2. Wählen Sie die Version aus, die Sie als veraltet kennzeichnen möchten. Wenn Sie alle Versionen als veraltet kennzeichnen möchten, wählen Sie Option **Alle Versionen auswählen** aus.

    ![Auswahl der Paketversionen, die als veraltet gekennzeichnet werden sollen](media/deprecation-select-version.png)

3. Wählen Sie einen Grund aus, weshalb die Versionen als veraltet gekennzeichnet werden sollen. Wenn das Paket nicht mehr verwaltet wird, wählen Sie die **Legacy**-Option aus. Wenn die spezifische Version einen kritischen Fehler aufweist, wählen Sie die Option **has critical bugs** (weist kritische Fehler auf) aus. Wählen Sie **Andere** für alle anderen Gründe aus. Sie können jederzeit ein alternatives empfohlenes Paket (und eine alternativ empfohlene Version) und eine benutzerdefinierte Meldung an die Besitzer festlegen. 

    ![Auswahl der Gründe für eine alternative Paketempfehlung oder für eine benutzerdefinierte Meldung](media/deprecation-save.png)

> [!Note]
> Benutzerdefinierte Meldungen werden nur auf nuget.org, aber nicht von den Clients angezeigt. Derzeit wird die benutzerdefinierte Meldung von Clients wie `dotnet.exe` und dem NuGet Paket-Manager nicht angezeigt.

## <a name="client-experience-for-deprecated-packages"></a>Clienterfahrung für veraltete Pakete
Sobald ein Paket als veraltet gekennzeichnet worden ist, werden seine Nutzer wie folgt benachrichtigt (je nach verwendetem Client).

### <a name="visual-studio"></a>Visual Studio 
*Verfügbar ab Visual Studio 2019, Version 16.3*

Visual Studio warnt auf der Registerkarte `Installed` vor der Nutzung eines veralteten Pakets. Es werden eine Warnung für das Paket und Informationen über dessen Veraltung angezeigt. Dabei erfahren Sie auch, wieso es als veraltet gekennzeichnet wurde und welches Paket sie alternativ verwenden können, falls eines vorhanden ist.

   ![Veraltete Pakete auf der Registerkarte „installiert“ des Paket-Managers in Visual Studio](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*Verfügbar ab .NET SDK 3.0*

Wenn Sie „dotnet.exe“ verwenden, können Sie den `dotnet list package --deprecated`-Befehl für den Projektmappen- oder Projektordner ausführen, um eine Liste der veralteten Pakete zusammen mit den Informationen über deren Veraltung zu erhalten:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
