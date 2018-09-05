---
title: Anmerkungen zu NuGet 3.4.3
description: Anmerkungen zu dieser Version für die Einbindung von NuGet 3.4.3 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549164"
---
# <a name="nuget-343-release-notes"></a>Anmerkungen zu NuGet 3.4.3

[Anmerkungen zu NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [Anmerkungen zu NuGet 3.4.4](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 wurde veröffentlicht, auf dem 22. April 2016, mehrere Probleme zu beheben, die in den Versionen 3.4 und nachfolgende identifiziert wurden.

Sie können sowohl VSIX-als auch nuget.exe [hier](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Updates und Verbesserungen

* Verbesserte Zuverlässigkeit von Visual Studio. Wir haben einige Probleme in NuGet behoben, die Visual Studio Abstürze verursacht haben.

## <a name="fixes"></a>Fehlerbehebungen

* Einige Autorisierungsprobleme behoben mit Kennwortgeschützte private Nuget Feeds.
* Korrigiert: rund um die nicht auf die PCL von wiederherstellen `project.json` mit Laufzeiten angegeben.
* Beim Installieren von Paketen, wurden einige Kunden in kann auch zeitweilige Ausfälle ausgeführt. Dies wurde jetzt in dieser Version behoben.
* Ein Problem wurde behoben, die aufgrund von Fehlern bei der datenbankwiederherstellung in C++ / CLI-Projekte mit `project.json`.
* Einige Pakete (z. B. ModernHttpClient), in denen nicht ordnungsgemäß entpackt bei Verwendung von Nuget in Mono. Dies wurde jetzt in dieser Version behoben.

Die vollständige Liste der Korrekturen und Verbesserungen in dieser Version, sehen Sie sich die Liste der Probleme [hier](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).