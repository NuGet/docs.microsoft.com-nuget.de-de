---
title: Anmerkungen zu NuGet-Version 1.5
description: Anmerkungen zu NuGet 1.5, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c2b549f65e675e5fde9ae1dfea3f44f7d691a86b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548724"
---
# <a name="nuget-15-release-notes"></a>Anmerkungen zu NuGet-Version 1.5

[Anmerkungen zu NuGet 1.4](../release-notes/nuget-1.4.md) | [Anmerkungen zu NuGet 1.6](../release-notes/nuget-1.6.md)

NuGet 1.5 wurde am 30. August 2011 veröffentlicht.

## <a name="features"></a>Features

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Projektvorlagen vorinstallierte NuGet-Pakete
Wenn Sie eine neue ASP.NET MVC 3-Projektvorlage erstellen, werden die jQuery-Skriptbibliotheken, die im Projekt enthaltenen tatsächlich dort platziert, durch die Installation von NuGet-Pakete.

Die ASP.NET MVC 3-Projektvorlage enthält einen Satz von NuGet-Pakete, die installiert werden, wenn die Projektvorlage aus aufgerufen wird. Diese Fähigkeit zum Einschließen von NuGet-Pakete mit einer Projektvorlage ist jetzt ein Feature von NuGet, _alle_ Projektvorlage kann jetzt nutzen.

Weitere Informationen zu diesem Feature finden Sie in diesem [Blogbeitrag vom Entwickler des Features](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Explizite Assemblyverweise

Einen neuen `<references />` Element, das verwendet wird, explizit angeben, welche Assemblys in der das Paket verwiesen werden soll.

Angenommen, Sie Folgendes hinzufügen:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Nur die `xunit.dll` und `xunit.extensions.dll` in den entsprechenden verwiesen [Frameworkprofil/Unterordner](../reference/nuspec.md#explicit-assembly-references) von der `lib` Ordner, auch wenn es andere Assemblys im Ordner.

Wenn dieses Element ist nicht angegeben, wird das übliche Verhalten, die bezieht auf jede Assembly in den `lib` Ordner.

__Was wird für dieses Feature verwendet?__

Dieses Feature unterstützt nur die Assemblys zur Entwurfszeit. Beispielsweise müssen bei der Verwendung von Codeverträgen die Vertragsassemblys neben den runtimeassemblys sein, die sie erweitern, damit Visual Studio sie finden jedoch die Vertragsassemblys sollte nicht tatsächlich vom Projekt verwiesen werden, und in nicht kopiert werden sollen die `bin` Ordner.

Ebenso kann das Feature für Komponententestframeworks wie XUnit die benötigen die Tools-Assemblys werden neben den runtimeassemblys befinden, aber von der Projekt-verweisen ausgeschlossen, verwendet werden.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Neue Möglichkeit zum Ausschließen von Dateien in der NuSpec
Die `<file>` Element innerhalb einer `.nuspec` Datei kann verwendet werden, um eine bestimmte Datei oder einen Satz von Dateien, die mit einem Platzhalter enthalten. Wenn Sie einen Platzhalter zu verwenden, besteht keine Möglichkeit, eine bestimmte Teilmenge der in Ihr enthaltenen Dateien ausschließen. Nehmen wir beispielsweise an, dass Sie möchten, dass alle Textdateien in einem Ordner mit Ausnahme einer bestimmten.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

Verwenden Sie Semikolons, um mehrere Dateien anzugeben.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

Oder verwenden Sie einen Platzhalter, um einen Satz von Dateien, z. B. alle Sicherungsdateien ausschließen

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Entfernen von Paketen mithilfe des Dialogfelds aufgefordert, Abhängigkeiten zu entfernen
Bei der Deinstallation eines Pakets mit Abhängigkeiten von NuGet aufgefordert werden, sodass das Entfernen eines Pakets Abhängigkeiten zusammen mit dem Paket.

![Entfernen die abhängigen Pakete](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` Befehl zur Verbesserung der
Die `Get-Package` Befehl unterstützt jetzt eine `-ProjectName` Parameter. Also den Befehl

    Get-Package –ProjectName A

Listet alle Pakete im Projekt a installiert

### <a name="support-for-proxies-that-require-authentication"></a>Unterstützung von Proxys, für die Authentifizierung erforderlich
Wenn Sie NuGet hinter einem Proxy verwenden zu können, die eine Authentifizierung erforderlich ist, fordert NuGet nun Proxyanmeldeinformationen. Eingeben von Anmeldeinformationen können NuGet, um die Verbindung mit des remote-Repositorys.

### <a name="support-for-repositories-that-require-authentication"></a>Unterstützung für Repositorys, die Authentifizierung erforderlich ist
NuGet unterstützt jetzt die Verbindung mit [private Repositorys](../hosting-packages/local-feeds.md) , Basic oder NTLM-Authentifizierung erfordern.

Unterstützung für Digest-Authentifizierung wird in einer zukünftigen Version hinzugefügt werden.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Leistungsverbesserungen für das nuget.org-repository
Wir haben mehrere leistungsverbesserungen auf der NuGet-Katalog zum Paket, auflisten und Durchsuchen schneller werden vorgenommen.

### <a name="solution-dialog-project-filtering"></a>Dialogfeld Projekt lösungsfilterung
Auf Projektmappenebene im Dialogfeld bei für welche Projekte zu installieren erläutert, nur Projekte, die mit dem ausgewählten Paket kompatibel sind.

### <a name="package-release-notes"></a>Anmerkungen zur Version des Pakets
NuGet-Pakete umfassen jetzt Unterstützung für Anmerkungen zu dieser Version. Die Anmerkungen zu dieser Version nur Sie beim Anzeigen von _Updates_ für ein Paket, sodass es nicht sinnvoll So fügen sie dem ersten Release hinzu.

![Anmerkungen zu dieser Version in der Registerkarte "Updates"](./media/manage-nuget-packages-release-notes.png)

Um die Anmerkungen zu dieser Version eines Pakets hinzugefügt haben, verwenden Sie die neue `<releaseNotes />` Metadata-Element in der NuSpec-Datei.

### <a name="nuspec-ltfiles-gt-improvement"></a>NuSpec & Ltfiles /&gt; zur Verbesserung der
Die `.nuspec` -Datei können nun leere `<files />` -Element, das weist nuget.exe nicht auf eine beliebige Datei im Paket enthalten.

## <a name="bug-fixes"></a>Fehlerkorrekturen
NuGet 1.5 mussten insgesamt 107 Arbeitsaufgaben behoben. 103 davon waren als Fehler gekennzeichnet.

Eine vollständige Liste der Arbeit Elemente eine feste in NuGet 1.5, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Fehlerbehebungen zu beachten:

* [Problem 1273](http://nuget.codeplex.com/workitem/1273): vorgenommen `packages.config` Weitere Versionskontrolle benutzerfreundliche durch Pakete alphabetisch zu sortieren und Entfernen von zusätzlichen Leerzeichen.
* [Problem 844](http://nuget.codeplex.com/workitem/844): Versionsnummern werden jetzt normalisiert, damit `Install-Package 1.0` funktioniert für ein Paket mit der Version `1.0.0`.
* [Problem 1060](http://nuget.codeplex.com/workitem/1060): beim Erstellen eines Pakets mithilfe von nuget.exe, die `-Version` flag Außerkraftsetzungen der `<version />` Element.
