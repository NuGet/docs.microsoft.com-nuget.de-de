---
title: Anmerkungen zu NuGet 1.4
description: Anmerkungen zu NuGet 1.4, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f4d712f83ea108a82a1bc4910c2a721a8c24d51
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550630"
---
# <a name="nuget-14-release-notes"></a>Anmerkungen zu NuGet 1.4

[Anmerkungen zu NuGet 1.3](../release-notes/nuget-1.3.md) | [Anmerkungen zu NuGet 1.5](../release-notes/nuget-1.5.md)

NuGet 1.4 wurde 17 Juni 2011 veröffentlicht.

## <a name="features"></a>Features

### <a name="update-package-improvements"></a>Update-Package-Verbesserungen
NuGet 1.4 führt eine Menge Verbesserungen an den Update-Package-Befehl, der Pakete auf die gleiche Version beschränken, die für mehrere Projekte in einer Projektmappe vereinfacht. Beispielsweise ist, wenn ein Paket auf die neueste Version zu aktualisieren, es üblich, alle Projekte mit diesem Paket installiert, um auf die gleiche Verision aktualisiert werden soll.

Die `Update-Package` Befehl jetzt erleichtert:

#### <a name="update-all-packages-in-a-single-project"></a>Aktualisieren Sie alle Pakete in einem einzelnen Projekt

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>Aktualisieren eines Pakets in allen Projekten

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>Aktualisieren Sie alle Pakete in allen Projekten

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>Ausführen eines "sicheren" Updates für alle Pakete
Die `-Safe` Flag schränkt Upgrades nur Versionen mit der gleichen Haupt- und Nebenversionen-Version-Komponente. Wenn Sie Version 1.0.0 eines Pakets installiert ist, und es stehen Versionen 1.0.1, 1.0.2 und 1.1 im Feed, z. B. die `-Safe` Flag aktualisiert das Paket 1.0.2. Aktualisieren, ohne die `-Safe` Flag würde aktualisieren Sie das Paket auf die neueste Version 1.1.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>Verwalten von Paketen auf Projektmappenebene
Vor NuGet 1.4 war die Installation eines Pakets in mehrere Projekte mühsam mithilfe des Dialogfelds. Starten das Dialogfeld einmal pro Projekt erforderlich.

NuGet 1.4 fügt Unterstützung für Installation/Deinstallation/Aktualisieren von Paketen in mehreren Projekten gleichzeitig hinzu. Starten Sie einfach die von der rechten Maustaste auf die Projektmappe, und wählen die **NuGet-Pakete verwalten** Option des Menüs.

![Dialogfeld "Projektmappe auf NuGet-Pakete verwalten"](./media/manage-nuget-packages-solution-dialog.png)

Beachten Sie, dass in der Titelleiste des Dialogfelds der Namen der Projektmappe angezeigt wird, nicht den Namen eines Projekts.
Paketvorgängen bieten jetzt eine Liste von Kontrollkästchen mit der Liste der Projekte, denen auf die Operation angewendet werden soll.

![Verwalten von NuGet-Pakete-Projekt-Auswahl](./media/manage-nuget-packages-project-selection.png)

Weitere Informationen finden Sie im Thema auf [Verwalten von Paketen für die Lösung](../tools/package-manager-ui.md#managing-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>Einschränken von ein Upgrade auf zulässige Version
Standardmäßig wird beim Ausführen der `Update-Package` Befehl für ein Paket (oder aktualisieren das Paket mithilfe des Dialogfeld), er aktualisiert, auf die neueste Version im Feed. Durch die neue Unterstützung für alle Pakete aktualisieren gibt es möglicherweise Fälle, die in denen Sie ein Paket auf einen bestimmten Versionsbereich sperren möchten. Beispielsweise können Sie im Voraus wissen, dass Ihre Anwendung nur mit Version 2. * eines Pakets, aber nicht 3.0 und höher funktionieren. Um zu verhindern, aktualisieren das Paket versehentlich auf 3, fügt NuGet 1.4-Unterstützung für das Einschränken des Bereichs von Versionen, die Pakete manuell bearbeiten, aktualisiert werden können die `packages.config` Datei mit dem neuen `allowedVersions` Attribut.

Das folgende Beispiel zeigt z. B. wie Sperren der `SomePackage` range-Paket der Version 2.0-3.0 (exklusiv).
Die `allowedVersions` Attribut akzeptiert Werte mit den [Bereich Versionsformat](../reference/package-versioning.md#version-ranges-and-wildcards).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

Beachten Sie, dass in 1.4, Sperren ein Paket auf einen bestimmten Versionsbereich manuell bearbeitet werden muss. In NuGet 1.5 wir planen Unterstützung für die Platzierung dieses Bereichs über die `Install-Package` Befehl.

### <a name="package-visualizer"></a>Paket-Schnellansicht
Das neue Paket-Visualizer, gestartet wird, über die **Tools** -> **Bibliothekspaket-Manager** -> **Paket Schnellansicht** Menüoption, können Sie Visualisieren Sie problemlos alle Projekte und ihre paketabhängigkeiten in einer Projektmappe ein.

_**Wichtiger Hinweis:** dieses Feature nutzt die DGML-Unterstützung in Visual Studio. Erstellen die Visualisierung wird nur in Visual Studio Ultimate unterstützt. Ein DGML-Diagramm anzeigen, wird nur in Visual Studio Premium oder höher unterstützt._

![Paket-Schnellansicht](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>Überprüfen Sie automatische Updates für das Dialogfeld "NuGet"
Einige Versionen von NuGet ggf. neue Features, die angegeben wird, über die `.nuspec` Datei, die von älteren Versionen von NuGet-Dialogfeld nicht verstanden werden.
Ein Beispiel ist die Einführung in NuGet 1.4 für [Framework-Assemblys angeben](../release-notes/nuget-1.2.md#framework-assembly-refs).
Aus diesem Grund ist es wichtig, dass die neueste Version von NuGet zum sicherstellen, dass Sie Pakete, die die neuesten Features nutzen können.
Um Updates zu NuGet besser sichtbar zu machen, enthält das Dialogfeld "NuGet" zu markieren, wenn eine neuere Version verfügbar ist.

_**Beachten Sie**: die Überprüfung erfolgt nur, wenn die **Online** Registerkarte in der aktuellen Sitzung ausgewählt wurde._

![Verwalten des NuGet-Pakete (Dialogfeld) mit der neuen Version verfügbar](./media/manage-nuget-packages-update-notification.png)

Um die automatische Prüfung auf Updates zu deaktivieren, wechseln Sie zu den NuGet-Dialogfeld "Einstellungen", und deaktivieren Sie **automatisch nach Updates suchen**.

![NuGet-Einstellungen](./media/nuget-settings.png)

Dieses Feature hinzugefügt und war in NuGet-Version 1.3, aber nicht angezeigt wird, natürlich, bis ein Update für 1.3, z. B. NuGet 1.4, verfügbar gemacht wurde.

### <a name="package-manager-dialog-improvements"></a>Dialogfeld "Paket-Manager"-Verbesserungen
* **Verbesserte Menünamen**: Optionen zum Starten des Dialogfelds aus Gründen der Übersichtlichkeit wurde umbenannt. Die Menüoption "" ist jetzt **NuGet-Pakete verwalten**.
* **Detailbereich werden die letzten Aktualisierungsdatum**: das NuGet-Dialogfeld zeigt das Datum des neuesten Updates im Detailbereich für ein Paket bei der **Online** oder **aktualisiert** Registerkarte ausgewählt ist.
* **Liste der Tags angezeigt**: Tags für das Nuget-Dialogfeld angezeigt.

### <a name="powershell-improvements"></a>Verbesserungen an der PowerShell
* **Signierte PowerShell-Skripts**: NuGet enthält signierte Powershell-Skripts, die Verwendung in restriktivere Umgebungen aktivieren.
* **Aufforderung Unterstützung**: die Paket-Manager-Konsole unterstützt jetzt die Eingabeaufforderung über den `$host.ui.Prompt` und `$host.ui.PromptForChoice` Befehle.
* **Verpacken von Datenquellennamen**: den Namen der Paketquelle angeben wird unterstützt, bei der Angabe der Quelle für ein Paket mit der `-Source` Flag.

### <a name="nugetexe-command-line-improvements"></a>Verbesserungen der NuGet.exe-Befehlszeile
* **Benutzerdefinierte NuGet-Befehle**: nuget.exe über benutzerdefinierte Befehle, die Sie mit MEF erweiterbar ist.
* **Einfachere der Workflow zum Erstellen von Symbolpaketen**: die `-Symbols` Flag kann auf eine normale konventionsbasierten-Ordnerstruktur erstellen ein Symbolpaket dazu nur die Quelle angewendet werden und `.pdb` Dateien innerhalb des Ordners.
* **Angeben von mehreren Quellen**: die `NuGet install` Befehl unterstützt die Angabe von mehreren Quellen verwenden Semikolons als Trennzeichen oder durch Angabe `-Source` mehrmals.
* **Proxy-Authentifizierung unterstützen**: NuGet 1.4 fügt Unterstützung für die Eingabeaufforderung für Anmeldeinformationen des Benutzers, wenn NuGet hinter einem Proxy zu verwenden, die eine Authentifizierung erforderlich ist.
* **NuGet.exe wichtige Änderung aktualisieren**: die `-Self` Flag ist jetzt erforderlich, für die nuget.exe sich selbst zu aktualisieren. `nuget.exe Update` verwendet jetzt in einen Pfad zu der `packages.config` Datei, und versucht, Pakete zu aktualisieren. Beachten Sie, dass dieses Update beschränkt ist, dass dies nicht der Fall: ** zu aktualisieren, hinzufügen und Entfernen von Inhalt in der Projektdatei.
** Führen Sie Powershell-Skripts innerhalb des Pakets.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>NuGet-Server-Unterstützung für mithilfe von nuget.exe-Pakete mithilfe von Push übertragen
NuGet schließt eine einfache Möglichkeit zum Hosten einer [NuGet-Repository für einfache webbasierte](../hosting-packages/nuget-server.md) über die `NuGet.Server` NuGet-Paket. Mit NuGet 1.4 unterstützt der kompakten Server mithilfe von Push übertragen und Löschen von Paketen, die mithilfe von nuget.exe.
Die neueste Version des `NuGet.Server` Fügt ein neues `appSetting`mit dem Namen `apiKey`. Wenn der Schlüssel weggelassen oder leer gelassen wird, ist das Übertragen von Paketen in den Feed deaktiviert. Die apikey-Variable auf einen Wert (im Idealfall ein sicheres Kennwort) festlegen, können Ablegevorgänge Pakete, die mithilfe von nuget.exe.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Unterstützung für Windows Phone-Tools Mango Edition
NuGet ist jetzt in der Release Candidate-Version von Windows Phone-Tools für Mango unterstützt.
Derzeit Windows Phone-Tools verfügt nicht über die Unterstützung der Visual Studio-Erweiterungs-Manager zum Installieren von NuGet für Windows Phone-Tools müssen Sie möglicherweise herunterladen, und führen die VSIX-Datei manuell.

Um NuGet für Windows Phone-Tools zu deinstallieren, führen Sie den folgenden Befehl aus.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Fehlerkorrekturen
NuGet 1.4 mussten insgesamt 88 Arbeitsaufgaben behoben. 71 davon waren als Fehler gekennzeichnet.

Eine vollständige Liste der Arbeit Elemente eine feste in NuGet 1.4, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Fehlerbehebungen zu beachten:

* [Problem 603](http://nuget.codeplex.com/workitem/603): paketabhängigkeiten für verschiedene Repositorys wird beim Angeben einer bestimmten Quelle ordnungsgemäß aufgelöst.
* [Problem 1036](http://nuget.codeplex.com/workitem/1036): Hinzufügen von `NuGet Pack SomeProject.csproj` Ereignis nicht mehr nach dem Erstellen verursacht eine Endlosschleife.
* [Problem 961](http://nuget.codeplex.com/workitem/961): `-Source` Flag unterstützt relative Pfade.

## <a name="nuget-14-update"></a>NuGet 1.4-Update
Kurz nach der Veröffentlichung von NuGet 1.4 stellten wir einige Probleme, die wichtig, die behoben wurden.
Die Versionsnummer des Updates auf 1.4 ist 1.4.20615.9020.

### <a name="bug-fixes"></a>Fehlerkorrekturen
* [Problem 1220](http://nuget.codeplex.com/workitem/1220): Update-Paket nicht ausgeführt. `install.ps1` / `uninstall.ps1` in allen Projekten bei mehr als ein Projekt
* [Problem 1156](http://nuget.codeplex.com/workitem/1156): Paket-Manager Computerkonsole hängen unter W2K3/XP (wenn es sich um eine Powershell-2 nicht installiert ist)
