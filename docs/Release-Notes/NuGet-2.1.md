---
title: Anmerkungen zur Version des NuGet-2.1 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Versionshinweise für NuGet 2.1 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
keywords: NuGet-2.1 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 06116a86887b5561ad4e2ecad8090222d16cd333
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-21-release-notes"></a>NuGet-Version 2.1 Hinweise

[Anmerkungen zur Version von NuGet 2.0](../release-notes/nuget-2.0.md) | [NuGet-2.2-Versionshinweise](../release-notes/nuget-2.2.md)

NuGet-2.1 wurde am 4. Oktober 2012 veröffentlicht.

## <a name="hierarchical-nugetconfig"></a>Hierarchische "NuGet.config".
NuGet-2.1 bietet Ihnen mehr Flexibilität beim Steuern des NuGet-Einstellungen über die Ordnerstruktur für die Suche am rekursiv `NuGet.Config` Dateien, und klicken Sie dann die Konfiguration aus dem Satz aller gefundenen Dateien erstellen.  Beispielsweise sollten Sie das Szenario, in dem ein Team eine interne paketrepository für CI-Builds von anderen internen Abhängigkeiten verfügt. Die Ordnerstruktur für ein einzelnes Projekt könnte folgendermaßen aussehen:

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

Wenn paketwiederherstellung für die Projektmappe aktiviert ist, wird darüber hinaus auch die folgende Ordner vorhanden:

    C:\myteam\solution1\.nuget

Um das Team interne paketrepository für alle Projekte zur Verfügung zu haben, die auf das Team arbeitet, während Sie nicht auf dem Computer für jedes Projekt verfügbar gemacht, können wir erstellen eine neue Datei mit "Nuget.Config" und platzieren Sie es im Ordner "c:\myteam". Es gibt keine Möglichkeit zu geben einen Ordner "Pakete" pro Projekt.

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

Jetzt sehen, dass die Quelle hinzugefügt wurde, durch Ausführen des Befehls "nuget.exe Quellen" aus einem beliebigen Ordner unterhalb c:\myteam wie unten dargestellt:

![Paketquellen aus der übergeordneten NuGet-Konfiguration](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` Dateien werden in der folgenden Reihenfolge gesucht:

1. `.nuget\Nuget.Config`
2. Rekursives durchlaufen aus dem Projektordner zum Stamm
3. Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)

Konfigurationen handelt es sich in angewendet der *Reihenfolge umkehren,*, d. h., die auf die oben genannten Reihenfolge basieren, die globale "NuGet.config" würde werden zuerst angewendet, gefolgt von den ermittelten "NuGet.config"-Dateien vom Stamm zum Projektordner, gefolgt durch `.nuget\Nuget.Config`.  Dies ist besonders wichtig, wenn Sie verwenden die `<clear/>` zu eine Gruppe von Elementen aus der Konfiguration zu entfernenden Elements.

## <a name="specify-packages-folder-location"></a>Geben Sie "Packages" Speicherort des Ordners
In der Vergangenheit wurde eine Lösung Pakete NuGet aus einem bekannten "Pakete" Ordner unterhalb des Ordners des Lösung Stamm gefunden verwaltet werden.  Entwicklungsteams, die viele verschiedene Lösungen auf die NuGet-Pakete installiert haben, kann dies im selben Paket wird in vielen verschiedenen Quellen im Dateisystem installiert führen.

NuGet-2.1 bietet eine detailliertere Kontrolle über den Speicherort des Ordners Pakete über die `repositoryPath` Element in der `NuGet.Config` Datei.  Baut auf dem vorherigen Beispiel der hierarchischen "NuGet.config" Unterstützung und wird davon ausgegangen Sie, dass wir alle Projekte unter C:\myteam\ Freigabe der gleichen Paketordner haben möchten.  Um dies zu erreichen, fügen Sie einfach den folgenden Eintrag zum `c:\myteam\Nuget.Config`.

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

In diesem Beispiel wird die freigegebene `Nuget.Config` Datei gibt einen freigegebenen Paketordner für jedes Projekt, das unter C:\myteam, unabhängig von der Tiefe erstellt wird. Beachten Sie, wenn Sie einen vorhandenen Ordner "Pakete" unterhalb der Lösung haben, müssen Sie es löschen, bevor NuGet Pakete am neuen Speicherort abgelegt werden.

## <a name="support-for-portable-libraries"></a>Unterstützung für Portable Bibliotheken
[Portable Bibliotheken](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) ist eine Funktion, die mit .NET 4, mit dem Sie zum Erstellen von Assemblys, die ohne Änderung auch in anderen Microsoft-Plattformen aus Versionen von.NET Framework für Silverlight, Windows Phone und Xbox sogar funktionieren können, eingeführt 360 (obwohl Sie zu diesem Zeitpunkt NuGet das Xbox portable Library-Ziel nicht unterstützt).  Durch das Erweitern der [Paket Konventionen](../create-packages/supporting-multiple-target-frameworks.md) für Framework-Versionen und Profile NuGet 2.1 unterstützt jetzt portable Bibliotheken aktivieren Sie zum Erstellen von Paketen, die zusammengesetzte Framework und profilziels haben `lib` Ordner.

Beispielsweise sollten Sie die folgenden portablen Bibliothek verfügbaren Zielplattformen.

![Dialogfeld zum Erstellen einer portablen Bibliothek](./media/releasenotes-21-plib.png)

Nach der Erstellung der Bibliotheks und der Befehl `nuget.exe pack MyPortableProject.csproj` ausgeführt wird, wird das neue Portable Bibliothek Paketordnerstruktur kann anzeigen, indem Sie den Inhalt der generierten NuGet-Pakets untersuchen.

![Portable Library-Paketlayouts](./media/releasenotes-21-plib-layout.png)

Wie Sie sehen können, portable Bibliothek Ordner Namenskonvention erfolgt nach dem Muster "portable-{Framework 1} + {Framework n}" folgen, in dem die Framework-Bezeichner der vorhandenen [Framework Name und Version Konventionen](../reference/target-frameworks.md). Eine Ausnahme zu den Name und Version Konventionen in der Framework-Bezeichner verwendet, die für Windows Phone gefunden.  Diesen Moniker sollten der FrameworkName "wp" (wp7, wp71 oder wp8) verwenden. Verwendung von "Silverlight-wp7" führt z. B. zu einem Fehler.

Wenn das Paket installieren, das aus dieser Ordnerstruktur erstellt wird, kann NuGet jetzt ihren Regeln Framework und das Profil auf mehrere Ziele, entsprechend den Angaben in den Namen des Ordners anwenden.  Ist Sie hinter Abgleichsregeln NuGet das Prinzip, dass "spezifischere" Ziele "weniger spezifischen" Vorrang werden.  Dies bedeutet, dass Moniker, der eine bestimmte Plattform abzielt immer bevorzugte portable überlagert werden, wenn sie sowohl mit einem Projekt kompatibel sind.  Wenn mehrere portable Ziele mit einem Projekt kompatibel sind, wird NuGet darüber hinaus die bevorzugen, in dem der Satz von unterstützten Plattformen für das Projekt verweisen auf das Paket "nächstgelegenen" ist.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Zielgruppenadressierung für Windows 8 und Windows Phone 8-Projekte
Zusätzlich zum Hinzufügen von Unterstützung für portable Library-Projekte abzielen, bietet NuGet 2.1 für Windows 8-Store und Windows Phone 8-Projekte sowie einige neue allgemeine Moniker für Windows Store und Windows Phone-Projekte, die neue frameworkMoniker einfacher zu verwalten, in zukünftigen Versionen der jeweiligen Plattformen.

Suchen die Bezeichner für Windows 8 Store-Anwendungen wie folgt:

|NuGet 2.0 und früheren Versionen|NuGet 2.1|
|----------------|-----------|
|winRT45, .NETCore45|Windows, Windows8, win, win8|

<br/>
Suchen die Bezeichner für Windows Phone-Projekte wie folgt:

|Phone-Betriebssystem|NuGet 2.0 und früheren Versionen|NuGet 2.1
|----------------|-----------|-----------|
|Windows Phone 7|silverlight3 wp|wp, wp7, WindowsPhone, WindowsPhone7|
|Windows Phone 7.5 (Mango)|silverilght4-wp71|wp71, WindowsPhone71|
|Windows Phone 8|(nicht unterstützt)|wp8, WindowsPhone8|
<br/>
In allen den oben beschriebenen Änderungen weiterhin die alten Framework Namen von NuGet 2.1 vollständig unterstützt werden müssen.  Hostdaten, sollte die neuen Namen verwendet werden, wie sie stabiler und ausgereifter für zukünftige Versionen von der jeweiligen Plattformen werden. Werden von die neuen Namen *nicht* werden in den Vorgängerversionen von NuGet 2.1 unterstützt, jedoch so planen Sie entsprechend für den Fall zu wechseln.

## <a name="improved-search-in-package-manager-dialog"></a>Verbesserte Suchvorgänge im Dialogfeld "Paket-Manager"
Über die letzten mehrere Iterationen wurden Änderungen in der NuGet Gallery eingeführt, die die Geschwindigkeit und die Relevanz der Paket-Suchvorgänge wesentlich verbessert.  Diese Verbesserungen wurden jedoch auf der Website nuget.org beschränkt.  NuGet-2.1 stellt die verbesserte Suchvorgänge, die auftreten, die über das Dialogfeld "NuGet-Paket-Manager" zur Verfügung.  Angenommen Sie, beispielsweise, dass Sie das Windows Azure Caching Preview-Paket suchen möchten.  Eine sinnvolle Suchabfrage für dieses Paket möglicherweise "Azure-Cache".  In früheren Versionen von das Dialogfeld "Paket-Manager" würde das gewünschte Paket selbst nicht auf der ersten Seite der Ergebnisse aufgelistet.  Allerdings wird in NuGet 2.1, das gewünschte Paket jetzt am Anfang der Suchergebnisse.

![Paket-Manager-Dialogfeld Suchen](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Erzwingen Sie die Paketaktualisierung
Vor dem NuGet-2.1 würde NuGet überspringen, aktualisieren ein Paket aus, wenn es kein wurde eine hohe Versionsnummer.  Dies führte Unstimmigkeiten für bestimmte Szenarien – insbesondere im Fall von Build oder CI-Szenarien, in denen das Team nicht die Paketversion Anzahl für jeden Build zu erhöhen möchten.  Das gewünschte Verhalten wurde ein Update unabhängig erzwingen.  NuGet-2.1 wird dies mit dem Flag "installieren" behandelt.  Vorgängerversionen von NuGet würde z. B. in der folgenden führen, beim Versuch, ein Paket zu aktualisieren, die nicht über eine neuere Paketversion verfügt:

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

Mit dem Flag "installieren" des Pakets aktualisiert werden wird, unabhängig davon, ob eine neuere Version verfügbar ist.

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

Ein weiteres Szenario, in denen das Flag Reinstall vorteilhaft beweist, entspricht der Framework-Zielversion. Wenn Sie ändern das Zielframework des Projekts (z. B. von .NET 4, .NET 4.5), Update-Paket-installieren können aktualisieren Sie Verweise auf die korrekten Assemblys für alle NuGet-Pakete im Projekt installiert.

## <a name="edit-package-sources-within-visual-studio"></a>Bearbeiten Sie die Paketquellen innerhalb von Visual Studio
Aktualisieren eine Paketquelle von innerhalb der Visual Studio-Optionsdialogfeld erforderlich, löschen und erneuten Hinzufügen der Paketquelle in früheren Versionen von NuGet.  NuGet 2.1 verbessert dieses Workflows durch die Unterstützung von Update als erstklassige Funktion der Konfigurationsbenutzeroberfläche an.

![Dialogfeld "Konfiguration" der Paket-manager](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Fehlerkorrekturen
NuGet-2.1 enthält zahlreiche Programmfehlerbehebungen. Eine vollständige Liste der Arbeit Artikel feste in NuGet 2.0 Bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
