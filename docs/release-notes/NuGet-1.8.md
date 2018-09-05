---
title: Anmerkungen zu NuGet Version 1.8
description: Anmerkungen zu NuGet 1.8, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ff6d12606b1bed479e63eebccd978ff9cd4a7faf
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546620"
---
# <a name="nuget-18-release-notes"></a>Anmerkungen zu NuGet Version 1.8

[Anmerkungen zu NuGet 1.7](../release-notes/nuget-1.7.md) | [Anmerkungen zu NuGet 2.0](../release-notes/nuget-2.0.md)

NuGet 1.8 wurde am 23 Mai 2012 veröffentlicht.

## <a name="known-installation-issue"></a>Problem für bekannte Installationsprobleme
Wenn Sie Visual Studio 2010 SP1 ausführen, können Sie ein Installationsfehler auftreten, beim Versuch, NuGet aktualisieren, wenn Sie eine ältere Version installiert haben.

Die problemumgehung besteht darin, einfach NuGet zuerst deinstallieren und installieren Sie es aus dem Katalog der VS-Erweiterung.  Finden Sie unter [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Informationen oder [gehen Sie direkt auf den VS-Hotfix](http://bit.ly/vsixcertfix).

Hinweis: Wenn Visual Studio ist es nicht zulässig, die die Erweiterung deinstallieren (die Schaltfläche "Deinstallieren" deaktiviert ist), müssen Sie wahrscheinlich zum Neustart von Visual Studio mithilfe von "Ausführen als Administrator."

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 inkompatibel mit Windows XP, Hotfix veröffentlicht

Kurz nach dem NuGet 1.8 veröffentlicht wurde, haben Sie erfahren, dass eine Änderung der Kryptografie 1.8 Benutzer unter Windows XP unterbrochen wurde.

Wir haben da einen Hotfix veröffentlicht, der dieses Problem behandelt.  Durch die Aktualisierung von NuGet über die Visual Studio Extension Gallery, erhalten Sie diesen Hotfix.

## <a name="features"></a>Features

### <a name="satellite-packages-for-localized-resources"></a>Satellitenpakete für lokalisierte Ressourcen
NuGet 1.8 unterstützt jetzt die Möglichkeit zum Erstellen von separaten Pakete für die lokalisierte Ressourcen, ähnlich den Funktionen des Satelliten-Assembly von .NET Framework.  Satellitenpakete wird an die gleiche Weise wie andere NuGet-Pakete durch das Hinzufügen von einigen Konventionen erstellt:

* Der Satelliten-Paket-ID und der Dateiname sollte ein Suffix, das einer der standardmäßigen entspricht enthalten [Kultur Zeichenfolgen, die von .NET Framework verwendet](http://msdn.microsoft.com/goglobal/bb896001.aspx).
* In der `.nuspec` -Datei des satellitenpakets fest, einen Language-Element mit der gleichen Kulturzeichenfolge, die in der ID verwendet
* Des satellitenpakets muss eine Abhängigkeit im Definieren der `.nuspec` Datei, die die Core-Paket, die einfach auf das Paket mit der gleichen ID ohne das Suffix für die Sprache darstellt.  Das Core-Paket muss im Repository für die erfolgreiche Installation verfügbar sein.

Um ein Paket mit lokalisierten Ressourcen zu installieren, wählt ein Entwickler explizit das lokalisierte Paket aus dem Repository. Derzeit werden im NuGet-Katalog keine Art von besondere Behandlung notwendig, um satellitenpakete gewährt.

![Paket-Manager-Dialogfeld mit lokalisierten pacakges](./media/dlg-w-loc-packs.png)

Da eine Abhängigkeit zu der Core-Paket des satellitenpakets aufgelistet werden, sind sowohl der Satelliten-als auch die Core-Pakete in der NuGet-Paketordner abgerufen und installiert.

![Ordner "Pakete" von lokalisierten Paketen](./media/fldr-loc-packs.png)

Darüber hinaus wird beim Installieren des satellitenpakets, ein NuGet erkennt außerdem die Namenskonvention für die Kultur Zeichenfolge und kopiert dann die lokalisierte Ressourcen-Assembly, in der richtigen Unterordner innerhalb des Pakets, damit sie von .NET Framework ausgewählt werden kann.

![Core-Paket-Ordner mit den kopierten Ordner](./media/fldr-copied-loc.png)

Einen vorhandenen Fehler mit satellitenpakete zu beachten ist, dass NuGet nicht lokalisierte Ressourcen, die die `bin` Ordner für Websiteprojekte.  Dieses Problem wird in der nächsten Version von NuGet behoben werden.

Ein vollständiges Beispiel veranschaulicht, wie zum Erstellen und Verwenden von Satellitenassemblys finden Sie unter [ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample).

### <a name="package-restore-consent"></a>Paket wiederherstellen Zustimmung
In NuGet 1.8 Layout wir die Grundlagen für eine wichtige Einschränkung bei der paketwiederherstellung zum Schutz der Privatsphäre der Benutzer zu unterstützen. Diese Einschränkung ist erforderlich, dass Entwickler, die Projekte und Projektmappen, die paketwiederherstellung verwenden explizit seine Zustimmung erteilen, Wiederherstellung Verpacken online zum Herunterladen von Paketen aus konfigurierten Paketquellen die Folie aufruft.

Es gibt 2 Möglichkeiten dieser zustimmen. Die erste finden Sie in der Paket-Manager-Dialogfeld "Konfiguration" wie unten dargestellt.  Diese Methode ist in erster Linie für Entwicklercomputer vorgesehen.

![Dialogfeld "Konfiguration" der Paket-manager](./media/pr-consent-configdlg.png)

Die zweite Methode ist die Umgebung "EnableNuGetPackageRestore"-Variable auf den Wert "True" festgelegt.  Diese Methode wird für unbeaufsichtigte Computer z. B. CI oder Build-Server vorgesehen.

Jetzt haben wie oben erwähnt, wir nur die Grundlagen für diese Funktion in NuGet 1.8 angeordnet.  In der Praxis bedeutet dies, dass, während wir die gesamte Logik zum Aktivieren des Features hinzugefügt haben, es derzeit nicht in dieser Version erzwungen wird. Es aktiviert, jedoch in der nächsten Version von NuGet, und wir Sie darauf aufmerksam machen so bald wie möglich vornehmen wollten, damit Sie Ihre Umgebungen ordnungsgemäß konfigurieren können und daher nicht betroffen, wenn zunächst die Zustimmung Einschränkung erzwungen.

Weitere Informationen finden Sie unter den [team-Blog-Beitrag](http://blog.nuget.org/20120518/package-restore-and-consent.html) zu dieser Funktion.

### <a name="nugetexe-performance-improvements"></a>NuGet.exe-Leistungsverbesserungen
Ändern Sie den Befehl "Install" herunterladen und Installieren von Paketen parallel, bringt NuGet 1.8 erhebliche leistungsverbesserungen nuget.exe – und durch Erweiterung die paketwiederherstellung auf.  Testen von hohen Ebene zeigt, dass es sich bei verbessert die Leistung für die Installation von 6 Pakete in ein Projekt von ca. 35 % in NuGet 1.8.  Erhöhen der Anzahl von Paketen in 25 zeigt einen Leistungsgewinn von ca. 60 %.

## <a name="bug-fixes"></a>Fehlerkorrekturen
NuGet 1.8 enthält einige Fehlerbehebungen mit Schwerpunkt auf die Paket-Manager-Konsole und Wiederherstellung Paketworkflow, vor allem mit Bezug auf das Paket wiederherstellen Zustimmung und Windows 8 Express-Integration.
Eine vollständige Liste der Arbeit Elemente eine feste in NuGet 1.8, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
