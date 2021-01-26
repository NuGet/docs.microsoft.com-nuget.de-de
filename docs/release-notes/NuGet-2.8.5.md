---
title: Nuget 2.8.5 Anmerkungen zu dieser Version
description: Anmerkungen zu dieser Version von nuget 2.8.5 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780353"
---
# <a name="nuget-285-release-notes"></a>Nuget 2.8.5 Anmerkungen zu dieser Version

[Nuget 2.8.3 Anmerkungen](../release-notes/nuget-2.8.3.md)  |  zu dieser Version [Nuget 2.8.6 Anmerkungen](../release-notes/nuget-2.8.6.md) zu dieser Version

Nuget 2.8.5 wurde am 30. März 2015 veröffentlicht. Es handelt sich um ein kleineres Update für unsere 2.8.3 VSIX mit einigen gezielten Korrekturen.

In dieser Version wurde das Dialogfeld Unterstützung für den nuget-Paket-Manager für [DNX-zielframeworkmoniker](https://github.com/aspnet/dnx)hinzugefügt.  Zu diesen neuen frameworkmonikern, die unterstützt werden, gehören:

* **core50** -ein Base-FrameworkMoniker (Target Framework Moniker, TFM), der mit der Core CLR kompatibel ist.
* **dnx452** -ein für DNX-basierte apps spezifischer TFM-Code, der die vollständige 4.5.2-Version des Frameworks verwendet.
* **dnx46** -ein für DNX-basierte apps spezifischer TFM-Code, der die Vollversion 4,6 des Frameworks verwendet.
* **dnxcore50** -ein für DNX-basierte apps spezifischer TFM-Code, der die Core 5,0-Version des Frameworks verwendet

Ein Fehler wurde behoben, der verhindert hat, dass Pakete ordnungsgemäß in FSharp-Projekte installiert wurden:

https://nuget.codeplex.com/workitem/4400