---
title: Anmerkungen zur Version von NuGet-3.0-Vorschau | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 3.0 Preview einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-3.0 Preview Release Notes aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cf7cd17065e1c83beb935fe2969e6ecd8b52aa29
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-30-preview-release-notes"></a>Anmerkungen zur Version von NuGet-3.0-Vorschau

[Anmerkungen zu dieser Version von NuGet 2.9 RC](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta-Anmerkungen zu dieser Version](../release-notes/nuget-3.0-beta.md)

NuGet-3.0-Vorschau wurde am 12. November 2014 als Teil der Visual Studio 2015 Preview-Version veröffentlicht. NuGet-3.0 Preview veröffentlicht. Dies ist eine große Version für uns (obwohl es sich um eine Vorschau), und wir freuen uns, erste Feedback auf unsere Änderungen an.

## <a name="visual-studio-2012"></a>Visual Studio 2012+

Dieses NuGet-3.0-Vorschau ist in Visual Studio 2015 Preview enthalten. Wir arbeiten daran, löscht der Preview für Visual Studio 2012 und Visual Studio 2013 sehr schnell abzurufen. Wir haben unsere versucht, eine zuvor freigegeben [Updates für Visual Studio 2010 eingestellt](http://blog.nuget.org/20141002/visual-studio-2010.html), und wir haben diese schwierige Entscheidung vorgenommen.

## <a name="brand-new-ui"></a>Brandneuen UI

Erstes fällt Ihnen NuGet-3.0-Vorschau ist unsere brandneuen UI. Es ist nicht mehr ein modales Dialogfeld an. Es ist jetzt eine vollständige Dokumentfenster von Visual Studio. Dadurch können Sie die Benutzeroberfläche für mehrere Projekte (bzw. die Projektmappe) auf einmal öffnen, entfernen das Fenster deaktiviert auf einen anderen Bildschirm, docken sie jedoch, z. B. usw. möchten.

![Die neue NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

Über die Verwendbarkeit Unterschiede aufgrund aufgeben das modale Dialogfeld haben wir auch viele neue Funktionen in die neue Benutzeroberfläche.

### <a name="version-selection"></a>Versionsauswahl

Vielleicht die am häufigsten angefordert Benutzeroberflächenfunktion ist Versionsauswahl für die Paketinstallation "und" Update – ermöglicht dies ist jetzt verfügbar.

![Versionsauswahl Paket](./media/NuGet-3.0-Preview/version-selection.png)

Sie installieren oder Aktualisieren eines Pakets, können mit die Version-Dropdownliste alle Versionen verfügbar, für das Paket mit einigen wichtigen Versionen, die an den Anfang der Liste für die einfache Auswahl höher gestuft finden Sie unter. Sie müssen nicht mehr auf die PowerShell-Konsole zu verwenden, um bestimmte Versionen abzurufen, die nicht die neuesten sind.

### <a name="combined-installedonlineupdates-workflows"></a>Kombinierte installierte/Online/Updates Workflows

Unserer vorherigen GUI mussten 3 Registerkarten für Updates und installiert, Online. Die aufgelisteten Pakete wurden speziell für diese Workflows und die verfügbaren Aktionen wurden speziell für den Workflows auch. Während, die logisch, wir haben, dass viele von Ihnen oft würde schien erhalten Sie durch diese Trennung ausgeführt.

Wir haben jetzt eine kombinierte erzielen Sie, in dem Sie installieren, aktualisieren oder deinstallieren ein Paket, unabhängig davon, wie Sie das Paket ausgewählt haben. Zur Erleichterung der welche spezifischen Workflows wir verfügen jetzt über ein Dropdownmenü Filter aus, die Sie die Pakete, die sichtbar filtern kann, aber klicken Sie dann die Aktionen, die für das Paket verfügbar konsistent sind.

![Deinstallieren Sie ein Paket](./media/NuGet-3.0-Preview/uninstall-package.png)

Mit dem Filter "Installiert", klicken Sie dann einfach sehen Sie Ihre installierten Pakete, welche Updates auf dem aufweisen, und Sie können entweder deinstalliert oder ein update des Pakets durch Ändern der Versionsauswahl finden Sie unter Ändern Sie die Aktion verfügbar.

![Aktualisieren eines Pakets](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Version-Konsolidierung

Es ist üblich, das gleiche Paket in mehrere Projekte innerhalb einer Projektmappe installiert haben. Die Versionen in jedes Projekt installiert wird, können in einigen Fällen auseinander Abweichung und es ist notwendig, den verwendeten Versionen zu konsolidieren. NuGet-3.0-Vorschau wird nur in diesem Szenario eine neue Funktion eingeführt.

Das Verwaltungsfenster auf lösungsebene Paket kann zugegriffen werden, indem Sie mit der rechten Maustaste auf die Projektmappe und NuGet-Pakete für Projektmappe verwalten. Wenn Sie ein Paket auswählen, die in mehrere Projekte, aber mit unterschiedlichen Versionen verwendet wird, installiert ist, wird eine neue "Konsolidieren" Aktion dort verfügbar. Im Screenshot unten `Newtonsoft.Json` installiert wurde, in der `SamplesClassLibrary` mit Version `6.0.4` und installierten in `SamplesConsoleApp` mit Version `5.0.4`.

![Konsolidieren von Versionen](./media/NuGet-3.0-Preview/consolidate.png)

Dies ist der Workflow für die Konsolidierung auf eine einzelne Version.

1. Wählen Sie die `Newtonsoft.Json` Paket in der Liste
1. Wählen Sie `Consolidate` aus der `Action` Dropdownliste
1. Verwenden der `Version` Dropdownliste zum Auswählen der Version, konsolidiert werden
1. Aktivieren Sie die Kontrollkästchen für die Projekte, die auf diese Version (Beachten Sie, die bereits für die ausgewählte Version Projekte abgeblendet ist) konsolidiert werden sollen
1. Klicken Sie auf die `Consolidate` Schaltfläche für die Konsolidierung

### <a name="operation-previews"></a>Vorgangs-Vorschau

Unabhängig davon, welcher Vorgang durchführen – bietet die Benutzeroberfläche für die neue Installation/Update/Deinstallation – jetzt eine Möglichkeit, die Änderungen in der Vorschau anzeigen, die dem Projekt vorgenommen werden. Diese Vorschau werden keine neuen Pakete, die installiert werden, Pakete, werden aktualisiert, und die Pakete, angezeigt, die, zusammen mit Paketen deinstalliert werden sollen, die während des Vorgangs nicht geändert werden.

Im folgenden Beispiel sehen wir, dass das Microsoft.AspNet.SignalR Installation in ein paar Änderungen am Projekt führt.

![Installieren von SignalR Preview](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Installationsoptionen

Mithilfe der PowerShell-Konsole haben Sie die Kontrolle über ein paar wichtige Installationsoptionen hatten. Wir haben diese Funktionen nun in die auch die Benutzeroberfläche eingebunden. Sie können jetzt steuern die Abhängigkeit Auflösungsverhalten wie Versionen der Abhängigkeiten ausgewählt werden.

![Das abhängigkeitsverhalten](./media/NuGet-3.0-Preview/dependency-behavior.png)

Sie können auch angeben, dass die Aktion an, wenn Inhaltsdateien von Paketen mit Dateien, die bereits in Ihrem Projekt in Konflikt stehen.

![Datei-Konfliktlösung-Aktion](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Unbegrenzte Durchführen eines Bildlaufs

Wir zum ziemlich Feedback auf unserer GUI müssen beide den Bildlauf und paging Paradigmen beim Auflisten von Paketen abrufen. Es wurde relativ üblich, um einen Bildlauf zum unteren Rand der kurze Liste und klicken Sie auf die Anzahl der nächsten Seite blättern Sie dann erneut zu verwenden. Mit der neuen Benutzeroberfläche haben wir die unendliche Bildlauf in der Liste der Pakete, Sie nur Scrollen--Paging nicht mehr müssen implementiert.

![Unbegrenzte Durchführen eines Bildlaufs](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Erleichtern Sie Arbeit, können sie die schnelle, unbedingt Schöndruck

Wir freuen uns, diese neue Benutzeroberfläche für die Sie testen abzurufen. Während dieser Milestone Vorschau haben wir. befolgen die gute alte Sprichwort erwiesen, der "" Stellen sie arbeiten, können sie schnell, besser formatieren." In dieser Vorschau haben wir die meisten erreicht der das erste Ziel – es funktioniert. Wir wissen, es ist sehr schnell noch nicht, und wir wissen, dass es sich nicht sehr ziemlich noch handelt. Vertrauen Sie, dass es für diese Ziele zwischen sofort aus, und die RC-Version aktiv werden müssen. In der Zwischenzeit können wir würden uns über Ihr Feedback freuen, zu der *benutzerfreundlichkeit* der neuen Benutzeroberfläche--der Workflows, die Vorgänge, und wie es *idealer* mithilfe die Benutzeroberfläche für neue.

Es gibt eine Reihe von Funktionen, die wir im Vergleich zu den alten UI entfernt haben. Eines der folgenden beabsichtigt war und anderen Knoten gerade nicht geschieht zeitlich.

#### <a name="searching-all-package-sources"></a>"Alle" Paketquellen suchen

Die alte Benutzeroberfläche konnten Sie in einem Paket für alle Ihre Paketquellen gesucht. Wir haben diese Funktion in der Benutzeroberfläche entfernt und es wird nicht werden danach zurück. Diese Funktion zum Ausführen von Suchvorgängen für alle Ihre Paketquellen verwendet die Ergebnisse zusammen mit Ihrer Hilfe, und versuchen zum Sortieren der Ergebnisse basierend auf Ihrer Auswahl sortieren.

Es wurde erkannt, dass Suchrelevanz nur schwer zu zusammen mit Ihrer Hilfe. Vorstellbar bei der Suche für Google und Bing und die Ergebnisse zusammen dabei? Darüber hinaus war diese Funktion langsam, leicht zu *versehentlich* verwenden, und wir glauben, dass es nur selten tatsächlich nützlich waren. Aufgrund der Probleme empfangen die Funktion eingeführt, wir eine Anzahl von Problemberichte darauf, die nie konnten behoben wurden.

#### <a name="update-all"></a>Alle aktualisieren

Wird verwendet, um eine Schaltfläche "Alle aktualisieren" in der alten Benutzeroberfläche haben, die es in der Benutzeroberfläche für neue noch nicht. Wir werden diese Funktion für unsere RC-Version aufrufen.

## <a name="new-clientserver-api"></a>Neue Client/Server-API

Zusätzlich zu allen neuen Funktionen in unserer neuen Paket-Benutzeroberfläche haben wir auch einige Implementierungsdetails für NuGet Client/Server-Protokoll gearbeitet. Unsere Arbeit ist die Erstellung von "API v3" für NuGet, das entworfen wurde, um hohe Verfügbarkeit für kritische Szenarien wie paketwiederherstellung und Installieren von Paketen. Die neue API basiert auf REST und Hypermedia und wir ausgewählt haben [JSON-LD](http://json-ld.org) als Ressourcenformat.

In den Bits NuGet 3.0 Vorschau finden Sie unter neue Paketquelle "preview.nuget.org" in der Dropdownliste der Paket-Quelle aufgerufen. Bei Auswahl dieser Paketquelle verwenden wir unserer neuen API zur Verbindung mit nuget.org. Wir haben die Preview-Quelle in der Benutzeroberfläche zur Verfügung gestellt, während wir weiterhin die testen, überarbeiten und verbessern die neue API. In NuGet 3.0 RC ersetzt dieser neuen API v3-basierte Paketquelle die Paketquelle v2-basierte "nuget.org".

Trotz der Investition, die wir in API v3 bereitstellen, haben wir versucht, alle diese neuen Funktionen auch mit unsere vorhandene API v2-Protokolls arbeiten, d. h. mit vorhandenen Paketquellen als nuget.org ebenfalls funktionieren.

## <a name="new-features-coming"></a>Neuen Features

Bis jetzt 3.0 RTM arbeiten wir auch über einige grundlegenden neuen NuGet-Funktionen, über hinaus Sie in der Benutzeroberfläche sehen. Hier ist eine kurze Liste der wichtigsten Bereiche:

1. Wir sind Partnerschaften mit Visual Studio und MSBuild um erhalten die teams [NuGet tiefer in der Plattform](http://blog.nuget.org/20141014/in-the-platform.html).
1. Wir arbeiten daran verwerfen Installationszeit Paket Konventionen und stattdessen zur Verpackungszeit dieser Konventionen anwenden, durch die Einführung eines neuen "autorisierend" [Paketmanifest](http://blog.nuget.org/20141023/package-manifests.html).
1. Wir arbeiten für die Umgestaltung der NuGet codebase, um die Client- und Serverkomponenten in unterschiedlichen Domänen außerhalb der paketverwaltung in Visual Studio wiederverwendbar machen.
1. Wir sind untersuchen das Problem des Begriff "private Abhängigkeiten", in denen ein Paket, dass die It angeben kann, ist unabhängig von anderen Paketen für nur Implementierungsdetails und diese Abhängigkeiten sollten nicht als der obersten Ebene Abhängigkeiten angefügt werden.

## <a name="stay-tuned"></a>Bleiben Sie dran

Bitte achten Sie auf [unserem Blog](http://blog.nuget.org) weitere Bearbeitung und Ankündigungen für NuGet 3.0!