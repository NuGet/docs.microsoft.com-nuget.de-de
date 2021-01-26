---
title: Anmerkungen zu dieser Version von nuget 3,0 rc2
description: Anmerkungen zu dieser Version von nuget 3,0 rc2 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780284"
---
# <a name="nuget-30-rc2-release-notes"></a>Anmerkungen zu dieser Version von nuget 3,0 rc2

Anmerkungen zu dieser [Version von nuget 3,0 RC](../release-notes/nuget-3.0-RC.md)  |  [Anmerkungen zu dieser Version von nuget 3,0](../release-notes/nuget-3.0.0.md)

Nuget 3,0 rc2 wurde am 3. Juni als vorläufige Version veröffentlicht, die im Visual Studio 2015-Erweiterungs Katalog und [codeplex](https://nuget.codeplex.com/releases/view/615507)verfügbar 2015 ist. Diese Version enthält eine Reihe wichtiger Fehlerbehebungen und Leistungsverbesserungen, die wir für die Veröffentlichung vor der abgeschlossenen Version von Visual Studio 2015 wichtig waren. Diese nuget-Erweiterungs Version ist nur für Visual Studio 2015 verfügbar.

Insgesamt haben wir 158 Probleme in dieser Version geschlossen, und Sie können die [vollständige Liste der Probleme auf GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01)überprüfen.

## <a name="summary-of-top-issues-resolved"></a>Zusammenfassung der gelösten Probleme

* [Häufige Aufrufe von Netzwerk Updates beim Aktualisieren des Paket-Manager-Fensters](https://github.com/NuGet/Home/issues/515)
* [Verzögerter Bildlauf beim Wechsel zu installierter Sicht im Paket-Manager](https://github.com/NuGet/Home/issues/519)
* [Netzwerk Aufrufe sollten in einem Hintergrund Thread ausgeführt werden.](https://github.com/NuGet/Home/issues/516)
* [Kontrollkästchen "Vorschau Fenster nicht anzeigen" wurde hinzugefügt.](https://github.com/NuGet/Home/issues/566)
* [Prozess Drosselung zum Verringern der Prozessorauslastung hinzugefügt](https://github.com/NuGet/Home/issues/356)
* Verbesserte Referenz Behandlung für die portable Klassenbibliothek
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Bei der Auto Vervollständigen](https://github.com/NuGet/Home/issues/198)
* [Aktualisieren, um die grundlegenden Authentifizierungs Anmelde Informationen erneut einzuführen](https://github.com/NuGet/Home/issues/456)
* [Verbessertes Fehlerprotokoll](https://github.com/NuGet/Home/issues/407)
* [Verbesserte PowerShell-Fehlermeldungen beim Aufrufen von Update-Package](https://github.com/NuGet/Home/issues/5)

Laden Sie dieses [Update für die nuget-Erweiterung](https://nuget.codeplex.com/releases/view/615507) von CodePlex herunter. Weitere Informationen zum Fortschritt und Ankündigungen zu nuget 3,0 finden Sie in [unserem Blog](http://blog.nuget.org) .