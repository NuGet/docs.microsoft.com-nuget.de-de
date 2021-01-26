---
title: Anmerkungen zu dieser Version von nuget 1,0 und 1,1
description: Anmerkungen zu dieser Version von nuget 1,1 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cdd4bad54b08d956dbfdaf54220971492fd3ab02
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777209"
---
# <a name="nuget-10-and-11-release-notes"></a>Anmerkungen zu dieser Version von nuget 1,0 und 1,1

[Anmerkungen zu dieser Version von nuget 1,2](../release-notes/nuget-1.2.md)

Nuget 1,0 wurde am 13. Januar 2011 veröffentlicht.  Nuget 1,1 wurde am 12. Februar 2011 veröffentlicht.

## <a name="overview"></a>Übersicht

Dieses Dokument enthält die Versions Hinweise für die verschiedenen Versionen von nuget 1,0, gruppiert nach der Haupt Vorschauversion.

Nuget umfasst die folgenden Komponenten:

* " *Nuget. Tools. vsix* *" besteht aus folgendem:
  * **Dialogfeld "Bibliothekspaket hinzufügen** " in Visual Studio, das zum Durchsuchen und Installieren von Paketen verwendet wird.
  * **Paket-Manager-Konsole** * PowerShell-basierte Konsole in Visual Studio.
* Das *nuget-Befehlszeilen Tool* *-Tool, das zum Erstellen (und schließlich veröffentlichen) von Paketen verwendet wird.

Die Visual Studio-Erweiterung für nuget-Tools (*nuget. Tools. vsix*) erfordert Folgendes:

* Visual Studio 2010 oder Visual Web Developer 2010 Express

Das nuget-Befehlszeilen Tool erfordert Folgendes:

* .NET Framework Version 4

## <a name="installation"></a>Installation

So verwenden Sie die [neueste Version](http://nuget.codeplex.com/releases/view/52018):

* Deinstallieren Sie zuerst Ihren älteren Build. Hierfür müssen Sie vs als Administrator ausführen.
* Entfernen Sie alle vorhandenen Feeds, die Sie besitzen.
* Fügen Sie einen neuen Feed hinzu, der auf verweist <https://go.microsoft.com/fwlink/?LinkId=206669> .

## <a name="nuget-11"></a>NuGet 1.1

Die Liste der in dieser Version [behobene](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0) Probleme finden Sie hier.

## <a name="nuget-10-rtm"></a>Nuget 1,0 RTM

Ein Problem wurde für RTM seit der RC behoben.

* [Problem 474: das Entfernen von Paketen betrifft alle Projekte in der Projekt Mappe.](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Release Candidate

Im folgenden finden Sie die Änderungen, die seit CTP 2 in diesem Release Candidate vorgenommen wurden. Besuchen Sie die Problemverfolgung, um die vollständige Liste der Fehler anzuzeigen.

* [Durch das Aktualisieren des Pakets über die-Konsole werden keine Abhängigkeiten aktualisiert.](http://nuget.codeplex.com/workitem/443)
* [Das Hinzufügen eines Pakets wird nicht als Paket Verweis ausgewählt (CTP1).](http://nuget.codeplex.com/workitem/442)
* [Beim Aktualisieren eines Pakets bleiben unterbrochene Verweise unverändert.](http://nuget.codeplex.com/workitem/440)
* ["Get-Package-Updates" schlägt im Dialogfeld fehl, oder wenn die Aggregat Quelle "All" in der Konsole ausgewählt ist](http://nuget.codeplex.com/workitem/439)
* [Fehler beim Überprüfen der Paketüberprüfung](http://nuget.codeplex.com/workitem/426)
* [Benutzer warnen, wenn ein Paket nicht über das Dialog Feld "Paket hinzufügen" installiert werden kann](http://nuget.codeplex.com/workitem/425)
* [Get-Package-Updates löst beim Aktualisieren einer großen Anzahl von Paketen aus](http://nuget.codeplex.com/workitem/424)
* [Verbessern der Fehlerbehandlung, wenn nuspec-Dateien falsch verfasst wurden](http://nuget.codeplex.com/workitem/423)
* [Das nuget-Paket ignoriert angegebene Dateien.](http://nuget.codeplex.com/workitem/422)
* [Entfernen der zweiten und letzten Paketquelle und anschließendes Klicken auf "nach unten" stürzt ab](http://nuget.codeplex.com/workitem/418)
* [Assemblyverweis beim Installieren von Paketen entfernen](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException beim Öffnen des Dialog Felds "Einstellungen"](http://nuget.codeplex.com/workitem/411)
* [Der Zugriffsschlüssel für die Paketquelle in der Paket-Manager-Konsole funktioniert nicht](http://nuget.codeplex.com/workitem/410)
* [Mit den Einstellungen des Dialog Felds "nuget-vs-Einstellungen" können Sie die Felder](http://nuget.codeplex.com/workitem/409)
* [Die Paket-ID IntelliSense sollte nicht zu viele Elemente Abfragen.](http://nuget.codeplex.com/workitem/404)
* [Fehler beim Hinzufügen des Pakets zum Projekt mit einem Punktzeichen im Projektnamen.](http://nuget.codeplex.com/workitem/403)
* [Problem mit angegebenen Dateien in der nuspec-Datei](http://nuget.codeplex.com/workitem/400)
* [Korrigieren des offiziellen Feeds sollte bei Verwendung eines neueren Builds registriert werden](http://nuget.codeplex.com/workitem/399)
* [Tags sollten anstelle von Leerzeichen verwenden. #](http://nuget.codeplex.com/workitem/397)
* [In ipackagemetadata sind einige nützliche Informationen nicht enthalten.](http://nuget.codeplex.com/workitem/388)
* [Link zum Melden von Missbrauch zum Dialog Feld hinzufügen](http://nuget.codeplex.com/workitem/386)
* [Verwenden von App_Data zum Entzippen von Paketen in Visual Studio](http://nuget.codeplex.com/workitem/380)
* [Implementieren von Tags](http://nuget.codeplex.com/workitem/376)
* [Packagebuilder ermöglicht das Erstellen eines leeren Pakets ohne Abhängigkeiten.](http://nuget.codeplex.com/workitem/373)
* [Feld "Besitzer hinzufügen" für das Paket](http://nuget.codeplex.com/workitem/365)
* [Aktualisieren Sie das VSIX-Manifest mit dem nuget-Paket-Manager und nicht mit VSIX-Tools.](http://nuget.codeplex.com/workitem/364)
* [Befehl "Get-Package" löst einen Fehler aus, wenn alle Quellen ausgewählt sind](http://nuget.codeplex.com/workitem/359)
* [Reihenfolge von Paketquellen im Dialogfeld "Optionen" zulassen](http://nuget.codeplex.com/workitem/356)
* [Update-Package entfernt keine ältere Version.](http://nuget.codeplex.com/workitem/352)
* [Implementieren der Versions Bereichs Spezifikation für Abhängigkeiten](http://nuget.codeplex.com/workitem/347)
* [Visual Studio stürzt ab, wenn Sie auf "neues Paket hinzufügen" klicken](http://nuget.codeplex.com/workitem/346)
* [Anzeigen von Downloads und Bewertungen im Dialog Feld "Paket hinzufügen"](http://nuget.codeplex.com/workitem/345)
* [Durch das Wechseln zwischen Paketquellen im Dialog Feld wird die aktive Quelle nicht aktualisiert](http://nuget.codeplex.com/workitem/344)
* [Schlüsselbindung für Paket-Manager-Konsolenfenster entfernen](http://nuget.codeplex.com/workitem/339)
* [Install-Package wird nicht als Name eines Cmdlets erkannt...](http://nuget.codeplex.com/workitem/338)
* [Die Installation eines Pakets aus einem lokalen Feed die Abhängigkeiten von regulären Feeds werden nicht aufgelöst.](http://nuget.codeplex.com/workitem/332)
* [Removeabhängigkeiten sollten Abhängigkeiten überspringen, die noch verwendet werden.](http://nuget.codeplex.com/workitem/331)
* [Beim Abbrechen der Seitennavigation kann der Benutzer nicht zu einer anderen Seite navigieren, während die ursprüngliche Seiten Anforderung zurückgegeben wird.](http://nuget.codeplex.com/workitem/325)
* [Untersuchen Sie die Leistung von nupack. Server, um Feeds mit einer großen Anzahl von Paketen zu betreuen.](http://nuget.codeplex.com/workitem/324)
* [Beim zweiten Filter für ein Paket wird die "neue" Paketquelle anstelle der zuvor ausgewählten Quelle verwendet.](http://nuget.codeplex.com/workitem/321)
* [Beim Auswählen der Registerkarte "Online" im Dialogfeld muss die Standardpaket Quelle ausgewählt werden.](http://nuget.codeplex.com/workitem/320)
* [List-Package sollte installierte Pakete standardmäßig anzeigen](http://nuget.codeplex.com/workitem/309)
* [Assemblyverweis HintPath](http://nuget.codeplex.com/workitem/294)
* [Ausnahme beim Öffnen der Paket-Manager-Konsole.](http://nuget.codeplex.com/workitem/268)
* [IntelliSense der Konsole lädt den gesamten Feed herunter](http://nuget.codeplex.com/workitem/259)
* [Die Paketquelle "Default" muss in "Active" umbenannt werden.](http://nuget.codeplex.com/workitem/258)
* [Benutzeroberfläche für Paketquellen: durch Drücken von "OK" sollte die neue Quelle hinzugefügt werden, wenn Name/Quell Felder nicht leer sind](http://nuget.codeplex.com/workitem/257)
* [Das Dialog Feld wird sehr langsam, wenn die Anzahl installierter Pakete groß ist.](http://nuget.codeplex.com/workitem/243)
* [Unterstützen von Bindungs Umleitungen für Assemblys mit starkem Namen](http://nuget.codeplex.com/workitem/238)
* [Paket Verweis hinzufügen... Benutzeroberfläche zum Einschließen der Dropdown-Datei für Paketquelle](http://nuget.codeplex.com/workitem/226)
* [Nupack muss die config-Transformation agnostisch des Konfigurations Dateinamens unterstützen.](http://nuget.codeplex.com/workitem/224)
* [Ermöglicht das Überschreiben von BasePath in NuPack.exe](http://nuget.codeplex.com/workitem/222)
* [Fall Back Verhalten der Paketquelle](http://nuget.codeplex.com/workitem/204)
* [Absturz auf GUI](http://nuget.codeplex.com/workitem/201)
* [Sortieroptionen zum Dialog Feld "Paket hinzufügen" hinzufügen](http://nuget.codeplex.com/workitem/179)
* [Tastenkombination zum Löschen der Paket-Manager-Konsole](http://nuget.codeplex.com/workitem/174)
* [Die powerconsole bewirkt, dass die nupack-Konsole ausfällt](http://nuget.codeplex.com/workitem/166)
* [Das Dialog Feld "Konsole" und "Paket hinzufügen" sollte Benutzer-Agent](http://nuget.codeplex.com/workitem/141)
* [Legen Sie die Versionsnummer der VSIX und NuPack.exe im Build fest.](http://nuget.codeplex.com/workitem/134)
* [Allgemeine PowerShell-Parameter aus-? ausblenden](http://nuget.codeplex.com/workitem/118)
* [Hinzufügen-ausführliche Hilfe für Konsolenbefehle](http://nuget.codeplex.com/workitem/110)
* [Dialog Feld "Paket hinzufügen" sollte das Auswählen der aktuellen Paketquelle ermöglichen](http://nuget.codeplex.com/workitem/88)
* [Verschieben von nupack. Core-Klassen in verschiedene Namespaces](http://nuget.codeplex.com/workitem/50)
* [Hinzufügen von Hilfe zu Cmdlets](http://nuget.codeplex.com/workitem/23)
* [Hash aus Feed nach Paket Download überprüfen](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

Im folgenden finden Sie die wichtigsten Änderungen, die in CTP 2 vorgenommen werden:

* Wechsel des paketfeeds von Atom zu einem odata-Dienst Endpunkt: Wenn Sie ein Upgrade auf die CTP2-Version von nuget durchführen, stellen Sie sicher, dass Sie die folgende URL als Paketquelle hinzufügen: `https://feed.nuget.org/ctp2/odata/v1/` .
* Der Add-Package-Befehl wurde in " *install-Package*" umbenannt.
* Das Format wurde aktualisiert `.nuspec` . Das `.nuspec` Format enthält jetzt das Feld *IconUrl* zum Angeben des Symbols 32x32 PNG, das im Dialog Feld Paket hinzufügen angezeigt wird. Stellen Sie daher sicher, dass Sie das Paket unterscheiden. Das `.nuspec` Format enthält auch das neue *projecturl* -Feld, das Sie verwenden können, um auf eine Webseite zu verweisen, die weitere Informationen zu Ihrem Paket bereitstellt.

Dieser Build funktioniert nicht mit alten `.nupkg` Dateien. Wenn Sie NULL-Verweis Ausnahmen erhalten, verwenden Sie eine alte `.nupkg` Datei, die Sie mit dem aktualisierten [nuget-Befehlszeilen Tool](http://nuget.codeplex.com/releases/52017/download/165468)neu erstellen müssen.

Im folgenden finden Sie eine Liste der Features und Fehler, die für nuget CTP 2 korrigiert wurden (enthält keine Fehler für kleinere Code Bereinigungen usw.).

* [Fehler beim Entpacken von paketassemblys beim Angeben von TargetFramework für eine Assembly.](http://nuget.codeplex.com/workitem/10)
* [Einerkennbarer anerkennbaren nupack-Konsolenfenster](http://nuget.codeplex.com/workitem/14)
* [nupack.exe Release ILMerge](http://nuget.codeplex.com/workitem/19)
* [Bessere Fehler-und Ausnahmebehandlung](http://nuget.codeplex.com/workitem/24)
* [[Nupack. core]: packagemanager sollte Feed-bezogene Fehler ordnungsgemäß behandeln.](http://nuget.codeplex.com/workitem/28)
* [Sie benötigen ein neues Symbol für die Konsole.](http://nuget.codeplex.com/workitem/29)
* [Lokalisieren von Zeichen folgen im Dialog Feld](http://nuget.codeplex.com/workitem/38)
* [Nupack speichert heruntergeladene nupack-Dateien im Arbeitsspeicher](http://nuget.codeplex.com/workitem/40)
* [Nupack-Konsole: Ändern Sie die Standard Verknüpfung für die Anzeige der Konsole.](http://nuget.codeplex.com/workitem/48)
* [Projectsystem muss Standardwerte für allgemeine Eigenschaften unterstützen](http://nuget.codeplex.com/workitem/49)
* [Wenn Sie nupack.exe in einem Ordner mit nur einer nuspec-Datei ausführen, sollte diese nuspec verwendet werden.](http://nuget.codeplex.com/workitem/52)
* [Das Projekt Menü wird angezeigt, auch wenn kein Projekt/keine Projekt Mappe geladen ist.](http://nuget.codeplex.com/workitem/54)
* ["Build. cmd" führt bei einem sauberen Klon der Codebasis zu einem Fehler.](http://nuget.codeplex.com/workitem/56)
* [Verfügbare Features für Updates](http://nuget.codeplex.com/workitem/57)
* [Dialog: durch Hinzufügen eines Pakets über das Dialogfeld wird die Eingabeaufforderung in der Konsole entfernt.](http://nuget.codeplex.com/workitem/73)
* [Das Hinzufügen eines Pakets durch Klicken auf "Install" ist oft langsam und ohne visuelles Feedback.](http://nuget.codeplex.com/workitem/80)
* [Es gibt keine Möglichkeit, zu ermitteln, welche der installierten Pakete über Updates verfügen.](http://nuget.codeplex.com/workitem/82)
* [Es gibt keine Möglichkeit, ein installiertes Paket im Dialogfeld zu aktualisieren.](http://nuget.codeplex.com/workitem/83)
* [Es gibt keine Möglichkeit, ein installiertes Paket im Dialogfeld zu deinstallieren.](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Paket Verweis hinzufügen wird &hellip; &rdquo; im Kontextmenü installierter Verweise angezeigt.](http://nuget.codeplex.com/workitem/85)
* [Nach dem Aktualisieren eines Pakets über die-Konsole werden sowohl die alte als auch die neue Version als installiert angezeigt.](http://nuget.codeplex.com/workitem/86)
* [Die Aktivität in der Konsole wird bei Verwendung des Dialog Felds nach der Verwendung nicht mehr angezeigt.](http://nuget.codeplex.com/workitem/87)
* [Bereinigen der Befehlszeilen Verarbeitung in nupack.exe](http://nuget.codeplex.com/workitem/89)
* [Hinzufügen eines anzeigen Amens zu Paketquellen](http://nuget.codeplex.com/workitem/98)
* [Update. nuspec zur Unterstützung der Einbeziehung von Paket Symbolen](http://nuget.codeplex.com/workitem/103)
* [Die Feed-Benutzeroberfläche lässt das Kopieren der URL nicht zu](http://nuget.codeplex.com/workitem/105)
* [Bessere Fehlerbehandlung beim Entfernen von Paketen.](http://nuget.codeplex.com/workitem/107)
* [Eingabe im Konsolenfenster hängt vom Cursor Fokus ab](http://nuget.codeplex.com/workitem/112)
* [Fehlermeldungen sind schrecklich.](http://nuget.codeplex.com/workitem/116)
* [Die Leistung von Remove-Package für ein Paket, das nicht installiert ist, ist schlecht.](http://nuget.codeplex.com/workitem/117)
* [Das Entfernen eines Pakets schlägt fehl, wenn keine Paketquellen vorhanden sind.](http://nuget.codeplex.com/workitem/119)
* [Remove-Package schlägt fehl, wenn die Paketquelle nicht verfügbar ist.](http://nuget.codeplex.com/workitem/120)
* [Fügen Sie den Paket Metadaten und dem Feed den Titel hinzu.](http://nuget.codeplex.com/workitem/125)
* [Fügen Sie den Parameter "-Source" wieder zum Add-Package hinzu.](http://nuget.codeplex.com/workitem/127)
* [List-Package muss einen-source-Parameter aufweisen.](http://nuget.codeplex.com/workitem/128)
* [Nupack. Server aktualisieren, um das Herunterladen des Pakets durch den nupack-Benutzer-Agent](http://nuget.codeplex.com/workitem/142)
* [Im Dialog Feld zum Akzeptieren der Lizenz müssen Lizenzen für alle Abhängigkeiten aufgeführt werden, die akzeptiert werden](http://nuget.codeplex.com/workitem/145)
* [Protokolliert einen Fehler, wenn ein Paket im Feed ausgelöst wird.](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe darf kein leeres &lt; licenenurl-Element zulassen. &gt;](http://nuget.codeplex.com/workitem/152)
* [Benennen Sie List-Package in Get-Package um, Add-Package Sie in install-Package, und Remove-Package Sie deinstallieren-Package.](http://nuget.codeplex.com/workitem/155)
* [Verwenden des Menü Elements "Paket Verweis hinzufügen" aus dem projektmappennavigator stürzt Visual Studio ab](http://nuget.codeplex.com/workitem/158)
* [In der Bezeichnung "verfügbare Paketquellen" fehlt ein Doppelpunkt.](http://nuget.codeplex.com/workitem/160)
* [Make. nuspec-XML-Element groß-und Kleinschreibung](http://nuget.codeplex.com/workitem/161)
* [Das VSIX-Manifest von nupack muss das "admin"-Bit aktivieren.](http://nuget.codeplex.com/workitem/162)
* [Wenn Sie List-Package ohne Feeds ausführen, erhalten Sie den Verweis Fehler NULL.](http://nuget.codeplex.com/workitem/164)
* [nuget.exe: Zielpfad angeben](http://nuget.codeplex.com/workitem/171)
* [PowerShell-Fehler beim Öffnen Paketverwaltung Konsole unter WinXP](http://nuget.codeplex.com/workitem/175)
* [VS stürzt beim Laden der Paketliste ab.](http://nuget.codeplex.com/workitem/176)
* [Meta-Pakete zulassen (keine Dateien, nur Abhängigkeiten)](http://nuget.codeplex.com/workitem/180)
* [Konvertieren eines PowerShell-Skripts in das PowerShell 2,0-Modul](http://nuget.codeplex.com/workitem/181)
* ["Pthresolver" sollte den Pfad Teil vor den Platzhalter Zeichen verwerfen, wenn "target" angegeben ist](http://nuget.codeplex.com/workitem/183)
* [Keine Abhängigkeiten](http://nuget.codeplex.com/workitem/186)
* [Fehler beim Installieren von ELMAH.](http://nuget.codeplex.com/workitem/192)
* [Konfigurations Transformationen funktionieren in configabschnitte nicht ordnungsgemäß. &lt;&gt;](http://nuget.codeplex.com/workitem/194)
* [Die Variable "$Global:p rojectcache" kann nicht abgerufen werden, da Sie nicht festgelegt wurde.](http://nuget.codeplex.com/workitem/203)
* [MSBuild-Aufgabe zum Erstellen von nupack-Paketen hinzufügen](http://nuget.codeplex.com/workitem/205)
* [List-Package muss suchen/Filtern unterstützen](http://nuget.codeplex.com/workitem/206)
* [Immer einen Link zur Lizenz anzeigen, wenn der Paket Ersteller eine Lizenz-URL bereitstellt](http://nuget.codeplex.com/workitem/208)
* [Gelegentliche Ausnahme "Zugriff verweigert" mit Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Fehler bei Komponenten Tests: invalidpackageisexclutodfromfeeditems " &amp; foratingfeedconvertspackagestoatomentries"](http://nuget.codeplex.com/workitem/214)
* [Hiermit wird ein Fallback/default-Satz von Dateien zugelassen, wenn eine bestimmtes runas Framework-Version nicht gefunden werden kann.](http://nuget.codeplex.com/workitem/223)
* [Paket Verweis hinzufügen... Benutzeroberfläche kann ein Paket nicht entfernen.](http://nuget.codeplex.com/workitem/225)
* [Paket Verweis hinzufügen stürzt Studio ab, wenn ein oder mehrere Projekte entladen werden](http://nuget.codeplex.com/workitem/228)
* [Die Konfigurations Transformation scheint nicht für web.debug.config Datei zu funktionieren.](http://nuget.codeplex.com/workitem/229)
* [init.ps1 wird nicht für benutzerdefiniertes Paket ausgelöst.](http://nuget.codeplex.com/workitem/237)
* [Wenn Sie der feedlist Pfade hinzufügen, wird die Standard Schaltfläche auf OK festgelegt, sodass beim Drücken der EINGABETASTE automatisch geschlossen wird.](http://nuget.codeplex.com/workitem/240)
* [Der Versuch, eine Abhängigkeit zu deinstallieren, stürzt im Vergleich zu zwei Mal in einer Zeile ab.](http://nuget.codeplex.com/workitem/241)
* [Anzeigen der Projekt-URL im Dialogfeld "Paket hinzufügen"](http://nuget.codeplex.com/workitem/253)
* [Standard-Dialogfeld "Add-Package" zu installierten Paketen](http://nuget.codeplex.com/workitem/254)
* [Ändern Sie das Menü Element Paket hinzufügen.](http://nuget.codeplex.com/workitem/261)
* [Umbenennen von Namespaces und Assemblys](http://nuget.codeplex.com/workitem/274)
* [Umbenennen des nupack-Projekts in nuget](http://nuget.codeplex.com/workitem/282)
* [Fügen Sie den folgenden Text in der Liste der Abhängigkeiten hinzu.](http://nuget.codeplex.com/workitem/288)
* [Ändern des Lizenz Annahme Texts im Dialog Feld "Lizenz Annahme"](http://nuget.codeplex.com/workitem/291)
* [Ändern Sie den Text im Dialog Feld "Lizenz Annahme" oberhalb der Liste der Pakete.](http://nuget.codeplex.com/workitem/292)
* [Odata funktioniert nicht mit einer URL für den URL-Link](http://nuget.codeplex.com/workitem/304)
* [Benutzeroberfläche des Paket-Managers: über aggressives Zwischenspeichern der für das Paging verwendeten Paket Anzahl](http://nuget.codeplex.com/workitem/317)
* [Fehler bei nupack/nuget- &gt; Paket-Manager-Konsole](http://nuget.codeplex.com/workitem/335)
* [Dialog Feld "Paket hinzufügen" zeigt die Lizenz Annahme für bereits installierte Pakete](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

Im folgenden finden Sie eine Liste der Features und Fehler, die für nuget CTP 1 korrigiert wurden.

* [Die Paket Erweiterung sollte in. nupack umbenannt werden.](http://nuget.codeplex.com/workitem/1)
* [Paketdatei in Ordner verschieben](http://nuget.codeplex.com/workitem/2)
* [Merge install &amp; Add PS-Befehle](http://nuget.codeplex.com/workitem/3)
* [Erstellen von Aliasen für Verb-Noun-Cmdlets](http://nuget.codeplex.com/workitem/4)
* [Nupack wird beim Wechseln der Projekt Mappe in vs verwechselt](http://nuget.codeplex.com/workitem/6)
* [Der Projektmappenordner "Packages" sollte standardmäßig ausgeblendet werden.](http://nuget.codeplex.com/workitem/11)
* [Fügen Sie Unterstützung für die Tokenersetzung in Inhalts Elementen hinzu.](http://nuget.codeplex.com/workitem/12)
* [Nupack. UI sollte die packagesource-API verwenden.](http://nuget.codeplex.com/workitem/26)
* [[Nupack. core]: packagemanager markiert Pakete als installiert, bevor Sie installiert werden.](http://nuget.codeplex.com/workitem/27)
* [Beim Löschen des Standard Projekts aus der Projekt Mappe wird das gelöschte Projekt weiterhin als Standard angezeigt](http://nuget.codeplex.com/workitem/30)
* [New-Package schlägt mit "der Teil kann nicht für den angegebenen URI hinzugefügt werden, da er bereits im Paket enthalten ist" fehl.](http://nuget.codeplex.com/workitem/32)
* [Entfernen von nupack-Zeichen folgen aus Visual Studio GUI](http://nuget.codeplex.com/workitem/35)
* [Apache-Header zu einer COPYRIGHT.txt Datei hinzufügen](http://nuget.codeplex.com/workitem/36)
* [Update-PackageSource Befehl entfernen](http://nuget.codeplex.com/workitem/37)
* [Beim Laden des Profils nicht verwendbar Paket-Manager löst eine Ausnahme aus](http://nuget.codeplex.com/workitem/39)
* [init.ps1, install.ps1 und uninstall.ps1 müssen einen zusätzlichen Zustand erhalten.](http://nuget.codeplex.com/workitem/41)
* [Kombinieren von Konsolen-und GUI-Paketen zu einem Paket](http://nuget.codeplex.com/workitem/42)
* [XML-Transformations Logik funktioniert nicht, wenn Sie auf XML angewendet wird, das nicht im Stammverzeichnis ist](http://nuget.codeplex.com/workitem/43)
* [Dialogfeld "Paketquellen Einstellungen verwalten" aktualisiert die nupack-Konsole nicht](http://nuget.codeplex.com/workitem/44)
* [Benutzeroberfläche der nupack-Konsole: Umbenennen der Dropdown Liste "paketfeed" in "Paketquelle"](http://nuget.codeplex.com/workitem/45)
* [Nupack-Konsolen Optionen: Umbenennen von "Repository UI", um mit der nupack-Konsole konsistent zu sein](http://nuget.codeplex.com/workitem/46)
* [Add-Package schlägt für eine Website fehl, die über IIS oder eine URL geöffnet wurde.](http://nuget.codeplex.com/workitem/53)
* [Die Paket-Manager-Quelle funktioniert nicht mit "f".](http://nuget.codeplex.com/workitem/55)
* [Festlegen der Standardpaket Quelle](http://nuget.codeplex.com/workitem/59)
* [Wenn beim Hinzufügen von Paketquellen in die Option nur eine Quelle angegeben ist, wird angenommen, dass es sich um den Standardwert handelt.](http://nuget.codeplex.com/workitem/60)
* [Die Benutzeroberfläche des Dialog Felds zeigt gefälschte "aktuelle" Pakete an.](http://nuget.codeplex.com/workitem/62)
* [Optionen: durch Klicken auf Abbrechen werden Änderungen nicht abgebrochen.](http://nuget.codeplex.com/workitem/63)
* [Bei der Suche im Dialog Feld "Paket Verweis hinzufügen" sollte die](http://nuget.codeplex.com/workitem/65)
* [Korrigieren von Firmen Metadaten in AssemblyInfo.cs-Dateien](http://nuget.codeplex.com/workitem/67)
* [Versionsnummer für die VSIX](http://nuget.codeplex.com/workitem/71)
* [Remove-Package: Using-? zeigt die Hilfe zweimal an](http://nuget.codeplex.com/workitem/72)
* [Ausführen von Installations-/deinstallationspaketen für Pakete auf Projektebene](http://nuget.codeplex.com/workitem/74)
* [Der Server kann keinen Feed erstellen, wenn die Überprüfung eines nupacks fehlschlägt](http://nuget.codeplex.com/workitem/90)
* [Nupack-Symbole müssen ersetzt werden.](http://nuget.codeplex.com/workitem/94)
* [Der NTLM-HTTP-Proxy wird nicht für den paketfeed authentifiziert.](http://nuget.codeplex.com/workitem/96)
* [Das Dialogfeld wird im vs-Fenster nicht immer zentriert](http://nuget.codeplex.com/workitem/100)
* [Viele Felder in den Paket Details werden nicht im Dialogfeld aufgefüllt.](http://nuget.codeplex.com/workitem/102)
* [Die Benutzernamen werden von der Dialog Feld-UI nicht angezeigt](http://nuget.codeplex.com/workitem/108)
* [Warum-Version für Remove-Package](http://nuget.codeplex.com/workitem/113)
* [Entfernen der Registerkarte "aktuell" in der Dialog Feld Oberfläche](http://nuget.codeplex.com/workitem/115)
* [VS Absturz, wenn Sie mit der rechten Maustaste auf den Projektmappenordner klicken, nachdem Sie mindestens einen Dialog Feld](http://nuget.codeplex.com/workitem/126)
* [Ändern Sie den-local-Parameter von List-Package in-installiert](http://nuget.codeplex.com/workitem/129)
* [Umbenennen von packages.xml in NuPack.config](http://nuget.codeplex.com/workitem/132)
* [Die Konsole erzwingt den Cursor bis zum Ende der Zeile.](http://nuget.codeplex.com/workitem/135)
* [Remove-Package IntelliSense ist beschädigt.](http://nuget.codeplex.com/workitem/136)
* [Requirelicenseacceptance-Flag zu. nuspec und Feed hinzufügen](http://nuget.codeplex.com/workitem/137)
* [Hinzufügen von licenseurl zu. nuspec-Format und paketfeed](http://nuget.codeplex.com/workitem/138)
* [Wenn Sie auf für das Paket installieren klicken, das akzeptiert werden muss](http://nuget.codeplex.com/workitem/139)
* [Hinzufügen von Haftungsausschluss Text zum Dialog Feld Paket hinzufügen](http://nuget.codeplex.com/workitem/140)
* [Haftungsausschluss hinzufügen, wenn die Paket Konsole erstmalig ausgeführt wird](http://nuget.codeplex.com/workitem/143)
* [Haftungsausschluss nach der Installation des Pakets in der-Konsole anzeigen](http://nuget.codeplex.com/workitem/144)
* [Umbenennen der Erweiterung ". nupack" in ". nupkg"](http://nuget.codeplex.com/workitem/146)