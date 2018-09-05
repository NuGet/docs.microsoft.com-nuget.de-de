---
title: Anmerkungen zu NuGet 3.4.4
description: Anmerkungen zu dieser Version für die Einbindung von NuGet 3.4.4 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 44a9f21c61f0552fdc21aab24f48eee993654b01
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547472"
---
# <a name="nuget-344-release-notes"></a>Anmerkungen zu NuGet 3.4.4

[Anmerkungen zu NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [Anmerkungen zu NuGet 3.5-Beta](../release-notes/nuget-3.5-Beta.md)

Der primäre Fokus von dieser Version wurde die Verbesserungen bei der die Qualität der 3.4.3 Version von nuget.exe einige Behebungen an sowie die Visual Studio-Erweiterung.

Sie können sowohl VSIX-als auch nuget.exe [hier](https://dist.nuget.org/index.html).

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Vollständigen Änderungsprotokoll](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Liste der Probleme](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Änderungen

- Pack-Verbesserungen: Verbesserungen bei der das Verpacken der Symbole, Packen mit `project.json` mehr [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- Ausnahme angezeigt wird, wenn Fehler beim Suchen von Projekten in der Update-Befehl [\#605](https://github.com/NuGet/NuGet.Client/pull/605)
- Pakettyp aus dem Eingabedatenstrom gelesenen `.nuspec` und `project.json` beim Packen [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- Stellen Sie NuGet.Shared nicht in einem Projekt. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Verwenden Sie das Push-Timeout als das Timeout der HTTP-Antwort [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- Paketdateien mit zukünftigen Zeiten haben sich die Zeiten verwendet keinen [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- Aktualisieren von `NuGet.Core.dll` Version 2.12.0 um XML-Problem zu beheben [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- ./NuGet.CommandLine.XPlat - V unterstützt \<Ausführlichkeit\> \<Modus\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- Anzeigen der Fehler beim Wiederherstellen ohne `project.json` oder `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- Beheben von abhängigkeitsversionen, wenn sich die erforderliche Versionen unterscheiden [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)