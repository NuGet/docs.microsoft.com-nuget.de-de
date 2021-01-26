---
title: Anmerkungen zu dieser Version von nuget 3,0 Preview
description: Anmerkungen zu dieser Version von nuget 3,0, einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ecaed21c5e689a488e033404f8042cd1f17eed0d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780324"
---
# <a name="nuget-30-preview-release-notes"></a>Anmerkungen zu dieser Version von nuget 3,0 Preview

Anmerkungen zu dieser [Version von nuget 2,9 RC](../release-notes/nuget-2.9-rc.md)  |  [Anmerkungen zu dieser Version von nuget 3,0 Beta](../release-notes/nuget-3.0-beta.md)

Nuget 3,0 Preview wurde am 12. November 2014 als Teil der Visual Studio 2015 Preview-Version veröffentlicht. Wir haben nuget 3,0 Preview veröffentlicht. Dies ist eine umfangreiche Version für uns (auch als Vorschau), und wir freuen uns, uns mit dem Feedback zu unseren Änderungen zu beschäftigen.

## <a name="visual-studio-2012"></a>Visual Studio 2012 und höher

Diese nuget 3,0 Preview-Version ist in Visual Studio 2015 Preview enthalten. Wir arbeiten daran, die Vorschau für Visual Studio 2012 zu erhalten, und Visual Studio 2013 sehr bald. Wir haben unsere Absicht bereits zum [Beenden von Updates für Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)freigegeben, und wir haben diese schwierige Entscheidung getroffen.

## <a name="brand-new-ui"></a>Neue Benutzeroberfläche

Das erste, was Sie über nuget 3,0 Preview bemerken, ist die neue Benutzeroberfläche. Es handelt sich nicht mehr um ein modales Dialogfeld. Es ist jetzt ein vollständiges Visual Studio-Dokument Fenster. Auf diese Weise können Sie die Benutzeroberfläche für mehrere Projekte (und/oder die Projekt Mappe) gleichzeitig öffnen, das Fenster an einen anderen Monitor andocken, Sie nach Belieben andocken, usw.

![Die neue nuget-Benutzeroberfläche](./media/NuGet-3.0-Preview/new-ui.png)

Abgesehen von den Nutzbarkeits unterschieden, da das modale Dialogfeld abgebrochen wurde, haben wir auch viele neue Features in der neuen Benutzeroberfläche.

### <a name="version-selection"></a>Versions Auswahl

Die am meisten angeforderte Benutzeroberfläche ist, die Versions Auswahl für die Paketinstallation und das Update zuzulassen. Dies ist jetzt verfügbar.

![Paket Versions Auswahl](./media/NuGet-3.0-Preview/version-selection.png)

Unabhängig davon, ob Sie ein Paket installieren oder aktualisieren, können Sie in der Dropdown Liste Version alle für das Paket verfügbaren Versionen anzeigen, wobei einige relevante Versionen zur einfacheren Auswahl an den Anfang der Liste herauf gestuft werden. Sie müssen nicht mehr die PowerShell-Konsole verwenden, um bestimmte Versionen zu erhalten, die nicht die neuesten Versionen sind.

### <a name="combined-installedonlineupdates-workflows"></a>Kombinierte installierte/Online/Update-Workflows

Unsere vorherige Benutzeroberfläche verfügte über drei Registerkarten für installierte, Online und Updates. Die aufgelisteten Pakete waren spezifisch für diese Workflows, und die verfügbaren Aktionen waren auch für die Workflows spezifisch. Obwohl das logisch war, haben wir gehört, dass viele von Ihnen häufig durch diese Trennung eingeschnitten werden.

Wir haben jetzt eine kombinierte Funktion, in der Sie ein Paket installieren, aktualisieren oder deinstallieren können, unabhängig davon, wie Sie das Paket ausgewählt haben. Zur Unterstützung der spezifischen Workflows verfügen wir jetzt über eine Filter Dropdown Liste, mit der Sie die verfügbaren Pakete filtern können. die für das Paket verfügbaren Aktionen sind jedoch konsistent.

![Deinstallieren eines Pakets](./media/NuGet-3.0-Preview/uninstall-package.png)

Mithilfe des Filters "installiert" können Sie die installierten Pakete auf einfache Weise anzeigen, für die Updates verfügbar sind, und Sie können das Paket entweder deinstallieren oder aktualisieren, indem Sie die Versions Auswahl ändern, um die verfügbare Aktion zu ändern.

![Aktualisieren eines Pakets](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Versions Konsolidierung

Es ist üblich, dass das gleiche Paket in mehreren Projekten in der Lösung installiert ist. Manchmal können die in den einzelnen Projekten installierten Versionen voneinander abweichen, und es ist erforderlich, die verwendeten Versionen zu konsolidieren. In der Vorschauversion von nuget 3,0 wird nur für dieses Szenario ein neues Feature eingeführt.

Sie können auf das Fenster Paketverwaltung auf Projektmappenebene zugreifen, indem Sie mit der rechten Maustaste auf die Lösung klicken und nuget-Pakete für Projekt Mappe verwalten auswählen. Wenn Sie ein Paket auswählen, das in mehreren Projekten installiert ist, aber mit unterschiedlichen Versionen verwendet wird, wird eine neue Aktion "konsolidieren" verfügbar. Im Screenshot unten `Newtonsoft.Json` wurde in `SamplesClassLibrary` mit Version installiert `6.0.4` und in `SamplesConsoleApp` mit Version installiert `5.0.4` .

![Konsolidieren von Versionen](./media/NuGet-3.0-Preview/consolidate.png)

Im folgenden finden Sie den Workflow für die Konsolidierung auf eine einzelne Version.

1. Wählen Sie das `Newtonsoft.Json` Paket in der Liste aus.
1. `Consolidate`Aus der `Action` Dropdown Liste auswählen
1. Verwenden `Version` Sie die Dropdown Liste, um die zu konsolidierte Version auszuwählen.
1. Aktivieren Sie die Kontrollkästchen für die Projekte, die auf diese Version konsolidiert werden sollen (Beachten Sie, dass Projekte, die bereits in der ausgewählten Version vorhanden sind, abgeblendet werden).
1. Klicken Sie `Consolidate` auf die Schaltfläche, um die Konsolidierung auszuführen.

### <a name="operation-previews"></a>Vorgangs Vorschau

Unabhängig von dem Vorgang, den Sie ausführen: installieren/aktualisieren/deinstallieren: die neue Benutzeroberfläche bietet nun eine Möglichkeit, die Änderungen in der Vorschau anzuzeigen, die an Ihrem Projekt vorgenommen werden. Diese Vorschau zeigt alle neuen Pakete, die installiert werden sollen, zu Aktualisier Ende Pakete und Pakete, die deinstalliert werden, zusammen mit Paketen, die während des Vorgangs unverändert bleiben werden.

Im folgenden Beispiel sehen Sie, dass die Installation von Microsoft. Aspnet. signalr zu einigen Änderungen am Projekt führt.

![Vorschau der Installation von signalr](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Installationsoptionen

Mithilfe der PowerShell-Konsole haben Sie die Kontrolle über einige wichtige Installationsoptionen. Wir haben diese Features nun ebenfalls in die Benutzeroberfläche gebracht. Sie können jetzt das Verhalten der Abhängigkeitsauflösung steuern, wie Versionen der Abhängigkeiten ausgewählt werden.

![Abhängigkeitsverhalten](./media/NuGet-3.0-Preview/dependency-behavior.png)

Sie können auch angeben, welche Aktion ausgeführt werden soll, wenn Inhalts Dateien aus Paketen mit Dateien in Konflikt stehen, die bereits im Projekt vorhanden sind.

![Dateikonflikt Aktion](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Unendliches Scrollen

Wir haben uns für ein sehr wenig Feedback zu unserer Benutzeroberfläche verwendet, das beim Auflisten von Paketen sowohl den Bildlauf als auch das Auslagerungs Paradigma hat. Es war ziemlich üblich, einen Bildlauf bis zum Ende der Kurzliste durchführen zu müssen, auf die nächste Seitenzahl zu klicken und dann erneut einen Bildlauf durchführen. Mit der neuen Benutzeroberfläche haben wir einen unendlichen Bildlauf in der Paketliste implementiert, sodass Sie nur einen Bildlauf durchführen müssen, ohne dass Sie auslagern müssen.

![Unendliches Scrollen](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Arbeiten Sie, machen Sie es so schnell, machen Sie es

Wir freuen uns, diese neue Benutzeroberfläche zu testen, die Sie ausprobieren können. Im Rahmen dieses Vorschau Meilensteins haben wir uns auf die gute alte Sprichworts "make it work, Make it fast, Make it" (so gut wie möglich) und eine ziemlich gute Folge " In dieser Vorschauversion haben wir das erste Ziel erreicht, es funktioniert. Wir wissen, dass es noch nicht so schnell ist, und wir wissen, dass es noch nicht ganz so einfach ist. Wir arbeiten an diesen Zielen zwischen jetzt und der RC-Version. In der Zwischenzeit würden wir uns Ihr *Feedback zur* *Benutzerfreundlichkeit* der neuen Benutzeroberfläche, den Workflows, den Vorgängen und der Verwendung der neuen Benutzeroberfläche gefallen.

Im Vergleich zur alten Benutzeroberfläche haben wir einige Funktionen entfernt. Eine davon war beabsichtigt, und die andere war einfach nicht in der Zeit.

#### <a name="searching-all-package-sources"></a>Alle Paketquellen suchen

Mit der alten Benutzeroberfläche können Sie eine Paket Suche für alle Paketquellen durchführen. Wir haben diese Funktion in der Benutzeroberfläche entfernt und werden nicht wieder zurückgebracht. Diese Funktion wird verwendet, um Suchvorgänge für alle Ihre Paketquellen auszuführen, die Ergebnisse zu kombinieren und zu versuchen, die Ergebnisse auf der Grundlage ihrer Sortier Auswahl zu ordnen.

Wir haben festgestellt, dass die Such Relevanz wirklich schwer zu vermischen ist. Könnten Sie sich vorstellen, dass Sie eine Suche für Google und die Suche durchführen und die Ergebnisse miteinander kombinieren? Außerdem war dieses Feature langsam und leicht *zu verwenden,* und wir glauben, dass es selten wirklich nützlich war. Aufgrund der Probleme, die das Feature eingeführt hat, erhielten wir eine Reihe von Fehlerberichten, die nie korrigiert wurden.

#### <a name="update-all"></a>Alle aktualisieren

Wir haben eine Schaltfläche "Alle aktualisieren" in der alten Benutzeroberfläche verwendet, die noch nicht in der neuen Benutzeroberfläche vorhanden ist. Wir werden dieses Feature für unsere RC-Version wiederbeleben.

## <a name="new-clientserver-api"></a>Neue Client/Server-API

Zusätzlich zu allen neuen Features in unserer neuen Benutzeroberfläche für die Paketverwaltung haben wir auch einige Implementierungsdetails für das Client/Server-Protokoll von nuget gearbeitet. Die Arbeit, die wir erledigt haben, ist das Erstellen von "API v3" für nuget, das um hohe Verfügbarkeit für kritische Szenarien wie die Paket Wiederherstellung und die Installation von Paketen entworfen wurde. Die neue API basiert auf Rest und Hypermedia, und wir haben [JSON-LD](http://json-ld.org) als Ressourcen Format ausgewählt.

In den nuget 3,0-Vorschau Bits wird in der Dropdown Liste Paketquelle eine neue Paketquelle namens "Preview.nuget.org" angezeigt. Wenn Sie diese Paketquelle auswählen, verwenden wir stattdessen unsere neue API, um eine Verbindung mit nuget.org herzustellen. Wir haben die Vorschau Quelle auf der Benutzeroberfläche zur Verfügung gestellt, während wir weiterhin testen, überarbeiten und die neue API verbessern. In nuget 3,0 RC ersetzt diese neue API-v3-basierte Paketquelle die V2-basierte Paketquelle "nuget.org".

Trotz der Investitionen, die wir in API v3 umsetzen, haben wir alle diese neuen Features auch mit unserem vorhandenen API v2-Protokoll zusammengearbeitet, was bedeutet, dass Sie mit vorhandenen Paketquellen außer nuget.org arbeiten.

## <a name="new-features-coming"></a>Neue Features

Zwischen jetzt und 3,0 RTM arbeiten wir auch an einigen grundlegenden neuen nuget-Features, die über das, was Sie in der Benutzeroberfläche sehen, hinausgehen. Im folgenden finden Sie eine kurze Liste der wichtigsten Investitionsbereiche:

1. Wir arbeiten mit den Visual Studio-und MSBuild-Teams zusammen, um [nuget tiefer in die Plattform](http://blog.nuget.org/20141014/in-the-platform.html)zu bringen.
1. Wir arbeiten daran, die Installationszeit Paket Konventionen zu verwerfen, und wenden diese Konventionen stattdessen zur verpackungszeit an, indem wir ein neues autoritative [Paket Manifest](http://blog.nuget.org/20141023/package-manifests.html)einführen.
1. Wir arbeiten daran, die nuget-Codebasis umzugestalten, damit die Client-und Serverkomponenten in verschiedenen Domänen über die Paketverwaltung hinaus in Visual Studio wiederverwendbar sind.
1. Wir untersuchen das Konzept von "privaten Abhängigkeiten", bei dem ein Paket angeben kann, dass es Abhängigkeiten von anderen Paketen für Implementierungsdetails aufweist, und diese Abhängigkeiten nicht als Abhängigkeiten auf oberster Ebene festzulegen sind.

## <a name="stay-tuned"></a>Bleiben Sie dran

Im [Blog](http://blog.nuget.org) erhalten Sie weitere Informationen zum Fortschritt und Ankündigungen für nuget 3,0!