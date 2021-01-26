---
title: Anmerkungen zu dieser Version von nuget 2,1
description: Anmerkungen zu dieser Version von nuget 2,1 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777022"
---
# <a name="nuget-21-release-notes"></a>Anmerkungen zu dieser Version von nuget 2,1

Anmerkungen zu dieser [Version von nuget 2,0](../release-notes/nuget-2.0.md)  |  [Anmerkungen zu dieser Version von nuget 2,2](../release-notes/nuget-2.2.md)

Nuget 2,1 wurde am 4. Oktober 2012 veröffentlicht.

## <a name="hierarchical-nugetconfig"></a>Hierarchische Nuget.Config

Mit nuget 2,1 können Sie die nuget-Einstellungen flexibler steuern, indem Sie die Ordnerstruktur rekursiv durchlaufen, um nach Dateien zu suchen, `NuGet.Config` und dann die Konfiguration aus dem Satz aller gefundenen Dateien aufbauen.  Sehen Sie sich als Beispiel das Szenario an, in dem ein Team über ein internes Paketrepository für CI-Builds anderer interner Abhängigkeiten verfügt. Die Ordnerstruktur für ein einzelnes Projekt könnte wie folgt aussehen:

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

Wenn die Paket Wiederherstellung für die Lösung aktiviert ist, ist außerdem der folgende Ordner vorhanden:

```
C:\myteam\solution1\.nuget
```

Um das interne Paketrepository des Teams für alle Projekte verfügbar zu machen, an denen das Team arbeitet, ohne es für jedes Projekt auf dem Computer verfügbar zu machen, können wir eine neue Nuget.Config Datei erstellen und Sie im Ordner c:\myteam platzieren. Es gibt keine Möglichkeit, einen Paket Ordner pro Projekt zu spezifippen.

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

Nun können Sie sehen, dass die Quelle hinzugefügt wurde, indem Sie den Befehl "nuget.exe Sources" in einem beliebigen Ordner unterhalb von "c:\myteam" ausführen, wie unten dargestellt:

![Paketquellen aus übergeordneter nuget-Konfiguration](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` Dateien werden in der folgenden Reihenfolge gesucht:

1. `.nuget\Nuget.Config`
2. Rekursiv durchlaufen vom Projektordner zum Stamm
3. Global `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )

Die Konfigurationen werden nicht in *umgekehrter Reihenfolge* angewendet, d. h., basierend auf der oben aufgeführten Reihenfolge werden die globalen Nuget.Config zuerst angewendet, gefolgt von den ermittelten Nuget.Config Dateien aus dem Stamm Ordner zum Projektordner, gefolgt von `.nuget\Nuget.Config` .  Dies ist besonders wichtig, wenn Sie das- `<clear/>` Element verwenden, um einen Satz von Elementen aus der Konfiguration zu entfernen.

## <a name="specify-packages-folder-location"></a>Speicherort für "Paket Ordner" angeben

In der Vergangenheit hat nuget die Pakete einer Projekt Mappe aus einem bekannten Ordner "Packages", der sich unter dem Stamm Ordner der Projekt Mappe befindet, verwaltet.  Für Entwicklungsteams, die über viele verschiedene Lösungen verfügen, für die nuget-Pakete installiert sind, kann dies dazu führen, dass das gleiche Paket an vielen unterschiedlichen Stellen im Dateisystem installiert wird.

Nuget 2,1 bietet eine präzisetere Kontrolle über den Speicherort des Paket Ordners über das- `repositoryPath` Element in der `NuGet.Config` Datei.  Wenn Sie auf dem vorherigen Beispiel der Unterstützung für hierarchische Nuget.Config aufbauen, gehen wir davon aus, dass alle Projekte unter "c:\myteam\" denselben Paket Ordner aufweisen sollen.  Fügen Sie hierzu einfach den folgenden Eintrag in hinzu `c:\myteam\Nuget.Config` .

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

In diesem Beispiel `Nuget.Config` gibt die freigegebene Datei einen freigegebenen Paket Ordner für jedes Projekt an, das unter c:\myteam erstellt wird, und zwar unabhängig von der Tiefe. Beachten Sie Folgendes: Wenn Sie einen vorhandenen Paket Ordner unterhalb des Projektmappenstamms haben, müssen Sie ihn löschen, damit nuget Pakete am neuen Speicherort platziert.

## <a name="support-for-portable-libraries"></a>Unterstützung für Portable Bibliotheken

[Portable Bibliotheken](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) ist ein Feature, das erstmals mit .NET 4 eingeführt wurde und es Ihnen ermöglicht, Assemblys zu erstellen, die ohne Änderungen auf verschiedenen Microsoft-Plattformen funktionieren, von Versionen von The.NET Framework zu Silverlight bis hin zu Windows Phone und sogar Xbox 360 (aber derzeit unterstützt nuget nicht das Portable Xbox-Bibliotheks Ziel).  Durch die Erweiterung der [Paket Konventionen](../create-packages/supporting-multiple-target-frameworks.md) für Frameworkversionen und Profile unterstützt nuget 2,1 jetzt Portable Bibliotheken, da Sie Pakete erstellen können, die über Verbund Framework und Profil Ziel `lib` Ordner verfügen.

Sehen Sie sich als Beispiel die folgenden verfügbaren Zielplattformen der portablen Klassenbibliothek an.

![Dialogfeld zur Erstellung portabler Bibliotheken](./media/releasenotes-21-plib.png)

Nachdem die Bibliothek erstellt und der Befehl `nuget.exe pack MyPortableProject.csproj` ausgeführt wurde, kann die neue Portable Library-Paket Ordnerstruktur angezeigt werden, indem Sie den Inhalt des generierten nuget-Pakets untersuchen.

![Layout des portablen Bibliotheks Pakets](./media/releasenotes-21-plib-layout.png)

Wie Sie sehen können, folgt die Name-Konvention des portablen Bibliotheks Ordners dem Muster ' Portable-{Framework 1} + {Framework n} ', wobei die frameworkbezeichner den vorhandenen [frameworknamen und Versions Konventionen](../reference/target-frameworks.md)folgen. Eine Ausnahme des Namens und der Versions Konventionen finden Sie im frameworkbezeichner, der für die Windows Phone verwendet wird.  Dieser Moniker muss den frameworknamen "WP" (WP7, wp71 oder WP8) verwenden. Die Verwendung von "Silverlight-WP7" führt z. b. zu einem Fehler.

Bei der Installation des Pakets, das aus dieser Ordnerstruktur erstellt wird, kann nuget nun seine Framework-und Profil Regeln auf mehrere Ziele anwenden, wie im Ordnernamen angegeben.  Hinter den nuget-abgleichsregeln ist das Prinzip, dass "spezifischere" Ziele Vorrang vor "weniger spezifischen" Zielen haben.  Dies bedeutet, dass Moniker für eine bestimmte Plattform immer als Portable verwendet werden, wenn beide mit einem Projekt kompatibel sind.  Wenn darüber hinaus mehrere Portable Ziele mit einem Projekt kompatibel sind, bevorzugt nuget das, in dem die Gruppe der unterstützten Plattformen dem Projekt, das auf das Paket verweist, dem Projekt am nächsten liegt.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Ziel Projekte für Windows 8 und Windows Phone 8

Zusätzlich zum Hinzufügen von Unterstützung für Portable Bibliotheks Projekte bietet nuget 2,1 neue FrameworkMoniker für Windows 8 Store-und Windows Phone 8-Projekte sowie einige neue allgemeine Moniker für Windows Store-und Windows Phone Projekte, die in zukünftigen Versionen der jeweiligen Plattformen einfacher zu verwalten sind.

Für Windows 8-Store-Anwendungen sehen die Bezeichner wie folgt aus:

| Nuget 2,0 und früher | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45,. NETCore45 | Windows, Windows8, Win, win8 |

<br/>
Für Windows Phone Projekte sehen die Bezeichner wie folgt aus:

| Telefon Betriebssystem | Nuget 2,0 und früher | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3-WP | WP, WP7, windowsphone, WindowsPhone7 |
| Windows Phone 7,5 (Mango) | silverlight4-wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (Nicht unterstützt) | WP8, WindowsPhone8 |

<br/>
In allen oben aufgeführten Änderungen werden die alten frameworknamen weiterhin vollständig von nuget 2,1 unterstützt.  Wenn Sie fortfahren, sollten die neuen Namen verwendet werden, da Sie in zukünftigen Versionen der jeweiligen Plattformen stabiler werden. Die neuen Namen werden in Versionen von nuget vor 2,1 jedoch *nicht* unterstützt. Planen Sie daher entsprechend, wann der Schalter erfolgen soll.

## <a name="improved-search-in-package-manager-dialog"></a>Verbesserte Suche im Dialog Feld "Paket-Manager"

In den letzten mehreren Iterationen wurden Änderungen in den nuget-Katalog eingeführt, die die Geschwindigkeit und Relevanz von Paket Suchvorgängen erheblich verbessert haben.  Diese Verbesserungen waren jedoch auf die nuget.org-Website beschränkt.  Mit nuget 2,1 ist die verbesserte Suchfunktion über das Dialogfeld "nuget-Paket-Manager" verfügbar.  Stellen Sie sich beispielsweise vor, dass Sie das Windows Azure Caching-Vorschau Paket finden möchten.  Eine sinnvolle Suchabfrage für dieses Paket kann "Azure Cache" lauten.  In früheren Versionen des Dialog Felds "Paket-Manager" ist das gewünschte Paket nicht einmal auf der ersten Seite der Ergebnisse aufgeführt.  In nuget 2,1 wird das gewünschte Paket jetzt jedoch oben in den Suchergebnissen angezeigt.

![Dialogfeld Suche im Paket-Manager](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Paketaktualisierung erzwingen

Vor nuget 2,1 würde nuget das Aktualisieren eines Pakets überspringen, wenn keine hohe Versionsnummer vorhanden wäre.  Dies führte zu einer Reibung für bestimmte Szenarien – insbesondere im Fall von Build-oder CI-Szenarien, in denen das Team die Paket Versionsnummer nicht bei jedem Build erhöhen wollte.  Das gewünschte Verhalten war, eine Aktualisierung unabhängig zu erzwingen.  Nuget 2,1 adressiert dies mit dem Flag "REINSTALL".  Frühere Versionen von nuget würden beispielsweise Folgendes ergeben, wenn versucht wird, ein Paket zu aktualisieren, das nicht über eine neuere Paketversion verfügt:

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

Mit dem Flag für die Neuinstallation wird das Paket aktualisiert, unabhängig davon, ob eine neuere Version vorhanden ist.

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

Ein weiteres Szenario, in dem das neuinstallationsflag von Vorteil ist, besteht in der Neuausrichtung des Frameworks. Wenn Sie das Ziel Framework eines Projekts ändern (z. b. von .NET 4 zu .NET 4,5), können Update-Package-REINSTALL Verweise auf die richtigen Assemblys für alle im Projekt installierten nuget-Pakete aktualisieren.

## <a name="edit-package-sources-within-visual-studio"></a>Bearbeiten von Paketquellen in Visual Studio

In früheren Versionen von nuget erforderte das Aktualisieren einer Paketquelle über das Visual Studio-Options Dialogfeld das Löschen und erneute hinzufügen der Paketquelle.  Nuget 2,1 verbessert diesen Workflow, indem er Update als erste Klassen Funktion der Konfigurations Benutzeroberfläche unterstützt.

![Dialog](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Fehlerkorrekturen

Nuget 2,1 umfasst viele Fehlerbehebungen. Eine vollständige Liste der Arbeitselemente, die in nuget 2,0 behoben wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
