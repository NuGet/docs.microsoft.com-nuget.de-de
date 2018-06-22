---
title: NuGet-2.6-Versionshinweise
description: Versionshinweise für NuGet 2.6.1 für WebMatrix, einschließlich der bekannten Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39ce6ac3d36464d26966b0dabb0893f09ad4afdc
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821901"
---
# <a name="nuget-26-release-notes"></a>NuGet-2.6-Versionshinweise

[Anmerkungen zur Version von NuGet 2.5](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 WebMatrix-Versionshinweise](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet-2.6 wurde am 26. Juni 2013 veröffentlicht.

## <a name="notable-features-in-the-release"></a>Wichtige Funktionen in der Version

### <a name="support-for-visual-studio-2013"></a>Unterstützung für Visual Studio 2013

NuGet-2.6 ist die erste Version, die Unterstützung für Visual Studio 2013 bereitstellt. Und wie Visual Studio 2012, die NuGet-Paket-Manager-Erweiterung in jeder Edition von Visual Studio enthalten ist.

Um die beste Möglichkeit Unterstützung für Visual Studio 2013 zugleich Unterstützung von Visual Studio 2010 und Visual Studio 2012, und halten die Erweiterung Größen so klein wie möglich zu bieten, werden wir eine separate Erweiterung für Visual Studio 2013 beim Erzeugen der ursprünglichen Erweiterung weiterhin für Visual Studio 2010 and 2012 gelten.

Mit NuGet 2.6 beginnen, werden zwei Erweiterungen wie unten beschrieben veröffentlichen:

1. [NuGet Package Manager](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (gilt für Visual Studio 2010 and 2012)
1. [NuGet-Paket-Manager für Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Mit diesen Teilen der [nuget.org](https://nuget.org) Startseite ""Installieren von NuGet"Schaltfläche gelangen Sie zur der [Installieren von NuGet](../install-nuget-client-tools.md) Seite, in denen Sie weitere Informationen zum Installieren der verschiedenen NuGet-Clients suchen können.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Die Transformation Unterstützung XDT "Web.config"

Eine der Funktionen für den NuGet-Client hoch angefordert wurde zur Unterstützung von leistungsfähiger XML-Transformations, die mit XDT Transformationsmodul die in Visual Studio Build Configuration Transformationen verwendet wird.

Im April 2013 haben wir zwei große Ankündigungen zu NuGet-Unterstützung für XDT haben. Die erste wurde, dass die XDT-Bibliothek selbst selbst gleichzeitig wurde [als NuGet-Paket veröffentlicht](https://nuget.org/packages/Microsoft.Web.Xdt) und [Open Source auf CodePlex](http://xdt.codeplex.com/). Dieser Schritt aktiviert das Modul XDT frei von anderen Open-Source-Software, einschließlich des NuGet-Clients verwendet werden. Die zweite Ankündigung wurde der Plan für die Unterstützung von XDT-Modul für Transformationen im NuGet-Client. NuGet-2.6 umfasst diese Integration.

#### <a name="how-it-works"></a>Informationen zur Funktionsweise

Um NuGet XDT-Unterstützung nutzen zu können, ähneln sich die Mechanismen, die von der [Transformationsfunktion für die aktuelle Konfiguration](../create-packages/source-and-config-file-transformations.md).
Transformationsdateien werden Inhaltsordner des Pakets hinzugefügt. Während eine einzelnen Datei Config Transformationen für die Installation und Deinstallation verwendet werden, aktivieren Sie XDT Transformationen jedoch eine präzisere Kontrolle über diese beiden Vorgänge verwenden die folgenden Dateien:

- Web.config.Install.XDT
- Web.config.Uninstall.XDT

Darüber hinaus verwendet NuGet das Dateisuffix, um zu bestimmen, welches Modul für Transformationen, ausgeführt werden, damit Pakete mithilfe der vorhandenen web.config.transforms weiterhin funktionieren. XDT-Transformationen können auch in eine XML-Datei (nicht nur "Web.config"), angewendet werden, damit Sie diese für andere Anwendungen in Ihrem Projekt nutzen können.

#### <a name="what-you-can-do-with-xdt"></a>Was können Sie mit XDT tun.

Einer der größten Stärken des XDT ist seine [einfache, aber leistungsfähigen Syntax](http://msdn.microsoft.com/library/dd465326.aspx) für die Struktur einer XML-DOM. bearbeiten Überlagern einfach einen festen Dokumentstruktur auf einer anderen Struktur, bietet XDT Steuerelemente für den Abgleich von Elementen in einer Vielzahl von Möglichkeiten, einfaches Attribut Name gefunden wird, um die vollständige XPath-Unterstützung. Sobald ein übereinstimmendes Element oder eine Gruppe von Elementen gefunden wird, bietet XDT einen umfangreichen Satz von Funktionen zum Bearbeiten der Elemente, ob bedeutet, dass hinzufügen, aktualisieren oder Entfernen von Attributen, platzieren ein neues Element an einem bestimmten Speicherort, oder ersetzen oder entfernen die gesamte Element und seine untergeordneten Elemente.

### <a name="machine-wide-configuration"></a>Computerweite-Konfiguration

Einer der großen Vorteile von NuGet ist, dass er eine andernfalls große ausführbare Datei oder Bibliothek in einer Reihe von modulare Komponenten, die integrierten, und vor allem verwaltet und mit Versionsangabe unabhängig sein kann unterteilt. Ein Nebeneffekt hiervon, ist jedoch, dass das herkömmliche Konzept eines Produkts oder der Produktfamilie möglicherweise mehr fragmentiert ist.
NuGet angepasstes Paket Quelle-Funktion bietet eine Möglichkeit zum Organisieren von Paketen; Benutzerdefinierte Paketquellen sind jedoch nicht auf ihre eigenen erkennbar.

NuGet-2.6 erweitert die Logik für NuGet konfigurieren, indem Sie die Ordnerhierarchie unter dem Pfad% ProgramData%/NuGet/Config suchen. Produktinstallationsprogramme können benutzerdefinierte NuGet-Konfigurationsdateien unter diesem Ordner so registrieren eine benutzerdefinierte Paketquelle für ihre Produkte hinzufügen. Darüber hinaus unterstützt die Ordnerstruktur Semantik für Produkt, Version und sogar SKU der IDE an. Einstellungen für diese Verzeichnisse werden in der folgenden Reihenfolge mit einer Strategie für "last in Wins" Rangfolge angewendet.

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*config
3. %ProgramData%\NuGet\Config\{IDE}\{Version}\*config
4. %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*config

In dieser Liste bezieht sich der Platzhalter {IDE} auf der IDE in der NuGet ausgeführt wird, damit im Fall von Visual Studio können sie "VisualStudio" werden. Der {Version} und {SKU} Platzhalter (z. B. von der IDE bereitgestellt werden "11,0" und "WDExpress", "VWDExpress" und "Pro" bzw.). Der Ordner kann dann viele verschiedene *.config-Dateien enthalten.
Aus diesem Grund kann, das ACME Komponente Unternehmen als Teil ihrer Produktinstallationsprogramm, eine benutzerdefinierte Paketquelle hinzufügen, die nur in der Professional oder Ultimate Edition von Visual Studio 2012 sichtbar sein wird, indem Sie den folgenden Dateipfad erstellen:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Während die Ordnerstruktur für Programme wie softwareinstallationsprogramme Paketquellen computerweiter NuGet Konfiguration hinzufügen einfach macht, wurde die NuGet-Dialogfeld "Konfiguration" auch aktualisiert, um für die Registrierung der Paketquellen als zulassen entweder (z. B. in % AppData%/NuGet/NuGet.Config registriert) benutzerspezifische oder computerweite.

Dieses Feature wird von Visual Studio 2013 verwendet, in dem eine Datei am installiert ist:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

In dieser Datei ist eine neues Paket Datenquelle mit dem Namen ".NET Framework-Pakete" konfiguriert.

![NuGet-Datei "App.config" wide computereinstellungen](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Contextualizing suchen

Wie die Anzahl der Pakete, die von der NuGet Gallery verarbeitet eine exponentielle Tempo wachsen weiterhin, bleibt die Verbessern der Suche nach jemals am oberen Rand der Liste von NuGet-Priorität. Keines der geplanten Funktionen für NuGet handelt es sich um Kontextsuche, was bedeutet, dass NuGet Informationen über die Version und SKU von Visual Studio, die Sie verwenden und den Typ des Projekts, die Sie erstellen als Kriterium verwenden wird, um zu bestimmen die Relevanz der potenziellen Suche / / ergibt.

Mit NuGet 2.6 beginnen, wird jedes Mal, wenn ein Paket installiert ist, der Kontext für die Installation als Teil der Daten zur Installation der Vorgang aufgezeichnet.  Sucht senden auch die gleichen Kontextinformationen, die der NuGet Gallery zur Verbesserung der Suchergebnisse von Trends kontextabhängige Installation ermöglicht.  Einem zukünftigen Update von der NuGet Gallery wird die Verstärkung dieser kontextbezogene Relevanz aktiviert.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Nachverfolgen von Vs direkt installiert. Abhängigkeit installiert

Paketersteller sind Vertrauensstellungen der vertrauenden Seite mehr auf die [Paket Statistiken](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) auf der NuGet Gallery bereitgestellt.  Ein wichtige fehlende Daten zeigen, dass Autoren für gebeten haben ist eine Differenzierung zwischen direkter Paket installiert und Abhängigkeit installiert.  Bis jetzt der NuGet-Client nicht senden jeglichen Kontext, um den Installationsvorgang für gibt an, ob der Entwickler das Paket direkt installiert, oder wenn er installiert wurde, um eine Abhängigkeit zu erfüllen.
Starten mit NuGet 2.6, dass die Daten für den Installationsvorgang jetzt gesendet werden.  Paket Statistiken auf der NuGet Gallery werden diese Daten als separate Installation-Vorgänge verfügbar machen, mit einem "-Abhängigkeit" Suffix.

* Installieren
* Install-Abhängigkeit
* Update
* Update-Abhängigkeit
* Neuinstallation
* Neuinstallation Abhängigkeit

Neben dem Namen des anderen Vorgang wird das abhängige Paket-Id für die Installation auch aufgezeichnet.  Einem zukünftigen Update von der NuGet Gallery werden diese Daten in Berichten und ermöglichen so Paketersteller vollständig zu verstehen, wie Entwickler ihre Pakete installieren, verfügbar machen.

## <a name="bug-fixes"></a>Fehlerkorrekturen

NuGet-2.6 enthält auch verschiedene Fehlerbehebungen. Eine vollständige Liste der Arbeit Artikel feste in NuGet 2.6 Bitte Ansicht der [NuGet Issue Tracker für diese Version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).