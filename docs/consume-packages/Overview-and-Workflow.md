---
title: 'Verwenden von NuGet-Paketen: Übersicht und Workflow'
description: Eine Übersicht über das Nutzen von NuGet-Paketen in einem Projekt, die Links zu anderen spezifischen Teilen des Prozesses enthält.
author: karann-msft
ms.author: karann
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: 4cfc2fde08b240288851b87a391dc42c1ac8ecaf
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842321"
---
# <a name="package-consumption-workflow"></a>Workflow der Nutzung von Paketen

Zwischen nuget.org und privaten Katalogen für Pakete, die Ihre Organisation möglicherweise erstellt, können Sie eine Vielzahl von nützlichen Paketen finden, die Sie für Ihre Apps und Dienste verwenden können. Unabhängig von der Quelle folgt die Nutzung eines Pakets demselben allgemeinen Workflow.

![Workflow: zur Quelle eines Pakets navigieren, ein Paket suchen, ein Paket in einem Projekt installiert, die using-Anweisung und Aufrufe der Paket-API hinzufügen](media/Overview-01-GeneralFlow.png)

\* _Nur Visual Studio und `dotnet.exe`. Der `nuget install`-Installationsbefehl ändert keine Projektdateien oder `packages.config`-Dateien. Die Einträge müssen manuell verwaltet werden._

Weitere Informationen finden Sie unter [Suchen und Auswählen von Paketen](../consume-packages/finding-and-choosing-packages.md) und [Was geschieht bei der Paketinstallation?](../concepts/package-installation-process.md).

NuGet speichert die Identität und Versionsnummer jedes installierten Pakets entweder in der Projektdatei (unter Verwendung von [PackageReference](../consume-packages/package-references-in-project-files.md)) oder in [`packages.config`](../reference/packages-config.md), abhängig vom Projekttyp und Ihrer NuGet-Version. Mit NuGet 4.0 und höher wird PackageReference bevorzugt, obwohl dies in Visual Studio über den [Paket-Manager](../tools/package-manager-ui.md) konfigurierbar ist. Sie können in der entsprechenden Datei jederzeit eine vollständige Liste der Abhängigkeiten für Ihr Projekt anzeigen lassen.

> [!Tip]
> Sie müssen die Lizenz für jedes Paket überprüfen, das Sie in Ihrer Software verwenden möchten. Auf nuget.org finden Sie auf der rechten Seite der Beschreibungsseite jedes Pakets den Link **License Info** (Lizenzinformationen). Wenn ein Paket keine Lizenzbedingungen angibt, kontaktieren Sie den Paketbesitzer direkt, indem Sie den Link **Contact owners** (Besitzer kontaktieren) auf der Seite für Pakete verwenden. Microsoft lizenziert kein geistiges Eigentum von Drittanbietern für Pakete und ist nicht verantwortlich für die durch Drittanbieter bereitgestellten Inhalte.

Bei der Installation eines Pakets überprüft NuGet üblicherweise, ob das Paket bereits aus seinem Cache verfügbar ist. Sie können diesen Cache manuell über die Befehlszeile löschen. Dieser Vorgang wird unter [Managing the NuGet cache (Verwalten des NuGet-Caches)](../consume-packages/managing-the-global-packages-and-cache-folders.md) beschrieben.

NuGet stellt ebenfalls sicher, dass die vom Paket unterstützten Zielframeworks mit Ihrem Projekt kompatibel sind. Wenn das Paket keine kompatiblen Assemblys enthält, zeigt NuGet eine Fehlermeldung an. Weitere Informationen dazu finden Sie unter [Resolving incompatible package errors (Beheben von Fehlern mit inkompatiblen Paketen)](dependency-resolution.md#resolving-incompatible-package-errors).

Wenn Sie Projektcode zu einem Quellrepository hinzufügen, schließen Sie üblicherweise keine NuGet-Pakete ein. Personen, die später ein Repository klonen oder auf andere Weise das Projekt erhalten, das Build-Agents auf Systemen wie Visual Studio Team Services enthält, müssen die erforderlichen Pakete wiederherstellen, bevor ein Build ausgeführt wird:

![Workflow: NuGet-Pakete wiederherstellen, indem ein Repository geklont wird oder durch Verwenden des restore-Befehls](media/Overview-02-RestoreFlow.png)

Die [Paketwiederherstellung](../consume-packages/package-restore.md) verwendet die in der Projektdatei oder `packages.config` enthaltenen Informationen, um alle Abhängigkeiten erneut zu installieren. Beachten Sie, dass es wie in [Abhängigkeitsauflösungen](../consume-packages/dependency-resolution.md) beschrieben Unterschiede zwischen den beteiligten Prozessen gibt. Im obigen Diagramm ist kein Wiederherstellungsbefehl für die Paket-Manager-Konsole enthalten, da Sie sich mit der Konsole bereits im Kontext von Visual Studio befinden. Dort werden Pakete normalerweise automatisch wiederherstellt, und der Befehl ist wie im Folgenden veranschaulicht auf Projektmappenebene verfügbar.

Gelegentlich ist es erforderlich, Pakete erneut zu installieren, die bereits in einem Projekt enthalten sind. Dadurch können auch Abhängigkeiten erneut installiert werden. Dazu können Sie einfach den Befehl `nuget reinstall` oder die NuGet-Paket-Manager-Konsole verwenden. Weitere Informationen finden Sie unter [Reinstalling and Updating Packages (Erneutes Installieren und Aktualisieren von Paketen)](../consume-packages/reinstalling-and-updating-packages.md).

Das Verhalten von NuGet wird von den `Nuget.Config`-Dateien gesteuert. Mehrere Dateien können zum Zentralisieren von bestimmten Eigenschaften auf verschiedenen Ebenen verwendet werden. Weitere Informationen dazu finden Sie unter [Configuring NuGet Behavior (Konfigurieren des NuGet-Verhaltens)](../consume-packages/configuring-nuget-behavior.md).

## <a name="ways-to-install-a-nuget-package"></a>Möglichkeiten zum Installieren eines NuGet-Pakets

NuGet-Pakete werden über eine beliebige der Methoden heruntergeladen und installiert, die in der folgenden Tabelle beschrieben werden.

| Tool | BESCHREIBUNG |
| --- | --- |
| [dotnet.exe-CLI](install-use-packages-dotnet-cli.md) | (Alle Plattformen) CLI-Tool für .NET Core- und .NET Standard-Bibliotheken und für Projekte im SDK-Stil für .NET Framework (siehe [SDK-Attribut](/dotnet/core/tools/csproj#additions)). Ruft das über \<package_name\> angegebene Paket ab und fügt einen Verweis in die Projektdatei ein. Ruft auch Abhängigkeiten ab und installiert sie. |
| Visual Studio | (Windows und Mac) Bietet eine Benutzeroberfläche, über die Sie die Liste der Pakete durchsuchen, Pakete auswählen und diese Pakete und ihre Abhängigkeiten in ein Projekt aus einer angegebenen Paketquelle installieren können. Fügt der Projektdatei Verweise auf installierte Pakete zu.<ul><li>[Installieren und Verwalten von Paketen mit Visual Studio](../tools/package-manager-ui.md)</li><li>[Einschließen eines NuGet-Pakets in Ihr Projekt (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| [Paket-Manager-Konsole in Visual Studio](../tools/package-manager-console.md) | (Nur Windows) Ruft das Paket ab, das durch \<package_name\> identifiziert wurde, und installiert es aus einer ausgewählten Quelle in ein angegebenes Projekt in der Projektmappe und fügt dann einen Verweis zur Projektdatei hinzu. Ruft auch Abhängigkeiten ab und installiert sie. |
| [nuget.exe-CLI](install-use-packages-dotnet-cli.md) | (Alle Plattformen) CLI-Tool für .NET Framework-Bibliotheken und Nicht-SDK-Projekte, die auf .NET Standard-Bibliotheken abzielen. Ruft das über \<package_name\> angegebene Paket ab und entpackt seine Inhalte in einem Ordner im aktuellen Verzeichnis. Kann auch alle Pakete abrufen, die in einer `packages.config`-Datei aufgelistet sind. Ruft außerdem Abhängigkeiten ab und installiert sie, nimmt aber keine Änderungen an Projektdateien oder `packages.config` vor. |
