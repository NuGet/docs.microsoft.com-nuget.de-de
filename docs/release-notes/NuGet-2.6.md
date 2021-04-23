---
title: Versionshinweise zu NuGet 2.6
description: Versionshinweise zu NuGet 2.6, einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6b25b9df062afc88466ad107e718f632878debfc
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901420"
---
# <a name="nuget-26-release-notes"></a>Versionshinweise zu NuGet 2.6

[Anmerkungen zu NuGet 2.5](../release-notes/nuget-2.5.md)  |  [Versionshinweise zu NuGet 2.6.1 für WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 wurde am 26. Juni 2013 veröffentlicht.

## <a name="notable-features-in-the-release"></a>Wichtige Features in der Version

### <a name="support-for-visual-studio-2013"></a>Unterstützung für Visual Studio 2013

NuGet 2.6 ist das erste Release, das Unterstützung für Visual Studio 2013. Und wie Visual Studio 2012 ist die NuGet-Paket-Manager-Erweiterung in jeder Edition von Visual Studio.

Um die bestmögliche Unterstützung für Visual Studio 2013 zu bieten und gleichzeitig sowohl Visual Studio 2010 als auch Visual Studio 2012 zu unterstützen und die Erweiterungsgrößen so klein wie möglich zu halten, erstellen wir eine separate Erweiterung für Visual Studio 2013, während die ursprüngliche Erweiterung weiterhin sowohl Visual Studio 2010 als auch 2012 als Ziel hat.

Ab NuGet 2.6 werden wir zwei Erweiterungen wie folgt veröffentlichen:

1. [NuGet Paket-Manager](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (gilt für Visual Studio 2010 und 2012)
1. [NuGet-Paket-Manager für Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Mit dieser Aufteilung werden Sie über [die](https://nuget.org) Schaltfläche "NuGet installieren" der nuget.org-Startseite zur Seite zum Installieren von [NuGet](../install-nuget-client-tools.md) weiterbewegt, auf der Sie weitere Informationen zum Installieren der verschiedenen NuGet-Clients finden.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Unterstützung für XDTWeb.config Transformation

Eines der am häufigsten angeforderten Features für den NuGet-Client war die Unterstützung leistungsfähigerer XML-Transformationen mithilfe der XDT-Transformations-Engine, die in Visual Studio Buildkonfigurationstransformationen verwendet wird.

Im April 2013 haben wir zwei große Ankündigungen zur NuGet-Unterstützung für XDT gemacht. Die erste war, dass die XDT-Bibliothek selbst als [NuGet-Paket](https://nuget.org/packages/Microsoft.Web.Xdt) veröffentlicht und auf [CodePlex als Open](http://xdt.codeplex.com/)Source veröffentlicht wurde. Dieser Schritt ermöglichte die freie Verwendung der XDT-Engine durch andere Open-Source-Software, einschließlich des NuGet-Clients. Die zweite Ankündigung war der Plan, die Verwendung der XDT-Engine für Transformationen im NuGet-Client zu unterstützen. NuGet 2.6 enthält diese Integration.

#### <a name="how-it-works"></a>Funktionsweise

Um die XDT-Unterstützung von NuGet zu nutzen, sehen die Mechanismen ähnlich wie die des [aktuellen Konfigurationstransformationsfeatures](../create-packages/source-and-config-file-transformations.md)aus.
Transformationsdateien werden dem Inhaltsordner des Pakets hinzugefügt. Während Konfigurationstransformationen eine einzelne Datei sowohl für die Installation als auch für die Deinstallation verwenden, ermöglichen XDT-Transformationen eine differenzierte Steuerung beider Prozesse mithilfe der folgenden Dateien:

- Web.config.install.xdt
- Web.config.uninstall.xdt

Darüber hinaus verwendet NuGet das Dateisuffix, um zu bestimmen, welche Engine für Transformationen ausgeführt werden soll, sodass Pakete, die die vorhandene web.config.transforms verwenden, weiterhin funktionieren. XDT-Transformationen können auch auf jede XML-Datei (nicht nur web.config) angewendet werden, sodass Sie dies für andere Anwendungen in Ihrem Projekt nutzen können.

#### <a name="what-you-can-do-with-xdt"></a>Möglichkeiten von XDT

Eine der größten Stärken von XDT ist die [einfache, aber leistungsstarke Syntax](/previous-versions/aspnet/dd465326(v=vs.110)) zum Bearbeiten der Struktur eines XML-DOM. Anstatt einfach eine feste Dokumentstruktur auf eine andere Struktur zu überlagern, bietet XDT Steuerelemente für den Abgleich von Elementen auf verschiedene Weise, von einfachem Attributnamenabgleich bis hin zur vollständigen XPath-Unterstützung. Sobald ein übereinstimmendes Element oder eine Gruppe von Elementen gefunden wurde, stellt XDT einen umfangreichen Satz von Funktionen zum Bearbeiten der Elemente bereit. Dabei spielt es keine Rolle, ob dies das Hinzufügen, Aktualisieren oder Entfernen von Attributen, das Platzieren eines neuen Elements an einer bestimmten Position oder das Ersetzen oder Entfernen des gesamten Elements und seiner untergeordneten Elemente bedeutet.

### <a name="machine-wide-configuration"></a>Machine-Wide-Konfiguration

Eine der großen Stärken von NuGet besteht darin, dass es eine ansonsten große ausführbare Datei oder Bibliothek in eine Reihe modularer Komponenten aufteilt, die integriert und vor allem unabhängig verwaltet und versioniert werden können. Ein Nebeneffekt davon ist jedoch, dass die herkömmliche Idee eines Produkts oder einer Produktfamilie potenziell fragmentierter wird.
Die Benutzerdefinierte Paketquellfunktion von NuGet bietet eine Möglichkeit zum Organisieren von Paketen. benutzerdefinierte Paketquellen können jedoch nicht allein ermittelt werden.

NuGet 2.6 erweitert die Logik zum Konfigurieren von NuGet durch Durchsuchen der Ordnerhierarchie unter dem Pfad %ProgramData%/NuGet/Config. Produktinstaller können benutzerdefinierte NuGet-Konfigurationsdateien unter diesem Ordner hinzufügen, um eine benutzerdefinierte Paketquelle für ihre Produkte zu registrieren. Darüber hinaus unterstützt die Ordnerstruktur Semantik für Produkt, Version und sogar SKU der IDE. Einstellungen aus diesen Verzeichnissen werden in der folgenden Reihenfolge mit der Rangfolgestrategie "Letzter in gewinnt" angewendet.

1. %ProgramData%\NuGet\Config \* .config
2. %ProgramData%\NuGet\Config \{ IDE} \* .config
3. %ProgramData%\NuGet\Config \{ IDE} \{ Version} \* .config
4. %ProgramData%\NuGet\Config \{ IDE} \{ Version} \{ SKU} \* .config

In dieser Liste ist der Platzhalter {IDE} spezifisch für die IDE, in der NuGet ausgeführt wird. Im Fall von Visual Studio ist er also "VisualStudio". Die Platzhalter {Version} und {SKU} werden von der IDE bereitgestellt (z.B. "11.0" bzw. "WDExpress", "VWDExpress" bzw. "Pro"). Der Ordner kann dann viele verschiedene *.config-Dateien enthalten.
Daher kann das ACME-Komponentenunternehmen im Rahmen des Produktinstallationsprogramms eine benutzerdefinierte Paketquelle hinzufügen, die nur in den Professional- und Ultimate-Versionen von Visual Studio 2012 sichtbar ist, indem der folgende Dateipfad erstellt wird:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Während die Ordnerstruktur es Programmen wie Softwareinstallern einfach macht, der NuGet-Konfiguration computerweite Paketquellen hinzuzufügen, wurde auch das NuGet-Konfigurationsdialogfeld aktualisiert, um die Registrierung von Paketquellen entweder als benutzerspezifisch (z. B. registriert in %AppData%/NuGet/NuGet.Config) oder computerweit zu ermöglichen.

Dieses Feature wird von Visual Studio 2013 verwendet, in dem eine Datei unter installiert wird:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

In dieser Datei wird eine neue Paketquelle mit dem Namen ".NET Framework Packages" konfiguriert.

![Computerweite Einstellungen der NuGet-Konfigurationsdatei](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Kontextualisieren der Suche

Da die Anzahl der pakete, die vom NuGet-Katalog bedient werden, mit exponentiellem Tempo weiter zunimmt, bleibt die Verbesserung der Suche immer ganz oben in der NuGet-Prioritätsliste. Eines der geplanten Features für NuGet ist die kontextbezogene Suche, d. h., NuGet verwendet Informationen zur Version und SKU von Visual Studio, die Sie verwenden, und den Typ des Projekts, das Sie als Kriterien zum Bestimmen der Relevanz potenzieller Suchergebnisse erstellen.

Ab NuGet 2.6 wird bei jeder Installation eines Pakets der Kontext für die Installation als Teil der Installationsvorgangsdaten aufgezeichnet.  Suchvorgänge senden auch die gleichen Kontextinformationen, sodass der NuGet-Katalog Suchergebnisse durch kontextbezogene Installationstrends verstärken kann.  Ein zukünftiges Update des NuGet-Katalogs ermöglicht diese kontextbezogene Relevanzverstärkung.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Nachverfolgen von direkten Installationen im Vergleich zu Abhängigkeitsinstallationen

Paketautoren verlassen sich immer mehr auf die [Paketstatistiken,](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) die im NuGet-Katalog bereitgestellt werden.  Ein wichtiger fehlender Datenpunkt, den Autoren angefordert haben, ist eine Unterscheidung zwischen direkten Paketinstallationen und Abhängigkeitsinstallationen.  Bisher hat der NuGet-Client keinen Kontext für den Installationsvorgang gesendet, um zu ermitteln, ob der Entwickler das Paket direkt installiert hat oder ob es installiert wurde, um eine Abhängigkeit zu erfüllen.
Ab NuGet 2.6 werden diese Daten nun für den Installationsvorgang gesendet.  Paketstatistiken im NuGet-Katalog machen diese Daten als separate Installationsvorgänge mit dem Suffix "-Dependency" verfügbar.

* Installieren
* Install-Dependency
* Aktualisieren
* Update-Dependency
* Neuinstallation
* Reinstall-Dependency

Zusätzlich zum anderen Vorgangsnamen wird auch die ID des abhängigen Pakets für die Installation aufgezeichnet.  Ein zukünftiges Update des NuGet-Katalogs macht diese Daten in Berichten verfügbar, sodass Paketautoren vollständig verstehen können, wie Entwickler ihre Pakete installieren.

## <a name="bug-fixes"></a>Fehlerbehebungen

NuGet 2.6 enthält auch mehrere Fehlerbehebungen. Eine vollständige Liste der in NuGet 2.6 behobenen Arbeitselemente finden Sie in der [NuGet-Problemverfolgung für dieses Release.](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)