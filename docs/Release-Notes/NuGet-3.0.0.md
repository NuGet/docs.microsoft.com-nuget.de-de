---
title: NuGet-3.0-Versionshinweise | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Versionshinweise für NuGet 3.0.0 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
keywords: NuGet-3.0.0 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: fc669e4a8440c295f08eef461186eef5f505df42
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-30-release-notes"></a>NuGet-Version 3.0-Hinweise

[Anmerkungen zur Version von NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1-Versionshinweise](../release-notes/nuget-3.1.md)

NuGet-3.0 wurde auf dem 20. Juli 2015 als Erweiterung des Pakets in Visual Studio 2015 veröffentlicht. Wir abgelegt, damit die vollständige aktualisierte NuGet-3.0-Erfahrung für neue Visual Studio-Benutzer verfügbar wäre dieser Version von Visual Studio zu übermitteln. Diese Version des NuGet-Erweiterung ist nur für Visual Studio 2015 verfügbar.

Es wird empfohlen, die Entwickler mit Zugriff auf die Visual Studio Gallery-Update auf die neueste Version, die verfügbar ist, wie wir ein Update kurz nach der Veröffentlichung von Visual Studio 2015 veröffentlichen, die Unterstützung für die Entwicklung von Windows 10 enthält.

Insgesamt, die wir geschlossen 240 Probleme in der Version 3.0, und Sie können überprüfen, die [vollständige Liste der Probleme auf GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Bekannte Probleme

Gab es eine Reihe bekannter Probleme, die im Lieferumfang dieser Version und alle diese Elemente sind in unserer geplanten 3.1-Version mit der Version von Windows 10 nach einer auf dem 29. Juli fest.  Sie können beim Aktualisieren Ihrer Visual Studio-Erweiterungs aus dem Katalog am oder nach diesem Datum dieser bekannten Probleme zu beheben.

*  Übersetzung ist nicht für die Bezeichnung "Nicht erneut anzeigen", auf das Vorschaufenster und die Bezeichnung "Autoren" im Fenster Beschreibung Paket bereitgestellt.
*  Wenn Sie die Arbeiten an einem Projekt mithilfe von TFS Datenquellen, kann nicht NuGet der Paket-Manager-Benutzeroberfläche vorhanden, wenn die Datei "Nuget.Config" als schreibgeschützt gekennzeichnet ist.
   * **Problemumgehung** sehen Sie sich die Datei von TFS.
*  Text in der gelbe "Restart-weißen Balken im NuGet Powershell-Fenster ist nicht sichtbar, wenn Sie die Visual Studio Design" dunkel "verwenden.
   * **Problemumgehung** das helle Design von Visual Studio verwenden.


## <a name="summary-of-top-issues-resolved"></a>Zusammenfassung der wichtigsten Probleme behoben

* [Häufige Netzwerk Update Ruft auf, wenn die Paket-Manager-Fenster wird aktualisiert](https://github.com/NuGet/Home/issues/515)
* [Führen Sie einen Bildlauf verzögert, wenn Ansicht ändern im Paket-Manager installiert werden.](https://github.com/NuGet/Home/issues/519)
* [Netzwerkaufrufe sollte in einem Hintergrundthread ausgeführt werden](https://github.com/NuGet/Home/issues/516)
* [Kontrollkästchen "Fenster" Preview "nicht anzeigen" hinzugefügt](https://github.com/NuGet/Home/issues/566)
* [Hinzugefügte Prozess Einschränkung zur prozessorauslastung zu reduzieren.](https://github.com/NuGet/Home/issues/356)
* Verbesserte Behandlung Portable Klassenbibliothek-Referenz
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [AutoVervollständigen-Dienst entsprechend seiner Groß-/Kleinschreibung unterschieden](https://github.com/NuGet/Home/issues/198)
* [Aktualisiert werden, um die Anmeldeinformationen für Standardauthentifizierung Rückmeldung](https://github.com/NuGet/Home/issues/456)
* [Verbesserte fehlerprotokollierung](https://github.com/NuGet/Home/issues/407)
* [Verbesserte Powershell Fehlermeldungen beim Aufrufen von Update-Paket](https://github.com/NuGet/Home/issues/5)
* [Korrigiert den Link "Weitere Informationen zu den Optionen", um zu verhindern, aber bei Windows 10](https://github.com/NuGet/Home/issues/822)
* [Denken Sie daran Vorabversion Checkbox-Einstellung](https://github.com/NuGet/Home/issues/732)
* [Verbesserte Gather-Leistung durch Zwischenspeichern der Ergebnisse übergreifend über Projekte in einer Projektmappe](https://github.com/NuGet/Home/issues/721)
* [Gleichzeitig können mehrere Pakete erfasst werden](https://github.com/NuGet/Home/issues/713)
* [Install-Package entfernt-Befehl zu erzwingen](https://github.com/NuGet/Home/issues/697)

Bitte achten Sie auf [unserem Blog](http://blog.nuget.org) weitere Bearbeitung und Ankündigungen wie wir bieten Unterstützung für die Entwicklung von Windows 10 bereiten.