---
title: 'Verwenden von NuGet-Paketen: Übersicht und Workflow'
description: Eine Übersicht über das Nutzen von NuGet-Paketen in einem Projekt, die Links zu anderen spezifischen Teilen des Prozesses enthält.
author: karann-msft
ms.author: karann
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: 556683e5a24c57a6c32d8b4e368bfdccd4d19b48
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812860"
---
# <a name="package-consumption-workflow"></a>Workflow der Nutzung von Paketen

Zwischen nuget.org und privaten Katalogen für Pakete, die Ihre Organisation möglicherweise erstellt, können Sie eine Vielzahl von nützlichen Paketen finden, die Sie für Ihre Apps und Dienste verwenden können. Unabhängig von der Quelle folgt die Nutzung eines Pakets demselben allgemeinen Workflow.

![Workflow: zur Quelle eines Pakets navigieren, ein Paket suchen, ein Paket in einem Projekt installiert, die using-Anweisung und Aufrufe der Paket-API hinzufügen](media/Overview-01-GeneralFlow.png)

\* _Nur Visual Studio und `dotnet.exe`. Der `nuget install`-Installationsbefehl ändert keine Projektdateien oder `packages.config`-Dateien. Die Einträge müssen manuell verwaltet werden._

Weitere Informationen finden Sie unter [Suchen und Auswerten von NuGet-Paketen für Ihr Projekt](../consume-packages/finding-and-choosing-packages.md) und [Verschiedene Möglichkeiten zum Installieren von NuGet-Paketen](ways-to-install-a-package.md).

NuGet speichert die Identität und Versionsnummer jedes installierten Pakets entweder in der Projektdatei (unter Verwendung von [PackageReference](../consume-packages/package-references-in-project-files.md)) oder in [`packages.config`](../reference/packages-config.md), abhängig vom Projekttyp und Ihrer NuGet-Version. Mit NuGet 4.0+ wird PackageReference bevorzugt, obwohl dies in Visual Studio über die [Paket-Manager-UI-Optionen](../tools/package-manager-ui.md) konfigurierbar ist. Sie können in der entsprechenden Datei jederzeit eine vollständige Liste der Abhängigkeiten für Ihr Projekt anzeigen lassen.

> [!Tip]
> Sie müssen die Lizenz für jedes Paket überprüfen, das Sie in Ihrer Software verwenden möchten. Auf nuget.org finden Sie auf der rechten Seite der Beschreibungsseite jedes Pakets den Link **License Info** (Lizenzinformationen). Wenn ein Paket keine Lizenzbedingungen angibt, kontaktieren Sie den Paketbesitzer direkt, indem Sie den Link **Contact owners** (Besitzer kontaktieren) auf der Seite für Pakete verwenden. Microsoft lizenziert kein geistiges Eigentum von Drittanbietern für Pakete und ist nicht verantwortlich für die durch Drittanbieter bereitgestellten Inhalte.

Bei der Installation eines Pakets überprüft NuGet üblicherweise, ob das Paket bereits aus seinem Cache verfügbar ist. Sie können diesen Cache manuell über die Befehlszeile löschen. Dieser Vorgang wird unter [Managing the NuGet cache (Verwalten des NuGet-Caches)](../consume-packages/managing-the-global-packages-and-cache-folders.md) beschrieben.

NuGet stellt ebenfalls sicher, dass die vom Paket unterstützten Zielframeworks mit Ihrem Projekt kompatibel sind. Wenn das Paket keine kompatiblen Assemblys enthält, zeigt NuGet eine Fehlermeldung an. Weitere Informationen dazu finden Sie unter [Resolving incompatible package errors (Beheben von Fehlern mit inkompatiblen Paketen)](dependency-resolution.md#resolving-incompatible-package-errors).

Wenn Sie Projektcode zu einem Quellrepository hinzufügen, schließen Sie üblicherweise keine NuGet-Pakete ein. Personen, die später ein Repository klonen oder auf andere Weise das Projekt erhalten, das Build-Agents auf Systemen wie Visual Studio Team Services enthält, müssen die erforderlichen Pakete wiederherstellen, bevor ein Build ausgeführt wird:

![Workflow: NuGet-Pakete wiederherstellen, indem ein Repository geklont wird oder durch Verwenden des restore-Befehls](media/Overview-02-RestoreFlow.png)

Die [Paketwiederherstellung](../consume-packages/package-restore.md) verwendet die in der Projektdatei oder `packages.config` enthaltenen Informationen, um alle Abhängigkeiten erneut zu installieren. Beachten Sie, dass es wie in [Abhängigkeitsauflösungen](../consume-packages/dependency-resolution.md) beschrieben Unterschiede zwischen den beteiligten Prozessen gibt. Im obigen Diagramm ist kein Wiederherstellungsbefehl für die Paket-Manager-Konsole enthalten, da Sie sich mit der Konsole bereits im Kontext von Visual Studio befinden. Dort werden Pakete normalerweise automatisch wiederherstellt, und der Befehl ist wie im Folgenden veranschaulicht auf Projektmappenebene verfügbar.

Gelegentlich ist es erforderlich, Pakete erneut zu installieren, die bereits in einem Projekt enthalten sind. Dadurch können auch Abhängigkeiten erneut installiert werden. Dazu können Sie einfach den Befehl `nuget reinstall` oder die NuGet-Paket-Manager-Konsole verwenden. Weitere Informationen finden Sie unter [Reinstalling and Updating Packages (Erneutes Installieren und Aktualisieren von Paketen)](../consume-packages/reinstalling-and-updating-packages.md).

Das Verhalten von NuGet wird von den `Nuget.Config`-Dateien gesteuert. Mehrere Dateien können zum Zentralisieren von bestimmten Eigenschaften auf verschiedenen Ebenen verwendet werden. Weitere Informationen dazu finden Sie unter [Configuring NuGet Behavior (Konfigurieren des NuGet-Verhaltens)](../consume-packages/configuring-nuget-behavior.md).

Nutzen Sie NuGet-Pakete, um produktiv zu programmieren.
