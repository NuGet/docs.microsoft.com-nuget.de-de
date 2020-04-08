---
title: 'Erstellen von NuGet-Paketen: Übersicht und Workflow'
description: Eine Übersicht über das Erstellen und Veröffentlichen von NuGet-Paketen, die Links zu anderen spezifischen Teilen des Prozesses enthält.
author: karann-msft
ms.author: karann
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: e4b9f6dae3a4be69e523888cc9bd2f212b45829c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488841"
---
# <a name="package-creation-workflow"></a>Workflow für die Paketerstellung

Das Erstellen eines Pakets beginnt mit dem kompilierten Code (üblicherweise .NET-Assemblys), den Sie verpacken und für andere freigeben möchten. Dies kann entweder über den öffentlichen Katalog auf nuget.org oder über einen privaten Katalog innerhalb Ihrer Organisation erfolgen. Das Paket kann ebenfalls zusätzliche Dateien wie z.B. eine Infodatei enthalten, die bei der Installation angezeigt wird, sowie Transformationen von bestimmten Projektdateien.

Ein Paket kann ebenfalls dafür verwendet werden, eine beliebige Anzahl von anderen Abhängigkeiten beziehen, ohne eigenen Code zu enthalten. Ein solches Paket stellt eine einfache Möglichkeit dar, ein SDK zu übermitteln, das aus mehreren unabhängigen Paketen besteht. In anderen Fällen kann ein Paket nur Symboldateien (`.pdb`) enthalten, um das Debuggen zu erleichtern.

> [!Note]
> Wenn Sie ein Paket erstellen, das von anderen Entwicklern verwendet werden soll, beachten Sie, dass diese Abhängigkeiten von Ihrer Arbeit erstellen. Daher bringt das Erstellen und Veröffentlichen eines Pakets ebenfalls die Verpflichtung mit sich, Probleme zu beheben und weitere Updates durchzuführen. Sie sollten jedoch mindestens die Open Source-Verfügbarkeit des Pakets gewährleisten, sodass andere Sie bei der Verwaltung unterstützen können.

Auf jeden Fall werden beim Erstellen eines Pakets zunächst sein Bezeichner, seine Versionsnummer, seine Lizenz, seine Copyrightinformationen und weitere erforderliche Inhalte festgelegt. Anschließend können Sie mit dem Befehl „pack“ alles zusammen in eine `.nupkg`-Datei einfügen. Diese Datei kann in einem NuGet-Feed, z. B. „nuget.org“, veröffentlicht werden.

> [!Tip]
> Bei einem NuGet-Paket mit der `.nupkg`-Erweiterung handelt es sich um eine einfache ZIP-Datei. Ändern Sie die Erweiterung in `.zip`, und erweitern Sie den Inhalt wie gewohnt, um den Inhalt von Paketen zu überprüfen. Stellen Sie jedoch sicher, dass Sie die Erweiterung wieder in `.nupkg` ändern, bevor Sie das Paket bei einem Host hochladen.

Beginnen Sie für grundlegende Informationen zum Erstellungsprozess mit [Creating a package (Erstellen eines Pakets)](../create-packages/creating-a-package.md). Dort werden Sie durch die wichtigsten Prozesse geführt, die für alle Pakete gleich sind.

Danach können Sie viele weitere Optionen für Ihr Paket in Betracht ziehen:

- Im Artikel [Supporting Multiple Target Frameworks (Unterstützen mehrerer Zielframeworks)](../create-packages/supporting-multiple-target-frameworks.md) wird beschrieben, wie Sie ein Paket mit mehreren Varianten für verschiedene .NET-Frameworks erstellen.
- Im Artikel [Creating Localized Packages (Erstellen von lokalisierten Paketen)](../create-packages/creating-localized-packages.md) wird beschrieben, wie Sie ein Paket mit mehreren Sprachressourcen strukturieren und wie Sie separate lokalisierte Satellitenpakete verwenden.
- Im Artikel [Pre-release Packages (Vorabversionen von Paketen)](../create-packages/prerelease-packages.md) wird veranschaulicht, wie Sie Alpha-, -Beta- und rc-Pakete für interessierte Kunden bereitstellen.
- Im Artikel [Source and Config File Transformations (Transformationen von Quell- und Konfigurationsdateien)](../create-packages/source-and-config-file-transformations.md) wird beschrieben, wie Sie unidirektionale Ersetzungen von Tokens in Dateien durchführen, die zu einem Projekt hinzugefügt wurden, und wie Sie `web.config` und `app.config` mit Einstellungen bearbeiten, die bei der Deinstallation des Pakets zurückgesetzt werden.
- Der Artikel [Symbol Packages (Symbolpakete)](../create-packages/symbol-packages-snupkg.md) enthält einen Leitfaden für das Bereitstellen von Symbolen für Ihre Bibliothek, wodurch es Nutzern ermöglicht wird, den Code während des Debuggens schrittweise auszuführen.
- Im Artikel [Package versioning (Paketversionsverwaltung)](../concepts/package-versioning.md) wird erläutert, wie die genauen Versionen identifiziert werden, die Sie für Ihre Abhängigkeiten (andere Pakete, die Sie über Ihr Paket nutzen) zulassen.
- Im Artikel [Native Packages (Native Pakete)](../guides/native-packages.md) wird beschrieben, wie Sie ein Paket für C++-Nutzer erstellen.
- Im Artikel [Signing Packages (Signieren von Paketen)](../create-packages/sign-a-package.md) wird der Vorgang zum Hinzufügen einer digitalen Signatur zu einem Paket beschrieben.

Wenn Sie dazu bereit sind, ein Paket auf nuget.org zu veröffentlichen, befolgen Sie einfach den im Artikel [Publish a package (Veröffentlichen eines Pakets)](../nuget-org/publish-a-package.md) beschriebenen Prozess.

Wenn Sie einen privaten Feed statt nuget.org verwenden möchten, finden Sie weitere Informationen unter [Hosting Packages Overview (Übersicht über das Hosting von Paketen)](../hosting-packages/overview.md).
