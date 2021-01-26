---
title: Anmerkungen zu dieser Version von nuget 2,9-RC
description: Anmerkungen zu dieser Version von nuget 2,9 RC, einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b9d32f09fae7e12f81cf92b5b6e6b36c71d55f26
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780321"
---
# <a name="nuget-29-rc-release-notes"></a>Anmerkungen zu dieser Version von nuget 2,9-RC

[Nuget 2.8.7 Anmerkungen](../release-notes/nuget-2.8.7.md)  |  zu dieser Version [Anmerkungen zu dieser Version von nuget 3,0 Preview](../release-notes/nuget-3.0-preview.md)

Nuget 2,9 wurde am 10. September 2015 als Update für 2.8.7 VSIX für Visual Studio 2012 und 2013 veröffentlicht.

### <a name="updates-in-this-release"></a>Updates in dieser Version

* Die Verarbeitung von Paketen wird übersprungen, wenn das enthaltene `.nuspec` Dokument falsch formatiert ist [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Korrigierte multipartwebrequest-Behandlung von \r\n für UNIX/Linux-Szenarien: [776](https://github.com/NuGet/Home/issues/776)
* Korrigierte Integration in Buildereignisse in Visual Studio 2013 Community Edition- [1180](https://github.com/NuGet/Home/issues/1180)


Die komplette Liste der Fixes in dieser Version finden Sie auf GitHub im 2.8.8- [Meilenstein](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed) .
