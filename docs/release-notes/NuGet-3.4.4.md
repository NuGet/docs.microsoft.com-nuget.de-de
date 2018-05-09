---
title: Anmerkungen zur Version von NuGet 3.4.4
description: Versionshinweise für NuGet 3.4.4 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 891d5c7ee884d31f405118739b57a169b9cd93b3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-344-release-notes"></a>Anmerkungen zur Version von NuGet 3.4.4

[Anmerkungen zur Version des NuGet-3.4.3](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 Beta-Versionshinweise](../release-notes/nuget-3.5-Beta.md)

Der Schwerpunkt dieser Version wurde verbessert die Qualität der 3.4.3-Versionen nuget.exe mit wenigen Korrekturen, die Visual Studio-Erweiterung.

Sie können sowohl VSIX-als auch nuget.exe herunterladen [hier](https://dist.nuget.org/index.html).

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Vollständige Änderungsprotokoll](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Liste der Probleme](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Änderungen

- Pack-Verbesserungen: Verbesserungen zum Packen von Symbolen mit Packen `project.json` und weitere [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- Ausnahme angezeigt wird, wenn Fehler beim Suchen von Projekten in der Update-Befehl [\#605] ()https://github.com/NuGet/NuGet.Client/pull/605
- Eingabe Pakettyp auslesen `.nuspec` und `project.json` beim Packen [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- Stellen Sie NuGet.Shared nicht in einem Projekt. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Verwenden Sie das Push-Timeout als das HTTP-Antwort-Timeout [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- Paketdateien mit zukünftigen Uhrzeiten keine sich die Zeiten verwendet [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- Aktualisieren von `NuGet.Core.dll` Version 2.12.0 XML-Problems [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- ./NuGet.CommandLine.XPlat - V unterstützt \<Ausführlichkeit\> \<Modus\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- Anzeige Fehler wiederherstellen, ohne `project.json` oder `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- Abhängigkeit Versionen behoben, wenn sich die erforderliche Versionen unterscheiden [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)