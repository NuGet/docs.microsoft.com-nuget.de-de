---
title: Anmerkungen zur Version des NuGet-2.8.1 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 2.8.1 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-2.8.1 versionsanmerkungen aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 99dd050eb06024972132d5b0dcc9f97f965adc12
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-281-release-notes"></a>Anmerkungen zur Version von NuGet 2.8.1

[Anmerkungen zur Version von NuGet 2.8](../release-notes/nuget-2.8.md) | [NuGet 2.8.2-Versionshinweise](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 wurde am 2. April 2014 veröffentlicht.

## <a name="notable-features-in-the-release"></a>Wichtige Funktionen in der Version

### <a name="support-for-windows-phone-81-projects"></a>Unterstützung für Windows Phone 8.1-Projekte
Diese Version unterstützt jetzt die folgenden neuen Ziel frameworkMoniker das Ziel Windows Phone 8.1-Projekte verwendet werden kann:

* WindowsPhone81 / WP81 (für Windows Phone Silverlight-basierte Projekte)
* WindowsPhoneApp81 / WPA81 (für Windows Phone-App WinRT-basierte Projekte)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Update der WebMatrix-Erweiterung von NuGet
Diese Version aktualisiert, die NuGet-Client finden in WebMatrix zum [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 und schaltet sie Funktionen wie z. B. XDT Transformationen mit. Vor allem die 2.6.1 Core Update ermöglicht dem WebMatrix-Client, die NuGet-Pakete installieren, die neuere Versionen enthalten die `.nuspec` Schema, d. h. die ASP.NET NuGet-Pakete enthält.

Weitere Informationen zu dem Update WebMatrix-Erweiterung finden Sie unter die speziellen [Anmerkungen zu dieser Version](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Fehlerkorrekturen
Zusätzlich zu diesen Features enthält diese Version von NuGet Weitere Fehlerkorrekturen. Es gab 16 insgesamt Probleme, die in der Version behoben. Eine vollständige Liste der Arbeit Artikel feste in NuGet 2.8.1, bitte Ansicht der [NuGet Issue Tracker für diese Version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Mit Visual Studio reshipping "14" CTP
In Visual Studio "14" CTP 3. 2014 Juni veröffentlicht ist NuGet 2.8.1 dem Produkt ausgeliefert. Funktionen, die sie unterstützen, bleiben in Par mit anderen 2.8.1 VSIXes wie für Visual Studio 2013.
