---
title: Was ist NuGet, und welche Funktion hat es? | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/26/2017
ms.topic: hero-article
ms.prod: nuget
ms.technology: 
ms.assetid: c3faf278-4cbf-4733-96f6-9ee9f7203af9
description: "Eine umfassende Einführung in NuGet und seine Funktionsweise"
keywords: NuGet-Paket-Manager, Nutzung, Paketerstellung, Pakethosting
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2bc6a9e154df287fee6a7e00cc1349dfa2100643
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/05/2018
---
# <a name="an-introduction-to-nuget"></a>Eine Einführung in NuGet

Ein unverzichtbares Tool für jede moderne Entwicklungsplattform ist ein Mechanismus, durch den Entwickler nützlichen Code erstellen, freigeben und verwenden können. Solch ein Code wird oft in „Paketen“ gebündelt, in denen kompilierter Code (z.B. DLLs) zusammen mit anderem Inhalt enthalten ist, der in Projekten benötigt wird, die diese Pakete nutzen.

Für .NET ist der Mechanismus zur Freigabe von Code **NuGet**, das definiert, wie Pakete für .NET erstellt, gehostet und verarbeitet werden, und es stellt die Tools für jede dieser Aktionen bereit. 

Einfach gesagt: ein NuGet-Paket ist eine einzelne ZIP-Datei mit der Erweiterung `.nupkg`, die kompilierten Code (DLLs), andere Dateien im Zusammenhang mit diesem Code und ein beschreibendes Manifest enthält, in dem Informationen wie die Versionsnummer des Pakets enthalten sind. Entwickler von Bibliotheken erstellen Paketdateien und veröffentlichen sie auf einem Host. Paketanwender erhalten diese Pakete, fügen diese zu ihren Projekten hinzu und rufen dann diese Bibliothekfunktion in ihrem Projektcode auf. NuGet selbst verarbeitet dann alle Zwischendetails.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Der Paketfluss zwischen Erstellern, Hosts und Benutzer

In seiner Rolle als Host verwaltet NuGet selbst das zentrale Repository von über 60.000 eindeutigen, öffentlich verfügbaren Paketen auf [nuget.org](https://www.nuget.org). Diese Pakete werden täglich von Millionen von .NET-Entwicklern verwendet. Mit NuGet können Sie auch Pakete privat in der Cloud, in einem privaten Netzwerk oder sogar nur auf Ihrem lokalen Dateisystem hosten. Auf diese Weise werden diese Pakete nur diesen Entwicklern innerhalb einer bestimmten Organisation oder Gruppe von Kunden zur Verfügung gestellt. Die Optionen werden in [Hosting your own NuGet feeds (Hosten Ihrer eigenen NuGet-Feeds)](Hosting-Packages/Overview.md) erläutert.

Ein beliebiger Host dient als Verbindungspunkt zwischen *Paketerstellern* und *Paketbenutzer*. Ersteller erstellen nützliche NuGet-Pakete und veröffentlichen Sie auf einem Host. Benutzer suchen dann nach nützlichen und kompatiblen Paketen auf zugänglichen Hosts, laden diese Pakete herunter und schließen sie in Ihre Projekte ein. Nach der Installation in einem Projekt sind die Paket-APIs für den restlichen Projektcode verfügbar.

![Beziehung zwischen Paketerstellern, Pakethosts und Paketbenutzer](media/nuget-roles.png)

Ein „kompatibles“ Paket bedeutet in diesem Fall, dass es Assemblys enthält, die für mindestens ein .NET Zielframework erstellt wurden, das mit dem Zielframework des nutzenden Projekts kompatibel ist. Um ein Paket weitgehend kompatibel zu machen, kompiliert der Ersteller separate Assemblys für verschiedene Zielframeworks und schließt sie alle im selben Paket ein. Wenn ein Benutzer dieses Paket installiert, extrahiert NuGet nur jene Assemblys, die vom Projekt benötigt werden. Dadurch wird der Speicherbedarf des Pakets in der fertigen Anwendung bzw. in den vom Projekt erzeugten Assemblys gesenkt.

## <a name="nuget-tools"></a>NuGet-Tools

Zusätzlich zur Unterstützung für das Hosting bietet NuGet außerdem eine Vielzahl von Tools, die vom Ersteller und Benutzer verwendet werden:

| Tool | Plattformen | Anwendbare Szenarios | description |
| --- | --- | --- | --- |
| [nuget.exe-CLI](Tools/nuget-exe-CLI-Reference.md) | Alle | Erstellung, Verbrauch | Bietet alle NuGet-Funktionen, mit einigen Befehlen, die speziell für Paketersteller bestimmt sind, anderen Befehlen, die nur für Benutzer, und wieder anderen, die für beide bestimmt sind. Beispielsweise verwenden Paketersteller den `nuget pack`-Befehl zum Erstellen eines Pakets aus verschiedenen Assemblys und zugehörigen Dateien, Paketbenutzer verwenden `nuget install`, um Pakete in ein Projekt einzubinden, und alle verwenden `nuget config`, um NuGet-Konfigurationsvariablen festzulegen.  |
| [Benutzeroberfläche des Paket-Managers](Tools/Package-Manager-UI.md) | Visual Studio unter Windows | Verbrauch | Stellt eine einfach zu bedienende Benutzeroberfläche zum Installieren und Verwalten von Paketen in .NET-Projekten bereit. | 
| [Manage NuGet UI (Verwalten der NuGet-Benutzeroberfläche)](/visualstudio/mac/nuget-walkthrough) | Visual Studio für Mac | Verbrauch | Stellt eine einfach zu bedienende Benutzeroberfläche zum Installieren und Verwalten von Paketen in .NET-Projekten bereit. |
| [Paket-Manager-Konsole](Tools/Package-Manager-Console.md) | Visual Studio unter Windows | Verbrauch | Stellt [PowerShell-Befehle](Tools/Powershell-Reference.md) zum Installieren und Verwalten von Paketen in .NET-Projekten bereit. | 
| [dotnet-CLI](Tools/dotnet-Commands.md) | Alle | Erstellung, Verbrauch | Stellt bestimmte NuGet-CLI-Funktionen direkt in der .NET Core-Toolkette bereit. |
| [MSBuild](Schema/msbuild-targets.md) | Windows | Erstellung, Verbrauch | Bietet die Möglichkeit zum Erstellen von Paketen und Wiederherstellen von Paketen, die in einem Projekt direkt über die MSBuild-Toolkette verwendet werden. |

Wie Sie sehen können, sind die Tools, mit denen Sie mit NuGet arbeiten, stark davon abhängig, ob Sie Pakete erstellen (und veröffentlichen) oder diese nutzen, und von der Plattform, mit der Sie arbeiten. Ausführlichere Informationen finden Sie unter [Package creation workflow (Paketerstellungsworkflow)](Create-Packages/Overview-and-Workflow.md) und [Package consumption workflow (Paketverbrauchsworkflow)](Consume-Packages/Overview-and-Workflow.md) zusammen mit anderen Themen in diesen Abschnitten. 

Paketersteller sind in der Regel auch Benutzer, da sie auf Funktionalität aufbauen, die in anderen NuGet-Paketen vorhanden ist. Und diese Pakete können natürlich wiederum von anderen abhängen.

## <a name="managing-dependencies"></a>Verwalten von Abhängigkeiten

Die Fähigkeit, auf der Arbeit anderer einfach aufzubauen, ist ein Faktor, der ein Paketverwaltungssystem so leistungsfähig machen. Entsprechend ist eine der wichtigsten Aufgaben von NuGet das Verwalten dieser Abhängigkeitsstruktur oder dieses „Diagramms“ für ihr Projekt. Einfach ausgedrückt müssen Sie sich nur mit jenen Paketen selbst befassen, die Sie direkt in einem Projekt verwenden. Wenn irgendeines dieser Pakete selbst andere Pakete verwendet (die Pakete verwenden können), übernimmt NuGet alle diese früheren Abhängigkeiten.

Die folgende Abbildung zeigt ein Projekt, das von fünf Paketen abhängig ist, die wiederum von einer Reihe anderer abhängen.  

![Ein Beispiel für ein NuGet-Abhängigkeitsdiagramm für ein .NET-Projekt](media/dependency-graph.png)

Beachten Sie, dass einige Pakete mehrmals im Abhängigkeitsdiagramm angezeigt werden. Beispielsweise gibt es drei verschiedene Benutzer des Pakets B, und jeder Benutzer könnte auch eine andere Version für das Paket (nicht gezeigt) angeben. Da dies häufig auftritt, übernimmt NuGet alle schwierigen Aufgaben, um genau zu bestimmen, welche Version des Pakets B all seine Benutzer zufriedenstellt. NuGet führt dies dann für alle anderen Pakete durch, unabhängig davon, wie ausführlich das Abhängigkeitsdiagramm wird.

Weitere Details wie NuGet diesen Dienst ausführt finden Sie unter [Dependency resolution (Abhängigkeitsauflösung)](Consume-Packages/Dependency-Resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Nachverfolgungsverweise und Wiederherstellen von Paketen

Da Projekte zwischen Entwicklercomputern, Quellcodeverwaltungsrepositorys, Buildservern usw. problemlos verschoben werden können, ist es höchst unpraktisch, dass binäre Assemblys von NuGet-Paketen direkt an ein Projekt gebunden bleiben. Nicht nur würde dies jede Kopie des Projekts unnötigerweise vergrößern (und somit Speicherplatz in Quellcodeverwaltungsrepositorys verschwenden), es würde auch das Aktualisieren von Paketbinärdateien auf neuere Versionen sehr erschweren, da dies in allen Kopien im gesamten Projekt erfolgen müsste. 

Stattdessen verwaltet NuGet einfach eine Liste der Pakete, von denen ein Projekt abhängt (einschließlich der beiden Abhängigkeiten auf der obersten und der untersten Ebene), und bietet die Möglichkeiten, alle referenzierten Pakete auf Anfrage wiederherzustellen, wie in [Package restore (Paketwiederherstellung)](Consume-Packages/Package-Restore.md) beschrieben. D.h. wenn Sie ein Paket in ein Projekt von einem Host aus installieren, zeichnet NuGet die Paket-ID und Versionsnummer in dieser Verweisliste auf. (Wenn ein Paket deinstalliert wird, wird dieses natürlich aus der Liste entfernt.) 

![Eine NuGet-Verweisliste wird bei Paketinstallation erstellt und kann zum Wiederherstellen von Paketen an einem anderen Ort verwendet werden.](media/nuget-restore.png)

Mit der Verweisliste kann NuGet anschließend alle Pakete von öffentlichen und/oder privaten Hosts zu einem späteren Zeitpunkt neu installieren, also wiederherstellen. (Aus diesem Grund lässt nuget.org kein permanentes Löschen von veröffentlichten Paketen zu, auch wenn sie ausgeblendet werden können. Nähere Angaben finden Sie unter [Löschen von Paketen](Policies/deleting-packages.md).) Wenn Sie ein Projekt auf die Quellcodeverwaltung committen oder auf andere Weise freigeben, muss nur die Verweisliste enthalten sein und keine Paketbinärdateien eingeschlossen werden (Näheres finden Sie unter [Pakete und Quellcodeverwaltung](Consume-Packages/Packages-and-Source-Control.md).)

Der Computer, der ein Projekt, z.B. einen Buildserver, erhält, der eine Kopie des Projekts als Teil eines automatisierten Bereitstellungssystems empfängt, fordert NuGet einfach auf, Abhängigkeiten wiederherzustellen, wenn sie benötigt werden. Buildsysteme, wie Visual Studio Team Services, stellen „NuGet restore“-Schritte für exakt diesen Zweck bereit. Auf ähnliche Weise, wenn Entwickler eine Kopie eines Projekts erhalten (wie beim Klonen eines Repositorys) und dann das Projekt in Visual Studio öffnen und einen Build ausführen. stellt Visual Studio automatisch die nötigen NuGet-Pakete wieder her. Entwickler können NuGet mit dem `nuget restore`-CLI-Befehl oder dem `Install-Package`-Cmdlet in der Paket-Manager-Konsole anweisen, Pakete zu einem beliebigen Zeitpunkt wiederherzustellen.

Die primäre Rolle von NuGet bei Entwicklern liegt dann klar im Verwalten der Verweisliste für Ihr Projekt und im Bereitstellen der Möglichkeiten, um diese referenzierten Pakete effizient wiederherzustellen (und zu aktualisieren).

Die Art und Weise, wie dies genau erfolgt, hat sich über die verschiedenen Versionen von NuGet weiterentwickelt, wodurch mehrere sogenannte *Paketverwaltungsformate* entstanden sind:

- [`packages.config`](Schema/packages-config.md): *(NuGet 1.0+)* Eine XML-Datei, die eine flache Liste aller Abhängigkeiten im Projekt, einschließlich der Abhängigkeiten von anderen installierten Paketen, verwaltet. 
- [`project.json`](Schema/project-json.md): *(NuGet 3.0+)* Eine JSON-Datei, die eine Liste der Projektabhängigkeiten mit einem allgemeinen Paketdiagramm in einer verknüpften Datei `project.lock.json` verwaltet. Diese Struktur bietet eine verbesserte Leistung gegenüber `packages.config` wie in [Abhängigkeitsauflösung](Consume-Packages/Dependency-Resolution.md) beschrieben, einschließlich transitiver Wiederherstellung, wurde aber in der Regel selbst durch „PackageReference“ unten ersetzt.
- [Packen von Verweisen in Projektdateien](Consume-Packages/Package-References-in-Project-Files.md) (auch bekannt als „PackageReference“) | *(NuGet 4.0+)* verwaltet eine Liste der Abhängigkeiten der obersten Ebene eines Projekts direkt in der Projektdatei, damit keine separate Datei benötigt wird. Eine zugeordnete Datei `project.assets.json` wird dynamisch generiert wie z.B. `project.lock.json`, um das gesamte Abhängigkeitsdiagramm zu verwalten.

Welches Paketverwaltungsformat in einen Projekt verwendet wird, hängt vom Projekttyp und der verfügbaren Version von NuGet und Visual Studio ab. Um zu überprüfen, welches Format verwendet wird, suchen Sie `packages.config` oder `project.json` im Projektstamm nach der Installation des ersten Pakets. Wenn keine der Dateien angezeigt wird, suchen Sie direkt in der Projektdatei nach einem &lt;PackageReference&gt;-Element.

In Visual Studio 2017 beispielsweise verwenden die meisten Projekttypen `packages.config`, mit Ausnahme von UWP C# und .NET Core-Projekten, die „PackageReference“ verwenden. 

## <a name="what-else-does-nuget-do"></a>Was macht NuGet außerdem?

Bisher haben Sie gelernt, dass NuGet (in seiner Hostingrolle) das zentrale nuget.org-Repository bereitstellt und privates Hosting unterstützt. NuGet stellt die Tools zur Verfügung, die Entwickler benötigen, um Pakete zu erstellen, zu veröffentlichen und zu nutzen. Und, was besonders wichtig ist, NuGet verwaltet eine Verweisliste der Pakete, die in einem Projekt verwendet werden und verfügt über die Möglichkeit zum Wiederherstellen und Aktualisieren dieser Pakete aus dieser Liste.

Damit diese Prozesse effizient arbeiten, führt NuGet einige Optimierungen im Hintergrund durch. Insbesondere verwaltet NuGet sowohl computerweite als auch projektspezifische Paketcaches, um die Installation und die Neuinstallation abzukürzen. Was die computerweiten Caches angeht, sind alle Pakete, die Sie in einem Projekt herunterladen und installieren, im Cache gespeichert, sodass für das Installieren des gleichen Pakets in einem anderen Projekt kein erneuter Download notwendig ist. Dies ist eindeutig sehr hilfreich, wenn Sie häufig eine größere Anzahl von Paketen wiederherstellen wie auf einem Buildserver. Weitere Details zum Mechanismus und dessen Funktionsweise finden Sie unter [Verwalten des NuGet-Caches](Consume-Packages/Managing-the-Nuget-Cache.md).

Innerhalb eines einzelnen Projekts leistet NuGet viel Arbeit, um das gesamte Abhängigkeitsdiagramm zu verwalten. (Bei Verwendung von `project.json` oder &lt;PackageReference&gt; speichert NuGet die Informationen in einer sekundären Datei namens `project.lock.json` bzw. `project.assets.json`.) Dies schließt das Auflösen von mehreren Verweisen auf verschiedene Versionen desselben Pakets ein.

Das bedeutet, dass es ist üblich ist, dass ein Projekt eine Abhängigkeit von ein oder mehreren Paketen annimmt, die über die gleichen Abhängigkeiten verfügen. Beispielsweise werden einige der nützlichsten Hilfsprogrammpakete auf nuget.org von vielen anderen Paketen verwendet. Im gesamten Abhängigkeitsdiagramm, 10, können sehr leicht zehn unterschiedliche Verweise auf verschiedene Versionen desselben Pakets vorkommen. Sie sollten jedoch nicht mehrere Versionen des Pakets in der Anwendung selbst platzieren, deshalb findet NuGet die Version, die alle verwenden können. (Siehe [Abhängigkeitsauflösung](Consume-Packages/Dependency-Resolution.md) für weitere Informationen zu diesem Thema.)

Darüber hinaus behält NuGet alle Spezifikationen im Zusammenhang mit der Struktur von Paketen (einschließlich [Lokalisierung](Create-Packages/Creating-Localized-Packages.md) und [Debugsymbole](Create-Packages/Symbol-Packages.md)) und wie auf sie verwiesen wird (einschließlich [Versionsbereiche](reference/package-versioning.md#version-ranges-and-wildcards) und [Vorabversionen](create-packages/Prerelease-Packages.md).) NuGet stellt auch APIs für Anmeldeinformationsanbieter (für den Zugriff auf private Hosts) sowie für Entwickler, die Visual Studio-Erweiterungen und -Projektvorlagen schreiben, zur Verfügung.

Nehmen Sie sich kurz Zeit, das Inhaltsverzeichnis nach dieser Dokumentation zu durchsuchen, und finden Sie alle diese Funktionen hier dargestellt, zusammen mit Versionshinweisen, die auf die Anfänge von NuGet zurückgehen.

## <a name="comments-contributions-and-issues"></a>Kommentare, Beiträge und Probleme

Abschließend freuen wir uns sehr auf viele Kommentare und Beiträge zu dieser Dokumentation. Wählen Sie einfach die Befehle **Kommentare** und **Bearbeiten** auf einer beliebigen Seite, oder besuchen Sie das [Dokumentationsrepository ](https://github.com/NuGet/docs.microsoft.com-nuget/) und die [Dokumentationsproblemliste](https://github.com/NuGet/docs.microsoft.com-nuget/issues) auf GitHub.

Wir freuen uns auch über Beiträge zu NuGet selbst über seine [verschiedenen GitHub-Repositorys](https://github.com/NuGet/Home). NuGet-Probleme finden Sie auf [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues).

Viel Vergnügen mit NuGet!
