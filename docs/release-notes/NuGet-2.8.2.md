---
title: Nuget 2.8.2 Anmerkungen zu dieser Version
description: Anmerkungen zu dieser Version von nuget 2.8.2 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780366"
---
# <a name="nuget-282-release-notes"></a>Nuget 2.8.2 Anmerkungen zu dieser Version

Anmerkungen zu dieser [Version von nuget 2.8.1](../release-notes/nuget-2.8.1.md)  |  [Nuget 2.8.3 Anmerkungen](../release-notes/nuget-2.8.3.md) zu dieser Version

Nuget 2.8.2 wurde am 22. Mai 2014 veröffentlicht.  Diese Version enthielt nur Änderungen an der Befehlszeile nuget.exe, das nuget. Server-Paket und andere nuget-Pakete.  Das Release enthielt keine aktualisierte Visual Studio-Erweiterung oder webmatrix-Erweiterung.

## <a name="notable-updates"></a>Relevante Updates

Die bemerkenswertesten Updates waren in der nuget.exe-Befehlszeile und im nuget. Server-Paket (bei selbstgeh osteten nuget-Feeds).

### <a name="important-nugetexe-bug-fixes"></a>Wichtige nuget.exe Fehlerbehebungen

1. [nuget.exe Push schlägt fehl und führt einen Wiederholungsversuch durch.](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe Push sendet die grundlegenden Authentifizierungs Anmelde Informationen nicht ordnungsgemäß.](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe Push folgt nicht der temporären Umleitung](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Wichtige Fehlerbehebung für nuget. Server

1. [Der von "nuget. Server" zurückgegebene falsche Wert von "isabsolutelatestversion".](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Aktualisierte Pakete

Die nuget.exe-Befehlszeilen-und nuget. Server-Fehlerbehebungen werden als nuget-Paket Aktualisierungen ausgeliefert.  Es wurden auch andere Pakete mit 2.8.2 aktualisiert.

Im folgenden finden Sie die Liste der aktualisierten Pakete:

1. [Nuget. Core](https://www.nuget.org/packages/NuGet.Core/)
1. ["Nuget. CommandLine"](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [Nuget. Build](https://www.nuget.org/packages/NuGet.Build/)
1. [Nuget. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (das Paket, nicht die Erweiterung)

## <a name="all-changes"></a>Alle Änderungen
In der Version wurden 10 Probleme behoben. Eine vollständige Liste der Arbeitselemente, die in nuget-2.8.2 korrigiert sind, finden Sie in der [nuget-Problemverfolgung für diese Version](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
