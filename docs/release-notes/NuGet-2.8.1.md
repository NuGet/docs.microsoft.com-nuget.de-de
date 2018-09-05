---
title: Anmerkungen zu NuGet 2.8.1
description: Anmerkungen zu dieser Version für die Einbindung von NuGet 2.8.1 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545238"
---
# <a name="nuget-281-release-notes"></a>Anmerkungen zu NuGet 2.8.1

[Anmerkungen zu NuGet 2.8](../release-notes/nuget-2.8.md) | [Anmerkungen zu NuGet 2.8.2](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 wurde am 2. April 2014 veröffentlicht.

## <a name="notable-features-in-the-release"></a>Wichtige Features in der Version

### <a name="support-for-windows-phone-81-projects"></a>Unterstützung für Windows Phone 8.1-Projekte
Diese Version unterstützt jetzt die folgenden neuen Target frameworkMoniker das Ziel Windows Phone 8.1-Projekten verwendet werden kann:

* WindowsPhone81 / WP81 (für Windows Phone Silverlight-basierte Projekte)
* WindowsPhoneApp81 / WPA81 (für WinRT-basierten Windows Phone-App-Projekte)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Update der NuGet WebMatrix-Erweiterung
Diese Version aktualisiert die NuGet-Client finden Sie in WebMatrix zum [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 und mit es bietet Ihnen z. B. mithilfe von XDT-Transformationen. Noch wichtiger ist, dass die 2.6.1 Core Update ermöglicht, dem WebMatrix-Client, die NuGet-Pakete zu installieren, die neuere Versionen enthalten die `.nuspec` -Schema, das die ASP.NET NuGet-Pakete enthält.

Weitere Informationen zu dem Update der WebMatrix-Erweiterung finden Sie die speziellen [Anmerkungen zu dieser Version](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Fehlerkorrekturen
Neben diesen Features enthält diese Version von NuGet andere Fehlerkorrekturen. Gab es 16 insgesamt in den Release behobenen Problemen. Eine vollständige Liste der Arbeit Elemente eine feste NuGet 2.8.1, bitte Ansicht der [NuGet Issue Tracker für diese Version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Werden mit Visual Studio "14" CTP-Version
In Visual Studio "14" CTP-Version am 3. Juni-2014 veröffentlicht wird NuGet 2.8.1 gelieferten. Die Funktionen, die sie unterstützen bleiben in Par mit anderen 2.8.1 VSIXes wie für Visual Studio 2013.
