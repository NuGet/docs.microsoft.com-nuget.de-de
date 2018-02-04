---
title: NuGet-2.9 RC-Versionsanmerkungen | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 2.9 RC einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-2.9 RC-versionsanmerkungen, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0e73b54ab7bbf97806269834c67ad0a159c9065b
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-29-rc-release-notes"></a>NuGet-2.9 RC-Versionsanmerkungen

[Anmerkungen zur Version des NuGet-2.8.7](../release-notes/nuget-2.8.7.md) | [Anmerkungen zur Version von NuGet-3.0-Vorschau](../release-notes/nuget-3.0-preview.md)

NuGet-2.9 10 September 2015 freigegeben wurde, als Update für die 2.8.7 VSIX für Visual Studio 2012 und 2013.

### <a name="updates-in-this-release"></a>Updates in dieser Version

* Jetzt Verarbeitung Pakete wird übersprungen, wenn ihre enthaltenen `.nuspec` Dokument ist falsch formatiert - [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Korrigiert Multipartwebrequest Behandlung von \r\n für Unix/Linux-Szenarien – [776](https://github.com/NuGet/Home/issues/776)
* Integration in Visual Studio 2013 Community Edition - Buildereignisse korrigiert [1180](https://github.com/NuGet/Home/issues/1180)


Die vollständige Liste der Fixes in dieser Version finden Sie auf GitHub in der [2.8.8 Meilenstein](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
