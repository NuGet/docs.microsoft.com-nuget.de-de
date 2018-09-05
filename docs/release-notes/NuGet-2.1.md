---
title: Anmerkungen zu NuGet-Version 2.1
description: Anmerkungen zu NuGet 2.1, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fd6dadc7968991c77c1b06a6a261415355b2fd73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548596"
---
# <a name="nuget-21-release-notes"></a>Anmerkungen zu NuGet-Version 2.1

[Anmerkungen zu NuGet 2.0](../release-notes/nuget-2.0.md) | [Anmerkungen zu NuGet 2.2](../release-notes/nuget-2.2.md)

NuGet 2.1 wurde am 4. Oktober 2012 veröffentlicht.

## <a name="hierarchical-nugetconfig"></a>Hierarchische "NuGet.config"

NuGet 2.1 bietet Ihnen mehr Flexibilität bei der Steuerung von NuGet-Einstellungen über das Durchlaufen der Ordnerstruktur, die für die Suche rekursiv `NuGet.Config` Dateien und anschließend die Konfiguration aus dem Satz aller gefundenen Dateien erstellen.  Beispielsweise sollten Sie das Szenario, in denen ein Team eine interne paketrepository für CI-Builds von anderen internen Abhängigkeiten verfügt. Die Ordnerstruktur für ein einzelnes Projekt könnte folgendermaßen aussehen:

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

Wenn die paketwiederherstellung für die Lösung aktiviert ist, sind darüber hinaus auch der folgende Ordner vorhanden:

    C:\myteam\solution1\.nuget

Wir können erstellen Sie eine neue Datei "NuGet.config"-Datei und platzieren Sie es im Ordner "c:\myteam", um das Repository des Teams interner Paket für alle Projekte verfügbar, die auf das Team arbeitet, und nicht auf dem Computer für jedes Projekt verfügbar gemacht. Es gibt keine Möglichkeit zu angeben einer Paketordner pro Projekt.

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

Wir können sehen, dass die Quelle hinzugefügt wurde, mithilfe des "Quellen" nuget.exe "-Befehls aus einem beliebigen Ordner unter c:\myteam wie unten dargestellt:

![Paketquellen aus der übergeordneten Nuget-Konfiguration](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` Dateien werden in der folgenden Reihenfolge gesucht:

1. `.nuget\Nuget.Config`
2. Rekursive Durchlaufen von Projektordner zum Stamm
3. Globale `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)

Die Konfigurationen sind in angewendet der *Reihenfolge umkehren*, d. h., die auf die oben genannten Reihenfolge basieren, der globalen Datei "NuGet.config" würde werden zuerst angewendet, gefolgt von den ermittelten Nuget.Config-Dateien vom Stamm zum Projektordner, gefolgt durch `.nuget\Nuget.Config`.  Dies ist besonders wichtig, wenn Sie verwenden die `<clear/>` Elements, das einen Satz von Elementen aus der Konfiguration entfernt.

## <a name="specify-packages-folder-location"></a>Geben Sie "Pakete" Speicherort des Ordners

In der Vergangenheit hat NuGet Pakete mit einer Lösung aus einem bekannten "Pakete" Ordner finden Sie unter den Stammordner der Lösung verwaltet.  Für Entwicklungsteams mit vielen verschiedenen Lösungen, die NuGet-Pakete installiert haben, kann dies im selben Paket installiert wird, an vielen verschiedenen Speicherorten im Dateisystem führen.

NuGet 2.1 verfügt über eine feiner abgestufte Kontrolle über den Speicherort des Paketordners "über die `repositoryPath` Element in der `NuGet.Config` Datei.  Erstellen von auf dem vorherigen Beispiel hierarchische "NuGet.config" nicht unterstützt, wird davon ausgegangen, dass wir alle Projekte unter C:\myteam\ Freigabe der gleichen Paketordner enthalten sein sollen.  Zu diesem Zweck fügen Sie einfach den folgenden Eintrag zum `c:\myteam\Nuget.Config`.

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

In diesem Beispiel ist der gemeinsam verwendeten `Nuget.Config` Datei gibt einen freigegebenen Paketordner für jedes Projekt, das unter C:\myteam, unabhängig von der Tiefe erstellt wird. Beachten Sie, dass wenn Sie einen vorhandenen Ordner "Pakete" unter Ihrem Projektmappenstamms haben, müssen Sie gelöscht werden, bevor Sie NuGet Pakete am neuen Speicherort abgelegt werden.

## <a name="support-for-portable-libraries"></a>Unterstützung für Portable Bibliotheken

[Portable Bibliotheken](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) ist ein Feature eingeführt, mit .NET 4, mit der Sie zum Erstellen von Assemblys, die ohne Änderung auf andere Microsoft-Plattformen und Versionen von.NET Framework, Silverlight, Windows Phone und sogar Xbox verwenden können, 360 (auch wenn Sie zu diesem Zeitpunkt NuGet das Ziel der Xbox-portablen Bibliothek nicht unterstützt).  Durch die Erweiterung der [Paket Konventionen](../create-packages/supporting-multiple-target-frameworks.md) für Framework-Versionen und Profile NuGet 2.1 unterstützt jetzt portable Bibliotheken aktivieren Sie zum Erstellen von Paketen, die zusammengesetzte Framework und profilziels `lib` Ordner.

Betrachten Sie beispielsweise die folgende portablen Bibliothek verfügbar für Plattformen aus.

![Dialogfeld zur tresorerstellung Portable Bibliothek](./media/releasenotes-21-plib.png)

Nach der Erstellung der Bibliotheks und der Befehl `nuget.exe pack MyPortableProject.csproj` ausgeführt wird, wird das neue Portable Library-Paket-Ordnerstruktur finden Sie im Inhalt des generierten NuGet-Pakets.

![Portable Bibliothek paketlayout](./media/releasenotes-21-plib-layout.png)

Wie Sie sehen können, der portablen Bibliothek Ordner Namenskonvention erfolgt nach dem Muster "portable {Framework - 1} + {Framework n}" folgen, in denen die frameworkbezeichner der vorhandenen [Framework Name und Version Konventionen](../reference/target-frameworks.md). Eine Ausnahme aus, um die Konventionen für Name und Version befindet sich in der frameworkbezeichner, die für Windows Phone verwendet.  Diesem Moniker befindet, sollten den Namen des "wp" ("wp7", "wp71" oder "wp8") verwenden. Mithilfe von "Silverlight-wp7" führt beispielsweise zu einem Fehler.

Bei der Installation des Pakets, das von dieser Ordnerstruktur erstellt wird, kann NuGet nun seine Regeln Framework und das Profil auf mehrere Ziele, wie in den Namen des Ordners angegeben anwenden.  Hinter der NuGet Abgleichsregeln geht es darum, "spezielle" Ziele "weniger spezifischen" ab Vorrang hat.  Dies bedeutet, dass es sich bei Moniker, die unterschiedlichen Plattformen immer bevorzugt gegenüber portable Versionen ist, wenn sie sowohl mit einem Projekt kompatibel sind.  Wenn mehrere portable Ziele mit einem Projekt kompatibel sind, wird NuGet darüber hinaus die bevorzugen, in denen die verschiedenen unterstützten Plattformen "nächstgelegene" auf das Projekt verweisen auf das Paket ist.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Für die Zielgruppenadressierung für Windows 8 und Windows Phone 8-Projekten

Zusätzlich zum Hinzufügen von Unterstützung für die Zielgruppenadressierung von portable Library-Projekten, bietet NuGet 2.1 neue frameworkMoniker für sowohl Windows 8 Store und Windows Phone 8-Projekte als auch für Windows Store und Windows Phone-Projekte, die einige neue allgemeine-Moniker einfacher in zukünftigen Versionen der jeweiligen Plattformen zu verwalten.

Für Windows 8 Store-Anwendungen wird die Bezeichner wie folgt aussehen:

| NuGet 2.0 und früheren Versionen | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45, .NETCore45 | Windows, Windows8, win, win8 |

<br/>
Für Windows Phone-Projekte wird die Bezeichner wie folgt aussehen:

| Phone-Betriebssystem | NuGet 2.0 und früheren Versionen | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3-wp- | wp, wp7, WindowsPhone, WindowsPhone7 |
| Windows Phone 7.5 (Mango) | silverlight4-wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (nicht unterstützt) | wp8, WindowsPhone8 |

<br/>
In allen oben beschriebenen Änderungen weiterhin die alten Frameworknamen von NuGet 2.1 vollständig unterstützt werden müssen.  Zukunft sollte die neuen Namen verwendet werden, wie sie stabilere in zukünftigen Versionen der jeweiligen Plattformen werden. Werden von die neuen Namen *nicht* werden im NuGet-Versionen vor 2.1 unterstützt, jedoch so planen Sie entsprechend für die Ausführung umstellen.

## <a name="improved-search-in-package-manager-dialog"></a>Verbesserte Suche im Dialogfeld "Paket-Manager"

Über die letzten mehrere Iterationen wurden Änderungen an den NuGet-Katalog eingeführt, die die Geschwindigkeit und die Relevanz der Paket-Suchvorgänge wesentlich verbessert.  Allerdings konnten diese Verbesserungen der nuget.org-Website.  NuGet 2.1 stellt der verbesserten Suchfunktion auftreten, die über das Dialogfeld "NuGet-Paket-Manager" zur Verfügung.  Stellen Sie sich beispielsweise vor, Sie das Paket für Windows Azure Caching (Vorschau) finden möchten.  Eine angemessene Suchabfrage für dieses Paket möglicherweise "Azure-Cache".  In früheren Versionen des Dialogfelds "Paket-Manager" wird das gewünschte Paket noch nicht auf der ersten Seite der Ergebnisse aufgelistet.  Allerdings wird in NuGet 2.1, das gewünschte Paket jetzt am oberen Rand der Ergebnisse.

![Paket-Manager-Dialogfeld Suchen](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Paketupdate erzwingen

Vor NuGet 2.1, würde NuGet überspringen, aktualisieren ein Paket aus, wenn es keine wurde hohen Versionsnummer.  Dies führte Reibung für bestimmte Szenarien – insbesondere im Fall von Build oder CI-Szenarien, in denen das Team nicht wollten die Anzahl für jeden Build Paketversion inkrementiert werden soll.  Das gewünschte Verhalten bestand darin, unabhängig davon, eine Aktualisierung zu erzwingen.  NuGet 2.1 wird dies mit dem Flag "installieren" behandelt.  Beispielsweise würde die frühere Versionen von NuGet in der folgenden führen, beim Versuch, ein Paket zu aktualisieren, die nicht mit eine neuere Paketversion verfügt:

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

Mit dem Flag neu installieren, die das Paket aktualisiert werden, unabhängig davon, ob eine neuere Version vorhanden ist.

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

Ein weiteres Szenario, in denen das Flag für die Neuinstallation nützlich erweist sich als, entspricht der neuzuweisung der Framework. Wenn Sie das Zielframework eines Projekts (z. B. von .NET 4, .NET 4.5), Update-Package-erneut installieren können Verweise auf die richtigen Assemblys für alle im Projekt installierten NuGet-Pakete aktualisieren.

## <a name="edit-package-sources-within-visual-studio"></a>Bearbeiten Sie die Paketquellen in Visual Studio

In früheren Versionen von NuGet aktualisieren eine Paketquelle von innerhalb der Visual Studio-Optionsdialogfeld erforderlich sind, löschen und erneuten Hinzufügen der Paketquelle.  NuGet 2.1 verbessert dieses Workflows durch die Unterstützung von Update als erster Klasse Funktion Teile der Benutzeroberfläche für die Konfiguration an.

![Dialogfeld "Konfiguration" der Paket-manager](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Fehlerkorrekturen

NuGet 2.1 enthält zahlreiche Programmfehlerbehebungen. Eine vollständige Liste der Arbeit Elemente eine feste in NuGet 2.0 Bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
