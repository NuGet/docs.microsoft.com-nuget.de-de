---
title: Anmerkungen zu NuGet 2.6
description: Anmerkungen zu NuGet 2.6.1 für WebMatrix, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f011a8db7ac2067a2ed7db67849d63f7dd40d1ce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551942"
---
# <a name="nuget-26-release-notes"></a>Anmerkungen zu NuGet 2.6

[Anmerkungen zu NuGet 2.5](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 für WebMatrix-Versionshinweise](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet ab Version 2.6 wurde am 26. Juni 2013 veröffentlicht.

## <a name="notable-features-in-the-release"></a>Wichtige Features in der Version

### <a name="support-for-visual-studio-2013"></a>Unterstützung für Visual Studio 2013

NuGet ab Version 2.6 wird die erste Version, die Unterstützung für Visual Studio 2013 bietet. Und wie Visual Studio 2012, die NuGet-Paket-Manager-Erweiterung ist in jeder Edition von Visual Studio enthalten.

Um die bestmögliche Unterstützung für Visual Studio 2013, während weiterhin sowohl Visual Studio 2010 und Visual Studio 2012 unterstützt, und halten die Erweiterung Größen so klein wie möglich bereitzustellen, erzeugen wir separate Erweiterung für Visual Studio 2013, während die ursprüngliche Erweiterung weiterhin sowohl Visual Studio 2010 und 2012 ausgerichtet.

Ab NuGet ab Version 2.6 können veröffentlichen zwei Erweiterungen wie folgt wir:

1. [NuGet-Paket-Manager](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (gilt für Visual Studio 2010 und 2012)
1. [NuGet-Paket-Manager für Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Mit diesen Teilen die ["NuGet.org"](https://nuget.org) "Installieren von NuGet"-Schaltfläche "Startseite" gelangen Sie zu der [Installieren von NuGet](../install-nuget-client-tools.md) Seite Sie weitere Informationen zum Installieren der verschiedenen NuGet-Clients Hier können.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Unterstützung von XDT "Web.config" für Transformationen

Eine stark nachgefragte Funktionen für den NuGet-Client wurde zur Unterstützung von leistungsstarke XML-Transformations mit der XDT Transformations-Engine die in Visual Studio Build Konfiguration von Transformationen verwendet wird.

Im April 2013 haben wir zwei große Ankündigungen zu NuGet-Unterstützung für XDT. Die erste war, dass die XDT-Bibliothek selbst selbst wird wurde [als NuGet-Paket veröffentlicht](https://nuget.org/packages/Microsoft.Web.Xdt) und [Open Source auf CodePlex](http://xdt.codeplex.com/). Dieser Schritt aktiviert die XDT-Engine frei von andere Open Source-Software, einschließlich des NuGet-Clients verwendet werden. Die zweite Ankündigung wurde der Plan für die Unterstützung der XDT-Engine für Transformationen im NuGet-Client. NuGet ab Version 2.6 enthält diese Integration.

#### <a name="how-it-works"></a>So funktioniert es

Um NuGets-Unterstützung von XDT nutzen zu können, ähneln sich die Funktionsweise mit denen die [Transformationsfunktion für die aktuelle Konfiguration](../create-packages/source-and-config-file-transformations.md).
Transformationsdateien werden die Paket Ordner "Content" hinzugefügt. Während der Config-Transformationen über eine einzelne Datei für Installation und Deinstallation verwenden, aktivieren mithilfe von XDT-Transformationen jedoch eine präzisere Kontrolle über diese beiden Vorgänge mithilfe der folgenden Dateien:

- Web.config.Install.XDT
- Web.config.Uninstall.XDT

Darüber hinaus verwendet NuGet das Dateisuffix, um zu bestimmen, welche Engine für Transformationen ausgeführt werden, damit Pakete mithilfe der vorhandenen web.config.transforms weiterhin funktionieren. XDT-Transformationen können auch angewendet werden, für jede XML-Datei (nicht nur "Web.config"), sodass Sie dies in Ihrem Projekt für andere Anwendungen nutzen können.

#### <a name="what-you-can-do-with-xdt"></a>Was können Sie mit XDT tun.

Einer der größten Stärken von XDT ist der [einfachen, aber leistungsfähigen Syntax](http://msdn.microsoft.com/library/dd465326.aspx) für die Bearbeitung der Struktur einer XML-DOM. Überlagern einfach auf eine andere Struktur einer fixierten Dokuments-Struktur, bietet mithilfe von XDT Steuerelemente für übereinstimmende Elemente in einer Vielzahl von Möglichkeiten, von einfachen Attribut Name zugeordnet werden, um die vollständige XPath-Unterstützung. Wenn ein übereinstimmendes Element oder eine Gruppe von Elementen gefunden wurde, bietet mithilfe von XDT einen umfangreichen Satz von Funktionen zum Bearbeiten von den Elementen, ob das bedeutet, hinzufügen, aktualisieren oder Entfernen von Attributen, platzieren ein neues Element an einem bestimmten Speicherort, oder ersetzen oder entfernen die gesamte Element und seine untergeordneten Elemente.

### <a name="machine-wide-configuration"></a>Konfiguration des Computers

Der große Vorteile von NuGet ist, dass er eine andernfalls große ausführbare oder in einen Satz von modulare Komponenten, die integrierte und allem verwaltet und versioniert unabhängig können unterteilt. Ein Nebeneffekt dieser, ist jedoch, dass das herkömmliche Konzept eines Produkts oder einer Produktfamilie potenziell mehr fragmentiert wird.
Feature für die NuGet-anpassungspaket-Quelle bietet eine Möglichkeit zum Organisieren von Paketen; Benutzerdefinierte Paketquellen sind jedoch nicht selbst ermittelt.

NuGet ab Version 2.6 wird die Logik für die Konfiguration von NuGet Durchsuchen der Ordnerhierarchie unter dem Pfad % ProgramData%/NuGet/Config erweitert. Produktinstallationsprogramme können benutzerdefinierte NuGet-Konfigurationsdateien in diesem Ordner zum Registrieren einer benutzerdefinierten Paketquelle für ihre Produkte hinzufügen. Darüber hinaus unterstützt die Ordnerstruktur Semantik für Produkt, Version und sogar die IDE-SKU. Einstellungen in diesen Verzeichnissen werden in der folgenden Reihenfolge mit einer Strategie für "last in Wins" Rangfolge angewendet.

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*config
3. %ProgramData%\NuGet\Config\{IDE}\{Version}\*config
4. %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*config

In dieser Liste ist der Platzhalter {IDE} speziell für die IDE, die in der NuGet ausgeführt wird, damit im Fall von Visual Studio sie "Visual Studio" werden. Die {Version} und {SKU}-Platzhalter (z. B. von der IDE bereitgestellt werden "11,0" und "WDExpress", "VWDExpress" und "Pro" bzw.). Der Ordner kann dann viele verschiedene *.config-Dateien enthalten.
Aus diesem Grund kann der Firma ACME Komponente als Teil ihrer Product-Installer, eine benutzerdefinierte Paketquelle hinzufügen, die nur im der Professional oder Ultimate-Edition von Visual Studio 2012 angezeigt werden kann, indem Sie den folgenden Dateipfad erstellen:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Während die Ordnerstruktur für Programme wie softwareinstallationsprogramme computerweite Paketquellen zu NuGet Konfiguration hinzufügen einfach erleichtert, wurde das NuGet-Dialogfeld "Konfiguration" auch aktualisiert, um für die Registrierung von Paketquellen als zulassen entweder (z. B. in % AppData%/NuGet/NuGet.Config registriert) benutzerspezifische oder computerweite.

Dieses Feature wird von Visual Studio 2013 verwendet, in dem eine Datei am installiert ist:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

In dieser Datei ist eine neue Paketquelle, die auch ".NET Framework-Pakete" konfiguriert.

![Große computereinstellungen NuGet-Konfigurationsdatei](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Kontextualisieren von Suchen

Wächst die Anzahl der Pakete, die von der NuGet Gallery bedient nimmt, bleibt die Verbessern der Suche nach jemals am oberen Rand der Liste der NuGet-Priorität. Eine der geplanten Funktionen für NuGet ist Kontextsuche, was bedeutet, dass NuGet Informationen über die Version und SKU von Visual Studio, die Sie verwenden und den Typ des Projekts, die Sie erstellen als Kriterium verwenden für die Bestimmung der Relevanz von potenziellen suchen Ergebnisse.

Ab NuGet ab Version 2.6, wird jedes Mal, wenn ein Paket installiert ist, der Kontext für die Installation als Teil der Daten zur Installation Vorgang aufgezeichnet.  Suchvorgänge senden Ihnen außerdem die gleichen Kontextinformationen, sodass im NuGet-Katalog, um Suchergebnisse durch kontextabhängige Installation Trends zu steigern.  Einem zukünftigen Update von NuGet-Katalog können diese Verstärkung der kontextbezogenen Relevanz.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Abfragen mit nachverfolgung Vs direkt installiert. Abhängigkeit wird installiert

Paketersteller sind der vertrauenden Seite mehr und mehr auf die [Paket Statistiken](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) im NuGet-Katalog bereitgestellt.  Eine wichtige fehlende Daten zeigen, dass die Autoren für gebeten haben ist es sich um eine Unterscheidung zwischen direkter Paketinstallationen und Abhängigkeiten installiert.  Bis jetzt der NuGet-Client nicht senden einen beliebigen Kontext rund um den Installationsvorgang für gibt an, ob der Entwickler das Paket direkt installiert oder ob sie installiert wurde, um eine Abhängigkeit zu erfüllen.
Das Starten mit NuGet 2.6 Daten werden jetzt für den Installationsvorgang gesendet.  Paket Statistiken auf der NuGet Gallery werden diese Daten als separate Installationsvorgänge verfügbar machen, mit einem "-Abhängigkeit" Suffix.

* Installieren
* Install-Abhängigkeit
* Update
* Update-Abhängigkeit
* Neuinstallation
* Installieren von Abhängigkeiten

Zusätzlich zu den anderen Vorgangsnamen wird die abhängige Paket-Id für die Installation auch aufgezeichnet.  Einem zukünftigen Update von NuGet-Katalog wird verfügbar gemacht, diese Daten in Berichten und ermöglichen so Paketersteller vollständig zu verstehen, wie Entwickler ihre Pakete installieren.

## <a name="bug-fixes"></a>Fehlerkorrekturen

NuGet ab Version 2.6 enthält auch mehrere Fehler behoben. Eine vollständige Liste der Arbeit Elemente eine feste in NuGet 2.6 Bitte Ansicht der [NuGet Issue Tracker für diese Version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).