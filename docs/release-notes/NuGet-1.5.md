---
title: Anmerkungen zu dieser Version von nuget 1,5
description: Anmerkungen zu dieser Version von nuget 1,5 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c9946f3d8cf545ec14f842c40105743c231b4b72
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777088"
---
# <a name="nuget-15-release-notes"></a>Anmerkungen zu dieser Version von nuget 1,5

Anmerkungen zu dieser [Version von nuget 1,4](../release-notes/nuget-1.4.md)  |  [Anmerkungen zu dieser Version von nuget 1,6](../release-notes/nuget-1.6.md)

Nuget 1,5 wurde am 30. August 2011 veröffentlicht.

## <a name="features"></a>Features

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Projektvorlagen mit vorinstallierten nuget-Paketen
Beim Erstellen einer neuen ASP.NET MVC 3-Projektvorlage werden die im Projekt enthaltenen jQuery-Skript Bibliotheken tatsächlich durch die Installation von nuget-Paketen platziert.

Die ASP.NET MVC 3-Projektvorlage enthält einen Satz von nuget-Paketen, die installiert werden, wenn die Projektvorlage aufgerufen wird. Diese Möglichkeit, nuget-Pakete mit einer Projektvorlage aufzunehmen, ist jetzt eine Funktion von nuget, die _alle_ Projektvorlagen jetzt nutzen können.

Weitere Informationen zu diesem Feature finden Sie in diesem [Blogbeitrag vom Entwickler des Features](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Explizite Assemblyverweise

Es wurde ein neues Element hinzugefügt `<references />` , mit dem explizit angegeben wird, auf welche Assemblys im Paket verwiesen werden soll.

Wenn Sie z. b. Folgendes hinzufügen:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

`xunit.dll`Auf und wird nur `xunit.extensions.dll` aus dem entsprechenden [Framework/Profil-Unterordner](../reference/nuspec.md#explicit-assembly-references) des `lib` Ordners verwiesen, auch wenn im Ordner weitere Assemblys vorhanden sind.

Wenn dieses Element weggelassen wird, gilt das übliche Verhalten, das auf jede Assembly im `lib` Ordner verweist.

__Wofür wird dieses Feature verwendet?__

Diese Funktion unterstützt nur-Assemblys zur Entwurfszeit. Wenn Sie z. b. Code Verträge verwenden, müssen sich die Vertragsassemblys neben den ausführungsassemblys befinden, die Sie erweitern, sodass Sie von Visual Studio gefunden werden können, aber die Vertragsassemblys sollten nicht tatsächlich vom Projekt referenziert werden und sollten nicht in den Ordner kopiert werden `bin` .

Ebenso kann die-Funktion für Komponenten Test-Frameworks wie xUnit verwendet werden, deren toolsassemblys sich neben den Laufzeitassemblys befinden, aber von Projekt verweisen ausgeschlossen werden.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Hinzugefügte Fähigkeit zum Ausschließen von Dateien in der. nuspec-Datei
Das- `<file>` Element in einer- `.nuspec` Datei kann verwendet werden, um eine bestimmte Datei oder einen Satz von Dateien mithilfe eines Platzhalters einzuschließen. Wenn Sie einen Platzhalter verwenden, besteht keine Möglichkeit, eine bestimmte Teilmenge der enthaltenen Dateien auszuschließen. Angenommen, Sie möchten alle Textdateien in einem Ordner außer einem bestimmten Ordner.

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

Oder verwenden Sie eine Platzhalter Karte, um eine Gruppe von Dateien auszuschließen, z. b. alle Sicherungsdateien.

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Entfernen von Paketen mithilfe des Dialog Felds zum Entfernen von Abhängigkeiten
Wenn Sie ein Paket mit Abhängigkeiten deinstallieren, werden Sie von nuget aufgefordert, das Entfernen der Abhängigkeiten eines Pakets zusammen mit dem Paket zu ermöglichen.

![Entfernen von abhängigen Paketen](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` Befehls Verbesserung
Der- `Get-Package` Befehl unterstützt jetzt einen- `-ProjectName` Parameter. Der Befehl

```
Get-Package –ProjectName A
```

Listet alle Pakete auf, die in Project A installiert sind.

### <a name="support-for-proxies-that-require-authentication"></a>Unterstützung für Proxys, die Authentifizierung erfordern
Wenn Sie nuget hinter einem Proxy verwenden, der eine Authentifizierung erfordert, fordert nuget nun zur Eingabe von Proxy Anmelde Informationen auf. Durch Eingeben von Anmelde Informationen kann nuget eine Verbindung mit dem Remoterepository herstellen

### <a name="support-for-repositories-that-require-authentication"></a>Unterstützung für Depots, die eine Authentifizierung erfordern
Nuget unterstützt jetzt das Herstellen einer Verbindung mit [privaten Depots](../hosting-packages/local-feeds.md) , die eine Basic-oder NTLM-Authentifizierung erfordern

Die Unterstützung für die Digest-Authentifizierung wird in einer zukünftigen Version hinzugefügt.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Leistungsverbesserungen für das nuget.org-Repository
Wir haben eine Reihe von Leistungsverbesserungen an der nuget.org Gallery vorgenommen, um die Paket Auflistung zu beschleunigen und schneller zu suchen.

### <a name="solution-dialog-project-filtering"></a>Projekt Filterung für Projekt Mappe
Wenn Sie im Dialogfeld auf Projektmappenebene aufgefordert werden, die zu installierenden Projekte anzugeben, werden nur Projekte angezeigt, die mit dem ausgewählten Paket kompatibel sind.

### <a name="package-release-notes"></a>Anmerkungen zu dieser Paketversion
Nuget-Pakete enthalten jetzt Unterstützung für Versions Anmerkungen. Die Anmerkungen zu dieser Version werden nur angezeigt, wenn Sie _Updates_ für ein Paket anzeigen, daher ist es nicht sinnvoll, Sie Ihrer ersten Version hinzuzufügen.

![Anmerkungen zur Version auf der Registerkarte "Updates"](./media/manage-nuget-packages-release-notes.png)

Verwenden Sie zum Hinzufügen von Versions Anmerkungen zu einem Paket das neue `<releaseNotes />` Metadata-Element in der nuspec-Datei.

### <a name="nuspec-ltfiles-gt-improvement"></a>. nuspec &ltfiles/ &gt; Improvement
Die `.nuspec` Datei lässt jetzt ein leeres- `<files />` Element zu, das anweist, nuget.exe keine Datei in das Paket aufzunehmen.

## <a name="bug-fixes"></a>Fehlerkorrekturen
Für nuget 1,5 wurden insgesamt 107 Arbeitselemente korrigiert. 103 von diesen wurden als Fehler gekennzeichnet.

Eine vollständige Liste der Arbeitselemente, die in nuget 1,5 behoben wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Fehlerbehebungen beachten Sie Folgendes:

* [Problem 1273](http://nuget.codeplex.com/workitem/1273): Sie haben `packages.config` eine bessere Versionskontrolle erzielt, indem Sie Pakete alphabetisch sortieren und zusätzliche Leerzeichen entfernen.
* [Problem 844](http://nuget.codeplex.com/workitem/844): Versionsnummern werden jetzt normalisiert, sodass Sie `Install-Package 1.0` für ein Paket mit der-Version verwendet werden können `1.0.0` .
* [Problem 1060](http://nuget.codeplex.com/workitem/1060): Wenn Sie ein Paket mit nuget.exe erstellen, `-Version` überschreibt das Flag das- `<version />` Element.
