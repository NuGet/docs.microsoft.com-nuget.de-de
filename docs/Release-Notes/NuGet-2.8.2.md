---
title: NuGet-2.8.2-Versionshinweise | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: bb547f5d-3c0e-4721-b2c7-3fc7e09c34de
description: "Versionshinweise für NuGet 2.8.2 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-2.8.2 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 221b8970663ca80a986fc3ee542b99971c5e2018
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-282-release-notes"></a>NuGet-2.8.2-Versionshinweise

[Anmerkungen zur Version des NuGet-2.8.1](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3-Versionshinweise](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 wurde am 22. Mai 2014 veröffentlicht.  Dieser Version enthalten nur Änderungen an der Befehlszeile nuget.exe, das Paket NuGet.Server in und andere NuGet-Pakete.  Die Version nicht aktualisierte Visual Studio-Erweiterung oder WebMatrix-Erweiterung enthalten.

## <a name="notable-updates"></a>Wichtige Updates

Die wichtigste Updates wurden in der Befehlszeile nuget.exe und NuGet.Server in Pakets (für selbst gehostete NuGet-Feeds).

### <a name="important-nugetexe-bug-fixes"></a>Wichtige nuget.exe Fehlerkorrekturen

1. [NuGet.exe Push schlägt fehl, und hält, und wiederholen Sie dann](https://nuget.codeplex.com/workitem/4000)
1. [NuGet.exe Push keine Anmeldeinformationen für Standardauthentifizierung ordnungsgemäß gesendet](https://nuget.codeplex.com/workitem/4109)
1. [NuGet.exe Push wird nicht temporäre Umleitung folgen.](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Fehlerbehebung für wichtige NuGet.Server in

1. [Falscher Wert für IsAbsoluteLatestVersion zurückgegebenes NuGet.Server in](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Pakete aktualisiert

Die nuget.exe Befehlszeilen und NuGet.Server in Updates werden als NuGet-Paket-Updates zur Verfügung gestellt.  Andere Pakete mit 2.8.2 ebenfalls aktualisiert wurden.

So sieht die Liste der aktualisierten Pakete aus:

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server in](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (das Paket, nicht die Erweiterung)

## <a name="all-changes"></a>Alle Änderungen
Es gab 10 Probleme, die in der Version behoben. Eine vollständige Liste der Arbeit Artikel feste in NuGet 2.8.2, bitte Ansicht der [NuGet Issue Tracker für diese Version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
