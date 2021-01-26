---
title: Nuget 3.4.4 Anmerkungen zu dieser Version
description: Anmerkungen zu dieser Version von nuget 3.4.4 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780230"
---
# <a name="nuget-344-release-notes"></a>Nuget 3.4.4 Anmerkungen zu dieser Version

[Nuget 3.4.3 Anmerkungen](../release-notes/nuget-3.4.3.md)  |  zu dieser Version [Anmerkungen zu dieser Version von nuget 3,5-Beta Version](../release-notes/nuget-3.5-Beta.md)

Der Hauptschwerpunkt dieser Version bestand darin, die Qualität der 3.4.3-Version von nuget.exe mit einigen wenigen Korrekturen an der Visual Studio-Erweiterung zu verbessern.

Sie können die vsix-Datei und die-nuget.exe [hier](https://dist.nuget.org/index.html)herunterladen.

## <a name="344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Vollständiges Änderungsprotokoll](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Liste der Probleme](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Änderungen

- Pack-Verbesserungen: Verbesserungen beim Packen von Symbolen, Verpacken mit `project.json` und mehr [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606)
- Ausnahme anzeigen, wenn beim Suchen nach Projekten im Update-Befehl [605] ein Fehler auftritt. \#https://github.com/NuGet/NuGet.Client/pull/605
- Lesen des Pakettyps aus der Eingabe `.nuspec` und `project.json` beim Verpacken von [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)
- Erstellen Sie "nuget. Shared" nicht als Projekt. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Pushtimeout als HTTP-Antwort Timeout [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599) verwenden
- Für Paketdateien mit zukünftigen Zeiten wird die Zeit nicht verwendet [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)
- Aktualisieren der `NuGet.Core.dll` Version auf 2.12.0, um das XML-Problem [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594) zu beheben
- Support./NuGet.commandline.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)
- Fehler beim Wiederherstellen ohne `project.json` oder `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590) anzeigen
- Beheben von Abhängigkeits Versionen, wenn die erforderlichen Versionen [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)