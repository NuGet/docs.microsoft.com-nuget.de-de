---
title: Anmerkungen zu dieser Version von nuget 3,0
description: Anmerkungen zu dieser Version von nuget 3.0.0 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776559"
---
# <a name="nuget-30-release-notes"></a>Anmerkungen zu dieser Version von nuget 3,0

Anmerkungen zu dieser [Version von nuget 3,0 rc2](../release-notes/nuget-3.0-RC2.md)  |  [Anmerkungen zu dieser Version von nuget 3,1](../release-notes/nuget-3.1.md)

Nuget 3,0 wurde am 20. Juli 2015 als Bündel Erweiterung für Visual Studio 2015 veröffentlicht. Wir haben diese Version mit Visual Studio bereitgestellt, damit die gesamte aktualisierte nuget 3,0-Umgebung für neue Visual Studio-Benutzer verfügbar ist. Diese nuget-Erweiterungs Version ist nur für Visual Studio 2015 verfügbar.

Wir empfehlen Entwicklern, die Zugriff auf das Visual Studio Gallery-Update haben, auf die neueste verfügbare Version, da wir kurz nach der Veröffentlichung von Visual Studio 2015 ein Update veröffentlichen, das Unterstützung für die Windows 10-Entwicklung enthält.

Insgesamt haben wir 240 Probleme in der 3,0-Version geschlossen, und Sie können die [vollständige Liste der Probleme auf GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)überprüfen.

## <a name="known-issues"></a>Bekannte Probleme

In dieser Version sind einige bekannte Probleme aufgetreten, und alle diese Elemente wurden in unserer geplanten Version 3,1 korrigiert, damit Sie am 29. Juli mit der Veröffentlichung von Windows 10 übereinstimmen.  Sie können Ihre Visual Studio-Erweiterung aus dem Katalog am oder nach diesem Datum aktualisieren, um diese bekannten Probleme zu beheben.

*  Die Bezeichnung "nicht mehr anzeigen" im Vorschaufenster und die Bezeichnung "Autoren" im Paket Beschreibungs Fenster wurde nicht bereitgestellt.
*  Wenn Sie mit der TFS-Quell Code Verwaltung an einem Projekt arbeiten, kann nuget die Benutzeroberfläche des Paket-Managers nicht präsentieren, wenn die Nuget.Config Datei als schreibgeschützt gekennzeichnet ist.
   * Problem **Umgehung** Sehen Sie sich die Datei aus TFS an.
*  Wenn Sie das Design "dunkel" von Visual Studio verwenden, wird der Text im Fenster "nuget-PowerShell" nicht angezeigt.
   * Problem **Umgehung** Verwenden Sie das Design "Light" von Visual Studio.


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
* [Der Link "Informationen zu Optionen" wurde korrigiert, um Abstürze unter Windows 10 zu verhindern.](https://github.com/NuGet/Home/issues/822)
* [Kontrollkästchen "Vorabversion speichern"](https://github.com/NuGet/Home/issues/732)
* [Verbesserte Leistungs Erfassung durch Zwischenspeichern von Ergebnissen in Projekten in einer Projekt Mappe](https://github.com/NuGet/Home/issues/721)
* [Mehrere Pakete können parallel gesammelt werden.](https://github.com/NuGet/Home/issues/713)
* [Befehl "Install-package-Force" entfernt](https://github.com/NuGet/Home/issues/697)

Beachten Sie [unseren Blog](http://blog.nuget.org) , um mehr über den Fortschritt und die Ankündigungen zu erfahren, da wir bereit sind, Support für die Windows 10-Entwicklung bereitzustellen.