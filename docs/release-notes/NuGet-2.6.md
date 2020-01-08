---
title: Anmerkungen zu dieser Version von nuget 2,6
description: Anmerkungen zu dieser Version von nuget 2.6.1 für webmatrix einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5e80965aad4caa69130be31a37b7f5f5ffb12ea6
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384123"
---
# <a name="nuget-26-release-notes"></a>Anmerkungen zu dieser Version von nuget 2,6

[Anmerkungen zu dieser Version von nuget 2,5](../release-notes/nuget-2.5.md) | [nuget-2.6.1 für webmatrix](../release-notes/nuget-2.6.1-for-webmatrix.md) -Versions Hinweise

Nuget 2,6 wurde am 26. Juni 2013 veröffentlicht.

## <a name="notable-features-in-the-release"></a>Wichtige Features in der Version

### <a name="support-for-visual-studio-2013"></a>Unterstützung für Visual Studio 2013

Nuget 2,6 ist die erste Version, die Unterstützung für Visual Studio 2013 bietet. Ebenso wie Visual Studio 2012 ist die nuget-Paket-Manager-Erweiterung in jeder Edition von Visual Studio enthalten.

Um die bestmögliche Unterstützung für Visual Studio 2013 bereitzustellen und gleichzeitig sowohl Visual Studio 2010 als auch Visual Studio 2012 zu unterstützen und die Erweiterungs Größen so klein wie möglich zu halten, erstellen wir eine separate Erweiterung für Visual Studio 2013, während der die ursprüngliche Erweiterung hat weiterhin sowohl Visual Studio 2010 als auch 2012 als Ziel.

Ab nuget 2,6 veröffentlichen wir zwei Erweiterungen wie folgt:

1. [Nuget-Paket-Manager](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (gilt für Visual Studio 2010 und 2012)
1. [Nuget-Paket-Manager für Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Mit dieser Aufteilung gelangen Sie auf die Schaltfläche "Installieren von nuget" der [nuget.org](https://nuget.org) -Startseite, auf der Sie die [nuget](../install-nuget-client-tools.md) -Seite installieren, auf der Sie weitere Informationen zum Installieren der verschiedenen nuget-Clients finden.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Xdt Web. config-Transformations Unterstützung

Eines der hochgradig angeforderten Features für den nuget-Client war die Unterstützung leistungsfähigerer XML-Transformationen mithilfe der xdt-Transformations-Engine, die in Visual Studio-buildkonfigurationstransformationen verwendet wird.

Im April 2013 haben wir zwei große Ankündigungen bezüglich der nuget-Unterstützung für xdt vorgenommen. Der erste bestand darin, dass die xdt-Bibliothek selbst [als nuget-Paket freigegeben](https://nuget.org/packages/Microsoft.Web.Xdt) und [auf CodePlex frei](http://xdt.codeplex.com/)gegeben wurde. Dieser Schritt ermöglichte die Verwendung der xdt-Engine durch andere Open Source-Software, einschließlich des nuget-Clients, frei. Die zweite Ankündigung war der Plan, die Verwendung der xdt-Engine für Transformationen im nuget-Client zu unterstützen. Nuget 2,6 umfasst diese Integration.

#### <a name="how-it-works"></a>So funktioniert's

Um die xdt-Unterstützung von nuget nutzen zu können, ähneln die Mechanismen der [aktuellen config-Transformations Funktion](../create-packages/source-and-config-file-transformations.md).
Transformations Dateien werden dem Inhalts Ordner des Pakets hinzugefügt. Während Konfigurations Transformationen jedoch eine einzelne Datei sowohl für die Installation als auch für die Installation verwenden, ermöglichen xdt-Transformationen eine differenzierte Steuerung dieser beiden Prozesse mithilfe der folgenden Dateien:

- "Web. config. install. xdt"
- Web. config. Uninstall. xdt

Darüber hinaus verwendet nuget das Datei Suffix, um zu bestimmen, welche Engine für Transformationen ausgeführt werden soll, sodass Pakete, die die vorhandenen Web. config. Transformationen verwenden, weiterhin funktionieren. Xdt-Transformationen können auch auf alle XML-Dateien (nicht nur "Web. config") angewendet werden, sodass Sie dies für andere Anwendungen in Ihrem Projekt nutzen können.

#### <a name="what-you-can-do-with-xdt"></a>Was Sie mit xdt tun können

Eine der größten Stärken von xdt ist eine [einfache, aber leistungsfähige Syntax](https://docs.microsoft.com/previous-versions/aspnet/dd465326(v=vs.110)) zum Bearbeiten der Struktur eines XML-DOM. Anstatt eine Fixed-Dokumentstruktur einfach auf eine andere Struktur zu überlagern, bietet xdt Steuerelemente für übereinstimmende Elemente auf verschiedene Weise, von einem einfachen Attributnamen, der mit der vollständigen XPath-Unterstützung übereinstimmt. Sobald ein entsprechendes Element oder eine Reihe von Elementen gefunden wird, stellt xdt einen umfangreichen Satz von Funktionen zum Bearbeiten der Elemente bereit, d. h. ob das Hinzufügen, aktualisieren oder Entfernen von Attributen, das Platzieren eines neuen Elements an einem bestimmten Speicherort oder das ersetzen oder Entfernen des gesamten -Element und seine untergeordneten Elemente.

### <a name="machine-wide-configuration"></a>Computer weite Konfiguration

Eine der großen Vorteile von nuget besteht darin, dass eine anderweitig große ausführbare Datei oder Bibliothek in einen Satz von modularen Komponenten aufgeteilt wird, der integriert werden kann und die wichtigsten Komponenten unabhängig verwaltet und versioniert werden. Ein Nebeneffekt hiervon ist jedoch, dass die konventionelle Idee eines Produkts oder einer Produktfamilie potenziell fragmentierter wird.
Das benutzerdefinierte Paket Quell Feature von nuget bietet eine Möglichkeit zum Organisieren von Paketen. benutzerdefinierte Paketquellen können jedoch nicht selbst erkannt werden.

Nuget 2,6 erweitert die Logik für die Konfiguration von nuget durch Durchsuchen der Ordnerhierarchie unter dem Pfad% Program Data%/NuGet/config. Produkt Installationsprogramme können benutzerdefinierte nuget-Konfigurationsdateien unter diesem Ordner hinzufügen, um eine benutzerdefinierte Paketquelle für Ihre Produkte zu registrieren. Außerdem unterstützt die Ordnerstruktur die Semantik für Produkt, Version und sogar SKU der IDE. Die Einstellungen dieser Verzeichnisse werden in der folgenden Reihenfolge mit der Rang folgen Strategie "Last in WINS" angewendet.

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\nuget\config\{IDE}\*. config
3. %ProgramData%\nuget\config\{IDE}\{Version}\*. config
4. %ProgramData%\nuget\config\{IDE}\{Version}\{SKU}\*. config

In dieser Liste ist der {IDE}-Platzhalter für die IDE spezifisch, in der nuget ausgeführt wird. im Fall von Visual Studio lautet der Platzhalter "VisualStudio". Die Platzhalter "{Version}" und "{SKU}" werden von der IDE bereitgestellt (z. b. "11,0" und "wdexpress", "VWDExpress" und "pro"). Der Ordner kann dann viele verschiedene *. config-Dateien enthalten.
Daher kann das Unternehmen der Acme-Komponente als Teil des Produkt Installers eine benutzerdefinierte Paketquelle hinzufügen, die nur in den Professional-und Ultimate-Versionen von Visual Studio 2012 sichtbar ist, indem der folgende Dateipfad erstellt wird:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Obwohl die Ordnerstruktur es Programmen wie Software Installationsprogrammen ermöglicht, Computer weite Paketquellen zur nuget-Konfiguration hinzuzufügen, wurde auch das nuget-Konfigurations Dialogfeld aktualisiert, um die Registrierung von Paketquellen entweder als Benutzer spezifisch (z. b. registriert in% APPDATA%/NuGet/NuGet.config) oder Computer weit zuzulassen.

Diese Funktion wird von Visual Studio 2013 verwendet, bei dem eine Datei installiert wird:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

In dieser Datei wird eine neue Paketquelle namens ".NET Framework Packages" konfiguriert.

![Computer weite Einstellungen für nuget-Konfigurationsdatei](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Contextualisieren der Suche

Da die Anzahl der Pakete, die vom nuget-Katalog bedient werden, immer weiter zunimmt, bleibt die Verbesserungen bei der Suche immer am Anfang der nuget-Prioritäts Liste. Eines der geplanten Features für nuget ist die Kontextsuche. Dies bedeutet, dass nuget Informationen über die von Ihnen verwendete Version und SKU von Visual Studio und den Projekttyp, den Sie als Kriterium zum Ermitteln der Relevanz der potenziellen Suche erstellt haben, verwendet. Folgen.

Ab nuget 2,6 wird bei jeder Installation eines Pakets der Kontext für die Installation als Teil der Installationsvorgangs Daten aufgezeichnet.  Bei der Suche werden auch die gleichen Kontextinformationen gesendet, die es dem nuget-Katalog ermöglichen, Suchergebnisse nach kontextbezogenen Installations Trends zu steigern.  Bei einem zukünftigen Update für den nuget-Katalog wird diese kontextabhängige Erhöhung der Relevanz ermöglicht.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Nachverfolgung von direkten Installationen im Vergleich zu Abhängigkeiten der Abhängigkeit

Paket Autoren verlassen sich mehr und mehr auf die [Paket Statistiken](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) , die im nuget-Katalog bereitgestellt werden.  Ein wichtiger fehlender Datenpunkt, den die Autoren angefordert haben, ist eine Unterscheidung zwischen direkten Paketinstallationen und der Installation von Abhängigkeiten.  Bis jetzt hat der nuget-Client keinen Kontext um den Installationsvorgang gesendet, um zu erfahren, ob der Entwickler das Paket direkt installiert hat oder ob es installiert wurde, um eine Abhängigkeit zu erfüllen.
Ab nuget 2,6 werden diese Daten für den Installationsvorgang gesendet.  Paket Statistiken für den nuget-Katalog machen diese Daten als separate Installations Vorgänge mit dem Suffix "-Abhängigkeiten" verfügbar.

* Installieren von
* Installation-Abhängigkeit
* Aktualisierung
* Update-Abhängigkeit
* Neuinstallation
* Neuinstallation-Abhängigkeit

Neben dem Namen des unterschiedlichen Vorgangs wird auch die abhängige Paket-ID für die Installation aufgezeichnet.  In einem zukünftigen Update für den nuget-Katalog werden diese Daten in Berichten verfügbar gemacht, sodass Paket Autoren vollständig verstehen können, wie Entwickler ihre Pakete installieren.

## <a name="bug-fixes"></a>Fehlerkorrekturen

Nuget 2,6 umfasst auch mehrere Fehlerbehebungen. Eine vollständige Liste der Arbeitselemente, die in nuget 2,6 behoben wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).