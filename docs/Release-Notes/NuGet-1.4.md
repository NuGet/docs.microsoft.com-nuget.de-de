---
title: Anmerkungen zur Version von NuGet 1.4 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 1.4 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet 1.4 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bc0800361551b996d958e03b9cfa3d745b78e43d
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-14-release-notes"></a>1.4 NuGet-Versionshinweise

[Anmerkungen zur Version des NuGet-1.3](../release-notes/nuget-1.3.md) | [NuGet 1.5-Versionshinweise](../release-notes/nuget-1.5.md)

NuGet 1.4 wurde 17 Juni 2011 veröffentlicht.

## <a name="features"></a>Features

### <a name="update-package-improvements"></a>Updatepaket Verbesserungen
NuGet 1.4 führt viele Verbesserungen an den Update-Paket-Befehl zu Pakete über die gleiche Version für mehrere Projekte in einer Projektmappe erleichtern. Beispielsweise ist, wenn ein Paket auf die neueste Version zu aktualisieren, es üblich, die alle Projekte mit diesem Paket installiert, um auf die gleiche Verision aktualisiert werden soll.

Die `Update-Package` Befehl jetzt vereinfacht:

#### <a name="update-all-packages-in-a-single-project"></a>Aktualisieren Sie alle Pakete in einem einzelnen Projekt

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>Aktualisieren eines Pakets in allen Projekten

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>Aktualisieren Sie alle Pakete in allen Projekten

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>Ausführen eines "sicheren" Updates für alle Pakete
Die `-Safe` Flag beschränkt Upgrades auf nur Versionen mit der gleichen Haupt- und Version-Komponente. Angenommen, wenn die Version 1.0.0 eines Pakets installiert ist und die Versionen 1.0.1, 1.0.2 und 1.1 im Feed verfügbar sind die `-Safe` Flag aktualisiert das Paket auf die Version 1.0.2. Aktualisieren der ohne die `-Safe` Flag würde aktualisieren Sie das Paket auf die neueste Version 1.1.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>Verwalten von Paketen auf Projektmappenebene
Vor der Einführung NuGet 1.4 war die Installation eines Pakets in mehrere Projekte mühsam mithilfe des Dialogfelds. Das Dialogfeld ", einmal pro Projekt starten muss.

NuGet 1.4 fügt Unterstützung für Installation/Deinstallation/Aktualisieren von Paketen in mehreren Projekten gleichzeitig hinzu. Starten Sie einfach die von mit der rechten Maustaste auf die Projektmappe, und wählen die **NuGet-Pakete verwalten** Option des Menüs.

![Dialogfeld für Projektmappen auf NuGet-Pakete verwalten](./media/manage-nuget-packages-solution-dialog.png)

Beachten Sie, dass in der Titelleiste des Dialogfelds, der Namen der Projektmappe angezeigt wird, nicht den Namen eines Projekts.
Paketvorgängen bieten nun eine Liste von Kontrollkästchen mit der Liste der Projekte, denen die Operation angewendet werden sollen.

![Verwalten von NuGet-Pakete Projektauswahl](./media/manage-nuget-packages-project-selection.png)

Weitere Informationen finden Sie im Thema auf [Verwaltung von Paketen für die Projektmappe](../tools/package-manager-ui.md#managing-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>Einschränken von Upgrades auf Versionen zulässig
Standardmäßig wird beim Ausführen der `Update-Package` Befehl für ein Paket (oder beim Aktualisieren des Pakets im Dialogfeld), wird Sie auf die neueste Version im Feed aktualisiert werden. Mit der neuen Unterstützung für alle Pakete aktualisiert es gibt möglicherweise Fälle, die in denen Sie ein Paket für eine bestimmte Version Palette sperren möchten. Sie können z. B. im Voraus wissen, dass Ihre Anwendung nur bei Version 2.* eines Pakets, aber nicht 3.0 und höher verwendet wird. Um zu verhindern, dass versehentlich beim Aktualisieren des Pakets auf 3 NuGet 1.4 fügt Unterstützung für die Beschränkung der Bereich von Versionen, die Pakete von Hand bearbeiten aktualisiert werden können die `packages.config` Datei mit dem neuen `allowedVersions` Attribut.

Z. B. das folgende Beispiel veranschaulicht das Sperren der `SomePackage` Paket die Version im Bereich (exklusiv) 2.0-3.0.
Die `allowedVersions` Attribut akzeptiert die Werte mithilfe der [Bereich Versionsformat](../reference/package-versioning.md#version-ranges-and-wildcards).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

Beachten Sie, dass in 1.4, Sperren ein Paket für eine bestimmte Version Palette manuell bearbeitet werden muss. In NuGet 1.5 wir planen die zum Hinzufügen der Unterstützung für die Platzierung dieser Bereich über dem `Install-Package` Befehl.

### <a name="package-visualizer"></a>Paket-Schnellansicht
Das neue Paket-Schnellansicht gestartet wird, über die **Tools** -> **Bibliothekspaket-Manager** -> **Paket Schnellansicht** Menüoption, können Sie Visualisieren Sie einfach alle Projekte und ihre Abhängigkeiten des Pakets in einer Projektmappe ein.

_**Wichtiger Hinweis:** diese Funktion nutzt die DGML-Unterstützung in Visual Studio. Erstellen die Visualisierung wird nur in Visual Studio Ultimate unterstützt. Anzeigen von DGML-Diagrammen wird nur in Visual Studio Premium oder höher unterstützt._

![Paket-Schnellansicht](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>Automatische Updates für das Dialogfeld "NuGet"
Einige Versionen von NuGet ggf. neue Features, die über ausgedrückt der `.nuspec` Datei, die nicht mit älteren Versionen von das Dialogfeld "NuGet" verstanden werden.
Ein Beispiel ist der Einführung in NuGet 1.4 für [angeben Frameworkassemblys](../release-notes/nuget-1.2.md#framework-assembly-refs).
Aus diesem Grund ist es wichtig, die neueste Version von NuGet verwenden, um sicherzustellen, dass Sie die neuesten Features nutzen Pakete verwenden können.
Um Updates zu NuGet mehr sichtbar zu machen, enthält das Dialogfeld "NuGet" Logik zum Markieren, wenn eine neuere Version verfügbar ist.

_**Hinweis**: die Überprüfung erfolgt nur, wenn die **Online** Registerkarte in der aktuellen Sitzung ausgewählt wurde._

![Dialogfeld mit neuen Version verfügbaren NuGet-Pakete verwalten](./media/manage-nuget-packages-update-notification.png)

Um die automatische Prüfung auf Updates zu deaktivieren, wechseln Sie zum Dialogfeld "NuGet-Einstellungen", und deaktivieren Sie **automatisch nach Updates suchen**.

![NuGet-Einstellungen](./media/nuget-settings.png)

Diese Funktion tatsächlich in NuGet 1.3 hinzugefügt wurde, aber nicht sichtbar ist, natürlich, bis ein Update für 1.3, z. B. NuGet 1.4, zur Verfügung gestellt wurde.

### <a name="package-manager-dialog-improvements"></a>Dialogfeld "Paket-Manager"-Verbesserungen
* **Verbesserte Menünamen**: Menüoptionen zum Starten Sie des Dialogfeld "wurden aus Gründen der Übersichtlichkeit umbenannt. Die Menüoption ist jetzt **NuGet-Pakete verwalten**.
* **Im Detailbereich zeigt die neuesten Update Datum**: das NuGet-Dialogfeld zeigt das Datum des neuesten Updates im Detailbereich für ein Paket bei der **Online** oder **aktualisiert** Registerkarte ausgewählt ist.
* **Liste der RFID-Transponder angezeigt**: Tags für das NuGet-Dialogfeld angezeigt.

### <a name="powershell-improvements"></a>PowerShell-Verbesserungen
* **PowerShell-Skripts signiert**: NuGet enthält signierte Powershell-Skripts, die Verwendung in enger gefassten Umgebungen aktivieren.
* **Unterstützung aufzufordern**: die Package Manager Console unterstützt jetzt die Bestätigung über die `$host.ui.Prompt` und `$host.ui.PromptForChoice` Befehle.
* **Paket Quellennamen**: der Name der Paketquelle wird unterstützt, bei der Angabe der Quelle für ein Paket mit der `-Source` Flag.

### <a name="nugetexe-command-line-improvements"></a>NuGet.exe Befehlszeile Verbesserungen
* **Benutzerdefinierte NuGet-Befehle**: nuget.exe über benutzerdefinierte Befehle, die mithilfe von MEF erweiterbar ist.
* **Einfacher Workflow zum Erstellen von Paketen Symbol**: die `-Symbols` -Flag kann in einer normalen konventionsbasierten Ordnerstruktur erstellen ein Symbolpaket dazu nur die Quelle angewendet werden und `.pdb` Dateien innerhalb des Ordners.
* **Angeben von mehreren Quellen**: die `NuGet install` Befehl unterstützt die Angabe von mehreren Quellen mit Semikolons als Trennzeichen oder durch Angabe `-Source` mehrere Male.
* **Proxy-Authentifizierung unterstützen**: NuGet 1.4 fügt Unterstützung für die Eingabeaufforderung für Anmeldeinformationen des Benutzers, wenn NuGet hinter einem Proxy verwenden, die eine Authentifizierung erforderlich ist.
* **NuGet.exe unterbrechende Änderung aktualisieren**: die `-Self` Flag ist jetzt erforderlich für nuget.exe selbst aktualisieren. `nuget.exe Update` Jetzt dauert in einen Pfad zu der `packages.config` Datei und versucht, Pakete zu aktualisieren. Beachten Sie, dass dieses Update beschränkt ist, da dies nicht der Fall: ** zu aktualisieren, hinzufügen und Entfernen von Inhalt in der Projektdatei.
** Führen Sie Powershell-Skripts im Paket.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>NuGet-Server-Unterstützung für Push-Pakete, die mittels nuget.exe
NuGet enthält eine einfache Methode zum Hosten einer [einfache webbasierte NuGet-Repository](../hosting-packages/nuget-server.md) über die `NuGet.Server` NuGet-Paket. Mit NuGet-1.4 unterstützt einfache Server per Push übertragen, und Löschen von Paketen mit nuget.exe.
Die neueste Version des `NuGet.Server` wird ein neues `appSetting`mit dem Namen `apiKey`. Wenn der Schlüssel weggelassen oder leer gelassen wird, wird die Pakete auf den Feed übertragen deaktiviert. Durch das Festlegen der "apikey" auf einen Wert (im Idealfall ein sicheres Kennwort) können wie Pakete mit nuget.exe.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Unterstützung für Windows Phone Tools Mango Edition
NuGet ist jetzt in der Release Candidate-Version von Windows Phone-Tools für Mango unterstützt.
Aktuell-Tools für Windows Phone verfügt nicht über die Unterstützung für die Erweiterung für Visual Studio-Manager damit NuGet für Windows Phone-Tools zu installieren, müssen Sie möglicherweise herunterladen und die VSIX manuell ausführen.

Führen Sie den folgenden Befehl zum Deinstallieren von NuGet für Windows Phone-Tools.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Fehlerkorrekturen
NuGet 1.4 mussten insgesamt 88 Arbeitsaufgaben behoben. 71 dieser wurden als Fehler gekennzeichnet.

Eine vollständige Liste der Arbeit Elemente in behoben NuGet 1.4, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Fehlerkorrekturen Folgendes zu beachten:

* [Problem 603](http://nuget.codeplex.com/workitem/603): paketabhängigkeiten über unterschiedliche Repositorys ordnungsgemäß aufgelöst werden bei der eine bestimmte Paketquelle angeben.
* [Problem 1036](http://nuget.codeplex.com/workitem/1036): Hinzufügen von `NuGet Pack SomeProject.csproj` Ereignis nicht mehr nach dem Erstellen verursacht eine Endlosschleife.
* [Problem 961](http://nuget.codeplex.com/workitem/961): `-Source` Flag unterstützt relative Pfade.

## <a name="nuget-14-update"></a>NuGet-1.4-Update
Kurz nach der Version des NuGet-1.4 stellten wir eine Reihe von Problemen, die wichtig, die behoben wurden.
Die spezifische Versionsnummer für dieses Update 1.4 ist 1.4.20615.9020.

### <a name="bug-fixes"></a>Fehlerkorrekturen
* [Problem 1220](http://nuget.codeplex.com/workitem/1220): Update-Paket nicht ausgeführt werden `install.ps1` / `uninstall.ps1` in allen Projekten bei mehr als ein Projekt
* [Problem 1156](http://nuget.codeplex.com/workitem/1156): Paket-Manager Computerkonsole hängen unter W2K3/XP (wenn es sich um eine Powershell-2 nicht installiert ist)
