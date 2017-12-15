---
title: Anmerkungen zur Version des NuGet-1.6 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ed433790-99bf-4b71-92a8-17314bd49867
description: "Versionshinweise für NuGet 1.6 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-1.6 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7824d62cb73c54205175ec742cfc26d1ca3aa741
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
 # <a name="nuget-16-release-notes"></a>1.6 NuGet-Versionshinweise

[Anmerkungen zur Version des NuGet-1.5](../release-notes/nuget-1.5.md) | [NuGet 1.7-Versionshinweise](../release-notes/nuget-1.7.md)

NuGet-1.6 wurde 13 Dezember 2011 veröffentlicht.

## <a name="known-installation-issue"></a>Bekannte Problem
Wenn Sie Visual Studio 2010 SP1 ausführen, kann ein Installationsfehler auftreten beim Upgrade von NuGet ausführen, wenn Sie eine ältere Version installiert haben.

Die problemumgehung besteht darin, einfach NuGet deinstallieren und installieren Sie es aus dem Katalog der VS-Erweiterung.  Finden Sie unter [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) für Weitere Informationen.

Hinweis: Wenn Visual Studio lässt Sie beim Deinstallieren der Erweiterung (die Schaltfläche "Deinstallieren" deaktiviert ist), müssen Sie wahrscheinlich zum Neustart von Visual Studio, die mit "Als Administrator ausführen".

## <a name="features"></a>Features

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Unterstützung für semantische Versionsverwaltung und Vorabversionen von Paketen
NuGet-1.6 wird Unterstützung für semantische Versionsverwaltung (SemVer) eingeführt. Weitere Informationen dazu, wie sie SemVer verwendet, finden Sie unter der [Versionsverwaltung Dokumentation](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Mithilfe von NuGet ohne Überprüfung der In Paketen (Paketwiederherstellung)
NuGet-1.6 hat jetzt erstklassige Unterstützung für den Workflow, in welche, den, den NuGet Pakete werden nicht zur quellcodeverwaltung hinzugefügt, stattdessen werden jedoch wiederhergestellt zur Buildzeit sofern noch nicht vorhanden. Weitere Informationen finden Sie unter der [NuGet verwenden, ohne dass Pakete, Datenquellen-Steuerelements](../consume-packages/packages-and-source-control.md) Thema.

### <a name="item-templates-that-install-nuget-packages"></a>Elementvorlagen, die NuGet-Pakete installieren
Erstellen auf der Arbeit vorinstallierte NuGet-Paket zu Visual Studio-Projektvorlagen unterstützen, fügt 1.6 NuGet-Unterstützung für Visual Studio-Elementvorlagen. Elementvorlagen können NuGet-Pakete zugeordnet, die installiert werden, wenn die Vorlage in aufgerufen.

Details dazu, wie ein Projektelement/Vorlage zum Installieren von NuGet-Pakete zu ändern, finden Sie unter der [Pakete in Visual Studio-Vorlagen](../visual-studio-extensibility/visual-studio-templates.md) Thema.

### <a name="support-for-disabling-package-sources"></a>Unterstützung für Paketquellen deaktivieren
Wenn mehrere Paketquellen konfiguriert sind, sieht NuGet während der Installation eines Paketes und seiner Abhängigkeiten in jeder Kategorie für Pakete. Eine Paketquelle, die für Sie aus irgendeinem Grund eine schwerwiegende Beschädigung NuGet verlangsamt kann nicht ausgeführt wird.

Vor dem NuGet-1.6 könnten Sie die Paketquelle entfernen, müssen dann aber zu merken, wieder die Details für, wenn Sie ihn hinzufügen möchten.

NuGet-1.6 ermöglicht eine Paketquelle zum deaktivieren, halten Sie es aber deaktivieren.

![Deaktivieren ein Paket](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Fehlerkorrekturen
NuGet-1.6 mussten insgesamt 106 Arbeitsaufgaben behoben. 95 dieser wurden als Fehler eingestuft, und 10 dieser Waren Funktionen.

Eine vollständige Liste der Arbeit Elemente in behoben NuGet 1.6, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
