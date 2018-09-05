---
title: Anmerkungen zu NuGet-Version 1.6
description: Anmerkungen zu NuGet-1.6, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549011"
---
 # <a name="nuget-16-release-notes"></a>Anmerkungen zu NuGet-Version 1.6

[Anmerkungen zu NuGet 1.5](../release-notes/nuget-1.5.md) | [Anmerkungen zu NuGet 1.7](../release-notes/nuget-1.7.md)

NuGet-1.6 wurde am 13 Dezember 2011 veröffentlicht.

## <a name="known-installation-issue"></a>Problem für bekannte Installationsprobleme
Wenn Sie Visual Studio 2010 SP1 ausführen, können Sie ein Installationsfehler auftreten, beim Versuch, NuGet aktualisieren, wenn Sie eine ältere Version installiert haben.

Die problemumgehung besteht darin, einfach NuGet zuerst deinstallieren und installieren Sie es aus dem Katalog der VS-Erweiterung.  Weitere Informationen finden Sie unter [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

Hinweis: Wenn Visual Studio ist es nicht zulässig, die die Erweiterung deinstallieren (die Schaltfläche "Deinstallieren" deaktiviert ist), müssen Sie wahrscheinlich zum Neustart von Visual Studio mithilfe von "Ausführen als Administrator."

## <a name="features"></a>Features

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Unterstützung für semantische Versionierung und Vorabversionen von Paketen
NuGet-1.6 führt die Unterstützung für semantische Versionskontrolle (SemVer). Lesen Sie weitere Informationen dazu, wie sie SemVer verwendet die [Versionsverwaltung Dokumentation](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Verwenden von NuGet ohne das Einchecken von Paketen (Paketwiederherstellung)
NuGet-1.6 verfügt jetzt über erstklassige Unterstützung für den Workflow, in welche, den, den NuGet Pakete werden in die quellcodeverwaltung nicht hinzugefügt, jedoch stattdessen werden wiederhergestellt zum Zeitpunkt der Erstellung bei fehlen. Weitere Informationen finden Sie in der [mithilfe von NuGet ohne das Übernehmen von Paketen in der quellcodeverwaltung](../consume-packages/packages-and-source-control.md) Thema.

### <a name="item-templates-that-install-nuget-packages"></a>Vorlagen, die NuGet-Pakete installieren
Auf der Arbeit zur Unterstützung von Visual Studio-Projektvorlagen vorinstallierte NuGet-Paket erstellen, fügt NuGet 1.6 auch Unterstützung für Visual Studio-Projektelementvorlagen. Elementvorlagen können NuGet-Paketen zugeordnet, die installiert werden, wenn die Vorlage in aufgerufen.

Weitere Informationen zum Ändern einer Projekt-/Elementvorlage zum Installieren von NuGet-Pakete finden Sie in der [Pakete in Visual Studio-Vorlagen](../visual-studio-extensibility/visual-studio-templates.md) Thema.

### <a name="support-for-disabling-package-sources"></a>Unterstützung zur Deaktivierung von Paketquellen
Wenn mehrerer Paketquellen konfiguriert sind, sucht NuGet jeweils für Pakete während der Installation von einem Paket und seine Abhängigkeiten. Eine Paketquelle, das Sie für aus irgendeinem Grund stark NuGet verlangsamen kann.

Vor dem NuGet-1.6 könnten Sie die Paketquelle entfernen, aber anschließend müssen Sie denken Sie daran, dass die Details für, wenn Sie sie hinzufügen möchten in back.

NuGet-1.6 ermöglicht es, wenn Sie eine Paketquelle zum Halten Sie es aber deaktivieren, deaktivieren.

![Deaktivieren ein Paket](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Fehlerkorrekturen
NuGet-1.6 mussten insgesamt 106 Arbeitsaufgaben behoben. 95 davon wurden als Fehler eingestuft, und 10 dieser wurden die Funktionen.

Eine vollständige Liste der Arbeit Elemente eine feste in NuGet-1.6, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
