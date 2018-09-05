---
title: Anmerkungen zu NuGet 2.8.5
description: Anmerkungen zu dieser Version für die Einbindung von NuGet 2.8.5 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548624"
---
# <a name="nuget-285-release-notes"></a>Anmerkungen zu NuGet 2.8.5

[Anmerkungen zu NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [Anmerkungen zu NuGet 2.8.6](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 wurde am 30. März 2015 veröffentlicht. Es ist eine Aktualisierung für unsere 2.8.3 vorgesehen VSIX mit einigen Korrekturen.

In dieser Version wurde die Unterstützung für NuGet-Paket-Manager-Dialogfeld für hinzugefügt [DNX-Zielframeworkmoniker](https://github.com/aspnet/dnx).  Diese neue frameworkMoniker, die unterstützt werden gehören:

* **core50** – eine "base" target frameworkMoniker (TFM), die mit der Core CLR kompatibel ist.
* **dnx452** – ein TFM für DNX-basierter apps, die mit der vollständigen 4.5.2 Framework-Version
* **dnx46** – ein TFM bestimmte DNX-basierte apps, die mit der vollständigen 4.6-Version des Frameworks
* **dnxcore50** – ein TFM bestimmte DNX-basierte apps, die mit der Core 5.0-Version des Frameworks

Ein Fehler wurde, verhindert hat, dass die von Paketen in Projekten der FSharp ordnungsgemäße Installation von behoben:

https://nuget.codeplex.com/workitem/4400