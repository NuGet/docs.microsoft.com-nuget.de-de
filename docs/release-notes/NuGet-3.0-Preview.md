---
title: Anmerkungen zu NuGet 3.0 Preview
description: Anmerkungen zu NuGet 3.0 Vorschauversion ein, wie bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9389639476172d05556b95d589e429ddfe0e3026
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546464"
---
# <a name="nuget-30-preview-release-notes"></a>Anmerkungen zu NuGet 3.0 Preview

[Anmerkungen zu dieser Version von NuGet 2.9 RC](../release-notes/nuget-2.9-rc.md) | [Anmerkungen zu NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md)

NuGet 3.0-Vorschauversion wurde am 12. November 2014 als Teil der Visual Studio 2015 Preview-Version veröffentlicht. NuGet 3.0 Preview veröffentlicht. Dies ist ein umfangreiches Release für uns, (wenn auch eine Vorschau), und wir freuen uns, die ab jetzt erhalten Sie Feedback zu unseren Änderungen.

## <a name="visual-studio-2012"></a>Visual Studio 2012 und höher

Dieser Preview-Version des NuGet 3.0 ist in Visual Studio 2015 Preview enthalten. Wir arbeiten daran, Vorschau löscht sehr bald für Visual Studio 2012 und Visual Studio 2013 machen. Wir haben unsere Absicht, zuvor freigegeben [Updates für Visual Studio 2010 eingestellt](http://blog.nuget.org/20141002/visual-studio-2010.html), und wir, schwierige Entscheidung treffen.

## <a name="brand-new-ui"></a>Neue Benutzeroberfläche

Als Erstes fällt Ihnen NuGet 3.0 Preview ist unsere neue Benutzeroberfläche. Es ist nicht mehr ein modales Dialogfeld an. Es ist jetzt ein vollständiger Dokumentfenster von Visual Studio. Dadurch können Sie die Benutzeroberfläche für mehrere Projekte (bzw. die Projektmappe) auf einmal öffnen, entfernen das Fenster aus, auf einen anderen Bildschirm, jedoch, wie z. B. usw. möchten Andocken.

![Die neue NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

Über die Nutzbarkeit Unterschiede aufgrund das modale Dialogfeld Abbrechen haben wir auch viele neue Features in der neuen Benutzeroberfläche.

### <a name="version-selection"></a>Versionsauswahl

Vielleicht am häufigsten gewünscht UI-Funktion ist, um Auswahl für die Paketinstallation und Update - Version zu ermöglichen. Dies ist jetzt verfügbar.

![Paket-Versionsauswahl](./media/NuGet-3.0-Preview/version-selection.png)

Sie installieren oder Aktualisieren eines Pakets, kann der versionsdropdownliste aus Sie alle Versionen zur Verfügung, für das Paket mit einigen wichtigen Versionen höher gestuft, an den Anfang der Liste für die einfache Auswahl finden Sie unter. Sie müssen nicht mehr auf die PowerShell-Konsole verwenden, um bestimmte Versionen zu erhalten, die nicht die neueste Version.

### <a name="combined-installedonlineupdates-workflows"></a>Kombinierte installierte/Online/Updates-Workflows

Unsere vorherigen UI mussten 3 Registerkarten installiert, Online, und Updates. Die aufgeführten Pakete wurden speziell für diese Workflows und die verfügbaren Aktionen wurden speziell für den Workflows auch. Während, die logische schien, gehört es, dass viele von Ihnen oft durch diese Trennung gebracht erhalten würde.

Wir haben jetzt eine kombinierte zu, in dem Sie installieren, aktualisieren oder Deinstallieren eines Pakets, unabhängig davon, wie Sie das Paket ausgewählt haben. Um mit den Workflows zu unterstützen, wir verfügen jetzt über ein Filter-Dropdownmenü, in dem Sie die Pakete, die sichtbar filtern kann, aber klicken Sie dann die Aktionen für das Paket konsistent sind.

![Deinstallieren eines Pakets](./media/NuGet-3.0-Preview/uninstall-package.png)

Verwenden den Filter "Installiert", klicken Sie dann ganz einfach erkennen Sie Ihre installierten Pakete, welche über die verfügbaren Updates verfügen, und klicken Sie dann können Sie entweder deinstallieren oder Aktualisieren des Pakets durch Ändern der Versionsauswahl finden Sie unter Ändern Sie die Aktion zur Verfügung.

![Aktualisieren eines Pakets](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Version-Konsolidierung

Es ist üblich, die das gleiche Paket in mehreren Projekten innerhalb einer Projektmappe installiert wird, verwenden. Die Versionen in jedem Projekt installiert wird, können manchmal voneinander abweichen, und es ist notwendig, den verwendeten Versionen zu konsolidieren. NuGet 3.0 Preview lernen Sie ein neues Feature für genau dieses Szenario.

Verwaltungsfenster auf Projektmappenebene-Paket kann zugegriffen werden, indem Sie mit der rechten Maustaste auf die Projektmappe und Auswählen von NuGet-Pakete für Projektmappe verwalten. Wenn Sie ein Paket auswählen, die in mehrere Projekte, aber mit unterschiedlichen Versionen verwendet werden, installiert ist, wird eine neue Aktion für "Konsolidieren" dort verfügbar. Im Screenshot unten `Newtonsoft.Json` installiert wurde, in der `SamplesClassLibrary` mit Version `6.0.4` und installierten in `SamplesConsoleApp` mit Version `5.0.4`.

![Konsolidieren von Versionen](./media/NuGet-3.0-Preview/consolidate.png)

So sieht der Workflow für die Konsolidierung auf eine einzelne Version aus.

1. Wählen Sie die `Newtonsoft.Json` Paket in der Liste
1. Wählen Sie `Consolidate` aus der `Action` Dropdownliste
1. Verwenden der `Version` Dropdownliste zum Auswählen der Version auf konsolidiert werden soll
1. Aktivieren Sie die Kontrollkästchen für die Projekte, die auf diese Version (Beachten Sie, die Projekte, die bereits für die ausgewählte Version abgeblendet ist) konsolidiert werden soll
1. Klicken Sie auf die `Consolidate` Schaltfläche, um die Konsolidierung durchführen

### <a name="operation-previews"></a>Vorgang Vorschauversionen

Unabhängig davon, welcher Vorgang, die Sie durchführen – bietet die Benutzeroberfläche für die neue Installation/Aktualisierung/Deinstallation – jetzt eine Möglichkeit, eine Vorschau der Änderungen, die zu Ihrem Projekt vorgenommen werden. Dieser Preview-Version werden neue Pakete, die installiert werden, Pakete, die aktualisiert werden, und die Pakete angezeigt, die, zusammen mit Paketen deinstalliert werden, die während des Vorgangs nicht geändert werden.

Im folgenden Beispiel sehen wir, dass das Installieren der Microsoft.AspNet.SignalR einige Änderungen auf das Projekt führt.

![Installieren von SignalR (Vorschau)](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Installationsoptionen

Verwenden die PowerShell-Konsole, hatten Sie Kontrolle über ein paar wichtige Installationsoptionen. Wir haben diese Funktionen jetzt in der Benutzeroberfläche sowie geschaltet. Sie können jetzt steuern, dass die Abhängigkeit Auflösungsverhalten wie die Abhängigkeiten ausgewählt werden.

![Verhalten der Abhängigkeit](./media/NuGet-3.0-Preview/dependency-behavior.png)

Sie können auch angeben, dass die Aktion an, wenn Inhaltsdateien von Paketen mit Dateien bereits im Projekt in Konflikt stehen.

![Datei-Konfliktlösung-Aktion](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Unbegrenzte Bildläufe

Es verwendet, um ein wenig des Feedbacks unserer GUI müssen sowohl den Bildlauf und Paradigmen paging, wenn Pakete aufgelistet. Es war ziemlich üblich, einen Bildlauf zum unteren Rand die kurze Liste und klicken Sie auf die Nummer der nächsten Seite blättern Sie dann erneut zu verwenden. Mit der neuen Benutzeroberfläche haben wir die unbegrenzte Bildläufe in der Paketliste, Sie nur Scrollen – keine weiteren Paging müssen implementiert.

![Unbegrenzte Bildläufe](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Erleichtern Sie Arbeit, stellen Sie schnelle, machen es sehr

Wir freuen uns, diese neue Benutzeroberfläche für die Sie testen zu machen. Während dieser Preview-Meilenstein, wir haben befolgen die gute alte Spruch der "Mach es funktioniert, können sie schnell, besser formatieren." In dieser Vorschau haben wir die meisten erreicht der das erste Ziel – es funktioniert. Wir wissen es sehr schnell noch nicht, und wir wissen, dass es ganz Recht noch nicht ist. Vertrauen Sie, dass wir werden auf diese Ziele zwischen jetzt und die RC-Version arbeiten. In der Zwischenzeit wir würden uns über Ihr Feedback hören die *benutzerfreundlichkeit* der neuen Benutzeroberfläche – die Workflows, Betrieb, und wie es *fühlt* verwenden Sie die neue Benutzeroberfläche.

Es gibt eine Reihe von Funktionen, die wir im Vergleich zur alten Benutzeroberfläche entfernt haben. Eines der folgenden haben wir absichtlich getan, und der andere eine gerade nicht erledigt rechtzeitig.

#### <a name="searching-all-package-sources"></a>Suchen "All" Paketquellen

Die alte Benutzeroberfläche konnten Sie eine paketsuche für alle Ihre Paketquellen durchzuführen. Wir haben dieses Feature in der Benutzeroberfläche entfernt und es wird nicht werden schaltet sie wieder. Diese Funktion verwendet, um den Search-Vorgängen für alle Ihre Paketquellen und binden die Ergebnisse zusammen, und versuchen zum Sortieren der Ergebnisse basierend auf Ihrer Auswahl sortieren.

Wir festgestellt, dass die Suchrelevanz nur schwer zu zusammen mit Ihrer Hilfe ist. Können Sie sich vorstellen, Durchführen einer Suche mit Google und Bing und bearbeiten die Ergebnisse zusammen? Darüber hinaus wurde dieses Feature, langsam ist, einfach zu *versehentlich* verwenden, und wir sind der Meinung war es nur selten tatsächlich nützlich. Aufgrund der Probleme, wurden die das Feature eingeführt, eine Anzahl von Fehlerberichten auf, die noch nie konnten behoben wurden.

#### <a name="update-all"></a>Alle aktualisieren

Um eine Schaltfläche "Alle aktualisieren" in der alten Benutzeroberfläche zu erhalten, die es in der neuen Benutzeroberfläche noch nicht verwendet. Wir werden dieses Feature für unsere RC-Version erwecken.

## <a name="new-clientserver-api"></a>Neue Client/Server-API

Zusätzlich zu allen neuen Funktionen in unserer neuen paketverwaltungs-UI haben wir auch einige Implementierungsdetails für NuGets-Client/Server-Protokoll gearbeitet. Die Arbeit habe ist die Erstellung von "-API v3" für NuGet, das entworfen wurde, um hochverfügbarkeit für kritische Szenarien wie z. B. das Wiederherstellen von Paketen und Installieren von Paketen. Die neue API basiert auf REST und Hypermedia, und wir ausgewählt haben [JSON-LD](http://json-ld.org) als unsere Ressourcenformat.

In der NuGet 3.0 Preview-Teile sehen Sie eine neue Paketquelle, die Namen "preview.nuget.org" in der Dropdownliste der Paket-Quelle. Wenn Sie diese Paketquelle auswählen, verwenden wir unsere neue API, sondern für die Verbindung "NuGet.org". Wir haben die Preview-Quelle in der Benutzeroberfläche verfügbar gemacht, während wir weiterhin zu testen, überarbeiten und verbessern die neue API. In NuGet 3.0 RC wird diese neue API-v3-basierte Paketquelle Paketquelle von v2-basierte "nuget.org" ersetzt.

Trotz der Investition, die wir in-API v3 ablegen, haben wir all diese neuen Features auch mit unserer vorhandenen API-v2-Protokoll, arbeiten, was bedeutet, dass sie mit vorhandenen Paketquellen als "NuGet.org" auch funktionieren vorgenommen.

## <a name="new-features-coming"></a>Neuen Funktionen

Zwischen jetzt und RTM-Version 3.0 arbeiten wir auch über einige grundlegenden neuen NuGet Funktionen, nach was Sie in der Benutzeroberfläche angezeigt wird. Hier ist eine kurze Liste der wichtigsten Investitionsbereiche:

1. Eine Partnerschaft möchten wir mit dem Visual Studio und MSBuild-teams um erhalten [NuGet tiefer in die Plattform](http://blog.nuget.org/20141014/in-the-platform.html).
1. Wir arbeiten daran, Installationszeit paketkonventionen Abbrechen und stattdessen diese Konventionen zur Verpackungszeit anwenden, durch die Einführung einer neuen "autorisierend" [Paketmanifest](http://blog.nuget.org/20141023/package-manifests.html).
1. Wir arbeiten daran, für das Umgestalten des NuGet-Pakets Codebasis, um die Client- und Serverkomponenten in unterschiedlichen Domänen außerhalb der paketverwaltung in Visual Studio wiederverwendbarkeit sicherzustellen.
1. Wir untersuchen das Konzept der "private Abhängigkeiten", ein Paket, dass die It angeben kann, verfügt über Abhängigkeiten von anderen Paketen nur Implementierungsdetails, und diese Abhängigkeiten sollten nicht als Abhängigkeiten der obersten Ebene angezeigt werden.

## <a name="stay-tuned"></a>Bleiben Sie dran

Bitte achten Sie auf [unseren Blog](http://blog.nuget.org) für die weitere Bearbeitung sowie Ankündigungen von NuGet 3.0!