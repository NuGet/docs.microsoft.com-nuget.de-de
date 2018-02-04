---
title: Anmerkungen zur Version des NuGet-2.8.5 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 2.8.5 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-2.8.5 versionsanmerkungen aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ace56284e56f24394d49c0598ec3604b62caaf67
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
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