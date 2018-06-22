---
title: Anmerkungen zur Version von NuGet 2.8.5
description: Versionshinweise für NuGet 2.8.5 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820078"
---
# <a name="nuget-285-release-notes"></a>Anmerkungen zur Version von NuGet 2.8.5

[Anmerkungen zur Version des NuGet-2.8.3](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6-Versionshinweise](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 wurde 30 März 2015 veröffentlicht. Es ist ein kleineres Update an unsere 2.8.3 VSIX mit einigen Korrekturen vorgesehen.

In dieser Version wurde die Unterstützung für Dialogfeld "NuGet-Paket-Manager" hinzugefügt, für die [DNX-Ziel-Framework-Moniker](https://github.com/aspnet/dnx).  Schließen diese neue frameworkMoniker, die unterstützt werden:

* **core50** - ein 'base' Zielframeworkmoniker (TFM), die mit der zentrale CLR kompatibel ist.
* **dnx452** – ein TFM spezifisch für die DNX-basierte apps, die mit der vollständigen 4.5.2 Framework-Version
* **dnx46** – ein TFM bestimmte DNX-basierte apps, die mit der vollständigen 4.6 Version des Frameworks
* **dnxcore50** – ein TFM bestimmte DNX-basierte apps, die mit der Core 5.0-Version des Frameworks

Ein Fehler behoben wurde, verhindert die von Paketen in FSharp Projekte ordnungsgemäß installiert:

https://nuget.codeplex.com/workitem/4400