---
title: "Verwenden von NuGet-Paketen: Übersicht und Workflow | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Eine Übersicht über das Nutzen von NuGet-Paketen in einem Projekt, die Links zu anderen spezifischen Teilen des Prozesses enthält."
keywords: "Nutzung von NuGet-Paketen, Übersicht über die Nutzung von NuGet-Paketen, Workflow der Nutzung von NuGet-Paketen, Workflow der Nutzung von Paketen, Übersicht über die Nutzung von Paketen"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 731e0d3eb4ccb887624e4e46a18b4cc77857a784
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="package-consumption-workflow"></a>Workflow der Nutzung von Paketen

Zwischen nuget.org und privaten Katalogen für Pakete, die Ihre Organisation möglicherweise erstellt, können Sie eine Vielzahl von nützlichen Paketen finden, die Sie für Ihre Apps und Dienste verwenden können. Unabhängig von der Quelle folgt die Nutzung eines Pakets dem im Folgenden dargestellten allgemeinen Workflow. Weitere Informationen finden Sie unter [Suchen und Auswerten von Paketen](../consume-packages/finding-and-choosing-packages.md) und [Verschiedene Möglichkeiten zum Installieren von NuGet-Paketen](ways-to-install-a-package.md).

![Workflow: zur Quelle eines Pakets navigieren, ein Paket suchen, ein Paket in einem Projekt installiert, die using-Anweisung und Aufrufe der Paket-API hinzufügen](media/Overview-01-GeneralFlow.png)

\*  _Außer `nuget install` wird über die Befehlszeile aufgerufen. In diesem Fall müssen die Konfigurationsdateien manuell bearbeitet werden. Weitere Informationen finden Sie unter [install command reference (Referenz zum install-Befehl)](../tools/cli-ref-install.md)._

NuGet speichert die Identität und die Versionsnummer jedes installierten Pakets. Diese werden je nach Projekttyp und NuGet-Version entweder in [`packages.config`](../reference/packages-config.md) oder der Projektdatei aufgezeichnet. Bei NuGet 4.0 und höher ist das [Speichern von Abhängigkeiten in der Projektdatei oder in PackageReference](../consume-packages/package-references-in-project-files.md) in der Regel die Standardeinstellung. Dies ist in Visual Studio jedoch über die [Optionen der Paket-Manager-Benutzeroberfläche](../tools/package-manager-ui.md) konfigurierbar. Sie können in der entsprechenden Datei jederzeit eine vollständige Liste der Abhängigkeiten für Ihr Projekt anzeigen lassen.

> [!Tip]
> Sie müssen die Lizenz für jedes Paket überprüfen, das Sie in Ihrer Software verwenden möchten. Auf nuget.org finden Sie auf der rechten Seite der Beschreibungsseite jedes Pakets den Link **License Info** (Lizenzinformationen). Wenn ein Paket keine Lizenzbedingungen angibt, kontaktieren Sie den Paketbesitzer direkt, indem Sie den Link **Contact owners** (Besitzer kontaktieren) auf der Seite für Pakete verwenden. Microsoft lizenziert kein geistiges Eigentum von Drittanbietern für Pakete und ist nicht verantwortlich für die durch Drittanbieter bereitgestellten Inhalte.

Bei der Installation eines Pakets überprüft NuGet üblicherweise, ob das Paket bereits aus seinem Cache verfügbar ist. Sie können diesen Cache manuell über die Befehlszeile löschen. Dieser Vorgang wird unter [Managing the NuGet cache (Verwalten des NuGet-Caches)](../consume-packages/managing-the-nuget-cache.md) beschrieben.

NuGet stellt ebenfalls sicher, dass die vom Paket unterstützten Zielframeworks mit Ihrem Projekt kompatibel sind. Wenn das Paket keine kompatiblen Assemblys enthält, gibt NuGet eine Fehlermeldung aus. Weitere Informationen dazu finden Sie unter [Resolving incompatible package errors (Beheben von Fehlern mit inkompatiblen Paketen)](dependency-resolution.md#resolving-incompatible-package-errors).

Wenn Sie Projektcode zu einem Quellrepository hinzufügen, schließen Sie üblicherweise keine NuGet-Pakete ein. Personen, die später ein Repository klonen, das Build-Agents auf Systemen wie Visual Studio Team Services enthält, müssen die erforderlichen Pakete wiederherstellen, bevor ein Build ausgeführt wird:

![Workflow: NuGet-Pakete wiederherstellen, indem ein Repository geklont wird oder durch Verwenden des restore-Befehls](media/Overview-02-RestoreFlow.png)

Die [Paketwiederherstellung](../consume-packages/package-restore.md) verwendet die in der Projektdatei oder `packages.config` enthaltenen Informationen, um alle Abhängigkeiten erneut zu installieren. Beachten Sie, dass es wie in [Abhängigkeitsauflösungen](../consume-packages/dependency-resolution.md) beschrieben Unterschiede zwischen den beteiligten Prozessen gibt.

Gelegentlich ist es erforderlich, Pakete erneut zu installieren, die bereits in einem Projekt enthalten sind. Dadurch können auch Abhängigkeiten erneut installiert werden. Dazu können Sie einfach den Befehl `reinstall` über die NuGet-Befehlszeile oder über die Konsole des NuGet-Paket-Managers verwenden. Weitere Informationen finden Sie unter [Reinstalling and Updating Packages (Erneutes Installieren und Aktualisieren von Paketen)](../consume-packages/reinstalling-and-updating-packages.md).

Das Verhalten von NuGet wird von den `Nuget.Config`-Konfigurationsdateien gesteuert. Mehrere Dateien können zum Zentralisieren von bestimmten Eigenschaften auf verschiedenen Ebenen verwendet werden. Weitere Informationen dazu finden Sie unter [Configuring NuGet Behavior (Konfigurieren des NuGet-Verhaltens)](../consume-packages/configuring-nuget-behavior.md).

Nutzen Sie NuGet-Pakete, um produktiv zu programmieren.
