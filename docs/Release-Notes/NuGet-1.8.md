---
title: 1.8 NuGet-Versionshinweise
description: Versionshinweise für NuGet 1.8 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1801d62b786717c088429fbeca6f1f72f5ab6b4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-18-release-notes"></a>1.8 NuGet-Versionshinweise

[Anmerkungen zur Version des NuGet-1.7](../release-notes/nuget-1.7.md) | [NuGet 2.0-Versionshinweise](../release-notes/nuget-2.0.md)

NuGet 1.8 wurde 23 Mai 2012 veröffentlicht.

## <a name="known-installation-issue"></a>Bekannte Problem
Wenn Sie Visual Studio 2010 SP1 ausführen, kann ein Installationsfehler auftreten beim Upgrade von NuGet ausführen, wenn Sie eine ältere Version installiert haben.

Die problemumgehung besteht darin, einfach NuGet deinstallieren und installieren Sie es aus dem Katalog der VS-Erweiterung.  Finden Sie unter [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) für Weitere Informationen oder [fahren Sie direkt mit den VS-Hotfix](http://bit.ly/vsixcertfix).

Hinweis: Wenn Visual Studio lässt Sie beim Deinstallieren der Erweiterung (die Schaltfläche "Deinstallieren" deaktiviert ist), müssen Sie wahrscheinlich zum Neustart von Visual Studio, die mit "Als Administrator ausführen".

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet-1.8 inkompatibel mit Windows XP, Hotfix veröffentlicht

Kurz nach dem NuGet-1.8 freigegeben wurde, Sie gelernt, dass eine Änderung der Kryptografie 1.8 Benutzer unter Windows XP unterbrochen wurde.

Wir haben seit einen Hotfix veröffentlicht, der dieses Problem behoben.  Durch die Aktualisierung über die Visual Studio-Erweiterung Gallery NuGet, erhalten Sie diesen Hotfix an.

## <a name="features"></a>Features

### <a name="satellite-packages-for-localized-resources"></a>Satelliten-Pakete für lokalisierte Ressourcen
NuGet-1.8 unterstützt jetzt die Möglichkeit zum Erstellen von separaten Paketen für lokalisierte Ressourcen, ähnlich den Funktionen des Satelliten-Assembly von .NET Framework.  Ein Satellit-Paket wird in die gleiche Weise wie andere NuGet-Paket sowie zusätzlich einige Konventionen erstellt:

* Der Satellit Paket-ID und der Dateiname sollte ein Suffix, das einem des Standards entspricht enthalten [Kultur Zeichenfolgen, die von .NET Framework verwendet](http://msdn.microsoft.com/goglobal/bb896001.aspx).
* In seiner `.nuspec` , das Paket Satellit sollten definieren ein Sprachelement mit derselben Kulturzeichenfolge, die in der ID verwendet
* Die Satelliten-Paket sollte eine Abhängigkeit im Definieren der `.nuspec` Datei, die die zentrale Paket, d. h. einfach das Paket mit der gleichen ID minus der Language-Suffix.  Das Hauptpaket muss im Repository für die erfolgreiche Installation verfügbar sein.

Zum Installieren eines Pakets mit lokalisierten Ressourcen wählt ein Entwickler explizit das lokalisierte Paket aus dem Repository. Zu diesem Zeitpunkt geben die NuGet Gallery kein beliebiger besondere Behandlung notwendig, um die Satelliten-Pakete.

![Paket-Manager-Dialogfeld mit lokalisierten pacakges](./media/dlg-w-loc-packs.png)

Da das Paket Satellit eine Abhängigkeit zu seiner Hauptpaket aufgelistet sind, sind die Satelliten und die Core-Pakete in den Ordner "NuGet-Pakete" abgerufen und installiert.

![Pakete mit lokalisierte Pakete (Ordner)](./media/fldr-loc-packs.png)

Darüber hinaus wird beim Installieren der Satelliten-Paket, ein NuGet erkennt außerdem die Namenskonvention für die Kultur Zeichenfolge und kopiert dann die lokalisierte Ressourcen-Assembly, in der richtigen Unterordner das Hauptpaket, damit sie von .NET Framework ausgewählt werden kann.

![Core-Paketordner mit kopierten Ressourcenordner](./media/fldr-copied-loc.png)

Einem vorhandenen Fehler mit Satelliten-Paketen beachten ist, dass NuGet nicht lokalisierte Ressourcen kopiert die `bin` Ordner für Websiteprojekte.  Dieses Problem wird in der nächsten Version von NuGet behoben werden.

Ein vollständiges Beispiel demonstriert, zum Erstellen und Verwenden von Satelliten-Paketen finden Sie unter [ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample).

### <a name="package-restore-consent"></a>Paket-Restore-Zustimmung
NuGet-1.8 gemäß wir die Grundlagen für eine wichtige Einschränkung auf paketwiederherstellung zum Schutz der Privatsphäre der Benutzer zu unterstützen. Diese Einschränkung ist erforderlich, dass Entwickler Erstellen von Projekten und Projektmappen, die paketwiederherstellung explizit zu Restore-Paket Zustimmung verwenden zum Herunterladen von Paketen von konfigurierten Paketquellen online geschaltet des.

Es gibt 2 Möglichkeiten, diese Zustimmung bereitzustellen. Die erste kann in der Paket-Manager-Dialogfeld "Konfiguration" unten abgebildeten gefunden werden.  Diese Methode dient in erster Linie für Entwickler-Computer.

![Dialogfeld "Konfiguration" der Paket-manager](./media/pr-consent-configdlg.png)

Die zweite Methode ist die Umgebung Variable "EnableNuGetPackageRestore" auf den Wert "True" festgelegt.  Diese Methode wird für unbeaufsichtigte Computer z. B. CI oder Build Server vorgesehen.

Jetzt haben wie oben erwähnt, wir nur die Grundlagen für diese Funktion in NuGet 1.8 angeordnet.  In der Praxis bedeutet dies, dass, während wir die gesamte Logik zum Aktivieren der Funktion hinzugefügt haben, es wird derzeit nicht in dieser Version erzwungen wird. Es wird aktiviert, jedoch in der nächsten Version von NuGet, daher Sie sie so bald wie möglich erkennen sollten, damit Sie Ihre Umgebungen entsprechend konfigurieren können und daher nicht betroffen, wenn wir beginnen die Zustimmung Einschränkung erzwungen.

Weitere Informationen finden Sie unter der [team-Blogbeitrag](http://blog.nuget.org/20120518/package-restore-and-consent.html) zu dieser Funktion.

### <a name="nugetexe-performance-improvements"></a>Leistungsverbesserungen NuGet.exe
Ändern Sie den Befehl installieren, herunterladen und Installieren von Paketen parallel, bringt NuGet 1.8 erhebliche Leistungssteigerungen nuget.exe – und durch Erweiterung paketwiederherstellung.  Testen von hoher Ebene zeigt an, verbessert die Leistung für die Installation von 6 Pakete in ein Projekt von ca. 35 % in NuGet 1.8.  Erhöhen der Anzahl von Paketen in 25 zeigt eine Leistungssteigerung von ca. 60 %.

## <a name="bug-fixes"></a>Fehlerkorrekturen
NuGet 1.8 enthält einige Fehlerkorrekturen mit Schwerpunkt auf der Paket-Manager-Konsole und die Wiederherstellung Paketworkflows, besonders in Bezug auf das Paket wiederherstellen Zustimmung und Windows 8 Express-Integration.
Eine vollständige Liste der Arbeit Elemente in behoben NuGet 1.8, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
