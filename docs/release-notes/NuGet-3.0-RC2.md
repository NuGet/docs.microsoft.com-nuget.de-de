---
title: NuGet 3.0 RC2 – Versionshinweise
description: Anmerkungen zu NuGet 3.0 RC2 einschließlich bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 863e48e632387b768a43530b987683605baf6db7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545820"
---
# <a name="nuget-30-rc2-release-notes"></a>NuGet 3.0 RC2 – Versionshinweise

[Anmerkungen zu dieser Version von NuGet 3.0 RC](../release-notes/nuget-3.0-RC.md) | [Anmerkungen zu NuGet 3.0](../release-notes/nuget-3.0.0.md)

NuGet 3.0 RC2 wurde als eine vorläufige Version aus der Visual Studio 2015-Erweiterungskatalog 3 Juni 2015 veröffentlicht und [Codeplex](https://nuget.codeplex.com/releases/view/615507). Diese Version enthält eine Reihe von wichtigen Fehlerbehebungen und leistungsverbesserungen, die unserer Meinung nach war sehr wichtig, bevor Sie die vollständige Visual Studio 2015-Version freizugeben. Diese Version des NuGet-Erweiterung ist nur für Visual Studio 2015 verfügbar.

Insgesamt, die wir geschlossen 158 Probleme in dieser Version, und Sie können überprüfen, die [vollständige Liste der Probleme auf GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).

## <a name="summary-of-top-issues-resolved"></a>Zusammenfassung der wichtigsten Probleme behoben

* [Häufige Netzwerk Update aufruft, wenn Fenster der Paket-Manager aktualisiert](https://github.com/NuGet/Home/issues/515)
* [Scrollen Sie verzögert, wenn Ansicht ändern, um im Paket-Manager installiert werden.](https://github.com/NuGet/Home/issues/519)
* [Netzwerkaufrufe sollte in einem Hintergrundthread ausgeführt werden](https://github.com/NuGet/Home/issues/516)
* [Kontrollkästchen "Fenster" Vorschau "nicht anzeigen" hinzugefügt](https://github.com/NuGet/Home/issues/566)
* [Hinzugefügte Prozess Drosselung, um die prozessorauslastung zu reduzieren.](https://github.com/NuGet/Home/issues/356)
* Verbesserte Behandlung der Referenz zur portablen Klassenbibliothek
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [AutoVervollständigen-Dienst konnte die Groß-/Kleinschreibung beachten](https://github.com/NuGet/Home/issues/198)
* [Aktualisiert werden, um die Anmeldeinformationen für Standardauthentifizierung Rückmeldung](https://github.com/NuGet/Home/issues/456)
* [Verbessertes Fehlerprotokoll](https://github.com/NuGet/Home/issues/407)
* [Verbesserte Powershell Fehlermeldungen beim Aufrufen des Update-Package](https://github.com/NuGet/Home/issues/5)

Diese Software [aktualisieren Sie auf der NuGet-Erweiterung](https://nuget.codeplex.com/releases/view/615507) von CodePlex herunter, und halten Sie Ausschau auf [unseren Blog](http://blog.nuget.org) für die weitere Bearbeitung sowie Ankündigungen von NuGet 3.0!