---
title: Was ist NuGet, und welche Funktion hat es?
description: Eine umfassende Einführung in NuGet und seine Funktionsweise
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: overview
ms.openlocfilehash: f16cc6f66bc12727a4ec8eb5da4ff44a9eeb1764
ms.sourcegitcommit: ba8ad1bd13a4bba3df94374e34e20c425a05af2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2019
ms.locfileid: "68833332"
---
# <a name="an-introduction-to-nuget"></a>Eine Einführung in NuGet

Ein unverzichtbares Tool für jede moderne Entwicklungsplattform ist ein Mechanismus, durch den Entwickler nützlichen Code erstellen, freigeben und verwenden können. Solch ein Code wird oft in „Paketen“ gebündelt, in denen kompilierter Code (z.B. DLLs) zusammen mit anderen Inhalten enthalten ist, die in Projekten benötigt werden, die diese Pakete nutzen.

Für .NET (einschließlich .NET Core) ist der von Microsoft unterstützte Mechanismus zur Freigabe von Code **NuGet**. NuGet definiert, wie Pakete für .NET erstellt, gehostet und verarbeitet werden, und [stellt die Tools für jede dieser Aufgaben bereit](install-nuget-client-tools.md).

Einfach gesagt: ein NuGet-Paket ist eine einzelne ZIP-Datei mit der Erweiterung `.nupkg`, die kompilierten Code (DLLs), andere Dateien im Zusammenhang mit diesem Code und ein beschreibendes Manifest enthält, in dem Informationen wie die Versionsnummer des Pakets enthalten sind. Entwickler, die Code teilen wollen, erstellen und veröffentlichen Pakete auf einem öffentlichen oder privaten Host. Paketverbraucher erhalten diese Pakete über entsprechende Hosts, fügen diese ihren Projekten hinzu und rufen dann die Funktionalität eines Pakets in ihrem Projektcode auf. NuGet selbst verarbeitet dann alle Zwischendetails.

Da NuGet neben dem öffentlichen Host „nuget.org“ auch private Hosts unterstützt, können Sie NuGet-Pakete verwenden, um Code zu teilen, der ausschließlich für eine Organisation oder eine Arbeitsgruppe zur Verfügung steht. Sie können NuGet-Pakete auch als einfache Möglichkeit verwenden, um Ihren eigenen Code nur in Ihre eigenen Projekte einzubinden. Kurz gesagt: Ein NuGet-Paket ist eine teilbare Codeeinheit, die eine bestimmte Art und Weise der Freigabe weder benötigt noch vorgibt.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Der Paketfluss zwischen Erstellern, Hosts und Benutzer

In seiner Rolle als öffentlicher Host verwaltet NuGet selbst das zentrale Repository von über 100.000 eindeutigen Paketen auf [nuget.org](https://www.nuget.org). Diese Pakete werden täglich von Millionen von .NET/.NET Core-Entwicklern verwendet. Mit NuGet können Sie auch Pakete privat in der Cloud (z.B. Azure DevOps), in einem privaten Netzwerk oder sogar nur auf Ihrem lokalen Dateisystem hosten. Auf diese Weise stehen diese Pakete nur den Entwicklern zur Verfügung, die Zugriff auf den Host haben, wodurch Sie die Möglichkeit haben, Pakete für eine bestimmte Gruppe von Anwendern verfügbar zu machen. Die Optionen werden in [Hosting your own NuGet feeds (Hosten Ihrer eigenen NuGet-Feeds)](hosting-packages/overview.md) erläutert. Durch Konfigurationsoptionen können Sie auch steuern, auf welchen Host von einem Computer zugegriffen werden kann, wodurch sichergestellt wird, dass Pakete von bestimmten Quellen abgerufen werden, anstelle von öffentlichen Repositorys wie nuget.org.

Ein beliebiger Host dient als Verbindungspunkt zwischen *Paketerstellern* und *Paketverbrauchern*. Ersteller erstellen nützliche NuGet-Pakete und veröffentlichen Sie auf einem Host. Benutzer suchen dann nach nützlichen und kompatiblen Paketen auf zugänglichen Hosts, laden diese Pakete herunter und schließen sie in Ihre Projekte ein. Nach der Installation in einem Projekt sind die Paket-APIs für den restlichen Projektcode verfügbar.

![Beziehung zwischen Paketerstellern, Pakethosts und Paketbenutzer](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>Paket mit Zielkompatibilität

Ein „kompatibles“ Paket bedeutet, dass es Assemblys enthält, die für mindestens ein .NET-Zielframework erstellt wurden, das mit dem Zielframework des nutzenden Projekts kompatibel ist. Entwickler können Pakete erstellen, die spezifisch auf ein Framework ausgelegt sind, wie bei UWP-Steuerelementen, oder sie unterstützen eine größere Anzahl von Zielen. Entwickler legen [.NET Standard](/dotnet/standard/net-standard) als Ziel fest, da es von allen .NET- und .NET Core-Projekten verwendet werden kann, um die Kompatibilität eines Pakets zu maximieren. Dies ist die effizienteste Methode für Ersteller und Verbraucher, da ein einzelnes Paket (das in der Regel nur eine einzelne Assembly enthält) für alle verarbeitenden Projekte funktioniert.

Im Gegensatz dazu erstellen Paketentwickler, die APIs außerhalb von .NET Standard verwenden, separate Assemblys für verschiedene Zielframeworks, die sie unterstützen wollen, und schließen all diese Assemblys in das gleiche Paket mit ein (auch bekannt als „Festlegung von mehreren Zielversionen“). Wenn ein Verbraucher ein solches Paket installiert, extrahiert NuGet nur die Assemblys, die vom Projekt benötigt werden. Dadurch wird der Speicherbedarf des Pakets in der fertigen Anwendung bzw. in den vom Projekt erzeugten Assemblys gesenkt. Es ist für den Ersteller aufwendiger, ein Paket mit mehreren Zielversionen auf dem neuesten Stand zu halten.

> [!Note]
> Die Zielsetzung von .NET Standard ersetzt den vorherigen Ansatz, verschiedene portable Klassenbibliotheken (PCL) als Ziele zu verwenden. Deshalb liegt in dieser Dokumentation der Schwerpunkt auf dem Erstellen von Paketen für .NET Standard.

## <a name="nuget-tools"></a>NuGet-Tools

Zusätzlich zur Unterstützung für das Hosting bietet NuGet außerdem eine Vielzahl von Tools, die vom Ersteller und Benutzer verwendet werden. Informationen dazu, wie Sie bestimmte Tools erhalten, finden Sie unter [Installieren von NuGet-Clienttools](install-nuget-client-tools.md).

| Tool | Plattformen | Anwendbare Szenarios | BESCHREIBUNG |
| --- | --- | --- | --- |
| [dotnet-CLI](consume-packages/install-use-packages-dotnet-cli.md) | Alle | Erstellung, Verbrauch | CLI-Tool für .NET Core- und .NET Standard-Bibliotheken und für Projekte im SDK-Stil für .NET Framework (Informationen finden Sie unter [SDK-Attribut](/dotnet/core/tools/csproj#additions)). Stellt bestimmte NuGet-CLI-Funktionen direkt in der .NET Core-Toolkette bereit. Ähnlich wie `nuget.exe`-CLI interagiert die dotnet-CLI nicht mit Visual Studio-Projekten. |
| [nuget.exe-CLI](consume-packages/install-use-packages-nuget-cli.md) | Alle | Erstellung, Verbrauch | CLI-Tool für .NET Framework-Bibliotheken und Nicht-SDK-Projekte, die auf .NET Standard-Bibliotheken abzielen. Bietet alle NuGet-Funktionen, mit einigen Befehlen, die speziell für Paketersteller bestimmt sind, anderen Befehlen, die nur für Benutzer, und wieder anderen, die für beide bestimmt sind. Beispielsweise verwenden Paketersteller den Befehl `nuget pack` zum Erstellen eines Pakets aus verschiedenen Assemblys und zugehörigen Dateien, Paketverbraucher verwenden `nuget install`, um Pakete in einen Projektordner einzubinden, und alle verwenden `nuget config`, um NuGet-Konfigurationsvariablen festzulegen. Als ein plattformunabhängiges Tool interagiert die NuGet-CLI nicht mit Visual Studio-Projekten. |
| [Paket-Manager-Konsole](consume-packages/install-use-packages-powershell.md) | Visual Studio unter Windows | Verbrauch | Stellt [PowerShell-Befehle](reference/Powershell-Reference.md) zum Installieren und Verwalten von Paketen in Visual Studio-Projekten bereit. |
| [Benutzeroberfläche des Paket-Managers](consume-packages/install-use-packages-visual-studio.md) | Visual Studio unter Windows | Verbrauch | Stellt eine einfache zu bedienende Benutzeroberfläche zum Installieren und Verwalten von Paketen in Visual Studio-Projekten bereit. |
| [Manage NuGet UI (Verwalten der NuGet-Benutzeroberfläche)](/visualstudio/mac/nuget-walkthrough) | Visual Studio für Mac | Verbrauch | Stellt eine einfache zu bedienende Benutzeroberfläche zum Installieren und Verwalten von Paketen in Projekten von Visual Studio für Mac bereit. |
| [MSBuild](reference/msbuild-targets.md) | Windows | Erstellung, Verbrauch | Bietet die Möglichkeit zum Erstellen und Wiederherstellen von Paketen, die in einem Projekt direkt über die MSBuild-Toolkette verwendet werden. |

Wie Sie sehen können, sind die NuGet-Tools, mit denen Sie arbeiten, stark davon abhängig, ob Sie Pakete erstellen, verwenden oder veröffentlichen und mit welcher Plattform Sie arbeiten. Paketersteller sind in der Regel auch Benutzer, da sie auf Funktionalität aufbauen, die in anderen NuGet-Paketen vorhanden ist. Und diese Pakete können natürlich wiederum von anderen abhängen.

Weitere Informationen finden Sie unter den Artikeln [Workflow für die Paketerstellung](create-packages/Overview-and-Workflow.md) und [Workflow für die Nutzung von Paketen](consume-packages/Overview-and-Workflow.md).

## <a name="managing-dependencies"></a>Verwalten von Abhängigkeiten

Die Fähigkeit, einfach auf der Arbeit anderer aufbauen zu können, ist eines der stärksten Features eines Paketverwaltungssystems. Dementsprechend ist eine der wichtigsten Aufgaben von NuGet das Verwalten der Abhängigkeitsstruktur bzw. des „Diagramms“ für ein Projekt. Einfach ausgedrückt müssen Sie sich nur mit jenen Paketen selbst befassen, die Sie direkt in einem Projekt verwenden. Wenn irgendeines dieser Pakete selbst andere Pakete verwendet (die wiederum weitere Pakete verwenden können), übernimmt NuGet alle der früheren Abhängigkeiten.

Die folgende Abbildung zeigt ein Projekt, das von fünf Paketen abhängig ist, die wiederum von einer Reihe anderer abhängen.

![Ein Beispiel für ein NuGet-Abhängigkeitsdiagramm für ein .NET-Projekt](media/dependency-graph.png)

Beachten Sie, dass einige Pakete mehrmals im Abhängigkeitsdiagramm angezeigt werden. Beispielsweise gibt es drei verschiedene Benutzer des Pakets B, und jeder Benutzer könnte auch eine andere Version für das Paket (nicht gezeigt) angeben. Dieser Fall tritt häufig auf, insbesondere bei häufig verwendeten Paketen. NuGet übernimmt alle schwierigen Aufgaben, um genau zu bestimmen, welche Version des Pakets B alle Benutzer zufriedenstellt. NuGet führt dies dann für alle anderen Pakete durch, unabhängig davon, wie ausführlich das Abhängigkeitsdiagramm wird.

Weitere Details wie NuGet diesen Dienst ausführt finden Sie unter [Dependency resolution (Abhängigkeitsauflösung)](consume-packages/dependency-resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Nachverfolgungsverweise und Wiederherstellen von Paketen

Da Projekte zwischen Entwicklercomputern, Repositorys für die Quellcodeverwaltung, Buildservern usw. problemlos verschoben werden können, ist es höchst unpraktisch, dass binäre Assemblys von NuGet-Paketen direkt an ein Projekt gebunden bleiben. Wäre das der Fall, wäre jede Kopie des Projekts unnötigerweise vergrößert (und deshalb eine Verschwendung von Speicherplatz in Repositorys zur Quellcodeverwaltung). Es wäre auch schwer, Binärdateien von Paketen auf neuere Versionen zu aktualisieren, da Updates auf alle Kopien des Projekts angewendet werden müssten.

Stattdessen verwaltet NuGet eine einfach Verweisliste der Pakete von denen ein Projekt abhängig ist, einschließlich der Abhängigkeiten der obersten und untersten Ebenen. D.h. wenn Sie ein Paket in ein Projekt von einem Host aus installieren, zeichnet NuGet die Paket-ID und Versionsnummer in der Verweisliste auf. (Wenn ein Paket deinstalliert wird, wird dieses natürlich aus der Liste entfernt.) NuGet bietet dann eine Möglichkeit, auf Anfrage alle Pakete, auf die verwiesen wird, wiederherzustellen, wie im Artikel [Wiederherstellen von Paketen](consume-packages/package-restore.md) beschrieben wird.

![Eine NuGet-Verweisliste wird bei Paketinstallation erstellt und kann zum Wiederherstellen von Paketen an einem anderen Ort verwendet werden.](media/nuget-restore.png)

Mit der Verweisliste kann NuGet anschließend alle Pakete zu einem späteren Zeitpunkt neu installieren &mdash; also *wiederherstellen* &mdash; die von öffentlichen und bzw. oder privaten Hosts stammen. Wenn Sie ein Projekt auf die Quellcodeverwaltung committen oder auf andere Weise freigeben, muss nur die Verweisliste enthalten sein. Es müssen keine Paketbinärdateien eingeschlossen werden (Näheres finden Sie unter [Pakete und Quellcodeverwaltung](consume-packages/packages-and-source-control.md)).

Der Computer, der ein Projekt, z.B. einen Buildserver, erhält, der eine Kopie des Projekts als Teil eines automatisierten Bereitstellungssystems empfängt, fordert NuGet einfach auf, Abhängigkeiten wiederherzustellen, wenn sie benötigt werden. Buildsysteme, wie Azure DevOps, stellen „NuGet restore“-Schritte für exakt diesen Zweck bereit. Auf ähnliche Weise können Entwickler einen Befehl wie `nuget restore` (NuGet-CLI), `dotnet restore` (dotnet-CLI) oder `Install-Package` (Paket-Manager-Konsole) aufrufen, wenn sie eine Kopie eines Projekts erhalten (z.B. beim Kopieren eines Repositorys), um alle benötigten Pakete zu erhalten. Visual Studio seinerseits stellt Pakete beim Erstellen eines Projekts automatisch wieder her (vorausgesetzt, die automatische Wiederherstellung ist aktiviert, wie unter [Paketwiederherstellung](consume-packages/package-restore.md) beschrieben).

Die primäre Rolle von NuGet bei Entwicklern liegt dann klar im Verwalten der Verweisliste für Ihr Projekt und im Bereitstellen der Möglichkeiten, um diese referenzierten Pakete effizient wiederherzustellen (und zu aktualisieren). Die Liste wird in einem von zwei *Paketverwaltungsformaten* verwaltet:

- [PackageReference](consume-packages/package-references-in-project-files.md) (bzw. „Packen von Verweisen in Projektdateien“) | *(NuGet 4.0 und höher)* verwaltet eine Liste der Abhängigkeiten der obersten Ebene eines Projekts direkt in der Projektdatei, damit keine separate Datei benötigt wird. Eine zugehörige Datei, `obj/project.assets.json`, wird dynamisch generiert, um das gesamte Abhängigkeitsdiagramm der von einem Projekt verwendeten Pakete zusammen mit allen untergeordneten Abhängigkeiten zu verwalten. PackageReference wird immer von .NET Core-Projekten verwendet.

- [`packages.config`](reference/packages-config.md): *(NuGet 1.0 und höher)* Eine XML-Datei, die eine flache Liste aller Abhängigkeiten im Projekt, einschließlich der Abhängigkeiten von anderen installierten Paketen, verwaltet. Installierte oder wiederhergestellte Pakete werden in einem `packages`-Ordner gespeichert.

Welches Paketverwaltungsformat in einen Projekt verwendet wird, hängt vom Projekttyp und der verfügbaren Version von NuGet (und bzw. oder Visual Studio) ab. Suchen Sie nach `packages.config` im Projektstamm, nachdem Sie das erste Paket installiert haben, um zu überprüfen, welches Format verwendet wird. Wenn die Datei nicht angezeigt wird, suchen Sie direkt in der Projektdatei nach einem \<PackageReference\>-Element.

Wenn Sie die Wahl haben, wird die Verwendung von PackageReference empfohlen. `packages.config` wird zu Legacyzwecken beibehalten und befindet sich nicht mehr in der aktiven Entwicklung.

> [!Tip]
> Verschiedene `nuget.exe`-CLI-Befehle, wie `nuget install`, fügen das Paket nicht automatisch zur Verweisliste hinzu. Die Liste wird bei der Installation eines Pakets mit dem Visual Studio-Paket-Manager (Benutzeroberfläche oder Konsole) und mit der `dotnet.exe`-CLI aktualisiert.

## <a name="what-else-does-nuget-do"></a>Was macht NuGet außerdem?

Bisher haben Sie folgende Eigenschaften von NuGet kennengelernt:

- NuGet stellt das zentrale nuget.org-Repository mit Unterstützung von privatem Hosting bereit.
- NuGet stellt die Tools zur Verfügung, die Entwickler benötigen, um Pakete zu erstellen, zu veröffentlichen und zu nutzen.
- Besonders wichtig ist: NuGet verwaltet eine Verweisliste der Pakete, die in einem Projekt verwendet werden und verfügt über die Möglichkeit zum Wiederherstellen und Aktualisieren dieser Pakete aus dieser Liste.

Damit diese Prozesse effizient arbeiten, führt NuGet einige Optimierungen im Hintergrund durch. Insbesondere verwaltet NuGet einen Paketcache und einen globalen Paketordner, um die Installation und Neuinstallation zu beschleunigen. Der Cache verhindert das Herunterladen eines Pakets, das bereits auf dem Rechner installiert ist. Der globale Paketordner ermöglicht es mehreren Projekten, das gleiche installierte Paket gemeinsam zu nutzen, wodurch insgesamt der Speicherbedarf von NuGet auf dem Computer verringert wird. Der Cache und der globale Paketordner sind sehr hilfreich, wenn Sie häufig eine größere Anzahl von Paketen wiederherstellen, wie z.B. auf einem Buildserver. Weitere Informationen zu diesen Mechanismen finden Sie unter [Verwalten der globalen Paketordner und Cacheordner](consume-packages/managing-the-global-packages-and-cache-folders.md).

Innerhalb eines individuellen Projekts verwaltet NuGet den gesamten Abhängigkeitsdiagramm, was die Auflösung mehrerer Verweise auf verschiedene Versionen des selben Pakets enthält. Es ist üblich, dass ein Projekt eine Abhängigkeit von ein oder mehreren Paketen annimmt, die über die gleichen Abhängigkeiten verfügen. Einige der nützlichsten Hilfsprogrammpakete auf nuget.org werden von vielen anderen Paketen verwendet. Im gesamten Abhängigkeitsdiagramm, können dann sehr leicht zehn unterschiedliche Verweise auf verschiedene Versionen desselben Pakets vorkommen. NuGet sortiert aus, welche Version von allen Verbrauchern verwendet werden kann, um zu verhindern, dass mehrere Versionen eines Pakets in die Anwendung selbst platziert werden. (Weitere Informationen finden Sie unter [Auflösung von Abhängigkeiten](consume-packages/dependency-resolution.md).)

Darüber hinaus behält NuGet alle Spezifikationen im Zusammenhang mit der Struktur von Paketen (einschließlich [Lokalisierung](create-packages/creating-localized-packages.md) und [Debugsymbole](create-packages/symbol-packages.md)) und wie auf sie [verwiesen](consume-packages/package-references-in-project-files.md) wird (einschließlich [Versionsbereiche](reference/package-versioning.md#version-ranges-and-wildcards) und [Vorabversionen](create-packages/prerelease-packages.md)) bei. NuGet stellt auch verschiedene APIs für die programmgesteuerte Arbeit mit seinen Diensten bereit und unterstützt Entwickler, die Visual Studio-Erweiterungen und Projektvorlagen.

Im Inhaltsverzeichnis dieser Dokumentation finden Sie alle hier dargestellten Funktionen und Versionshinweise, die bis zu den Anfängen von NuGet zurückgehen.

## <a name="comments-contributions-and-issues"></a>Kommentare, Beiträge und Probleme

Abschließend, freuen wir uns auf Kommentare und Beiträge zu dieser Dokumentation &mdash; klicken Sie einfach auf die Befehle **Feedback** und **Bearbeiten** auf einer beliebigen Seite, oder besuchen Sie das [docs-repository](https://github.com/NuGet/docs.microsoft.com-nuget/) oder die [docs issue list (docs-Problemliste)](https://github.com/NuGet/docs.microsoft.com-nuget/issues) auf GitHub.

Wir freuen uns auch über Beiträge zu NuGet selbst über seine [verschiedenen GitHub-Repositorys](https://github.com/NuGet/Home). NuGet-Probleme finden Sie auf [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues).

Viel Vergnügen mit NuGet!
