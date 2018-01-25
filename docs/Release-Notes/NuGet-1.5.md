---
title: Anmerkungen zur Version des NuGet-1.5 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 1.5 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-1.5 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 261cfbbd262bad28f142b0c3dff8a541641d9fda
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-15-release-notes"></a>1.5 NuGet-Versionshinweise

[Anmerkungen zur Version von NuGet 1.4](../release-notes/nuget-1.4.md) | [NuGet 1.6-Versionshinweise](../release-notes/nuget-1.6.md)

NuGet-1.5 wurde am 30. August 2011 veröffentlicht.

## <a name="features"></a>Features

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Projektvorlagen mit vorinstallierte NuGet-Pakete
Wenn Sie eine neue ASP.NET MVC 3-Projektvorlage erstellen, sind die im Projekt enthaltenen jQuery-Skriptbibliotheken tatsächlich dort platziert, durch die Installation von NuGet-Pakete.

Die ASP.NET MVC 3-Projektvorlage enthält eine Reihe von NuGet-Pakete installiert, wenn die Projektvorlage aufgerufen wird. Diese Fähigkeit zum Einschließen von NuGet-Pakete mit einer Projektvorlage ist jetzt ein Feature von NuGet, _alle_ Projektvorlage kann jetzt nutzen.

Weitere Informationen zu diesem Feature finden Sie diese [Blogbeitrag vom Entwickler der Funktion](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Explizite Assemblyverweise

Ein neues hinzugefügt `<references />` , das verwendet wird, explizit angeben, welche Assemblys in der das Paket verwiesen werden soll.

Angenommen, Sie Folgendes hinzufügen:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Dann nur die `xunit.dll` und `xunit.extensions.dll` erfolgt der Verweis in den entsprechenden [Frameworkprofil/Unterordner](../schema/nuspec.md#explicit-assembly-references) von der `lib` Ordner selbst wenn andere Assemblys in den Ordner vorhanden sind.

Wenn dieses Element nicht angegeben ist, und klicken Sie dann das übliche Verhalten gilt, dies ist zum Verweisen auf jede Assembly in den `lib` Ordner.

__Was ist für diese Funktion verwendet?__

Diese Funktion unterstützt nur die Assemblys zur Entwurfszeit. Beispielsweise müssen bei Verwendung von Codeverträgen Vertragsassemblys neben den Runtime-Assemblys werden, die sie erhöhen, damit Visual Studio sie finden jedoch den Vertragsassemblys sollten nicht tatsächlich vom Projekt verwiesen werden und nicht in kopiert werden sollen die `bin` Ordner.

Ebenso kann die Funktion für Komponententest-Frameworks wie z. B. XUnit, bedürfen der Assemblys Tools befindet sich neben der Laufzeitassemblys, aber die Projektverweise ausgeschlossen werden, verwendet werden.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Die Möglichkeit zum Ausschließen von Dateien in den .nuspec hinzugefügt
Die `<file>` Element innerhalb einer `.nuspec` Datei kann verwendet werden, um eine bestimmte Datei oder einen Satz von Dateien, die mit einem Platzhalterzeichen enthalten. Wenn Sie einen Platzhalter verwenden, besteht keine Möglichkeit, eine bestimmte Teilmenge der in Ihr enthaltenen Dateien ausschließen. Angenommen Sie, dass alle Textdateien in einem Ordner mit Ausnahme einer bestimmten werden soll.

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

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Entfernen von Paketen, die mit dem Dialogfeld werden Sie aufgefordert, Abhängigkeiten zu entfernen
Wenn ein Paket mit Abhängigkeiten, NuGet aufgefordert werden, sodass das Entfernen eines Pakets Abhängigkeiten zusammen mit dem Paket wird deinstalliert.

![Entfernen von abhängigen Pakete](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package`Befehl zur Verbesserung der
Die `Get-Package` Befehl unterstützt jetzt einen `-ProjectName` Parameter. Daher den Befehl

    Get-Package –ProjectName A

Listet alle Pakete im Projekt A. installiert

### <a name="support-for-proxies-that-require-authentication"></a>Unterstützung für Proxys, die eine Authentifizierung erfordern
Wenn Sie NuGet hinter einem Proxy verwenden, die eine Authentifizierung erforderlich ist, fordert NuGet jetzt zur Proxy-Anmeldeinformationen. Ermöglicht das Eingeben von Anmeldeinformationen NuGet zur Verbindung mit des remote-Repositorys.

### <a name="support-for-repositories-that-require-authentication"></a>Unterstützung für Repositorys, die eine Authentifizierung erfordern
NuGet unterstützt jetzt die Herstellen einer Verbindung mit [private Repositorys](../hosting-packages/local-feeds.md) , Standard- oder NTLM-Authentifizierung erfordern.

Unterstützung für die Digestauthentifizierung werden in einer zukünftigen Version hinzugefügt werden.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Leistungsverbesserungen der nuget.org-Repository
Wir haben mehrere leistungsverbesserungen an den Katalog nuget.org Paket auflisten, und suchen schneller zu vorgenommen.

### <a name="solution-dialog-project-filtering"></a>Filtern von Projektmappen Dialogfeld Projekt
Im Dialogfeld Projektmappen auf Dokumentebene, wenn aufgefordert werden, für welche Projekte zu installieren zeigen wir nur Projekte, die mit dem ausgewählten Paket kompatibel sind.

### <a name="package-release-notes"></a>Paket-Versionshinweise
NuGet-Pakete umfassen jetzt Unterstützung für Anmerkungen zu dieser Version. Die Anmerkungen zu dieser Version nur Sie beim Anzeigen von _Updates_ für ein Paket, sodass es nicht sinnvoll sie Ihre erste Version hinzugefügt.

![Anmerkungen zu dieser Version in der Registerkarte "Updates"](./media/manage-nuget-packages-release-notes.png)

Um ein Paket Anmerkungen zu dieser Version hinzugefügt haben, verwenden Sie die neue `<releaseNotes />` Metadatenelement in die NuSpec-Datei.

### <a name="nuspec-ltfiles-gt-improvement"></a>.NuSpec & Ltfiles /&gt; zur Verbesserung der
Die `.nuspec` Datei ermöglicht jetzt leer `<files />` -Element, das weist nuget.exe jede Datei im Paket einschließen möchten.

## <a name="bug-fixes"></a>Fehlerkorrekturen
NuGet-1.5 mussten insgesamt 107 Arbeitsaufgaben behoben. 103 dieser wurden als Fehler gekennzeichnet.

Eine vollständige Liste der Arbeit Elemente in behoben NuGet 1.5, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Fehlerkorrekturen Folgendes zu beachten:

* [Problem 1273](http://nuget.codeplex.com/workitem/1273): vorgenommen `packages.config` Weitere Versionskontrolle angezeigten durch Pakete alphabetisch zu sortieren und Entfernen von zusätzlichen Leerzeichen.
* [Problem 844](http://nuget.codeplex.com/workitem/844): Versionsnummern werden jetzt normalisiert, damit `Install-Package 1.0` funktioniert für ein Paket mit der Version `1.0.0`.
* [Problem 1060](http://nuget.codeplex.com/workitem/1060): beim Erstellen eines Pakets nuget.exe, mit der `-Version` flag überschreibt die `<version />` Element.
