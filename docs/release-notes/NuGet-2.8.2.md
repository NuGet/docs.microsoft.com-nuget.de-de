---
title: Anmerkungen zu NuGet 2.8.2
description: Anmerkungen zu dieser Version für die Einbindung von NuGet 2.8.2 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551147"
---
# <a name="nuget-282-release-notes"></a>Anmerkungen zu NuGet 2.8.2

[Anmerkungen zu NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [Anmerkungen zu NuGet 2.8.3](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 wurde am 22. Mai 2014 veröffentlicht.  Dieser Release enthalten nur Änderungen an der Befehlszeile nuget.exe, das Paket "NuGet.Server" und andere NuGet-Pakete.  Die Version es sich nicht um eine aktualisierte Erweiterung für Visual Studio oder WebMatrix-Erweiterung enthalten.

## <a name="notable-updates"></a>Wichtige Updates

Die wichtigsten Updates wurden in der Befehlszeile nuget.exe und das Paket "NuGet.Server" (für selbst gehostete NuGet-Feeds).

### <a name="important-nugetexe-bug-fixes"></a>Wichtige nuget.exe-Fehlerbehebungen

1. [NuGet.exe Push schlägt fehl, und behält die Wiederholung](https://nuget.codeplex.com/workitem/4000)
1. [NuGet.exe Push keine Anmeldeinformationen für Standardauthentifizierung ordnungsgemäß gesendet](https://nuget.codeplex.com/workitem/4109)
1. [NuGet.exe Push wird nicht temporäre Umleitung folgen.](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Programmfehlerbehebung für wichtige "NuGet.Server"

1. [Falscher Wert für "NuGet.Server" zurückgegebenes IsAbsoluteLatestVersion](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Pakete aktualisiert

Die Befehlszeile nuget.exe und "NuGet.Server" Korrekturen werden als NuGet-Paket-Updates ausgeliefert.  Andere Pakete, die mit 2.8.2 auch aktualisiert wurden.

So sieht die Liste der aktualisierten Pakete aus:

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (das Paket, nicht die Erweiterung)

## <a name="all-changes"></a>Alle Änderungen
Es waren 10 in der Release behobenen Problemen. Eine vollständige Liste der Arbeit Elemente eine feste NuGet 2.8.2, bitte Ansicht der [NuGet Issue Tracker für diese Version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
