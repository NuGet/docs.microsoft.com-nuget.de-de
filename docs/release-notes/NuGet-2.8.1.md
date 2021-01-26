---
title: Anmerkungen zu dieser Version von nuget 2.8.1
description: Anmerkungen zu dieser Version von nuget 2.8.1 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776763"
---
# <a name="nuget-281-release-notes"></a>Anmerkungen zu dieser Version von nuget 2.8.1

Anmerkungen zu dieser [Version von nuget 2,8](../release-notes/nuget-2.8.md)  |  [Nuget 2.8.2 Anmerkungen](../release-notes/nuget-2.8.2.md) zu dieser Version

Nuget 2.8.1 wurde am 2. April 2014 veröffentlicht.

## <a name="notable-features-in-the-release"></a>Wichtige Features in der Version

### <a name="support-for-windows-phone-81-projects"></a>Unterstützung für Windows Phone 8,1-Projekte
In dieser Version werden nun die folgenden neuen zielframeworkmoniker unterstützt, die zum Ziel Windows Phone 8,1-Projekten verwendet werden können:

* WindowsPhone81/WP81 (für Silverlight-basierte Windows Phone-Projekte)
* WindowsPhoneApp81/WPA81 (für WinRT-basierte Windows Phone-App-Projekte)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Aktualisieren der nuget-webmatrix-Erweiterung
Diese Version aktualisiert den nuget-Client in webmatrix an [nuget. Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 und bietet IT-Funktionen wie xdt-Transformationen. Noch wichtiger ist, dass das 2.6.1 Core-Update dem webmatrix-Client ermöglicht, nuget-Pakete zu installieren, die neuere Versionen des `.nuspec` Schemas enthalten, einschließlich der ASP.net nuget-Pakete.

Weitere Informationen zum Update der webmatrix-Erweiterung finden Sie in den [Anmerkungen](../release-notes/nuget-2.6.1-for-WebMatrix.md)zu dieser Version.

### <a name="bug-fixes"></a>Fehlerkorrekturen
Zusätzlich zu diesen Features enthält diese Version von nuget andere Fehlerbehebungen. In der Version wurden 16 Gesamtprobleme behandelt. Eine vollständige Liste der Arbeitselemente, die in nuget 2.8.1 behoben sind, finden Sie in der [nuget-Problemverfolgung für diese Version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Erneute Bereitstellung mit Visual Studio "14" CTP
In Visual Studio "14" CTP, das am 3. Juni 2014 veröffentlicht wurde, wird nuget 2.8.1 in der Box ausgeliefert. Die von ihm unterstützten Funktionen bleiben mit anderen 2.8.1-vsixes, z. b. dem für Visual Studio 2013, unverändert.
