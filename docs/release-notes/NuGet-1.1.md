---
title: Anmerkungen zu NuGet 1.0 und 1.1
description: Anmerkungen zu NuGet 1.1, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6222a996f2fdcaaa81a1b16d1c6da2749936712a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547020"
---
# <a name="nuget-10-and-11-release-notes"></a>Anmerkungen zu NuGet 1.0 und 1.1

[Anmerkungen zu NuGet Version 1.2](../release-notes/nuget-1.2.md)

NuGet 1.0 wurde am 13 Januar 2011 veröffentlicht.  NuGet 1.1 wurde am 12. Februar 2011 veröffentlicht.

## <a name="overview"></a>Übersicht

Dieses Dokument enthält die Versionshinweise für die verschiedenen Versionen von NuGet 1.0 gruppiert nach wichtigen Preview-Version.

NuGet schließt die folgenden Komponenten:

* *NuGet.Tools.vsix* * die besteht aus:
  * **Library-Paket-Dialogfeld "hinzufügen"** * Dialogfeld in Visual Studio zum Suchen und Installieren von Paketen verwendet.
  * **Paket-Manager-Konsole** * Powershell-basierte Konsole in Visual Studio.
* *NuGet-Befehlszeilentools* * Tool verwendet, um Pakete zu erstellen (und später veröffentlicht).

Die NuGet-Tools für Visual Studio-Erweiterung (*NuGet.Tools.vsix*) erfordert:

* Visual Studio 2010 noch Visual Web Developer 2010 Express.

Das NuGet-Befehlszeilentool ist erforderlich:

* .NET Framework, Version 4

## <a name="installation"></a>Installation

Dieses [neueste Version](http://nuget.codeplex.com/releases/view/52018):

* Deinstallieren Sie zunächst Ihre älteren Build. Sie müssen Visual Studio als Administrator dazu ausführen.
* Entfernen Sie alle vorhandenen Feeds, die Sie haben.
* Hinzufügen ein neues Feeds auf [ http://go.microsoft.com/fwlink/?LinkId=206669 ](http://go.microsoft.com/fwlink/?LinkId=206669).

## <a name="nuget-11"></a>NuGet 1.1

Die Liste der Probleme, die in diesem Release behobene [finden Sie hier.](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>RTM von NuGet 1.0

Da die RC-Version wurde ein Fehler RTM-Version behoben.

* [: 474 Entfernen von Paketen betrifft jedoch alle Projekte In der Lösung](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Release Candidate

Im folgenden werden die Änderungen, die in diesem Release Candidate seit der CTP-Version 2. Besuchen Sie die Problemverfolgung, um die vollständige Liste von Fehlern finden Sie unter.

* [Aktualisieren eines Pakets aus der Konsole werden Abhängigkeiten nicht aktualisiert werden.](http://nuget.codeplex.com/workitem/443)
* [Hinzufügen von Paket übernimmt "bin" Paketverweis nicht (CTP1)](http://nuget.codeplex.com/workitem/442)
* [Aktualisieren eines Pakets bleibt fehlerhafte verweisen](http://nuget.codeplex.com/workitem/440)
* [Get-Package-Updates ein Fehler auftritt, im Dialogfeld, oder wenn die Quelle "Alle" aggregate in der Konsole aktiviert ist](http://nuget.codeplex.com/workitem/439)
* [Abrufen der Paket-Überprüfungsfehler](http://nuget.codeplex.com/workitem/426)
* [Benutzer zu warnen, wenn ein Paket über das Dialogfeld "Paket-" installiert werden können](http://nuget.codeplex.com/workitem/425)
* [Get-Package-löst aktualisiert, wenn große Anzahl von Paketen aktualisieren](http://nuget.codeplex.com/workitem/424)
* [Verbesserung der Fehlerbehandlung, wenn die Nuspec-Dateien nicht ordnungsgemäß erstellt werden](http://nuget.codeplex.com/workitem/423)
* [NuGet Pack ignoriert die angegebene Dateien](http://nuget.codeplex.com/workitem/422)
* [Entfernen die Quelle des zweiten bis letzten, und klicken Sie dann auf "Nach unten" stürzt Visual Studio](http://nuget.codeplex.com/workitem/418)
* [Assemblyverweis zu entfernen, während der Installation von Paketen](http://nuget.codeplex.com/workitem/413)
* ["InvalidOperationException" beim Dialogfeld "Einstellungen" Öffnen](http://nuget.codeplex.com/workitem/411)
* [Zugriffsschlüssel für die Paketquelle in die Paket-Manager-Konsole funktioniert nicht](http://nuget.codeplex.com/workitem/410)
* [NuGet Visual Studio-Einstellungen Dialogfeld Zugriffsschlüssel legen den Fokus auf falsche Felder](http://nuget.codeplex.com/workitem/409)
* [Paket-ID Intellisense sollten nicht zu viele Elemente Abfragen.](http://nuget.codeplex.com/workitem/404)
* [Fehler beim Hinzufügen des Pakets zum Projekt mit einem Punkt in den Namen des Projekts](http://nuget.codeplex.com/workitem/403)
* [Problem mit der angegebenen Dateien in NuSpec-Datei](http://nuget.codeplex.com/workitem/400)
* [Richtige offizielle Feed muss registriert werden, bei Verwendung der neueren build](http://nuget.codeplex.com/workitem/399)
* [Tags sollten Leerzeichen anstelle von # verwenden](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata fehlen einige nützliche Informationen.](http://nuget.codeplex.com/workitem/388)
* [Fügen Sie diesen Link, um das Dialogfeld](http://nuget.codeplex.com/workitem/386)
* [App_Data verwenden, um Unterbrechungen der Pakete in Visual Studio zu entpacken](http://nuget.codeplex.com/workitem/380)
* [Implementieren von Tags](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder ermöglicht, leeres Paket ohne Abhängigkeiten erstellt werden](http://nuget.codeplex.com/workitem/373)
* [Feld "Besitzer" für das Paket hinzufügen](http://nuget.codeplex.com/workitem/365)
* [Aktualisieren Sie das VSIX-Manifest, NuGet-Paket-Manager anstelle des VSIX-Tools, z. B.](http://nuget.codeplex.com/workitem/364)
* [Befehl "Get-Package" löst Fehler aus, wenn alle Quellen ausgewählt ist](http://nuget.codeplex.com/workitem/359)
* [Ermöglichen Sie die Reihenfolge der Paketquellen im Dialogfeld "Optionen"](http://nuget.codeplex.com/workitem/356)
* [Update-Package wird ältere Version nicht entfernt werden.](http://nuget.codeplex.com/workitem/352)
* [Implementieren von Version Bereichsspezifikation für Abhängigkeiten](http://nuget.codeplex.com/workitem/347)
* [Visual Studio stürzt ab, wenn Sie auf "Neues Paket hinzufügen"](http://nuget.codeplex.com/workitem/346)
* [Anzeigen von Downloads und Bewertungen im Dialogfeld "Paket hinzufügen"](http://nuget.codeplex.com/workitem/345)
* [Wechseln zwischen Paketquellen im Dialogfeld für die nicht aktive Quelle aktualisiert werden.](http://nuget.codeplex.com/workitem/344)
* [Tastenzuordnung für Fenster der Paket-Manager-Konsole entfernen](http://nuget.codeplex.com/workitem/339)
* [Install-Package wird nicht als Name eines Cmdlets erkannt...](http://nuget.codeplex.com/workitem/338)
* [Installieren eines Pakets aus einer lokalen feed-Abhängigkeiten auf regelmäßigen Feeds werden nicht aufgelöst.](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies überspringen soll Abhängigkeiten, die noch verwendet werden](http://nuget.codeplex.com/workitem/331)
* [Wenn Seitennavigation abgebrochen wird, kann nicht Benutzer zu einer anderen Seite navigieren Sie während die ursprünglichen Seitenanforderung zurückgibt.](http://nuget.codeplex.com/workitem/325)
* [Überprüfen Sie Leistung NuPack.Server zum Bereitstellen von Feeds mit einer großen Anzahl von Paketen.](http://nuget.codeplex.com/workitem/324)
* [Ein zweites Mal, das ich filtern, für ein Paket wird die Paketquelle "Neu", anstelle der zuvor ausgewählten Quelle verwendet.](http://nuget.codeplex.com/workitem/321)
* [Standardpaketquelle muss ausgewählt werden, wenn Sie die Registerkarte "Online" im Dialogfeld auswählen.](http://nuget.codeplex.com/workitem/320)
* [Paketauflistung sollte standardmäßig installierten Pakete anzuzeigen.](http://nuget.codeplex.com/workitem/309)
* [Assembly-Verweis HintPaths](http://nuget.codeplex.com/workitem/294)
* [Ausnahme beim Öffnen des Paket-Manager-Konsole](http://nuget.codeplex.com/workitem/268)
* [Konsole Intellisense – die gesamte downloadfeed](http://nuget.codeplex.com/workitem/259)
* [Paketquelle "Default" muss in "Aktiv" umbenannt werden](http://nuget.codeplex.com/workitem/258)
* [Paket Datenquellen Benutzeroberfläche: dann auf OK sollte die neue Quelle hinzufügen, wenn der Name/Quellfelder nicht leer sind.](http://nuget.codeplex.com/workitem/257)
* [Dialogfeld wird extrem langsam, wenn die Anzahl der installierten Pakete groß ist](http://nuget.codeplex.com/workitem/243)
* [Unterstützung von Bindungsumleitungen für Assemblys mit starkem Namen](http://nuget.codeplex.com/workitem/238)
* [Paketverweis hinzufügen... Benutzeroberfläche, löschen Sie für die Paketquelle einschließen](http://nuget.codeplex.com/workitem/226)
* [NuPack konfigurationstransformation agnostically mit dem Namen der Config-Datei unterstützt werden müssen](http://nuget.codeplex.com/workitem/224)
* ["BasePath", um in NuPack.exe überschrieben werden können](http://nuget.codeplex.com/workitem/222)
* [Package Source Authentifizierungsfallback-Verhalten](http://nuget.codeplex.com/workitem/204)
* [Auf der grafischen Benutzeroberfläche stürzt ab](http://nuget.codeplex.com/workitem/201)
* [Sortieren die Optionen zum Hinzufügen von Paket-Dialogfeld hinzufügen](http://nuget.codeplex.com/workitem/179)
* [Tastenkombination, deaktivieren Sie die Paket-Manager-Konsole](http://nuget.codeplex.com/workitem/174)
* [Bewirkt, dass PowerConsole NuPack Konsole fehlschlägt](http://nuget.codeplex.com/workitem/166)
* [Konsole und die Paket-Dialogfeld hinzufügen sollten Benutzer-Agent in Anforderungen festlegen.](http://nuget.codeplex.com/workitem/141)
* [Legen Sie die Versionsnummer der VSIX und NuPack.exe im Build.](http://nuget.codeplex.com/workitem/134)
* [Ausblenden von allgemeinen PowerShell-Parameter von-?](http://nuget.codeplex.com/workitem/118)
* [Fügen Sie hinzu – detaillierte Hilfe für Befehle-Konsole](http://nuget.codeplex.com/workitem/110)
* [Fügen Sie, dass das Paket Dialogfeld zulassen soll die aktuellen Paketquelle auswählen](http://nuget.codeplex.com/workitem/88)
* [Verschieben von NuPack.Core Klassen in verschiedene namespaces](http://nuget.codeplex.com/workitem/50)
* [Hilfe zu Cmdlets hinzufügen](http://nuget.codeplex.com/workitem/23)
* [Hash-Angriff auf den Feed heruntergeladene Paket überprüfen](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

Im folgenden sind die wichtigsten Änderungen, die in CTP 2 vorgenommen:

* Wechseln Sie das Paket auf einen OData-Dienstendpunkt aus ATOM-feed: Wenn Sie auf die CTP2-Version von NuGet aktualisieren, werden Sie sicher, dass die folgende URL als Paketquelle hinzufügen: `https://feed.nuget.org/ctp2/odata/v1/`.
* Die Add-Package-Befehl aus, um umbenannt *Install-Package*.
* Aktualisiert die `.nuspec` Format. Die `.nuspec` Format enthält jetzt die *"iconUrl"* Feld für die Angabe ein 32 x 32 Png-Symbol in das Dialogfeld "Paket hinzufügen" angezeigt werden. Achten Sie also darauf festlegen, um das Paket zu unterscheiden. Die `.nuspec` Format schließt außerdem das neue *URLs "projectUrl"* Feld, das Sie verwenden können, um zu einer Webseite zu verweisen, die Weitere Informationen zu Ihrem Paket enthält.

Dieser Build funktioniert nicht mit alten `.nupkg` Dateien. Wenn Sie null-verweisausnahmen erhalten, verwenden Sie eine alte `.nupkg` Datei, und müssen es neu erstellen, mit der aktualisierten [NuGet-Befehlszeilentools](http://nuget.codeplex.com/releases/52017/download/165468).

Im folgenden finden eine Liste der Features und Fehler, die für NuGet CTP 2 behoben wurden (die Fehler für kleinere Code Bereinigungen usw. werden nicht berücksichtigt werden.).

* [Fehler beim Entpacken des paketassemblys Wenn bei der Angabe der TargetFramework für eine Assembly.](http://nuget.codeplex.com/workitem/10)
* [NuPack Konsolenfenster leichter auffindbar machen](http://nuget.codeplex.com/workitem/14)
* [ILMerge der nupack.exe-Version](http://nuget.codeplex.com/workitem/19)
* [Bessere Fehler/Ausnahmebehandlung](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager sollten ordnungsgemäß behandelt werden Fehler im Zusammenhang mit Feed](http://nuget.codeplex.com/workitem/28)
* [Benötigen Sie ein neues Symbol für die Konsole](http://nuget.codeplex.com/workitem/29)
* [Lokalisieren von Zeichenfolgen in das Dialogfeld "](http://nuget.codeplex.com/workitem/38)
* [NuPack Caches heruntergeladene .nupack-Dateien im Arbeitsspeicher](http://nuget.codeplex.com/workitem/40)
* [NuPack-Konsole: Ändern Sie die Standard-Verknüpfung für die Anzeige der Konsole](http://nuget.codeplex.com/workitem/48)
* [Project System sollte Standardwerte für allgemeine Eigenschaften unterstützen.](http://nuget.codeplex.com/workitem/49)
* [Ausführen von nupack.exe in einem Ordner mit nur einer Nuspec-Datei sollte dieses NuSpec-Element verwenden.](http://nuget.codeplex.com/workitem/52)
* [Menü "Projekt" angezeigt wird, wird auch angezeigt, wenn kein Projekt/Projektmappe geladen wird](http://nuget.codeplex.com/workitem/54)
* [Build.cmd ein Fehler auf einem sauberen Klon der Codebasis auftritt.](http://nuget.codeplex.com/workitem/56)
* [Verfügbares Feature für Updates](http://nuget.codeplex.com/workitem/57)
* [Dialogfeld ": Hinzufügen eines Pakets über das Dialogfeld wird die Eingabeaufforderung in der Konsole entfernt](http://nuget.codeplex.com/workitem/73)
* [Hinzufügen eines Pakets durch Klicken auf "Installieren" ist häufig langsam, kein visuelles Feedback](http://nuget.codeplex.com/workitem/80)
* [Es ist keine Möglichkeit zum Ermitteln, welche meiner installierten Pakete Updates haben.](http://nuget.codeplex.com/workitem/82)
* [Es gibt keine Möglichkeit zum Aktualisieren von eines installierten Pakets im Dialogfeld.](http://nuget.codeplex.com/workitem/83)
* [Es gibt keine Möglichkeit zum Deinstallieren von eines installierten Pakets im Dialogfeld ""](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Hinzufügen des Paketverweises&hellip; &rdquo; angezeigt wird, klicken Sie im Kontextmenü der installierten Verweise](http://nuget.codeplex.com/workitem/85)
* [Nach der Aktualisierung eines Pakets aus der Konsole zeigt er sowohl die alte Version und die neue Version installiert](http://nuget.codeplex.com/workitem/86)
* [Die Aktivität in der Konsole, die bei Verwendung der im Dialogfeld nicht mehr angezeigt, nach der Verwendung](http://nuget.codeplex.com/workitem/87)
* [Analysieren von im nupack.exe Cleanup-Befehlszeile](http://nuget.codeplex.com/workitem/89)
* [Fügen Sie einen Anzeigenamen Paketquellen](http://nuget.codeplex.com/workitem/98)
* [Aktualisieren der NuSpec, einschließlich der Symbole für Bereitstellungspakete unterstützen](http://nuget.codeplex.com/workitem/103)
* [Feed-Benutzeroberfläche gestattet nicht die URL kopieren](http://nuget.codeplex.com/workitem/105)
* [Eine bessere Remove-Package-Fehlerbehandlung.](http://nuget.codeplex.com/workitem/107)
* [Im Konsolenfenster eingeben, hängt davon ab, den Cursorfokus](http://nuget.codeplex.com/workitem/112)
* [Sehen Sie Fehlermeldungen sehr häufig](http://nuget.codeplex.com/workitem/116)
* [Die Leistung des entfernen-Pakets für ein Paket, das nicht installiert ist, ist ungültig.](http://nuget.codeplex.com/workitem/117)
* [Entfernen eines Pakets schlägt fehl, wenn es keine Paketquellen sind](http://nuget.codeplex.com/workitem/119)
* [Remove-Paket scheitert, wenn die Paketquelle nicht verfügbar ist.](http://nuget.codeplex.com/workitem/120)
* [Fügen Sie Titel, der die Metadaten von Paketen und den Feed hinzu.](http://nuget.codeplex.com/workitem/125)
* [Hinzufügen des - Source-Parameters an Add-Package](http://nuget.codeplex.com/workitem/127)
* [Paketauflistung müssen einen "Quelle"-Parameter](http://nuget.codeplex.com/workitem/128)
* [Update NuPack.Server NuPack Benutzer-Agent zum Download-Paket erforderlich ist.](http://nuget.codeplex.com/workitem/142)
* [Dialogfeld zum Akzeptieren der Lizenz muss Lizenzen für alle Abhängigkeiten auflisten, die akzeptiert werden](http://nuget.codeplex.com/workitem/145)
* [Ein Fehler protokolliert, wenn ein Paket im Feed auslöst.](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe sollte ein leeres nicht gestatten &lt;"licenseUrl"&gt; Element](http://nuget.codeplex.com/workitem/152)
* [Benennen Sie die Liste-Paket in Get-Package, Add-Package-Installationspaket und Remove-Package, Uninstall-Package](http://nuget.codeplex.com/workitem/155)
* [Über das Menüelement "Paket-Verweis hinzufügen" aus dem Projektmappen-Navigator stürzt Visual Studio](http://nuget.codeplex.com/workitem/158)
* [Bezeichnung für "Verfügbare Paketquellen" fehlt einen Doppelpunkt](http://nuget.codeplex.com/workitem/160)
* [Stellen Sie .NuSpec-Datei XML-Element Groß-/Kleinschreibung einheitlich Camel-Case Groß-/Kleinschreibung](http://nuget.codeplex.com/workitem/161)
* [Die NuPack VSIXs-Manifest muss das Bit 'Admin' aktivieren](http://nuget.codeplex.com/workitem/162)
* [Wenn Sie Liste-Paket mit kein Feeds ausführen, erhalten Sie null-Verweis-Fehler](http://nuget.codeplex.com/workitem/164)
* [NuGet.exe: Zielpfad angeben](http://nuget.codeplex.com/workitem/171)
* [Öffnen die Paketverwaltungskonsole unter WinXP PowerShell-Fehler](http://nuget.codeplex.com/workitem/175)
* [Visual Studio-Abstürze beim Laden der Paketliste](http://nuget.codeplex.com/workitem/176)
* [Damit Meta-Pakete (keine Dateien, nur die Abhängigkeiten)](http://nuget.codeplex.com/workitem/180)
* [Konvertieren eines Powershell-Skripts in Powershell 2.0-Modul](http://nuget.codeplex.com/workitem/181)
* [PathResolver sollten Pfad-Teil vorherigen Platzhalterzeichen zu verwerfen, wenn Ziel angegeben wird](http://nuget.codeplex.com/workitem/183)
* [Keine Abhängigkeiten](http://nuget.codeplex.com/workitem/186)
* [Fehler beim Installieren von Elmah](http://nuget.codeplex.com/workitem/192)
* [Konfigurationstransformationen nicht ordnungsgemäß funktionieren, mit &lt;Configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [Die Variable "$globale: ProjectCache' kann nicht abgerufen werden, da es nicht festgelegt wurde](http://nuget.codeplex.com/workitem/203)
* [Fügen Sie MSBuild-Aufgabe zum Erstellen von NuPack Paketen hinzu](http://nuget.codeplex.com/workitem/205)
* [Liste-Paket muss Such-/Filterfunktionen unterstützen](http://nuget.codeplex.com/workitem/206)
* [Einen Link immer Lizenz angezeigt wird, wenn der Autor des Pakets eine Lizenz-URL enthält](http://nuget.codeplex.com/workitem/208)
* [Gelegentlich "Zugriff verweigert"-Ausnahme mit Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Unit Tests treten Fehler auf: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Zulassen Sie für ein Fallback/Standardsatz von Dateien, wenn eine bestimmte Framework-Version nicht gefunden werden kann](http://nuget.codeplex.com/workitem/223)
* [Paketverweis hinzufügen... Benutzeroberfläche kann kein Paket entfernt werden.](http://nuget.codeplex.com/workitem/225)
* [Hinzufügen von Paketverweisen abstürzt, Studio, wenn eine oder mehrere Projekt entladen wird](http://nuget.codeplex.com/workitem/228)
* [Konfigurationstransformation erscheint in der Datei "web.debug.config" funktioniert nicht](http://nuget.codeplex.com/workitem/229)
* [init.ps1 benutzerdefinierten Paket wird nicht ausgelöst.](http://nuget.codeplex.com/workitem/237)
* [Beim Hinzufügen von Pfaden zu den Feedlist ist die Schaltfläche "Standard" auf "OK", festgelegt, sodass Wenn ich die EINGABETASTE drücken sie automatisch geschlossen wird](http://nuget.codeplex.com/workitem/240)
* [Versucht, deinstallieren Sie eine Abhängigkeit stürzt Visual Studio, wenn in einer Zeile 2 Mal zu versuchen](http://nuget.codeplex.com/workitem/241)
* [Die Projekt-URL in das Dialogfeld "Paket hinzufügen" angezeigt](http://nuget.codeplex.com/workitem/253)
* [Das Dialogfeld "Add-Package", um die installierten Pakete Standard](http://nuget.codeplex.com/workitem/254)
* [Ändern Sie die Menüelement-Paket-Dialogfeld hinzufügen.](http://nuget.codeplex.com/workitem/261)
* [Umbenennen von Namespaces und Assemblys](http://nuget.codeplex.com/workitem/274)
* [Benennen Sie das NuPack-Projekt auf NuGet](http://nuget.codeplex.com/workitem/282)
* [Fügen Sie den folgenden Text in der Liste der Abhängigkeiten](http://nuget.codeplex.com/workitem/288)
* [Ändern Sie den Lizenzbedingungen akzeptieren Text in das Dialogfeld "Zustimmung zur Lizenz"](http://nuget.codeplex.com/workitem/291)
* [Ändern Sie den Text in das Dialogfeld "Zustimmung zur Lizenz" über der Liste der Pakete](http://nuget.codeplex.com/workitem/292)
* [OData funktioniert mit einer URL Fwlink nicht](http://nuget.codeplex.com/workitem/304)
* [Paket-Manager-UI: über der Anzahl der Pakete für das Paging verwendete aggressives caching](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet -&gt; Package Manager Console-Fehler](http://nuget.codeplex.com/workitem/335)
* [Fügen Sie, dass Paket Dialogfeld Lizenz akzeptieren für bereits installierte verpackt angezeigt wird.](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

Im folgenden finden eine Liste der Features und Fehler, die für NuGet CTP 1 behoben wurden.

* [Paket-Erweiterung sollte in .nupack umbenannt werden](http://nuget.codeplex.com/workitem/1)
* [Paket-Datei in Ordner verschieben](http://nuget.codeplex.com/workitem/2)
* [Zusammenführen von Installation &amp; hinzufügen PS-Befehlen](http://nuget.codeplex.com/workitem/3)
* [Erstellen von Aliasen für Verb-Nomen-cmdlets](http://nuget.codeplex.com/workitem/4)
* [NuPack ruft verwechselt, beim Wechseln von Projektmappen in Visual Studio](http://nuget.codeplex.com/workitem/6)
* [Wir sollten den Projektmappenordner "Pakete" standardmäßig ausblenden.](http://nuget.codeplex.com/workitem/11)
* [Fügen Sie Unterstützung für die tokenersetzung in Elemente hinzu.](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI sollten die API "packagesource" verwenden.](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager markiert Pakete aus, als vor der Installation werden installiert](http://nuget.codeplex.com/workitem/27)
* [Löschen von Standardprojekt aus Projektmappe zeigt das gelöschte Projekt immer noch als Standard](http://nuget.codeplex.com/workitem/30)
* [Neues Paket schlägt fehl mit "Teil kann nicht für den angegebenen URI hinzugefügt werden, da er bereits im Paket enthalten ist."](http://nuget.codeplex.com/workitem/32)
* [Entfernen Sie "NuPack" Zeichenfolgen aus Visual Studio-GUI](http://nuget.codeplex.com/workitem/35)
* [Apache-Header um ein "Copyright.txt"-Datei hinzufügen](http://nuget.codeplex.com/workitem/36)
* [Befehl "Update-PackageSource" entfernen](http://nuget.codeplex.com/workitem/37)
* [Paket-Manager kann nicht verwendet werden, beim Laden des Profils löst eine Ausnahme aus.](http://nuget.codeplex.com/workitem/39)
* [init.ps1 "," Install. ps1 "und" uninstall.ps1 benötigen, um zusätzlichen Status zu erhalten.](http://nuget.codeplex.com/workitem/41)
* [Kombinieren von Konsole und GUI-Pakete in einem Paket](http://nuget.codeplex.com/workitem/42)
* [XML-Transformation Logik funktioniert nicht, wenn auf XML angewendet werden soll, die nicht im Stammverzeichnis](http://nuget.codeplex.com/workitem/43)
* [Verwalten von Paket Quellen Dialogfeld "Einstellungen" die NuPack-Konsole wird nicht aktualisiert.](http://nuget.codeplex.com/workitem/44)
* [NuPack Verwaltungskonsolen-Benutzeroberfläche: Benennen Sie "Feed-Paket" Dropdown-Liste für "Paketquelle"](http://nuget.codeplex.com/workitem/45)
* [NuPack Konsolenoptionen: Benennen Sie "Repository UI', konsistent mit NuPack-Konsole](http://nuget.codeplex.com/workitem/46)
* [Paket hinzufügen, die für eine Website, die von IIS oder eine URL geöffnet wurde schlägt fehl](http://nuget.codeplex.com/workitem/53)
* [Paket-Manager-Quelle funktioniert nicht mit FwLink](http://nuget.codeplex.com/workitem/55)
* [Legen Sie die Standardpaketquelle](http://nuget.codeplex.com/workitem/59)
* [Beim Hinzufügen von Paketquellen Option, wenn nur eine Quelle angegeben wird, wird davon ausgegangen Sie, dass dies die Standardeinstellung ist.](http://nuget.codeplex.com/workitem/60)
* [Die Benutzeroberfläche für Dialogfeld zeigt falsche "neue" Pakete](http://nuget.codeplex.com/workitem/62)
* [Optionen: Klicken Sie auf "Abbrechen" ist keine Änderungen zu verwerfen](http://nuget.codeplex.com/workitem/63)
* [Fügen Sie, dass das Paket Verweis Dialogfeld Suche berücksichtigt Groß-/Kleinschreibung werden soll](http://nuget.codeplex.com/workitem/65)
* [Korrigieren Sie die Unternehmens-Metadaten in der Datei "AssemblyInfo.cs"-Dateien](http://nuget.codeplex.com/workitem/67)
* [Die Nummer für die VSIX-Datei](http://nuget.codeplex.com/workitem/71)
* [Remove-Package: Mithilfe von-? Zeigt die Hilfe zweimal](http://nuget.codeplex.com/workitem/72)
* [Ausführen von Paketen installieren/deinstallieren, für das Projekt auf Pakete](http://nuget.codeplex.com/workitem/74)
* [Bei einem Überprüfungsfehler für ein Nupack Server kann nicht erstellt werden-feed](http://nuget.codeplex.com/workitem/90)
* [Ersetzen NuPack Symbole müssen](http://nuget.codeplex.com/workitem/94)
* [NTLM-http-Proxy wird nicht auf das Paket mit dem feed authentifiziert.](http://nuget.codeplex.com/workitem/96)
* [Starten des Dialogfelds nicht immer zentriert im Visual Studio-Fenster](http://nuget.codeplex.com/workitem/100)
* [Viele der Felder einen Pakete-Details werden nicht im Dialogfeld aufgefüllt wird](http://nuget.codeplex.com/workitem/102)
* [Dialogfeld Benutzeroberfläche Namen Autoren nicht angezeigt werden.](http://nuget.codeplex.com/workitem/108)
* [Warum - Version für die Remove-Package](http://nuget.codeplex.com/workitem/113)
* [Entfernen Sie die Registerkarte "Aktuell", auf der Benutzeroberfläche für Dialogfeld](http://nuget.codeplex.com/workitem/115)
* [VS-Absturz bei der richtigen klicken Sie auf Projektmappenordner nach dem Öffnen der Benutzeroberfläche für Dialogfeld mindestens auf.](http://nuget.codeplex.com/workitem/126)
* [Change - lokalen Parameter Liste-Pakets installiert:](http://nuget.codeplex.com/workitem/129)
* [Benennen Sie packages.xml in NuPack.config](http://nuget.codeplex.com/workitem/132)
* [Konsole erzwingt, dass Cursor am Ende der Zeile](http://nuget.codeplex.com/workitem/135)
* [Remove-Package Intellisense ist fehlerhaft](http://nuget.codeplex.com/workitem/136)
* [Flag "RequireLicenseAcceptance" NuSpec und Feed hinzufügen](http://nuget.codeplex.com/workitem/137)
* [Fügen Sie "licenseUrl" NuSpec-Format und die Paket-Feeds](http://nuget.codeplex.com/workitem/138)
* [Klicken auf die Installation des Pakets, die Zustimmung erfordert sollte Dialogfeld für die Annahme anzeigen.](http://nuget.codeplex.com/workitem/139)
* [Hinzufügen von Haftungsausschlusses zum Dialogfeld "Paket hinzufügen"](http://nuget.codeplex.com/workitem/140)
* [Fügen Sie, dass Haftungsausschluss bei der Paket-Konsole zum ersten Mal ausführen wird](http://nuget.codeplex.com/workitem/143)
* [Zeigen Sie Haftungsausschluss nach der Installation des Pakets In der Konsole an](http://nuget.codeplex.com/workitem/144)
* [Benennen Sie die Erweiterung .nupack in NUPKG-Datei](http://nuget.codeplex.com/workitem/146)