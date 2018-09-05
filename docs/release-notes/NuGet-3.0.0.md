---
title: Anmerkungen zu NuGet-Version 3.0
description: Anmerkungen zu dieser Version für die Einbindung von NuGet 3.0.0 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551862"
---
# <a name="nuget-30-release-notes"></a>Anmerkungen zu NuGet-Version 3.0

[Anmerkungen zu NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1: Anmerkungen zu dieser Version](../release-notes/nuget-3.1.md)

NuGet 3.0 wurde am 20. Juli 2015 als Erweiterung des Pakets in Visual Studio 2015 veröffentlicht. Wir mithilfe von Push übertragen dieser Version mit Visual Studio bereitstellen, damit die vollständige aktualisierte NuGet 3.0-Benutzeroberfläche für neue Benutzer von Visual Studio verfügbar ist. Diese Version des NuGet-Erweiterung ist nur für Visual Studio 2015 verfügbar.

Es wird empfohlen, die Entwickler, die Zugriff auf Visual Studio-Update-Katalog auf die neueste Version, die verfügbar ist verfügen, da wir ein Update kurz nach der Veröffentlichung von Visual Studio 2015 veröffentlichen, die Unterstützung für Windows 10-Entwicklung enthält.

Insgesamt, die wir geschlossen 240 Probleme in der Version 3.0, und Sie können überprüfen, die [vollständige Liste der Probleme auf GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Bekannte Probleme

Es gab eine Reihe bekannter Probleme, die mit dieser Version bereitgestellt, und alle diese Elemente sind in unserer geplanten 3.1-Version an mit der Veröffentlichung von Windows 10 ab dem 29. Juli festgelegt.  Sie können zum Aktualisieren Ihrer Visual Studio-Erweiterungs über den Katalog am oder nach diesem Datum dieser bekannten Probleme zu beheben.

*  Übersetzung wird nicht für die Bezeichnung "Nicht mehr anzeigen", auf das Fenster "Vorschau" und die Bezeichnung "Autoren" in das Fenster der Paket-Beschreibung bereitgestellt.
*  Wenn Sie an einem Projekt arbeiten, mit der TFS--Steuerelement Source kann nicht NuGet der Paket-Manager-Benutzeroberfläche vorhanden, wenn die Datei "NuGet.config" als schreibgeschützt markiert ist.
   * **Problemumgehung** sehen Sie sich die Datei von TFS.
*  Text in Gelb "Neustart Bar" im NuGet-Powershell-Fenster ist nicht sichtbar, wenn Sie das dunkle Design von Visual Studio verwenden.
   * **Problemumgehung** das helle Design von Visual Studio verwenden.


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
* [Korrigiert den "Erfahren Sie mehr zu den Optionen"-Link, um zu vermeiden, stürzt ab, unter Windows 10](https://github.com/NuGet/Home/issues/822)
* [Beachten Sie die Vorabversion Kontrollkästchen-Einstellung](https://github.com/NuGet/Home/issues/732)
* [Verbesserte Gather-Leistung durch Zwischenspeichern der Ergebnisse für Projekte in einer Projektmappe](https://github.com/NuGet/Home/issues/721)
* [Mehrere Pakete können gleichzeitig gesammelt werden](https://github.com/NuGet/Home/issues/713)
* [Entfernt die Install-Package-Befehls erzwingen](https://github.com/NuGet/Home/issues/697)

Bitte achten Sie auf [unseren Blog](http://blog.nuget.org) weitere Bearbeitung und Ankündigungen, da wir für die Unterstützung für Windows 10-Entwicklung vorzubereiten.