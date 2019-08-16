---
title: Anmerkungen zu dieser Version von nuget 1,4
description: Anmerkungen zu dieser Version von nuget 1,4 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5f1d3ed6a1b20fb07437f1718faafaac0a193773
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488709"
---
# <a name="nuget-14-release-notes"></a>Anmerkungen zu dieser Version von nuget 1,4

[Anmerkungen zu nuget 1,3 Anmerkungen](../release-notes/nuget-1.3.md) | zu dieser Version von[nuget 1,5](../release-notes/nuget-1.5.md)

Nuget 1,4 wurde am 17. Juni 2011 veröffentlicht.

## <a name="features"></a>Features

### <a name="update-package-improvements"></a>Update-Paket Verbesserungen
Mit nuget 1,4 werden viele Verbesserungen am Befehl "Update-Package" eingeführt, was die Beibehaltung von Paketen in derselben Version in mehreren Projekten in einer Projekt Mappe vereinfacht. Wenn beispielsweise ein Paket auf die neueste Version aktualisiert wird, ist es sehr üblich, dass alle Projekte, die dieses Paket installiert haben, auf dieselbe Verifizierung aktualisiert werden.

Der `Update-Package` Befehl vereinfacht nun Folgendes:

#### <a name="update-all-packages-in-a-single-project"></a>Alle Pakete in einem einzelnen Projekt aktualisieren

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>Aktualisieren eines Pakets in allen Projekten

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>Alle Pakete in allen Projekten aktualisieren

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>Ausführen eines "sicheren" Updates für alle Pakete
Das `-Safe` Flag schränkt Upgrades auf Versionen ein, die die gleiche Haupt-und neben Versions Komponente haben. Wenn z. b. Version 1.0.0 eines Pakets installiert ist und die Versionen 1.0.1, 1.0.2 und 1,1 im Feed verfügbar sind, aktualisiert das `-Safe` Flag das Paket auf 1.0.2. Wenn Sie ohne `-Safe` das-Flag aktualisieren, wird das Paket auf die neueste Version 1,1 aktualisiert.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>Verwalten von Paketen auf Projektmappenebene
Vor dem nuget 1,4 war das Installieren eines Pakets in mehreren Projekten mit dem Dialogfeld mühsam. Es war erforderlich, dass das Dialogfeld einmal pro Projekt gestartet wird.

Nuget 1,4 bietet Unterstützung für das Installieren/Deinstallieren/Aktualisieren von Paketen in mehreren Projekten gleichzeitig. Starten Sie einfach mit der rechten Maustaste auf die Projekt Mappe, und wählen Sie die Menüoption **nuget-Pakete verwalten** aus.

![Dialogfeld "nuget-Pakete verwalten" auf Lösungsebene](./media/manage-nuget-packages-solution-dialog.png)

Beachten Sie, dass in der Titelleiste des Dialog Felds der Name der Projekt Mappe und nicht der Name eines Projekts angezeigt wird.
Paket Vorgänge bieten nun eine Liste von Kontrollkästchen mit der Liste der Projekte, auf die der Vorgang angewendet werden soll.

![Projektauswahl für nuget-Pakete verwalten](./media/manage-nuget-packages-project-selection.png)

Weitere Informationen finden Sie im Thema zum [Verwalten von Paketen für die Lösung](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>Einschränken von Upgrades auf zulässige Versionen
Wenn Sie den `Update-Package` Befehl für ein Paket ausführen (oder das Paket mithilfe des Dialog Felds aktualisieren), wird er standardmäßig auf die neueste Version im Feed aktualisiert. Mit der neuen Unterstützung für das Aktualisieren aller Pakete kann es Fälle geben, in denen Sie ein Paket für einen bestimmten Versions Bereich sperren möchten. Beispielsweise können Sie im Voraus wissen, dass Ihre Anwendung nur mit Version 2. * eines Pakets funktioniert, aber nicht mit 3,0 und höher. Um zu verhindern, dass das Paket versehentlich auf 3 aktualisiert wird, fügt nuget 1,4 Unterstützung für das Einschränken des Bereichs von Versionen hinzu, auf die Pakete aktualisiert werden `packages.config` können, indem die `allowedVersions` Datei mithilfe des neuen Attributs bearbeitet wird.

Im folgenden Beispiel wird z. b. gezeigt, wie `SomePackage` das Paket den Versions Bereich 2,0-3,0 (exklusiv) sperrt.
Das `allowedVersions` Attribut akzeptiert Werte unter Verwendung des [Versions Bereichs Formats](../concepts/package-versioning.md#version-ranges-and-wildcards).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

Beachten Sie, dass in 1,4 das Sperren eines Pakets in einen bestimmten Versions Bereich Hand bearbeitetet werden muss. In nuget 1,5 planen wir die Unterstützung für das Platzieren dieses Bereichs über `Install-Package` den Befehl.

### <a name="package-visualizer"></a>Paket Schnellansicht
Mithilfe der neuen Paket Schnellansicht, die über die -> Menüoption "Paket-Manager-**Paket** -Manager-Paket-Manager" in der Paket-**Manager** -> -Menüoption gestartet wird, können Sie alle Projekte und ihre Paketabhängigkeiten in einer Not.

_**Wichtiger Hinweis:** Diese Funktion nutzt die DGML-Unterstützung in Visual Studio. Das Erstellen der Visualisierung wird nur in Visual Studio Ultimate unterstützt. Das Anzeigen eines dgml-Diagramms wird nur in Visual Studio Premium oder höher unterstützt._

![Paket Schnellansicht](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>Automatische Update Überprüfung für das nuget-Dialog Feld
In einigen Versionen von nuget werden neue Funktionen eingeführt, `.nuspec` die über die Datei ausgedrückt werden, die von älteren Versionen des nuget-Dialog Felds nicht verstanden werden.
Ein Beispiel hierfür ist die Einführung in nuget 1,4 zum [angeben](../release-notes/nuget-1.2.md#framework-assembly-refs)von Frameworkassemblys.
Daher ist es wichtig, dass Sie die neueste Version von nuget verwenden, um sicherzustellen, dass Sie Pakete verwenden können, die die neuesten Features nutzen.
Um nuget-Aktualisierungen besser sichtbar zu machen, enthält das nuget-Dialogfeld Logik zum hervorheben, wenn eine neuere Version verfügbar ist.

_**Hinweis**: Die Überprüfung wird nur vorgenommen, wenn die Registerkarte **Online** in der aktuellen Sitzung ausgewählt wurde._

![Dialogfeld "nuget-Pakete verwalten" mit neuer verfügbarer Version](./media/manage-nuget-packages-update-notification.png)

Wenn Sie die automatische Suche nach Updates deaktivieren möchten, wechseln Sie zum Dialogfeld nuget-Einstellungen, und deaktivieren Sie **automatisch nach Updates suchen**.

![Nuget-Einstellungen](./media/nuget-settings.png)

Diese Funktion wurde in nuget 1,3 tatsächlich hinzugefügt, wäre aber natürlich nicht sichtbar, bis ein Update auf 1,3, z. b. nuget 1,4, verfügbar gemacht wurde.

### <a name="package-manager-dialog-improvements"></a>Verbesserungen im Paket-Manager
* **Verbesserte Menü Namen**: Die Menü Optionen zum Starten des Dialog Felds wurden aus Gründen der Übersichtlichkeit umbenannt. Die Menüoption ist jetzt **nuget-Pakete verwalten**.
* **Detailbereich zeigt das aktuellste Aktualisierungsdatum**an: Das nuget-Dialogfeld zeigt das Datum des letzten Updates im Detailbereich für ein Paket an, wenn die Registerkarte **Online** oder **Updates** ausgewählt ist.
* **Liste der angezeigten Tags**: Im nuget-Dialogfeld werden Tags angezeigt.

### <a name="powershell-improvements"></a>PowerShell-Optimierungen
* **Signierte PowerShell-Skripts**: Nuget umfasst signierte PowerShell-Skripts, die die Verwendung in restriktiveren Umgebungen ermöglichen
* **Unterstützung der Aufforderung**: Die Paket-Manager-Konsole unterstützt nun `$host.ui.Prompt` die `$host.ui.PromptForChoice` Eingabeaufforderung über die Befehle und.
* **Paketquellen Namen**: Das Angeben des Namens einer Paketquelle wird unterstützt, wenn Sie eine Paketquelle `-Source` mit dem-Flag angeben.

### <a name="nugetexe-command-line-improvements"></a>Verbesserungen der Befehlszeile "nuget. exe"
* **Benutzerdefinierte nuget-Befehle**: "nuget. exe" kann über benutzerdefinierte Befehle mithilfe von MEF erweitert werden.
* **Einfacherer Workflow zum Erstellen von Symbol Paketen**: Das `-Symbols` Flag kann auf eine normale, auf der Konvention basierende Ordnerstruktur angewendet werden, indem ein Symbol Paket erstellt wird `.pdb` , indem nur die Quelle und die Dateien in den Ordner eingeschlossen werden.
* **Angeben mehrerer Quellen**: Der `NuGet install` -Befehl unterstützt die Angabe mehrerer Quellen mithilfe von Semikolons als Trennzeichen oder durch `-Source` mehrmals Angabe.
* **Unterstützung der Proxy Authentifizierung**: Bei Verwendung von nuget hinter einem Proxy, für den eine Authentifizierung erforderlich ist, fügt nuget 1,4 Unterstützung für Benutzer Anmelde Informationen hinzu.
* wichtige Änderung bei der **Aktualisierung von nuget. exe**: Das `-Self` -Flag ist nun erforderlich, damit "nuget. exe" sich selbst aktualisiert. `nuget.exe Update`Es wird nun ein Pfad zur `packages.config` Datei verwendet, und es wird versucht, Pakete zu aktualisieren. Beachten Sie, dass dieses Update so eingeschränkt ist, dass es nicht: * * aktualisieren, hinzufügen und Entfernen von Inhalten in der Projektdatei.
\* * Führen Sie PowerShell-Skripts innerhalb des Pakets aus.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Unterstützung für nuget-Server zum Übertragen von Paketen mithilfe von nuget. exe
Nuget bietet eine einfache Möglichkeit, ein einfaches [webbasiertes nuget-Repository](../hosting-packages/nuget-server.md) über das `NuGet.Server` nuget-Paket zu hosten. Mit nuget 1,4 unterstützt der Lightweight-Server das pushen und Löschen von Paketen mithilfe von "nuget. exe".
Die neueste Version von `NuGet.Server` fügt ein neues `appSetting`mit dem `apiKey`Namen hinzu. Wenn der Schlüssel weggelassen oder leer gelassen wird, ist das Übertragen von Paketen in den Feed deaktiviert. Wenn Sie den APIKey auf einen Wert festlegen (im Idealfall ein sicheres Kennwort), können Pakete mithilfe von "nuget. exe" per Push

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Unterstützung für die Windows Phone Tools-Mango-Edition
Nuget wird jetzt in der Release Candidate-Version von Windows Phone Tools für MANGO unterstützt.
Derzeit verfügt Windows Phone Tools nicht über Unterstützung für den Visual Studio-Erweiterungs-Manager. um nuget für Windows Phone Tools zu installieren, müssen Sie die VSIX möglicherweise manuell herunterladen und ausführen.

Führen Sie den folgenden Befehl aus, um nuget für Windows Phone Tools zu deinstallieren.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Fehlerkorrekturen
Für nuget 1,4 wurden insgesamt 88 Arbeitselemente korrigiert. 71 von diesen wurden als Fehler gekennzeichnet.

Eine vollständige Liste der Arbeitselemente, die in nuget 1,4 behoben wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Fehlerbehebungen beachten Sie Folgendes:

* [Problem 603](http://nuget.codeplex.com/workitem/603): Paketabhängigkeiten in verschiedenen Depots werden ordnungsgemäß aufgelöst, wenn eine bestimmte Paketquelle angegeben wird.
* [Problem 1036](http://nuget.codeplex.com/workitem/1036): Das `NuGet Pack SomeProject.csproj` hinzufügen zum Postbuildereignis verursacht keine unendliche Schleife mehr.
* [Problem 961](http://nuget.codeplex.com/workitem/961): `-Source` das Flag unterstützt relative Pfade.

## <a name="nuget-14-update"></a>Nuget 1,4-Update
Kurz nach der Veröffentlichung von nuget 1,4 haben wir einige Probleme festgestellt, die für die Behebung wichtig waren.
Die spezifische Versionsnummer dieses Updates auf 1,4 lautet 1.4.20615.9020.

### <a name="bug-fixes"></a>Fehlerkorrekturen
* [Problem 1220](http://nuget.codeplex.com/workitem/1220): Update-Package wird nicht `install.ps1` in allen Projekten ausgeführt / `uninstall.ps1` , wenn mehr als ein Projekt vorhanden ist.
* [Problem 1156](http://nuget.codeplex.com/workitem/1156): Der Paket-Manager ist auf W2K3/XP hängen (Wenn PowerShell 2 nicht installiert ist).
