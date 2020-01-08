---
title: Anmerkungen zu dieser Version von nuget 1,8
description: Anmerkungen zu dieser Version von nuget 1,8 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 973a2d010cb75eeeb383be94baf2fb17a999dd7c
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383460"
---
# <a name="nuget-18-release-notes"></a>Anmerkungen zu dieser Version von nuget 1,8

Anmerkungen zu [nuget 1,7](../release-notes/nuget-1.7.md) | Anmerkungen zur [nuget](../release-notes/nuget-2.0.md) -Version 2,0

Nuget 1,8 wurde am 23. Mai 2012 veröffentlicht.

## <a name="known-installation-issue"></a>Bekanntes Installationsproblem
Wenn Sie Visual Studio 2010 SP1 ausführen, tritt möglicherweise ein Installationsfehler auf, wenn Sie versuchen, ein Upgrade für nuget auszuführen, wenn Sie eine ältere Version installiert haben.

Die Problem Umgehung besteht darin, dass Sie nuget einfach deinstallieren und anschließend aus dem vs-Erweiterungs Katalog installieren.  Weitere Informationen finden Sie unter <https://support.microsoft.com/kb/2581019>, oder wechseln [Sie direkt zum vs-Hotfix](http://bit.ly/vsixcertfix).

Hinweis: Wenn Visual Studio die Deinstallation der Erweiterung nicht zulässt (die Schaltfläche "deinstallieren" ist deaktiviert), müssen Sie Visual Studio wahrscheinlich mit "als Administrator ausführen" neu starten.

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>Nuget 1,8 nicht kompatibel mit Windows XP, veröffentlichte Hotfix

Kurz nach der Veröffentlichung von nuget 1,8 haben wir gelernt, dass eine kryptografieänderung in 1,8 Benutzer unter Windows XP abgebrochen hat.

Wir haben seitdem einen Hotfix veröffentlicht, der dieses Problem behandelt.  Wenn Sie nuget über den Visual Studio-Erweiterungs Katalog aktualisieren, erhalten Sie diesen Hotfix.

## <a name="features"></a>Features

### <a name="satellite-packages-for-localized-resources"></a>Satelliten Pakete für lokalisierte Ressourcen
Nuget 1,8 unterstützt jetzt die Möglichkeit, separate Pakete für lokalisierte Ressourcen zu erstellen, ähnlich wie die satellitenassemblyfunktionen der .NET Framework.  Ein Satelliten Paket wird auf die gleiche Weise wie jedes andere nuget-Paket erstellt, wobei einige Konventionen hinzugefügt werden:

* Die Satelliten Paket-ID und der Dateiname sollten ein Suffix enthalten, das einer der [vom .NET Framework verwendeten Standard Kultur](https://docs.microsoft.com/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)Zeichenfolgen entspricht.
* In der `.nuspec` Datei sollte das Satelliten Paket ein sprach Element mit derselben Kultur Zeichenfolge definieren, die in der ID verwendet wird.
* Das Satellitenpaket sollte eine Abhängigkeit in der `.nuspec`-Datei mit dem Kern Paket definieren, d. h. das Paket mit der gleichen ID und dem sprach Suffix.  Das Core-Paket muss im Repository zur erfolgreichen Installation verfügbar sein.

Zum Installieren eines Pakets mit lokalisierten Ressourcen wählt ein Entwickler explizit das lokalisierte Paket aus dem Repository aus. Der nuget-Katalog bietet derzeit keine besondere Behandlung von Satelliten Paketen.

![Dialogfeld "Paket-Manager" mit lokalisierten Paketen](./media/dlg-w-loc-packs.png)

Da das Satelliten Paket eine Abhängigkeit zu seinem Kern Paket auflistet, werden sowohl das Satelliten-als auch das Core-Paket in den nuget-Paket Ordner gezogen und installiert.

![Paket Ordner mit lokalisierten Paketen](./media/fldr-loc-packs.png)

Außerdem erkennt nuget beim Installieren des Satelliten Pakets auch die Kultur Zeichenfolgen-Benennungs Konvention und kopiert dann die lokalisierte Ressourcenassembly in den richtigen Unterordner innerhalb des Core-Pakets, damit Sie vom .NET Framework ausgewählt werden kann.

![Kernpaket Ordner mit kopiertem Ressourcen Ordner](./media/fldr-copied-loc.png)

Ein bereits vorhandener Fehler bei Satelliten Paketen besteht darin, dass nuget keine lokalisierten Ressourcen in den Ordner `bin` für Website Projekte kopiert.  Dieses Problem wird in der nächsten Version von nuget behoben.

Ein umfassendes Beispiel, das zeigt, wie Satelliten Pakete erstellt und verwendet werden, finden Sie unter [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).

### <a name="package-restore-consent"></a>Zustimmung zur Paket Wiederherstellung
In nuget 1,8 haben wir die Grundlagen für die Unterstützung einer wichtigen Einschränkung bei der Paket Wiederherstellung zum Schutz der Privatsphäre von Benutzern geschaffen. Diese Einschränkung erfordert, dass Entwickler Projekte und Projektmappen mit der Paket Wiederherstellung explizit dem Online schalten der Paket Wiederherstellung zustimmen, um Pakete aus den konfigurierten Paketquellen herunterzuladen.

Es gibt zwei Möglichkeiten, diese Zustimmung bereitzustellen. Die erste finden Sie im Dialogfeld Paket-Manager-Konfiguration, wie unten gezeigt.  Diese Methode ist hauptsächlich für Entwickler Computer vorgesehen.

![Dialog](./media/pr-consent-configdlg.png)

Die zweite Methode besteht darin, die Umgebungsvariable "enablenugetpackagerestore" auf den Wert "true" festzulegen.  Diese Methode ist für unbeaufsichtigte Computer wie CI-oder Buildserver vorgesehen.

Wie oben bereits erwähnt, haben wir den Grund für dieses Feature in nuget 1,8 festgelegt.  Praktisch bedeutet dies, dass zwar die gesamte Logik zum Aktivieren der Funktion hinzugefügt wurde, aber in dieser Version zurzeit nicht erzwungen wird. Sie wird jedoch in der nächsten Version von nuget aktiviert, daher sollten Sie Sie so schnell wie möglich kennen, damit Sie Ihre Umgebungen entsprechend konfigurieren können und daher nicht beeinträchtigt werden, wenn wir beginnen, die Zustimmungs Einschränkung zu erzwingen.

Weitere Informationen finden Sie im [Teamblog Beitrag](http://blog.nuget.org/20120518/package-restore-and-consent.html) zu diesem Feature.

### <a name="nugetexe-performance-improvements"></a>Leistungsverbesserungen für "nuget. exe"
Durch Ändern des Installations Befehls zum parallelen herunterladen und Installieren von Paketen bringt nuget 1,8 drastische Leistungsverbesserungen für "nuget. exe" – und die Wiederherstellung von Erweiterungs Paketen.  Tests auf hoher Ebene zeigen, dass die Leistung für die Installation von 6 Paketen in einem Projekt um ungefähr 35% in nuget 1,8 verbessert wird.  Das Erhöhen der Anzahl von Paketen auf 25 zeigt einen Leistungsgewinn von ungefähr 60%.

## <a name="bug-fixes"></a>Fehlerkorrekturen
Nuget 1,8 enthält eine Reihe von Fehlerbehebungen mit einem Schwerpunkt auf die Paket-Manager-Konsole und den Paket Wiederherstellungs Workflow, insbesondere in Bezug auf die Zustimmung zur Paket Wiederherstellung und Windows 8 Express-Integration.
Eine vollständige Liste der Arbeitselemente, die in nuget 1,8 behoben wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
