---
title: Anmerkungen zur Version von NuGet 1.0 und 1.1
description: Versionshinweise für NuGet 1.1 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a11248a96109c879946e7e28a50e7753b644f042
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822122"
---
# <a name="nuget-10-and-11-release-notes"></a>Anmerkungen zur Version von NuGet 1.0 und 1.1

[NuGet 1.2-Versionshinweise](../release-notes/nuget-1.2.md)

NuGet 1.0 wurde 13 Januar 2011 veröffentlicht.  NuGet-1.1 wurde am 12. Februar 2011 veröffentlicht.

## <a name="overview"></a>Übersicht

Dieses Dokument enthält die Versionshinweise für die verschiedenen Versionen des gruppiert nach wichtigen Preview-Version von NuGet-1.0.

NuGet umfasst die folgenden Komponenten:

* *NuGet.Tools.vsix* * die besteht aus:
  * **Bibliothek-Paket-Dialogfeld "hinzufügen"** * Dialogfeld in Visual Studio zum Suchen und Installieren von Paketen verwendet.
  * **Paket-Manager-Konsole** * Powershell-basierte Verwaltungskonsole in Visual Studio.
* *NuGet-Befehlszeilentool* * Tool verwendet, um Pakete zu erstellen (und schließlich veröffentlichen).

Die NuGet-Tools für Visual Studio-Erweiterung (*NuGet.Tools.vsix*) erfordert:

* Visual Studio 2010 noch Visual Web Developer 2010 Express.

Das NuGet-Befehlszeilentool benötigen Sie Folgendes:

* .NET Framework, Version 4

## <a name="installation"></a>Installation

Dieses [neueste Release](http://nuget.codeplex.com/releases/view/52018):

* Deinstallieren Sie zunächst den älteren Build. Sie müssen Visual Studio als Administrator dazu ausführen.
* Entfernen Sie alle vorhandenen Feeds, die Sie haben.
* Hinzufügen ein neues Feeds auf [ http://go.microsoft.com/fwlink/?LinkId=206669 ](http://go.microsoft.com/fwlink/?LinkId=206669).

## <a name="nuget-11"></a>NuGet-1.1

Die Liste der in dieser Version behobene Probleme [finden Sie hier](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

Ein Problem behoben wurde seit dem RC für RTM.

* [Problem 474: Entfernen von Paketen beeinflusst alle Projekt In der Projektmappe](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Release Candidate

Im folgenden sind die Änderungen, die in diesem Release Candidate seit CTP 2. Besuchen Sie die Problemverfolgung, um die vollständige Liste von Fehlern finden Sie unter.

* [Aktualisieren eines Pakets aus der Konsole aktualisiert Abhängigkeiten nicht.](http://nuget.codeplex.com/workitem/443)
* [Hinzufügen von Paket übernimmt "bin" Paket nicht-Verweis (CTP1)](http://nuget.codeplex.com/workitem/442)
* [Aktualisieren eines Pakets bleibt funktionierende Referenzen](http://nuget.codeplex.com/workitem/440)
* [Get-Package-Updates fehlschlägt, klicken Sie im Dialogfeld, oder wenn der "Alle" aggregatquelle in der Konsole ausgewählt ist](http://nuget.codeplex.com/workitem/439)
* [Abrufen von Paket-Überprüfungsfehler](http://nuget.codeplex.com/workitem/426)
* [Benutzer zu warnen, wenn ein Paket über das Dialogfeld "Paket-" installiert werden können](http://nuget.codeplex.com/workitem/425)
* [Get-Package-löst aktualisiert, wenn große Anzahl von Paketen aktualisieren](http://nuget.codeplex.com/workitem/424)
* [Verbessern Sie die Fehlerbehandlung, wenn die Nuspec-Dateien nicht ordnungsgemäß erstellt werden](http://nuget.codeplex.com/workitem/423)
* [NuGet-Pack ignoriert die angegebene Dateien](http://nuget.codeplex.com/workitem/422)
* [Entfernen die zweite vorletztes Paketquelle, und klicken Sie dann auf "Nach unten" stürzt ab Visual Studio](http://nuget.codeplex.com/workitem/418)
* [Entfernen des Assemblyverweises während der Installation von Paketen](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException beim Öffnen der Dialog "Einstellungen"](http://nuget.codeplex.com/workitem/411)
* [Zugriffsschlüssel für die Paketquelle im Paket-Manager-Konsole funktioniert nicht](http://nuget.codeplex.com/workitem/410)
* [Setzen Sie den Fokus auf falsche Felder Zugriffstasten Dialogfeld "Einstellungen" NuGet im Vergleich](http://nuget.codeplex.com/workitem/409)
* [Paket-ID Intellisense sollten zu viele Elemente nicht abgefragt werden.](http://nuget.codeplex.com/workitem/404)
* [Fehler beim Hinzufügen des Pakets zum Projekt mit einem Punktzeichen in den Namen des Projekts](http://nuget.codeplex.com/workitem/403)
* [Geben Sie mit angegebenen Nuspec-Dateien](http://nuget.codeplex.com/workitem/400)
* [Richtige offizielle Feed sollte registriert werden, wenn neueren Build verwenden](http://nuget.codeplex.com/workitem/399)
* [RFID-Transponder sollten Leerzeichen anstelle von # verwenden](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata fehlen einige nützliche Informationen](http://nuget.codeplex.com/workitem/388)
* [Fügen Sie diesen Link zum Dialogfeld ""](http://nuget.codeplex.com/workitem/386)
* [Verwenden App_Data beim Entzippen von Paketen zu Unterbrechungen im Visual Studio](http://nuget.codeplex.com/workitem/380)
* [Implementieren von Tags](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder ermöglicht, leeres Paket ohne Abhängigkeiten erstellt werden](http://nuget.codeplex.com/workitem/373)
* [Fügen Sie Besitzer Feld für das Paket hinzu](http://nuget.codeplex.com/workitem/365)
* [Aktualisieren Sie das VSIX-Manifest bedeutet NuGet Package Manager anstatt von VSIX-Tools](http://nuget.codeplex.com/workitem/364)
* [Befehl "Get-Package" löst Fehler aus, wenn alle Quelle ausgewählt ist](http://nuget.codeplex.com/workitem/359)
* [Zulassen Sie Reihenfolge der Paketquellen im Dialogfeld "Optionen"](http://nuget.codeplex.com/workitem/356)
* [Update-Paket wird nicht mit älteren Version entfernt.](http://nuget.codeplex.com/workitem/352)
* [Implementieren von Versionsbereich-Spezifikation für Abhängigkeiten](http://nuget.codeplex.com/workitem/347)
* [Visual Studio stürzt ab, wenn Sie auf "Neues Paket hinzufügen"](http://nuget.codeplex.com/workitem/346)
* [Zeigt die Downloads und Bewertungen in das Paket "hinzufügen"](http://nuget.codeplex.com/workitem/345)
* [Wechseln zwischen Paketquellen im Dialogfeld "" Aktualisieren keine aktiven Quelle.](http://nuget.codeplex.com/workitem/344)
* [Entfernen Sie Schlüsselbindung für Paket-Manager-Konsolenfensters](http://nuget.codeplex.com/workitem/339)
* [Install-Package wird nicht als Name eines Cmdlets erkannt...](http://nuget.codeplex.com/workitem/338)
* [Installieren eines Pakets aus einem lokalen feed Abhängigkeiten auf reguläre Feeds werden nicht aufgelöst.](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies überspringen soll Abhängigkeiten, die weiterhin zu verwenden sind](http://nuget.codeplex.com/workitem/331)
* [Benutzer wenn Seitennavigation abbrechen zu können, kann nicht zu einer anderen Seite navigieren, während die ursprüngliche Seitenanforderung zurückgibt](http://nuget.codeplex.com/workitem/325)
* [Untersuchen Sie Leistung NuPack.Server Feeds mit einer großen Anzahl von Paketen zu verarbeiten.](http://nuget.codeplex.com/workitem/324)
* [Ein zweites Mal, das ich filtern, für ein Paket wird durch die Paketquelle "Neu" anstelle der zuvor ausgewählten Quelle.](http://nuget.codeplex.com/workitem/321)
* [Standard-Paketquelle muss ausgewählt werden, bei der Auswahl der Registerkarte "Online" im Dialog.](http://nuget.codeplex.com/workitem/320)
* [Liste Paket sollte standardmäßig installierten Pakete anzeigen.](http://nuget.codeplex.com/workitem/309)
* [Assembly-Verweis HintPaths](http://nuget.codeplex.com/workitem/294)
* [Ausnahme beim Öffnen des Paket-Manager-Konsole](http://nuget.codeplex.com/workitem/268)
* [Konsole Intellisense downloads gesamten feed](http://nuget.codeplex.com/workitem/259)
* [Paketquelle 'Default' sollte auf 'Active' umbenannt werden soll](http://nuget.codeplex.com/workitem/258)
* [Paket Datenquellen UI: Sie auf OK sollten neue Quelle hinzufügen, wenn Name/Quellfelder nicht leer sind](http://nuget.codeplex.com/workitem/257)
* [Dialogfeld wird äußerst langsam, wenn die Anzahl der installierten Pakete groß ist](http://nuget.codeplex.com/workitem/243)
* [Unterstützung von Bindungsumleitungen für Assemblys mit starkem Namen](http://nuget.codeplex.com/workitem/238)
* [Paket-Verweis hinzufügen... UI Drop nach unten für die Paketquelle einschließen](http://nuget.codeplex.com/workitem/226)
* [NuPack muss konfigurationstransformation agnostically des Dateinamens Config unterstützen](http://nuget.codeplex.com/workitem/224)
* [Ermöglicht das BasePath-Argument außer Kraft gesetzte in NuPack.exe sein.](http://nuget.codeplex.com/workitem/222)
* [Alternative Quelle Paketverhalten](http://nuget.codeplex.com/workitem/204)
* [Bei GUI abstürzen](http://nuget.codeplex.com/workitem/201)
* [Hinzufügen, die Sortieroptionen Paket Dialog "hinzufügen"](http://nuget.codeplex.com/workitem/179)
* [Tastenkombination, deaktivieren Sie die Paket-Manager-Konsole](http://nuget.codeplex.com/workitem/174)
* [PowerConsole bewirkt, dass NuPack Konsole fehlschlägt](http://nuget.codeplex.com/workitem/166)
* [Konsole und Paket-Dialogfeld hinzufügen, sollten Benutzer-Agent in Anforderungen festlegen.](http://nuget.codeplex.com/workitem/141)
* [Legen Sie die Versionsnummer der VSIX und NuPack.exe im Build.](http://nuget.codeplex.com/workitem/134)
* [Ausblenden von allgemeine PowerShell-Parameter vom-?](http://nuget.codeplex.com/workitem/118)
* [-Die ausführliche Hilfe Konsolenbefehle hinzufügen](http://nuget.codeplex.com/workitem/110)
* [Das Hinzufügen eines Pakets Dialogfeld zulassen sollte die aktuellen Paketquelle auswählen](http://nuget.codeplex.com/workitem/88)
* [Verschieben Sie NuPack.Core Klassen in verschiedenen namespaces](http://nuget.codeplex.com/workitem/50)
* [Hilfe zu Cmdlets für das Hinzufügen](http://nuget.codeplex.com/workitem/23)
* [Hash-Angriff auf den Feed nach dem Download des Pakets überprüfen](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

Es folgen die wichtigsten Änderungen in CTP 2:

* Das Paket zu einem OData-Dienst-Endpunkt aus ATOM-feed gewechselt: Wenn Sie ein auf die CTP2-Version von NuGet Upgrade, sicher, dass die folgende URL als Paketquelle hinzugefügt werden: `https://feed.nuget.org/ctp2/odata/v1/`.
* Den Befehl Add-Package umbenannt *Install-Package*.
* Aktualisiert die `.nuspec` Format. Die `.nuspec` Format enthält jetzt die *"iconUrl"* Feld zum Angeben einer 32 x 32 Png Symbol in der Paket-Dialogfeld angezeigt wird. Achten Sie daher darauf fest, um das Paket zu unterscheiden. Die `.nuspec` Format schließt außerdem die neuen *ProjectUrl* Feld, das Sie verwenden können, um zu einer Webseite zu verweisen, die Weitere Informationen zu Ihrem Paket bereitstellt.

Dieser Build funktioniert nicht mit alten `.nupkg` Dateien. Wenn Sie null-verweisausnahmen erhalten, verwenden Sie eine alte `.nupkg` Datei, und es mit den aktualisierten neu erstellen müssen [NuGet-Befehlszeilentool](http://nuget.codeplex.com/releases/52017/download/165468).

Im folgenden ist eine Liste von Funktionen und Fehlern, die für den NuGet-CTP 2 behoben wurden (schließt nicht Fehlern für kleinere Code Rowsets usw. ein).

* [Fehler beim Entpacken Paket Assemblys bei der Angabe der TargetFramework für eine Assembly.](http://nuget.codeplex.com/workitem/10)
* [NuPack Konsolenfenster mehr erkennbar machen](http://nuget.codeplex.com/workitem/14)
* [ILMerge der nupack.exe-Version](http://nuget.codeplex.com/workitem/19)
* [Eine bessere Fehler/Ausnahmebehandlung](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager sollten sauber Fehler im Zusammenhang mit dem Feed](http://nuget.codeplex.com/workitem/28)
* [Benötigen Sie ein neues Symbol für die Konsole](http://nuget.codeplex.com/workitem/29)
* [Lokalisieren von Zeichenfolgen, die im Dialogfeld "](http://nuget.codeplex.com/workitem/38)
* [NuPack Caches heruntergeladene .nupack-Dateien im Arbeitsspeicher](http://nuget.codeplex.com/workitem/40)
* [NuPack-Konsole: Ändern Sie die Standardtastenkombination zum Anzeigen der Konsole](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem sollte Standardwerte für allgemeine Eigenschaften unterstützen.](http://nuget.codeplex.com/workitem/49)
* [Bei der Ausführung nupack.exe in einem Ordner mit nur einem Nuspec-Datei sollte diese Nuspec verwenden](http://nuget.codeplex.com/workitem/52)
* [Menüs "Projekt" angezeigt wird, wird auch angezeigt, wenn kein Projekt/Projektmappe geladen wird](http://nuget.codeplex.com/workitem/54)
* [Build.cmd schlägt fehl, auf eine fehlerfreie Klon die Codebasis nutzen](http://nuget.codeplex.com/workitem/56)
* [Verfügbare Updates-feature](http://nuget.codeplex.com/workitem/57)
* [Dialogfeld ": Hinzufügen eines Pakets über das Dialogfeld die Aufforderung entfernt, in der Konsole](http://nuget.codeplex.com/workitem/73)
* [Hinzufügen eines Pakets, indem Sie auf "Installieren" wird häufig langsam, keine visuelle Bestätigung](http://nuget.codeplex.com/workitem/80)
* [Es gibt keine Möglichkeit zum Ermitteln von meinem installierten Pakete den Updates aufweisen.](http://nuget.codeplex.com/workitem/82)
* [Es gibt keine Möglichkeit zum Aktualisieren von einem installierten Paket im Dialogfeld "".](http://nuget.codeplex.com/workitem/83)
* [Es gibt keine Möglichkeit zum Deinstallieren von einem installierten Paket im Dialogfeld ""](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Fügen Sie Paket Verweis&hellip; &rdquo; von installierten verweisen Sie im Kontextmenü angezeigt wird](http://nuget.codeplex.com/workitem/85)
* [Nach der Aktualisierung eines Pakets aus der Konsole, zeigt er die alte Version und die neue Version installiert](http://nuget.codeplex.com/workitem/86)
* [Die Aktivität in der Konsole, wenn das Dialogfeld mit verschwindet nach Verwendung](http://nuget.codeplex.com/workitem/87)
* [Analysieren von im nupack.exe Cleanup-Befehlszeile](http://nuget.codeplex.com/workitem/89)
* [Fügen Sie einen Anzeigenamen zu Paketquellen](http://nuget.codeplex.com/workitem/98)
* [Aktualisieren von .nuspec einschließlich Paketsymbole unterstützt.](http://nuget.codeplex.com/workitem/103)
* [Feed UI lässt nicht die URL kopieren](http://nuget.codeplex.com/workitem/105)
* [Eine bessere Remove-Package-Fehlerbehandlung.](http://nuget.codeplex.com/workitem/107)
* [Geben Sie im Konsolenfenster, hängt davon ab, den Fokus Cursors](http://nuget.codeplex.com/workitem/112)
* [Fehlermeldungen suchen unsinnig](http://nuget.codeplex.com/workitem/116)
* [Die Leistung des entfernen-Pakets für ein Paket, das nicht installiert ist, ist ungültig.](http://nuget.codeplex.com/workitem/117)
* [Entfernen eines Pakets schlägt fehl, wenn es keine Paketquellen sind](http://nuget.codeplex.com/workitem/119)
* [Remove-Paket scheitert, wenn die Paketquelle nicht verfügbar ist.](http://nuget.codeplex.com/workitem/120)
* [Fügen Sie Titel aus, um die Metadaten von Paketen und den Feed hinzu.](http://nuget.codeplex.com/workitem/125)
* [Hinzufügen des - Source-Parameters an Add-Package](http://nuget.codeplex.com/workitem/127)
* [Liste Paket müssen einen "Quelle"-Parameter](http://nuget.codeplex.com/workitem/128)
* [Aktualisieren von NuPack.Server dahingehend NuPack Benutzer-Agent zum Paket herunterladen](http://nuget.codeplex.com/workitem/142)
* [Dialogfeld zum Akzeptieren von Lizenzbedingungen muss Lizenzen für alle Abhängigkeiten aufgelistet, die Zustimmung erforderlich ist.](http://nuget.codeplex.com/workitem/145)
* [Schreibt einen Fehler aus, wenn ein Paket im Feed auslöst](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe nicht möglich, eine leere &lt;"licenseUrl"&gt; Element](http://nuget.codeplex.com/workitem/152)
* [Benennen Sie die Liste-Paket in Get-Package, Add-Package Install-Package und Remove-Package zu Uninstall-Package](http://nuget.codeplex.com/workitem/155)
* [Über das Menüelement "Paket-Verweis hinzufügen" aus dem Projektmappen-Navigator stürzt Visual Studio ab.](http://nuget.codeplex.com/workitem/158)
* [Bezeichnung "verfügbaren Paketquellen" fehlt einen Doppelpunkt](http://nuget.codeplex.com/workitem/160)
* [Stellen Sie .nuspec XML-Element Groß-/Kleinschreibung einheitlich Kamel falscher Groß-/Kleinschreibung](http://nuget.codeplex.com/workitem/161)
* [Die NuPack VSIX-Manifest muss so aktivieren Sie das Bit "Admin"](http://nuget.codeplex.com/workitem/162)
* [Wenn Sie keine Feeds Liste-Paket ausführen, erhalten Sie null Ref-Fehler](http://nuget.codeplex.com/workitem/164)
* [NuGet.exe: Zielpfad angeben](http://nuget.codeplex.com/workitem/171)
* [PowerShell-Fehler beim Öffnen von Paket-Verwaltungskonsole auf WinXP](http://nuget.codeplex.com/workitem/175)
* [Visual Studio stürzt beim Laden der Liste der Pakete](http://nuget.codeplex.com/workitem/176)
* [Damit Meta-Pakete (keine Dateien, sondern nur Abhängigkeiten)](http://nuget.codeplex.com/workitem/180)
* [Konvertieren eines Powershell-Skripts in Powershell 2.0-Moduls](http://nuget.codeplex.com/workitem/181)
* [Beim Ziel angegeben ist, sollten PathResolver Pfad Teil jeweils vorgehenden Platzhalterzeichen verwerfen.](http://nuget.codeplex.com/workitem/183)
* [Keine Abhängigkeiten](http://nuget.codeplex.com/workitem/186)
* [Fehler beim Installieren des Elmah](http://nuget.codeplex.com/workitem/192)
* [Config-Transformationen nicht ordnungsgemäß mit &lt;"configSections"&gt;](http://nuget.codeplex.com/workitem/194)
* [Die Variable "$globale: ProjectCache" kann nicht abgerufen werden, da es nicht festgelegt wurde](http://nuget.codeplex.com/workitem/203)
* [Fügen Sie MSBuild-Aufgabe zum Erstellen von Paketen NuPack hinzu](http://nuget.codeplex.com/workitem/205)
* [Liste-Paket muss zur Unterstützung von Suchen/filtern](http://nuget.codeplex.com/workitem/206)
* [Einen Link immer mit der Lizenz angezeigt wird, wenn Paketersteller eine Lizenz-URL enthält](http://nuget.codeplex.com/workitem/208)
* [Gelegentlich "Zugriff verweigert"-Ausnahme mit Remove-Paket](http://nuget.codeplex.com/workitem/213)
* [Komponententests fehlschlagen: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Zulassen Sie für ein Fallback/Standardsatz von Dateien, wenn eine spezifische Framework-Version nicht gefunden werden kann](http://nuget.codeplex.com/workitem/223)
* [Paket-Verweis hinzufügen... UI kann kein Paket entfernt werden.](http://nuget.codeplex.com/workitem/225)
* [Hinzufügen von Paket Verweis abstürzt Studio, wenn eine oder mehrere Projekt wird entladen](http://nuget.codeplex.com/workitem/228)
* [Konfigurationstransformation scheint nicht auf die Datei "Web.Debug.config" arbeiten](http://nuget.codeplex.com/workitem/229)
* [init.ps1 nicht auf benutzerdefinierte Paket ausgelöst.](http://nuget.codeplex.com/workitem/237)
* [Beim Hinzufügen von Pfaden zu den "feedlist" hinzugefügt, wird die Standardschaltfläche auf "OK", festgelegt, wenn ich die EINGABETASTE drücken sie automatisch geschlossen wird](http://nuget.codeplex.com/workitem/240)
* [So deinstallieren Sie versuchen eine Abhängigkeit stürzt VS 2 Mal versucht, in einer Zeile](http://nuget.codeplex.com/workitem/241)
* [Die Projekt-URL in das Dialogfeld "Paket hinzufügen" angezeigt](http://nuget.codeplex.com/workitem/253)
* [Das Dialogfeld "Add-Package", um installierte Pakete Standard](http://nuget.codeplex.com/workitem/254)
* [Paket-Dialogfeld hinzufügen Menüelement zu ändern.](http://nuget.codeplex.com/workitem/261)
* [Umbenennen von Namespaces und Assemblys](http://nuget.codeplex.com/workitem/274)
* [Benennen Sie das Projekt NuPack zu NuGet](http://nuget.codeplex.com/workitem/282)
* [Fügen Sie den folgenden Text unter der Liste der Abhängigkeiten](http://nuget.codeplex.com/workitem/288)
* [Ändern Sie den Lizenzbedingungen akzeptieren Text in das Dialogfeld zum Akzeptieren der Lizenz](http://nuget.codeplex.com/workitem/291)
* [Ändern Sie den Text in das Dialogfeld zum Akzeptieren der Lizenz über der Liste der Pakete](http://nuget.codeplex.com/workitem/292)
* [OData funktioniert nicht mit einer URL fwlink](http://nuget.codeplex.com/workitem/304)
* [Paket-Manager-UI: über aggressives caching der Paket-Anzahl für das Paging verwendete](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet -&gt; Package Manager Console-Fehler](http://nuget.codeplex.com/workitem/335)
* [Das Hinzufügen eines Pakets Dialogfeld Lizenz Zustimmung für bereits installierte verpackt angezeigt.](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

Im folgenden finden eine Liste von Funktionen und Fehlern, die für den NuGet-CTP 1 behoben wurden.

* [Paketerweiterung sollte in .nupack umbenannt werden](http://nuget.codeplex.com/workitem/1)
* [Verschieben Sie die Paketdatei in Ordner](http://nuget.codeplex.com/workitem/2)
* [Merge installieren &amp; hinzufügen PS-Befehlen](http://nuget.codeplex.com/workitem/3)
* [Erstellen von Aliasen für Verb-Substantiv-cmdlets](http://nuget.codeplex.com/workitem/4)
* [NuPack ruft verwechselt werden, beim Wechseln von Projektmappen in Visual Studio](http://nuget.codeplex.com/workitem/6)
* [Es sollte "Pakete" Projektmappenordner standardmäßig ausgeblendet.](http://nuget.codeplex.com/workitem/11)
* [Hinzufügen von Unterstützung für den Austausch von token in Inhaltselemente.](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI sollten die PackageSource-API verwenden.](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager markiert Pakete aus, als vor der Installation installiert](http://nuget.codeplex.com/workitem/27)
* [Löschen von Standardprojekt Lösung zeigt gelöschten Projekts immer noch als Standard](http://nuget.codeplex.com/workitem/30)
* [Neues Paket schlägt fehl mit "Teil kann nicht für den angegebenen URI hinzugefügt werden, da es bereits im Paket enthalten ist."](http://nuget.codeplex.com/workitem/32)
* [Entfernen Sie "NuPack" Zeichenfolgen von Visual Studio-Benutzeroberfläche](http://nuget.codeplex.com/workitem/35)
* [Apache-Header um ein COPYRIGHT.txt-Datei hinzufügen](http://nuget.codeplex.com/workitem/36)
* [Entfernen Sie die Update-PackageSource-Befehl](http://nuget.codeplex.com/workitem/37)
* [Paket-Manager kann nicht verwendet werden, beim Laden des Profils löst eine Ausnahme aus.](http://nuget.codeplex.com/workitem/39)
* [init.ps1 "," ps1 "und" ps1 müssen zusätzliche Zustände empfangen](http://nuget.codeplex.com/workitem/41)
* [Kombinieren von Konsole und GUI-Pakete in ein Paket](http://nuget.codeplex.com/workitem/42)
* [XML-Transformation Logik funktioniert nicht, wenn auf XML angewendet, die nicht im Stammverzeichnis](http://nuget.codeplex.com/workitem/43)
* [Verwalten Sie Paket Quellen Einstellungendialogfeld keine Aktualisierung der Konsole NuPack ""](http://nuget.codeplex.com/workitem/44)
* [NuPack Konsole UI: Benennen Sie "Feed-Paket" Dropdown-Liste "Paketquelle"](http://nuget.codeplex.com/workitem/45)
* [NuPack Konsolenoptionen: Umbenennen Sie 'Repository UI' konsistent mit NuPack-Konsole](http://nuget.codeplex.com/workitem/46)
* [Paket hinzufügen, die für eine Website, die von IIS oder eine URL geöffnet wurde schlägt fehl](http://nuget.codeplex.com/workitem/53)
* [Paket-Manager-Quelle funktioniert nicht mit FwLink](http://nuget.codeplex.com/workitem/55)
* [Die Paketquelle an Standardeinstellung festlegen](http://nuget.codeplex.com/workitem/59)
* [Beim Hinzufügen von Paketquellen Option, wenn nur eine Quelle angegeben wird, wird davon ausgegangen Sie, dass dies die Standardeinstellung ist.](http://nuget.codeplex.com/workitem/60)
* [Die Benutzeroberfläche für Dialogfeld zeigt gefälschte "Letzte" Pakete](http://nuget.codeplex.com/workitem/62)
* [Optionen: Sie auf "Abbrechen" nicht Änderungen abgebrochen](http://nuget.codeplex.com/workitem/63)
* [Das Hinzufügen eines Pakets Verweis Dialogfeld Suche Groß-/Kleinschreibung beachtet werden soll](http://nuget.codeplex.com/workitem/65)
* [Korrigieren Sie Unternehmens-Metadaten in der AssemblyInfo.cs-Dateien](http://nuget.codeplex.com/workitem/67)
* [Die Versionsnummer für VSIX](http://nuget.codeplex.com/workitem/71)
* [Remove-Package: Mithilfe von-? Zeigt die Hilfe zweimal](http://nuget.codeplex.com/workitem/72)
* [Führen Sie Pakete installieren/deinstallieren, für die Ebene Projektpakete](http://nuget.codeplex.com/workitem/74)
* [Der Server keine Feed erstellen, bei einem Überprüfungsfehler eine nupack](http://nuget.codeplex.com/workitem/90)
* [Ersetzen Sie NuPack Symbole müssen](http://nuget.codeplex.com/workitem/94)
* [NTLM-HTTP-Proxy authentifiziert sich nicht auf das Paket mit dem feed.](http://nuget.codeplex.com/workitem/96)
* [Das Dialogfeld "ist nicht immer zentriert im VS-Fenster starten](http://nuget.codeplex.com/workitem/100)
* [Viele der Felder in einem Details Pakete werden nicht im Dialogfeld "" aufgefüllt wird](http://nuget.codeplex.com/workitem/102)
* [Dialogfeld-Benutzeroberfläche Namen Autoren nicht angezeigt werden.](http://nuget.codeplex.com/workitem/108)
* [Warum - Version für Remove-Paket](http://nuget.codeplex.com/workitem/113)
* [Entfernen Sie die Registerkarte "Aktuell" auf der Benutzeroberfläche für Dialogfeld](http://nuget.codeplex.com/workitem/115)
* [VS-Absturzes, wenn rechts klicken Sie auf auf Projektmappenordner nach dem Öffnen der Benutzeroberfläche für Dialogfeld mindestens ein.](http://nuget.codeplex.com/workitem/126)
* [Change - lokalen Parameter Liste-Pakets in - installiert](http://nuget.codeplex.com/workitem/129)
* [Benennen Sie packages.xml in NuPack.config](http://nuget.codeplex.com/workitem/132)
* [Konsole erzwingt Cursor am Ende der Zeile](http://nuget.codeplex.com/workitem/135)
* [Remove-Package Intellisense ist fehlerhaft](http://nuget.codeplex.com/workitem/136)
* [.Nuspec und Feed RequireLicenseAcceptance Flag hinzufügen](http://nuget.codeplex.com/workitem/137)
* [Das Hinzufügen eines "licenseUrl" für .nuspec-Format und das Paket Feed](http://nuget.codeplex.com/workitem/138)
* [Klicken auf die Installation des Pakets, die Akzeptanz erfordert sollte das Dialogfeld zum akzeptieren anzeigen.](http://nuget.codeplex.com/workitem/139)
* [Fügen Sie Haftungsausschluss-hinzu, um das Paket "hinzufügen"](http://nuget.codeplex.com/workitem/140)
* [Das Hinzufügen eines Haftungsausschluss bei der Paket-Konsole erstmalig ausgeführt wird](http://nuget.codeplex.com/workitem/143)
* [Zeigen Sie Haftungsausschluss nach der Installation des Pakets In der Konsole an](http://nuget.codeplex.com/workitem/144)
* [Benennen Sie die .nupack auf .nupkg](http://nuget.codeplex.com/workitem/146)